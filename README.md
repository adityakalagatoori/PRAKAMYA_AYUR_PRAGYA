# AYUR PRAGYA: site, audio and design workflow

The GitHub Pages site lives in `docs/`. Pages serves `docs/index.html` at the repo's Pages URL.

## Files

| Path | What it is |
|---|---|
| `docs/index.html` | The page: documents, team explanations, prototype screens |
| `docs/PRAKAMYA_AYUR_PRAGYA_Round1_Abstract.pdf` | Phase 1 abstract |
| `docs/AYUR_PRAGYA_Final_Proposal.pdf` | Full proposal |
| `docs/images/` | Figure images used on the page |
| `docs/audio/` | Team voice notes (see below) |

## Audio workflow (team voice notes)

1. Record each voice note from the script. Keep one take per person.
2. Clean it with ffmpeg. This is the chain used for the earlier narration files (high-pass, click removal, gentle noise reduction, loudness normalisation, limiter, short fade-in):

   ```
   ffmpeg -i input.m4a -af "highpass=f=80,adeclick,afftdn=nf=-25,loudnorm=I=-16:TP=-1.5:LRA=11,alimiter=limit=0.95,afade=t=in:st=0:d=0.1" -ac 1 -ar 44100 -b:a 128k docs/audio/aditya.mp3
   ```

3. Name the output exactly as the page expects:
   - `docs/audio/aditya.mp3`
   - `docs/audio/apurva.mp3`
   - `docs/audio/aswin.mp3`
   - `docs/audio/preenithi.mp3`
4. Listen once in a browser. Check there are no clicks or hiss, and that the voice is clear at 1x, 1.5x and 2x.
5. Commit and push. Until a file exists, its card shows "Voice note to be added." and the buttons are disabled.

## Design workflow

- Colours are CSS tokens at the top of `docs/index.html` (`--accent`, `--bg`, `--card`, and so on). Dark mode is handled by the same tokens, so change a token once and both themes update.
- Figures are PNG files in `docs/images/`. Keep the file names so the captions still match. Keep each figure under about 2.5 MB; if a new export is larger, resize it to 1600 px wide first.
- Mock-ups must stay labelled as design mock-ups with synthetic patients and illustrative numbers.
- Phone width: the page keeps a 16 px side gutter and does not scroll sideways. Check it at about 400 px wide before pushing.

## Publishing

```
git add docs
git commit -m "Update AYUR PRAGYA site"
git push origin main
```

GitHub Pages rebuilds in about a minute. Hard-refresh the page after each change, because the browser may hold an older copy.
