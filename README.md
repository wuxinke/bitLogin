

# 公众号换取 openID

## 参考文档

https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/

https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html

## 部署

> 需要 node 10 以上
>
> docker 可使用 node:12-alpine 镜像

```shell
# 安装依赖
npm i
# 如果需要开发则要安装typescript 部署不用
# tsc
# 部署
npx pm2 start ./dist/app.js --name bitlogin
#查看状态
npx pm2 ls
# 重启
npx pm2 restart bitlogin
# 查看日志
npx pm2 log bitlogin
```

## api 使用

### 登陆

获取 code

> 默认跳转下一个接口，不需要跳转的`redirectOther=1`

**xxxx.yy **这个域名必须在公众号上配置`公众号设置`=>`网页授权域名`

`http://xxxx.yy/?state=key&redirectOther=0`

| 参数          | 说明                                                     | 必须 |
| :------------ | -------------------------------------------------------- | ---- |
| state         | 业务对应的 key，这个每个业务都需要在后台进行配置         | 是   |
| redirectOther | 是否跳转到 key 对应的地址，默认跳回本服务自动换取 openid | 否   |

### code2openid

通过 code 获取 openid

> 默认由上面接口自动跳转到微信再跳回这个接口

`http://xxxx.yy/code2openid?code=iiiiii&state=key`

| 参数  | 说明                                             | 必须 |
| ----- | ------------------------------------------------ | ---- |
| code  | 微信登陆后获得的 code                            | 是   |
| state | 业务对应的 key，这个每个业务都需要在后台进行配置 | 是   |

### .env 文件

根目录下须有该文件

下面是模板

```
# 业务配置 key=链接
# 变更后务必重启服务
test1=http://wuxinke.top:13000
ww4=https://wishingwall.bitworkshop.cn

# 端口
PORT=13000
# appid & secret
APPID=xxxxxx
SECRET=xxxxx

```

