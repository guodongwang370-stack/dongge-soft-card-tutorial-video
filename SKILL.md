---
name: dongge-soft-card-tutorial-video
description: Create Dongge-style soft, minimal, card-based vertical tutorial videos for talking-head lessons with Codex and HyperFrames. Use when the user wants to package a口播/教程/知识分享 video into the reference layout with a theme summary header, synchronized PPT-style progress cards, exact verbatim transcript subtitle strip, rounded talking-head window, text animations, and final MP4 rendering. Trigger for requests like 栋哥卡片教程视频, 学习附件视频风格, 做成这个风格, 卡片式教程视频, 口播视频包装, Codex视频包装, HyperFrames剪辑, 逐字稿同步字幕, PPT风格卡片, or turn this reference style into a reusable skill.
---

# 柔和卡片教程视频

## Overview

把口播类知识视频包装成固定的四层竖屏结构：上方主题总结区、中间 PPT 风格内容卡片、下方逐字稿字幕条、底部人物视频窗。这个 skill 的核心不是“套一个好看的模板”，而是把口播内容转成和语音进度同步的教学型卡片视频。

参考风格板在 `assets/reference-style-board.jpg`。需要确认视觉细节时先看它，但不要照搬其中的专有文案、水印、人物或版权元素。

Hard rules:

- Always transcribe or load the user's exact script before writing visible copy.
- Never place generic placeholder copy on cards when a real voice track exists.
- Keep three text layers separate: theme summary, PPT progress cards, and exact transcript subtitles.
- Animate text as well as cards. Static text-only cards are not acceptable.

## Four-Layer Layout

Use a vertical canvas by default: `1080x1920`.

Layer order from top to bottom:

1. Theme summary header.
2. PPT-style content/progress card area.
3. Exact transcript subtitle strip.
4. Rounded talking-head video window.

Approximate zones:

- Header zone: top 110-360px.
- PPT card zone: about 420-930px.
- Verbatim subtitle strip: about 980-1120px.
- Talking-head zone: about 1180-1840px.

Keep generous margins and clear separation between layers. Do not let the subtitle strip cover the speaker's face or merge visually with the PPT card.

## Layer 1: Theme Summary Header

Purpose: summarize the whole video's topic. This area is not a subtitle and does not follow each spoken sentence.

Content rules:

- Derive the header after reading the full transcript.
- Use two text levels:
  - Main title: the compressed core topic of the whole video.
  - Subtitle: a short supporting line that explains the direction, benefit, or angle.
- The header should answer: “这条视频主要讲什么？”
- It should stay stable for the whole video unless the user explicitly asks for chapter headers.
- Do not put verbatim transcript here unless the spoken line is truly the best topic summary.

Layout rules:

- Small top-left label: topic family, such as `CODEX 视频包装`.
- Optional top-right label: series marker, such as `FULL VERSION` or `SHORT VERSION`.
- Main title: 44-64px, left aligned, one or two lines.
- Subtitle/supporting line: smaller than the main title; place under or near the title when needed.
- Thin divider line below the title area.

## Layer 2: PPT-Style Progress Cards

Purpose: explain the video's structure like a compact PPT slide. These cards summarize the current section, step, comparison, or key point.

Content rules:

- Card copy must come from the transcript's semantic structure.
- It may summarize the current spoken idea, but it must not invent unrelated content.
- If the video has steps, show step cards.
- If the video has a contrast, show comparison cards.
- If the video has a process, show flow cards.
- If the video has one central point, show a hero card plus emphasis bar.

Synchronization rules:

- Build a beat map before rendering: `start`, `end`, `spoken_line`, `ppt_card_text`, `active_item`, `subtitle_text`, `emphasis_words`.
- The active PPT card state must match the video progress.
- When the speaker enters a new step or idea, update the active card, highlight, or card content.
- Do not show all progress cards statically for the whole video unless they are intentionally a roadmap; even then, the current item must highlight as the voice reaches it.

Card types:

- Hero card: opening claim or section summary.
- Step list: 2-5 stacked pill cards with numbers `01/02/03`.
- Step detail card: small label, large headline, and a green emphasis bar.
- Two-column comparison cards: “以前 / 现在”, “问题 / 方法”, or paired concepts.
- Flow card: 3 small cards connected by arrows.
- Note card: a short warning or reminder.

## Layer 3: Exact Transcript Subtitle Strip

Purpose: show the actual spoken words at the bottom of the card area.

This layer must be a verbatim transcript:

- Do not summarize.
- Do not rewrite.
- Do not polish.
- Do not replace with “轻度概括版”.
- Keep the spoken wording exactly, including natural spoken phrasing, unless the user explicitly approves cleanup.

Synchronization rules:

