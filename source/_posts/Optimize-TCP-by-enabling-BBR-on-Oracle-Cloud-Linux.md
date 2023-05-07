---
title: Optimize TCP by enabling BBR on Oracle Cloud Linux
date: 2023-05-07 16:03:12
tags:
---

## Introduction

BBR ("Bottleneck Bandwidth and Round-trip propagation time") aims to improve network performance and reduce latency. BBR estimates the available network bandwidth and the round-trip time (RTT) to adjust the TCP sending rate dynamically, reducing queuing delays and reducing packet loss.

## Prerequisites

Check if your Linux kernel version is 4.9 or higher.

```bash
uname -r
```

## Congestion Control Status

```bash
sysctl net.ipv4.tcp_available_congestion_control
```

If you see `net.ipv4.tcp_available_congestion_control = bbr cubic reno`, then BBR is enabled. You can check it again after we enable BBR.

## Enable BBR

```bash
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sudo sysctl -p
```

The first line enables Fair Queueing (FQ), which is a network scheduler that improves network performance by reducing latency and jitter. The second line enables BBR.

The last line reloads the configuration file for the changes to take effect.

## References

Optimizing HTTP/2 prioritization with BBR and tcp_notsent_lowat:
https://blog.cloudflare.com/http-2-prioritization-with-nginx/

TCP BBR congestion control comes to GCP – your Internet just got faster:
https://cloud.google.com/blog/products/networking/tcp-bbr-congestion-control-comes-to-gcp-your-internet-just-got-faster
