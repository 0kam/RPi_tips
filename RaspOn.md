# [RaspOn](https://www.nekorisu-embd.com/ras_p-on_products.html)の設定
## テスト環境
- RaspberryPi 4B 4GB
- RaspberryPi OS Lite 64bit bullseye

## ソフトウェアのインストール
以下、[公式マニュアル](https://www.nekorisu-embd.com/download/Ras_p-On_Users_Manual-Rev4.pdf)から抜粋
- `raspi-config`でi2cを有効化し、LocaleとTimeZoneを設定
- 以下を実行
```
sudo apt install i2c-tools
# fake-rtcを削除
sudo apt-get remove fake-hwclock
sudo dpkg --purge fake-hwclock
＃作業用のフォルダを用意します。
mkdir raspon
cd raspon
＃インストーラーをサイトからダウンロードし解凍します。
wget https://www.nekorisu-embd.com/download/raspon-installer.tar.gz
tar xzpvf raspon-installer.tar.gz
＃インストールを実行します。
sudo apt update
sudo ./install.sh
```
