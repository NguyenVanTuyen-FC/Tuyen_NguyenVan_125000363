# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)
- **Họ và tên:** Nguyễn Văn Tuyền
- **MSSV:** 125000363
- **Tên đề tài Website:** Đặt lịch dịch vụ cho thuê phòng trọ thông qua cộng tác viên (TrọNhanh.vn)
- **Công cụ AI đã sử dụng:** Gemini, Antigravity

## 1. Yêu cầu ban đầu (System/Initial Prompt)
> *Ghi lại prompt tổng quan ban đầu bạn dùng để khởi tạo khung website.*
> 
> **Prompt:** 
"Hãy đóng vai trò là một Frontend Developer chuyên nghiệp. Hãy giúp tôi tạo một trang web hoàn chỉnh bằng HTML5 và CSS3 với đề tài: 'Đặt lịch dịch vụ cho thuê phòng trọ thông qua cộng tác viên' (TrọNhanh.vn). Website phải sử dụng đúng chuẩn Semantic HTML5 (có các thẻ `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`, `<aside>`, `<figure>`), tuyệt đối không lạm dụng thẻ `<div>` vô nghĩa. Áp dụng CSS Variables (`:root`) để quản lý toàn diện bảng màu, font chữ và hệ thống spacing nhất quán. Sử dụng layout hiện đại Flexbox và CSS Grid để giao diện responsive cân đối, đồng thời tích hợp thư viện Animate.css và AOS để tạo hiệu ứng chuyển động mượt mà, tinh tế, không gây rối mắt."
Hãy nhìn vào đề thi để thực hiện yêu cầu cần làm đủ và đúng, và chỉ được dùng code css và html để thiết kế và đáp ứng các tiêu chí trong file và hình ảnh làm sao hoàn thành đủ tiêu chí cần làm để hoàn thành
Đề tài: Đặt lịch dịch vụ cho thuê phòng trọ thông qua cộng tác viên.

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & CSS Variable
- **Prompt đã dùng:** "Kiểm tra lại cấu trúc HTML bạn vừa tạo. Đảm bảo không lạm dụng thẻ `<div>` vô nghĩa ở các khối nội dung chính. Thay vào đó hãy dùng các thẻ semantic như `<section>`, `<article>`, `<figure>`, `<figcaption>`, `<address>`. Đồng thời khai báo rõ các biến màu sắc (`--primary-color`, `--secondary-color`, `--accent-color`), font chữ và hệ thống khoảng cách (`--spacing-xs` đến `--spacing-3xl`) trong `:root` của file `style.css`."
- **Kết quả AI tạo ra:** AI đã chuẩn hóa lại mã nguồn HTML, gom nhóm các khối dịch vụ và danh sách phòng trọ bằng thẻ `<article>`, cấu hình bộ biến màu sắc và kích thước đồng bộ trong `style.css`.
- **Nhận xét & Tinh chỉnh của SV:** AI ban đầu có xu hướng đặt nhiều thẻ `<div>` lồng nhau để bọc hình ảnh và tiện ích phòng trọ. Tôi đã nhắc AI sửa lại thành `<figure>`, `<figcaption>` cho ảnh phòng, dùng `<ul class="room-amenities">` thay cho danh sách các thẻ `<span>` bọc trong `<div>`, và dùng `<header class="room-header">` bên trong thẻ `<article>`, giúp cây DOM gọn gàng và chuẩn ngữ nghĩa HTML5.

### Lần 2: Tích hợp thư viện Animate.css & AOS
- **Prompt đã dùng:** "Thêm các lớp hiệu ứng `animate__animated animate__fadeInLeft` vào tiêu đề Hero section, Logo và nút CTA. Đồng thời tích hợp thư viện Animate On Scroll (AOS) qua CDN vào các section nội dung, các thẻ dịch vụ và danh sách phòng trọ để khi cuộn trang nội dung hiện lên sinh động hơn."
- **Thách thức gặp phải:** Hiệu ứng AOS bị xung đột hoặc không hoạt động khi cuộn trang do thiếu khai báo khởi tạo JavaScript `AOS.init()`, đồng thời thuộc tính độ trễ ở một số thẻ bị AI viết nhầm thành `data-delay="100"` thay vì cú pháp chuẩn `data-aos-delay="100"`.
- **Cách sửa prompt (Debug prompt):** "Cú pháp AOS đang bị lỗi cú pháp `data-delay` và thiếu hàm kích hoạt. Hãy sửa lại đúng chuẩn `data-aos="fade-up"` kèm `data-aos-delay="100"`, đồng thời viết đoạn mã JavaScript khởi tạo `AOS.init({ duration: 750, easing: 'ease-in-out', once: true, offset: 60 })` đặt ở cuối file `index.html` trước thẻ đóng `</body>` để thư viện hoạt động ổn định và mượt mà."

### Lần 3: Tối ưu Layout Flexbox/Grid, Tránh rối mắt & Tinh chỉnh Performance
- **Prompt đã dùng:** "Rà soát lại toàn bộ giao diện theo tiêu chí đề thi: Hiệu ứng chuyển động phải mượt mà, không lạm dụng gây rối mắt. Kiểm tra layout các khối cards bằng CSS Grid. Đồng thời kiểm tra điểm Performance trên Lighthouse: xử lý dứt điểm tình trạng giật cục layout và độ trễ tải trang."
- **Thách thức gặp phải:** 
  1. Hiệu ứng nhấp nháy `animate__pulse animate__infinite` mà AI thêm vào thẻ floating card ở phần Hero có tốc độ mặc định quá nhanh (1 giây/lần), gây chớp nháy liên tục làm phân tâm và mỏi mắt người dùng.
  2. Điểm kiểm thử Performance trên Lighthouse bị cảnh báo đỏ do sử dụng ảnh online từ Unsplash gây nghẽn mạng, thiếu kích thước `width`, `height` cố định làm phát sinh lỗi dịch chuyển giao diện (CLS).
