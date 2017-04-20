# 交易带附件

---

## 文件名命名规则

### 明细文件

`交易流水号_业务类型_IN/OUT_子序号.dat`

* 业务类型：`BMPXXX` 后三位数字
* IN：P8 接收
* OUT：P8 发送
* 子序号
  * 一笔交易只有一个附件时，子序号为 `00`
  * 一笔交易有多个附件时，子序号从 `01` 开始累加

例如：`10510009801320170527_835_IN/OUT_00.dat`

### 图像文件

#### COS\_T 到 P8

以 COS\_T 命名规则为准，以相同文件名发送给 P5

#### P5 到 P8

`交易流水号_业务类型_IN_子序号.jpeg`

* 业务类型：`BMPXXX` 后三位数字
* 子序号
  * 一笔交易只有一个图像文件时，子序号为 `00`
  * 一笔交易有多个图像文件时，子序号从 `01` 开始累加

---

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

---

## 文件格式

文件内容使用 xml 格式，例如：

```xml
<xml version="1.0"encoding="UTF-8"?>                    
<BJ_TX>
    <BJ_BODY>                
        <BJ_DF2>
            <BJ_CDT>明细流水号1</BJ_CDT>
            <BJ_AGN>合同（协议）号1</BJ_AGN>
            <BJ_52A>付款人开户行行号1</BJ_52A>
        </BJ_DF2>
        <BJ_DF2>
            <BJ_CDT>明细流水号2</BJ_CDT>
            <BJ_AGN>合同（协议）号2</BJ_AGN>
            <BJ_52A>付款人开户行行号2</BJ_52A>
        </BJ_DF2>
    </BJ_BODY>
</BJ_TX>
```

每个字段的标签使用人行报文标准标签加 `BJ_` 前缀，明细序号/流水号可使用 `BJ_CDT`，备注可使用 `BJ_RMK`，其他找不到的需和 P5 约定。

