# TensorFlowのインストール
## 実行環境
RaspberryPi OS Lite 64bit bullseye
## 方法① [Qengineering](https://github.com/Qengineering/TensorFlow-Raspberry-Pi_64-bit)のリポジトリを使う。
[ここ](https://qengineering.eu/install-tensorflow-on-raspberry-64-os.html)を参照。

### 準備
```
sudo apt update
sudo apt upgrade
sudo apt install python3-pip git
sudo apt install libclang-9-dev
sudo -H pip3 install --upgrade protobuf==3.19.6
```
TensorFlowIOを**先に**インストール
```
git clone https://github.com/Qengineering/Tensorflow-io.git
cd Tensorflow-io
sudo -H pip3 install tensorflow_io_gcs_filesystem-0.23.1-cp39-cp39-linux_aarch64.whl
```

### TensorFlowのインストール
```
# install gdown to download from Google drive
sudo -H pip3 install gdown
# download the wheel
gdown https://drive.google.com/uc?id=1G2P-FaHAXJ-UuQAQn_0SYjNwBu0aShpd
# install TensorFlow 2.10.0
sudo -H pip3 install tensorflow-2.10.0-cp39-cp39-linux_aarch64.whl
```