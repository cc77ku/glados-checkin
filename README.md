# GLaDOS-Checkin

GLaDOS 自动签到脚本 - 专用于 **glados.cloud**

## 功能特点

- ✅ 支持多账号签到（使用 `&` 分隔）
- ✅ 自动获取账号信息和剩余天数
- ✅ 每天自动执行两次（北京时间 10:00 和 22:00）
- ✅ 支持手动触发
- ✅ 仅适配 **glados.cloud** 域名

## 快速开始

### 1、获取 Cookie

1. 登录 [glados.cloud](https://glados.cloud)
2. 按 `F12` 打开开发者工具
3. 转到 `Application` 或 `应用程序` 标签页
4. 左侧选择 `Cookies` -> `https://glados.cloud`
5. 找到并复制以下 Cookie 的完整值：
   - `koa:sess`
   - `koa:sess.sig`

完整的 Cookie 格式应该像这样：
```
koa:sess=eyJxxxxxx; koa:sess.sig=xxxxxx
```

**多账号配置**：使用 `&` 分隔，例如：
```
koa:sess=cookie1; koa:sess.sig=sig1&koa:sess=cookie2; koa:sess.sig=sig2
```

### 2、配置 GitHub Secret

1. 进入仓库的 `Settings` -> `Secrets and variables` -> `Actions`
2. 点击 `New repository secret`
3. 输入：
   - **Name**: `GLADOS_COOKIE`
   - **Value**: 粘贴你的 Cookie 完整值
4. 点击 `Add secret`

### 3、启用 GitHub Actions

1. 进入仓库的 `Actions` 标签页
2. 如果看到提示，点击 `I understand my workflows, go ahead and enable them`
3. 选择 `GLaDOS Auto Checkin` workflow
4. 点击 `Run workflow` 按钮进行手动测试

## 自动签到时间

- 每天 UTC 02:00（北京时间 10:00）
- 每天 UTC 14:00（北京时间 22:00）

你也可以在 Actions 页面手动触发 workflow。

## 查看签到结果

1. 进入 `Actions` 标签页
2. 点击最近的 workflow 运行
3. 点击 `checkin` job
4. 展开 `Run checkin script` 步骤查看详细日志

## 注意事项

⚠️ **重要**：此脚本仅适配 **glados.cloud** 域名，不适用于其他域名（如 glados.rocks、glados.space 等）。

- 定时检查 Cookie 是否过期，如果签到失败需要重新获取 Cookie
- GitHub Actions 免费版每月有 2000 分钟的额度，足够使用
- 为了保持仓库活跃，建议每 60 天至少进行一次提交或操作

## 文件说明

- `checkin.py` - Python 签到脚本
- `.github/workflows/checkin.yml` - GitHub Actions 配置文件

## 故障排除

### Cookie 无效
如果看到 `✗ 错误: 未找到 GLADOS_COOKIE 环境变量` 或签到失败：
1. 检查 Secret 是否正确配置
2. 重新登录 glados.cloud 获取新的 Cookie
3. 更新 `GLADOS_COOKIE` Secret

### Workflow 未自动执行
1. 检查 Actions 是否已启用
2. 检查仓库是否公开（Private 仓库需要 Pro 计划）
3. 尝试手动触发一次

## License

MIT

## 声明

本项目仅供学习和交流使用，请遵守 glados.cloud 的服务条款。
