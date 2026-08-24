---
name: pod-product-scoring
description: Tiêu chí chấm điểm để xác định sản phẩm/niche POD đang hot. BẮT BUỘC dùng MCP tools, KHÔNG dùng search_web.
---

> [!IMPORTANT]
> **BẮT BUỘC SỬ DỤNG MCP TOOLS:**
> Agent KHÔNG ĐƯỢC sử dụng các công cụ tìm kiếm web thông thường (`search_web`, `read_url_content`) cho skill này. Hãy dùng `call_mcp_tool` để gọi các API chuyên dụng từ MCP Servers (như `niftyjs-hub`, `tiktok`, `etsy`, `pinterest`).

# POD Product Scoring — Tiêu chí xác định sản phẩm/niche "đang hot"

**Nguyên tắc cốt lõi:** "Đang hot" = **Demand đang vượt Supply**. Velocity (tốc độ tăng) quan trọng hơn tổng tích lũy. Một listing 3 năm có 1000 favorites KHÔNG phải hot — nhưng listing 2 tuần tuổi có 200 favorites THÌ hot.

---

## Định nghĩa chuẩn

> **Sản phẩm/niche đang hot** = Có **velocity tăng cao trong 2–4 tuần gần nhất**, có **tín hiệu từ ít nhất 2 nguồn độc lập**, và **số sellers chưa bắt kịp demand** (competition còn low–medium).

---

## Scoring Rubric (Thang điểm 0–10)

Agent chấm điểm mỗi sản phẩm/niche theo các tiêu chí dưới đây. Cộng tổng điểm để ra mức độ.

### A. Tín hiệu Etsy (tối đa 4 điểm)

| Tiêu chí | Điểm | Ngưỡng |
|---|---|---|
| **Listing age** | +2 | `listing_age_days` < 30 ngày (mới mà đã có traction) |
| **Hot reason** | +1 | `hot_reason` chứa "sales" hoặc "views" |
| **Conversion rate** | +1 | `conversion_rate` > `niche_avg_conversion` |

> ⚠️ Nếu `listing_age_days` > 90 ngày, bỏ qua toàn bộ điểm Etsy — đây là tích lũy cũ, không phải momentum mới.

### B. Tín hiệu TikTok (tối đa 4 điểm)

| Tiêu chí | Điểm | Ngưỡng |
|---|---|---|
| **Sales velocity** | +2 | `total_sale_nd_cnt` > 0 VÀ tăng so với tuần trước |
| **Video coverage** | +1 | `videos_count` > 5 (nhiều người làm content = word of mouth) |
| **Rating + reviews** | +1 | `product_rating` ≥ 4.0 VÀ đủ reviews để trust |

### C. Cross-Platform Signal (tối đa 2 điểm)

| Tiêu chí | Điểm | Điều kiện |
|---|---|---|
| **Xác nhận chéo** | +1 | Keyword hot trên Etsy VÀ có sản phẩm đang bán trên TikTok |
| **Arbitrage window** | +1 | Hot trên TikTok nhưng < 200 sellers trên Etsy (hoặc ngược lại) |

---

## Phân loại kết quả

| Tổng điểm | Nhãn | Hành động |
|---|---|---|
| **8–10** | 🔥 **HOT** — Vào ngay | Clone & launch trong 48h |
| **5–7** | 🌱 **Emerging** — Theo dõi | Chuẩn bị design, launch trong 1–2 tuần |
| **3–4** | 🟡 **Moderate** — Chờ thêm | Validate thêm 1 tuần trước khi đầu tư |
| **0–2** | ❌ **Skip** | Không đủ tín hiệu, bỏ qua |

---

## Tín hiệu định tính (Bonus — không tính điểm nhưng quan trọng)

Nếu thấy các dấu hiệu dưới đây, **nâng bậc lên 1 cấp** (ví dụ Emerging → HOT):

- 📹 Comments trên TikTok hỏi **"mua ở đâu?"** hoặc **"link?"**
- 🔁 Nhiều sellers **clone cùng một design** (tự chứng minh demand)
- 📰 Keyword xuất hiện ở nhiều video **khác nhau** (không phải 1 viral fluke)
- 🗓️ Sản phẩm gắn với **event/holiday sắp tới** trong 4–8 tuần

---

## Bẫy thường gặp — TRÁNH

| ❌ Sai | ✅ Đúng |
|---|---|
| "1000 favorites = hot" | Hỏi: bao nhiêu favorites trong **7–14 ngày gần nhất**? |
| Chỉ nhìn 1 platform | Luôn cross-validate Etsy + TikTok |
| Tin vào tổng sales tích lũy | Nhìn vào **sales gần đây** (`total_sale_nd_cnt`) |
| Competition cao = skip | Competition cao + demand tăng = **cần differentiate**, không phải skip |

---

## Cách dùng skill này

Các skills khác nên tham chiếu skill này khi cần ra quyết định về mức độ "hot":

- **`pod-spy-hot-products`** → Dùng khi filter sản phẩm clone-worthy
- **`pod-trend-discovery`** → Dùng khi phân loại Trend Stage
- **`pod-cross-platform-arbitrage`** → Dùng khi đánh giá strength của arbitrage signal
- **`pod-report-format`** → Dùng điểm số này trong cột **Score** của bảng sản phẩm
