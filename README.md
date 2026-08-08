# 每日计划打卡表（网页版）

一个纯静态的月度每日打卡表网页，数据保存在浏览器本地（localStorage），按月独立存储。

## 功能

- 逐月切换，自动按当前月份生成 1-31 天
- 每行三组打卡项：学习 / 锻炼 / 复盘（勾选框 + 计划输入框）
- 周末行浅色区分，今天所在行高亮
- 底部「月度目标」三行，随月份独立保存
- 一键打印，输出 A4 竖向单页
- 「清空本月」一键重置当月数据

> 数据仅保存在当前浏览器的 localStorage 中，换浏览器 / 换设备不共用，清浏览器缓存会丢失。

## 本地预览

直接双击 `index.html` 打开即可。或用本地服务器：

```
python -m http.server 8000
```

访问 http://localhost:8000

## 部署到 Gitee Pages

Gitee Pages 需要实名认证后才能使用（免费版需申请开通，通常一两个工作日内审核）。

1. **注册 / 登录** gitee.com，并完成实名认证（设置 → 安全设置 → 手机/证件实名认证）。

2. **新建仓库**
   - 仓库名称建议：`daily-checkin-page`
   - 仓库属性：**公开**
   - 不要勾选「初始化仓库」的各项模板（或勾选也都可以）

3. **把代码推到仓库**

   ```bash
   git remote add origin https://gitee.com/<你的用户名>/daily-checkin-page.git
   git branch -M master
   git push -u origin master
   ```

4. **开启 Gitee Pages**
   - 仓库页面 → 左侧「服务」→「Gitee Pages」
   - 选择分支 `master`，部署目录填 `/`
   - 点击「启动」/「部署」
   - 免费版首次使用会提示先「申请升级」，按提示申请并由管理员审核通过后再部署启动。

5. 部署成功后，会提供一个类似 `https://<用户名>.gitee.io/daily-checkin-page/` 的网址，把链接分享即可使用。

## 更新页面

本地修改 `index.html` 后：

```
git add .
git commit -m "update"
git push
```

然后在 Gitee Pages 页面再点一次「更新」/「部署」即可生效。