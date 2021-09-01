> 提醒： 滥用可能导致账户被BAN！！！   
  
* 使用v2ray+caddy同时部署通过ws传输的vmess vless trojan shadowsocks socks等协议  
* 支持tor网络，且可通过自定义网络配置文件启动v2ray和caddy来按需配置各种功能  
* 支持存储自定义文件,目录及账号密码均为AUUID,客户端务必使用TLS连接  
  
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/Jamcurr/thtnrbv)  
  
### 服务端
点击上面紫色`Deploy to Heroku`，会跳转到heroku app创建页面，填上app的名字、选择节点、按需修改部分参数和AUUID后点击下面deploy创建app即可开始部署  
如出现错误，可以多尝试几次，待部署完成后页面底部会显示Your app was successfully deployed  
  * 点击Manage App可在Settings下的Config Vars项**查看和重新设置参数**  
  * 点击Open app跳转[欢迎页面](/etc/CADDYIndexPage.md)域名即为heroku分配域名，格式为`appname.herokuapp.com`，用于客户端  
  * 默认协议密码为$UUID，WS路径为$UUID-[vmess|vless|trojan|ss|socks]格式
  
### 客户端
* **务必替换所有的appname.herokuapp.com为heroku分配的项目域名**  
* **务必替换所有的8f91b6a0-e8ee-11ea-adc1-0242ac120002为部署时设置的AUUID**  
  
<details>
<summary>v2ray</summary>

```bash
* 客户端下载：https://github.com/v2fly/v2ray-core/releases
* 代理协议：vless 或 vmess
* 地址：appname.herokuapp.com
* 端口：443
* 默认UUID：8f91b6a0-e8ee-11ea-adc1-0242ac120002
* 加密：none
* 传输协议：ws
* 伪装类型：none
* 路径：/8f91b6a0-e8ee-11ea-adc1-0242ac120002-vless // 默认vless使用/$uuid-vless，vmess使用/$uuid-vmess
* 底层传输安全：tls
```
</details>
  
<details>
<summary>trojan-go</summary>

```bash
* 客户端下载: https://github.com/p4gefau1t/trojan-go/releases
{
    "run_type": "client",
    "local_addr": "127.0.0.1",
    "local_port": 1080,
    "remote_addr": "appname.herokuapp.com",
    "remote_port": 443,
    "password": [
        "8f91b6a0-e8ee-11ea-adc1-0242ac120002"
    ],
    "websocket": {
        "enabled": true,
        "path": "/8f91b6a0-e8ee-11ea-adc1-0242ac120002-trojan",
        "host": "appname.herokuapp.com"
    }
}
```
</details>
  
<details>
<summary>shadowsocks</summary>

```bash
* 客户端下载：https://github.com/shadowsocks/shadowsocks-windows/releases/
* 服务器地址: appname.herokuapp.com
* 端口: 443
* 密码：password
* 加密：chacha20-ietf-poly1305
* 插件程序：v2ray-plugin_windows_amd64.exe  //需将插件https://github.com/shadowsocks/v2ray-plugin/releases下载解压后放至shadowsocks同目录
* 插件选项: tls;host=appname.herokuapp.com;path=/8f91b6a0-e8ee-11ea-adc1-0242ac120002-ss
```
</details>
  
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
  
> [更多来自热心网友PR的使用教程](/tutorial)> 鎻愰啋锛?婊ョ敤鍙兘瀵艰嚧璐︽埛琚獴AN锛侊紒锛?  
  
* 浣跨敤v2ray+caddy鍚屾椂閮ㄧ讲閫氳繃ws浼犺緭鐨剉mess vless trojan shadowsocks socks绛夊崗璁? 
* 鏀寔tor缃戠粶锛屼笖鍙�氳繃鑷畾涔夌綉缁滈厤缃枃浠跺惎鍔╲2ray鍜宑addy鏉ユ寜闇�閰嶇疆鍚勭鍔熻兘  
* 鏀寔瀛樺偍鑷畾涔夋枃浠?鐩綍鍙婅处鍙峰瘑鐮佸潎涓篈UUID,瀹㈡埛绔姟蹇呬娇鐢═LS杩炴帴  
  
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/alicepear/kuhero)  
  
