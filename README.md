# 每日计划打卡表（网页版）

一个纯静态的月度每日打卡日历网页。打卡数据**绑定登录账号**，云端按账号独立存储（LeanCloud），换设备登录同一账号即可看到同一份数据。

> 目录里 `vendor/av-min.js` 是 LeanCloud 浏览器端 SDK，已本地内置，不依赖外部 CDN。

## 功能

- **登录 / 注册**：进入页面需登录；注册需回答资格问题（答案只有你自己知道），防止陌生人随意注册
- **数据绑定用户**：打卡数据归登录账号所有，云端 ACL 仅本人可读写，未登录或他人账号看不到你的内容
- 日历视图：每月一张月历，点击任意日期格子即可添加当天任务
- 格子内**任务预览**：每行一个小勾选框（已完成为绿色勾）+ 任务文字，超长自动省略号缩略；任务过多时格子大小不变，超出部分隐藏并提示「＋N 条未显示」；打印时会完整列出所有任务
- 完成状态一目了然：
  - 当天任务**全部完成** → 日期格子显示**绿色**
  - 当天**还有未完成任务** → 日期格子显示**淡红色**
  - 当天**没有任务** → 中性底色
- 已完成任务与任务弹窗样式统一：勾选框绿色、文字加删除线
- 底部「月度目标」三行，随月份独立保存
- 一键打印，输出 A4 竖向月历（含每天任务清单）
- 逐月切换、一键回到今天、「清空本月」重置当月数据
- **云端同步**：改动自动上传、打开自动拉取，多设备共享

## 部署（GitHub Pages + 自定义域名）

1. 代码推送到 GitHub 仓库（公开仓库才能免费托管 Pages）：

   ```bash
   git remote add github git@github.com:jinjiao-king/monthly-checkin-web.git
   git branch -M main
   git push -u github main
   ```

2. 开启 Pages：仓库 **Settings → Pages**，Source 选「Deploy from a branch」，分支 `main`，目录 `/`。

3. 绑定自定义域名：
   - 在 Pages 设置页的 **Custom domain** 填入 `work.superdiscount.cn`
   - 在域名解析服务商（阿里云 DNS）添加解析：`CNAME  work → jinjiao-king.github.io`
   - 等待 Let's Encrypt 自动签发 HTTPS 证书后，勾选 **Enforce HTTPS**

4. 访问 `https://work.superdiscount.cn` 或 `https://jinjiao-king.github.io/monthly-checkin-web/`

## 本地预览

直接双击 `index.html` 打开即可。或用本地服务器：

```
python -m http.server 8000
```

访问 http://localhost:8000

## 更新页面

```
git add .
git commit -m "update"
git push github main
```

推送后 GitHub Pages 会自动重新构建部署（约 1 分钟），强制刷新（Ctrl+Shift+R）即可看到新版本。

## 数据与安全说明

- **云端存储**：数据保存在 LeanCloud `CheckinStore` 表，按账号（`u:<用户ID>`）一行独立存储，ACL 仅本人可读写
- **登录密码**：密码存于 LeanCloud 用户系统，无法找回，请牢记
- **注册资格**：注册前需回答你自定义的问题，答对才能创建账号
- **客户端密钥**：页面内置 AppID / AppKey（客户端公开凭据，浏览器端正常），但数据已按账号做 ACL 隔离，他人无法读取你的数据
- **本地兜底**：数据同时缓存在本机 localStorage，云端临时不可用时页面仍可离线使用
