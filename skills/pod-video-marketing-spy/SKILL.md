---
name: pod-video-marketing-spy
description: >-
  Kích hoạt khi người dùng muốn phân tích video marketing TikTok, tìm video hiệu quả,
  hoặc học cách làm content cho sản phẩm POD.
  Trigger khi user nhắc: 'video marketing', 'tìm video', 'spy video', 'content TikTok',
  'video bán hàng', 'influencer', 'viral video', 'video strategy', 'hook', 'UGC'.
---

# POD Video Marketing Spy — Phân tích video TikTok hiệu quả

Khi user muốn học cách làm video marketing hoặc tìm video reference, thực hiện workflow sau.

## Bước 1: Thu thập top videos

Gọi `tiktok_browse_videos` với 2 lần, sort khác nhau:

1. **Sort by views** (order: `views_count`): Video viral nhất → learn về hook/format
2. **Sort by sales** (order: `sales`): Video bán hàng nhiều nhất → learn về conversion

Nếu user cho keyword/niche → truyền vào `keyword`.
Nếu có date range → truyền `start_time`, `end_time`.

## Bước 2: Phân biệt 2 loại video

### 🔥 Viral Videos (high views, low sales):
- Giỏi thu hút attention nhưng chưa convert
- Học được: **Hook**, **format**, **trend sound**
- Không nên copy 100% — chỉ lấy inspiration

### 💰 Converting Videos (moderate views, high sales):
- Biết cách convert viewer → buyer
- Học được: **CTA**, **product showcase**, **urgency**
- ĐÂY là mục tiêu chính để spy

### 🏆 Unicorn Videos (high views + high sales):
- Hiếm, nhưng cực kỳ giá trị
- Phân tích kỹ: Tại sao video này VỪA viral VỪA convert?

## Bước 3: Phân tích pattern

Với top 10-15 videos, phân tích:

### Video Format:
- 📦 **Unboxing/Reveal**: Mở hộp sản phẩm → tạo surprise
- 🎭 **UGC (User Generated)**: Người thật dùng sản phẩm → authentic
- 🖼️ **Showcase/Slideshow**: Zoom vào design → simple, scalable
- 😂 **Meme/Trend**: Gắn sản phẩm vào trend → viral potential
- ✨ **Before/After**: Transform → satisfying
- 🗣️ **Talking Head**: Người nói về sản phẩm → trust

### Hook Analysis (3 giây đầu):
- **Question hook**: "Bạn có biết...?" / "Why do all dog moms need this?"
- **Statement hook**: "This is the best gift for..." / "I can't believe..."
- **Visual hook**: Sản phẩm xuất hiện ngay frame 1
- **Controversy hook**: "Unpopular opinion..." / "Stop buying..."

### Duration:
- < 15s: Quick showcase → tốt cho scroll-stopping
- 15-30s: Sweet spot cho conversion
- 30-60s: Story-telling → tốt cho UGC
- > 60s: Hiếm khi effective cho POD

### Influencer Tier:
- 📱 **Nano** (1K-10K): Cheap, authentic, niche-specific
- 👤 **Micro** (10K-100K): Best ROI cho POD
- ⭐ **Macro** (100K-1M): Expensive, broad reach
- 🌟 **Mega** (1M+): Brand awareness, ít conversion

## Bước 4: Tạo Video Playbook

Dựa trên phân tích, đề xuất:

### Template cho từng product type:
```
T-shirt/Hoodie:
- Format: UGC (người mặc + reaction)
- Duration: 15-20s
- Hook: "Wait until you see what my [person] got me"
- CTA: "Link in bio" / "Shop now"

Mug:
- Format: Morning routine + mug reveal
- Duration: 10-15s
- Hook: Visual hook (coffee pour → reveal design)
```

### Influencer Strategy:
- Budget recommendation based on product price
- Outreach template
- Content brief gợi ý

## Bước 5: Output

Tạo artifact:

1. **Video Performance Matrix**: Bảng với Views vs Sales (2 cột metric riêng biệt)
2. **Pattern Analysis**: Tổng hợp format, hook, duration nào hiệu quả nhất
3. **🏆 Best-in-Class Videos**: Top 5 videos đáng study nhất + lý do
4. **Video Playbook**: Template cụ thể cho niche của user
5. **Influencer Recommendations**: Tier + budget + strategy

## Lưu ý

- Phân biệt rõ **views ≠ sales** — video triệu views có thể 0 sales
- `engagement_rate` > 10% thường là signal tốt
- `likes_per_views` cao = content hay, nhưng cần check sales riêng
- Video có `is_promote: true` = paid ads, pattern khác organic
- Ghi rõ link video (`video_url`) để user có thể study trực tiếp
