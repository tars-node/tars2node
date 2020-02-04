# Tars2Node

`tars2node` 可以将 Tars IDL 定义文件转换为 JavaScript 语言所使用的版本，结合 [@tars/stream](https://www.npmjs.com/package/@tars/stream) 模块执行编解码操作。

如您有 Tars RPC 需求可结合 [@tars/rpc](https://www.npmjs.com/package/@tars/rpc) 模块进行调用。

## 用法

直接使用 build 目录中的 `tars2node` 预编译程序即可（Linux 平台）。

```bash
tars2node [OPTIONS] tarsfile
```

## 选项

| 选项 | 作用 |
| ------------- | ------------- |
| --stream-path=[DIRECTORY]              | 指定编解码模块名称，默认为 @tars/stream。 |
| --rpc-path=[DIRECTORY]                 | 指定 RPC 模块名称，默认为 @tars/rpc。 |
| --allow-reserved-namespace             | 是否允许 `tars` 作为命名空间（因为此命名空间主要用于框架服务的 tars 文件定义）。 |
| --dir=[DIRECTORY]                      | 生成文件的输出目录。 |
| --relative                             | 限定所有的 `.tars` 文件都在当前目录寻找。|
| --tarsBase=[DIRECTORY]                 | 指定 `.tars` 文件的搜索目录。|
| --r                                    | 转换嵌套的 `.tars` 文件。|
| --r-minimal                            | 精简依赖文件，移除非必须成员。|
| --r-reserved                           | 精简依赖文件时需保留的成员。|
| --client                               | 生成客户端的调用类代码。|
| --server                               | 生成服务端的框架代码。|
| --ts                                   | 打开此选项将后将只生成 TypeScript (.ts) 代码。|
| --dts                                  | 生成时附加 TypeScript 描述文件（.d.ts）。|
| --long-type=[number|string|bigint]     | 可选择使用 \<Number\|String\|BigInt\> 表达 \<long\> 类型，默认值为 \<Number\>。|
| --string-binary-encoding               | 遇到字符编码问题或需对原始数据进行存取时，打开此选项使用 \<buffer\> 存储 \<string\>。|
| --enum-reverse-mappings                | 输出代码 \<enum\> 支持枚举值到枚举名的反向映射 。|
| --optimize=[0\|s]                      | 优化输出代码大小，默认为 0（也就是不优化）。|

## 例子

```bash
tars2node Protocol.tars
```

上述命令将转换 `Protocol.tars` 文件中定义的 `常量`、`枚举`、`结构体` 等数据类型生成 `ProtocolTars.js` 供编解码使用。
使用方法请参考 [@tars/stream](https://www.npmjs.com/package/@tars/stream) 模块说明文档。

```bash
tars2node Protocol.tars --client
```

上述命令将转换文件中定义的 `常量`、`枚举值`、`结构体` 等数据类型，并将 `interface` 描述段转换为 Tars RPC 客户端接口文件，最终生成 `ProtocolProxy.js` 供调用方使用。
使用方法请参考 [@tars/rpc](https://www.npmjs.com/package/@tars/rpc) 模块说明文档。

```bash
tars2node Protocol.tars --server
```

上述命令将转换文件中定义的 `常量`、`枚举值`、`结构体` 等数据类型，并将 `interface` 描述段转换为 Tars RPC 服务端接口文件，最终生成 `Protocol.js` 以及 `ProtocolImp.js` 供服务提供方使用。
开发者无需改动 `Protocol.js`，只需要继续完善 `ProtocolImp.js` 实现文件中具体的函数，即可作为 Tars RPC 服务端提供服务。
使用方法请参考 [@tars/rpc](https://www.npmjs.com/package/@tars/rpc) 模块说明文档。

## 从源码编译

1. 安装对应平台的 build-essential
2. 安装 [CMake](https://cmake.org/)
3. 在源码 build 目录下执行 `cmake ../ && make`
