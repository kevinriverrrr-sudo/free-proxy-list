# Free Proxy List (auto-updated)

Automatically scraped from open sources and **strictly verified** by direct
connection test (the same method used by web-based proxy checkers such as
proxyscrape.com/online-proxy-checker — under the hood every checker just opens
a test URL through the proxy).

## Files

| File        | Protocol | Count |
|-------------|----------|-------|
| `proxies/http.txt`   | HTTP   | 6 |
| `proxies/https.txt`  | HTTPS  | 0 |
| `proxies/socks4.txt` | SOCKS4 | 0 |
| `proxies/socks5.txt` | SOCKS5 | 0 |
| `proxies/all.txt`    | ALL    | 6 |

Each file contains one proxy per line in `ip:port` format.

## Schedule

- **Every 5 minutes**: scrape new proxies from open sources, verify, push to GitHub.
- **Every 7 minutes**: re-verify existing proxies, drop dead ones, push updated lists.

Invalid proxies are removed automatically; new proxies are added in batches of
100 / 200 / 500 depending on how many were found.

## Last update

`2026-06-17 20:17 UTC` (UTC)

## License

MIT — see `LICENSE`.
