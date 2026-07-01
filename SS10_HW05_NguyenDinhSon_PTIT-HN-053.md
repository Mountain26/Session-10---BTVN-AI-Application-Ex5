## Bài 5. Khởi Tạo Workflow SRS Hoàn Chỉnh

### Thiết kế luồng

- Input:
  - Người dùng đang xem một sản phẩm.
  - Lịch sử mua hàng của người dùng.
  - Danh mục sản phẩm và dữ liệu sản phẩm liên quan.
- Output:
  - Danh sách sản phẩm được gợi ý.
  - Mỗi gợi ý gồm productId, tên sản phẩm, điểm liên quan và lý do gợi ý.

### Luồng logic

1. Người dùng mở trang chi tiết một sản phẩm.
2. Hệ thống lấy product hiện tại.
3. Hệ thống đọc lịch sử mua hàng của người dùng.
4. Hệ thống so khớp sản phẩm đang xem với lịch sử mua để tìm mẫu liên quan.
5. Hệ thống lọc ra các sản phẩm cùng nhóm, cùng ngữ cảnh hoặc có quan hệ bổ trợ.
6. Hệ thống loại bỏ sản phẩm đã mua, đã hiển thị hoặc không còn khả dụng.
7. Hệ thống xếp hạng các gợi ý theo mức liên quan.
8. Hệ thống trả về danh sách gợi ý cho giao diện.

### Sơ đồ ASCII

```text
User views product
        |
        v
Get current product + purchase history
        |
        v
Match patterns and related items
        |
        v
Filter unavailable / duplicated items
        |
        v
Rank recommendations
        |
        v
Return top suggested products
```

### Workflow Prompt

```text
Bạn là System Analyst. Hãy chuyển yêu cầu thô sau thành tài liệu SRS cho module AI Product Recommendation của Shop AI:

Yêu cầu thô:
Khi người dùng đang xem một sản phẩm, hệ thống tự động gợi ý các sản phẩm liên quan dựa trên lịch sử mua hàng của họ.

Nhiệm vụ:
1. Viết Use Case Description đầy đủ.
2. Viết Functional Requirements.
3. Viết Data Dictionary sơ bộ cho các thực thể dữ liệu chính.

Ràng buộc:
- Phải xác định rõ actor, trigger, precondition, main flow, alternative flow và postcondition.
- Phải nêu cách hệ thống lấy dữ liệu lịch sử mua hàng và cách dùng dữ liệu đó để tạo gợi ý.
- Phải nêu quy tắc lọc sản phẩm đã mua, sản phẩm không còn hàng, và sản phẩm không còn active.
- Phải đề xuất logic xếp hạng gợi ý ở mức nghiệp vụ, không đi quá sâu sang code.
- Phải có dữ liệu đầu vào, đầu ra và các field cốt lõi.
- Tránh câu chữ mơ hồ.

Định dạng đầu ra:
- Trả về bằng tiếng Việt.
- Trình bày theo 3 phần:
  1. Use Case Description
  2. Functional Requirements
  3. Data Dictionary
Hãy viết tài liệu hoàn chỉnh và có thể đưa vào SRS.
```

### Minh chứng chạy thực tế

```text
Người dùng: Tôi muốn hệ thống tự động gợi ý các sản phẩm liên quan khi người dùng đang xem một món đồ, dựa trên lịch sử mua hàng của họ.

AI: Tôi sẽ chuyển yêu cầu này thành tài liệu SRS cho module AI Product Recommendation.

AI: Use Case Description
- Tên use case: Gợi ý sản phẩm thông minh
- Actor chính: Người dùng
- Trigger: Người dùng mở trang chi tiết sản phẩm
- Tiền điều kiện: Người dùng đã đăng nhập và hệ thống có lịch sử mua hàng
- Luồng chính:
  1. Người dùng xem một sản phẩm.
  2. Hệ thống lấy thông tin sản phẩm hiện tại.
  3. Hệ thống lấy lịch sử mua hàng của người dùng.
  4. Hệ thống phân tích các sản phẩm đã mua để tìm quan hệ liên quan.
  5. Hệ thống lọc các sản phẩm không phù hợp.
  6. Hệ thống xếp hạng và trả danh sách gợi ý.
- Luồng thay thế:
  - Nếu không có lịch sử mua hàng, hệ thống dùng dữ liệu sản phẩm đang xem và danh mục tương tự.
  - Nếu không đủ dữ liệu, hệ thống trả danh sách gợi ý mặc định theo độ phổ biến.

AI: Functional Requirements
- Hệ thống phải sinh danh sách gợi ý khi người dùng mở trang chi tiết sản phẩm.
- Hệ thống phải sử dụng lịch sử mua hàng để tăng độ liên quan của gợi ý.
- Hệ thống phải loại bỏ sản phẩm đã mua, hết hàng hoặc không active.
- Hệ thống phải trả tối đa N sản phẩm theo cấu hình.
- Hệ thống phải lưu nhận xét hoặc tín hiệu chọn gợi ý để cải thiện xếp hạng.

AI: Data Dictionary
- user_id: định danh người dùng
- product_id: định danh sản phẩm đang xem
- purchase_history: lịch sử mua hàng của người dùng
- recommendation_score: điểm xếp hạng gợi ý
- recommendation_reason: lý do gợi ý

Người dùng: Kết quả này dùng được, tôi sẽ bổ sung vào SRS.
```
