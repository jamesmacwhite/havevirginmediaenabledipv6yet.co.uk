---
layout: default
---

<p class="lead">Virgin Media like many UK Internet Service Providers (ISPs) have not yet deployed IPv6. While this isn't major news because loads of ISPs suffer from IPv6 deployment lag (since December 1995), Virgin Media UK has an interesting IPv6 story which is why I felt I needed to create this page, to inform others who may be looking at IPv6 (or the lack of) and happen to be a Virgin Media customer.</p>

## About this page

[Virgin Media UK](https://www.virginmedia.com) does not currently have IPv6 deployed however [Virgin Media Ireland](https://www.virginmedia.ie) does, just to make it confusing. DS-Lite is used by Liberty Global and Virgin Media inherits this IPv6 transitional technology because Liberty Global (being the parent company) likes to deploy it A LOT it seems. Personally DS-Lite can go die in a fire, but that's just me. The focus of this is IPv6 generally which Virgin Media have a great track record of not having. So we'll focus on that. This website domain is specifically named for this purpose after all!

All this information relates to Virgin Media UK Broadband services.

## The unofficial IPv6 event timeline

A summarised list of key IPv6 related events at Virgin Media UK, completely made up by me as I don't work for them and after creating this little site, likely have zero chance of doing so either.

* **March 2010**: [The IPv6 mega thread was born](https://community.virginmedia.com/t5/QuickStart-set-up-and/IPv6-support-on-Virgin-media/td-p/35748) on the Virgin Media Community Forums. The original thread asked a simple question, when will Virgin Media deploy IPv6? The answer: "When we are ready". Over 10 years later, Virgin Media still aren't ready...
* **October 2014**: First appearance and presentation at the [UK IPv6 council](https://www.ipv6.org.uk/).
* **September 2015**: Second appearance at the UK IPv6 council.
* **August 2017**: ISPreview reveals there is a super “secret” [IPv6 trial for 100 members of Virgin Media’s own staff](https://www.ispreview.co.uk/index.php/2017/08/virgin-media-invite-100-uk-staff-secret-trial-ipv6-internet-addresses.html). The first hint of serious activity related to IPv6 beyond Virgin Media’s own network engineers and testnet.
* **February 2018**: Liberty Global (parent company of Virgin Media) released some interesting information about [Virgin Media and it’s plans for DOCSIS 3.1 and IPv6 adoption](https://www.ispreview.co.uk/index.php/2018/02/update-virgin-medias-uk-ipv6-docsis-3-1-plans.html) (spoiler, it didn't happen). At this point it became known that Virgin Media UK had chosen Benu Networks DS-Lite solution for their IPv6 rollout.
* **June 2018**: [A wider customer trial was reported to be underway](https://www.ispreview.co.uk/index.php/2018/06/cable-isp-virgin-media-start-uk-customer-trial-of-ipv6-addresses.html) and judging by the APNIC IPv6 stats for Virgin Media’s AS number during that period, this seemed to involve a sizable amount of IPv6 testing. Granted, not all of numbers may have been residential broadband customers, but none the less there was all of sudden a lot of IPv6 traffic being recorded when there was pretty much zero from Virgin Media prior.
* **December 2018**: Third appearance at the UK IPv6 council, with some additional information about the wider IPv6 test currently happening and further information about DS-Lite. Hints of an IPv6 rollout in 2019.
* **2019**: No IPv6 rollout happens. IPv6 activity on the Virgin Media AS goes quiet.
* **2020**: Nothing happened (Besides a global pandemic)
* **2021**: YOU ARE HERE

## IPv6 tunnels (It's complicated...)

If you are into networking or technical, you'll know that just because some ISPs don't have IPv6, doesn't mean you can't get IPv6 another way. Many ISPs not deploying IPv6 means users who want it turn to other solutions, mainly tunnels and most commonly 6in4. If it wasn't insulting enough to not have native IPv6 from your ISP, Virgin Media decides to play the ultimate checkmate and specifically screws around with certain protocols in their network too. They'll deny it, but there is evidence to prove otherwise. Guess what protocol happens to be caught up in all of this? Ah yes, 6in4 also known as protocol 41.

It has long been documented that running a 6in4 tunnel from a provider such as Hurricane Electric results in horribly slow speeds that look to be "capped" on Virgin Media connections. Virgin Media will state there is no speed caps on any protocol on the unlimited broadband services, but I call shenanigans. Here's why...

One day I decided that I would investigate what was going on here, because I'd put up with the issue for so long myself and couldn't find any detailed information around the subject, I decided to be the IPv6 hero and investigate this once and for all for great protocol justice. We live in a society where everyone should be treated equally, so should protocols! I ended up documenting my findings which has attracted the attention of other Virgin Media broadband customers who were in similar situations, as well as Virgin Media itself (HI!).

[The full article and analysis of 6in4 IPv6 on Virgin Media and the issue in play](https://jamesmacwhite.medium.com/is-virgin-media-traffic-shaping-protocol-41-6in4-ipv6-c1b8b6e645f7)

**If you don't want to read the full article above. No worries, here's the TL;DR highlights**

1. When a 6in4 tunnel is pointed at a Virgin Media IP, the performance is awful. This is well known. (This includes Virgin Media Business as well by the way)
2. If you encapsulate 6in4 over something like UDP, suddenly the problem goes away. Plot twist
3. If you have a 6in4 tunnel pointed to a non Virgin Media IP, you'll not have any issues either

**Two key findings stand out from this**

1. Virgin Media is the problem (We kind of knew this, but confirmation is always nice)
2. Encapsulating 6in4 within another protocol seems to avoid the performance issues

L2TP, UDP, Wireguard you name it, if you send 6in4 over any of them, you'll not see the same performance problems. So about that not throttling traffic thing...

No one knows for sure because Virgin Media deny any discussion around throttling, however you read the full details and tests done to show the speed issues and make up your own mind. We are unlikely to ever get an official detailed explanation of why 6in4 is so bad on Virgin Media broadband, but this is the situation we find ourselves in. Tools like curl and iperf3 don't lie.

It is worth pointing out that 6in4 is also a transitional technology and shouldn't be used forever. The real fix here is to make Virgin Media do the needful and rollout IPv6. Thus resolving the lack of IPv6 problem and negating the need to use any form of transitional IPv6 deployment. Unless of course they decide to use DS-Lite, then you should just switch providers. Seriously.

## Alternative IPv6 options that aren't 6in4

Now you've been informed about 6in4/tunnel issues. What other options are available since Virgin Media currently refuses to deploy IPv6 or providing useful information on their plans?

1. **Andrews and Arnold L2TP service** - Unlike Virgin Media, Andrews and Arnold actually thought about IPv6 a while ago and have had it working for a long time. Their L2TP service allows you to have one, or a block of static IPv4 address and at minimum a /48 native IPv6 prefix. The downside? There is a speed cap and data isn't unlimited, but if you can configure an L2TP tunnel, you'll be in business.

2. **Rent a VPS with native IPv6** - If you can get a VPS from a provider like Linode, Digital Ocean etc, you can setup your own VPN tunnel with something like Wireguard and provide a IPv6 prefix over the tunnel. You could also do this with 6in4 but at this point, if you've gone that far, you might as well have native IPv6.

3. **Configure 6in4 on another independent WAN link** - Multihoming is becoming more common and it's not just in the enterprise world anymore. We know that the 6in4 issues are specifically related to Virgin Media, so there is nothing stopping you from having a tunnel point to an IP address on another internet connection on the same router, if you happen to have multiple internet connections.

There is however one major issue with all of these solutions, they'll cost you money in addition to your existing Virgin Media contract. You will need to weight up how much is it worth to have performant IPv6 vs not at all or putting up with poor 6in4 performance and living with it. Great options right?!

## The real solution is IPv6 (No, really)

The simple solution to fix all of this complicated mess is for Virgin Media to deploy IPv6, which seems obvious when you say it. If this happened, the 6in4 problem goes away because no one would need 6in4 anymore. Unfortunately, this has been the catch 22 problem from the beginning. There are several issues which essentially create an ironic recursive loop scenario.

* Virgin Media won't deploy IPv6 in a hurry (Native IPv6 not possible)
* A free and common transitional IPv6 technology performs poorly on Virgin Media (That's the free IPv6 solution out)
* Other IPv6 solutions require additional cost, time and additional network complexity (The biggest slap in the face is the cost)
* Go back to the first problem and repeat

## Tell Virgin Media what you think about the lack of IPv6

Historically Virgin Media have been resistant to deploy IPv6. The general view appears to be that they don't see any business or customer benefits to do it. While that might be true to a degree and has been one of the major issues with getting providers to roll out IPv6, some of their major competitors like BT and Sky, deployed IPv6 years ago with little fuss. Equally, Virgin Media will have to deploy IPv6 at some point, because it is the future, like it or not. Therefore, the only option we have as customers is to make Virgin Media listen. If they get enough noise from customers about IPv6, they might just start to pay more attention, instead of disregarding it as they have done for over 10 years. While a lot of Virgin Media customers won't know or even care about IPv6, the people that do have a responsibility to at least make Virgin Media listen and convince them that the time is now!

**Time to spread the word**