# 参考代码

---

## 示例报文

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<TX>		
<TX_HEADER>
	<SYS_HDR_LEN>0</SYS_HDR_LEN>            
	<SYS_PKG_VRSN>01</SYS_PKG_VRSN>          
	<SYS_TTL_LEN>0</SYS_TTL_LEN>            
	<SYS_REQ_SEC_ID>108064</SYS_REQ_SEC_ID>      
	<SYS_SND_SEC_ID>108064</SYS_SND_SEC_ID>      
	<SYS_TX_TYPE>720000</SYS_TX_TYPE>            
	<SYS_EVT_TRACE_ID>6110011001490404136044054</SYS_EVT_TRACE_ID>  
	<SYS_SND_SERIAL_NO>0000000000</SYS_SND_SERIAL_NO>
	<SYS_PKG_TYPE>1</SYS_PKG_TYPE>          
	<SYS_MSG_LEN>0</SYS_MSG_LEN>            
	<SYS_IS_ENCRYPTED>0</SYS_IS_ENCRYPTED>  
	<SYS_ENCRYPT_TYPE>3</SYS_ENCRYPT_TYPE>  
	<SYS_COMPRESS_TYPE>0</SYS_COMPRESS_TYPE>
	<SYS_EMB_MSG_LEN>0</SYS_EMB_MSG_LEN>    
	<SYS_PKG_STS_TYPE>01</SYS_PKG_STS_TYPE>  
	<SYS_TX_STATUS>00</SYS_TX_STATUS> 
	<SYS_RECV_TIME>20170325092505955</SYS_RECV_TIME> 
	<SYS_RESP_TIME>20170325092505963</SYS_RESP_TIME>
</TX_HEADER>
<TX_BODY>
	<COMMON>
		<!—请求通用域字段。-->
	</COMMON>
	<ENTITY>
		<XML_CONTENT>
			<![CDATA[<xml version="1.0"encoding="UTF-8"?>
				<BJ_TX>
					<BJ_HEADER>											<APP_TRADE_CODE>B001    </APP_TRADE_CODE>
						<START_ADDR>303100000014</START_ADDR>
						<DEST_ADDR>105100098013</DEST_ADDR>
						<MESG_ID>Msg20120208008582608</MESG_ID>
						<MESG_REQ_NO></MESG_REQ_NO>
						<WORK_DATE>20120205</WORK_DATE>
						<SENT_TIME>20170325092505955</SENT_TIME>					                             </BJ_HEADER>
					<BJ_BODY>
						<BJ_CLZ>31310001601920120206000000759138</BJ_CLZ>
						<BJ_WD0>20120206</BJ_WD0>
						<BJ_SBN>313100016019</BJ_SBN>
						<BJ_52A>313100016019</BJ_52A>
						<BJ_50C>6212440100068773</BJ_50C>
						<BJ_50A>刘群</BJ_50A>
						<BJ_RBN>105100098013</BJ_RBN>
						<BJ_58A>007</BJ_58A>
						<BJ_59C>6227000012450155120</BJ_59C>
						<BJ_59A>刘永英</BJ_59A>
						<BJ_CUN>010</BJ_CUN>
						<BJ_32A>1100</BJ_32A>
						<BJ_CET>01</BJ_CET>
						<BJ_30B>20170316</BJ_30B>
						<BJ_21A></BJ_21A>
						<BJ_SIG>MEUCIQDf7Q
						MxwdpUVXBr7QordunP7EzuLe0c2mxcKVg2S7pJ5gIg
						Wyl39KYH9PEjW9J0qj/+JiitpjRHDrt3PTZEP7AVVyg</BJ_SIG>
						<BJ_72A></BJ_72A>
						<BJ_72C></BJ_72C>
						<BJ_LRF>L</BJ_LRF>								</BJ_BODY>
				</BJ_TX>]]>
		<XML_CONTENT>	
	</ENTITY>
</TX_BODY>
<TX_EMB/>
</TX>
```

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

P8外呼P5请求报文生成时需要将utfp121ReqVo中的bmp138ReqVo用到的各个栏位赋值

P5外呼P8返回响应报文时需要将utfp121RespVo中的utfp121RespVo用到的各个栏位赋值

也即是：**能使用bmp138格式的统一使用bmp138格式**

贷记提出示例：

![](/assets/20170419194909_B5717AA2-D6A8-481F-979B-E1F4D4A0F7FA.jpg)

---



