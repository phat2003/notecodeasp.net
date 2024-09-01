=======tạo valid kiểm tra data nhập vào database có đúng với ràng buộc không? cho dự án=============
if (ModelState.IsValid)
{
    
}

ở html phải thêm lệnh này thì mới có báo lỗi valid
<span asp-validation-for="Name" class="text-danger"></span>