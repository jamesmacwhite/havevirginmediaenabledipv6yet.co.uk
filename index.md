---
layout: default
---

## About this website

This website is meant to be an informative resource (with an admittedly somewhat sarcastic tone) on the lack of IPv6 on Virgin Media Broadband services along with additional information around specific issues with IPv6 tunnels and other areas (it is a fun ride). The domain name is a bit of a cheeky dig to see if the marketing team at Virgin Media are watching. Let's find out!

All this information relates to Virgin Media UK Broadband services. I am a Virgin Media Broadband customer myself. That in no way makes me any more qualified, but I thought I'd just throw that out there.

## Notable IPv6 events

A summarised list of key IPv6 related events at Virgin Media UK, completely made up by me as I don't work for Virgin Media and after creating this little site, likely have zero chance of doing so either. Oops.

* **March 2010**: [The IPv6 mega thread was born](https://community.virginmedia.com/t5/QuickStart-set-up-and/IPv6-support-on-Virgin-media/td-p/35748) on the Virgin Media Community Forums. The original thread asked a simple question, when will Virgin Media deploy IPv6? The answer: "When we are ready". Over 10 years later, Virgin Media still aren't ready...
* **October 2014**: First appearance and presentation at the [UK IPv6 council](https://www.ipv6.org.uk/).
* **September 2015**: Second appearance at the UK IPv6 council. Talks about DOCSIS bears LOL.
* **August 2017**: ISPreview reveals there is a super “secret” [IPv6 trial for 100 members of Virgin Media’s own staff](https://www.ispreview.co.uk/index.php/2017/08/virgin-media-invite-100-uk-staff-secret-trial-ipv6-internet-addresses.html). The first hint of some serious activity related to IPv6. Exciting.
* **February 2018**: Liberty Global (parent company of Virgin Media) released some interesting information about [Virgin Media and it’s plans for DOCSIS 3.1 and IPv6 adoption](https://www.ispreview.co.uk/index.php/2018/02/update-virgin-medias-uk-ipv6-docsis-3-1-plans.html) (spoiler, it didn't happen). At this point it became known that Virgin Media UK had seemed to have chosen DS-Lite for their IPv6 rollout. Technical users start crying in pain see DS-Lite mentioned.
* **June 2018**: [A wider customer trial was reported to be underway](https://www.ispreview.co.uk/index.php/2018/06/cable-isp-virgin-media-start-uk-customer-trial-of-ipv6-addresses.html) and judging by the APNIC IPv6 stats for Virgin Media’s AS number during that period, this seemed to involve a sizable amount of IPv6 testing. Granted, not all recorded stats may have been residential broadband customers, but there was a lot of IPv6 traffic being recorded when there was pretty much zero from Virgin Media prior. Cautiously optimistic was the word.
* **December 2018**: Third appearance at the UK IPv6 council, with a presentation and some interesting details around the on-going IPv6 trial through DS-Lite. Looks promising for some kind of launch in 2019.
* **2019**: No IPv6 rollout happens. IPv6 activity on the Virgin Media AS goes quiet. (Hopes dashed)
* **2020**: Nothing happened (Besides a global pandemic)
* **2021**: YOU ARE HERE

As you can see, it has been a bit of wild ride!

## IPv6

### DS-Lite

While Virgin Media hasn't deployed IPv6 officially, it has in the past trialled IPv6 through DS-Lite. DS-Lite is something Liberty Global (parent company of Virgin Media) have regularly deployed in other countries, they seem to like it. In contrast Virgin Media Ireland does in fact have IPv6 through DS-Lite live right now. So Virgin Media have technically deployed IPv6, just not for the UK customer base. However, DS-Lite is horrible (opinion), so even though the objective is to get Virgin Media to deploy IPv6, preferably, it should be a dual stack approach, not DS-Lite. There are rumours to suggest that DS-Lite might have been abandoned a while ago for the UK, but no one knows for sure, given Virgin Media doesn't like to talk about IPv6. So it is all speculation at this point.

#### DS-Lite issues

Technically, the DS-Lite isn't "bad", it is after all standardised and used by various providers. However, here are some key issues with DS-Lite from a consumer basis here which might catch a lot of people out:

* DS-Lite is believed to be only possible in router mode based on the Hub firmware code, using it means you give up modem mode (NO THANKS)
* DS-Lite removes have your own IPv4 address being routed to you and instead this will be done through CGNAT (CGNAT IS EVIL)
* DS-Lite is horrible for gamers as most gaming/match making systems will not use IPv6 (SAY BYE TO YOUR NAT TYPE)

DS-Lite provides you a native IPv6 prefix (GOOD!) with IPv4 translated through CGNAT (BAD!). This is why the preferred approach is dual stack, yes it is more complex to maintain two protocols, but since Virgin Media had boasted in the past that its IPv4 space was plentiful, they've got the address space to do it. I'm pretty sure Liberty Global even raided their address space when they acquired Virgin Media, maybe they stole it all! Greedy buggers. GIVE IT BACK!

### IPv6 tunnels

If you are into networking or technical, you'll know that just because some ISPs don't have IPv6, doesn't mean you can't get IPv6 another way. Many ISPs not deploying IPv6 means users who want it turn to other solutions, mainly tunnels and most commonly 6in4. If it wasn't insulting enough to not have native IPv6 from your ISP, Virgin Media decides to play the ultimate checkmate and specifically screws around with certain protocols in their network too. They'll deny it, but there is some evidence to prove otherwise. Regardless, guess what protocol happens to be caught up in all of this? Ah yes, 6in4.

It has long been known and more recently documented that running a 6in4 tunnel from a provider such as Hurricane Electric results in horribly slow speeds that look to be "capped" on Virgin Media connections. Virgin Media will state there is no speed caps on any protocol on the unlimited broadband services, but some call shenanigans. Here's why...

I decided that I would investigate what was going on here in a bit more detail, because I'd put up with the issue for so long myself and couldn't find any detailed information around the subject, I decided to be the IPv6 hero and investigate this once and for all for great internet protocol justice. We live in a society where everyone should be treated equally, so should protocols! I ended up documenting my findings which has attracted the attention of other Virgin Media broadband customers who were found themselves in a similar situation, as well as Virgin Media itself (HI!).

<a href="https://jamesmacwhite.medium.com/is-virgin-media-traffic-shaping-protocol-41-6in4-ipv6-c1b8b6e645f7" target="_blank" class="btn">Read my technical analysis</a>

**If you don't want to read the full article above. No worries, here's the TL;DR highlights**

1. When a 6in4 tunnel is pointed at a Virgin Media IP, the performance is awful. This is well known. (This includes Virgin Media Business as well by the way).
2. If you encapsulate 6in4 over something like UDP, suddenly the problem goes away. Plot twist.
3. If you have a 6in4 tunnel pointed to a non Virgin Media IP, you'll not have any issues either.

**Two key findings stand out from this**

1. Virgin Media is the problem (We kind of knew this, but confirmation is always nice)
2. Encapsulating 6in4 within another protocol seems to avoid the performance issues

L2TP, UDP, Wireguard you name it, if you send 6in4 over any of them, you'll not see the same performance problems. So about that not throttling traffic thing...

**The main theories of the issue are**:

* Throttling is indeed happening somewhere
* Some form of QoS or prioritisation of protocols happens in the network 
* The CPE i.e. SuperHub/Hub is the problem. The theory being the infamous Intel Puma SoC, but this isn't limited to just the Intel Puma SoC units.
* Bad MTU configuration (unlikely)

The theories as to what the specific issue is are widely debated and disputed. Ultimately, it doesn't really matter as it is worth pointing out that 6in4 is also a transitional technology and shouldn't be used forever. The real fix here is to make Virgin Media do the needful and rollout IPv6. Thus resolving the lack of IPv6 problem and negating the need to use any form of transitional IPv6 deployment. Unless of course they decide to use DS-Lite, then you should just switch providers. Seriously.

### Alternative IPv6 options

Now you've been informed about the lack of native IPv6 and the specific 6in4/tunnel issues. What other options are available?

1. **Andrews and Arnold L2TP service** - Unlike Virgin Media, Andrews and Arnold actually thought about IPv6 a while ago and have had it working for a long time (IT CAN BE DONE!). Their L2TP service allows you to have one, or a block of static IPv4 address and at minimum a /48 native IPv6 prefix. The downside? There is a speed cap and data isn't unlimited, but if you can configure an L2TP tunnel, you'll be in business and essentially have your IPv6 transit from someone else entirely. It isn't unheard of after all.

2. **Rent a VPS with native IPv6** - If you can get a VPS from a provider like Linode, Digital Ocean etc, you can setup your own VPN tunnel with something like Wireguard and provide a IPv6 prefix over the tunnel. You could also do this with 6in4 but at this point, if you've gone that far, you might as well have native IPv6.

3. **Configure 6in4 on another independent WAN link** - Multihoming is becoming more common, and it's not just in the enterprise world anymore. We know that the 6in4 issues are specifically related to Virgin Media regardless of the actual cause, so there is nothing stopping you from having a tunnel point to an IP address on another internet connection on the same router, if you happen to have multiple internet connections of course.

There is however one major issue with all of these solutions, they'll cost you money in addition to your existing Virgin Media contract. You will need to weight up how much is it worth to have performant IPv6 vs not at all or putting up with poor 6in4 performance and living with it. Great options right?!

### The real solution is IPv6 (No, really)

The simple solution to fix all of this complicated mess is for Virgin Media to deploy IPv6, which seems obvious when you say it but it really is.

## Tell Virgin Media what you think about the lack of IPv6

By now you know that Virgin Media have been resistant to deploy IPv6. The general view and consensus is that they just don't see any business or customer benefits to do it. While that might be true to a degree some of their major competitors like BT and Sky, deployed IPv6 years ago with little fuss. Equally, Virgin Media will have to deploy IPv6 at some point, because it is the future, like it or not. Therefore, the only option we have as customers is to make Virgin Media listen. Perhaps if they get enough noise from customers about IPv6, they might just start to pay more attention, instead of disregarding it as they have done for over 10 years. While a lot of Virgin Media customers won't know or even care about IPv6, the people that do have a responsibility to at least make Virgin Media listen and convince them that the time is now!

**Time to spread the word. Sign the petition and tweet them. Let your voice be heard!**