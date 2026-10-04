# 9proxy adspower: How to Set Up Residential Proxies in AdsPower Profiles, Which Plan Fits Your Profile Count, and Fixes for Failed Proxy Checks

Two questions show up when people search for 9proxy adspower. First: does this combination actually work, or is it one of those integrations that exists on a landing page and nowhere else? Second, and the one that costs real money: which 9Proxy package do you buy when AdsPower is the thing sitting on top of it?

The answer to the first is yes, and there is a documented setup path. The answer to the second is more interesting, because 9Proxy sells two completely different products — per-IP and per-GB — and they behave very differently once you have 20, 200 or 2,000 browser profiles to keep separated. Most guides stop at "paste your host and port." That's the easy part. Picking the wrong billing model is the part that bites.

## What AdsPower expects from a proxy

AdsPower is an antidetect browser built for running many isolated profiles, each with its own fingerprint and its own exit IP. It takes proxies in the plainest possible format: a type, a host, a port, a username, a password. That's it. No plugin, no SDK, no special API.

Because of that, compatibility comes down to three things:

- Protocol. AdsPower accepts HTTPS and SOCKS5. 9Proxy supports HTTP, HTTPS and SOCKS5 through its residential pool, so either option is available on the AdsPower side.
- Authentication. You need either user/pass or an IP whitelist. Which one you get depends on the 9Proxy product you bought.
- IP behaviour. This is where the two 9Proxy models diverge, and where the plan decision actually lives.

9Proxy has an official integration guide for AdsPower that walks through the profile setup, which tells you this is a supported pairing rather than something users reverse-engineered. It sits inside the docs for the GB-based residential product, which is a detail worth noticing — more on that below.

## Before you touch AdsPower

Three things need to exist first.

**A 9Proxy account with a balance on it.** Registration is free; the proxies are not. You can <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank">👉 create your 9Proxy account with the invite code applied</a> and then decide on a package size once you know your profile count.

**A sub-account.** The username AdsPower sends to 9Proxy is built out of sub-account credentials, not your main login. If you haven't created a sub-user, the proxy fields in AdsPower have nothing valid to authenticate against. Create the sub-account first, then generate or forward a proxy.

A note on the invite code: the referral link carries `inviteCode=9P_VIPOFF20`, and 9Proxy's partner terms advertise a 5% discount for users who sign up through a referral. If a discount is active on your order, that's where it comes from — check the order summary before you pay rather than assuming.

**The 9Proxy desktop app, if you're on the per-IP product.** Windows, macOS and Linux builds exist. The per-IP model routes through local port forwarding inside that app, so it isn't optional.

## Adding a 9Proxy proxy to an AdsPower profile

The documented flow, in order:

1. Install AdsPower and launch it.
2. Click **New Profile** from the main dashboard.
3. Open the **Proxy** section inside the new profile.
4. Set **Proxy Type** to HTTPS or SOCKS5, matching your 9Proxy configuration.
5. Fill in **Proxy Host** with the IP address, and **Proxy Port** with the assigned port.
6. Fill in **Proxy Username** using 9Proxy's structured format, and **Proxy Password** with your sub-account password.
7. Click **Check Proxy** to test the connection.
8. Click **OK** to save.

That's the whole setup. No fingerprint settings need adjusting and nothing else in the profile has to change.

## The username string, decoded

The long username is the part people paste wrong. 9Proxy's documented format is:

`<subaccount>-country-<country_code>-st-<state_code>-city-<city_code>-isp-<isp_code>-ssid-<session_id>-sst-<session_time>`

| Field | What it does | Example |
| --- | --- | --- |
| `subaccount` | Your 9Proxy sub-account name | `9proxy` |
| `country` + code | Country-level targeting | `country-US` |
| `st` + code | State or region targeting | `st-CA` |
| `city` + code | City-level targeting | `city-LA` |
| `isp` + code | Carrier targeting | `isp-comcast` |
| `ssid` + value | Session identifier — keeps the same IP for a session | `ssid-phTMYuotAy` |
| `sst` + value | Session duration before rotation | `sst-30` |

The docs' own working example looks like `9proxy-country-US-ssid-phTMYuotAy` against host `38.180.149.107` and port `17521`. You don't need every field — target only what your task requires. If a profile is meant to look like a Los Angeles Comcast household, build the string accordingly; if country-level is enough, stop there and keep the string short enough to debug.

`ssid` is the field that matters most inside AdsPower. It pins one profile to one session. Leave it out and you'll watch a "stable" profile drift across IPs mid-session, which is exactly the signal fingerprint-spoofing is supposed to avoid.

## Per-IP or per-GB — the decision that actually matters

Here's the honest split, taken from 9Proxy's own product comparison:

