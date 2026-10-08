# Bài 4: Lưu trữ dữ liệu với Docker Volume

## Các lệnh đã thực hiện

Tạo named volume có tên `easy-volume`:

```bash
docker volume create easy-volume
```

Kết quả:

```text
easy-volume
```

Kiểm tra danh sách volume trên máy:

```bash
docker volume ls
```

Kết quả:

```text
DRIVER    VOLUME NAME
local     easy-volume
```

Dùng container Alpine ghi dữ liệu vào tệp `/data/test.txt` trong volume:

```bash
docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"
```

Container kết thúc và tự động bị xóa do sử dụng tùy chọn `--rm`. Dữ liệu vẫn được lưu trong named volume `easy-volume`.

## Kiểm tra

Dùng một container Alpine khác để đọc lại tệp đã lưu:

```bash
docker run --rm -v easy-volume:/data alpine cat /data/test.txt
```

Kết quả:

```text
Luu tru du lieu Docker
```

Kết quả trên cho thấy dữ liệu không bị mất sau khi container đầu tiên dừng và bị xóa.
