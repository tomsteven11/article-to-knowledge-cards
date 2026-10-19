# make-knowledge-cards v0.1.0 发布总结

- **发布日期**：2026-10-19
- **仓库**：https://github.com/tomsteven11/article-to-knowledge-cards
- **Release 页面**：https://github.com/tomsteven11/article-to-knowledge-cards/releases/tag/v0.1.0
- **版本标签**：`v0.1.0`（附注标签，指向提交 `86fdd9d`）
- **许可证**：MIT（Copyright (c) 2026 Tobby Logan）
- **维护者**：Tobby Logan（@tomsteven11）

## 一、项目定位

一个把文章变成知识卡片的 Agent Skill：粘贴文章正文或提供本地 Markdown/TXT 文件，自动提炼 5~8 张结构化知识卡片，用于复习与记忆。核心价值是用固定的提炼规则和卡片模板约束 AI 输出，避免手动整理笔记的耗时和 AI 常见的编造、注水问题。

## 二、当前功能（v0.1.0）

- **卡片结构**：每张卡片包含标题、核心知识、简明解释、例子或自测问题四部分
- **提炼规则**（内置约束）：
  - 只提取真正重要的知识（核心概念、因果机制、关键数据、可操作方法、误区澄清）
  - 一张卡片只讲一个知识点
  - 重复内容自动合并去重
  - 不编造原文没有的信息，例子只能来自原文
  - 信息不足时不强行凑数（可少于 5 张并说明原因）
- **输入**：粘贴的文本，或本地 `.md` / `.txt` 文件
- **输出**：默认在对话中输出，可按要求保存为 `.md` 文件；卡片语言与原文一致
- **暂不支持**：网页抓取（URL）、PDF、Anki 导出、图形界面

## 三、质量验证

- **结构验证**：通过官方 `quick_validate.py`（输出 "Skill is valid!"）
- **功能实测**（3 类文章）：
  - 中文技术文章（`.md`，HTTP 缓存主题）→ 7 张卡片，内容全部可溯源
  - 英文科普文章（`.txt`，睡眠与记忆主题）→ 6 张卡片，语言正确跟随英文原文
  - 信息稀薄的通知类短文 → 只输出 2 张并说明原因，未注水
- **测试驱动完善**：实测发现并修订 3 处规则——"误区澄清"纳入重要知识、对比型知识点合并规则、例子字段硬约束（禁止虚构例子）

## 四、提交历史

| 提交 | 说明 | 备注 |
|------|------|------|
| `fb3b9f1` | Initial commit: make-knowledge-cards Agent Skill | 首次提交（4 个文件，175 行） |
| `86fdd9d` | Set LICENSE copyright holder | **v0.1.0 标签指向此提交** |
| `96de5a7` | Link v0.1.0 release in README install section | 发布后追加（README 中加入 Release 链接），不包含在标签内 |

## 五、发布过程记录

1. `git init -b main` 初始化仓库并完成首次提交
2. 关联远程 `origin`（SSH 协议）：GitHub 直连超时，改走本机代理 `127.0.0.1:7890` 解决
3. `gh` CLI 设备授权两次：登录 + 补充 `admin:public_key` 权限范围
4. 上传本机 SSH 公钥（标题 `macbook-*`），验证认证通过
5. `gh repo create article-to-knowledge-cards --public --source . --remote origin --push` 一条命令完成建仓、添加远程、推送 main
6. 公开前安全检查：无密钥/隐私/绝对路径/临时文件，LICENSE 署名确认
7. 推送 LICENSE 署名修复 → 打附注标签 `v0.1.0` → 发布 GitHub Release（标题 `make-knowledge-cards v0.1.0`，含中文发布说明）

## 六、后续建议

- **版本策略**：遵循语义化版本（v0.1.x 修复与文档，v0.2.0 功能新增）
- **发布清单**：更新 README 版本链接 → 提交推送 → 打标签 → `gh release create`
- **可做增强**：为仓库添加 About 描述与 Topics（如 `agent-skills`、`knowledge-management`、`flashcards`）；发布 v0.2.0 时再考虑 CHANGELOG.md
