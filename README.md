# 1:1 视频复刻 Skill

把有权使用的参考视频拆成可核对的镜头信息，再生成可直接使用的 Seedance 提示词，或用于重拍与版本差异检查。

> **1:1 是重建目标，不是生成保证。** 视频参考、首帧锚点、剪辑和逐版比对，通常比不断加长提示词更能控制差异。

## 能做什么

| 模式 | 适合的请求 | 输出 |
| --- | --- | --- |
| Seedance Direct | 按参考视频生成新视频 | 逐镜头字段与完整提示词 |
| Reference Analysis | 拆解、测量、建蓝图 | 镜头、动作、机位、光色和统一时间轴 |
| Reshoot Blueprint | 真人或实体产品重拍 | 机位、灯光、站位、时间提示和叠帧建议 |
| Difference Detection | 已有参考版和复刻版 | 同步对比、误差分级和局部修正清单 |

技能会区分参考视频与新人物、产品照片各自的用途。用户明确指定的产品数量、颜色和结构优先于参考视频中的产品数量。对于画面文字，默认输出无可读文字的生成提示词；口播只作为声音处理。

## 安装

把整个仓库复制到 Codex 的技能目录，让 `SKILL.md` 位于 `one-to-one-video-replica/SKILL.md`：

```powershell
git clone https://github.com/haibo0505/one-to-one-video-replica.git
New-Item -ItemType Directory -Force -Path (Join-Path $env:USERPROFILE '.codex\skills') | Out-Null
Copy-Item -Recurse -Force -LiteralPath '.\one-to-one-video-replica' -Destination (Join-Path $env:USERPROFILE '.codex\skills\one-to-one-video-replica')
```

已经安装过时，先在自己的技能目录中检查本地改动，再更新相应文件。

## 使用

在对话中调用 `$one-to-one-video-replica`，同时提供你有权使用的参考视频及所需产品、人物、音频素材。例如：

```text
使用 $one-to-one-video-replica。
参考视频负责镜头顺序、动作和节奏；产品照片负责鞋型。
目标产品只有酒红、白、黑三种颜色，群组镜头每色一只，总共三只。
请按镜头输出可直接使用的 Seedance 提示词。
```

也可以要求“只分析参考视频”“给我重拍蓝图”，或同时上传参考版和复刻版，让技能列出局部修正项。

## 文件

- `SKILL.md`：路由、输入映射、提示词格式和使用边界。
- `references/frame-reconstruction-playbook.md`：帧级分析、镜头与差异检查的详细工作手册。
- `agents/openai.yaml`：技能在 Codex 中的显示信息。
- `test-prompts.json`：典型请求及预期输出，可用来做人工回归检查。

## 使用边界

- 仅对你有权使用的参考素材进行复刻或修改。
- 无参考素材时只能提供文字近似方案，不能声称达到逐帧一致。
- 外部付费生成需要用户单独授权；本技能首先输出可检查的提示词。
- 生成结果出现产品身份、数量、切点或声音误差时，优先补充视觉锚点并局部修正。

## 许可

[MIT License](LICENSE) © 2026 haibo0505。