|  | Residential by IPs | Residential by GB |
| --- | --- | --- |
| Billing unit | Fixed package of IPs | Fixed package of GB |
| Bandwidth | Unlimited while the IP is active | Capped by purchased GB |
| Validity | Unused IPs never expire | 180 days, unlimited on Enterprise |
| IP lifespan | A few hours up to ~24h | Rotates per request or per session |
| Authentication | 9Proxy app with local port forwarding, optional proxy auth | Username/password or IP whitelist |
| Setup | Desktop app required | Works straight from the dashboard |
| Best for | Fixed-IP, account-based work | Automation and high-volume traffic |

For AdsPower specifically:

**Take the per-IP product** when each browser profile needs its own sticky address that stays put for hours — account farming, marketplace sellers, social profiles that log in and stay logged in. The catch is the local port forwarding. AdsPower reads `localhost:port` on the machine where the app is running, which is fine for profiles you open locally. If your team runs profiles somewhere other than the machine running the 9Proxy app, that architecture stops making sense and you'd be better served by the GB-based credentials, which are plain host/port/user/pass from anywhere.

**Take the GB-based product** when profiles rotate aggressively, when per-request traffic is small, and when you want to add a new endpoint without thinking about how many IPs you have left. Rotation is handled per request in rotating mode or per session in sticky mode, and region targeting is baked into the username string instead of the app.

Bundles exist for the case where a single project needs both, and their traffic keeps the 180-day validity window.

## The full plan list

9Proxy raised prices on IP-based and bundle packages on June 1, 2026. GB-based pricing was left alone. Everything below reflects the post-adjustment numbers. These are balance purchases, not subscriptions — you top up, and unused IPs stay in the account.

### Residential Proxy by IPs

| Package | Per-IP price | Total | Buy |
| --- | --- | --- | --- |
| 100 IPs | $0.24 | $24 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Get the 100 IP starter pack</a> |
| 500 IPs | $0.144 | $72 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Grab 500 IPs</a> |
| 1,000 IPs + 500 bonus | $0.084 | $126 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Order 1,000 IPs + 500 free</a> |
| 2,500 IPs | $0.084 | $210 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Take 2,500 IPs</a> |
| 5,000 IPs | $0.072 | $360 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Buy 5,000 IPs</a> |
| 15,000 IPs | $0.048 | $720 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Choose 15,000 IPs</a> |
| 25,000 IPs | $0.035 | $863 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Go with 25,000 IPs</a> |
| 50,000 IPs | $0.029 | $1,438 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Scale to 50,000 IPs</a> |
| 100,000 IPs (Business) | $0.023 | $2,300 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Business package: 100,000 IPs</a> |
| 200,000 IPs (Business) | $0.021 | $4,140 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Business package: 200,000 IPs</a> |
| 500,000 IPs (Business) | $0.018 | $8,625 | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Business package: 500,000 IPs</a> |

### Residential Proxy by GB

| Package | Per-GB price | Total | Validity | Buy |
| --- | --- | --- | --- | --- |
| 5 GB | $3.00 | $15 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Start with 5 GB</a> |
| 50 GB + 5 GB bonus | $2.10 | $105 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Get 50 GB + 5 GB free</a> |
| 100 GB | $1.50 | $150 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Buy 100 GB</a> |
| 200 GB | $1.00 | $200 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Pick 200 GB</a> |
| 1,000 GB | $0.80 | $800 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Order 1,000 GB</a> |
| 2,000 GB | $0.75 | $1,500 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Choose 2,000 GB</a> |
| 3,000 GB (Enterprise) | $0.72 | $2,160 | No expiry | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Enterprise 3,000 GB</a> |
| 6,000 GB (Enterprise) | $0.70 | $4,200 | No expiry | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Enterprise 6,000 GB</a> |
| 10,000 GB (Enterprise) | $0.68 | $6,800 | No expiry | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Enterprise 10,000 GB</a> |

### Bundle packages (IPs + GB)

| Bundle | Contents | Price | Traffic validity | Buy |
| --- | --- | --- | --- | --- |
| Starter | 100 IPs + 5 GB | $30 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Get the Starter bundle</a> |
| Popular | 1,500 IPs + 50 GB | $180 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Get the Popular bundle</a> |
| Pro | 5,000 IPs + 500 GB | $720 | 180 days | <a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank"> Get the Pro bundle</a> |

A data center proxy line is listed as coming soon on 9Proxy's plan overviews; it isn't purchasable yet, so there's nothing to compare.

## What this costs in practice for an AdsPower setup

Do the arithmetic honestly and the per-IP entry tier is not really a per-profile subscription.

