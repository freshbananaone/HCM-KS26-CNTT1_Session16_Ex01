# Bài 1: Hệ thống quản lý tài liệu dự án doanh nghiệp

**Dự án: Số hóa Bảo tàng PTIT**

## 1. Vấn đề của nhóm

Trong tình huống của đề bài, việc ổ cứng bị Bad Sector khiến bạn A mất file thiết kế, còn bản đã gửi qua Zalo lại hết hạn tải xuống. Nguyên nhân khiến nhóm khó khôi phục công việc là chỉ có một bản làm việc trên máy A và chưa có thói quen sao lưu thường xuyên. Nếu bản gửi qua Zalo vẫn tải được thì bản đó cũng có thể đã cũ, thiếu những chỉnh sửa gần nhất.

Em đề xuất nhóm sử dụng mô hình Hybrid Workflow: vẫn thiết kế trên SSD của máy tính, nhưng lưu file trong thư mục được đồng bộ tự động lên Cloud. Cách này phù hợp với công việc 3D vì bạn A có thể thao tác trực tiếp trên máy, đồng thời cả nhóm có một nơi chung để lưu và theo dõi tài liệu.

Với giả định nhà trường đã cung cấp tài khoản Microsoft 365 phù hợp, nhóm có thể dùng SharePoint làm nơi lưu tài liệu chung và OneDrive để đồng bộ thư mục đó về từng máy.

## 2. Quy trình làm việc từ Local SSD lên Cloud

Nhóm tạo thư mục dự án `PTIT-Museum`, bên trong chia theo từng hiện vật. Mỗi thư mục chứa file thiết kế và các tài nguyên đi kèm, chẳng hạn hình ảnh dùng làm vật liệu. Bạn A mở và chỉnh sửa file ngay trong thư mục đã đồng bộ, không lưu rải rác ở Desktop hay Downloads.

Luồng dữ liệu được tổ chức như sau:

```text
Bạn A chỉnh sửa mô hình 3D
             |
          Ctrl + S
             v
File được lưu vào thư mục dự án trên SSD
             |
             v
OneDrive phát hiện thay đổi
             |
             +-- Mất mạng / file chưa thể tải lên
             |          |
             |          v
             |   Giữ bản đã lưu trên máy
             |   và đồng bộ khi đủ điều kiện
             |          |
             v          v
      Tải file lên SharePoint
             |
             +-- Có xung đột --> Giữ các bản để đối chiếu
             |                  rồi chọn bản thống nhất
             v
Cloud cập nhật file và lưu lịch sử theo cấu hình
             |
             v
Các thành viên nhận bản mới qua đồng bộ
```

Sau khi nhấn Ctrl + S, bạn A không cần tự nén file rồi gửi lại cho từng người. OneDrive sẽ xử lý việc đồng bộ khi có kết nối và file có thể được tải lên.

Tuy nhiên, “sao lưu ngay khi Ctrl + S” cần được hiểu là tự động đồng bộ sau khi lưu, chứ không phải Cloud lập tức có bản hoàn chỉnh. File 3D lớn vẫn cần thời gian tải lên; một số file đang được phần mềm sử dụng có thể phải đóng lại mới đồng bộ xong. Trước khi bàn giao, bạn A cần kiểm tra trạng thái OneDrive và xem bản mới đã xuất hiện trên SharePoint hay chưa.

Nhóm cũng nên dành một thư mục riêng cho các bản đã được duyệt. Mỗi mốc quan trọng cần có ghi chú ngắn, ví dụ “đã kiểm tra hình dáng và vật liệu”, để sau này dễ chọn bản khôi phục.

## 3. Khi mất mạng hoặc sập nguồn thì xử lý thế nào?

**Nếu mất Internet**, bạn A vẫn có thể làm việc với các file đã được tải đầy đủ về máy. Những thay đổi đã lưu nằm trên SSD và sẽ được đồng bộ khi mạng hoạt động trở lại. Vì vậy, thư mục đang làm cần được chọn chế độ **Always keep on this device**, thay vì chỉ giữ file trên Cloud.

Nếu mạng mất giữa lúc tải lên, nhóm chưa được xem lần tải đó là hoàn tất. Khi có mạng, để OneDrive xử lý lại rồi kiểm tra bản trên web. Cũng cần lưu ý rằng nhiều lần Ctrl + S trong lúc offline không có nghĩa Cloud sẽ giữ riêng từng lần lưu đó; khi kết nối lại, có thể chỉ trạng thái cuối cùng được tải lên.

**Nếu máy sập nguồn**, cần phân biệt hai trường hợp. Khi file đã được ghi hoàn chỉnh xuống SSD, bản Local có thể vẫn còn và tiếp tục được đồng bộ sau khi khởi động lại. Nhưng nếu mất điện đúng lúc phần mềm đang ghi file, bản đang lưu có thể bị hỏng. Lúc này phải tìm bản phục hồi của phần mềm thiết kế hoặc lấy lại bản ổn định trên Cloud.

Để giảm thiệt hại, nhóm nên bật tính năng tự lưu và tạo bản dự phòng của phần mềm 3D nếu phần mềm hỗ trợ. Máy trạm có thể dùng bộ lưu điện UPS để có thời gian lưu và tắt máy khi mất điện. Ngoài ra, các mốc thiết kế quan trọng nên được sao lưu thêm sang ổ ngoài hoặc một kho độc lập.

