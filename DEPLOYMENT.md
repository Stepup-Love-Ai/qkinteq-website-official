# GitHub Pages 部署指南 - qkinteq.com

本指南将帮助你使用 GitHub Pages 将网站部署到 `https://www.qkinteq.com`

## 什么是 GitHub Pages？

GitHub Pages 是 GitHub 提供的免费静态网站托管服务，可以：
- ✅ 完全免费
- ✅ 自动 HTTPS（SSL 证书）
- ✅ 与 GitHub 仓库无缝集成
- ✅ 自动部署（推送代码即更新）
- ✅ 支持自定义域名

---

## 部署步骤

### 第一步：准备代码并推送到 GitHub

1. **确保所有更改已提交**
   ```bash
   git add .
   git commit -m "Ready for deployment"
   git push origin main
   ```

2. **确认仓库已推送到 GitHub**
   - 访问你的 GitHub 仓库：`https://github.com/Stepup-Love-Ai/qkinteq-website-official`
   - 确认所有文件都在仓库中

---

### 第二步：启用 GitHub Pages

1. **进入仓库设置**
   - 在 GitHub 仓库页面，点击右上角的 **Settings**（设置）

2. **找到 Pages 设置**
   - 在左侧菜单中找到 **Pages**（页面）选项

3. **配置 Pages 源**
   - **Source（源）**：选择 `Deploy from a branch`
   - **Branch（分支）**：选择 `main`
   - **Folder（文件夹）**：选择 `/ (root)`
   - 点击 **Save（保存）**

4. **等待部署完成**
   - GitHub 会自动开始部署
   - 通常需要 1-2 分钟
   - 部署完成后，你会看到一个绿色的提示框，显示你的网站地址：
     ```
     Your site is live at https://Stepup-Love-Ai.github.io/qkinteq-website-official/
     ```

---

### 第三步：配置自定义域名

#### 3.1 创建 CNAME 文件

1. **在仓库根目录创建 CNAME 文件**
   ```bash
   echo "www.qkinteq.com" > CNAME
   ```

2. **提交并推送 CNAME 文件**
   ```bash
   git add CNAME
   git commit -m "Add custom domain CNAME"
   git push origin main
   ```

   > **注意**：CNAME 文件内容只需要一行：`www.qkinteq.com`（不要包含 `http://` 或 `https://`）

#### 3.2 在 GitHub Pages 设置中验证域名

1. **回到 GitHub Pages 设置**
   - 在 Settings → Pages 页面
   - 你会看到 "Custom domain" 部分
   - 输入 `www.qkinteq.com` 并点击 **Save**

2. **等待 DNS 检查**
   - GitHub 会检查你的 DNS 配置
   - 如果配置正确，会显示绿色的勾选标记

---

### 第四步：配置 DNS 记录

在你的域名注册商（如 GoDaddy、Namecheap、Cloudflare 等）配置 DNS 记录：

#### 4.1 登录域名管理面板

- 登录你购买 `qkinteq.com` 域名的服务商网站
- 找到 DNS 管理或域名设置页面

#### 4.2 添加 CNAME 记录

添加以下 DNS 记录：

```
类型: CNAME
名称: www
值: Stepup-Love-Ai.github.io
TTL: 3600 (或默认值)
```


**示例**：
- 如果你的 GitHub 用户名是 `Stepup-Love-Ai`
- 那么 CNAME 值应该是：`Stepup-Love-Ai.github.io`

#### 4.3 配置根域名（可选）

如果你也想让 `qkinteq.com`（不带 www）访问网站，需要添加 A 记录：

```
类型: A
名称: @ (或留空)
值: 185.199.108.153
TTL: 3600
```

然后添加另外三个 A 记录（GitHub Pages 的 IP 地址）：
```
185.199.109.153
185.199.110.153
185.199.111.153
```

---

### 第五步：启用 HTTPS

1. **在 GitHub Pages 设置中**
   - 找到 "Enforce HTTPS" 选项
   - 勾选此选项
   - 等待几分钟让 SSL 证书生效

2. **验证 HTTPS**
   - 访问 `https://www.qkinteq.com`
   - 确认浏览器地址栏显示锁图标 🔒

---

## 部署后更新网站

每次更新网站内容后，只需：

```bash
git add .
git commit -m "Update website content"
git push origin main
```

GitHub Pages 会自动检测到更改并重新部署，通常 1-2 分钟内完成。