$24 buys 100 IP activations. The docs are specific that an IP is deducted when you forward it to a port — so you're spending IPs, not renting 100 addresses forever. Once an IP expires, Auto Refresh swaps in a fresh one and Auto Rotation cycles them on a schedule. Whether you spend the balance quickly depends entirely on how many profiles you keep live and how long you leave them running, so watch the balance for a few days before committing to a bigger tier rather than trusting a rule of thumb.

If you're running ten or twenty profiles at a time, 100 IPs is a low-risk test size. If you're running hundreds and refreshing constantly, the volume tiers are where the price drops — from $0.24 per IP down to under two cents at the top. The 1,000 + 500 bonus tier is the first real step change: $126 for 1,500 IPs works out to $0.084 per IP, less than the 500-IP tier at $0.144.

On the GB side, the useful comparison is the 50 GB + 5 GB pack at $105 against the 5 GB pack at $15. If your browser profiles are mostly staying logged in and idle rather than loading heavy pages, small GB packs go further than you'd expect, which makes the $3/GB entry price less painful than it looks.

> If you only open a handful of AdsPower profiles and keep them idle most of the day, buying 15,000 IPs is money sitting in a balance. Buy the smallest pack that covers a week of work, measure actual consumption, then size up.

## When the proxy check fails

**Wrong type.** AdsPower's HTTPS option and a SOCKS5-configured 9Proxy endpoint don't mix. Match the two.

**Password from the main account instead of the sub-account.** The documented password field is the sub-account password. Using your login password is a silent failure.

**Malformed username string.** A missing hyphen or a country code in the wrong position breaks the whole string, and AdsPower will simply report a failed check. Test the same credentials outside AdsPower if you want to know whether the string or the browser is at fault.

**Expecting `localhost:port` to work from a different machine.** Per-IP plans route through the desktop app. GB-based credentials don't have that limitation.

**An expired IP.** Residential IPs have a natural lifespan of hours to about 24 hours. If a profile that worked this morning fails at 6pm, that's the pool behaving normally — Auto Refresh exists for exactly this.

## What independent reviews say

Geekflare ran 300 requests against the network and logged 293 successes, 2 hard blocks and 5 CAPTCHA challenges, all five from a single IP range that cleared up after rotating away from it. They also flagged two things worth knowing before you buy: there's no self-serve free trial on the site, and coverage is 90+ countries rather than the near-universal list some providers advertise. Their read on 9Proxy's Trustpilot score is that the complaints cluster around the refund policy and mismatched plan choices rather than broken proxies — which argues for testing with the smallest package before scaling.

An older iTWire review makes a related point from the other direction: the mandatory desktop app makes multi-device use less convenient than a browser extension would, and free trials are promotional rather than automatic. Both observations still apply to the per-IP product.

## Questions that come up

**Does 9Proxy work with AdsPower out of the box?**
Yes, and it's documented. AdsPower takes host, port, username and password; 9Proxy's GB-based product supplies all four, and the per-IP product supplies them via local port forwarding.

**Can I use one 9Proxy IP across several AdsPower profiles?**
Technically yes, but it defeats the point of running isolated profiles. One profile, one exit IP.

**Is SOCKS5 better than HTTPS here?**
9Proxy supports both and the pool is residential either way. Pick the protocol your existing workflow already uses; there's no documented performance difference between them in the integration guide.

**How do I pay?**
9Proxy accepts credit cards, bank cards, crypto including USDT, BTC, ETH, LTC and DOGE, plus Alipay, Apple Pay, Google Pay and its own wallet balance. Coupon fields exist at checkout, and coupons are only valid on qualifying product lines — historically the April GB campaign's 9% coupon applied to GB orders only, explicitly not to bundles or IP-based plans.

**Do unused IPs expire?**
Not on the per-IP product. Unused IPs stay in your balance. GB bundles and standard GB packs carry a 180-day validity window, with Enterprise GB packages sold without expiry.

**Is there a free trial?**
No self-serve trial. 9Proxy's team has offered limited trials through community channels depending on availability, and you can always ask support directly — but plan on paying for the smallest pack.

## The short version

The 9proxy adspower setup is a two-minute job: new profile, proxy section, type, host, port, structured username, sub-account password, check, save. The part that deserves your attention is the plan. Sticky per-profile identity points to the per-IP product and its desktop app; rotating, location-scattered automation points to the GB-based credentials that work from anywhere. Test that conclusion with a $24 or $30 pack, watch what your profiles actually burn, and then commit to a tier — because at 500,000 IPs the price is $0.018 each, and at 100 it's $0.24, and the difference between those two numbers is entirely about knowing your own workload first.

<a href="https://9proxy.com/sign-up?inviteCode=9P_VIPOFF20" target="_blank">👉 Open the 9Proxy sign-up page and put your first AdsPower profile on a residential IP</a>