Không có cách đồng bộ nào bảo đảm tải dữ liệu lên Cloud khi máy không có mạng hoặc đã tắt nguồn. Nếu SSD hỏng trong lúc offline, phần việc chưa được sao lưu ra nơi khác vẫn có thể mất. Vì thế, giải pháp cần kết hợp đồng bộ tự động với bản dự phòng, thay vì chỉ dựa vào một công cụ.

## 4. Cách xử lý xung đột phiên bản

Ví dụ, A và B cùng mở file `HienVat_001.blend`. A mất mạng rồi sửa hình dáng mô hình, còn B sửa vật liệu và lưu lên Cloud. Khi máy A có mạng trở lại, hai người đã tạo ra hai bản khác nhau từ cùng một file ban đầu. Đây là tình huống có thể dẫn đến File Version Conflict.

Với file 3D, nhóm không nên trông chờ OneDrive tự ghép các chỉnh sửa. Khi có thông báo xung đột hoặc xuất hiện bản trùng, hai người cần tạm dừng sửa file đó và giữ lại cả hai bản. Bản Local chưa đồng bộ nên được sao chép ra ngoài thư mục đồng bộ trước khi xử lý, tránh mất thay đổi do chọn nhầm thao tác ghi đè.

Sau đó, người phụ trách mở từng bản trong phần mềm thiết kế để kiểm tra. Nếu cả hai đều có phần cần giữ, người thiết kế sẽ kết hợp các thành phần phù hợp bằng công cụ của phần mềm. Nếu một bản bị lỗi, nhóm chọn bản còn lại sau khi đối chiếu với yêu cầu dự án. Không nên mặc định bản có thời gian sửa mới nhất là bản đúng nhất.

Khi đã thống nhất, lưu bản được chọn vào file làm việc chính, chờ đồng bộ xong rồi báo cho cả nhóm nhận bản mới. Các bản đối chiếu nên được giữ lại cho đến khi kiểm tra hoàn tất.

Để hạn chế tình huống này, nhóm phân công mỗi người phụ trách một hiện vật hoặc một phần riêng. Với cùng một file, chỉ một người chỉnh sửa tại một thời điểm; người tiếp theo bắt đầu sau khi người trước đã lưu và đồng bộ xong.

## 5. Khôi phục bản ổn định bằng Version History

Version History giúp nhóm lấy lại các phiên bản trước đã được lưu trên Cloud. Trước khi làm việc, người quản lý cần kiểm tra thư viện đã bật tính năng này, thời gian hoặc số lượng phiên bản được giữ lại và quyền khôi phục của các thành viên.

Chẳng hạn, nhóm đã duyệt bản V5 nhưng sau đó một thành viên sửa nhầm, làm bản V6 bị lỗi. Nhóm sẽ khôi phục theo trình tự sau:

1. Tạm dừng chỉnh sửa file và giữ riêng các thay đổi chưa đồng bộ để tránh ghi đè trong lúc khôi phục.
2. Mở SharePoint trên trình duyệt, tìm file rồi chọn **Version history**.
3. Xem thời điểm và người chỉnh sửa để tìm V5. Tải hoặc mở bản này để kiểm tra trước khi quyết định khôi phục.
4. Chọn **Restore** cho bản đã xác nhận, sau đó chờ các máy đồng bộ và mở lại file để kiểm tra.

Việc kiểm tra phải bao gồm cả mô hình và tài nguyên đi kèm. Nếu bản vẽ dùng texture hoặc file liên kết đã thay đổi, chỉ khôi phục riêng file mô hình có thể chưa đủ; nhóm cần lấy lại các tài nguyên tương ứng.

Version History chỉ khôi phục được những phiên bản đã lên Cloud và còn trong thời hạn lưu giữ. Tính năng này không cứu được phần việc chưa từng đồng bộ. Đồng bộ cũng có thể đưa thao tác xóa nhầm lên Cloud, nên bản sao độc lập vẫn cần thiết.

## 6. Ba bước thiết lập cho một Designer

**Bước 1: Cài OneDrive và kết nối thư mục dự án.**

Designer đăng nhập OneDrive bằng tài khoản của trường hoặc đơn vị, mở thư viện SharePoint của nhóm rồi chọn **Sync**. Kiểm tra thư mục dự án đã xuất hiện trên SSD và bật OneDrive chạy khi đăng nhập máy. Người quản lý xác nhận quyền truy cập và Version History đã được thiết lập.

**Bước 2: Đặt đúng nơi lưu và chuẩn bị làm việc offline.**

Chọn **Always keep on this device** cho thư mục đang làm và chờ tải đầy đủ. Chuyển file thiết kế cùng các tài nguyên liên quan vào đó, rồi mở file từ chính thư mục này để làm việc. Bật tự lưu và bản dự phòng trong phần mềm thiết kế nếu có.

**Bước 3: Thử đồng bộ và khôi phục trước khi dùng chính thức.**

Dùng một file thử, chỉnh sửa rồi nhấn Ctrl + S và kiểm tra bản trên web. Tiếp theo, ngắt mạng, sửa và lưu file, sau đó kết nối lại để kiểm tra đồng bộ. Cuối cùng, thử lấy lại một bản cũ bằng Version History. Khi các thao tác đều thực hiện được, Designer áp dụng quy trình cho dữ liệu thật và kiểm tra đồng bộ trước mỗi lần bàn giao.

