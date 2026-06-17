# Free Proxy List (auto-updated)

Auto-scraped from **open sources** (GitHub raw lists, public APIs, free proxy
web portals) and **strictly verified** by direct TCP/HTTP connection test —
the same method used by every web-based proxy checker (including
proxyscrape.com/online-proxy-checker): we open a test URL **through** the
proxy and accept only those that respond with a valid HTTP status.

## Files

| File               | Protocol | Format    |
|--------------------|----------|-----------|
| `proxies/http.txt`   | HTTP    | `ip:port` |
| `proxies/https.txt`  | HTTPS   | `ip:port` |
| `proxies/socks4.txt` | SOCKS4  | `ip:port` |
| `proxies/socks5.txt` | SOCKS5  | `ip:port` |
| `proxies/all.txt`    | ALL     | `ip:port` |

One proxy per line, sorted, deduplicated.

## Sources

**~30 GitHub raw lists** (auto-updated by bots every 10–60 min):
TheSpeedX/PROXY-List, TheSpeedX/SOCKS-List, ShiftyTR/Proxy-List,
monosans/proxy-list, hookzof/socks5_list, clarketm/proxy-list,
mmpx12/proxy-list, roosterkid/openproxylist, Zaeem20/GRABBER,
proxifly/free-proxy-list, officialputuid/tools, jetkai/proxy-list,
rdavydov/proxy-list, HyperBeats/proxy-list, BobaHolic/active-proxy,
ObcbO/Fastest-Proxy, vakhov/fresh-proxy-list, UptimerBot/proxy-list,
prxchk/proxy-list, ErcinDedeoglu/proxies, caliphdev/Proxy-List,
saisuiu/Lion00, Anonym0usWork12/Proxy-List, elliot3112/ProxyList,
Vann-Dev/proxy-list, proxy4parsing/proxy-list, sunny9577/proxy-list.

**Open APIs**: api.proxyscrape.com, proxy-list.download, proxyspace.pro,
pubproxy.com, openproxy.space, proxylist.geonode.com.

**HTML portals**: free-proxy-list.net, sslproxies.org, us-proxy.org,
socks-proxy.net, proxyscrape.com/free-proxy-list, openproxy.space/list.

**Dynamic list-of-sources** (scrapers that index other lists):
TeaByte/proxy-scraper, itsanwar/proxy-scraper-ak, sakha1370/OpenRay,
roosterkid/openproxylist, sunny9577/proxy-scraper.

## How verification works

Every proxy checker (web or CLI) does the same thing under the hood: it
tries to fetch a known URL **through** the proxy and checks the response.
We do exactly that:

1. For each candidate, try multiple test URLs (`httpbin.org/ip`,
   `ip-api.com/json`, `azenv.net/`, `api.ipify.org`).
2. Accept the proxy if any URL responds with HTTP 200/204/301/302/401/403/503
   within 6 seconds.
3. SOCKS4/SOCKS5 tested via PySocks (`socks4://` / `socks5://` schemes).
4. Parallel checking (200 workers), in batches of 100/200/500.

## Schedule (run on your VPS via cron)

- **Every 5 min** — `refresh`: scrape → verify → push to GitHub
- **Every 7 min** — `recheck`: re-verify existing → drop dead → push

Invalid proxies are removed automatically; new ones added in batches.

## Deploy on your VPS

```bash
git clone https://github.com/kevinriverrrr-sudo/free-proxy-list.git
cd free-proxy-list
pip install -r requirements.txt
cp .env.example .env
# edit .env: put your GITHUB_TOKEN and GITHUB_OWNER
crontab -e
# add:
#   */5 * * * * cd /path/to/free-proxy-list && python3 proxy_scraper.py refresh  >> cron.refresh.log 2>&1
#   */7 * * * * cd /path/to/free-proxy-list && python3 proxy_scraper.py recheck >> cron.recheck.log 2>&1
```

## License

MIT — see [LICENSE](LICENSE).

## Disclaimer

Use responsibly and in accordance with the laws of your jurisdiction and the
terms of service of the sites you access. The maintainer is not responsible
for any misuse.
