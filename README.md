# PTUD_voi_MNM3<br>

# MÔN HỌC: PHÁT TRIỂN ỨNG DỤNG VỚI MÃ NGUỒN MỞ<br>

# HỌ VÀ TÊN: LÊ TUẤN ANH<br>

# MSSV: K225480106001<br>
# LỚP: K58KTP<br>


## BÀI TẬP 04: SỬ DỤNG N8N ĐỂ TỰ ĐỘNG ĐĂNG BÀI LÊN WORDPRESS<br>

1. Triển khai và thiết lập Domain (Cloudflare Tunnel)<br>

- Cấu hình docker-compose.yml<br>

+ Sử dụng lệnh `mkdir mywordpress` và `cd mywordpress` để tạo thư mục chứa project<br>

<img width="692" height="82" alt="image" src="https://github.com/user-attachments/assets/c87f1f31-726a-44b8-82e2-2c8523ea499d" /><br>

+ Sử dụng lệnh `sudo nano docker-compose.yml` để tạo file và khi cửa sổ nano hiện ra thì thêm nội dung vào file và bấm `Ctrl + O` để lưu và `Ctrl + X` để thoát<br>


- Lấy Token và định tuyến trên Cloudflare Zero Trust<br>

+ Đăng nhập vào Cloudflare Zero Trust<br>

+ Chọn Networks -> Tunnels -> Bấm Create a tunnel -> Chọn Cloudflared -> Đặt tên -> Bấm Create tunnel<br>

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/1d077116-9bbe-49c9-a5ca-e8f24b11c91e" /><br>

+ Ở màn hình "Install and run a connector", chọn môi trường Docker. Chuỗi ký tự dài nằm ngay sau chữ --token chính là TUNNEL_TOKEN<br>

<img width="692" height="434" alt="image" src="https://github.com/user-attachments/assets/97aa7002-4694-45ed-8f6e-39fdab021220" /><br>

+ Lấy TUNNEL_TOKEN thêm vào TUNNEL_TOKEN trong file docker-compose.yml<br>

<img width="692" height="370" alt="image" src="https://github.com/user-attachments/assets/6114de6e-897e-4d87-952e-9eb33057a878" /><br>


- Khởi chạy Docker<br>

+ Sử dụng lệnh `docker compose up -d` để khởi chạy<br>

<img width="692" height="136" alt="image" src="https://github.com/user-attachments/assets/2d0c63bd-b215-4062-8fa6-58dc13d7f4a7" /><br>

+ Sau khi khởi chạy thành công quay lại màn hình "Install and run a connector" chọn Continue<br>

<img width="691" height="453" alt="image" src="https://github.com/user-attachments/assets/4bf22c78-0834-4cba-8088-5f30c335ab6c" /><br>

+ Tại màn hình Route traffic chọn Add route -> Published application, tại đây cấu hình 3 sub-domain -> Add route<br>

<img width="691" height="368" alt="image" src="https://github.com/user-attachments/assets/9a966f8b-289a-4a2d-ae9b-b7babb550087" /><br>

+ Sub-domain 1: Cho WordPress<br>

<img width="692" height="745" alt="image" src="https://github.com/user-attachments/assets/7b57bb88-45fd-481e-8a62-b17be6e2ac5d" /><br>

+ Sub-domain 2: Cho phpMyAdmin<br>

<img width="692" height="671" alt="image" src="https://github.com/user-attachments/assets/6ee114ec-6140-4a4f-af98-cc34c056c3bd" /><br>

+ Sub-domain 3: Cho n8n<br>

<img width="692" height="740" alt="image" src="https://github.com/user-attachments/assets/00350574-6d03-486c-8651-2322c9f78693" /><br>

+ Sau khi tạo 3 sub-domain, lấy địa chỉ n8n và thêm vào WEBHOOK_URL TRONG file docker-compose.yml và khởi chạy file<br>

<img width="692" height="283" alt="image" src="https://github.com/user-attachments/assets/eeee370f-cc87-4808-a68b-93396d9bd43e" /><br>


- Kiểm tra Sub-domain<br>

+ phpmyadmin: truy cập `https://mydb.letuananh123pl.id.vn` để vào trang quản trị database, lúc này database hiện đang trống<br>

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/51576542-f5ce-4cee-b4de-5a0e47b9585f" /><br>

+ WordPress:  truy cập vào `https://mywp.letuananh123pl.id.vn<br>

+ Điền tên Website, tên đăng nhập Admin, Mật khẩu, cuối cùng chọn cài đặt và đăng nhập vào trang quản trị của WordPress<br>

<img width="691" height="370" alt="image" src="https://github.com/user-attachments/assets/9884dc38-cceb-48d8-8da1-7ec252ab7952" /><br>

+ Truy cập lại `https://mydb.letuananh123pl.id.vn` lúc này sẽ thấy WordPress đã tự động sinh ra hàng loạt các bảng dữ liệu (có tiền tố wp_...)<br>