- Display the current spoken sentence or short phrase according to the timeline.
- The text must change with the voice progress.
- If ASR is uncertain, mark it in working notes and ask for confirmation before using it as final subtitle text.
- For long sentences, split visually into two lines, but do not change the words.

Layout rules:

- Place a white rounded strip between PPT card area and talking-head window.
- Keep 1-2 lines max.
- Center align by default.
- Use 30-38px for 1080x1920 output.

## Layer 4: Talking-Head Window

Purpose: preserve the human presence while the cards explain the content.

Rules:

- Bottom-centered rounded rectangle, about 650-760px wide on 1080px output.
- Use 24-36px corner radius, thin white/cream stroke, and soft shadow.
- Crop speaker to upper body or head-and-shoulders.
- Keep the speaker window stable; do not bounce or constantly zoom it.
- Keep enough bottom breathing room.

## Visual System

Core look:

- Background: warm off-white or light beige, not pure white.
- Decorative shapes: very soft pastel blobs in pale pink and pale green, low opacity.
- Cards: rounded rectangles with subtle border and soft shadow.
- Text color: warm charcoal for normal text, muted brown/red for emphasis.
- Accent colors: dusty rose and sage green.

Suggested palette:

- Canvas: `#F7F1EA`
- Card: `#FFFDF8`
- Card border: `#DDD4CA`
- Main text: `#5D5650`
- Muted text: `#8A8178`
- Rose accent: `#A87570`
- Pale rose fill: `#F5E7E3`
- Sage fill: `#EAF2E8`
- Sage bar: `#C8D8BF`

Typography:

- Use a clean Chinese sans-serif for Chinese body text: system UI, PingFang SC, Noto Sans SC, or Microsoft YaHei.
- Use a restrained serif only for small English labels or final emphasis if available.
- Avoid exaggerated bold display fonts.

## Required Workflow

Before rendering:

1. Inspect the source video: duration, aspect ratio, audio availability, and whether it already has subtitles.
2. Transcribe the voice track or load the exact user-provided script.
3. Build the full transcript timeline.
4. Derive the theme summary header from the full transcript.
5. Split the transcript into semantic beats for PPT cards.
6. Build a beat map with exact subtitle text and active card states.
7. Render only after the beat map exists.

If transcription is unavailable and the user has not provided the script, do not produce a final version with guessed copy. Ask for the口播稿 or clearly mark the output as a visual-only draft.

## Text Animation Rules

Text animation is required.

Use restrained animations:

- Theme title: fade in and move up slightly; subtitle follows after 0.1-0.2s.
- PPT card: card fades/slides in first, then card label, headline, chips, and emphasis bar appear in sequence.
- Active progress item: highlight when its spoken section begins.
- Subtitle strip: fade or slide in at sentence changes; optionally reveal phrase by phrase.
- Key words: use subtle color shift, underline/bar reveal, or 1.03 scale pulse.

Do not animate every single character unless the user asks for a typewriter effect. The transcript subtitle may be phrase-level or sentence-level animated, but the wording must remain exact.

## HyperFrames Implementation

Use the `hyperframes` and `hyperframes-cli` skills when building the actual video.

Requirements:

- Create or update `DESIGN.md` with this style before writing composition HTML.
- Use `npx hyperframes init` when starting a new project.
- Store the beat map in the project as a readable JSON or Markdown planning file.
- Put the original video on a muted video track and add its audio as a separate audio track.
- Keep the talking-head video in a CSS-clipped wrapper; animate the wrapper only if needed.
- Register all timelines in `window.__timelines`.
- Run `npx hyperframes lint`, then `npx hyperframes inspect`, then preview, then render.
- Hand back the Studio URL for preview and the final MP4 path.

For non-HyperFrames fallback rendering, keep the same four-layer structure and verify frame samples manually.

## Quality Bar

Before final delivery, verify:

- Header summarizes the whole video with a main title and subtitle.
- PPT cards match the current video progress.
- Bottom subtitle strip is a verbatim transcript and synchronized to the voice.
- Visible text has animation.
- No text overlaps or spills outside cards.
- Subtitle strip never covers the speaker's face.
- Speaker window stays visually stable.
- Cards are readable on a phone screen.
- Final video can play from beginning to end.

## Anti-Patterns

Avoid:

- Generic card copy unrelated to the actual voiceover.
- Using the same text for header, PPT card, and transcript subtitle.
- Rewriting the verbatim subtitle strip into polished copy.
- Static PPT cards with no active progress or text animation.
- Full-screen karaoke subtitles.
- Bright saturated colors or cyber/tech gradients.
- Too many stickers, arrows, or attention effects.
- Dense paragraph cards that look like copied document pages.
- Covering the speaker with subtitles or cards.
- Copying the reference video's exact proprietary text, person, or branding unless the user owns it.
