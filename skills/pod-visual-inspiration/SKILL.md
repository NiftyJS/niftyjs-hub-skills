---
name: pod-visual-inspiration
description: Trigger khi cần tìm ý tưởng visual và quotes thiết kế POD.
---

# POD Visual Inspiration — Tìm cảm hứng & Visual Trends từ Pinterest

**Triggers:** Kích hoạt khi người dùng muốn tìm ý tưởng thiết kế (visual), trích xuất quotes/text cho áo, phân tích color palette, hoặc tìm các niche visual đang hot (aesthetic). Từ khóa: 'tìm ý tưởng thiết kế', 'visual trend', 'pinterest', 'aesthetic', 'tìm quotes', 'cảm hứng thiết kế', 'color palette'.

Khi user cần ý tưởng thiết kế, phong cách visual, hoặc quotes text, hãy dùng quy trình sau với Pinterest MCP tools.

## Bước 1: Khám phá Trend (Nếu user chưa có niche cụ thể)

Nếu user hỏi chung chung (ví dụ: "có trend visual nào đang lên?"):
- Gọi `getGrowingTrends` (Pinterest MCP) để tìm các từ khóa có tốc độ tăng trưởng cao nhất.
- Lọc ra các từ khóa liên quan đến lifestyle, fashion, decor (ví dụ: "coquette", "mob wife aesthetic", "dopamine dressing").
- Chọn 1-2 trends phù hợp nhất với POD và chuyển sang Bước 2.

## Bước 2: Đào sâu Keywords & Niche Ideas (Nếu user đã có niche)

Nếu user đã cho niche (ví dụ: "dog mom" hoặc niche vừa tìm được ở Bước 1):
- Gọi `generateKeywords` với tham số `term="<niche>"`, BẮT BUỘC set `recursive=true` để đào sâu ra các ngách.
- Lọc các long-tail keywords mang tính thị giác hoặc dễ in ấn (ví dụ: "funny dog mom quotes aesthetic", "minimalist dog mom tattoo").

## Bước 3: Thu thập Hình Ảnh Thực Tế & Fresh Content

- Dùng `searchPinsRecent` (hoặc `searchPins` nếu không cần mới nhất) với top keywords từ Bước 2.
- Gọi khoảng 25 pins để lấy mẫu đại diện.

## Bước 4: Phân tích & Trích Xuất Ý Tưởng

Dựa trên dữ liệu các Pins trả về (Description, Tags, Title), Agent phải đóng vai trò là Giám đốc Nghệ thuật (Art Director) để tổng hợp:

### 1. Style & Aesthetic (Phong cách)
- Trào lưu thiết kế chung là gì? (Minimalist, Y2K, Retro 70s wavy text, Vintage illustration, Groovy, v.v.)
- Bố cục thường gặp (chữ to tràn viền, icon nhỏ ngực trái, typography kết hợp doodle).

### 2. Color Palette (Bảng màu)
- Gam màu chủ đạo đang được Repin nhiều nhất (Ví dụ: "Pastel pink + Sage green", "Earthy tones", "Neon on Black").

### 3. Quotes & Text Ideas (ĐỂ LÀM TYPOGRAPHY T-SHIRTS)
- Trích xuất 5-10 câu quotes, slogans, hoặc funny texts thường xuất hiện trong niche này. ĐÂY LÀ PHẦN QUAN TRỌNG NHẤT VÌ POD CHỦ YẾU BÁN TEXT-BASED DESIGNS.

## Bước 5: Output

Tạo artifact với định dạng rõ ràng:

1. **Visual Trend Summary**: Tóm tắt phong cách đang thống trị niche này.
2. **Top Quotes & Text Ideas**: Bảng danh sách các câu quote/text dễ bán nhất, kèm theo (Funny, Sarcastic, hay Sweet).
3. **Design Briefs (Đề bài cho Designer)**: 3 ý tưởng cụ thể có thể gửi ngay cho designer.
    - Ý tưởng 1: Mô tả chi tiết (Text + Hình họa + Bảng màu).
    - Ý tưởng 2...
    - Ý tưởng 3...
4. **Scale Opportunity**: Niche visual này có thể scale sang các sản phẩm nào (Stickers, Tote bags, Tumblers...).

## Lưu ý
- Phải dùng `recursive=true` ở `generateKeywords` để ra được text quotes dài.
- Agent KHÔNG hiển thị lại hàng đống JSON vô nghĩa, phải tiêu hóa data và trả ra **Design Brief** thực tiễn.
