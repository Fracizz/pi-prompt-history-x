# pi-prompt-history-x

[English](README.md) · **简体中文**

在 pi 中按 ↑/↓ 找回上一条或下一条提示词，按 Ctrl+R 搜索历史。这个分支还会把技能调用恢复为 `/skill:name args`，并保留发送给模型的斜杠提示词。

[安装](#安装) · [快捷键](#快捷键) · [上游改动](https://github.com/ravshansbox/pi-prompt-history/pull/7)

## 安装

从 GitHub 安装指定版本。

```bash
pi install git:github.com/Fracizz/pi-prompt-history-x@v0.3.0
```

省略 `@v0.3.0` 可跟踪 `main` 的最新提交。加 `-l` 可安装到项目设置。原版 `@ravshansbox/pi-prompt-history` 也占用 Ctrl+R，使用同一个快捷键时只启用其中一个。

## 快捷键

在有历史会话的目录里打开新的 pi 交互式会话。扩展会将这个目录以前发送的提示词载入输入框历史。

| 按键        | 操作                                               |
| ----------- | -------------------------------------------------- |
| ↑ / ↓       | 光标在输入框顶部或底部时，找回上一条或下一条提示词 |
| Ctrl+R      | 打开模糊搜索。若输入框已有文本，会将它用作初始查询 |
| Tab         | 在当前目录和所有目录的历史之间切换                 |
| Enter / Esc | 将选中的提示词填入输入框，或关闭搜索               |

## 历史范围

- ↑/↓ 和 Ctrl+R 的默认搜索范围都是当前目录。切换到 **All folders** 可以搜索其他目录的会话。使用自定义会话目录时，以该目录为范围。
- 交互式会话中新提交的提示词会立即保存。空输入与行内 Bash（`!`、`!!`）会跳过。只有发送给模型的斜杠提示词会进入会话历史。
- 找回技能调用后，重新提交时会按当前技能说明执行。相同提示词只保留最近一次，第一次按 ↑ 会找回最新的内容。
- Ctrl+R 每个范围最多搜索最近 500 条不同的提示词。↑/↓ 使用 pi 内置的历史缓冲区，包含最近约 100 条和当前会话的新输入。

## 开发

```bash
npm install
npm run check
```

## 上游与许可证

本项目派生自 [Ravshan 的 pi-prompt-history](https://github.com/ravshansbox/pi-prompt-history)，沿用 [MIT 许可证](LICENSE)。技能与斜杠提示词的历史改动也[提交给了上游](https://github.com/ravshansbox/pi-prompt-history/pull/7)。上游合并后建议使用原版。
