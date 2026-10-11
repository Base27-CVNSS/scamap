# SCAMAP · WebGIS hồ sơ lừa đảo tài chính Việt Nam

**Vietflex Map SDK 1.0.0 · nền OpenStreetMap trực tuyến (mặc định), Google Legacy (chọn riêng) và bản đồ vector offline · 2016–10/2026.**

Trang ứng dụng: `index.html` (CSS/JS logic và dữ liệu hồ sơ tích hợp trong một tệp). **Vietflex SDK** tải từ CDN jsDelivr tại commit cố định `6144d565fcf236727577ab3c4471bbe49f86892f`, dự phòng bằng bản sao trong `vendor/`. Không cần backend hay API key cho chế độ OSM; tùy chọn Google Legacy không phải tích hợp API chính thức.

## Chạy ứng dụng

- **GitHub Pages:** trong `Settings → Pages`, chọn **Deploy from a branch**, `main` và `/(root)`. Sau khi GitHub Pages triển khai xong, đường dẫn dự kiến: https://base27-cvnss.github.io/scamap/
- **Trực tuyến:** mở GitHub Pages, dùng **🌍 Vietflex / OpenStreetMap** (mặc định) hoặc chọn **🇻🇳 Vietflex / Google Legacy** theo yêu cầu khi chấp nhận điều kiện sử dụng. Cả hai đều sử dụng Vietflex/Leaflet để hiển thị marker, popup, GeoJSON, zoom và pan. Nền đường phố yêu cầu Internet.
- **Offline:** mở `index.html` đã tải về máy hoặc mở bản sao từ repository; chế độ **▧ Bản đồ offline** sử dụng SVG vector tích hợp. Bộ lọc, bảng và dữ liệu hồ sơ hoạt động offline. Không tải và không lưu tile OSM hoặc Google để dùng offline. File HTML đơn lẻ chạy được ở chế độ SVG; khi chạy trực tuyến cần mạng hoặc đặt thư mục `vendor/` bên cạnh HTML. Lỗi tải thư viện/tile chuyển về dự phòng.
- **Di động:** lựa chọn nền bản đồ xuất hiện ở góc trên bên phải vùng bản đồ.

## Dữ liệu

- Dữ liệu ban đầu kế thừa bộ Fraud Atlas trước đó: **106 nhóm hồ sơ** sau khi gộp bản ghi trùng, trong đó **28 hồ sơ có nguồn công khai để đối chiếu** và 78 nhóm cần tiếp tục xác minh. Chưa đủ 300 vụ được kiểm chứng.
- Có bộ lọc 2016–2026, loại hình, tình trạng đối chiếu, sơ đồ liên hệ theo thuộc tính, timeline và chi tiết nguồn.
- Điểm trên bản đồ nằm tại **tọa độ đại diện cấp tỉnh/thành**, không phải vị trí xảy ra hành vi, vị trí nghi can hay nơi chuyển tiền. Một điểm có thể biểu thị nhiều vụ.
- Không được cộng lẫn tiền giao dịch, tiền huy động, tài sản phong tỏa và số tiền thiệt hại.
- CSV tại thư mục `data/` gồm bảng kiểm toán trùng, nhật ký nguồn, mẫu nhập các hồ sơ còn thiếu.
- Dữ liệu tự nhập vào trình duyệt được lưu tại localStorage của chính trình duyệt; **hãy xuất JSON định kỳ**. GitHub không đồng bộ dữ liệu do người xem tự nhập.

## Vietflex SDK, OSM và quyền sử dụng

Bản đồ sử dụng Vietflex SDK v1.0.0 xây trên Leaflet, với `new Vietflex.ZoomControl({position:'topleft'})` và `new Vietflex.AttributionControl({position:'bottomright'})`. Thư viện đóng gói tại `vendor/vietflex.js`, `vendor/vietflex.css` cùng bản quyền BSD-2-Clause tại `vendor/LEAFLET_BSD_2_CLAUSE.txt`.

