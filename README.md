# dongge-soft-card-tutorial-video

栋哥柔和卡片教程视频 skill。

这个 skill 用于把口播/教程/知识分享视频包装成固定的竖屏卡片风格：

- 上方主题总结：主标题 + 副标题，概括整条视频主题。
- 中间 PPT 卡片：根据口播进度切换重点、步骤、对比或行动提示。
- 下方逐字稿字幕条：和语音同步，一字不差显示原始口播。
- 底部人物窗口：保留真人口播画面，使用稳定圆角视频窗。
- 文字动画：标题、卡片、字幕都需要有清晰但克制的动画。

## Usage

在 Codex 里调用：

```text
Use $dongge-soft-card-tutorial-video to package my talking-head video with a topic header, synchronized PPT cards, and exact transcript subtitles.
```

## Files

- `SKILL.md`: skill 主说明文件
- `agents/openai.yaml`: Codex UI 元数据
- `assets/reference-style-board.jpg`: 参考风格图
