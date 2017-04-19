# 参考代码

---

## BMP009 报文处理方式

对于收到 P5 返回的 BMP009 报文，由于是通用回执，可能对应很多场景，在`A0339P5BJServiceImpl.java`中按如下方式处理：

```java
// 普通借记回执入账
ServiceMapping.put("B009021", "BjNmlDebitReceiptIncomingServiceFlow");

// 009通用回执增加原交易码来区分子服务
if("B009".equals(trnCode)) {
    trnCode += uftpReq.getBmp138Info().getBjBody().getBj02b();
}
```

---

## “121”和“138”的使用方式

**P8外呼P5请求报文生成时需要将utfp121ReqVo中的bmp138ReqVo用到的各个栏位赋值**

**P5外呼P8返回响应报文时需要将utfp121RespVo中的utfp121RespVo用到的各个栏位赋值**

**也即是：**能使用bmp138格式的统一使用bmp138格式

**贷记提出示例：**