<img width="691" height="368" alt="image" src="https://github.com/user-attachments/assets/c7e070f1-f7a9-4bae-b06a-c1cbb7232267" /><br>

+ Cấu hình tài khoản n8n: truy cập `https://myn8n.letuananh123pl.id.vn<br>

+ Điền đúng email thật và đặt một mật khẩu để tạo tài khoản Admin<br>

<img width="691" height="371" alt="image" src="https://github.com/user-attachments/assets/20a4de0b-77c7-4fea-9563-6bfdc4375e9f" /><br>

+ Tại góc dưới cùng bên trái, bấm vào chữ Settings (Cài đặt) -> Chọn mục Usage and plan -> License Key (chuỗi mã kích hoạt) sẽ được gửi về email, copy cái License Key -> quay lại n8n, dán vào ô Enter activation key và bấm Activate<br>

<img width="691" height="370" alt="image" src="https://github.com/user-attachments/assets/f81a07d5-16f3-4670-a39a-ded13f23d22b" /><br>


2. Tạo 2 bài viết trên Wordpress<br>

+ bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...<br>

<img width="692" height="370" alt="image" src="https://github.com/user-attachments/assets/faa7b65f-1d61-44be-b362-fe270d1d4ab3" /><br>

+ bài viết trong wordpress giới thiệu về ngành học mà em yêu thích trong trường TNUT. bài viết phải chứa hình ảnh, video, …<br>

<img width="692" height="370" alt="image" src="https://github.com/user-attachments/assets/885eda03-6b00-49a5-882c-e07f720fed70" /><br>


3. Chuẩn bị Credentials cho n8n<br>

-  **WordPress Application Password :** Vào trang quản trị WordPress ở thanh menu chọn `Tài khoản` -> `Hồ sơ` . Tìm mục Mật khẩu ứng dụng (Application Passwords) và ở ô "Tên mật khẩu ứng dụng mới" gõ n8n_auto rồi bấm nút Thêm mật khẩu ứng dụng mới. WordPress sẽ hiện ra một dãy mật khẩu<br>

<img width="691" height="369" alt="image" src="https://github.com/user-attachments/assets/b46c6ea7-2b4c-48c9-b90e-12b01df679d6" /><br>

- **Telegram Bot Token:** Mở ứng dụng Telegram gõ vào ô tìm kiếm chữ: @BotFather. Bấm Start rồi gõ lệnh /newbot, gõ tên Bot (Name) tùy thích, gõ tên Username của Bot (bắt buộc phải gõ không dấu, viết liền và kết thúc bằng chữ bot). BotFather sẽ đưa ra một dòng Token (dạng 123456789:AAH...)<br>

<img width="687" height="813" alt="image" src="https://github.com/user-attachments/assets/e8d7e4db-6d06-4206-8fbe-e92a318de550" /><br>

- **Google Gemini API Key:** Truy cập vào Google AI Studio: `https://aistudio.google.com/` và đăng nhập bằng Gmail, ở menu bên trái bấm vào Get API key -> Create API key -> Create API key in new project. Hệ thống sẽ sinh ra một chuỗi mã API Key<br>

<img width="691" height="370" alt="image" src="https://github.com/user-attachments/assets/1edc94ff-ca32-43c3-98a4-65c3b24594c6" /><br>


4. Xây dựng workflow trên n8n<br>

- Khởi tạo Workflow: Tại trang chủ n8n, chọn Workflows -> Bấm Create workflow (hoặc Start from scratch)<br>


- NODE 1 - Telegram Trigger<br>

+ Bấm Add first step, gõ tìm Telegram -> Chọn Telegram -> Chọn On message<br>

<img width="691" height="370" alt="image" src="https://github.com/user-attachments/assets/2fb4cd92-4702-4549-86f3-87bee119cbe8" /><br>

+ Ở phần Parameter tại mục Credential chọn Set up Credential. Khi cửa sổ hiện ra dán mã Token của BotFather vào ô Access Token rồi bấm Save<br>

<img width="691" height="371" alt="image" src="https://github.com/user-attachments/assets/0b2f371c-f964-468b-914d-737a3347932d" /><br>

+ Đóng cửa sổ cài đặt Token, chọn Test this trigger để n8n bắt đầu ở trạng thái chờ. Chat với Telegram Bot 1 câu bất kì. Quay lại n8n sẽ thấy hiện chữ Success<br>

<img width="691" height="372" alt="image" src="https://github.com/user-attachments/assets/903ee64e-5a23-40b4-a29c-320d5aa4c92a" /><br>


- Cấu hình NODE 2 - Google Gemini<br>

