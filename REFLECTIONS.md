# Reflections — G13 costctl

1. Multi-account:
Để chạy costctl trên hàng trăm tài khoản, mình sẽ đổi CLI để lặp qua danh sách tài khoản (từ file config/profile). Cốt lõi là dùng sts:AssumeRole lấy quyền cross-account và tạo boto3 session riêng cho mỗi tài khoản đích. Data xuất ra CSV/JSON theo từng account rồi mới gộp báo cáo. Ngoài ra, bắt buộc phải thêm cơ chế bắt lỗi và retry/backoff cho từng account để tránh dính rate limit của AWS.

2. AI assistance:
AI hỗ trợ khoảng 70% code ban đầu, nhưng mình phải tự "nhúng tay" sửa nhiều để pass test và đúng spec. Cụ thể, mình chủ động code lại các đoạn AI xử lý kém như: format output, AWS exception handling, gộp tag S3, và luồng confirm trước khi terminate. Đặc biệt khi test với moto, AI hay đoán sai mock data nên mình phải tự debug và nắn lại input/output liên tục thì bộ test mới xanh.
