---
name: pod-trend-discovery
description: Trigger khi muốn phát hiện xu hướng mới hoặc niche POD trend.
---

# POD Trend Discovery — Workflow phát hiện trends đang lên

**Triggers:** Kích hoạt khi người dùng muốn phát hiện trends, tìm xu hướng mới, hoặc khám phá niche tiềm năng. Từ khóa: 'trend', 'xu hướng', 'niche mới', 'keyword trending', 'thị trường đang hot', 'opportunity', 'cơ hội', 'niche nào đang lên', 'tìm ý tưởng mới'.

Khi user muốn phát hiện trends mới hoặc tìm cơ hội, thực hiện workflow sau.

## Bước 1: Scan trending keywords

Gọi `etsy_trending_keywords`:
- `sort`: `momentum` (ưu tiên keywords đang tăng tốc)
- `limit`: 50
- Nếu user cho seed keyword → truyền vào `search`

Kết quả: Danh sách keywords với momentum score, volume, growth.

## Bước 2: Deep-dive top keywords

Chọn top 10 keywords có momentum cao nhất, gọi `etsy_keywords_research` cho từng keyword:
- `sort`: `opportunity` hoặc `revenue`
- Lấy: competition score, avg price, sellers count, revenue

Phân tích mỗi keyword:
- **Opportunity Score**: Competition thấp + Revenue cao = 🏆 Golden
- **Risk Level**: Competition cao + Revenue thấp = ⚠️ Risky

## Bước 3: Cross-validate trên TikTok

Gọi `tiktok_browse_videos` với top keywords:
- Kiểm tra có viral video liên quan không
- Nếu có video > 100K views + sales > 0 = **trend confirmed cross-platform**

Gọi `tiktok_browse_listings` nếu keyword phù hợp:
- So sánh volume bán hàng TikTok vs Etsy

## Bước 4: Phân loại trend

Với mỗi trend phát hiện, xác định:

### Trend Stage:
- 🌱 **Emerging** (1-2 tuần): Momentum cao, sellers ít, chưa nhiều sản phẩm → **CỬA SỔ VÀNG**
- 🔥 **Hot** (2-6 tuần): Nhiều sellers vào, demand cao, vẫn còn room → Vào nhanh
- 📈 **Peak** (6-12 tuần): Saturated nhưng demand vẫn có → Cần differentiate mạnh
- 📉 **Declining**: Momentum giảm, sellers > demand → Skip

### Trend Type:
- 🎄 **Seasonal**: Gắn với mùa/holiday → Ghi nhận timeline
- ♾️ **Evergreen**: Luôn có demand → Đầu tư dài hạn
- ⚡ **Viral**: Bùng nổ từ TikTok/meme → Nhanh tay hoặc bỏ

### Cross-Platform Signal:
- 🟢 Hot trên cả Etsy + TikTok = Strong
- 🟡 Hot trên 1 platform = Moderate (có thể là arbitrage opportunity)
- 🔴 Chỉ trending keywords, chưa có sản phẩm = Early/Risky

## Bước 5: Đề xuất ý tưởng thiết kế

Với mỗi trend đáng chú ý, đề xuất:
- **3-5 design concepts**: Mô tả ngắn gọn ý tưởng design
- **Target audience**: Ai sẽ mua (demographics, interests)
- **Suggested products**: T-shirt, hoodie, mug, tote...
- **Pricing strategy**: Dựa trên `niche_avg_price`
- **Keywords/tags**: Top 5-10 tags cho listing

## Bước 6: Output

Tạo artifact theo format `pod-report-format`:

1. **Trend Radar**: Bảng tổng hợp tất cả trends phát hiện với Stage + Type + Signal
2. **Top 3 Golden Opportunities**: Trends có tiềm năng nhất + lý do
3. **Design Ideas Board**: Ý tưởng design cho mỗi trend
4. **Action Timeline**: Trend nào cần hành động ngay, trend nào theo dõi

## Lưu ý

- Agent phải đưa ra OPINION — không chỉ list data
- Ưu tiên trends **Emerging** vì đó là lúc margin cao nhất
- Nếu phát hiện trend seasonal, ghi rõ timeline (ví dụ: "Halloween trends bắt đầu từ tháng 9")
- Cross-reference nhiều tools để validate — 1 tool = signal, 2+ tools = confirmation
