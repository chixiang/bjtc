# 交易带附件

---

## 文件名命名规则

`交易流水号_业务类型_IN/OUT_子序号.dat`

* 业务类型：`BMPXXX` 后三位数字
* IN：P8 接收
* OUT：P8 发送
* 子序号
  * 一笔交易只有一个附件时，子序号为 `00`
  * 一笔交易有多个附件时，子序号从 `01` 开始累加

例如：`10510009801320170527_835_IN/OUT_00.dat`

## 文件存放路径

`$HOME/file/`

## 报文

使用文件独立传输模式，多个文件不打包，`COMMON` 域中需包含：

```xml
<FILE_LIST_SERIAL>
    <FILE_NUM>文件个数</FILE_NUM>
    <FILE_INFO>文件信息</FILE_INFO>
    <FILE_NODE>文件节点</FILE_NODE>
    <FILE_NAME>文件名</FILE_NAME>
    <FILE_PATH>文件路径</FILE_PATH>
    <FILE_MODE>文件处理模式</FILE_MODE>
    <APP_MODE>文件应用模式</APP_MODE>
</FILE_LIST_SERIAL>
```

具体可参考《CCB-NIS-TG-AA-应用平台联机交易接口报文规范.doc》

