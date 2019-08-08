---
title: 开发插件
---

通过定义插件，开发人员可以扩展Steedos现有的功能。

## 创建插件
任何 Steedos 项目都可以转换为一个插件。每个插件就是一个npm包，必须先发布到npm，才能在其他项目中引用。

### 插件名称
package.json 中定义的 npm 包名称，就是插件名称。

## 插件初始化
每个插件必须定义一个 init 函数，供 Steedos 在插件初始化时调用。
```js
export function init(context) {
    // 执行插件初始化。
}
```
context中包含以下参数：
- app: express 服务端，用于引入路由。
- settings: 项目 steedos-config.yml 中配置的所有参数。

## 定义服务端API
可以在插件中定义 Express Routes，并在插件初始化函数中注册相关路由。
```js
const router = express.Router();

router.get('/plugins/test/hello', async (req, res) => {
    res.status(200).send(`Hello World`);
    res.end();
    return;
}

export function init(context) {
    context.app.use(router);
}
```