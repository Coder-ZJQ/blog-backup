---
title: vscode 更改显示语言
date: 2016-10-23 09:31:48
categories: 
- Technology
- Tips
- VSCode
tags: 
- VSCode
---
## Configure Language 指令
1. `shift` + `command` 唤出 **Command Palette**
2. 输入 `Configure Language` 确定
3. 编辑 `locale.json` 文件
``` json
{
    // 定义 VSCode 的显示语言。
    // 请参阅 https://go.microsoft.com/fwlink/?LinkId=761051，了解支持的语言列表。
    // 要更改值需要重启 VSCode。
    "locale":"en"
}
```
## 可选的语言环境

| Display Language    | Locale  |
| ------------------- | ------- |
| English (US)        | `en`    |
| Simplified Chinese  | `zh-CN` |
| Traditional Chinese | `zh-TW` |
| French              | `fr`    |
| German              | `de`    |
| Italian             | `it`    |
| Japanese            | `ja`    |
| Korean              | `ko`    |
| Russian             | `ru`    |
| Spanish             | `es`    |