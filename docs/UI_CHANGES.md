# Đồng bộ PnL Replayer với Chart Replayer

## Giao diện

- Dùng cùng palette, font, spacing, control, bo góc và theme sáng/tối của Chart Replayer.
- Màn hình bắt đầu tập trung vào tra cứu Token hoặc Wallet.
- Workspace gồm thanh công cụ, bảng tra cứu bên trái và vùng kết quả.
- Token/Wallet chỉ xuất hiện một lần trong workspace; màn hình bắt đầu vẫn có bộ chọn loại tra cứu.
- API key và thông tin sử dụng dữ liệu mở trong hộp thoại.
- Trình chỉnh video dùng cùng bố cục công cụ, cài đặt, preview và timeline.
- Các mốc thời lượng chia thành hai hàng 4 + 3; không còn nút 5m rơi xuống hàng riêng.

## Card và biểu đồ video

- Card dùng font và màu semantic từ `design-system.ts` và `frame-kit.ts`.
- Chọn theme video, nền khung, nền gradient hoặc màu riêng; hỗ trợ 4:5, 16:9, 9:16 và 1:1.
- Đường giá dùng nội suy mượt, đi qua các giá đóng và không vượt biên giữa hai điểm.
- Trục giá theo phần dữ liệu đang replay; khoảng cách nến giữ cố định trong suốt clip.
- Nến dùng cùng hình học thân/râu và cách vẽ nến đang hình thành của Chart Replayer.
- Dữ liệu mẫu dùng multi-scale value noise và wick profile của Chart, thay cho sóng sin cũ. Các số liệu mẫu vẫn được tính lại từ ledger.
- Dữ liệu OHLC thật từ Birdeye được giữ nguyên.
- Cuối clip có card tổng hợp riêng: Total PnL, multiple, tags, Invested, Entry market cap, Realized, Unrealized và đường PnL.
- Card tổng hợp dùng cùng font, theme, surface, viền và badge với dự án; giữ hiệu ứng đếm số.
- Xuất video xong có bước xem lại và nút Save video.

## Kiểm tra

- Production build: thành công.
- TypeScript và ESLint: thành công.
- 69 bài kiểm tra: thành công, gồm ledger, API, phân trang, portfolio, replay, bố cục, nội suy giá và mật độ nến.
- Trình duyệt: tra cứu mẫu token/ví, lọc và sắp xếp token, mở editor từ bảng trader và danh mục ví, chuyển tab, sáng/tối, bốn tỷ lệ video và viewport điện thoại 390 × 844.
- Xuất thử MP4 4:5, 1080 × 1350, 30 fps, có âm thanh; video đọc được và có card tổng hợp.
- Kiểm tra trực quan sử dụng dữ liệu mẫu; chưa thử API Birdeye với khóa thật.

## Chạy bản độc lập

Trong thư mục dự án:

```bash
npm ci
npm run dev -- --port 3001
```

Mở http://127.0.0.1:3001. Chọn Try a sample token hoặc Try a sample wallet để xem mà không cần API key.

Ảnh: [studio](./media/ui-editor.png), [ví](./media/ui-wallet.png), [card replay](./media/card-replay.png), [card tổng hợp](./media/card-result.png).


## Follow-up: wallet controls and confidence summary

- Tokens filters now fit their content, with Sort aligned on the same toolbar row and wrapping independently at small widths. Counts use a quieter, consistent style.
- High / Medium / Low use three equal-width centered columns with a visible Ledger confidence label.
- Verified filter empty state, restored All state, and Total PnL sorting in the browser. TypeScript and scoped ESLint checks pass.
- User approved direction A (Plata Card) on Mobbin. The outro now places a left-aligned PnL total above a prominent line chart, with supporting metrics below it on the replay surface. The fully opaque final surface removes the previous replay showing through.
- Checked all four aspect ratios, light/dark palette, and a successful 1080 × 1350, 30 fps MP4 export with audio. All 69 tests, TypeScript and scoped ESLint pass.
- Reference: https://mobbin.com/explore/screens/341fcc04-2597-4279-b662-030e5ba2c34b
