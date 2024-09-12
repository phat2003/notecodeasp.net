=====tạo method action trả về views======
_public IActionResult `Index()`_
{
    _return `View();`_
}
nguyên câu lệnh trên hiểu ngắn gọn là `url:home/index` `home` là `controller` còn `index` là `action`
============================================================================
======tạo 1 biến đọc để đọc dữ liệu đang được lưu trữ trong database=======
private readonly `ApplicationDbContext` _db;//biến này chỉ được đọc(không được ghi hay làm gì khác).
public CategoryController(`ApplicationDbContext` `db`)
{
    _db = db;
}
`ApplicationDbContext` : là tên của file dùng để chuyển đổi Models thành bảng database thông qua add-migration và update database lên sql server.
`db` : là tên bất kỳ được đặt làm param cho `ApplicationDbContext`
truyền vào param db khai báo bằng `ApplicationDbContext` giống biến _readonly_ và gọi `_db` = `db`; ở trong đối tượng `CategoryController` để có thể sử dụng đối tượng `CategoryController` để đọc dữ liệu trong database ở bất cứ đâu thông qua biến `_db` khi được gọi tới.
đọc dữ liệu đã được thêm vào database như là id,sản phẩm,số lượng,....
===========================================================================
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
====method action Create post dùng để post data được tạo khi nhập và nhấn action create=========
//post
[HttpPost]
[ValidateAntiForgeryToken]//lệnh này dùng để chống giả mạo về method này
_public IActionResult_ `Create`(`Models` `tên biến bất kỳ tự đặt`)
{
    `_db`.`Data`.Add(`tên biến bất kỳ tự đặt`);
    `_db`.SaveChanges();
    _return RedirectToAction_("`index`");
}

`_db`.`Data`._Add_(`tên biến bất kỳ tự đặt`); : thêm param của method vào database.
`_db`._SaveChanges_(); : lưu thay đổi sau khi đã đưa param lên database.
_return RedirectToAction_("`index`"); : hành động trả về action khác (ví dụ ở đây đang là hành động trả về action index)
=====================================================
=======tạo valid kiểm tra data nhập vào database có đúng với ràng buộc không? cho dự án=============
_public IActionResult_ `Create`(`Category` `obj`)
{
    _if (ModelState.IsValid)_
    {
        `_db`.`Categories`._Add_(`obj`);
        `_db`._SaveChanges_();
        _return RedirectToAction_("`index`");
    }
    _return View_(`obj`);
}

_if (ModelState.IsValid)_ {} :đây chính là lệnh tạo ra valid khi nhập sai ràng buộc.

ở html phải thêm lệnh này thì mới có báo lỗi valid: 
<span asp-validation-for="Name" class="text-danger"></span>

============================================================
=====tuỳ chỉnh kiểm tra valid==========
public IActionResult Edit(Category obj)
{
    if (`obj`.`Name` == `obj`.`DisplayOrder`._ToString_())
    {
        _ModelState.AddModelError_("`name`", "The Name must not same displayorder");
    }
    if (ModelState.IsValid)
    {
        _db.Categories.Update(obj);
        _db.SaveChanges();
        return RedirectToAction("index");
    }
    return View(obj);
}
_ModelState.AddModelError_("Tên của cột trong table", "này là thông báo lỗi tuỳ chỉnh(muốn ghi gì thì ghi)"); : thêm lỗi tuỳ chỉnh vào cột bất kỳ trong model.
ở đây đang đặt điều kiện là nếu name = DisplayOrder cả 2 có giá trị trùng nhau thì thực thi lệnh thêm lỗi bên trong if.

ở html thêm lệnh này:
<div asp-validation-summary=All></div>

================================================
========action Edit===========
_public IActionResult_ `Edit`(`int?` `id`)
{
    if (`id`==`null` || `id`==`0`)
    {
        _return NotFound();_
    }
    _var_ `categoryfromDb` = `_db.Categories`._Find(`id`)_;
    //var categoryfromDbFirst = _db.Categories.FirstOrDefault(u=>u.Id==id);
    //var categoryfromDbsingle = _db.Categories.SingleOrDefault(u => u.Id == id);
    _if_ (`categoryfromDb` == `null`)
    {
        _return NotFound();_
    }
    _return View(`categoryfromDb`);_
}

truyền vào 1 param `id` kiểu int vào action edit để dùng nó lấy dữ liệu từ database ra để edit thông qua cột `Id` trong database
điều kiện id = null hoặc = 0 thì trả về notFound();
tạo 1 biến var và truyền biến id vào Find() để tìm kiếm dựa trên giá trị của id
-
_FirstOrDefault_: trả về phần tử đầu tiên của một tập hợp dữ liệu thoả mãn điều kiện được cung cấp, hoặc giá trị mặc định của kiểu dữ liệu đó nếu không có phần tử nào phù hợp. Đối với kiểu tham chiếu như lớp hoặc chuỗi (_string_), giá trị mặc định là `null`. Đối với kiểu giá trị (value types) như _int_, giá trị mặc định là `0`.
truyền vào hàm ẩn danh `u=>u.Id==id` : `u` sẽ bị ép trỏ tới cột `Id` trong database để nhận data từ cột `Id`, nghĩa là `u` bây giờ chính là giá trị của cột `Id` mà `u` == `id` tương đương `Id` == `id`.
_FirstOrDefault_ :thường được dùng để xử lý những dữ liệu không tồn tại trong hệ thống
-
`categoryfromDb` biến này được tạo ra để lấy data từ Database ra ngoài
nếu giá trị là `id` mà `null`, cũng tức là không tìm thấy giá trị nào trong database có `id` = `Id` trong database(cũng tức là nói `categoryfromDb` bị `null`) thì trả về _notFound();_

