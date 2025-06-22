# Reset Dev Move

- Enable dev mode + key server
- After 1000 hours = 41 days the dev timer will run out, and since this is dev mode, the youtube app will be uninstalled >:(. To stop that we auto reset the dev timer >:).
- Original script: [https://github.com/webosbrew/dev-utils/blob/main/scripts/devmode-reset.sh](https://github.com/webosbrew/dev-utils/blob/main/scripts/devmode-reset.sh)
- Lets imagine the TVs IP is `10.0.0.40`

<br>

1. Log into a Linux server/router or something. Enter `crontab -e` and click enter. Lets configure update every 19th hour (19:00 = 7pm) on the first, second and third day of the week.
````shell
0 19 * * 1,2,3 /root/update-lg-session-token.sh
````
3. On the server let's create a script in e.g. `/root/` with `nano update-lg-session-token.sh` and add
````shell
#!/bin/sh
SSH_KEYFILE="/root/.ssh/tv_webos"

#Change the IP of your TV here:
TV_HOST=10.0.0.40

sessionToken=$(ssh -i ${SSH_KEYFILE} -o ConnectTimeout=3 -p 9922 prisoner@${TV_HOST} cat /var/luna/preferences/devmode_enabled)
if [ -z "${sessionToken}" ]; then
  sessionToken=$(cat /tmp/webos_devmode_token.txt)
else
  echo "${sessionToken}" >/tmp/webos_devmode_token.txt
fi

if [ -z "${sessionToken}" ]; then
  echo "Unable to get token" >&2
  exit 1
fi

#check the left of time with:
#curl https://developer.lge.com/secure/CheckDevModeSession.dev?sessionToken={your_token}

#Lets reset by changing 'Check' to 'Reset' in the URL below:
#btw add '-s' after curl to make output silent. This would silence output
checkSession=$(curl --max-time 3 "https://developer.lge.com/secure/ResetDevModeSession.dev?sessionToken=${sessionToken}")

echo "$checkSession"
````
Make the script executable
````shell
chmod +x /root/update-lg-session-token.sh
````
Make config file with `nano /root/.ssh/config` or else we might have problem with using ssh into the tv:
````shell
HostkeyAlgorithms +ssh-rsa
PubkeyAcceptedKeyTypes ssh-rsa,ssh-ed25519
````
Lets download the key file from the tv and save it into `/root/.ssh`
````shell
wget -O /root/.ssh/tv_webos http://10.0.0.40:9991/webos_rsa
````
Make both files executable. It is important only root can read these files.
````shell
chmod 600 /root/.ssh/config
chmod 600 /root/.ssh/tv_webos
````
Remove the password protection on `tv_webos` so we can use the key without having to type the password you wrote down from Dev Mode on the TV.
````shell
cd /root/.ssh/
cp tv_webos tv_webos.backup   #always nice to have a backup, even though we can easily donwload it when keyserver is enabled
ssh-keygen -p -f tv_webos
<ENTERYOURPASSWORD>
<enter nothing - just click enter>
<confirm by clicking enter again>

#Expected output
ssh-keygen -p -f tv_webos
Enter old passphrase:
Enter new passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved with the new passphrase.
````


