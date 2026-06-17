# Free Proxy List (auto-updated)

Automatically scraped from **open sources** (GitHub raw lists, public APIs,
free proxy web portals) and **strictly verified** by direct TCP connection
test — the same method used by every web-based proxy checker (including
proxyscrape.com/online-proxy-checker): we simply open a test URL **through**
the proxy and accept only those that respond with HTTP 200.

## Repository contents

| File               | Protocol | Format        |
|--------------------|----------|---------------|
| `proxies/http.txt`   | HTTP    | `ip:port`     |
| `proxies/https.txt`  | HTTPS   | `ip:port`     |
| `proxies/socks4.txt` | SOCKS4  | `ip:port`     |
| `proxies/socks5.txt` | SOCKS5  | `ip:port`     |
| `proxies/all.txt`    | ALL     | `ip:port`     |

Each file contains one proxy per line, sorted, deduplicated.

## Sources (all public / open)

- **GitHub raw** (auto-updated by bots every 10–60 min):
  TheSpeedX/PROXY-List, TheSpeedX/SOCKS-List, ShiftyTR/Proxy-List,
  monosans/proxy-list, hookzof/socks5_list, clarketm/proxy-list,
  mmpx12/proxy-list, roosterkid/openproxylist, Zaeem20/GRABBER,
  proxifly/free-proxy-list, officialputuid/tools, jetkai/proxy-list,
  rdavydov/proxy-list, HyperBeats/proxy-list, BobaHolic/active-proxy,
  ObcbO/Fastest-Proxy, vakhov/fresh-proxy-list, UptimerBot/proxy-list,
  prxchk/proxy-list, ErcinDedeoglu/proxies, caliphdev/Proxy-List,
  saisuiu/Lion00, Anonym0usWork12/Proxy-List, elliot3112/ProxyList,
  Vann-Dev/proxy-list, proxy4parsing/proxy-list, sunny9577/proxy-list
- **Public APIs**:
  api.proxyscrape.com, proxy-list.download, proxyspace.pro, pubproxy.com,
  openproxy.space, proxylist.geonode.com
- **HTML portals**:
  free-proxy-list.net, sslproxies.org, us-proxy.org, socks-proxy.net,
  proxyscrape.com/free-proxy-list, openproxy.space/list
- **Dynamic list-of-sources** (scrapers that themselves index other lists):
  TeaByte/proxy-scraper, itsanwar/proxy-scraper-ak, sakha1370/OpenRay,
  roosterkid/openproxylist, sunny9577/proxy-scraper

## How verification works

Under the hood every proxy checker (web-based or CLI) does the same thing:
it tries to fetch a known URL **through** the proxy and checks the response.
We do exactly that — for each candidate proxy:

1. Open a TCP/HTTP(S) request to `http://httpbin.org/ip` (or HTTPS variant)
   routed through the proxy.
2. Accept the proxy only if we get HTTP 200 within 6 seconds.
3. SOCKS4/SOCKS5 are tested via PySocks (`socks4://` / `socks5://` schemes).
4. Checking is parallel (200 workers), in batches of 100/200/500.

This is **stricter** than relying on a third-party website, because we
control the timeout, the test URL, and we never leak the proxy list to
a third party.

## Schedule

- **Every 5 minutes** — `refresh`: scrape new candidates from all sources,
  verify, push updated lists to GitHub.
- **Every 7 minutes** — `recheck`: re-verify every proxy currently in the
  lists, **drop dead ones**, push the cleaned lists.

Invalid proxies are removed automatically. New proxies are added in batches
of 100 / 200 / 500 depending on how many were found in this cycle.

## Last update

See commit history — every push carries a timestamped commit message.

## License

MIT — see [LICENSE](LICENSE).

## Disclaimer

Use responsibly and in accordance with the laws of your jurisdiction and the
terms of service of the sites you access. The maintainer is not responsible
for any misuse.
