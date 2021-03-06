

# go-admin

go-admin是一个go语言开发的后台管理系统，该系统以角色为基础的权限管理设计（RBAC），完成了系统管理模块功能的开发（其他示例模块后续加上），采用前后端分离实现方式，服务端基于go开源gin框架，前端开源框架[vue-element-admin](https://github.com/PanJiaChen/vue-element-admin)。

### 设计原则

1. 采用比较流行开源框架[gin](https://github.com/gin-gonic/gin)、[vue-element-admin](https://github.com/PanJiaChen/vue-element-admin)，这些项目维护和更新比较好。
2. 尽量少修改vue-element-admin框架的代码，便于以后升级。
3. 前后端分离，前后端可以独立开发互不影响。
4. 走神了，忘了等想起补上。

### 系统环境

golang语言：go1.13.3+ 、

数据库：mysql5.7 

缓存：redis

### 项目地址

 <https://github.com/guyan0319/go-admin>

### 安装步骤

1、clone项目源代码

```
git clone  https://github.com/guyan0319/go-admin.git
```

2、导入data目录下的数据库文件systemdb.sql至你的数据库

修改数据库配置文件conf/mysql.go

```
var Db = map[string]DbConfig{
	"db1": {
		DriverName: "mysql",
		Dsn:        "root:123456@tcp(127.0.0.1:3306)/systemdb?charset=utf8mb4&parseTime=true&loc=Local",
		ShowSql:    true,
		ShowExecTime:    false,
		MaxIdle:    10,
		MaxOpen:    200,
	},
}

```

3、修改conf/redis.go文件，设置你自己的redis服务配置信息。

```
var Redis = map[string]string{
	"name":    "redis",
	"type":    "tcp",
	"address": "127.0.0.1:6379",
	"auth":    "",
}
```

4、启动服务端

```
go run main.go
```

注意：go-admin采用前后端分离，运行之前需要解决跨域问题，这里我们修改main.go文件即可。

```
func GetCorsConfig() cors.Config {
	config := cors.DefaultConfig()
	config.AllowOrigins = []string{"http://localhost:9529","http://localhost:9528","http://localhost:9527","http://localhost"}//此处加上你的前端域名
	config.AllowMethods = []string{"POST", "GET", "OPTIONS", "PUT", "DELETE"}
	config.AllowCredentials = true
	config.AllowHeaders = []string{"x-requested-with", "Content-Type", "AccessToken", "X-CSRF-Token","X-Token", "Authorization","token"}
	return config
}
```

 5、运行客户端

```
npm run dev
```

这里我们假定你是开发开发环境，且已经安装node.js。如应用于线上环境，则需要打包前端文件，web服务相关部署工作（这里不再赘述，有需要的可联系我，或issues）。

6、运行结果

![](https://github.com/guyan0319/golang_development_notes/blob/master/images/10.0.png?raw=true)

![](https://github.com/guyan0319/golang_development_notes/blob/master/images/10.1.png?raw=true)

![](https://github.com/guyan0319/golang_development_notes/blob/master/images/10.2.png?raw=true)


![](https://github.com/guyan0319/golang_development_notes/blob/master/images/10.3.png?raw=true)

![](https://github.com/guyan0319/golang_development_notes/blob/master/images/10.4.png?raw=true)

![](https://github.com/guyan0319/golang_development_notes/blob/master/images/10.5.png?raw=true)

### 小结：

目前只是完成系统管理模块开发，其他功能后续补上，如在使用过程中遇到任何问题或任何建议欢迎回复留言，您的支持的是我前进的动力。