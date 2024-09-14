if (obj.name != null && obj.name.Length >= 10)
{
    // Thêm lỗi vào ModelState nếu vượt quá 100 ký tự
    ModelState.AddModelError("Name", "Name cannot be longer than 100 characters.");
}