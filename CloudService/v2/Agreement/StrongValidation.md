# 加固接口的签名验证
## 签名传输方式：
Header:  
&nbsp;&nbsp;timestamp=1532059200000  
&nbsp;&nbsp;sign=8b1f8907a23c97e6b48965f0481f8634  

## 签名计算
timestamp = 2018-07-20 12:00:00  => 1532059200000（毫秒)  
sign = MD5(signKey + Sort(params) + Timestamp)

| 参数 | 意义 |
| ---- | ---- |
| signKey | 双份约定的混淆的Key |
| sort(params) | 按参数名升序排序的接口参数，直接累加出来的字符串 |
| timestamp | 10进制的unix时间戳 | 

**注：params 根据请求类型取值，比如Post会取所有Form中的值，Get会取所有Query中的值。**

## 示例
POST请求A接口：  
signKey:  CdLvNRRQvy0xjORPNvuVaA  
  
请求参数：B=2,A=1,C=3  

	signKey= CdLvNRRQvy0xjORPNvuVaA
	sort(params) = A + B + C = 123
	timestamp = 1532059200000
	
	sign = MD5(signKey+ Sort(params) + timestamp)
	sign = MD5 (CdLvNRRQvy0xjORPNvuVaA + 123 + 1532059200000)
	sign =  MD5 (CdLvNRRQvy0xjORPNvuVaA1231532059200000)
	sign = d5680a902dd2de08cf2bf9df819ffb9d
	
	传输参数：  
    A?timestamp=1532059200000&sign=e10adc3949ba59abbe56e057f20f883e