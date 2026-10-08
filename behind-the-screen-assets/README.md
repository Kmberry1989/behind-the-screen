# behind-the-screen-assets/ — placeholder art & audio

Drop-in asset folder for `behind-the-screen.html` (keep this folder **next to the
HTML file**, e.g. both at the root of your GitHub repo). The game looks for each
file at the path shown below, relative to the HTML file:

```
repo/
  behind-the-screen.html   (or index.html)
  behind-the-screen-assets/
    ...
```

**How the auto-wiring works:** on load, the page tries to fetch every file in the
`ASSETS` map at the top of the page's script. Any file that loads successfully
replaces the built-in procedural fallback (emoji / CSS shapes / WebAudio synth).
Any file that is missing, corrupt, or in an unsupported format is silently
ignored and the fallback is used instead — so you can replace files one at a
time, and deleting a file always restores the built-in version. To point a slot
at a differently-named file, edit the `ASSETS` map in the HTML (keys are listed
in the last column below).

## Visuals

| File | Dimensions | Used for | Asset key |
|---|---|---|---|
| `os/wallpaper.png` | **1170 × 2532** (iPhone 14 portrait) | Mock-iPhone home-screen wallpaper | `os.wallpaper` |
| `os/icons/mail.png` | **180 × 180** | Mail app icon | `os.icon.mail` |
| `os/icons/messages.png` | **180 × 180** | Messages app icon | `os.icon.messages` |
| `os/icons/safari.png` | **180 × 180** | Safari app icon | `os.icon.safari` |
| `os/icons/photos.png` | **180 × 180** | Photos app icon | `os.icon.photos` |
| `os/icons/camera.png` | **180 × 180** | Camera app icon | `os.icon.camera` |
| `os/icons/settings.png` | **180 × 180** | Settings app icon | `os.icon.settings` |
| `os/icons/appstore.png` | **180 × 180** | App Store app icon | `os.icon.appstore` |
| `os/icons/phone.png` | **180 × 180** | Phone dock icon | `os.icon.phone` |
| `os/icons/bingo-winner-icon.png` | **180 × 180** | Bingo Winner app icon (the one that wiggles) | `os.icon.bingo` |
| `app/splash-logo.png` | **1024 × 512**, transparent | Bingo Winner splash-screen logo | `app.splashLogo` |
| `app/bingo/card-bg.png` | **1080 × 1080** | Bingo card background (the 5×5 grid) | `app.bingo.cardBg` |
| `app/bingo/ball.png` | **512 × 512**, transparent | Called-ball graphic (drawn behind the "B 12" text) | `app.bingo.ball` |
| `app/slots/machine-bg.png` | **1080 × 720** | Slot-machine cabinet background | `app.slots.machineBg` |
| `app/slots/reels/cherry.png` | **512 × 512**, transparent | 🍒 reel symbol | `app.slots.reel.cherry` |
| `app/slots/reels/lemon.png` | **512 × 512**, transparent | 🍋 reel symbol | `app.slots.reel.lemon` |
| `app/slots/reels/bell.png` | **512 × 512**, transparent | 🔔 reel symbol | `app.slots.reel.bell` |
| `app/slots/reels/star.png` | **512 × 512**, transparent | ⭐ reel symbol | `app.slots.reel.star` |
| `app/slots/reels/diamond.png` | **512 × 512**, transparent | 💎 reel symbol | `app.slots.reel.diamond` |
| `app/slots/reels/seven.png` | **512 × 512**, transparent | 7️⃣ reel symbol | `app.slots.reel.seven` |

Notes:
- Icons are displayed at ~57 px with a ~15 px corner radius; 180 × 180 source
  files stay crisp on retina screens. Any square PNG works — transparency is
  fine.
- Reel symbols are rendered at ~72% of the reel window with `object-fit:
  contain`; keep the symbol centered with transparent padding.
- The placeholders in this folder are exactly these dimensions with labels, so
  you can measure against them.

## Audio

| File | Length / format | Used for | Asset key |
|---|---|---|---|
| `app/audio/music-splash.wav` | ~6.9 s loop, 22050 Hz mono 16-bit | Background music (whole page) | `app.audio.music.splash` |
| `app/audio/music-slots.wav` | ~6.9 s loop, 22050 Hz mono 16-bit | Background music while the Slots section is on screen (crossfades from splash music) | `app.audio.music.slots` |
| `app/audio/sfx-coin.wav` | ~0.4 s | Coin/win blip | `app.audio.sfx.coin` |
| `app/audio/sfx-fanfare.wav` | ~0.8 s | Claim / big-win fanfare | `app.audio.sfx.fanfare` |
| `app/audio/sfx-click.wav` | ~0.08 s | UI tap click | `app.audio.sfx.click` |
| `app/audio/sfx-notif.wav` | ~0.5 s | Phone notification ding | `app.audio.sfx.notif` |
| `app/audio/sfx-pop.wav` | ~0.12 s | Bingo ball-call pop | `app.audio.sfx.pop` |

Notes:
- Any of **.wav / .mp3 / .ogg / .m4a** works — just keep the same filename or
  update the `ASSETS` map.
- The placeholder WAVs are real synthesized audio (rendered from the same
  melodies the page synthesizes live), so they loop cleanly and sound fine
  until you replace them with your own tracks.
- Music files should be seamless loops; the page plays them with `loop=true`.
- Audio only starts after a user tap (browser autoplay policy) via the music
  toggle or TAP TO PLAY.

## Replacing files

1. Export your art at the dimensions in the table above (or any size — the page
   scales with `cover`/`contain`).
2. Overwrite the file with the same name, or add your file and update the
   matching path in the `ASSETS` map inside `behind-the-screen.html`.
3. Push to GitHub — no code changes needed; the next page load picks it up.
4. To revert any slot to the built-in procedural version, just delete the file.
