go-iprs
===============================================

![](https://img.shields.io/badge/status-WIP-red.svg?style=flat-square)

> Go implementation of [IPRS spec](https://github.com/ipfs/specs/tree/master/iprs)

Note: This module is a work in progress

During this process, you can check more about the state of this project on:

- [issues](https://github.com/dirkmc/go-iprs/issues)
- [libp2p specs](https://github.com/libp2p/specs)
- [IPRS spec](https://github.com/ipfs/specs/tree/master/iprs)

## Table of Contents

- [Install](#install)
- [Usage](#usage)
- [License](#license)

## Install

`go-iprs` is a standard Go module which can be installed with:

```sh
go get github.com/ipfs/go-iprs
```

Note that `go-iprs` is packaged with Gx, so it is recommended to use Gx to install and use it (see Usage section).

## Usage

### Using Gx and Gx-go

This module is packaged with [Gx](https://github.com/whyrusleeping/gx). In order to use it in your own project it is recommended that you:

```sh
go get -u github.com/whyrusleeping/gx
go get -u github.com/whyrusleeping/gx-go
cd <your-project-repository>
gx init
gx import github.com/ipfs/go-iprs
gx install --global
gx-go --rewrite
```

Please check [Gx](https://github.com/whyrusleeping/gx) and [Gx-go](https://github.com/whyrusleeping/gx-go) documentation for more information.

### Examples

#### Creating an EOL record signed with a public key

```go
privateKey := GenerateAPrivateKey()
dataStore := CreateADataStore()
valueStore := CreateAValueStore()
ns := NewNameSystem(valueStore, dataStore, 20)

// Publish a record ...
f := NewRecordFactory(valueStore)
p := iprspath.IprsPath("/iprs/" + u.Hash(privateKey))
eol := time.Now().Add(time.Hour)
record = f.NewEolKeyRecord(path.Path("/ipfs/myIpfsHash"), privateKey, eol)
err := ns.Publish(ctx, p, record)
if err != nil {
	fmt.Println(err)
}

// ... retrieve the record's value from a different piece of code
p, err := ns.resolve(ctx, p.String())
```

## License

MIT