+ Bấm vào dấu +  bên phải Node Telegram Trigger rồi gõ chữ Google Gemini -> Chọn biểu tượng Google Gemini -> Message a model<br>

<img width="691" height="370" alt="image" src="https://github.com/user-attachments/assets/cc9a8167-046a-4009-bb8e-d752b082cace" /><br>

+ Tại mục Credential chọn Set up Credential. Khi cửa sổ hiện ra dán mã dán mã API Key đã lấy ở Google AI Studio vào, sau đó bấm Save<br>

<img width="691" height="370" alt="image" src="https://github.com/user-attachments/assets/19466054-1789-4b94-b552-015a8f02f2a6" /><br>

+ Mục Model chọn gemini-3-flash-preview, có thể chọn phiên bản khác nếu muốn. Tại ô tên là Message thêm nội dung vào Prompt rồi chọn Expression. Kéo xuống dưới cùng của Node Gemini gạt công tắc của Output Content as JSON sang TURN ON<br>

<img width="691" height="370" alt="image" src="https://github.com/user-attachments/assets/db0268e4-2be4-4ef1-8537-556258b31817" /><br>

+ Bấm nút Execute step và chờ Gemini xử lý. Khi thành công, ở cột Output bên phải sẽ thấy AI trả về một chuỗi text thô lộn xộn nhưng chứa cấu trúc post_title và post_content.<br>

<img width="691" height="369" alt="image" src="https://github.com/user-attachments/assets/bfd2dd6e-ce48-41cf-bcf2-7908ea155d05" /><br>


- NODE 3 - Code in JavaScript<br>

+ Bấm vào dấu + bên phải Node Gemini, tìm kiếm chữ Code -> Chọn Node Code -> Chọn Code in Javascript<br>

<img width="691" height="371" alt="image" src="https://github.com/user-attachments/assets/7621dcf3-1006-4494-a013-72098988ec2f" /><br>

+ Tại ô cấu hình, đảm bảo mục Language đang chọn là JavaScript, xóa sạch Code mặc định của n8n và thêm Code mới<br>

<img width="691" height="370" alt="image" src="https://github.com/user-attachments/assets/a43b8035-c1e9-4865-8e69-3257c3b4814c" /><br>

+ Bấm Execute step. Lúc này, ở cột Output bên phải sẽ thấy dữ liệu được bóc tách gọn gàng, chia rõ làm 2 mục title và content<br>

<img width="691" height="369" alt="image" src="https://github.com/user-attachments/assets/07435ec3-cf93-4b6d-b628-6e0fdcd19603" /><br>


- NODE 4 - WordPress<br>

+ Bấm vào dấu + bên phải Node Code, tìm kiếm WordPress -> Chọn Create a post<br>

<img width="691" height="369" alt="image" src="https://github.com/user-attachments/assets/40b4acb8-d607-479a-bf2d-353d9d10b68b" /><br>

+ Ở phần Parameter tại mục Credential chọn Set up Credential. Khi cửa sổ hiện ra điền địa chỉ URL, Username và Password (dùng Application Password). Ở Credential, tìm dòng Ignore SSL Issues (Insecure) và gạt sang TURN ON và bấm Save<br>

<img width="691" height="371" alt="image" src="https://github.com/user-attachments/assets/cd66d4c6-2aa0-451f-ab69-ed398f1819fc" /><br>

+ Tại ô Title: Chọn tab Expression, nhìn sang cột dữ liệu bên trái của Node Code, kéo thả biến title vào<br>

<img width="692" height="327" alt="image" src="https://github.com/user-attachments/assets/20747d08-c008-49ed-9257-9ec420319bbf" /><br>

+ Chọn Add Field -> Chọn Content. Chọn tab Expression, kéo thả biến content từ Node Code vào<br>

<img width="691" height="369" alt="image" src="https://github.com/user-attachments/assets/d4ad7ab2-c711-4fbc-9e3d-15aebf849a99" /><br>

+ Chọn Add Field -> Chọn Status. Chuyển từ Draft sang Publish. Bấm Execute step để kiểm tra, cột bên phải báo thành công là bài đăng đã tự đăng lên wordpress<br>

<img width="691" height="368" alt="image" src="https://github.com/user-attachments/assets/f0d78612-cb2f-497d-80e9-935e645ca91d" /><br>


5. Kiểm thử kết quả<br>

- Tại góc trên cùng bên phải màn hình n8n, bấm nút Publish để chuyển trạng thái Workflow sang Active<br>

<img width="691" height="371" alt="image" src="https://github.com/user-attachments/assets/c6ef107e-6732-40dc-ad6c-8a09c80c1334" /><br>


- Gửi yêu cầu đăng bài từ telegram và xem kết quả<br
  
<img width="692" height="367" alt="image" src="https://github.com/user-attachments/assets/b484375a-bef1-4c89-b350-ec70566544f3" /><br>