_return View(`categoryfromDb`);_ : nếu không có cái nào đáp ứng 2 điều kiện trên thì trả về View với giá trị `categoryfromDb` được truyền vào và hiển thị data lấy được từ database thông qua `categoryfromDb`.
-

//post
[HttpPost]
[ValidateAntiForgeryToken]//lệnh này dùng để chống giả mạo về method này
_public IActionResult_ `Edit`(`Category` `obj`)
{
    if (`obj`.`Name` == `obj`.`DisplayOrder`.ToString())
    {
        ModelState.AddModelError("`name`", "The Name must not same displayorder");
    }
    if (ModelState.IsValid)
    {
        _db.Categories._Update_(obj);
        _db.SaveChanges();
        return RedirectToAction("`index`");
    }
    return View(`obj`);
}
_db.Categories._Update_(obj); : lưu ý chỗ này phải để là Update để cập nhật các thay đổi khi edit dữ liệu lên database.

ở html nên thêm vào asp-action="Edit" ở thẻ chứa method="post" để trỏ đúng tới action Edit
<form method="post" asp-action="Edit">
</form>

=============================================================
=========method delete========
public IActionResult Delete(int? id)
{
    if (id == null || id == 0)
    {
        return NotFound();
    }
    var categoryfromDb = _db.Categories.Find(id);
    //var categoryfromDbFirst = _db.Categories.FirstOrDefault(u=>u.Id==id);
    //var categoryfromDbsingle = _db.Categories.SingleOrDefault(u => u.Id == id);
    if (categoryfromDb == null)
    {
        return NotFound();
    }
    return View(categoryfromDb);
}

//post
[HttpPost]
[ValidateAntiForgeryToken]//lệnh này dùng để chống giả mạo về method này
public IActionResult DeletePost(int? id)
{
    var obj = _db.Categories.Find(id);
    //var categoryfromDbFirst = _db.Categories.FirstOrDefault(u=>u.Id==id);
    //var categoryfromDbsingle = _db.Categories.SingleOrDefault(u => u.Id == id);
    if (ModelState.IsValid)
    {
        _db.Categories.Remove(obj);
        _db.SaveChanges();
        return RedirectToAction("index");
    }
    return View(obj);
}
=======================================================
=====action Delete======
trong Controller:

public IActionResult Delete(int? id)
{
    if (id == null || id == 0)
    {
        return NotFound();
    }
    var categoryfromDb = _db.Categories.Find(id);
    //var categoryfromDbFirst = _db.Categories.FirstOrDefault(u=>u.Id==id);
    //var categoryfromDbsingle = _db.Categories.SingleOrDefault(u => u.Id == id);
    if (categoryfromDb == null)
    {
        return NotFound();
    }
    return View(categoryfromDb);
}
Giải thích code:
Method Get này của Delete y chang Edit


//post
[HttpPost]
[ValidateAntiForgeryToken]//lệnh này dùng để chống giả mạo về method này
public IActionResult `DeletePost`(_int?_ `id`)
{
    var `obj` = _db.Categories.Find(`id`);
    //var categoryfromDbFirst = _db.Categories.FirstOrDefault(u=>u.Id==id);
    //var categoryfromDbsingle = _db.Categories.SingleOrDefault(u => u.Id == id);
    if (`obj` == `null`)
    {
        return NotFound();
    }
    else
    {
        _db.Categories._Remove_(obj);
        _db.SaveChanges();
        return RedirectToAction("index");
    }
    return View(obj);
}
Giải thích code:
method Post của `Delete` được lấy `id` được truyền vào làm param
biến obj được khởi tạo để tìm `id` trong database Categories.
dùng if-else làm điều kiện để lọc ra obj bị null. Nếu id bị null nghĩa là biến tìm id là obj cũng bị null thì trả về NotFound, còn nếu id tìm được có giá trị thì sẽ xoá obj chứa id đó.

trong Views:
thêm _disabled_ vào thẻ html nào mà chúng ta không muốn thẻ đó hoạt động.
thêm <input asp-for="Id" hidden/> ở sau thẻ mở <form> để View nhận dữ liệu của trường Id và ẩn nó để không hiện ra field nhập Id do id đã được nhận khi nhấn nút Delete của vòng lặp tương ứng với data của Id đó rồi.
nếu bình thưởng thẻ input mà không có hidden.
=====================================================
========temp Data===========
TempData[] là một tính năng được sử dụng để lưu trữ dữ liệu tạm thời giữa các yêu cầu HTTP
Dữ liệu trong TempData chỉ tồn tại trong thời gian ngắn và sẽ bị xóa sau khi được truy xuất (hoặc hết phiên làm việc).
_TempData_["Sucess"] = "`Category Delete sucessfully`";
ở đây chúng ta sẽ dùng nó để hiển thị ra giá trị được truyền vào trong _TempData_ lên View khi được gọi tới action chứa nó với điều kiện là _TempData_ phải được truyền vào vị trí mà chúng ta cần hiển thị _TempData_ lên View.

Ở View:
_TempData_ được truyền vào với điều kiện khác null là hiển thị ra thẻ tiêu đề h2 nhưng vốn dĩ _TempData_ được truyền vào giá `Category Delete sucessfully` nên không thể nào có chuyện nó nul được
cho nên `Category Delete sucessfully` sẽ được hiển thị khi được chuyển hướng từ action chứa _TempData_ đến View được truyền vào _TempData_.
và khi làm mới lại trang View đó thì _TempData_ sẽ biến mất.
@if (TempData["Sucess"] != null)
{
    <h2>@TempData["Sucess"]</h2>
}
===========================================================