Lớp nền OSM trực tuyến là các tile chuẩn `https://tile.openstreetmap.org/{z}/{x}/{y}.png`. Hiển thị ghi công **© OpenStreetMap contributors** và liên kết giấy phép. OSM thuộc giấy phép **Open Database License (ODbL)** đối với cơ sở dữ liệu; mã ứng dụng của SCAMAP là **MIT**; các hồ sơ/bài báo bên ngoài giữ nguyên quyền và điều kiện của nguồn.

**TUYỆT ĐỐI KHÔNG** tự động tải hàng loạt tile OSM, prefetch toàn quốc, tạo MBTiles/PMTiles từ tile.openstreetmap.org hoặc dùng tile cộng đồng cho mục đích offline. Để có **nền đường phố offline thực sự**, phải tự host tile theo đúng bản quyền hoặc sử dụng nhà cung cấp cho phép tải/gói offline.

Chính sách: https://operations.osmfoundation.org/policies/tiles/ · ghi công https://www.openstreetmap.org/copyright

### Cấu hình Google Legacy theo mẫu người dùng

```js
const map = Vietflex.vietflexMap('vietflex-map', {
  center: [16.25, 106.3], zoom: 5,
  googleMaps: true,
  useLegacyGoogleTiles: true,
  googleMapType: 'roadmap',
  zoomControl: false, attributionControl: false
});
new Vietflex.ZoomControl({position: 'topleft'}).addTo(map);
new Vietflex.AttributionControl({position: 'bottomright'}).addTo(map);
```

**Lưu ý bản quyền/kỹ thuật:** tùy chọn Google Legacy của SDK lấy trực tiếp ảnh tile từ `*.google.com/vt` theo cơ chế cũ. Đây **không phải Map Tiles API chính thức** của Google; việc tải có thể bị chặn, thay đổi hoặc không phù hợp điều khoản dịch vụ. Chỉ chọn khi có quyền sử dụng phù hợp. **Để triển khai thương mại hoặc công khai, sử dụng SDK/API chính thức của Google với key và tuân thủ logo/ghi công**, hoặc dùng OSM. Xem https://developers.google.com/maps/documentation/tile/policies và https://developers.google.com/maps/documentation/tile/overview.

Nguồn SDK: https://github.com/Vietflexmap/VN/tree/6144d565fcf236727577ab3c4471bbe49f86892f

CDN ghim phiên bản:

- `https://cdn.jsdelivr.net/gh/Vietflexmap/VN@6144d565fcf236727577ab3c4471bbe49f86892f/dist/vietflex.css`
- `https://cdn.jsdelivr.net/gh/Vietflexmap/VN@6144d565fcf236727577ab3c4471bbe49f86892f/dist/vietflex.js`

## Đóng góp dữ liệu và lưu ý pháp lý

Đối chiếu từng vụ theo nguồn công khai, ngày đăng, hành vi bị điều tra và tiến độ tố tụng. Không suy diễn một người là có tội từ tin điều tra hoặc đơn tố giác. Chỉ dùng thông tin công khai có kiểm chứng. Ưu tiên gộp giai đoạn điều tra/truy tố/xét xử của cùng một vụ vào **một nhóm hồ sơ**.

Mục đích: trực quan hóa phục vụ nghiên cứu, giáo dục và nhận diện thủ đoạn lừa đảo. **Không phải hồ sơ nghiệp vụ hoặc kết luận điều tra.**

## Giấy phép

- Mã nguồn SCAMAP: MIT, © 2026 Long Ngo.
- Vietflex SDK: © Vietflexmap / Long Ngo (MIT phần bổ sung), mã Leaflet gốc BSD-2-Clause.
- OpenStreetMap: © OpenStreetMap contributors (ODbL); tile do OSMF vận hành có điều kiện sử dụng riêng.
- Google Maps: nội dung/tile theo quy định Google, không nằm trong giấy phép MIT của SCAMAP.
- Thông tin, trích dẫn từ cơ quan báo chí: theo quyền của bên cung cấp.
