# ラズパイをUSB Ether gadgetでPC（Linux）につなぐ
## Step 1. コンフィグファイルの編集
Raspberry Pi OS (Lite bullseye 64bitを使用)をSDカードに焼いたあと、SDカードの/boot以下に入っているconfig.txtとcmdline.txtをPCのから編集する。

まず、cmdline.txtの末尾に以下を挿入。
```
modules-load=dwc2,g_ether g_ether.host_addr=a6:34:44:45:00:2c g_ether.dev_addr=3e:b9:c9:06:f4:4d
```
ここで指定したMACアドレスはなんでも良い。MACアドレスを指定しないとランダムに変わってしまい、後に接続した際、毎回インターフェース名が変わって煩わしい。

次に、config.txtの末尾に、新しい行として`dtoverlay=dwc2`を追加する。

## Step 2. 接続先のPCでのインターフェース名の設定
先程`g_ether.host_addr`で設定したMACアドレスをUDEVに登録する。
`/etc/udev/rules.d`に`99-rpi-usb-ether.rules`のような名前のファイルを作成し、以下を書き込む。
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="a6:34:44:45:00:2c", NAME="rpi-usb-ether0"
```

## Step 3. Network Managerの設定
`nmcli`で以下を設定する。
```
nmcli con add type ethernet con-name rpi-usb0 ifname rpi-usb-ether0
nmcli con modify rpi-usb0 ipv4.method shared
```
Step 2. で設定したデバイスが接続されたらrpi-usb-ether0というインターフェース名を割り当て、「他のコンピュータへの共有」で接続する。これによって、ラズパイはPC経由でインターネットに接続できる。

## Step 4. IPアドレスの確認
ラズパイを接続し、`rpi-usb0`が見えている状態で`nmap -sn 10.42.0.0/24`を実行し、IPアドレスを割り出す。

## 参考
https://qiita.com/otsuka512/items/856032a730ce9d1ec2ae