======method action đưa database hiển thị lên html=========
Trong controllers
_public IActionResult `Index`()_
{
    _IEnumerable_<`Models`> objCategoryList = `_db`.`tên của table đặt trong lệnh Dbset ở class trong folder Data`._ToList_();
    _return View_(`tên của table đặt trong lệnh Dbset ở class trong folder Data`);
}
// biến IEnumerable là biến dùng được tạo ra với mục đích để hiển thị data của Models lên html
// ở đây trả về View truyền vào biến `IEnumerable` được đặt tên là objCategoryList
//khi muốn hiển thị data của Models lên trang html nào thì phải thêm @model IEnumerable<`Model`> vào file html cần hiển thị giao diện database

trong html phải nhúng vào các lệnh này để sử dụng vòng lặp đưa dữ liệu lên html và lặp các khối chứa từng data trong database:
@foreach (var item in Model)
{
        <div class="box-character">
            <img class="img-characters" src="https://www.w3schools.com/w3images/mountains.jpg" alt="image-character" />
            <div class="container-characters">
                <p class="name-characters"><b class="namechar">@item.name</b></p>
                <span>@item.role</span>
                <p>@item.team</p>
            </div>
        </div>
}