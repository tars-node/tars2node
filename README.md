# Tars2Node

`tars2node` 可以将 Tars IDL 定义文件转换为 JavaScript 语言所使用的版本，结合 [@tars/stream](https://www.npmjs.com/package/@tars/stream) 模块执行编解码操作。

如您有 Tars RPC 需求可结合 [@tars/rpc](https://www.npmjs.com/package/@tars/rpc) 模块进行调用。

## 用法

直接使用 build 目录中的 `tars2node` 预编译程序即可（Linux 平台）。

```bash
tars2node [OPTIONS] tarsfile
```

## 选项

> Options:
>  --version                    print tars2node version.  
>  --rpc-path=[DIRECTORY]       specify the path of rpc module.  
>  --stream-path=[DIRECTORY[]   specify the path of stream module.  
>  --allow-reserved-namespace   allow you to use reserved word as a namespace.  
>  --dir=DIRECTORY              generate source file to DIRECTORY.  
>  --relative                   use current path.  
>  --tarsBase=DIRECTORY          where to search tars files.  
>  --r                          generate source all tars files.  
>  --r-minimal                  minimize the dependent members.  
>  --r-reserved                 list of names(split by ",") that should be keeped.  
>  --client                     just for client side source file.  
>  --server                     just for server side source file.  
>  --dts                        generate d.ts file.  
>  --use-string-represent       use string represent long type.  
>  --string-binary-encoding     get string raw bytes <BinBuffer>.  
>  --optimize=[0|s]             support "s" to reduce code size, default is 0.  

## 从源码编译

1. 安装对应平台的 build-essential
2. 安装 [CMake](https://cmake.org/)
3. 在源码 build 目录下执行 `cmake ../ && make`