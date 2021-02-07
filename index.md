---
layout: default
---

**Virgin Media like many UK Internet Service Providers have not yet deployed IPv6. While this isn't major news because loads of ISPs suffer from IPv6 deployment lag (since 1995), Virgin Media UK has an interesting IPv6 story and lots of plot twists which is why I felt I needed to create this page, to inform others who may be looking at IPv6 and happen to be a Virgin Media customer.**

## Summary

Virgin Media UK does not currently have IPv6 however Virgin Media Ireland does just to make it confusing. DS-Lite is used by Liberty Global and Virgin Media inherits this IPv6 transitional technology, because Liberty Global (parent company) likes to deploy it A LOT it seems. Personally DS-Lite can go die in a fire, but that's just me. The focus is IPv6 generally which Virgin Media have a great track record of not having. So we'll focus on that. After all the website domain is specifically aimed at this purpose.

All this information relates to Virgin Media UK Broadband services.

## The unofficial IPv6 event timeline

A summarised list of key IPv6 related events at Virgin Media, completely made up by me as I don't work for them and after creating this little site, have likely zero chance of doing so either. Nevermind.

* **March 2010**: [The IPv6 mega thread was born](https://community.virginmedia.com/t5/QuickStart-set-up-and/IPv6-support-on-Virgin-media/td-p/35748) on the Virgin Media Community Forums. The original thread asked a simple question, when will Virgin Media deploy IPv6? The answer: "When we are ready". Over 10 years later, Virgin Media still aren't ready...
* **October 2014**: First appearance and presentation at the UK IPv6 council.
* **September 2015**: Second appearance at the UK IPv6 council.
* **August 2017**: ISPreview reveals there is a super “secret” IPv6 trial for 100 members of Virgin Media’s own staff. The first hint of serious activity related to IPv6 beyond Virgin Media’s own network engineers and testnet.
* **February 2018**: Liberty Global (parent company of Virgin Media) released some interesting information about Virgin Media and it’s plans for DOCSIS 3.1 and IPv6 adoption (spoiler, didn't happen). At this point it became known that Virgin Media UK had chosen Benu Networks DS-Lite solution for their IPv6 rollout.
* **June 2018**: A wider customer trial was reported to be underway and judging by the APNIC IPv6 stats for Virgin Media’s AS number during that period, this seemed to involve a sizable amount of IPv6 testing. Granted, not all of numbers may have been residential broadband customers, but none the less there was all of sudden a lot of IPv6 traffic being recorded when there was pretty much zero from Virgin Media prior.
* **December 2018**: Third appearance at the UK IPv6 council, with some additional information about the wider IPv6 test currently happening and further information about DS-Lite. Hints of an IPv6 rollout in 2019.
* **2019**: No IPv6 rollout happens. IPv6 activity on the Virgin Media AS goes quiet.
* **2020**: Nothing happened (Besides a global pandemic)
* **2021**: YOU ARE HERE

## IPv6 tunnels

If you are into networking or technicial, you'll know that just because some providers don't have IPv6, doesn't mean you can't get IPv6 another way. Many ISPs not deploying IPv6 means users who want it turn to other solutions, mainly tunnels, most commonly 6in4. If it wasn't insulting to not have native IPv6 from your ISP, Virgin Media decides to play the ultimate checkmate and specifically screws around with certain protocols in their network. They'll deny it, but there is evidence to prove otherwise. Guess what protocol is hampered by this? YEP. 6in4. NICE.

It has long been documented that running a 6in4 tunnel from a provider such as Hurricane Electric results in horribly slow speeds that look to be "capped". Virgin Media will state there is no speed caps on any protocol on the unlimited broadband services, but I call shenanigans. Here's why.

One day I decided that I would investigate what was going on here, because I'd put up with the issue for so long myself and couldn't find any detailed information around the subject, I decided to be the IPv6 hero and investigate for great protocol justice. We live in a society where everyone should be treated equally, so should protocols! I ended up documentating my findings which has attracted the attention of other users who were in similar situations as well as Virgin Media iself (HI!).

[The full article and analysis of 6in4 IPv6 on Virgin Media](https://jamesmacwhite.medium.com/is-virgin-media-traffic-shaping-protocol-41-6in4-ipv6-c1b8b6e645f7)

**If you can't be bothered to read the article. No worries, here's the TL;DR highlights**

1. When a 6in4 tunnel is pointed at a Virgin Media IP, the performance is awful. This is well known. (This include Virgin Media Business as well by the way)
2. If you encapsulate 6in4 over something like UDP, suddenly the problem goes away. Plot twist.
3. If you have a 6in4 tunnel pointed to a non Virgin Media IP, you'll not have any issues either

So two points are clear:

1. Virgin Media is the problem (We kind of knew this, but confirmation is always nice)
2. Encapsulating 6in4 within another protocol seems to avoid the performance issues

L2TP, UDP, Wireguard you name it, if you send 6in4 over that, you'll not see the same problem. So about that not throttling traffic thing...

No one knows for sure because Virgin Media deny any discussion around throttling, however you read the full details and tests done to show the speed issues and make up your own mind. We are unlikely to ever get an official detailed explanation of why anyway.