---
layout: default
image: '/assets/images/World_IPv6_launch_logo.svg'
---

## About this website

This website is meant to be an informative resource (with an admittedly somewhat sarcastic tone) and raise awareness of the lack of IPv6 on Virgin Media UK Broadband services along with additional information around specific issues with IPv6 tunnels and other areas (it is quite a fun ride). The domain name is a bit of a cheeky dig to see if the marketing team at Virgin Media are watching. Let's find out!

All this information relates to Virgin Media UK Broadband services. I am a Virgin Media Broadband customer myself. This in no way makes me more qualified, but I thought I'd just throw that out there.

## Notable IPv6 events

A summarised list of key IPv6 related events with Virgin Media.

* **March 2010**: [The IPv6 mega thread was born](https://community.virginmedia.com/t5/QuickStart-set-up-and/IPv6-support-on-Virgin-media/td-p/35748) on the Virgin Media Community Forums. The original thread asked a simple question, when will Virgin Media deploy IPv6? The answer: "When we are ready". Over 10 years later, Virgin Media still aren't ready...
* **October 2014**: [First appearance and presentation](https://tv.theiet.org/?videoid=5899) at the [UK IPv6 council](https://www.ipv6.org.uk/).
* **September 2015**: [Second appearance at the UK IPv6 council](https://tv.theiet.org/?videoid=7412) (Something about DOCSIS bears?!)
* **August 2017**: ISPreview reveals there is a super “secret” [IPv6 trial for 100 members of Virgin Media’s own staff](https://www.ispreview.co.uk/index.php/2017/08/virgin-media-invite-100-uk-staff-secret-trial-ipv6-internet-addresses.html). The first hint of some serious activity related to IPv6. Exciting.
* **February 2018**: Liberty Global (parent company of Virgin Media) released some interesting information about [Virgin Media and it’s plans for DOCSIS 3.1 and IPv6 adoption](https://www.ispreview.co.uk/index.php/2018/02/update-virgin-medias-uk-ipv6-docsis-3-1-plans.html) (spoiler, it didn't happen). At this point it became known that Virgin Media UK had seemed to have chosen DS-Lite for their IPv6 rollout. Technical users start crying in pain seeing DS-Lite mentioned.
* **June 2018**: [A wider customer trial was reported to be underway](https://www.ispreview.co.uk/index.php/2018/06/cable-isp-virgin-media-start-uk-customer-trial-of-ipv6-addresses.html) and judging by the APNIC IPv6 stats for Virgin Media’s AS number during that period, this seemed to involve a sizable amount of IPv6 testing. Granted, not all recorded stats may have been residential broadband customers, but a significant amount of IPv6 traffic had been recorded when there was pretty much zero from Virgin Media prior. Cautiously optimistic was the word.
* **December 2018**: Third appearance at the UK IPv6 council, with a presentation and some interesting details around the ongoing IPv6 trial through DS-Lite. Looks promising for some kind of launch in 2019.
* **2019**: No IPv6 rollout happens. IPv6 activity on the Virgin Media AS goes quiet. (Hopes dashed)
* **2020**: Nothing happened (Besides a global pandemic)
* **2021**: YOU ARE HERE

As you can see, it has been a bit of a wild ride!

## IPv6

Searching for "Virgin Media IPv6" will probably bring up many of the resources linked above and articles I've likely written or commented on, given I've been quite vocal about the subject for a while now.

### DS-Lite

While Virgin Media hasn't deployed IPv6 officially in the UK, it has in the past trialled IPv6 through [DS-Lite](https://en.wikipedia.org/wiki/IPv6_transition_mechanism#Dual-Stack_Lite_(DS-Lite)). DS-Lite is something Liberty Global (parent company of Virgin Media) have regularly deployed in other countries and seems to be their preferred IPv6 deployment technology. In contrast, Virgin Media Ireland does in fact have IPv6 through DS-Lite live right now. So Virgin Media have technically deployed IPv6, just not for the UK customer base. However, on a personal opinion level DS-Lite is horrible for consumers, so even though the objective is to get Virgin Media to deploy IPv6, preferably, it should be a dual stack approach, not DS-Lite. There are rumours to suggest that DS-Lite might have been abandoned a while ago for the UK, but no one knows for sure, given Virgin Media doesn't like to talk about IPv6. So it is all speculation at this point.

#### Issues with DS-Lite

Why is DS-Lite seen as "bad", it is after all standardised and used by various providers right? Here are some key issues with DS-Lite from a consumer basis which might catch a lot of people out and possibly a reason why it was rumoured to be abandoned.

* DS-Lite is believed to be only possible in router mode based on the Virgin Media Hub firmware code, to use it means you have to give up modem mode. This won't sit well with many customers given a lot of customers choose to use this functionality and have done for years
* DS-Lite removes having your own IPv4 address being routed to you and instead this will be translated through CGNAT. (CGNAT IS EVIL, ask Interpol)
* DS Lite means you will no longer be able to run external services over IPv4 anymore
* DS-Lite is horrible for gamers as most games/lobby systems will not use IPv6 (irony)
* DS-Lite removes IPv4 port forwarding, so if you are currently doing that right now, that's not possible anymore

DS-Lite provides you a native IPv6 prefix (GOOD!) with IPv4 translated through CGNAT (BAD!). This is why the preferred approach is dual stack, yes it is more complex to maintain two protocols, but since Virgin Media has boasted in the past that its IPv4 space was plentiful, they've most likely got the address space to do it. Two of their biggest competitors in the fixed line broadband space went dual stack (BT and Sky).

### IPv6 tunnels

If you have a reasonable understanding of networking or have a technical background, you'll likely know that just because some ISPs don't have IPv6, doesn't mean you can't get IPv6 another way. Many ISPs not deploying IPv6 means users who want it turn to other solutions, one common method is a 6in4 tunnel. If it wasn't insulting or frustrating enough to not have native IPv6 from your ISP, Virgin Media has a troubled history with the 6in4 protocol on it's network, leading to a bit of a checkmate scenario.

It has long been known and more recently documented that running a 6in4 tunnel from a provider such as Hurricane Electric results in horribly slow speeds that exhibit a "capped" behaviour on Virgin Media connections. Virgin Media will state there is no speed caps on any protocol on the unlimited broadband services, but some customers call shenanigans. I myself decided I'd investigate the issue and decided to document my findings below.

<a href="https://jamesmacwhite.medium.com/is-virgin-media-traffic-shaping-protocol-41-6in4-ipv6-c1b8b6e645f7" target="_blank" class="btn">Read my technical analysis</a>

**If you don't want to read the full article above, these are the main findings**

1. When a 6in4 tunnel is pointed at a Virgin Media IP, the speed is very poor. (This also includes Virgin Media Business)
2. If you encapsulate 6in4 over something like UDP, suddenly the problem goes away
3. If you have a 6in4 tunnel pointed to a non Virgin Media IP, you will not experience any problems

**Two key findings stand out from this**

1. Something on the Virgin Media side is the problem
2. Encapsulating 6in4 within another protocol seems to avoid the performance issues

L2TP, UDP, OpenVPN, Wireguard you name it, if you send 6in4 over any of them, you'll not see the same performance problems. So about that not throttling traffic thing...

**The main theories of why this is the case are <ins>widely debated</ins>**:

* Throttling may well be happening somewhere, but Virgin Media state there isn't any
* Some form of QoS or prioritisation of protocols happens in the network, treating 6in4 like a lower class citizen compared to other protocols
* The CPE (Customer Premise Equipment) i.e. SuperHub/Hub has been hinted as a potential factor
* General CPU bottlenecks (6in4 does have some CPU requirements)
* Bad configuration e.g. MTU.

The alternative theory which Virgin Media itself seems to think might be the case is it's their CPE causing the performance problem for customers. This however is also debated as the issue has been proven to occur on the first version of the SuperHub and up. Equally, remember the encapsulation theory.

The many theories as to what the specific issue is with 6in4 are widely debated and disputed. Ultimately, it doesn't really matter as it is worth pointing out that 6in4 is also a transitional technology and shouldn't be used forever either, so holding out on 6in4 is basically just like not deploying IPv6 anyway. The real "fix" here is to demonstrate to Virgin Media that IPv6 is needed now. Thus resolving the lack of IPv6 problem and negating the need to use any form of transitional IPv6 deployment.

### Alternative IPv6 options

Now you've been informed about the lack of native IPv6, and the specific 6in4/tunnel issues. What other options are available without native IPv6? You could of course just not bother and wait for Virgin Media to eventually deploy it after all. Chances are however you are interested in IPv6 and likely an enthusiast like me. Here are some alternatives you could look into.

1. **[Andrews and Arnold L2TP service](https://www.aa.net.uk/broadband/l2tp-service/)** - Unlike Virgin Media, Andrews and Arnold actually thought about IPv6 a while ago and have had it working on their network for a long time (IT CAN BE DONE!). While not a sales pitch, their L2TP service allows you to have one, or a block of static IPv4 address and at minimum a /48 native IPv6 prefix. The downside? There is a speed cap and data isn't unlimited, but if you can configure an L2TP tunnel on a client somewhere, you'll be in business and essentially have your IPv6 transit from someone else entirely. This isn't unheard of after all and Andrews and Arnold themselves note some of their customers do this right now.

2. **Rent a VPS with native IPv6** - If you can get a VPS from a provider like Linode, Digital Ocean etc, you can setup your own VPN tunnel with something like Wireguard and provide a IPv6 prefix over the tunnel. You could also do this with 6in4 but at this point, if you've gone that far, you might as well have native IPv6 to start with. Any VPN solution should likely be based on Wireguard these days compared to OpenVPN, given Wireguard is more optimised for embedded devices and offers better speed due to being less taxing on CPU.

3. **Configure 6in4 on another independent WAN link** - Multihoming is becoming more common, and it's not just something in the enterprise world anymore. We know that the 6in4 issues are specifically related to Virgin Media regardless of what the actual cause is, so there is nothing stopping you from having a tunnel point to an IP address on another internet connection on the same router, if you happen to have multiple internet connections of course.

There is however one major issue with all of these solutions, they'll cost you money in addition to your existing Virgin Media contract. You will need to weight up how much is it worth to have performant IPv6 vs not at all or putting up with poor 6in4 performance and living with it given that is the free option without cost.

## Tell Virgin Media what you think

By now you know that Virgin Media have been very resistant to deploy IPv6. The general view and consensus they are signalling suggests that they just don't see any business or customer benefits to do it. While that might be true to a degree some of their major competitors like BT and Sky, deployed IPv6 years ago with little fuss. Equally, Virgin Media will have to deploy IPv6 at some point, because it is the future, like it or not. Therefore, the only option we have as customers is to make Virgin Media listen. Perhaps if they get enough noise from customers about IPv6, they might just start to pay more attention, instead of disregarding it as they have done for over 10 years. While a lot of Virgin Media customers won't know or even care about IPv6, the people that do have a responsibility to at least make Virgin Media listen and convince them that the time is now!

The simple solution to fix all of this complicated mess is for Virgin Media to deploy IPv6, which seems obvious when it is said like that, but it really is!

**Time to spread the word! Sign the petition and tweet them. Let your voice be heard. Deploy IPv6!**