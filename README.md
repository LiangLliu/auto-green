# auto-green

[![Build Status](https://github.com/LiangLliu/auto-green/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/LiangLliu/auto-green/actions)

🌍 **语言**: **中文** | [English](README_EN.md)

自动保持 GitHub 提交状态常绿。

> a commit a day keeps your girlfriend away.

## 原理

使用 GitHub Actions 的定时任务功能，每隔一段时间自动执行 `git commit`，提交信息为 "a commit a day keeps your girlfriend
away"
，灵感来自知乎问题[在 GitHub 上保持 365 天全绿是怎样一种体验？](https://www.zhihu.com/question/34043434/answer/57826281)
下某匿名用户的回答：

> 曾经保持了 200 多天全绿，但是冷落了女朋友，一直绿到现在。

## 使用

- 点右上角 **Use this template** 按钮复制本 GitHub 仓库，**:warning: 千万不要 Fork，因为 fork 项目的动态并不会让你变绿 :
  warning:**
- 修改 [ci.yml 文件的第 19、20 行](https://github.com/LiangLliu/auto-green/blob/master/.github/workflows/ci.yml#L19) 为自己的
  GitHub 邮箱和用户名
- (可选)
  你可以通过修改 [ci.yml 文件的第 8 行](https://github.com/LiangLliu/auto-green/blob/master/.github/workflows/ci.yml#L8)
  来调整频率

**重要提醒**：

- 确保你的仓库是 **Public** 的，私有仓库的提交不会在 GitHub 个人首页显示为绿色
- 本项目使用 `GITHUB_TOKEN` 进行身份验证，这是 GitHub Actions 自动提供的，无需额外配置

计划任务语法有 5 个字段，中间用空格分隔，每个字段代表一个时间单位。

```plain
┌───────────── 分钟 (0 - 59)
│ ┌───────────── 小时 (0 - 23)
│ │ ┌───────────── 日 (1 - 31)
│ │ │ ┌───────────── 月 (1 - 12 或 JAN-DEC)
│ │ │ │ ┌───────────── 星期 (0 - 6 或 SUN-SAT)
│ │ │ │ │
│ │ │ │ │
│ │ │ │ │
* * * * *
```

每个时间字段的含义：

| 符号  | 描述   | 举例                                |
|-----|------|-----------------------------------|
| `*` | 任意值  | `* * * * *` 每天每小时每分钟              |
| `,` | 值分隔符 | `1,3,4,7 * * * *` 每小时的 1 3 4 7 分钟 |
| `-` | 范围   | `1-6 * * * *` 每小时的 1-6 分钟         |
| `/` | 每    | `*/15 * * * *` 每隔 15 分钟           |

**注**：

- 由于 GitHub Actions 的限制，如果设置为 `* * * * *` 实际的执行频率为每 5 分钟执行一次
- 默认设置为每日 UTC 时间 0:00 执行一次 (`0 0 * * *`)
- GitHub Actions 对于定时任务可能有延迟，实际执行时间可能会有几分钟的偏差

## 注意事项

- **环保提醒**：虽然这个项目很有趣，但请适度使用。过度的无意义提交可能会被视为垃圾信息
- **学习导向**：建议将此项目作为学习 GitHub Actions 的起点，而不是长期保持绿色的唯一方式
- **真实贡献**：最好的绿色方块来自于真实的代码贡献和有意义的项目

## 工作原理

本项目通过以下步骤实现自动提交：

1. **定时触发**：GitHub Actions 根据 cron 表达式定时执行
2. **环境准备**：在 Ubuntu 环境中检出代码
3. **Git 配置**：设置提交者信息
4. **身份验证**：使用 GitHub 提供的 `GITHUB_TOKEN` 进行认证
5. **同步代码**：拉取最新代码避免冲突
6. **空提交**：执行 `git commit --allow-empty` 创建空提交
7. **推送更改**：将提交推送到远程仓库

## 常见问题

**Q: 为什么要使用"Use this template"而不是 Fork？**
A: GitHub 只会显示你拥有或作为协作者的仓库中的贡献。Fork 的仓库不会计入你的贡献图表，除非你向原项目提交代码。

**Q: 这会影响我的 GitHub 统计数据吗？**
A: 会的，它会在你的贡献图表上显示绿色方块。但不会影响仓库洞察中的实际代码贡献统计。

**Q: 这是否违反了 GitHub 的服务条款？**
A: 这个项目不违反 GitHub 的服务条款，但请负责任地使用，不要滥用。

## License

[auto-green](https://github.com/LiangLliu/auto-green) is released under the MIT License. See the
bundled [LICENSE](./LICENSE) file for details.
