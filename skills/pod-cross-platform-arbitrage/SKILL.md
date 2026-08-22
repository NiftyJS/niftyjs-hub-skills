---
name: pod-cross-platform-arbitrage
description: >-
  Kích hoạt khi người dùng muốn tìm cơ hội arbitrage giữa Etsy và TikTok Shop,
  hoặc so sánh sản phẩm/niche giữa 2 nền tảng.
  Trigger khi user nhắc: 'arbitrage', 'cross-platform', 'so sánh Etsy TikTok',
  'hot trên TikTok chưa có trên Etsy', 'chênh lệch', 'cơ hội giữa 2 nền tảng'.
---

# POD Cross-Platform Arbitrage — Tìm cơ hội chênh lệch giữa Etsy & TikTok

Sản phẩm viral trên TikTok thường mất 2-4 tuần để saturate trên Etsy (và ngược lại).
Skill này giúp phát hiện cửa sổ vàng đó.

## Bước 1: Thu thập top sellers cả 2 platform

Gọi song song:
- `tiktok_browse_listings` — order: `total_sale_nd_cnt`, per_page: 30
- `etsy_hot_listings` — sort: `sold`, limit: 30

Nếu user cho keyword → truyền vào cả 2.

## Bước 2: Cross-reference

### TikTok → Etsy (phổ biến nhất):
Với mỗi sản phẩm hot trên TikTok:
1. Lấy keywords từ tên sản phẩm
2. Gọi `etsy_keywords_research` với keywords đó
3. Kiểm tra:
   - **Sellers count** trên Etsy cho keyword đó
   - **Competition level**
   - **Revenue** trên Etsy

### Etsy → TikTok:
Với mỗi sản phẩm hot trên Etsy:
1. Gọi `tiktok_browse_videos` với keyword tương ứng
2. Kiểm tra:
   - Có ai đang bán trên TikTok chưa?
   - Có video marketing không?
   - Volume sales trên TikTok

## Bước 3: Đánh giá cơ hội arbitrage

Với mỗi cặp so sánh, tính **Arbitrage Score**:

| Signal | Điểm |
|--------|------|
| Hot trên Platform A (top 20% sales) | +3 |
| Ít sellers trên Platform B (< 200) | +3 |
| Competition score thấp trên Platform B | +2 |
| Có proven demand (reviews, ratings) | +1 |
| Design dễ adapt cross-platform | +1 |

→ Score >= 8: 🏆 **Golden Arbitrage** — Vào ngay!
→ Score 5-7: 🟢 **Good Opportunity** — Nên thử
→ Score 3-4: 🟡 **Monitor** — Theo dõi thêm
→ Score < 3: ⏭️ **Skip**

## Bước 4: Chiến lược entry

Với mỗi cơ hội arbitrage, đề xuất:
- **Platform target**: Nên list ở đâu
- **Pricing**: So sánh giá 2 platform → đề xuất giá tối ưu
- **Timing**: Ước tính bao lâu trước khi saturated
- **Marketing**: TikTok cần video, Etsy cần SEO/tags
- **Product adaptation**: Cần thay đổi gì (title, tags, image style)

## Bước 5: Output

Tạo artifact:

1. **Arbitrage Radar**: Bảng tổng hợp cơ hội với scores, sắp xếp theo Arbitrage Score
2. **Platform Comparison**: So sánh metrics (sales, price, competition) cùng keyword giữa 2 platform
3. **Top 3 Arbitrage Plays**: Chi tiết + action plan cho mỗi cơ hội
4. **Timing Map**: Ước tính cửa sổ cơ hội (tuần/tháng)

## Lưu ý

- **TikTok → Etsy** thường là hướng chính: viral video tạo demand, Etsy chưa kịp đáp ứng
- **Etsy → TikTok** hiếm hơn nhưng có: niche evergreen trên Etsy nhưng chưa ai làm video
- Cửa sổ arbitrage thường ngắn (2-4 tuần) — phải action nhanh
- Ghi rõ **risk**: nếu trend chỉ viral 1 tuần thì không đáng đầu tư