---

## 部署前检查清单

在开始部署前，请确认：

- [ ] 所有文件已提交到 Git
- [ ] 代码已推送到 GitHub 仓库
- [ ] 测试所有页面链接是否正常
- [ ] 检查图片路径是否正确（使用相对路径）
- [ ] 确保所有页面都能正常访问
- [ ] 域名 `qkinteq.com` 已购买
- [ ] 可以访问域名的 DNS 管理面板

---

## 常见问题

### Q1: 部署后网站显示 404 错误？

**A:** 可能的原因：
- 检查 `index.html` 是否在仓库根目录
- 确认 GitHub Pages 设置中选择了正确的分支和文件夹
- 等待几分钟让部署完成

### Q2: 自定义域名不生效？

**A:** 检查以下几点：
- CNAME 文件内容是否正确（只有一行：`www.qkinteq.com`）
- DNS 记录是否正确配置
- 等待 DNS 传播（可能需要 5 分钟到 48 小时）
- 在 GitHub Pages 设置中验证域名状态

### Q3: 如何同时支持 www.qkinteq.com 和 qkinteq.com？

**A:** 
- CNAME 文件只能包含一个域名，建议使用 `www.qkinteq.com`
- 对于根域名，配置 A 记录指向 GitHub Pages 的 IP 地址
- 或者使用域名重定向服务，将 `qkinteq.com` 重定向到 `www.qkinteq.com`

### Q4: SSL 证书需要单独购买吗？

**A:** 不需要。GitHub Pages 提供免费的 SSL 证书，只需在设置中启用 "Enforce HTTPS" 即可。

### Q5: 部署后如何查看部署日志？

**A:** 
- 在 GitHub 仓库页面，点击 **Actions** 标签
- 可以看到每次部署的详细日志和状态

### Q6: 网站更新后没有变化？

**A:** 
- 清除浏览器缓存（Ctrl+Shift+R 或 Cmd+Shift+R）
- 检查 GitHub Actions 中部署是否成功
- 确认代码已正确推送到 main 分支

---

## DNS 配置详细说明

### 如果使用 GoDaddy：

1. 登录 GoDaddy 账户
2. 进入 "我的产品" → "DNS"
3. 找到 "记录" 部分
4. 点击 "添加" 创建新记录：
   - 类型：CNAME
   - 名称：www
   - 值：your-username.github.io
   - TTL：1 小时

### 如果使用 Namecheap：

1. 登录 Namecheap 账户
2. 进入 "域名列表" → 选择 `qkinteq.com` → "管理"
3. 找到 "高级 DNS" 标签
4. 在 "主机记录" 部分添加：
   - 类型：CNAME Record
   - 主机：www
   - 值：your-username.github.io
   - TTL：自动

### 如果使用 Cloudflare：

1. 登录 Cloudflare 账户
2. 选择你的域名
3. 进入 "DNS" → "记录"
4. 添加记录：
   - 类型：CNAME
   - 名称：www
   - 目标：your-username.github.io
   - 代理状态：仅 DNS（灰色云朵）

---

## 验证部署

部署完成后，访问以下地址验证：

1. **GitHub Pages 默认地址**：
   ```
   https://Stepup-Love-Ai.github.io/qkinteq-website-official/
   ```

2. **自定义域名**：
   ```
   https://www.qkinteq.com
   ```

两个地址都应该能正常访问你的网站。

---

## 需要帮助？

如果遇到问题：

1. **查看 GitHub Pages 文档**：
   https://docs.github.com/en/pages

2. **检查 DNS 配置**：
   - 使用在线工具如 https://dnschecker.org 检查 DNS 传播状态

3. **查看部署日志**：
   - 在 GitHub 仓库的 Actions 标签中查看详细错误信息

4. **常见错误排查**：
   - 确认 CNAME 文件格式正确
   - 检查 DNS 记录是否生效
   - 等待 DNS 传播完成（最多 48 小时）

---

## 总结

使用 GitHub Pages 部署网站的完整流程：

1. ✅ 推送代码到 GitHub
2. ✅ 在仓库设置中启用 Pages
3. ✅ 创建并推送 CNAME 文件
4. ✅ 配置 DNS 记录
5. ✅ 启用 HTTPS
6. ✅ 验证网站访问

完成以上步骤后，你的网站就可以通过 `https://www.qkinteq.com` 访问了！
