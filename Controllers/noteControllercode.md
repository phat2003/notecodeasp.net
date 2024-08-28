=====method action trả về views======
_public IActionResult `Index()`_
{
    _return `View();`_
}
nguyên câu lệnh trên hiểu ngắn gọn là `url:home/index` `home` là `controller` còn `index` là `action`
===============================
======method action đưa database lên html=========
_public IActionResult `Index`()_
{
    _IEnumerable_<`Models`> objCategoryList = `_db`.`tên của table đặt trong lệnh Dbset ở class trong folder Data`._ToList_();
    _return View_(`tên của table đặt trong lệnh Dbset ở class trong folder Data`);
}
// biến IEnumerable là biến dùng được tạo ra với mục đích để hiển thị data của Models lên html
// ở đây trả về View truyền vào biến `IEnumerable` được đặt tên là objCategoryList
//khi muốn hiển thị data của Models lên trang html nào thì phải thêm @model IEnumerable<`Model`> vào file html cần hiển thị giao diện database
========================================
====method post create dùng để post data được tạo khi nhập và nhấn action create=========
//post
[HttpPost]
[ValidateAntiForgeryToken]//lệnh này dùng để chống giả mạo về method này
_public IActionResult_ `Create`(`Models` `tên biến bất kỳ tự đặt`)
{
    `_db`.`Data`.Add(`tên biến bất kỳ tự đặt`);
    `_db`.SaveChanges();
    return RedirectToAction("`index`");
}
`_db`.`Data`.Add(`tên biến bất kỳ tự đặt`); : thêm param của method vào database.
`_db`.SaveChanges(); : lưu thay đổi sau khi đã đưa param lên database.
return RedirectToAction("`index`"); : hành động trả về action khác (ví dụ ở đây đang là hành động trả về action index)
=====================================================
