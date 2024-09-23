编译，和执行步骤:
1. 安装go1.21.0：
    1.1. sudo apt-get update
    1.2. wget https://go.dev/dl/go1.21.0.linux-amd64.tar.gz
    1.3. sudo tar -xvf go1.21.0.linux-amd64.tar.gz
    1.4. sudo mv go /usr/local
    1.5. export GOROOT=/usr/local/go
    1.6. export GOPATH=$HOME/go
    1.7. export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
    把以上export设置，放入$HOME/.bashrc文件最后几行
    注意：如果使用Ubuntu22里面apt自带的go，则其版本是1.18,在编译clash-core的过程中会报告版本不兼容的错误，经过测试go1.21的版本能够顺利编译成功，其他更高的版本，并没有测过。
2. 编译出可执行文件：
    git clone https://github.com/clockzhong/clash-core.git
    cd clash-core
    根据自己要编译的目标代码要运行的平台选择编译target，比如
    make linux-amd64
    表示要编译在操作系统linux，CPU是X86-64位系统上运行的可执行文件
    make windows-amd64
    表示要编译在操作系统windows，CPU是X86-64位系统上运行的可执行文件
    操作系统的选择有:darwin/linux/freebsd/windows
    cpu的选择有:amd64/arm64/386/armv5/armv6/armv7/arm64/mips/mipsle/mips64/mips64le/riscv64/loong64
    操作系统和CPU的组合并非自由充分组合，有些组合是不支持的，详情参看Makefile的内容。
3. 准备Country.mmdb：
    wget https://cdn.jsdelivr.net/gh/Dreamacro/maxmind-geoip@release/Country.mmdb
    然后把这个文件复制到与可执行文件，比如clash-linux-amd64， clash-windows-amd64.exe相同的路经下
4. 准备clash配置文件，比如config.yaml
5. 把可执行文件clash-linux-amd64， 配置文件config.yaml，Country.mmdb，一共三个文件放置到一个路经下，执行如下:
    ./clash-linux-amd64 -f config.yaml -d .
    或者
    clash-windows-amd64.exe -f config.yaml -d .

        clock
        2024/09/23
