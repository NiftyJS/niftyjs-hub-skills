---
name: pod-report-format
description: Trigger khi yêu cầu format báo cáo nghiên cứu sản phẩm POD. BẮT BUỘC dùng MCP tools, KHÔNG dùng search_web.
---

> [!IMPORTANT]
> **BẮT BUỘC SỬ DỤNG MCP TOOLS:**
> Agent KHÔNG ĐƯỢC sử dụng các công cụ tìm kiếm web thông thường (`search_web`, `read_url_content`) cho skill này. Hãy dùng `call_mcp_tool` để gọi các API chuyên dụng từ MCP Servers (như `niftyjs-hub`, `tiktok`, `etsy`, `pinterest`).

# POD Market Research — Hướng dẫn format output

**Triggers:** Kích hoạt khi người dùng yêu cầu tìm kiếm, nghiên cứu, phân tích sản phẩm POD trên Etsy hoặc TikTok. Bao gồm tìm sản phẩm hot, keywords, listings, videos. Từ khóa: 'tìm sản phẩm', 'research niche', 'trending', 'hot listings', 'browse products', 'tìm video', 'phân tích thị trường', hoặc các niche cụ thể.

Khi sử dụng các MCP tools từ `niftyjs-hub` server, **luôn trình bày kết quả** theo format chuẩn dưới đây.

## Quy tắc chung

1. **Luôn tạo artifact** (file `.md`) để trình bày kết quả — KHÔNG dump JSON thô ra chat
2. **Sử dụng bảng markdown** để hiển thị danh sách sản phẩm/keywords
3. **Embed hình ảnh** sản phẩm bằng `![](url)` nếu có `cover_url`
4. **Sắp xếp** theo metric chính (sales, views, revenue) từ cao xuống thấp
5. **Tóm tắt insights** ở đầu artifact trước khi hiển thị bảng chi tiết
6. **Ghi rõ nguồn** (Etsy/TikTok) và thời điểm search
7. **Link tên sản phẩm** về trang gốc theo quy tắc:
   - **Etsy**: `[product title](https://www.etsy.com/listing/{listing_id})`
   - **TikTok product**: `[product name](https://shop.tiktok.com/us/pdp/{product_name_slug}/{product_id})`
   - **TikTok video**: `[video title](video_url)` — field `video_url` có sẵn trong response
8. **Ghi rõ platform** khi kết quả mix nhiều nền tảng: thêm cột `Platform` (🟠 Etsy / 🎵 TikTok) vào bảng để phân biệt nguồn

---

## Format cho Etsy Products (hot-listings, browse-listings)

### Artifact structure:

```markdown
# 🔥 Etsy [Hot/Browse] Listings — "[keyword]"

> **Tổng**: X sản phẩm | **Sắp xếp**: [sort] | **Thời gian**: YYYY-MM-DD HH:mm

## 📊 Quick Insights
- Top seller: [seller_name] với [X] sales
- Giá trung bình: $XX.XX
- Niche phổ biến nhất: [observation]

## 📋 Danh sách sản phẩm

| # | Hình | Tên sản phẩm | Ngày tạo | Sales 24h | Views 24h | Favorites | Shop |
|---|------|-------------|----------|-----------|-----------|-----------|------|
| 1 | ![](image_url) | [title](https://www.etsy.com/listing/{listing_id}) | X ngày | XX | XX | XX | shop_name |
```

---

## Format cho Etsy Keywords (trending-keywords, keywords-research)

```markdown
# 🔑 Etsy [Trending/Research] Keywords — "[seed keyword]"

> **Tổng**: X keywords | **Sắp xếp**: [sort]

## 📊 Quick Insights
- Keyword tiềm năng nhất: [tag] (opportunity score cao, competition thấp)
- Niche có revenue cao nhất: [tag]

## 📋 Danh sách Keywords

| # | Keyword | Listings | Sellers | Avg Price | Sales/Day | Revenue | Competition | Action |
|---|---------|----------|---------|-----------|-----------|---------|-------------|--------|
| 1 | tag | XX | XX | $XX | XX | $XX | low/medium/high | ✅/⚠️/❌ |
```

### Recommended Action mapping:
- ✅ = "enter" hoặc "scale" — nên tham gia
- ⚠️ = "monitor" hoặc "test" — cần theo dõi
- ❌ = "avoid" — quá cạnh tranh

---

## Format cho TikTok Products (browse-listings)

```markdown
# 🛒 TikTok Shop Listings — "[keyword]"

> **Categories**: [list] | **Tổng**: X sản phẩm/category

## 📊 Quick Insights
- Sản phẩm bán chạy nhất: [product_name]
- Category hot nhất: [category]

## 📋 [Category Name]

| # | Hình | Tên sản phẩm | Giá | Sales Today | Sales 30D | Total Sales | GMV | Rating | Videos |
|---|------|-------------|-----|-------------|-----------|-------------|-----|--------|--------|
| 1 | ![](cover_url) | [name](https://shop.tiktok.com/us/pdp/{product_name_slug}/{product_id}) | $XX | XX | XX | XX | $XX | ⭐X.X | XX |
```

Lặp lại bảng cho mỗi category.

---

## Format cho TikTok Videos (browse-videos)

```markdown
# 🎬 TikTok Videos — "[keyword]"

> **Categories**: 601152, 824328 | **Thời gian**: start_time → end_time

## 📊 Quick Insights
- Video viral nhất: [title] — XX views, XX% engagement
- Influencer nổi bật: [name] (XX followers)

## 📋 Top Videos

| # | Thumbnail | Tiêu đề | Views | Likes | Engagement | Sales | GMV | Influencer | Link |
|---|-----------|---------|-------|-------|------------|-------|-----|------------|------|
| 1 | ![](cover_url) | [title](video_url) | XXM | XXK | XX% | XX | $XX | @name (XXK followers) | [🔗](video_url) |
```

---

## Quy tắc bổ sung

- **Số lớn**: Format dạng human-readable (1.2K, 3.5M) — giữ nguyên format từ API
- **Giá**: Luôn hiển thị ký hiệu $ 
- **Hình ảnh**: Chỉ embed khi user yêu cầu xem chi tiết hoặc khi số lượng ≤ 20. Nếu > 20 sản phẩm, bỏ cột hình
- **Carousel**: Dùng carousel khi so sánh nhiều categories hoặc nhiều niches
- **Khi user hỏi tiếp**: Nếu user muốn đi sâu vào 1 sản phẩm cụ thể, hiển thị full detail bao gồm seller info, tất cả metrics
