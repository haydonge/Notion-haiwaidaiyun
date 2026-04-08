# 🚀 Dokploy 快速部署指南

## 📋 部署前准备

### 1. 获取 Notion 页面 ID

1. 访问 [NotionNext 模板](https://tanghh.notion.site/02ab3b8678004aa69e9e415905ef32a5)
2. 点击右上角 "Duplicate" 复制模板到你的工作区
3. 分享页面并获取页面 ID（32位字符串）

### 2. 准备域名（可选）
- 准备好你的域名
- 将域名解析到你的 Dokploy 服务器

## 🎯 一键部署步骤

### 步骤 1：配置环境变量

复制环境变量文件：
```bash
cp .env.dokploy .env
```

编辑 `.env` 文件，**必须修改以下配置**：

```env
# ⚠️ 必填项
NOTION_PAGE_ID=你的Notion页面ID
DOMAIN=你的域名.com

# ✅ 已预设为你的项目信息
NEXT_PUBLIC_AUTHOR=海外代孕
NEXT_PUBLIC_BIO=海外合法代孕服务
NEXT_PUBLIC_LINK=https://suprebaby.com
NEXT_PUBLIC_KEYWORD=代孕官网,海外代孕,合法代孕
```

### 步骤 2：Dokploy 部署

1. **登录 Dokploy 控制台**
   - 打开你的 Dokploy 管理面板
   - 通常地址是：`http://你的服务器IP:3000`

2. **创建新应用**
   - 点击 "Create Project"
   - 选择 "Git Repository"
   - 填写应用信息：

3. **配置 Git 仓库**
   ```
   Repository: https://github.com/haydonge/Notion-haiwaidaiyun.git
   Branch: main
   Build context: ./
   Docker Compose: docker-compose.dokploy.yml
   ```

4. **设置环境变量**
   - 在 Dokploy 界面中找到 "Environment Variables"
   - 复制 `.env` 文件中的所有变量
   - 粘贴到 Dokploy 的环境变量设置中

5. **配置域名**
   - 在 "Domains" 选项卡中添加你的域名
   - Dokploy 会自动配置 HTTPS

6. **部署应用**
   - 点击 "Deploy" 按钮
   - 等待部署完成（通常需要 3-5 分钟）

## ✅ 部署成功验证

部署完成后，你可以：

1. **访问网站**
   - 通过配置的域名访问
   - 或通过 Dokploy 提供的临时链接访问

2. **查看日志**
   - 在 Dokploy 控制台查看实时日志
   - 确认没有错误信息

3. **测试功能**
   - 检查页面是否正常加载
   - 验证 Notion 数据是否正确显示

## 🔧 常见问题解决

### ❌ 部署失败

**问题**：部署过程中失败
**解决**：
1. 检查环境变量是否正确设置
2. 查看 Dokploy 日志中的具体错误
3. 确认 Notion 页面 ID 正确

### ❌ 页面空白

**问题**：访问页面显示空白
**解决**：
1. 检查 Notion 页面是否为公开
2. 确认页面 ID 正确
3. 查看浏览器控制台错误信息

### ❌ 样式加载失败

**问题**：页面样式异常
**解决**：
1. 清除浏览器缓存
2. 检查主题配置
3. 确认静态资源加载正常

## 📊 性能优化建议

### 缓存优化
```env
# 增加缓存时间（生产环境）
NEXT_PUBLIC_REVALIDATE_SECOND=300
```

### 数据库缓存（可选）
```env
# 如果需要更好的性能，配置 Redis
REDIS_URL=redis://redis:6379
```

## 🔄 更新部署

当代码更新时：

1. **自动更新**：Dokploy 会自动检测 Git 推送并重新部署
2. **手动更新**：在 Dokploy 控制台点击 "Redeploy"

## 📞 获取帮助

如果遇到问题：

1. 查看 Dokploy 官方文档
2. 检查容器日志：`docker logs notion-haiwaidaiyun`
3. 在 GitHub 提交 Issue

---

**🎉 恭喜！你的 NotionNext 博客已经成功部署到 Dokploy 上了！**