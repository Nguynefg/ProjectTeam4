# Hướng dẫn dùng chung project GitHub

Git lưu lịch sử thay đổi trên máy; GitHub lưu repository trực tuyến để nhóm chia sẻ code và review. Repository public cho mọi người xem, nhưng chỉ người được cấp quyền mới đẩy thay đổi trực tiếp. Người ngoài có thể đóng góp bằng fork và pull request.

## 1. Chuẩn bị

Mỗi người tạo tài khoản GitHub riêng và cài Git từ https://git-scm.com/downloads. Mở terminal trong thư mục project. Chạy các lệnh sau và thay tên/email bằng thông tin của chính mình; nên dùng email đã liên kết với GitHub hoặc email noreply do GitHub cung cấp:

```sh
git config --global user.name "Ten cua ban"
git config --global user.email "email-cua-ban"
```

## 2. Trưởng nhóm tạo repository

Trên GitHub chọn **New repository**, đặt tên `project-nhom-github`, chọn Public hoặc Private. Khi đẩy project có sẵn, để repository trống: không thêm README, .gitignore hoặc license trên GitHub.

Project mẫu đã được khởi tạo Git và có commit ban đầu. Trong thư mục project chạy (thay `TEN-TAI-KHOAN`):

```sh
git remote add origin https://github.com/TEN-TAI-KHOAN/project-nhom-github.git
git push -u origin main
```

Nếu tự làm project mới chưa có Git, chạy `git init -b main`, `git add .`, rồi `git commit -m "Tao project ban dau"` trước khi thêm remote. Khi Git yêu cầu xác thực, dùng đăng nhập qua trình duyệt/credential manager hoặc token; mật khẩu tài khoản GitHub không dùng cho thao tác Git qua HTTPS.

## 3. Cho cả nhóm quyền đóng góp

Chủ repository vào **Settings → Collaborators → Add people**, tìm username từng thành viên và gửi lời mời. Từng người chấp nhận lời mời trong GitHub/thông báo/email. Không chia sẻ tài khoản hoặc token giữa các thành viên.

Tài liệu chính thức: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository

## 4. Thành viên lấy project và tạo nhánh

Ví dụ dưới đây dành cho thành viên A; B và C thay tên nhánh theo công việc:

```sh
git clone https://github.com/TEN-TAI-KHOAN/project-nhom-github.git
cd project-nhom-github
git switch -c feature/a-noi-dung
```

Sửa `index.html`, thay tên và mô tả mẫu. Mở trang để kiểm tra, rồi lưu thay đổi:

```sh
git status
git add index.html
git commit -m "Them ten va mo ta nhom"
git push -u origin feature/a-noi-dung
```

B dùng nhánh `feature/b-giao-dien`, sửa và add `style.css`. C dùng nhánh `feature/c-loi-chao`, sửa và add `script.js`. Với mỗi công việc mới, cập nhật main rồi tạo nhánh mới.

## 5. Tạo pull request, review và merge

Trên repository GitHub chọn **Pull requests → New pull request**. Chọn base `main`, compare là nhánh của mình. Ghi rõ đã sửa gì và đã kiểm tra thế nào, rồi tạo pull request. Thành viên khác đọc **Files changed**, gửi nhận xét hoặc review. Người có quyền merge chọn **Merge pull request** sau khi kiểm tra đạt.

Ví dụ mô tả PR của A:

> Thêm tên và nhiệm vụ của các thành viên vào trang giới thiệu. Đã mở index.html, kiểm tra danh sách hiển thị và nút chào hoạt động.

Tài liệu chính thức: https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-a-pull-request

## 6. Lấy bản chung mới nhất

Sau khi PR được merge, mỗi thành viên đảm bảo đã commit hoặc cất thay đổi đang làm trước khi chuyển nhánh:

```sh
git switch main
git pull --ff-only origin main
git switch -c feature/cong-viec-tiep-theo
```

Nếu có xung đột trên nhánh làm việc, lưu công việc rồi chạy `git fetch origin` và `git merge origin/main`. Mở file xung đột, thống nhất nội dung, bỏ các dấu `<<<<<<<`, `=======`, `>>>>>>>`, kiểm tra lại, `git add` các file đã sửa, commit và push. Có thể dùng `git merge --abort` để hủy lần merge đang xung đột.

## 7. Minh chứng nhóm dùng chung repository

Mỗi người hoàn thành PR bằng tài khoản thật. Ghi link repository, commit, PR và review vào `MINH-CHUNG-NHOM.md`. Chụp trạng thái PR đã merge và danh sách cộng tác viên sau khi mọi người chấp nhận lời mời. Chỉ có danh sách thành viên trong HTML không chứng minh được việc cộng tác.
