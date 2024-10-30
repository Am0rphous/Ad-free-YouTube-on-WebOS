# Ad-free YouTube on WebOS
_This information is just a rewrite of information given by user [Cr3z33-71](https://www.reddit.com/r/LGOLED/comments/wzs6hg/adfree_youtube_webos_app/) on reddit. Credits goes to you!_

Background: I had just made myself breakfast, when I grabbed the tv remote and put on the YouTube app on my LG TV. YouTube is fantastic for watching and learning all sorts of information. In todays society everything we need is on YouTube. After selecting my video, I expected the video to begin after an ad. Ads usually last between ten and fifteen seconds, which is annoying but fair enough. In recent times (december 2023) YouTube decided to force 40-60 seconds of ads when using the free version of YouTube on LG TVs. After traveling home i discovered the ads also lasted between 40-60 seconds, without the options to skip any time. This is robbing people of their time while providing nothing in return.

## Do you want to save valuable time? Try this

This assumes you have a LG TV.

1. Go to [LG's homepage](https://us.lgaccount.com/login/sign_in) and create a developer account.
2. Download and install LG's app called **Developer Mode** which you'll find in the TVs app store.
3. Now log into your developer account.
4. Enable `Dev Mode` and reboot. Then enable `Key Server`. Write down IP and passphrase.
5. Use your computer and download and install [webOS Dev Manager](https://github.com/webosbrew/dev-manager-desktop).
6. On the computer, open the app and click `Add Device` to the left. Follow the instructions, which will make you connect to your LG TV. (May 2024: look at known issues further down if you get connection timeout)
7. After that you have a connection, click on `Apps` and install the [Homebrew Channel](https://github.com/webosbrew/webos-homebrew-channel).
8. Then install `YouTube AdFree` and voilá! If you want to check out their source code, click [here](https://github.com/webosbrew/youtube-webos).

<br>

October 2024: There is some issues with the above method. I got something a la "unable to get local issuer certificate". My solution was to connect throug the webOS Dev Manager software, open the terminal and run this one liner: `curl -L https://raw.githubusercontent.com/webosbrew/webos-homebrew-channel/main/tools/install.sh | sh -`. This installed Homebrew on the TV. I couldn't install any app on the tv menu, but had to do it throug the webOS Dev Manager on my computer. There is a [issue](https://github.com/webosbrew/dev-manager-desktop/issues/259) on this matter. Cheers.

<br>

The capitalistic money-focused advertising industry is discusting:
<p>
  <img src="https://preview.redd.it/mvemxjb7nm861.jpg?width=1080&crop=smart&auto=webp&s=39e1581c42d32eb1ddbb27011194dd1de470cbd4" alt="Its disgusting" width="500" style="display:block; margin:auto;">
</p>

You might also try rooting your TV to get more access and control over your TV. You can try [https://rootmy.tv)](https://rootmy.tv) but I dind't have any success using the exploit. I suspect my TV has been patched.

Other stuff:
- [script 1 - reset devmode timer](https://github.com/webosbrew/dev-goodies) - archived
- [script 2 - reset devmode timer](https://github.com/webosbrew/dev-utils/blob/main/scripts/devmode-reset.sh)

### Known issues per May 2024
- You might get an error when connecting to the TV through the webOS Dev Manager software (it just hangs). And if you SSH in a terminal with e.g. `ssh prisoner@youriphere -p 9922` it says `Unable to negotiate with 10.0.0.20 port 9922: no matching host key type found. Their offer: ssh-rsa`. To fix that on macOS/Linux do the following:
1. Create/open the ssh config file with: `nano ~/.ssh/config` in the Terminal
2. Add the content `HostkeyAlgorithms +ssh-rsa` and save the file `ctrl+x` and `enter`
    - June 2024: You might also need to add `PubkeyAcceptedKeyTypes ssh-rsa,ssh-ed25519` to the config file
3. Add correct file permissions with `chmod 600 ~/.ssh/config`
4. Try SSH or with the webOS Dev Manager Software and it should work. Cheers!

#### tips
- Be patient and try more.
- you can get the private key by opening `http://ipaddresshere:9991/webos_rsa` in your browser. Use it with e.g.
````
chmod 700 Downloads/webos_rsa    #we need to update permissions on the key
ssh -v prisoner@10.0.0.11 -p 9922 -i Downloads/webos_rsa  #Example
````
- When doing ssh, add `-v` to the command to give verbose output. Use AI to help understand the output.
- Another resource that might be helpful [Key server is ON but Dev manager can't fetch](https://github.com/webosbrew/dev-manager-desktop/issues/165)
