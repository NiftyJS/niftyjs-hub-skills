# NiftyJS Hub Skills

Bộ sưu tập Antigravity Skills cho hệ sinh thái NiftyJS.

## 📦 Available Skills

### [pod-market-research](./skills/pod-market-research/SKILL.md)

Hướng dẫn agent format output khi nghiên cứu thị trường POD (Print on Demand) trên Etsy và TikTok Shop. Tự động kích hoạt khi user hỏi về trending products, hot listings, keyword research.

**Yêu cầu**: MCP Server `niftyjs-hub` — xem [niftyjs-hub-mcps](https://gitlab.niftyjs.com/niftyjs/niftyjs-hub-mcps)

## 🚀 Cài đặt

### Cách 1: Paste vào Antigravity Chat

> Tải skill từ `https://gitlab.niftyjs.com/niftyjs/niftyjs-hub-skills/-/raw/master/skills/pod-market-research/SKILL.md` và lưu vào `~/.gemini/config/skills/pod-market-research/SKILL.md`.

### Cách 2: Command line

```bash
mkdir -p ~/.gemini/config/skills/pod-market-research

curl -sL https://gitlab.niftyjs.com/niftyjs/niftyjs-hub-skills/-/raw/master/skills/pod-market-research/SKILL.md \
  -o ~/.gemini/config/skills/pod-market-research/SKILL.md

echo "✅ Done"
```

### Cách 3: Clone repo

```bash
git clone git@gitlab.niftyjs.com:niftyjs/niftyjs-hub-skills.git ~/.gemini/config/skills-repo
ln -s ~/.gemini/config/skills-repo/skills/pod-market-research ~/.gemini/config/skills/pod-market-research
```
