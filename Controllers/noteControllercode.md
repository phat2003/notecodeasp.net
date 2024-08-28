_public IActionResult `Index()`_
{
    _return `View();`_
}
nguyên câu lệnh trên hiểu ngắn gọn là `url:home/index` `home` là `controller` còn `index` là `action`

_public IActionResult `Privacy`()_
{
    _return View();_
}
ở đây là `url:home/privacy` `home` là `controller` còn `privacy` là `action`

_public IActionResult `Index`()_
{
    _IEnumerable_<`Models`> objCategoryList = `_db`.`Categories`._ToList_();
    _return View_(`objCategoryList`);
}
// biến IEnumerable là biến dùng được tạo ra với mục đích để hiển thị data của Models lên html
// ở đây trả về View truyền vào biến `IEnumerable` được đặt tên là objCategoryList
//khi muốn hiển thị data của Models lên trang html nào thì phải thêm @model IEnumerable<`Model`> vào file html cần hiển thị giao diện database