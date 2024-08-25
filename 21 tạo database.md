cài nuget package entityframeworkcore.tools và chạy các lệnh sau
_add-migration `tên của class database được render từ file cấu trúc database ở folder models(đặt gì cũng được)`_ dòng này sẽ tạo ra file database trong folder migrations theo cấu trúc database viết bằng c#.

_update-database_ dòng này sẽ update class database lên sqlserver