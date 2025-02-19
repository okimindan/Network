# Si-R G120

## IPsec間の通信（mainモード）

- 本社（IPsec用IPアドレス：192.168.101.1(グローバルIP) 実IP:192.168.101.1）
```
remote 0 ip route 0 192.168.101.2/32 1 1
remote 1 ap 0 tunnel local 192.168.101.1
remote 1 ap 0 tunnel remote 192.168.101.2
remote 1 ip route 0 172.16.2.0/24 1 1
```

- 拠点（192.168.101.2　実IP：172.16.2.0/24）
```
remote 0 ip route 0 192.168.101.1/32 1 1
remote 1 ap 0 ike mode main
remote 1 ap 0 tunnel local 192.168.101.2
remote 1 ap 0 tunnel remote 192.168.101.1
remote 1 ip route 0 default 1 1
```
- IPsec用VPNのルートはremote 0
- 実IP用のルートは拠点の定義したremote 1


- （本社コマンド）
```
ether 1 1 vlan untag 1
ether 2 1 vlan untag 2
ether 2 2 vlan untag 2
ether 2 3 vlan untag 2
ether 2 4 vlan untag 2
lan 0 vlan 1
lan 1 ip address 172.16.1.254/24 3
lan 1 ip route 0 default 172.16.1.253 1 1
lan 1 vlan 2
```
- （拠点コマンド）
```
remote 0 ip route 0 default 1 0
```
　→　デフォルトルートで本社に



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
