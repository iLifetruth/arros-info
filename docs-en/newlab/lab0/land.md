# Lab 0: Setup RISCV-64 with Rust Toolchain 
⏰ 2020.11.23

> Referred to:  
> 1. https://rcore-os.github.io/rCore-Tutorial-deploy/  
> 2. https://gitee.com/zjuicsr/lab20fall-stu  



## 0. Get Tools🔧 Ready！
```shell
$ sudo apt update 
# Install General tools
$ sudo apt  install         \
            autoconf        \
            automake        \
            autotools-dev   \
            curl            \
            libmpc-dev      \
            libmpfr-dev     \
            libgmp-dev      \
            gawk            \
            build-essential \
            bison           \
            flex            \
            texinfo         \
            gperf           \
            libtool         \
            patchutils      \
            bc              \
            zlib1g-dev      \
            libexpat-dev    \
            git
# Additional dependencies required for QEMU installation
$ sudo apt install libglib2.0-dev libpixman-1-dev pkg-config
```



## 1. Qemu Setup 
### 1.1 Download the Qemu Pakage

+ Download from github::Official QEMU mirror
```shell
$ git clone https://github.com/qemu/qemu.git
```


+ Download from Official QEMU Site
```shell
# Download
$ wget https://download.qemu.org/qemu-5.1.0.tar.xz
# Unpack
$ xz -d qemu-5.1.0.tar.xz
$ tar -xvf qemu-5.1.0.tar
# make & install
# Please make sure that libglib2.0-dev libpixman-1-dev are both installed
$ cd qemu-5.1.0
$ ./configure --target-list=riscv64-softmmu 
$ make -j $(nproc)
$ sudo make install -j $(nproc)
# now cheak your installation
$ qemu-system-riscv64 --version
```

⏰ 2020.11.23
```shell
QEMU emulator version 5.1.0
Copyright (c) 2003-2020 Fabrice Bellard and the QEMU Project developers
```


## 2. Setup the Rust Toolchain 

> You can get rust by visiting https://rustup.rs. 


```shell
$ curl https://sh.rustup.rs -sSf | sh
```

1. If installation is very slow, please use USTC's mirror server.
```shell
$ export RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
$ export RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup
$ curl https://sh.rustup.rs -sSf | sh

# 1) Proceed with installation (default)
# ...
# stable installed - rustc 1.48.0 (7eac88abb 2020-11-16)
# Rust is installed now. Great!

```

2. append  `source ~/.cargo/env` to the `~/.bashrc`

```sh

$ echo "source ~/.cargo/env" >> ~/.bashrc

# To get started you need Cargo's bin directory ($HOME/.cargo/bin) in your PATH
# environment variable. Next time you log in this will be done
# automatically.

# To configure your current shell run source $HOME/.cargo/env
$ source ~/.cargo/env

$ rustc --version
# rustc 1.48.0 (7eac88abb 2020-11-16)
```


3. Change the Chargo's registry
```sh
$ nano ~/.cargo/config
```

```
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"

```


## 3. Rust UP!🐳

⏰ 2020.11.25
### 3.1 Download The Rustling(4.2.0) Exercise

#### 3.1.1 Getting Started
Just run:
```
# 1. Auto run:
curl -L https://git.io/rustlings | bash
# 2. Or if you want it to be installed to a different path:
curl -L https://git.io/rustlings | bash -s mypath/
[To be deteled] #  e.g. 
[To be deteled  # $ curl -L https://git.io/rustlings | bash -s /mnt/hgfs/arros
# 3. Download from the github:
git clone https://github.com/rust-lang/rustlings
cd rustlings
git checkout tags/4.2.0 # or whatever the latest version is (find out at https://github.com/rust-lang/rustlings/releases/latest)
cargo install --force --path .
```