# Steedos Stimulsoft报表插件

### 报表Express请求总入口
- 总入口 /plugins/stimulsoft/
- 所有/plugins/stimulsoft/前缀的请求都会经过该总入口
- 发现URL以assets或static开头则请求下面的` 静态资源相关`
- 如果不是静态资源则返回html内容，详细请见`WEB界面相关`

### 报表API路由
- GET /plugins/stimulsoft/api/reports #获取报表列表
- GET /plugins/stimulsoft/api/mrt/:report_id #获取报表模板
- POST /plugins/stimulsoft/api/mrt/:report_id #保存报表模板
- GET /plugins/stimulsoft/api/data/:report_id #获取报表数据

### WEB界面路由
- /plugins/stimulsoft/web/ #报表浏览界面，显示报表列表，点击查看报表明细
- /plugins/stimulsoft/web/viewer/:id #查看报表详细
- /plugins/stimulsoft/web/designer/:id #报表设计工具

> 上述查看报表详细界面是重定向到`/plugins/stimulsoft/assets/viewer.html?reportUrl=/plugins/stimulsoft/api/mrt/:id`静态界面的
> 上述报表设计工具界面是重定向到`/plugins/stimulsoft/assets/designer.html?reportUrl=/plugins/stimulsoft/api/mrt/:id`静态界面的

### 静态资源相关路由
- /plugins/stimulsoft/assets/** #Stimulsoft相关js/css/html资源文件，指向react的build文件夹的assets文件夹
- /plugins/stimulsoft/static/** #React打包后的js/css资源文件，指向react的build文件夹的static文件夹


# 开发说明

### 安装依赖包

```
$ yarn
```

### 运行客户端
```
$ yarn start
```

访问地址: `http://localhost:3000/web`

> 依赖服务端，需要先运行`yarn server`跑起服务端

### 运行服务端
```
$ yarn server
```
访问地址: `http://localhost:3200/plugins/stimulsoft/web/`


### 插件使用
```
...
let app = express();
...
plugin.init(app);
...
```

参考：https://github.com/steedos/steedos-plugin-stimulsoft-report/blob/master/server.js

Example：https://github.com/steedos/steedos-contracts-app/blob/master/server.js

### 插件配置
- 插件会自动加载src文件夹中以report.yml后缀且其内容中report_type为'stimulsoft-report'的报表文件
- 识别到的报表会自动生成对应的以mrt后缀的文件
- 可以打开报表设计工具设计报表，并保存到mrt后缀文件中

参考：https://github.com/steedos/steedos-plugin-stimulsoft-report/blob/master/src/contracts.report.yml

Example：https://github.com/steedos/steedos-contracts-app/blob/master/src/contracts.report.yml