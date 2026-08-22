# NiftyJS Hub Skills

Bộ Antigravity Skills cho nghiên cứu thị trường POD (Print on Demand).

**Yêu cầu**: MCP Server `niftyjs-hub` — xem hướng dẫn cài đặt bên dưới.

## 📦 Available Skills

| Skill | Mô tả | Trigger |
|-------|--------|---------|
| [pod-report-format](./skills/pod-report-format/SKILL.md) | Format output chuẩn cho kết quả research | "tìm sản phẩm", "hot listings" |
| [pod-spy-hot-products](./skills/pod-spy-hot-products/SKILL.md) | Spy sản phẩm HOT, đánh giá khả năng clone | "spy", "clone", "winning products" |
| [pod-trend-discovery](./skills/pod-trend-discovery/SKILL.md) | Phát hiện trends đang lên, đề xuất ý tưởng | "trend", "xu hướng", "niche mới" |
| [pod-design-scaling](./skills/pod-design-scaling/SKILL.md) | Scale design đang có theo chiều ngang/dọc | "scale design", "mở rộng", "sub-niche" |
| [pod-cross-platform-arbitrage](./skills/pod-cross-platform-arbitrage/SKILL.md) | Tìm cơ hội chênh lệch Etsy ↔ TikTok | "arbitrage", "cross-platform" |
| [pod-video-marketing-spy](./skills/pod-video-marketing-spy/SKILL.md) | Phân tích video TikTok hiệu quả nhất | "video marketing", "spy video" |
| [pod-visual-inspiration](./skills/pod-visual-inspiration/SKILL.md) | Tìm cảm hứng visual, trích xuất quotes/text | "ý tưởng thiết kế", "pinterest", "aesthetic" |

## 🚀 Cài đặt

### Cách 1: Paste vào Antigravity Chat (nhanh nhất)

Cài MCP + tất cả skills:

> Cài MCP server `niftyjs-hub` với URL `https://mcps.niftyjs.com/mcp` vào `~/.gemini/config/mcp_config.json`. Sau đó tải tất cả skills từ repo `https://github.com/NiftyJS/niftyjs-hub-skills` — clone repo và tạo symlinks cho tất cả thư mục trong `skills/` vào `~/.gemini/config/skills/`.

### Cách 2: Command line

```bash
# 1. Cài MCP Server
python3 -c "
import json, os
cfg_path = os.path.expanduser('~/.gemini/config/mcp_config.json')
cfg = json.load(open(cfg_path)) if os.path.exists(cfg_path) else {'mcpServers': {}}
cfg.setdefault('mcpServers', {})['niftyjs-hub'] = {'url': 'https://mcps.niftyjs.com/mcp'}
json.dump(cfg, open(cfg_path, 'w'), indent=2)
print('✅ MCP server added')
"

# 2. Clone skills repo + symlink
git clone https://github.com/NiftyJS/niftyjs-hub-skills.git ~/.gemini/config/_niftyjs-skills
for skill in ~/.gemini/config/_niftyjs-skills/skills/*/; do
  name=$(basename "$skill")
  ln -sfn "$skill" ~/.gemini/config/skills/$name
done
echo "✅ All skills installed"
```

### Cách 3: Cài từng skill riêng lẻ

```bash
SKILL_NAME="pod-spy-hot-products"  # thay tên skill cần cài
mkdir -p ~/.gemini/config/skills/$SKILL_NAME
curl -sL "https://raw.githubusercontent.com/NiftyJS/niftyjs-hub-skills/master/skills/$SKILL_NAME/SKILL.md" \
  -o ~/.gemini/config/skills/$SKILL_NAME/SKILL.md
```
