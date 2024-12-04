# HomeProxy 配置文件
* ```RevisedVersion/homeproxy```为修改版的配置文件，原fork大佬，已经停止维护了。
* ```homeproxy```为HomeProxy的配置文件，用本项目下的```homeproxy```替换```/etc/config/homeproxy```
- 节点设置
  - 订阅　　　//这里订阅自己的机场
- 客户端设置
  - 路由节点　　//把节点中亮红色的```[direct]Apple```，有```tmp1-tmp10```时， 不亮红色，修改为自己刚订阅的节点，不可重复；苹果需要直连的，不用修改Apple，需要代理Apple时，节点选择自己需要的，DNS规则中，中国规则去除Apple,非中国规则添加Apple
  - 路由设置　　//默认出站，选择主要出口
* 保存并应用,这时会显示HomeProxy正在运行
* 节点设置中的节点下有tmp1 - tmp10 ，这里如果在意，觉得碍眼睛可以删除
* 如果在意DNS泄漏，按如下方法修改
- 客户端设置
  - DNS设置　　//默认DNS服务器，修改为Proxy_DNS ，勾选禁用DNS缓存。
  - DNS规则　　//中国规则，选择Proxy_DNS
# HomeProxy 自定义规则文件添加说明
- 客户端设置
  - 规则集　　//添加一个直连规则集,类型：远程，格式：源文件，规则集URL:```https://www.ghproxy.cn/```后面跟github地址，出站：直连；不要使用本仓库下的direct.json，里面域名地址是我随便写的，先fork到自己仓库，然后修改为自己想要的域名；添加代理规则和直连规则的方式一样。
* 只添加需要的规则，为空的规则要删除，不然HomeProxy会报错，```domain,domain_suffix,domain_keyword,ip_cidr```这四项，哪项有数据就保留哪一项，不要留空。
``` bash
{
  "version": 1,
  "rules": [
    {
      "domain": [
      ]
    },
    {
      "domain_suffix": [
      ]
    },
    {
      "domain_keyword": [
      ]
    },
    {
      "ip_cidr":[
      ]
    }
  ]
}
```
- 客户端设置
  - 路由规则　　//修改```非中国地区```，规则集中添加刚添加的proxy规则集，修改```中国```，规则集中添加刚添加的direct规则集
  - DNS规则　　//修改```中国规则```，规则集中添加刚添加的direct规则集，修改```非中国规则```，规则集中添加刚添加的proxy规则集
* 保存并应用
