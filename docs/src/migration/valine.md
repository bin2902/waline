---
title: 从 Valine 迁移
icon: valine
---

由于 Waline 在存储上完全复用了 Valine 的数据结构，所以从 Valine 迁移至 Waline 非常简单。

1. 按照 [Vercel 部署](../guide/get-started.md#vercel-部署-服务端) 一节部署服务端。`LEAN_ID` 和 `LEAN_KEY` 和之前使用 Valine 申请的保持一致即可。同时请不要忘记为 Waline 设置 `LEAN_MASTER_KEY`。
1. 按照 [HTML 片段](../guide/get-started.md#html-引入-客户端) 一节修改对应的前端脚本。

   ::: warning

   你需要删除 Valine 原始的配置 `appId` 和 `appKey`，并添加 `serverURL`。

   :::

   ```diff
   - <script src='//unpkg.com/valine/dist/Valine.min.js'></script>
   + <script src='//cdn.jsdelivr.net/npm/@waline/client'></script>

     <script>
   -  new Valine({
   +  Waline({
       el: '#vcomments',
   -   appId: 'Your appId',
   -   appKey: 'Your appKey'
   +   serverURL: 'YOUR SERVER URL'
     });
     </script>
   ```

::: tip 配置

Waline 和 Valine 大部分的配置都是一样的，但也存在些许不同。对于 v1 及 v0.x 版本，你只需要删除 Valine 原始的配置 `appId` 和 `appKey`，并添加 `serverURL`，其他选项均可正常工作。但是对于未来的 V2 我们将会移除某些 Valine 兼容，转向更好的配置方案。

Waline 具体的配置详见 [客户端配置](../reference/client.md)。你也可以查看 [Waline 客户端 v1 迁移指南](./client.md) 来了解与 Valine 不兼容的选项。

:::

::: tip 使用国内版 Leancloud

如果你是 Leancloud 国内版用户的话，除了 `LEAN_ID` 和 `LEAN_KEY`，还需要设置 `LEAN_SERVER` 环境变量，值为你的应用后台绑定的接入域名。

:::

## 迁移至 Cloudbase

如果你想要将你的 Valine 数据迁移至腾讯云开发的云数据库中的话，可以使用 LeanCloud 的导出功能配合云数据库的导入功能完成。在 LeanCloud 后台选择 <kbd>导入导出</kbd> > <kbd>限定 Class</kbd> > <kbd>Comment</kbd> > <kbd>导出</kbd>，之后会收到导出成功的邮件。

将导出成功的文件内容粘贴至下方的文本框中，点击下方的转换按钮，获得待导入的文件。进入 [腾讯云开发后台 → 数据库](https://console.cloud.tencent.com/tcb/db/index) 界面，选择 `Comment` 集合。若该集合不存在，点击左上角 <kbd>新建集合</kbd> 创建。进入后点击上方的导入按钮，选择刚才获得的转换后文件稍待片刻即可完成导入。

<MigrationTool />
