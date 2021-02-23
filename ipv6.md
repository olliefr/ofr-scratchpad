# IPv6

Start the server on _localhost_, which is IPv6 `::1`, port `8080`.

```shell
python3 -m http.server 8080 --bind ::1
```

Connect to the server. According to the RFC, literal IPv6 addresses in URLs should be enclosed in `[ ]`.

```shell
curl http://[::1]:8080
```
