# Dokploy 部署指南

## 概述

Dokploy 是一个开源的部署平台，可以轻松部署和管理 Docker 应用。本指南将帮助你把 NotionNext 项目部署到 Dokploy 上。

## 前置要求

1. 已安装 Dokploy 的服务器
2. 域名（可选，但推荐）
3. Notion 页面 ID

## 快速开始

### 1. 获取 Notion 页面 ID

1. 访问 https://tanghh.notion.site/02ab3b8678004aa69e9e415905ef32a5
2. 点击右上角的 "Duplicate" 复制模板
3. 在你的 Notion 工作区中找到复制的页面
4. 获取页面 URL 中的 ID（32位字符串）

### 2. 配置环境变量

复制环境变量模板：

```bash
cp .env.dokploy .env
```

编辑 `.env` 文件，修改以下关键配置：

```env
# 必填项
NOTION_PAGE_ID=你的Notion页面ID
DOMAIN=你的域名.com

# 网站信息（已预设为你的项目信息）
NEXT_PUBLIC_AUTHOR=海外代孕
NEXT_PUBLIC_BIO=海外合法代孕服务
NEXT_PUBLIC_LINK=https://suprebaby.com
NEXT_PUBLIC_KEYWORD=代孕官网,海外代孕,合法代孕
```

### 3. 部署到 Dokploy

#### 方法一：使用 Git 仓库

1. 登录 Dokploy 控制台
2. 创建新项目
3. 选择 "Git Repository"
4. 填写仓库信息：
   - Repository: `https://github.com/haydonge/Notion-haiwaidaiyun.git`
   - Branch: `main`
   - Build context: `./`
   - Docker Compose: `docker-compose.dokploy.yml`

5. 配置环境变量（在 Dokploy 界面中设置）
6. 点击部署

#### 方法二：手动部署

1. 将代码推送到你的 GitHub 仓库
2. 在 Dokploy 中创建应用
3. 上传 `docker-compose.dokploy.yml`
4. 配置环境变量
5. 部署应用

## 环境变量详解

### 基础配置
- `NOTION_PAGE_ID`: Notion 页面 ID（必填）
- `NEXT_PUBLIC_THEME`: 主题（默认：heo）
- `NEXT_PUBLIC_LANG`: 语言（默认：zh-CN）

### 网站信息
- `NEXT_PUBLIC_AUTHOR`: 网站作者
- `NEXT_PUBLIC_BIO`: 网站描述
- `NEXT_PUBLIC_LINK`: 网站地址
- `NEXT_PUBLIC_KEYWORD`: 关键词

### 功能配置
- `NEXT_PUBLIC_ENABLE_RSS`: 启用 RSS（默认：true）
- `NEXT_PUBLIC_REVALIDATE_SECOND`: 缓存时间（默认：60秒）

### 可选配置
- 分析统计（Google Analytics、百度统计等）
- 评论系统（Twikoo、 Cusdis 等）
- 广告配置（Google AdSense）

## 域名配置

### 自动 HTTPS

Dokploy 会自动为你的域名配置 HTTPS（使用 Let's Encrypt）。确保：

1. 域名已正确解析到服务器
2. 在 Dokploy 中正确设置了域名

### 手动配置

如果你不使用 Dokploy 的自动 HTTPS，可以手动配置：

```yaml
labels:
  - "traefik.enable=true"
  - "traefik.http.routers.notion-next.rule=Host(`your-domain.com`)"
  - "traefik.http.routers.notion-next.entrypoints=web"
```

## 故障排除

### 常见问题

1. **部署失败**
   - 检查环境变量是否正确设置
   - 查看 Dokploy 日志
   - 确保 Notion 页面 ID 正确

2. **页面空白**
   - 检查 Notion 页面是否为公开
   - 确认页面 ID 正确
   - 查看浏览器控制台错误

3. **样式问题**
   - 尝试清除浏览器缓存
   - 检查主题配置

### 查看日志

```bash
# 查看容器日志
docker logs notion-haiwaidaiyun

# 实时查看日志
docker logs -f notion-haiwaidaiyun
```

## 性能优化

### 缓存配置

```env
# 增加缓存时间（生产环境）
NEXT_PUBLIC_REVALIDATE_SECOND=300
```

### 数据库缓存（可选）

如果需要更好的性能，可以配置 Redis：

```env
REDIS_URL=redis://redis:6379
```

## 安全建议

1. 定期更新代码和依赖
2. 使用强密码和环境变量
3. 配置适当的防火墙规则
4. 定期备份 Notion 数据

## 更新部署

当代码更新时：

1. 推送新代码到 GitHub
2. Dokploy 会自动检测并重新部署（如果设置了自动部署）
3. 或者手动触发重新部署

## 支持

如遇到问题，可以：

1. 查看 Dokploy 文档
2. 检查 NotionNext 文档
3. 查看容器日志
4. 在 GitHub 提交 Issue