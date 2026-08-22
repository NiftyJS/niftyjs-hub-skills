---
name: pod-design-scaling
description: >-
  Kích hoạt khi người dùng muốn scale design đang có, phân tích niche/sub-niche, hoặc tìm hướng mở rộng sản phẩm.
  Trigger khi user nhắc: 'scale design', 'mở rộng', 'sub-niche', 'niche liên quan',
  'expand', 'variations', 'phát triển thêm', 'design này bán gì thêm', 'horizontal', 'vertical scaling'.
  Cũng trigger khi user cung cấp hình ảnh mockup/design và hỏi về tiềm năng mở rộng.
---

# POD Design Scaling — Workflow scale design hiện tại

Khi user có design đang bán (hoặc ý tưởng design) và muốn scale, thực hiện workflow sau.

## Bước 1: Xác định niche hiện tại

### Nếu user cung cấp hình ảnh:
- Phân tích design: chủ đề, phong cách, typography, target audience
- Xác định **primary niche** (ví dụ: "dog mom")

### Nếu user mô tả bằng text:
- Xác định niche từ mô tả
- Hỏi thêm nếu chưa rõ: loại sản phẩm, target market, phong cách design

## Bước 2: Map niche hierarchy

Xây dựng bản đồ niche:

```
Primary Niche: Dog Mom
├── Sub-niches (Vertical):
│   ├── Breed-specific: Golden Retriever Mom, Poodle Mom, Bulldog Mom
│   ├── Activity-specific: Dog Walking Mom, Dog Park Mom
│   └── Identity-specific: Rescue Dog Mom, Fur Baby Mom
├── Adjacent niches (Horizontal):
│   ├── Cat Mom, Plant Mom, Wine Mom
│   ├── Dog Dad, Dog Grandma, Dog Parents
│   └── Pet Lover, Animal Rescue
└── Occasion-based:
    ├── Mother's Day, Birthday, Christmas
    └── Gotcha Day, National Dog Day
```

## Bước 3: Validate với data thực

Gọi MCP tools để kiểm tra tiềm năng mỗi hướng scale:

### Cho primary niche + sub-niches:
- `etsy_keywords_research` — check revenue, competition, opportunity cho mỗi keyword
- `etsy_hot_listings` — xem sản phẩm hot trong niche

### Cho adjacent niches:
- `etsy_trending_keywords` — xem niche nào đang trending
- `tiktok_browse_listings` — so sánh volume bán hàng

## Bước 4: Đánh giá hướng scale

### Horizontal Scaling (mở rộng niche):
Đánh giá mỗi adjacent niche:

| Tiêu chí | Scoring |
|----------|---------|
| Revenue tương đương hoặc cao hơn primary | +3 |
| Competition thấp hơn primary | +2 |
| Design có thể adapt dễ (đổi text/icon) | +2 |
| Có momentum/trending | +1 |
| Audience overlap với primary | +1 |

→ Score >= 7: 🟢 Nên expand
→ Score 4-6: 🟡 Test thử
→ Score < 4: 🔴 Skip

### Vertical Scaling (đi sâu sub-niche):
Đánh giá mỗi sub-niche:
- Có đủ search volume không? (listings count > 100)
- Passion level: breed-specific fans CỰC KỲ passionate → willing to pay more
- Design effort: Chỉ cần đổi tên giống → effort thấp, ROI cao

### Product Type Expansion:
Kiểm tra primary niche bán trên product types nào:
- T-shirt ✅ → Hoodie, Sweatshirt (upsell)
- Mug ✅ → Tumbler, Wine Glass (adjacent)
- Tote Bag ✅ → Pillow, Blanket (home decor)
- Sticker ✅ → Phone Case, Laptop Sleeve (accessories)

## Bước 5: Output

Tạo artifact với:

1. **Niche Map**: Sơ đồ visual (mermaid diagram) của niche hierarchy
2. **Scaling Scorecard**: Bảng đánh giá mỗi hướng scale với scores
3. **Top 5 Scale Opportunities**: Hướng scale tốt nhất + lý do + estimated effort
4. **Design Adaptation Guide**: Cần thay đổi gì từ design gốc cho mỗi hướng
5. **Revenue Projection**: So sánh revenue tiềm năng mỗi hướng (dựa trên data)

## Lưu ý

- **Breed-specific** là goldmine cho POD — fans rất passionate, sẵn sàng trả premium
- **Horizontal scaling** ưu tiên niches có audience overlap (dog mom → cat mom là natural)
- **Seasonal occasions** cần timeline rõ ràng (bắt đầu list sản phẩm Christmas từ tháng 9)
- Mỗi hướng scale, ước tính **design effort** (low/medium/high) để user biết ROI
- Nếu có thể, dùng `generate_image` tool để tạo mockup minh họa cho ý tưởng scale
