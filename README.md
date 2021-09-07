# go-protobuf
go使用protobuf的避坑。

最新版本golang，1.17版本已经不支持用网上大多原本写的方式进行安装了。
会提示你用google下的插件而不是别的。但最新版的出来没几个星期，资料也比较少。
而很多人应该也是跟我一样，能解决当下问题，能用就行。

但用回旧版本的golang，现在下载的插件也是最新的了。最新版的插件，在要求上也跟旧版本有了区别。
哦= =！忘了说前提，这里用的是windows系统。
还是老步骤：
go get -u github.com/golang/protobuf/protoc-gen-go

装完后看看成功没，图方便的话，直接把生成gen exe拖到和protoc exe的相同目录下

现在我们来运行命令看看能不能成功
```
protoc --go_out=. *.proto
protoc-gen-go: unable to determine Go import path for "*.proto"

Please specify either:
        • a "go_package" option in the .proto source file, or
        • a "M" argument on the command line.

See https://developers.google.com/protocol-buffers/docs/reference/go-generated#package for more information.

--go_out: protoc-gen-go: Plugin failed with status code 1.
```

提示报错了。但为什么网上也没有提示这个问题怎么解决呢？这又是因为插件时最新版本的，他有强制要求在proto文件中写入这样一行话

```
syntax = "proto3";
option go_package = ".";
package ONE_MSG;
```

也就是导出到go的包的对应位置。可以是GOPATH，也可以是GO下src的位置。
