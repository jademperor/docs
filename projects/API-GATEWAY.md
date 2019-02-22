# API Gateway

* [Quick start](#quick-start)
* [Noun explanation](#noun-explanation)
* [Installation](#installation)
* [Custom plugin](#custom-plugin)
* [Restful API Docs](#restful-api-docs)

## Quick Start

```sh
# clone quick-start repo
git clone git@github.com:jademperor/quick-start.git
cd quick-start

# prepare and start simple http api server
go run pre/prepare.go
go run servers/servers.go

# start gateway-manager and apiproxier
cd bin/{platform}
./apiproxier -addr=:9000 -etcd-addr=http://node1.example.com:2379 -etcd-addr=http://node2.example.com:2379 &
./gateway-manager -addr=:8999 -etcd-addr=http://node1.example.com:2379 -etcd-addr=http://node2.example.com:2379 &

# request for testing
curl -X GET http://localhost:9000/example/name
```

## Installation

* prerequisite
    * [ETCD](https://github.com/etcd-io/etcd#getting-started)
    * go 1.8+ (only while compiling yourself; dev with `go 1.11`)

* download binary files
    * gateway-manager, goto [download](https://github.com/jademperor/gateway-manager/releases)
    * apiproxier, goto [download](https://github.com/jademperor/api-proxier/releases)

* run it
    * gateway-manager:
    ```sh
    ./gateway-manager -h
    -addr string
            the addr http api server listen and serve on, default = 8999 (default ":8999")
    -debug
            set debug mode on, default not open debug mode (false)
    -etcd-addr value
            set etcd endpoints to connect to etcd store
    -logpath string
            the folder directory what log files would be stored at (default "./logs")
    ```

    * apiproxier:
    ```sh
    ./apiproxier -h
    -addr string
            http server listen on (default ":9000")
    -etcd-addr value
            addr of etcd store
    -logpath string
            log files folder (default "./logs")
    ```
* then [CONFIG](./config.md) and use it.

## Noun explanation

1. `Cluster` is a set of Server Instance;
2. `Server Instance` is a available server instance;
3. `API` is a config about redirect `a request` that are sent to proxy to the server instance;
4. `Routing` is a config to forwards `requests` with certain characteristics to the specified `Cluster`;

## Custom Plugin

[click to redirect](https://https://github.com/jademperor/custom-plugin-demo)

## [Restful API Docs](./restful-api-docs.md)
