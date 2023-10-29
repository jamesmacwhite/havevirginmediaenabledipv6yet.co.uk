---
layout: default
image: /assets/images/card.jpg
---

## It's time for Virgin Media to deploy IPv6!

This website is meant to be an informative resource (with an undeniably somewhat sarcastic tone) and raise awareness of the lack of IPv6 on Virgin Media UK Broadband services along with additional information around specific issues with IPv6 tunnels and other areas (it is quite a fun ride). The domain name is a bit of a cheeky dig to see if the marketing team at Virgin Media are watching. Let's find out!

All this information relates to Virgin Media UK Broadband services. I am a Virgin Media Broadband customer myself. This in no way makes me more qualified, but I thought I'd just throw that out there.

## Notable IPv6 events

A summarised list of key public events with Virgin Media mostly related to IPv6.

* **March 2010**: A thread on the official Virgin Media Community Forum dubbed the [IPv6 mega thread](https://community.virginmedia.com/t5/QuickStart-set-up-and/IPv6-support-on-Virgin-media/td-p/35748) was born. The original thread asked a simple question, **"When will Virgin Media deploy IPv6?"** The answer: "When we are ready". Over 10 years later, Virgin Media still aren't ready... 😞
* **October 2014**: [First appearance and presentation](https://tv.theiet.org/?videoid=5899) at the [UK IPv6 council](https://www.ipv6.org.uk/).
* **September 2015**: [Second appearance at the UK IPv6 council](https://tv.theiet.org/?videoid=7412) (Something about DOCSIS bears?!)
* **November 2016**: [Virgin Media tells ISPreview](https://www.ispreview.co.uk/index.php/2016/11/virgin-media-plans-adopt-ipv6-middle-2017.html) they plan to adopt IPv6 by the middle of 2017. (They didn't).
* **August 2017**: ISPreview reveals there is a super “secret” [IPv6 trial for 100 members of Virgin Media’s own staff](https://www.ispreview.co.uk/index.php/2017/08/virgin-media-invite-100-uk-staff-secret-trial-ipv6-internet-addresses.html). The first hint of some serious activity related to IPv6. Exciting.
* **February 2018**: Liberty Global (parent company of Virgin Media) does the unthinkable and releases informative public information about [Virgin Media and it’s plans for DOCSIS 3.1 and IPv6 adoption](https://www.ispreview.co.uk/index.php/2018/02/update-virgin-medias-uk-ipv6-docsis-3-1-plans.html) plans to the public.
* **June 2018**: [A wider consumer trial was reported to be underway](https://www.ispreview.co.uk/index.php/2018/06/cable-isp-virgin-media-start-uk-customer-trial-of-ipv6-addresses.html). IPv6 stats from sources like APNIC confirmed this involved a sizable amount of participants. Everyone gets excited, is this the year?! (Spoiler, no).
* **December 2018**: [Third appearance at the UK IPv6 council](https://www.ipv6.org.uk/2018/11/12/ipv6-council-annual-meeting-dec-2018/), with a presentation and further interesting details around the ongoing IPv6 trial using DS-Lite. Hints for some kind of rollout in 2019.
* **October 2019:** [ISPreview asks Virgin Media for an update on IPv6 progress](https://www.ispreview.co.uk/index.php/2019/10/update-on-ipv6-plans-for-virgin-media-talktalk-and-vodafone.html). Virgin Media provides one of it's trademark canned statements. No IPv6 rollout happens. IPv6 activity goes quiet. (Everyone's IPv6 dreams crushed).
* **May 2020/2020**: Virgin Media and O2 announce they are going to merge, also there was a global pandemic.
* **June 2021**: Merger with O2 is formally completed. So about those IPv6 plans VMO2?
* **May 2021**: Turns out Virgin Media has [a IPv6 implementation hiding away](https://jamesmacwhite.medium.com/have-virgin-media-enabled-ipv6-sort-of-9443e5e855d?source=friends_link&sk=863cd14dc40d718be6d4f8bbf46e2220) if you know where to look. Kind of.
* **November 2021**: [ISPReview asks Virgin Media for an update on IPv6 progress again](https://www.ispreview.co.uk/index.php/2021/11/update-on-ipv6-plans-for-virgin-media-talktalk-plusnet-and-vodafone.html), the spokesperson did however pad it out with a few more words this time.
* **2022**: 12 years on, and no sign of any IPv6. Sad times.
* **October 2023**: Some [Virgin Media customers report](https://community.virginmedia.com/t5/QuickStart-set-up-and/IPv6-support-on-Virgin-media/m-p/5430869/highlight/true#M238987) their reverse DNS hostname has changed, which is a different format and adds "v4wan" into the hostname. Unconfirmed that this relates to any imminent IPv6 deployment, but interesting that now Virgin Media are specifying a hostname value with a specific protocol version, suggesting a v6wan version may exist or will do soon.

## The IPv6 saga

Searching for "Virgin Media IPv6" will probably bring up many of the resources linked above and articles I've likely written or commented on, given I've been quite vocal about the subject for a while now.

### DS-Lite

While Virgin Media hasn't ever deployed IPv6 officially in the UK, it has in the past trialled IPv6 through [DS-Lite](https://en.wikipedia.org/wiki/IPv6_transition_mechanism#Dual-Stack_Lite_(DS-Lite)). DS-Lite is something Liberty Global (parent company of Virgin Media) have regularly deployed in other countries and this seems to be their preferred IPv6 deployment technology. In contrast, [Virgin Media Ireland](https://virginmedia.ie) (Formerly UPC) does in fact have IPv6 through DS-Lite live currently. So Virgin Media have technically deployed IPv6, just not for the UK customer base. DS-Lite however has caused some divide between enthusiasts for a few reasons.

#### Issues with DS-Lite

1. The DS-Lite implementation is only compatible with CPEs in router mode. This has been confirmed by Virgin Media Ireland customers and can be seen in the JavaScript source files of the Virgin Media router firmware. To use this IPv6 implementation means you have to give up modem mode. This doesn't sit well with many customers given a lot of customers rely on this critical function in order to use their own router without double NAT. While IPv6 prefix delegation could allow for having your own router behind the Virgin Media CPE without modem mode, it is certainly not ideal. The reasoning behind the decision was based on the principle that support for DS-Lite itself is not common in many off the shelf' routers.

2. DS-Lite removes having your own IPv4 address being routed to you and instead this will be translated through CGNAT. (CGNAT IS EVIL, [ask Europol](https://www.europol.europa.eu/newsroom/news/are-you-sharing-same-ip-address-criminal-law-enforcement-call-for-end-of-carrier-grade-nat-cgn-to-increase-accountability-online)).
3. DS-Lite means you will no longer be able to run any external services over IPv4 anymore, devices that have questionable IPv6 support, may fall foul of this. Particularly suspect IoT devices, which probably should be an isolated VLAN with no way to communicate to the outside world anyway.
4. DS-Lite will likely be horrible for gamers as most games/lobby systems will not use IPv6 (expect a "strict" NAT type). I'm sure at some point Virgin Media pitched it's broadband with gamer focussed marketing. <small>Just don't talk about the latency!</small>
5. DS-Lite removes IPv4 port forwarding, so if you are currently using that right now, that's not possible with DS-Lite.

Overall DS-Lite provides you a native IPv6 prefix (GOOD!) with IPv4 translated through CGNAT (BAD!). This is why the preferred approach is dual stack, yes it is more complex to maintain two protocols, but since Virgin Media has boasted in the past that its IPv4 space was plentiful, they've most likely got the address space to do it. Two of their biggest competitors in the fixed line broadband space (BT and Sky) both use a dual stack approach and most customers will likely benefit from this approach.

In a more recent canned statement released by Virgin Media. It suggests that multiple IPv6 options have been considered. There may be hope!

<blockquote>
<p>We are continuing to plan our IPV6 deployment having tested several solutions and intend to introduce IPV6 for our customers in future.</p>
<cite>A VM02 Spokesperson, quote from <a href="https://www.ispreview.co.uk/index.php/2021/11/update-on-ipv6-plans-for-virgin-media-talktalk-plusnet-and-vodafone.html">ISPreview (November 2021)</a></cite>
</blockquote>

### IPv6 tunnels

If you have a reasonable understanding of networking or have a technical background, you'll likely know that just because some ISPs don't have IPv6, doesn't mean you can't get IPv6 another way. Many ISPs not deploying IPv6 means users who want it turn to other solutions, one common method is a 6in4 tunnel. If it wasn't insulting or frustrating enough to not have native IPv6 from your ISP, Virgin Media has a troubled history with the 6in4 protocol on its network, leading to a bit of a checkmate scenario.

It has long been known and more recently documented that running a 6in4 tunnel from a provider such as Hurricane Electric results in horribly slow speeds that exhibit a "capped" behaviour on Virgin Media connections. Virgin Media will state there is no speed caps on any protocol on the unlimited broadband services, but some customers call shenanigans. I myself decided I'd investigate the issue and decided to document my findings below.

<a href="https://jamesmacwhite.medium.com/is-virgin-media-traffic-shaping-protocol-41-6in4-ipv6-c1b8b6e645f7" target="_blank" class="btn text-center">Read my technical analysis</a>

**If you don't want to read the full article above, these are the main findings**

1. When a 6in4 tunnel is pointed at any Virgin Media IP, the speed can be very poor. (This also includes Virgin Media Business lines as well)
2. If you encapsulate 6in4 over something like UDP, suddenly the problem goes away
3. If you have a 6in4 tunnel pointed to a non Virgin Media IP, you will not experience any problems

**Two key findings stand out from this**

1. Something on the Virgin Media side is the problem
2. Encapsulating 6in4 within another protocol seems to avoid or circumvent the performance issues

Any protocol such as L2TP, UDP, OpenVPN, Wireguard you name it, if you send 6in4 inside them, you'll not see the same performance problems.

**The main theories of why this happens are <ins>widely debated</ins>**:

1. Throttling may well be happening somewhere, but Virgin Media itself states they aren't actively doing this.
2. Some form of QoS or prioritisation of protocols happens in the network, treating 6in4 like a lower class citizen compared to other protocols.
3. The CPE (Customer Premise Equipment) i.e. SuperHub/Hub has been hinted as a potential factor
4. General CPU hardware bottlenecks (6in4 does have some CPU requirements)
5. Bad configuration e.g. MTU.

The theory which [Virgin Media itself seems to think might be the case](https://www.ispreview.co.uk/index.php/2020/08/virgin-media-uk-move-to-fix-20mbps-speed-cap-on-ipv6-tunnels.html) is it's their CPE causing the performance problem for customers. It has been reported the Hub4, Hub5 and Hitron Chita Router for Virgin Media Business does not have the same performance problems, hinting that it is related to the hardware of the older SuperHub, SuperHub 2/2ac and Hub3 models.

Ultimately, it doesn't really matter as it is worth highlighting that 6in4 is also a transitional technology and shouldn't be used forever either, so holding out on 6in4 is basically just like not deploying IPv6 anyway. The real "fix" here is to demonstrate to Virgin Media that IPv6 is needed now. Thus resolving the lack of native IPv6 problem and negating the need to use any form of transitional IPv6 technology and indirectly resolving the 6in4 issue by making it a redundant issue.

### Alternative IPv6 options

Now you've been briefed about the lack of native IPv6 on Virgin Media along with the specific 6in4/tunnel issues you are likely to encounter. What are the potential alternative IPv6 options available? The easiest option would be to simply wait for Virgin Media to just deploy IPv6 themselves, however given it has been over 10 years since the question was first asked and we're still waiting, that's not really going to be a quick solution. Below are some alternatives you might want to consider if you cannot wait for Virgin Media itself to deploy IPv6.

1. **[Andrews and Arnold L2TP service](https://www.aa.net.uk/broadband/l2tp-service/)** - Unlike Virgin Media, Andrews and Arnold actually thought about IPv6 a while ago and have had it working on their network for a long time (IT CAN BE DONE!). Their L2TP service allows you to have one, or a block of static IPv4 address and at minimum a /48 native IPv6 prefix. The downside? There is a speed cap of 200 mbps and data isn't unlimited, but if you can configure an L2TP tunnel on a client somewhere, you'll be in business and essentially have your IPv6 transit from another ISP entirely without having to have another separate broadband line. Having transit from other providers is actually quite common, just not usually from a home consumer sense. Andrews and Arnold have noted that some of their customers do in fact use the L2TP service for this exact reason.

2. **Rent a Virtual Private Server (VPS) with native IPv6** - If you can get a VPS from a provider like [Linode](https://www.linode.com/), [Digital Ocean](https://www.digitalocean.com/) etc, you can setup your own VPN tunnel with something like Wireguard and provide a IPv6 prefix over the tunnel. You could also do this with 6in4 but if you've gone that far, you might as well have native IPv6 to start with. A VPN solution would likely be more favoured to use Wireguard compared to OpenVPN, given Wireguard is more optimised for embedded devices and offers better speed due to being less taxing on CPU with more modern cryptography.

3. **Configure a 6in4 tunnel on another independent WAN link** - Multihoming is becoming more common, and it's not just something in the enterprise world anymore. We know that the 6in4 issues are specifically related to Virgin Media regardless of what the actual true cause is, so there is nothing stopping you from having a tunnel point to an IP address on another internet connection on the same router, if you happen to have multiple internet connections of course.

4. **Switch to another Internet Service Provider (ISP)** - A nuclear option but if IPv6 is absolutely essential, critical and you want to send a clear message, changing provider is really the only other viable alternative. There are various ISPs in the UK that have deployed IPv6. To name a few these are, [BT](https://www.bt.com/), [Sky](https://www.sky.com/), [Andrews and Arnold](https://www.aa.net.uk/), [EE (Mobile broadband only)](https://ee.co.uk), [Zen Internet](https://www.zen.co.uk/), [Aquiss](https://www.aquiss.net/). This is by no means a complete list, but highlights that there are providers that do see the importance of IPv6 right now, some having deployed IPv6 for many years.

Aside from switching providers entirely, it is important to note that these alternative solutions will cost you additional money in addition to an existing Virgin Media contract or subscription therefore you will need to weight up how much is it worth to have performant IPv6 and essentially investing a workaround vs not at all.

## Tell Virgin Media what you think

By now you know that Virgin Media have been very resistant to deploy IPv6, otherwise this website wouldn't exist! The general view and consensus that Virgin Media are signalling suggests that they just don't see any business or customer benefits to do it. While it is true there might not be a strong customer use case currently (which is one of the major IPv6 adoption problem areas). Some of their major competitors like BT and Sky deployed IPv6 years ago with little fuss because they at least are thinking ahead. Equally, Virgin Media will have to deploy IPv6 at some point, because it is the future of the internet, like it or not. IPv4 is technically classified as legacy and holding on to it is just delaying the inevitable. Therefore, the only option we have as perhaps more technically minded customers is to make Virgin Media listen. Perhaps if they get enough noise from customers or businesses about IPv6, they might just start to pay more attention, instead of disregarding it as they have done for over 10 years. While a lot of Virgin Media customers won't know or even care about IPv6, the people that do have a responsibility to at least make Virgin Media listen and convince them that the time is now!

The simple solution to fix all of this complicated mess is for Virgin Media to deploy IPv6, which seems obvious when it is said like that, but it really is!

**Time to spread the word! Consider signing the petition and tweet them to raise awareness. Let your voice be heard. Deploy IPv6!**
