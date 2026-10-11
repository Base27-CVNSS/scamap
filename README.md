# SCAMAP · WebGIS hồ sơ lừa đảo tài chính Việt Nam

**Bản đồ OpenStreetMap trực tuyến + bản đồ vector dự phòng offline · 2016–10/2026.**

Trang ứng dụng: `index.html` (HTML độc lập, toàn bộ CSS/JS và dữ liệu ban đầu tích hợp trong một tệp). Không sử dụng API key, CDN JavaScript hoặc dịch vụ backend.

## Chạy ứng dụng

- **GitHub Pages:** trong `Settings → Pages`, chọn **Deploy from a branch**, `main` và `/(root)`. Sau khi GitHub Pages triển khai xong, đường dẫn dự kiến: https://base27-cvnss.github.io/scamap/
- **Trực tuyến:** mở trang từ GitHub Pages, bản đồ chọn **🌍 OpenStreetMap**. Tile bản đồ được yêu cầu khi người dùng đang xem vùng tương ứng, có Internet.
- **Offline:** tải `index.html` về máy, mở trong trình duyệt và chọn **▧ Offline · vector**. File HTML vẫn truy vấn/lọc/xem hồ sơ hoàn toàn offline. Không có ảnh nền đường phố OSM khi mất mạng. Nếu tile OSM không tải được, giao diện tự chuyển bản đồ vector dự phòng sau nhiều lỗi tải.
- **Di động:** lựa chọn nền bản đồ xuất hiện ở góc trên bên phải vùng bản đồ.

## Dữ liệu

- Dữ liệu ban đầu kế thừa bộ Fraud Atlas trước đó: **106 nhóm hồ sơ** sau khi gộp bản ghi trùng, trong đó **28 hồ sơ có nguồn công khai để đối chiếu** và 78 nhóm cần tiếp tục xác minh. Chưa đủ 300 vụ được kiểm chứng.
- Có bộ lọc 2016–2026, loại hình, tình trạng đối chiếu, sơ đồ liên hệ theo thuộc tính, timeline và chi tiết nguồn.
- Điểm trên bản đồ nằm tại **tọa độ đại diện cấp tỉnh/thành**, không phải vị trí xảy ra hành vi, vị trí nghi can hay nơi chuyển tiền. Một điểm có thể biểu thị nhiều vụ.
- Không được cộng lẫn tiền giao dịch, tiền huy động, tài sản phong tỏa và số tiền thiệt hại.
- CSV tại thư mục `data/` gồm bảng kiểm toán trùng, nhật ký nguồn, mẫu nhập các hồ sơ còn thiếu.
- Dữ liệu tự nhập vào trình duyệt được lưu tại localStorage của chính trình duyệt; **hãy xuất JSON định kỳ**. GitHub không đồng bộ dữ liệu do người xem tự nhập.

## Nền bản đồ OSM và quyền sử dụng

Lớp bản đồ trực tuyến là các tile chuẩn `https://tile.openstreetmap.org/{z}/{x}/{y}.png`. Hiển thị ghi công **© OpenStreetMap contributors** và liên kết giấy phép. OSM thuộc giấy phép **Open Database License (ODbL)** đối với cơ sở dữ liệu; mã ứng dụng của SCAMAP là **MIT**; các hồ sơ/bài báo bên ngoài giữ nguyên quyền và điều kiện của nguồn.

**TUYỆT ĐỐI KHÔNG** tự động tải hàng loạt tile OSM, prefetch toàn quốc, tạo MBTiles/PMTiles từ tile.openstreetmap.org hoặc dùng tile cộng đồng cho mục đích offline. Để có **nền đường phố offline thực sự**, phải tự host tile theo đúng bản quyền hoặc sử dụng nhà cung cấp cho phép tải/gói offline.

Chính sách: https://operations.osmfoundation.org/policies/tiles/ · ghi công https://www.openstreetmap.org/copyright

## Đóng góp dữ liệu và lưu ý pháp lý

Đối chiếu từng vụ theo nguồn công khai, ngày đăng, hành vi bị điều tra và tiến độ tố tụng. Không suy diễn một người là có tội từ tin điều tra hoặc đơn tố giác. Chỉ dùng thông tin công khai có kiểm chứng. Ưu tiên gộp giai đoạn điều tra/truy tố/xét xử của cùng một vụ vào **một nhóm hồ sơ**.

Mục đích: trực quan hóa phục vụ nghiên cứu, giáo dục và nhận diện thủ đoạn lừa đảo. **Không phải hồ sơ nghiệp vụ hoặc kết luận điều tra.**

## Giấy phép

- Mã nguồn SCAMAP: MIT, © 2026 Long Ngo.
- OpenStreetMap: © OpenStreetMap contributors (ODbL); tile do OSMF vận hành có điều kiện sử dụng riêng.
- Thông tin, trích dẫn từ cơ quan báo chí: theo quyền của bên cung cấp.
