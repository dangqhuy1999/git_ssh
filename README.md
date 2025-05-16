# git_ssh
git connect ssh permanent
Để kết nối SSH với GitHub vĩnh viễn (không phải nhập mật khẩu hay xác thực lại mỗi lần) khi push/pull code, bạn cần thực hiện các bước sau:

✅ 1. Kiểm tra SSH key đã có chưa
Chạy lệnh:

bash
Copy
Edit
ls ~/.ssh/id_ed25519.pub
Nếu file chưa tồn tại, tạo mới:

✅ 2. Tạo SSH key (nếu chưa có)
bash
Copy
Edit
ssh-keygen -t ed25519 -C "your_email@example.com"
Nhấn Enter liên tục để tạo key mặc định.

✅ 3. Thêm SSH key vào SSH agent
bash
Copy
Edit
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
✅ 4. Copy public key và thêm vào GitHub
bash
Copy
Edit
cat ~/.ssh/id_ed25519.pub
Sau đó:

Truy cập GitHub: https://github.com/settings/keys

Chọn "New SSH key"

Dán nội dung key vào, đặt tên (ví dụ: "Laptop Ubuntu") và lưu.

✅ 5. Kiểm tra kết nối SSH với GitHub
bash
Copy
Edit
ssh -T git@github.com
Kết quả nếu thành công:

rust
Copy
Edit
Hi dangqhuy1999! You've successfully authenticated...
✅ 6. Gán remote repo (nếu chưa làm)
bash
Copy
Edit
git remote add origin git@github.com:dangqhuy1999/supabase_rag_mcp.git
✅ 7. Push lần đầu
bash
Copy
Edit
git push -u origin main
Vậy là từ giờ về sau bạn sẽ không phải xác thực lại mỗi lần push/pull nữa ✅

Nếu cần kiểm tra danh sách các key đang hoạt động:

bash
Copy
Edit
ssh-add -l
Nếu đang dùng WSL hoặc server, đừng quên:

Kiểm tra SSH agent đang chạy: eval "$(ssh-agent -s)"

Thêm key vào config để tự dùng:

bash
Copy
Edit
# ~/.ssh/config
Host github.com
  User git
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
