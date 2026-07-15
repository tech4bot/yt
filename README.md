# Hack Around — Video Resources
 
Companion repository for the [Hack Around](https://www.youtube.com/@HackAround) YouTube channel.

## ⚠️ Disclaimer — read this first
 
All commands and scripts here are meant to be safe to use, but I cannot test them on every device, OS, or configuration — so **take everything with a grain of salt**. By using anything from this repo, you accept that **I take no responsibility if something goes wrong** (bricked devices, data loss, voided warranties, broken installs, you name it).
 
Before running anything:
 
- **Read and understand** what a command or script actually does — don't blind copy-paste.
- **Adapt it** to your own device, paths, and setup where needed.
- **If you're not sure — just don't run it.** Ask first: open an [issue](../../issues), leave a comment on the video, or paste the command into an AI assistant and ask it to explain what it does.
Many videos involve flashing firmware, opening hardware, or modifying system software. Proceed at your own risk.
 
Every video gets its own folder containing the scripts, commands, configs, and notes shown on screen — so you can copy-paste instead of pausing and typing. If you landed here from a video description, jump straight to the folder for that video below.
 
## 📼 Videos
 
| Published | Video | Resources |
|-----------|-------|-----------|
| 2026-07-16 | [Reverse Engineering Ep.1 — Evaluating Android Devices](https://youtu.be/hV__BqoP7aE) | [📁 2026-07-16-android-re-ep1](./2026-07-16-android-re-ep1) |
 
<!--
Row template — copy, fill in, keep newest on top:
| 2026-07-16 | [Reverse Engineering Ep.1 — Evaluating Android Devices](https://youtu.be/VIDEO_ID) | [📁 folder](./2026-07-16-android-re-ep1) |
-->
 
## 📂 Folder layout
 
Each video folder follows the same structure (files present only when relevant):
 
```
YYYY-MM-DD-topic/
├── README.md       # video link, summary, tools & hardware used
├── commands.md     # terminal commands in order of appearance
├── scripts/        # reusable scripts and tools
├── configs/        # docker-compose, systemd units, config files
└── resources.md    # datasheets, references, further reading
```
 
## 🔗 More from Hack Around
 
- YouTube: [Hack Around](https://www.youtube.com/@HackAround)
- GitHub: [tech4bot](https://github.com/tech4bot)
- Related project: [rk3562deb](https://github.com/tech4bot/rk3562deb) — Debian for RK3562 devices
## 📄 License
 
All scripts and content in this repo are released under the [MIT License](./LICENSE) unless noted otherwise in a specific folder.