### 鏈嶅姟绔?鐐瑰嚮涓婇潰绱壊`Deploy to Heroku`锛屼細璺宠浆鍒癶eroku app鍒涘缓椤甸潰锛屽～涓奱pp鐨勫悕瀛椼�侀�夋嫨鑺傜偣銆佹寜闇�淇敼閮ㄥ垎鍙傛暟鍜孉UUID鍚庣偣鍑讳笅闈eploy鍒涘缓app鍗冲彲寮�濮嬮儴缃? 
濡傚嚭鐜伴敊璇紝鍙互澶氬皾璇曞嚑娆★紝寰呴儴缃插畬鎴愬悗椤甸潰搴曢儴浼氭樉绀篩our app was successfully deployed  
  * 鐐瑰嚮Manage App鍙湪Settings涓嬬殑Config Vars椤?*鏌ョ湅鍜岄噸鏂拌缃弬鏁?*  
  * 鐐瑰嚮Open app璺宠浆[娆㈣繋椤甸潰](/etc/CADDYIndexPage.md)鍩熷悕鍗充负heroku鍒嗛厤鍩熷悕锛屾牸寮忎负`appname.herokuapp.com`锛岀敤浜庡鎴风  
  * 榛樿鍗忚瀵嗙爜涓?UUID锛學S璺緞涓?UUID-[vmess|vless|trojan|ss|socks]鏍煎紡
  
### 瀹㈡埛绔?* **鍔″繀鏇挎崲鎵�鏈夌殑appname.herokuapp.com涓篽eroku鍒嗛厤鐨勯」鐩煙鍚?*  
* **鍔″繀鏇挎崲鎵�鏈夌殑8f91b6a0-e8ee-11ea-adc1-0242ac120002涓洪儴缃叉椂璁剧疆鐨凙UUID**  
  
<details>
<summary>v2ray</summary>

```bash
* 瀹㈡埛绔笅杞斤細https://github.com/v2fly/v2ray-core/releases
* 浠ｇ悊鍗忚锛歷less 鎴?vmess
* 鍦板潃锛歛ppname.herokuapp.com
* 绔彛锛?43
* 榛樿UUID锛?f91b6a0-e8ee-11ea-adc1-0242ac120002
* 鍔犲瘑锛歯one
* 浼犺緭鍗忚锛歸s
* 浼绫诲瀷锛歯one
* 璺緞锛?8f91b6a0-e8ee-11ea-adc1-0242ac120002-vless // 榛樿vless浣跨敤/$uuid-vless锛寁mess浣跨敤/$uuid-vmess
* 搴曞眰浼犺緭瀹夊叏锛歵ls
```
</details>
  
<details>
<summary>trojan-go</summary>

```bash
* 瀹㈡埛绔笅杞? https://github.com/p4gefau1t/trojan-go/releases
{
    "run_type": "client",
    "local_addr": "127.0.0.1",
    "local_port": 1080,
    "remote_addr": "appname.herokuapp.com",
    "remote_port": 443,
    "password": [
        "8f91b6a0-e8ee-11ea-adc1-0242ac120002"
    ],
    "websocket": {
        "enabled": true,
        "path": "/8f91b6a0-e8ee-11ea-adc1-0242ac120002-trojan",
        "host": "appname.herokuapp.com"
    }
}
```
</details>
  
<details>
<summary>shadowsocks</summary>

```bash
* 瀹㈡埛绔笅杞斤細https://github.com/shadowsocks/shadowsocks-windows/releases/
* 鏈嶅姟鍣ㄥ湴鍧�: appname.herokuapp.com
* 绔彛: 443
* 瀵嗙爜锛歱assword
* 鍔犲瘑锛歝hacha20-ietf-poly1305
* 鎻掍欢绋嬪簭锛歷2ray-plugin_windows_amd64.exe  //闇�灏嗘彃浠秇ttps://github.com/shadowsocks/v2ray-plugin/releases涓嬭浇瑙ｅ帇鍚庢斁鑷硈hadowsocks鍚岀洰褰?* 鎻掍欢閫夐」: tls;host=appname.herokuapp.com;path=/8f91b6a0-e8ee-11ea-adc1-0242ac120002-ss
```
</details>
  
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
  
> [鏇村鏉ヨ嚜鐑績缃戝弸PR鐨勪娇鐢ㄦ暀绋媇(/tutorial)
