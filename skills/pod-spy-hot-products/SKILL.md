---
name: pod-spy-hot-products
description: Trigger khi muốn spy tìm sản phẩm POD bán chạy để clone. BẮT BUỘC dùng MCP tools, KHÔNG dùng search_web.
---

> [!IMPORTANT]
> **BẮT BUỘC SỬ DỤNG MCP TOOLS:**
> Agent KHÔNG ĐƯỢC sử dụng các công cụ tìm kiếm web thông thường (`search_web`, `read_url_content`) cho skill này. Hãy dùng `call_mcp_tool` để gọi các API chuyên dụng từ MCP Servers (như `niftyjs-hub`, `tiktok`, `etsy`, `pinterest`).

# POD Spy Hot Products — Workflow tìm sản phẩm HOT để clone

**Triggers:** Kích hoạt khi người dùng muốn spy, tìm sản phẩm HOT đang bán chạy để clone hoặc lấy ý tưởng. Từ khóa: 'spy sản phẩm', 'tìm sản phẩm hot', 'clone', 'sản phẩm bán chạy', 'top sellers', 'winning products', 'best sellers', 'sản phẩm nào đang hot'.

Khi user muốn spy sản phẩm hot, thực hiện workflow sau đây **đầy đủ các bước**.

## Bước 1: Thu thập data từ cả 2 nền tảng

Gọi **song song** các MCP tools:

- `etsy_hot_listings` — lấy sản phẩm hot trên Etsy (sort: `sold`, limit: 50)
- `tiktok_browse_listings` — lấy sản phẩm hot trên TikTok (order: `total_sale_nd_cnt`, per_page: 20)

Nếu user cung cấp keyword (ví dụ: "dog mom"), truyền vào param `search` / `keyword`.
Nếu không có keyword, vẫn chạy để lấy trending chung.

## Bước 2: Filter sản phẩm clone-worthy

Áp dụng tiêu chí filter:

### Etsy:
- `listing_age_days` < 30 (sản phẩm mới nhưng đã có traction = design mới, chưa saturated)
- `hot_reason` chứa "sales" hoặc "views" (momentum thực, không phải cũ)
- Ưu tiên sản phẩm có `conversion_rate` cao hơn `niche_avg_conversion`

### TikTok:
- `total_sale_nd_cnt` > 0 (có sales gần đây)
- `videos_count` > 0 (có video marketing = có thể spy video strategy)
- Ưu tiên sản phẩm có `product_rating` >= 4.0

## Bước 3: Phân tích từng sản phẩm tiềm năng

Với mỗi sản phẩm đáng chú ý, đánh giá:

### Clone Difficulty:
- 🟢 **Dễ clone**: Text-based design, simple graphics, typography
- 🟡 **Trung bình**: Custom illustration đơn giản, pattern
- 🔴 **Khó clone**: Artwork phức tạp, photography, brand-specific

### Market Saturation:
- Dựa vào số sellers cùng niche (`etsy_keywords_research` nếu cần)
- < 500 sellers = 🟢 Low competition
- 500-2000 = 🟡 Medium
- > 2000 = 🔴 High

### Recommended Action:
- ✅ **Clone & Improve**: Sản phẩm hot + low competition + dễ clone
- 🔄 **Twist ý tưởng**: Hot nhưng competition cao → cần góc nhìn khác
- ⏭️ **Skip**: Quá saturated hoặc brand-specific

## Bước 4: Đề xuất cải tiến

Với mỗi sản phẩm recommend clone, đưa ra:
- 2-3 **twist ideas** để differentiate (thay đổi style, thêm humor, target sub-niche khác)
- **Product types** nên bán (t-shirt, hoodie, mug, poster...)
- **Keywords/tags** gợi ý cho listing
- **Giá tham khảo** dựa trên `niche_avg_price` hoặc `avg_price`

## Bước 5: Output

Tạo artifact theo format của skill `pod-report-format`. Bao gồm:

1. **Executive Summary**: Tổng quan thị trường, số sản phẩm phân tích, top 3 highlights
2. **Bảng sản phẩm HOT** (theo format chuẩn, có cột Platform nếu mix data)
3. **Clone Recommendations**: Bảng chi tiết với Clone Difficulty + Action + Twist Ideas
4. **Quick Wins**: Top 3 sản phẩm nên clone ngay (dễ nhất + tiềm năng nhất)

## Lưu ý

- Luôn gọi cả Etsy và TikTok để có cái nhìn cross-platform
- Nếu 1 sản phẩm hot trên CẢ 2 platform = **strong signal**, highlight đặc biệt
- Đừng chỉ list data — agent phải **phân tích và đưa ra opinion** như một POD researcher
- Khi không chắc về clone difficulty, dựa vào hình ảnh sản phẩm (`image_url`, `cover_url`) để đánh giá
