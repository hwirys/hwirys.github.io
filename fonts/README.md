# Birthday typography

The current invitation and public birthday page use **Gowun Dodum** for their rounded, gentle headings and the unmodified **Pretendard Variable v1.3.9**, by Kil Hyung-jin, for readable body text and controls. The local `pretendard-variable.woff2` provides all weights and Korean glyphs without a runtime CDN request. Original source: https://github.com/orioncactus/pretendard/tree/v1.3.9/packages/pretendard/dist/web/variable/woff2 ; SIL OFL 1.1 is included as `Pretendard-OFL.txt`.

The following Gowun fonts are also available for in-game reading panels and earlier designs.

Self-hosted WOFF2, generated from Google Fonts' official source distribution:

- Gowun Dodum Regular: https://github.com/google/fonts/tree/main/ofl/gowundodum
- Gowun Batang Bold: https://github.com/google/fonts/tree/main/ofl/gowunbatang
- Original designer: Yanghee Ryu. https://github.com/yangheeryu/Gowun-Dodum

Both are SIL Open Font License 1.1. Original copyright and license files are included alongside the fonts. This use does not imply the designer's endorsement.

Modified for web delivery using fontTools `pyftsubset --flavor=woff2 --layout-features='*' --no-hinting`:

- `gowun-dodum-korean.woff2`: Latin 0000–00FF, Korean jamo 1100–11FF/3130–318F, all modern Hangul AC00–D7A3, punctuation 2000–206F/3000–303F, arrows 2190–21FF and symbols 2600–266F. Full modern Hangul supports future supporter nicknames without depending on an installed Korean font.
- `gowun-batang-invitation-v2.woff2`: characters in BirthdayInvitation.ts, BirthdayTribute.ts and TitleScene.ts, including the interactive letter's new heading and signature. Regenerated on 2026-09-28; the original subset lacked `편` and `싶`. Regenerate the headline subset when those texts change. The old `gowun-batang-invitation.woff2` remains for cached earlier pages.

Only the compressed fonts are shipped, not the multi-megabyte TTF sources. No Google Fonts runtime request or third-party tracking.
