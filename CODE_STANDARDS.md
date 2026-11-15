# 代码规范与协作约定

## 分支与提交

- `main`：可提交版本；`develop`：集成分支；`feature/<name>`：功能分支。
- 每个功能通过 Pull Request 合并，至少 1 名队友 Review。
- 提交信息采用 `type: summary`：`feat`、`fix`、`docs`、`test`、`refactor`、`chore`。
- 合并前必须完成手工验收清单，并在 PR 描述中附测试结果。

## JavaScript

- 使用 `const`/`let`，禁止 `var`。
- 函数和变量使用 camelCase，DOM id 使用语义化英文名称。
- 用户输入渲染到页面前必须经过 `esc()` 转义。
- 一个函数尽量只承担一个职责；导入、导出、渲染、持久化相互独立。
- 不提交调试用 `console.log`、密钥、个人数据或构建产物。

## HTML/CSS

- HTML 使用语义化元素，表单控件必须有可读 label 或 placeholder。
- CSS 颜色、间距集中使用变量；布局优先使用 Grid/Flex。
- 保证窄屏宽度下主要功能可用。

## Review 清单

- [ ] 需求与验收标准明确
- [ ] 无明显 XSS/数据泄露问题
- [ ] 收藏、多个联系方式、Excel 导入导出均可操作
- [ ] 空数据、错误文件、删除确认等边界情况已验证
- [ ] README 和博客证据同步更新
