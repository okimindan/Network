# Si-R G120

- DNSフォワーダを設定。
  - remote0(通信事業者)のDNSにフォワードする。
```
proxydns domain 0 any * any to 0
```

- NAPTの設定
  - グローバルIPアドレスを5分間だけ与える。
```
remote 0 ip nat mode multi any 1 5m
```


## 知識
- remote 0は一般的には通信事業者との情報を設定する。
- 
