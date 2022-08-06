# Installing or upgrading go on WSL2

1. Visit https://go.dev
2. Rigth click on _linux_ link and copy the URL
3. Run `cd ~/downloads`
4. Run `wget <link>` where link is the link you've copied on step 2
5. Follow the remaining instructions from [Go install - Linux](https://go.dev/doc/install)
   5.1. sudo su
6. Basically run `rm -rf /usr/local/go && tar -C /usr/local -xzf go<version>.linux-amd64.tar.gz`
7. Add `/usr/local/go/bin` to the PATH env var (if not present yet)
8. Run `go version`
