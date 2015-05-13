# Blackhatting for Good Guys
Evan DeLaney (@edelaney05)  
Fish Hook LLC  
~~April 2015 - CocoaHeads Atlanta~~  
May 2015 - iOS Meetup

---

## Who Am I?
- Fish Hook est. 2010
- Curious & anxious
- ... and probably drink too much coffee for that personality combination
- *I am not a security expert. I’m not even a security professional. I’m maybe a security amateur, and probably a pretty bad one at that.*

---

## Agenda
1. Man-in-the-middle network attack
2. Runtime manipulation with the help of jailbreaking
3. Disassembly to snoop for source code treasure 

---

## Network Security - Anecdotes
- Path.app in 2012: Address Book disaster
- Lenovo: Superfish rootkit
- NSA: always

---

## What Is Charles?
- It’s a local HTTP proxy.

“I’m not a network admin; What’s that?” - You

---

## Man-in-the-Middle Attacks (MitM)
- The attacker inserts themselves between two parties; eavesdropping

---

## Let’s Use Charles to MitM Attack an app
- Examine SSL Traffic
- Breakpoint client requests and server responses

---

## How Do We Prevent?
- SSL Pinning (iTunes Connect, Overcast, et al)
- AFNetwork 2.5.1 SSL Pinning Security Vulnerability

---

## Resources
[Charles’ Tools Documentation](http://www.charlesproxy.com/documentation/tools/)

[Paul Haddad’s tweetstorm from 2012](https://storify.com/johnmichel/paul-haddad-reviews-ios-apps-for-address-book-tran)

WWDC 2011  
[Securing iOS Application](https://developer.apple.com/videos/wwdc/2011/)

LumberBlog  
[Why app developers should care about SSL pinning](http://blog.lumberlabs.com/2012/04/why-app-developers-should-care-about.html)

Minded Security Research Labs  
[SSL MiTM attack in AFNetworking 2.5.1 - Do NOT use it in production!](http://blog.mindedsecurity.com/2015/03/ssl-mitm-attack-in-afnetworking-251-do.html)

## Application Runtime Attacks - Anecdotes
- Jailbreak tweaks
- LLDB
- View hierarchy inspectors (Reveal, Spark Inspector, Xcode 6)

---

## What is Reveal?
- Like Xcode 6’s exploded view debugging, but…
- ...it’s live: changes are reflected in the app
- ...it’s accurate: navigating the view hierarchy is much easier
- ...it shows constraints: ‘nuff said

---

## Using the Reveal library in Xcode (without linking!)
- LLDB’s `expr` command (evaluate expression)
- `dlopen(<path>, <mode>)` to load and link a dynamic library
- Fire a notification to “wake up” the Reveal library (normally fires on UIAppicationDidFinishLaunchingNotification)

---

## Cydia Substrate (previously Mobile Substrate)
- Build run-time patches

---

## Two pieces to Cydia Substrate
- MobileHooker (method swizzling)
- MobileLoader (dlopen)

---

## Let’s use MobileLoader to inject the Reveal iOS library
- Copy Reveal.framework and libReveal.dylib to jailbroken device
- Create MobileLoader plist
- Relaunch Spring Board
- Launch targeted app

---

## How Do We Prevent?
¯\\_(ツ)_/¯
 
---

## Resources:
Reveal’s Blog  
[Integrating Reveal without modifying your Xcode project](http://blog.ittybittyapps.com/blog/2013/11/07/integrating-reveal-without-modifying-your-xcode-project/)

Peter Steinberger (@steipete)  
[How to Inspect the View Hierarch of Third-Party Apps](http://petersteinberger.com/blog/2013/how-to-inspect-the-view-hierarchy-of-3rd-party-apps/)

Apple Mac Developer  
[OS X Manual Page for dlopen(3)](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man3/dlopen.3.html)

Cydia Substrate Docs  
[Getting Started](http://www.cydiasubstrate.com/id/264d6581-a762-4343-9605-729ef12ff0af/)

---

## Static Analysis & Disassembly - Anecdotes
- Having exception breakpoints stop in UIKit gobbledygook
- Steve Nygard’s cass-dump
- NSA’s hacked version of Xcode

---

## What is Hopper?
- Reverse engineering tool
- Turn executable binary into something programmer-readable

---

## Disassembly vs Decompilation
- Disassembly: converting a binary into the assembly for a specific processor architecture
- Decompilation: converting assembly into pseudo-code (hopefully)

---

## Let’s use Hopper to discover an app’s secret
- Disassemble the binary
- Let’s start with -application:didFinishLaunchingWithOptions:
- Decompile this chunk of assembly

---

## How Do We Prevent?
- Code obfuscation (hiding in plain sight)
- How do you keep secrets in the real world? Tell no one.
- Mitigate damage done if a secret is discovered

---

## Resources
[GitHub - nst/iOS-Runtime-Headers](https://github.com/nst/iOS-Runtime-Headers/)

[Future Workshops - Securing Sensitive Strings](http://www.futureworkshops.com/articles/securing-sensitive-strings.html)

[Hopper - Tutorial](http://www.hopperapp.com/tutorial.html)

[Mike Ash’s Friday Q&A - 2012-01-06: The Hopper Disassembler](https://www.mikeash.com/pyblog/friday-qa-2012-01-06-the-hopper-disassembler.html)

[Bart Cone - Hopper + lldb for iOS Developers: A Gentle Introduction](http://www.bartcone.com/new-blog/2014/11/26/hopper-lldb-for-ios-developers-a-gentle-introduction)

---
Books:  
Hacking and Securing iOS Applications - Jonathan Zdziarski  
http://fhk.io/hack-and-secure-ios-apps

iOS Hacker’s Handbook - Charlie Miller, et al  
http://fhk.io/ios-hackers-handbook

---

## Hopper Disassembly, Late Night Edition
- iTunes FairPlay DRM effects binary disassembly
- Jailbreak tool Clutch dumps de-DRM’d app

---

## Resources

Zdziarski’s Blog of Things  
[Introduction to iOS Binary Patching (Part 1)](http://www.zdziarski.com/blog/?p=2172)

[How App Store Apps are Hacked on Non-Jailbroken Phones (and Why Self-Expiring Messaging Apps Aren’t Trustworthy)](http://www.zdziarski.com/blog/?p=4002)

