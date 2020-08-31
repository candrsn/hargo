我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。

<!-- markdownlint-disable MD033 -->

# <img src="./img/hargo-logo.png" height="40"> Hargo

[![Hargo Build Status](https://travis-ci.org/mrichman/hargo.svg?branch=master)](https://travis-ci.org/mrichman/hargo)&nbsp;[![GoDoc](https://godoc.org/github.com/mrichman/hargo?status.svg)](https://godoc.org/github.com/mrichman/hargo) [![Go Report Card](https://goreportcard.com/badge/github.com/mrichman/hargo)](https://goreportcard.com/report/github.com/mrichman/hargo) [![Join the chat at https://gitter.im/mrichman/hargo](https://badges.gitter.im/mrichman/hargo.svg)](https://gitter.im/mrichman/hargo) [![GitHub license](https://img.shields.io/github/license/mrichman/hargo.svg)](https://github.com/mrichman/hargo/blob/master/LICENSE)
 [![GitHub issues](https://img.shields.io/github/issues/mrichman/hargo.svg)](https://github.com/mrichman/hargo/issues) [![Twitter](https://img.shields.io/twitter/url/https/github.com/mrichman/hargo.svg?style=plastic)](https://twitter.com/intent/tweet?text=Wow:&url=https%3A%2F%2Fgithub.com%2Fmrichman%2Fhargo)

Hargo parses [HAR](https://en.wikipedia.org/wiki/.har) files, can convert to curl format, and serve as a load test driver.

```text
NAME:
   hargo - work with HTTP Archive (.har) files

USAGE:
   hargo <command> [arguments] <.har file>

VERSION:
   0.1.2-dev.16 (28c9ef4)

AUTHOR:
   Mark A. Richman <mark@markrichman.com>

COMMANDS:
     fetch, f     Fetch URLs in .har
     curl, c      Convert .har to curl
     run, r       Run .har file
     validate, v  Validate .har file
     dump, d      Dump .har file
     load, l      Load test .har file
     help, h      Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --debug        Show debug output
   --help, -h     show help
   --version, -v  print the version

COPYRIGHT:
   (c) 2019 Mark A. Richman
```

## Running Hargo

```text
go get github.com/mrichman/hargo
cd $GOPATH/src/github.com/mrichman/hargo
go run cmd/hargo/hargo.go validate test/golang.org.har
```

## Building from source

Make sure that you have Go version 1.9 or greater (I haven't tested with lower) and that your `GOPATH` env variable is set (I recommand setting it to `~/go` if you don't have one). If `GOBIN` is not set, also try setting that to `~/go/bin`, as `make install` may fail. You can check all Go environment variables with `go env`.

```text
go get -d github.com/mrichman/hargo
cd $GOPATH/src/github.com/mrichman/hargo
make install
```

## About HAR Files

If you use Google Chrome, you can record these files by following the steps below:

1. Right-click anywhere on that page and click on Inspect Element to open Chrome's Developer Tools
2. The Developer Tools will open as a panel at the bottom of the page. Click on the Network tab.
3. Click the Record button, which is the solid black circle at the bottom of the Network tab, and you'll start recording activity in your browser.
4. Refresh the page and start working normally
5. Right-click within the Network tab and click Save as HAR with Content to save a copy of the activity that you recorded.
6. Within the file window, save the HAR file.

## Commands

### Fetch

The `fetch` command downloads all resources references in .har file:

`hargo fetch foo.har`

This will produce a directory named `hargo-fetch-yyyymmddhhmmss` containing all assets references by the .har file. This is similar to what you'd see when invoking `wget` on a particular URL.

### Curl

The `curl` command will output a [curl](https://curl.haxx.se/) command line for each entry in the .har file.

`hargo curl foo.har`

### Run

The `run` command executes each HTTP request in .har file:

`hargo run foo.har`

This is similar to `fetch` but will not save any output.

### Validate

The `validate` command will report any errors in the format of a .har file.

`hargo validate foo.har`

HAR file format is defined here: <https://w3c.github.io/web-performance/specs/HAR/Overview.html>

### Dump

Dump prints information about all HTTP requests in .har file

`hargo dump foo.har`

### Load

Hargo can act as a load test agent. Given a .har file, hargo can spawn a number of concurrent workers to repeat each HTTP request in order. By default, hargo will spawn 10 workers and run for a duration of 60 seconds.

Hargo will also save its results to [InfluxDB](https://www.influxdata.com/), if available. Each HTTP response is stored as a point of time-series data, which can be graphed by [Chronograf](https://www.influxdata.com/time-series-platform/chronograf/), [Grafana](http://grafana.org/), or similar visualization tool for analysis.
