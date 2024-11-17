if (obj.name != null && obj.name.Length >= 10)
{
    // Thêm lỗi vào ModelState nếu vượt quá 10 ký tự
    ModelState.AddModelError("Name", "Name cannot be longer than 100 characters.");
}