> 提醒： 滥用可能导致账户被BAN！！！[Telegram讨论群](https://t.me/starts_sh_group)  
  
* 本项目可选择性的把v2ray，shadowsocks，gost，brook四种代理工具部署到heroku空间，方便客户端各取所需！  
  
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/OTRSU/js-webtest-updatede--https-v2.herokuapp.com)  
  
1. [v2ray](https://github.com/2dust/v2rayN/releases)  
* 代理协议：vless 或 vmess (同时支持)
* 地址：appname.herokuapp.com
* 端口：443
* 默认UUID：8f91b6a0-e8ee-11ea-adc1-0242ac120002
* 加密：none
* 传输协议：ws
* 伪装类型：none
* 路径：/vlesspath // 默认vless使用/vlesspath，vmess使用/vmesspath
* 底层传输安全：tls
  
2. [shadowsocks](https://github.com/shadowsocks/shadowsocks-windows/releases/)   
* 服务器地址: appname.herokuapp.com
* 端口: 443
* 密码：password
* 加密：chacha20-ietf-poly1305
* 插件程序：D:\APP\v2ray-plugin_windows_amd64.exe  //此处要填[v2ray-plugin插件](https://github.com/shadowsocks/v2ray-plugin/releases)下载解压后在电脑上的绝对路径
* 插件选项: tls;host=appname.herokuapp.com;path=/sspath
  
3. [gost](https://github.com/ginuerzh/gost/releases)  
* 选择`gost-windows-amd64-*.zip`下载解压后复制gost的exe文件在电脑中的绝对路径，新建run.bat文件编辑内容如下保存后双击运行：      
```bash
C:\Users\Administrator\App\gost\gost-windows-amd64.exe -L :1080 -F=ss+wss://AEAD_CHACHA20_POLY1305:password@appname.herokuapp.com:443?path=/gostpath
```
  
4. [brook](https://github.com/txthinking/brook/releases)  
* 选择`Brook.exe`下载运行，配置`wsserver`内容`wss://appname.herokuapp.com:443/brookpath`以及密码`password`  
  
<details>
<summary>cloudflare workers example</summary>

```js
const SingleDay = 'appname.herokuapp.com'
const DoubleDay = 'appname.herokuapp.com'
addEventListener(
    "fetch",event => {
    
        let nd = new Date();
        if (nd.getDate()%2) {
            host = SingleDay
        } else {
            host = DoubleDay
        }
        
        let url=new URL(event.request.url);
        url.hostname=host;
        let request=new Request(url,event.request);
        event. respondWith(
            fetch(request)
        )
    }
)
```
</details>
