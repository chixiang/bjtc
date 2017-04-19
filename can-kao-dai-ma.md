# 参考代码

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





