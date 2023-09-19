# Recommanded Setup

Pure '*nix' environment may be better, but some member of OJ Lab use 'Windows + WSL'.

## Windows

Recommended to build development environment in
[WSL](https://learn.microsoft.com/zh-cn/windows/wsl/) with VSCode remote.

Make sure to have a reliable network to avoid download problems.

### Golang

Install by [brew](https://brew.sh/) with `brew install go`.

You may need to **reopen** VSCode to refresh go environment.
Also, you may need to change go proxy for essential installs `go env -w GOPROXY=https://goproxy.cn`.

#### Add GOPATH to PATH

Add `export PATH="$PATH:$(go env GOPATH)/bin"` to your cli profile,
or you might miss some ability installed by go.

### Docker

Install [docker desktop](https://www.docker.com/products/docker-desktop/) in windows host.
