# Ubuntu setting (Ubuntu20.04)_210716v
## Chrome install
- save the file >> install
## hangul
1. fctix install
- $ sudo apt-get install fcitx-hangul
2. ibus
- $ sudo apt install ibus-hangul # reboot 해줘야 뜸
- $ ibus-setup # settings

## Document
- $ touch ~/Templates/Document 


## ~/.bashrc 
```
alias eb="sudo gedit ~/.bashrc"
alias sb="source ~/.bashrc"
alias up="sudo apt update && sudo apt upgrade"
```


## NVIDIA Driver
[참고](https://webnautes.tistory.com/1428)
```
$ ubuntu-drivers devices
$ sudo apt install nvidia-driver-460
$ nvidia-smi # install check
$ sudo rm -rf /usr/local/cuda* #기존 cuda remove
```

### CUDA 
- [install](https://developer.nvidia.com/cuda-11.2.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=2004&target_type=runfilelocal)

```
$ wget https://developer.download.nvidia.com/compute/cuda/11.2.0/local_installers/cuda_11.2.0_460.27.04_linux.run
$ sudo sh cuda_11.2.0_460.27.04_linux.run
```
- continue
- accept
- driver 제외 후 install

- ~/.bashrc 설정
```
export PATH=$PATH:/usr/local/cuda-11.2/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.2/lib64
export CUDADIR=/usr/local/cuda-11.2
```
### Cudnn
- [install](https://developer.nvidia.com/rdp/cudnn-archive)
- library for Linux[x86_64]로 다운로드

* Download folder 
```
$ tar xvzf cudnn-11.2-linux-x64-v8.1.0.77.tgz
$ sudo cp cuda/include/cudnn* /usr/local/cuda/include
$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
$ sudo chmod a+r /usr/local/cuda/includ/cudnn.h /usr/local/cuda/lib64/libcudnn*
$ sudo chmod a+r cudnn.h /usr/local/cuda/lib64/libcudnn*
```

* linking 
```
sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_train.so.8.1.0 /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_train.so.8
sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8
sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8
sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8
sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_train.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_train.so.8
sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8.1.0 /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8
sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn.so.8
sudo ldconfig
ldconfig -N -v $(sed's/://'<<<$LD_LIBRARY_PATH)2>/dev/null|grep libcudnn
```