- **Cách sửa prompt (Debug prompt):** "Hãy lưu trữ hình ảnh cục bộ vào thư mục `assets/images/` theo đúng yêu cầu cấu trúc đề thi, khai báo tường minh thuộc tính `width`, `height` và `decoding="async"`, đặt `fetchpriority="high"` cho ảnh Hero và `loading="lazy"` cho các ảnh còn lại. Thay thế hiệu ứng nhấp nháy bằng `@keyframes subtleFloat` chạy êm dịu trên GPU compositor. Đồng thời căn chỉnh CSS Grid cho `.services-grid`, `.rooms-grid`, `.ctv-grid` với cấu trúc `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))` và `gap: var(--spacing-xl)`."

### Lần 4: Tự viết hiệu ứng :hover, :focus thuần CSS & Bổ sung khối Cộng Tác Viên
- **Prompt đã dùng:** "Viết toàn bộ hiệu ứng tương tác `:hover` và `:focus` bằng CSS thuần cho các nút bấm, thẻ bài viết (cards) và các ô nhập liệu trong form đặt lịch. Bổ sung khối thông tin CTV phụ trách trên từng thẻ phòng trọ (`<aside class="room-ctv-box">`) để làm nổi bật 100% đề tài 'Đặt lịch dịch vụ qua cộng tác viên'."
- **Kết quả AI tạo ra:** AI đã viết các pseudo-class `:hover` và `:focus` cho `.btn`, `.service-card`, `.room-card`, `.ctv-card` và các thẻ input trong form, đồng thời thêm box CTV có avatar, tên, số điện thoại và đánh giá sao.
- **Nhận xét & Tinh chỉnh của SV:** Tôi nhận thấy khi click vào ô input thì viền mặc định của trình duyệt không đồng bộ với màu chủ đạo của web. Tôi đã yêu cầu AI thêm hiệu ứng `:focus` với vòng viền phát sáng `box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.15)` theo biến màu `--primary-rgb`, vừa tăng tính thẩm mỹ UI vừa đạt chuẩn trải nghiệm người dùng (UX/Accessibility).

### Lần 5: Tích hợp hiệu ứng giao diện Sáng / Tối (Dark / Light Mode) bằng CSS Variables & :has()
- **Prompt đã dùng:** "Thêm tính năng chuyển đổi giao diện Sáng / Tối (Dark / Light Mode) bằng CSS Variables và selector `:has()`. Thiết kế nút gạt hiện đại có icon mặt trời/mặt trăng trên thanh Header, tự động đổi màu nền và màu chữ tương phản cao, lưu trạng thái vào LocalStorage và không làm ảnh hưởng đến điểm số Performance."
- **Kết quả AI tạo ra:** AI đã tạo nút gạt switch chuyển đổi ở góc phải Header, bổ sung bộ biến màu sắc cho `:root:has(#theme-toggle:checked)` và `[data-theme="dark"]`, biến đổi linh hoạt nền trang sang sắc đen xanh hiện đại (`#0b1120`, `#1e293b`) cùng chữ trắng sáng chuẩn WCAG.
- **Nhận xét & Tinh chỉnh của SV:** Tôi đã kiểm tra kỹ thuật chuyển đổi này và thấy nó hoạt động ngay cả khi không bật JavaScript nhờ selector thuần `:has(#theme-toggle:checked)`, đồng thời đoạn mã lưu `localStorage` giúp ghi nhớ chế độ xem yêu thích của người dùng sau khi tải lại trang web.

## 3. Đánh giá cá nhân về quá trình Vibe Coding
- **AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?**  
  AI giúp tiết kiệm đến 70% thời gian xây dựng khung sườn trang web ban đầu, viết nhanh các đoạn mã CSS căn chỉnh Grid và Flexbox phức tạp, gợi ý nội dung mô tả thực tế sát với đề tài thuê phòng trọ sinh viên, và liên kết nhanh các thư viện bên thứ ba (Animate.css, AOS, Google Fonts).

- **Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?**  
  1. **Tư duy kiến trúc phải đi trước:** Không nên để AI tự do sinh mã theo bản năng, vì AI thường lạm dụng thẻ `<div>` vô nghĩa ("div soup"). Sinh viên cần đưa ra ràng buộc kỹ thuật rõ ràng ngay từ đầu (bắt buộc dùng `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<figure>`, `<address>`).
  2. **Biết phân tích và gỡ lỗi (Debugging Iteration):** Khi thư viện không chạy hoặc animation bị giật lag, cần đọc hiểu bản chất vấn đề để đưa ra Debug Prompt chuẩn xác, chỉ đạo AI sửa đúng điểm nghẽn thay vì tạo lại từ đầu làm mất bố cục đã có.
  3. **Kiểm soát chất lượng UI/UX và chuẩn chấm điểm:** Cần kiểm soát hiệu ứng chuyển động ở mức tinh tế, không lạm dụng gây rối mắt, và sử dụng nhất quán CSS Variables cho toàn bộ màu sắc, khoảng cách để website đạt tính hoàn thiện cao nhất.