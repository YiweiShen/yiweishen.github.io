---
title: SNI in TLS Handshake
date: 2026-11-07 10:41:50
tags:
---

When a client performs a TLS handshake with a server, it sends a piece of information called SNI (Server Name Indication).

Why does it do this? Because a single server can easily host several different TLS certificates on the same IP. If the client doesn't say "who I'm looking for" during the handshake, the server is left clueless: with so many certificates on hand, which one should it present?

<!-- more -->

## Let's Walk Through the Timeline

1. **DNS lookup**: Translate the domain name into an IP address.
2. **TCP three-way handshake**: Knock on port 443 of that IP.
3. **TLS handshake**: Negotiate encryption parameters and verify the certificate. SNI is tucked into the ClientHello in this step, the key moment where the client "announces who it is looking for."
4. **HTTP request**: Now data can finally be sent safely through the encrypted channel.

## From the ISP's Point of View

Start with the DNS lookup. It's usually plaintext, so the ISP can see right through it. Even if you use encrypted DNS, the ISP can still see that you're talking to some DNS server, though it may not know what exactly you asked. This kind of traffic is generally let through. The TCP handshake is the same: nothing special about it, and it's usually let through as well.

So here's the question: if an ISP wants to block certain domains, or only allow domains on a whitelist, where does it start?

The answer is the first step of the TLS handshake, using SNI to determine your destination. The moment the client initiates a TLS handshake, it is, in the ISP's eyes, loudly announcing: "I'm going to visit such-and-such website!" Whether to let it through is entirely up to the ISP's policy.

> As for ECH (Encrypted ClientHello), let's set it aside for now.

Interrupting your connection isn't hard either, and can be done by tampering in the middle: send a TCP RST to each side of the communication, or simply drop packets and leave you waiting.

## SNI Spoofing: Putting on a Disguise

Now let's look at it from the proxy side, and see why SNI spoofing works.

The key is that you have a middleman VPS: traffic goes to the VPS first, and the VPS then forwards it to the real destination. So when establishing the TLS connection with the VPS, you're free to set the SNI to any other domain. You're clearly connecting to your own VPS, yet the SNI solemnly declares: "Oh, I'm Google." As a result, what the ISP sees may be you dutifully visiting Google.

So, observing SNI is indeed an effective means of traffic control. Overall, yes.

## But SNI Wasn't Made for This

I want to stress that SNI was never designed for traffic identification or access control, so being pressed into this job comes with plenty of limitations.

### Scenario 1: Better Safe Than Sorry Firewalls

For ISPs or firewalls that would rather wrongly block a thousand than let one slip through, if the SNI you claim is too famous, such as Microsoft or Google, they will likely get suspicious and go a step further, checking whether the destination IP belongs to a known data center or hosting provider, and then decide whether to allow it according to their own policy.

In this case, the relatively safe approach is to use `VLESS/VMess + TLS` with your own domain and certificate, and play it straight.

### Scenario 2: Simple Domain Management Only

Another kind of scenario uses SNI only for simple domain-based access control, such as Wi-Fi on planes and trains: some domains are free to access, while the rest require payment.

In this case, `VLESS + Reality` combined with a modified SNI may be able to bypass this kind of simple SNI-based access control.

---

That's all, just some casual thoughts from a purely technical perspective.
