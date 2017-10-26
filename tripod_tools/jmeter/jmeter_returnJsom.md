# Jmeter中处理返回的Json数据

#### 

#### 一、处理Jmeter返回Json数据乱码问题

> * 分两步
>   *  修改jmeter配置文件\(bin/jmeter.properties\)中编码的值。
>     ```bash
>     #sampleresult.default.encoding=ISO-8859-1
>     sampleresult.default.encoding=UTF-8
>     ```
>
>   *  测试计划中添加后置处理器\(Bean Shell PostProcessor）并写入如下代码。
>     ```java
>     String s=new String(prev.getResponseData(),"UTF-8");
>             char aChar;
>             int len= s.length();
>             StringBuffer outBuffer=new StringBuffer(len);
>             for(int x =0; x <len;){
>                 aChar= s.charAt(x++);
>                 if(aChar=='\\'){
>                     aChar= s.charAt(x++);
>                     if(aChar=='u'){
>                         int value =0;
>                         for(int i=0;i<4;i++){
>                             aChar= s.charAt(x++);
>                             switch(aChar){
>                                 case'0':
>                                 case'1':
>                                 case'2':
>                                 case'3':
>                                 case'4':
>                                 case'5':
>                                 case'6':
>                                 case'7':
>                                 case'8':
>                                 case'9':
>                                     value=(value <<4)+aChar-'0';
>                                     break;
>                                 case'a':
>                                 case'b':
>                                 case'c':
>                                 case'd':
>                                 case'e':
>                                 case'f':
>                                     value=(value <<4)+10+aChar-'a';
>                                     break;
>                                 case'A':
>                                 case'B':
>                                 case'C':
>                                 case'D':
>                                 case'E':
>                                 case'F':
>                                     value=(value <<4)+10+aChar-'A';
>                                     break;
>                                 default:
>                                     throw new IllegalArgumentException(
>                                             "Malformed   \\uxxxx  encoding.");}}
>                         outBuffer.append((char) value);}else{
>                         if(aChar=='t')
>                             aChar='\t';
>                         else if(aChar=='r')
>                         aChar='\r';
>                         else if(aChar=='n')
>                         aChar='\n';
>                         else if(aChar=='f')
>                         aChar='\f';
>                         outBuffer.append(aChar);}}else
>                     outBuffer.append(aChar);}
>             prev.setResponseData(outBuffer.toString());
>     ```

#### 二、格式化Jmeter返回的Json数据

> 测试计划中添加后置处理器\(Bean Shell PostProcessor\),脚本代码如下!
>
> 前提需要如下三个jar包
>
> * jackson-annotations-2.9.0.jar
> * jackson-core-2.9.2.jar
> * jackson-databind-2.9.2.jar
>
> 下载地址： [https://jar-download.com](https://jar-download.com)

```java
import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;


try {

        String response_data = prev.getResponseDataAsString();

        log.info("response_data: " + response_data);
        ObjectMapper objectMapper = new ObjectMapper();

        Map readValue = objectMapper.readValue(response_data, Map.class);
        String writeValueAsString = objectMapper.writerWithDefaultPrettyPrinter().writeValueAsString(readValue);
        log.info("PrettyFromatJson result: " + writeValueAsString);

        prev.setResponseData(writeValueAsString);



} catch (JsonProcessingException e) {

       log.info("BeanShell PostProcessor-解密数据 failed============== =========================", ex);

}
```



