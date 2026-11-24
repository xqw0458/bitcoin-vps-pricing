# Buy VPS with Bitcoin: What Does It Cost per Hour, How Fast Does Payment Clear, and Which Plan Fits a Node or a VPN? (Evoxt's Plan Table, Priced)

Paying for a VPS in bitcoin works roughly the same everywhere: send BTC to the deposit address on the checkout page, wait for the first on-chain confirmation, then spend the credited balance on a server. The confirmation is the slow part, usually 10 to 20 minutes, and deployment after that takes seconds. Entry prices across the market sit between about $0.014 and $0.018 per hour, or $3.50 to $10 a month for the smallest instance.

Evoxt, the provider behind the console link on this page, publishes 11 plans starting at $3.49/month for 1 vCPU, 512 MB RAM and 5 GB of storage, and its FAQ lists Bitcoin among accepted payment methods next to cards, PayPal and USDt on Tron. What follows is the full plan table, an honest account of what happens between "send" and "root access", the disk and bandwidth math for node runners, and the cases where Evoxt's monthly billing is the wrong shape for your project.

> **Quick pick:** a WireGuard exit, jump box or test server runs fine on VM-0.5 at $3.49/mo. If the box will hold Bitcoin chain data, start at VM-2 (2 vCPU, 4 GB RAM, 30 GB storage, 600 GB transfer, $11.99/mo). A pruned node's chain data runs to about 20 GB, which leaves nothing spare on a 20 GB disk once the OS is on it.
>
> 👉 [See Evoxt's current plans and prices](https://bit.ly/EvoXt)

## Every Evoxt plan, side by side

All CPUs are listed as running up to 6.0 GHz, and every plan ships with a weekly offsite backup at no extra cost. Storage is the advertised disk allocation, and traffic is metered rather than unlimited.

| Plan | vCPU / RAM | Storage | Transfer/mo | Price (USD/mo) | Order |
| --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 core / 512 MB | 5 GB | 150 GB | $3.49 | [Order VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core / 1 GB | 10 GB | 250 GB | $4.99 | [Order VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 core / 2 GB | 20 GB | 300 GB | $5.99 | [Order VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores / 2 GB | 20 GB | 300 GB | $6.95 | [Order VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 cores / 4 GB | 30 GB | 600 GB | $11.99 | [Order VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 cores / 4 GB | 30 GB | 700 GB | $14.99 | [Order VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 cores / 8 GB | 60 GB | 1000 GB | $23.99 | [Order VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 cores / 8 GB | 60 GB | 1250 GB | $29.99 | [Order VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 cores / 16 GB | 80 GB | 2000 GB | $47.99 | [Order VM-8](https://bit.ly/EvoXt) |
| VM-12 | 16 cores / 16 GB | 80 GB | 2500 GB | $60.95 | [Order VM-12](https://bit.ly/EvoXt) |
| VM-16 | 16 cores / 32 GB | 100 GB | 4000 GB | $95.99 | [Order VM-16](https://bit.ly/EvoXt) |

Extra IPv4 addresses are $3/month each. One inconsistency is worth flagging before you budget: Evoxt's card-payment page lists the entry plan at $2.99 while its pricing page lists $3.49. Read the invoice at checkout rather than either marketing page.

## What happens between sending BTC and getting root

Evoxt bills through invoices and account credit. You can prepay monthly up to three years, or top up credits and let the system draw against future invoices. The practical sequence is: pay the invoice or fund the balance, wait for confirmation, deploy. Four details decide whether that goes smoothly.

**Confirmation count.** Evoxt does not spell out how many confirmations it waits for before crediting a crypto payment. The norm across hosts that publish the number is one confirmation for small amounts, which is 10 to 20 minutes of Bitcoin block time. bithost credits after a single confirmation and says so explicitly; NoctHost credits small top-ups after the first confirmation, roughly 10 minutes. Altcoins settle faster, usually under five minutes, so if you are in a hurry and the checkout offers Litecoin or a stablecoin on a fast chain, that is the lever.

**Minimum top-up.** bithost and NoctHost both set a $20 floor, VPSWolf sets $25. Evoxt's public pages do not state a minimum for credit top-ups, so check the amount field before you send.

**Refunds.** NoctHost states plainly that top-ups are final and the balance is not refundable. VPSWolf's prepaid model works the same way. On-chain payments cannot be reversed by the sender regardless of policy, and Evoxt does not publish a crypto refund policy on its public pages. Send a small test amount first if you plan to fund a large balance.

**Billing while idle.** Hourly hosts bill for as long as a server exists, powered on or off; bithost says this outright and tells you to delete what you no longer need. Evoxt's invoice model changes the shape of the trap rather than removing it: a three-day experiment on a $3.49 monthly plan costs the full $3.49, so there is no reason to leave an idle VM running past the point you need it.

👉 [Compare Evoxt's plan sizes before you fund the account](https://bit.ly/EvoXt)

## Bitcoin is pseudonymous, which is not anonymity

Every Bitcoin transaction stays visible on a public ledger. VPSWolf is one of the few hosts that says this on its own sales page: BTC payments are pseudonymous and traceable, and Monero is the stronger choice if unlinkable payments matter. That is worth taking seriously, because the usual way a deposit address gets tied to a person is a withdrawal record from a KYC exchange.

What the private-hosting routine actually buys you is distance from your bank and your card issuer, not invisibility on-chain. bithost generates a fresh deposit address for every top-up and recommends a privacy coin plus a dedicated email address for stronger separation. The email is the identity most of these providers hold. bithost will close an account without notice if you register with a disposable email domain, so use a real mailbox you control rather than a throwaway.

For Evoxt specifically, third-party documentation of the signup flow says registration asks for a name and email address and nothing more. Whether a payment triggers any additional check is not documented, so treat that as unconfirmed rather than settled.

## Sizing the server to the job, not the spec sheet

Disk and transfer decide most of these purchases. CPU matters less, with one exception covered below.

A pruned Bitcoin node validates every rule while keeping roughly 20 GB of chain data, so 30 GB of total disk is the realistic floor once the OS takes its share. A full archival node needs the whole chain, which bithost puts at around 700 GB and VPSWolf sizes at 800 GB. Evoxt's largest plan carries 100 GB, so an archive node does not fit anywhere in this lineup; pruned is the only option, and it pushes you to VM-2 or VM-3.

BTCPay Server needs a node backend on the same box, so size it like a pruned node and lean toward VM-4's 60 GB if you also want room for backups and logs. A Lightning node cares about uptime more than storage, which makes VM-1 or VM-2 sufficient. A WireGuard or OpenVPN exit is the lightest workload here and VM-0.5 handles it. Trading bots want a fixed IP for exchange allow-lists and very little else, so the cheap end works.

Transfer deserves more attention than it usually gets. The smallest plan allows 150 GB a month and VM-1 allows 300 GB, while syncing a node pulls the full chain over the wire even in pruned mode. A few hundred gigabytes of initial block download sits badly against a 300 GB allowance, which is the real argument for syncing on VM-2 (600 GB) or VM-3 (700 GB) and then resizing down if the panel supports it.

The exception where CPU matters: initial block download is bound by disk speed, network throughput and single-core work verifying signatures. Evoxt's pitch is clock speed up to 6.0 GHz per core rather than core count, which is the right shape for signature verification and the wrong shape for nothing much else in this list.

👉 [Pick an Evoxt plan with enough disk and transfer](https://bit.ly/EvoXt)

## Where the reseller route differs

DigitalOcean, Vultr and Linode do not take Bitcoin directly. bithost and BitLaunch exist to sit in between: you pay the intermediary in crypto, and it holds the provider account. That convenience has a stated price. bithost's own FAQ says it is more expensive than buying directly from those three, to cover the risk of converting crypto back to USD, bank taxes and operating costs. BitLaunch runs first-party KVM hardware as well as reselling the same three providers, with zero-confirmation payments and a claimed 99.95% uptime.

What the margin buys is location choice and provider hardware: Vultr alone covers 32 regions and 512 MB to 96 GB of RAM, and Windows is only available on the Vultr leg at bithost. Evoxt removes the middleman and sells its own VMs with weekly offsite backups bundled.

On price per gigabyte of RAM, Evoxt is competitive at the low end. VM-1 gives 2 GB for $5.99/mo with 20 GB of disk and 300 GB of transfer. VPSWolf's Cub matches the RAM at $5/mo with 40 GB of storage and unlimited traffic, and NoctHost's Starter charges $18/mo for 2 GB and 50 GB. Where Evoxt loses is disk per dollar and metered bandwidth: the same money buys two to three times the storage at VPSWolf, whose cheapest tier is $3.50/mo for 25 GB.

## Hourly versus monthly, in actual money

Hourly billing means you pay only while a server exists, with no minimum term. To compare it against a monthly price, multiply by 730. NoctHost's $0.014/hr works out to about $10.22/mo, and bithost's $0.018/hr to roughly $13/mo. Evoxt's $3.49/mo entry plan is about $0.0048/hr, which is cheaper per month but commits you to the month.

That gives a clean rule. A server you will keep for two weeks or less is usually cheaper on an hourly host, especially when you factor in the ability to destroy it the moment the job finishes. Anything long-running, such as a node, a BTCPay store or a VPN exit, is cheaper on a monthly invoice, and the hourly model's idle-server billing makes "paused" machines quietly expensive.

## Questions that come up before checkout

**Does Evoxt actually accept Bitcoin?** Yes. Its FAQ lists Bitcoin alongside cards, PayPal and USDt on Tron. A third-party payment check verified BTC, ETH and LTC as of late 2026 and found no USDT listing, which contradicts the Tron mention. Choose the coin shown at your own checkout rather than either list, and never send USDT on the wrong network: an ERC-20 transfer to a TRC-20 address is unrecoverable.

**Is buying a VPS with Bitcoin cheaper than a card?** No. You are billed a USD-equivalent amount and the crypto is converted at the deposit rate, so the server costs the same. The savings are indirect: no foreign transaction fees, no card surcharges, no failed renewal at 3 a.m.

**Can I run a full Bitcoin node?** A pruned node, yes, on a 30 GB plan or larger. A full archival node needs roughly 700 to 800 GB and no Evoxt plan reaches that.

**Can I prepay?** Yes, from monthly up to three years, or as account credit.

## Choosing, in one pass

Only need a tunnel or a small always-on service: VM-0.5 at $3.49. Running a pruned node or a BTCPay backend: VM-2 at $11.99 for the 30 GB disk and 600 GB of transfer. Want headroom for a store, a Lightning node and backups on one box: VM-4 at $23.99. Planning an archival node: none of these plans will hold it, and you should look at a host selling 800 GB instances instead.

Two things to confirm before you send crypto: the minimum top-up Evoxt's checkout asks for, and whether unused credit can be refunded, since that policy is not published. A $5 test payment answers the first question and costs you almost nothing.

👉 [Start with Evoxt's plan list and pick your size](https://bit.ly/EvoXt)
