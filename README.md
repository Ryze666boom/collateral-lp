# 抵押用户裂变 H5 落地页

## 文件说明

| 文件 | 说明 |
|------|------|
| `index.html` | 落地页主文件（老用户入口 + 新用户受邀） |
| `poster.html` | 海报模板（可用于生成分享图片） |

## 页面流程

```
老用户入口页
    ↓ 输入手机号
成功页（显示专属链接 + 海报 + 分享按钮）
    ↓ 分享链接
新用户受邀页（显示50元券 + 服务入口）
    ↓ 选择服务
联系客服成交
```

## 部署方式

### 方式1：GitHub Pages（免费）

```bash
# 1. 上传文件到 GitHub 仓库
# 2. 开启 GitHub Pages
# 3. 访问 https://你的用户名.github.io/仓库名/
```

### 方式2：阿里云 OSS（推荐）

```bash
# 1. 开通阿里云 OSS
# 2. 创建 bucket，设置静态网站托管
# 3. 上传 index.html
# 4. 绑定自定义域名（可选）
```

### 方式3：Vercel / Netlify

```bash
# 1. 连接 GitHub 仓库
# 2. 自动部署
# 3. 获取访问地址
```

## 客服链接配置

在 `index.html` 中找到：

```javascript
document.getElementById('contact-btn').href = 
    'https://work.weixin.qq.com/kfid/YOUR_KFID?text=' + 
    encodeURIComponent('我想' + service + '，我有50元券');
```

将 `YOUR_KFID` 替换为你的企业微信客服链接。

## 数据追踪

当前版本使用 URL 参数 `?from=手机号` 追踪来源。

如需更完善的数据追踪，可对接数据库：

```javascript
// 提交手机号时
fetch('/api/submit', {
    method: 'POST',
    body: JSON.stringify({ phone: phone })
});

// 获取邀请来源
const fromUser = getQueryParam('from');
```

## 后续优化建议

- [ ] 对接数据库，自动记录邀请关系
- [ ] 生成真实二维码（可使用草料二维码API）
- [ ] 对接企业微信，自动发放优惠券
- [ ] 数据后台，查看邀请数据
- [ ] 海报自动生成（后端渲染）