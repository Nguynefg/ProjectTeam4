# Hướng dẫn kết nối và sửa project ProjectTeam4 bằng Git

Repository chung: https://github.com/Nguynefg/ProjectTeam4

## 1. Chuẩn bị

Mỗi thành viên cài Git, tạo tài khoản GitHub riêng và chấp nhận lời mời Collaborator từ trưởng nhóm.

Mở Git Bash, khai báo thông tin của mình một lần:

```bash
git config --global user.name "Ten cua ban"
git config --global user.email "email-cua-ban"
```

Thay tên và email bằng thông tin thật; dùng email đã liên kết với tài khoản GitHub.

Chỉ nhập các lệnh trong khung code. Không nhập dấu `$` hoặc các dòng kết quả terminal.

## 2. Kết nối với project chung

### Nếu chưa có project trên máy

Mở Git Bash trong thư mục muốn lưu project, chạy:

```bash
git clone https://github.com/Nguynefg/ProjectTeam4.git
cd ProjectTeam4
git status
```

Lệnh `clone` tải project về máy và tự thiết lập kết nối GitHub. Chỉ cần thực hiện một lần.

### Nếu đã có project trên máy

Đi vào đúng thư mục project. Ví dụ:

```bash
cd "/f/Zalo Data/Phát triển phần mềm mã nguồn Mở/ProjectTeam4"
git status
git remote -v
```

Thay đường dẫn bằng vị trí project của bạn. Đường dẫn có khoảng trắng phải đặt trong dấu ngoặc kép.

Nếu `git remote -v` hiển thị địa chỉ repository đúng, bạn đã kết nối thành công.

Nếu chưa có `origin`, chạy:

```bash
git remote add origin https://github.com/Nguynefg/ProjectTeam4.git
```

Nếu `origin` đang trỏ đến địa chỉ sai, chạy:

```bash
git remote set-url origin https://github.com/Nguynefg/ProjectTeam4.git
```

Nếu báo `not a git repository`, kiểm tra lại thư mục đang mở. Với thành viên mới, nên clone project chung thay vì khởi tạo Git trong một thư mục khác.

## 3. Tạo nhanh nhánh để sửa nội dung

Trước khi bắt đầu, lưu và commit công việc đang làm nếu có. Sau đó cập nhật code chung và tạo nhánh mới:

```bash
git switch main
git pull --ff-only origin main
git switch -c feature/ten-ban-sua-noi-dung
```

Thay `ten-ban` bằng tên thành viên. Mỗi công việc mới dùng một tên nhánh chưa tồn tại.

Ví dụ:

```bash
git switch -c feature/an-sua-gioi-thieu
```

Nhánh riêng giúp mỗi thành viên làm việc và gửi thay đổi để nhóm kiểm tra trước khi gộp vào `main`.

## 4. Sửa file và lưu thay đổi

Để sửa nội dung trang, mở:

```bash
notepad index.html
```

Sửa nội dung trong Notepad, nhấn **Ctrl+S**, rồi đóng cửa sổ.

Các file khác có thể mở tương tự:

```bash
notepad style.css
```

```bash
notepad script.js
```

- `index.html`: nội dung và danh sách thành viên.
- `style.css`: màu sắc, bố cục và giao diện.
- `script.js`: chức năng tương tác.

Kiểm tra thay đổi trước khi commit:

```bash
git status
git diff
```

Trong kết quả `git diff`, dòng có dấu `-` là nội dung cũ, dòng có dấu `+` là nội dung mới.

## 5. Commit và đẩy thay đổi lên GitHub

Ví dụ sau khi sửa `index.html`:

```bash
git add index.html
git commit -m "Cap nhat noi dung trang"
git push -u origin feature/ten-ban-sua-noi-dung
```

Tên nhánh trong lệnh `push` phải trùng với nhánh đã tạo ở bước 3.

| Lệnh | Ý nghĩa |
| --- | --- |
| `git add index.html` | Chọn thay đổi trong file để đưa vào commit |
| `git commit -m "..."` | Lưu một mốc lịch sử trên máy kèm mô tả |
| `git push -u origin ...` | Đẩy commit lên GitHub và liên kết nhánh trên máy với nhánh trực tuyến |

Nếu sửa file khác, thay tên file trong lệnh `git add`. Có thể chọn nhiều file:

```bash
git add index.html style.css script.js
```

Sau lần push đầu tiên có `-u`, những lần tiếp theo trên cùng nhánh chỉ cần:

```bash
git push
```

## 6. Tạo pull request và gộp vào project chung

Sau khi push:

1. Mở repository trên GitHub.
2. Chọn **Compare & pull request**, hoặc **Pull requests → New pull request**.
3. Chọn **base: main**, **compare: nhánh của bạn**.
4. Nhập tiêu đề và mô tả nội dung đã sửa.
5. Chọn **Create pull request**.
6. Nhờ thành viên khác kiểm tra và review.
7. Người có quyền chọn **Merge pull request** khi thay đổi đã đạt yêu cầu.

Nếu cần sửa thêm cho PR đang mở, tiếp tục sửa file trên cùng nhánh, commit và push. PR sẽ tự cập nhật.

Sau khi merge, lấy phiên bản chung mới nhất về máy:

```bash
git switch main
git pull --ff-only origin main
```

## 7. Xử lý lỗi thường gặp

| Thông báo | Cách xử lý |
| --- | --- |
| `not a git repository` | Đi vào đúng thư mục project bằng `cd` |
| `No such file or directory` | Kiểm tra đường dẫn và đặt trong dấu ngoặc kép nếu có khoảng trắng |
| `nothing to commit, working tree clean` | Chưa có thay đổi mới; kiểm tra đã sửa và lưu đúng file chưa |
| `Everything up-to-date` | Không có commit mới cần đẩy lên GitHub |
| `remote origin already exists` | Kiểm tra bằng `git remote -v`; dùng `git remote set-url` nếu địa chỉ sai |
| `a branch named ... already exists` | Dùng `git switch ten-nhanh` để tiếp tục nhánh cũ, hoặc tạo tên nhánh mới |
| `syntax error near unexpected token '('` | Đã nhập dòng kết quả hoặc URL có định dạng Markdown; chỉ nhập lệnh và URL thuần |
| `Permission denied` hoặc lỗi 403 | Kiểm tra tài khoản đang đăng nhập và đã chấp nhận lời mời Collaborator chưa |

Nếu push bị từ chối hoặc xuất hiện xung đột, đọc thông báo để xử lý; không dùng `git push --force` khi chưa hiểu ảnh hưởng đến công việc chung.

## 8. Minh chứng làm việc nhóm

Mỗi thành viên dùng tài khoản riêng và lưu:

- Link commit thể hiện thay đổi của mình.
- Link pull request.
- Review của thành viên khác.
- Ảnh pull request có trạng thái **Merged**.

Ghi các link vào `MINH-CHUNG-NHOM.md`. Những bằng chứng này thể hiện từng người đã đóng góp vào cùng repository.