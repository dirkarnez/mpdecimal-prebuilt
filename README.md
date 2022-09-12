mpdecimal-prebuilt
==================
- [libmpdec/libmpdec++ cross compilation](https://www.bytereef.org/howto/mpdecimal/cross-compile.html)
  - ```bash
    sudo apt-get install gcc-arm-linux-gnueabi g++-arm-linux-gnueabi

    tar xvf mpdecimal-2.5.1.tar.gz
    cd mpdecimal-2.5.1

    mkdir arm32
    ./configure --host=arm-linux-gnueabi --prefix=$PWD/arm32
    make
    make install

    # Now copy the relevant files from the ./arm32 directory to the target machine.
    ```
  - ```bash
    sudo apt-get install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu

    tar xvf mpdecimal-2.5.1.tar.gz
    cd mpdecimal-2.5.1

    mkdir arm64
    ./configure --host=aarch64-linux-gnu --prefix=$PWD/arm64
    make
    make install

    # Now copy the relevant files from the ./arm64 directory to the target machine.
    ```
  - ```bash
    # clang also uses the tool chain pulled in by these packages.
    sudo apt-get install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu

    # clang needs its own linker.
    sudo apt-get install lld

    tar xvf mpdecimal-2.5.1.tar.gz
    cd mpdecimal-2.5.1

    mkdir arm64
    ./configure --host=aarch64-linux-gnu --prefix=$PWD/arm64 CC=clang CXX=clang++ \
                CFLAGS="--target=aarch64-linux-gnu --sysroot=/usr/aarch64-linux-gnu" \
                CXXFLAGS="--target=aarch64-linux-gnu --sysroot=/usr/aarch64-linux-gnu -I/usr/aarch64-linux-gnu/include/c++/8/aarch64-linux-gnu" \
                LDFLAGS="--target=aarch64-linux-gnu --sysroot=/usr/aarch64-linux-gnu -fuse-ld=lld" \
                LDXXFLAGS="--target=aarch64-linux-gnu --sysroot=/usr/aarch64-linux-gnu -fuse-ld=lld"
    make
    make install

    # Now copy the relevant files from the ./arm64 directory to the target machine.
    ```
