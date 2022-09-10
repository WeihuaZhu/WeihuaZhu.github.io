---
layout:     post
title:      RPC, gRPC, and Protocol Buffer
subtitle:   blog template
date:       2022-09-09
author:     Weihua
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Protocol Buffer
    - RPC
    - gRPC
---
To be updated
# RPC framework & Protocol buffers (protobuff)

## RPC

[Martin Kleppman distributed systems lecture on RPC](https://www.youtube.com/watch?v=S2osKiqQG9s)

![Untitled](/img/rpc_1.png)

![Untitled](/img/rpc_2.png)

RPC key points:

- looks like a function/method call, but implementation of the function call is on another node, not part of the codebase(a list of URLS where the object code can be loaded from). This is underneath being translated into some kind of network communication
- RPC synonym: Remote method invocation (JAVA)
- stub: marshal args into a message, the message can be any format that can be translated back into a copy of the original object: JSON, binary/byte stream, etc.
- marshall/unmarshall synonym: ~encode/decode, ~serde. Marchal is like serialization except marshalling also records codebases(codebase here refers to a list of URLs where the object code can be loaded from, and not source code. see [marshaling definition on wikipedia](https://en.wikipedia.org/wiki/Marshalling_(computer_science)#:~:text=Marshalling%20is%20like%20serialization%2C%20except,marshalling%20treats%20remote%20objects%20specially.&text=Any%20object%20whose%20methods%20can,machine%5D%20must%20implement%20the%20java.)). (treats remote object specially)
- [Ideally] RPC achieved Location transparency: system hides where a resource is located. Ideally, RPC makes a call to a remote function look the same as a local function call
- In practice, a lot of error cases:
    - the system crashes during the function call
    - a message is lost
    - a message is delayed
    - if sth is wrong, is it safe to retry?
- Can help building Service-oriented architecture (SOA) / microservices. Splitting a large software application into multiple services (or multiple nodes) that communicate via RPC. Especially when different services are implemented in different languages:
    - interoperability: datatype conversions
    - this is implemented by Interface Definition Language (IDL): language-indenpendent API specification
- RPC framework can take an IDL specification and generate code in all supported programming languages. It can generate the stubs for both the RPC client and RPC server, that make it easy to write code that performs the RPC on both the caller side and server side that is being called.

## gRPC

[Introduction to gRPC](https://grpc.io/docs/what-is-grpc/introduction/)

[A basic tutorial to gRPC in Go](https://grpc.io/docs/languages/go/basics/)

gRPC uses an IDL called protocol buffer

![Untitled](/img/rpc_3.png)

## Thrift

[Thrift: the missing guide](https://diwakergupta.github.io/thrift-missing-guide/)

## REST

often with JSON

REST can be considered as a type of RPC framework

Ajax in web browser

![Untitled](/img/rpc_4.png)