# Ad-free YouTube on WebOS
_This information is just a rewrite of information given by user [Cr3z33-71](https://www.reddit.com/r/LGOLED/comments/wzs6hg/adfree_youtube_webos_app/) on reddit. Credits goes to you!_

Background: I had just made myself breakfast, when I grabbed the tv remote and put on the YouTube app on my LG TV. YouTube is fantastic for watching and learning all sorts of information. In todays society everything we need is on YouTube. After selecting my video, I expected the video to begin after an ad. Ads usually last between ten and fifteen seconds, which is annoying but fair enough. In recent times (december 2023) YouTube has now decided to force 30 seconds of ads when using the free version of YouTube on LG TVs. After traveling home i discovered the ads lasts 40 and even 50 seconds, without the options to skip any time. This is robbing people of their time while providing nothing in return. This is totally unacceptable.


## Are you tired of being tracked, bombarded with ads and being robbed of your valuable time?

1. Go to [LG's homepage](https://us.lgaccount.com/login/sign_in) and create a developer account.
2. Download and install LG's app called **Developer Mode** which you'll find in the TVs app store.
3. Now log into your developer account.
4. Enable `Dev Mode` and `Key Server`. Write down IP and passphrase.
5. Use your computer and download and install the app [webOS Dev Manager](https://github.com/webosbrew/dev-manager-desktop).
6. On the computer, open the app and click `Add Device` to the left. Follow the instructions, which will make you connect to your LG TV. (May 2024: look at known issues further down if you get connection timeout)
7. After that you have a connection, click on `Apps`and install the [Homebrew Channel](https://github.com/webosbrew/webos-homebrew-channel).
8. Then install `YouTube AdFree` and voilá, congrats!

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
- You might get an error when connecting to the TV through the webOS Dev Manager software (it just hangs). And if you SSH in a terminal with e.g. `ssh prisoner@10.0.0.20 -p 9922` it says `Unable to negotiate with 10.0.0.20 port 9922: no matching host key type found. Their offer: ssh-rsa`. To fix that on macOS/Linux do the following:
1. Create/open the ssh config file with: `nano ~/.ssh/config`
2. Add the content `HostkeyAlgorithms +ssh-rsa` and save the file `ctrl+x` and `enter`
3. Add correct file permissions with `chmod 600 ~/.ssh/config`
4. Do SSH or try again with the webOS Dev Manager Software and it should work. Cheers!
