# Fail2Ban IP Observations Feed

A public, automatically maintained feed of IP addresses observed and banned by Fail2Ban on a self-hosted server.

The feed collects ban events from multiple Fail2Ban jails protecting SSH and web services. It is intended for security monitoring, threat research, and optional integration into defensive tools.

## Repository contents

| File | Description |
|---|---|
| [`lists/ipv4.txt`](lists/ipv4.txt) | Observed IPv4 addresses, one per line |
| [`lists/ipv6.txt`](lists/ipv6.txt) | Observed IPv6 addresses, one per line |
| [`data/observations.jsonl`](data/observations.jsonl) | Observation metadata in JSON Lines format |

### Observation metadata

Each line in `data/observations.jsonl` represents an IP address and includes:

- `ip`: IP address observed by Fail2Ban.
- `first_seen`: First observation recorded by this feed.
- `last_seen`: Most recent recorded ban event.
- `jails`: Fail2Ban jails that have recorded the IP.
- `events`: Number of ban events recorded by the feed.

Timestamps use UTC in ISO 8601 format.

## Retention policy

Observations are retained for up to **90 days after the last recorded ban event**. When an IP is observed again, its `last_seen` timestamp is updated.

An IP may be removed manually if it was banned by mistake. Removal from this repository does not guarantee that the address is absent from other security feeds or blocklists.

For imported bans that predate the feed, the original ban time may be unavailable. In such cases, the initial observation timestamp represents when the address was imported, not necessarily when the original ban occurred.

## Data collection and updates

The feed is generated from Fail2Ban events on a self-hosted server. Updates are published automatically to GitHub on a scheduled basis.

The data reflects the configuration, logs, and ban decisions of that server. It is not a universal threat-intelligence source, and an observed address is not necessarily malicious in every context.

## Responsible use

**Use this feed as an additional security signal, not as definitive proof of malicious activity.**

- Review addresses and context before applying blocks.
- Consider false positives, shared IP addresses, NAT, VPNs, proxies, and cloud infrastructure.
- Avoid using the feed as the sole basis for critical access-control decisions.
- Validate the data and your own security requirements before integrating it into production systems.

No guarantee is made that every listed address is malicious, that the feed is exhaustive, or that every address remains harmful.

## Privacy

This repository publicly shares IP addresses observed and banned by Fail2Ban, together with observation timestamps and the names of the reporting jails.

The feed is limited to security-related observation metadata.

An IP address appearing in this feed indicates that it was observed and banned by the configured Fail2Ban rules. It does not, by itself, prove malicious activity or identify a specific person.

## License

This project is licensed under the MIT License.

You are free to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the software, subject to the terms and conditions of the MIT License.

Please refer to the LICENSE file for the full license text.
