# Si-R G120

- DNSフォワーダを設定する。
  - remote0(通信事業者)のDNSにフォワードする。
```
proxydns domain 0 any * any to 0
```


## 知識
- remote 0は一般的には通信事業との情報を設定する。
