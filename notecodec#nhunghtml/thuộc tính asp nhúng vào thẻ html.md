=========tạo method action trả về views======
_asp-controller_="`Tên của Controller`" _asp-action_="`Tên của action`"
====================
======method action đưa database lên html=======
_@model_ `Tên của Models` : lưu ý ở file nào cần dùng tới Models cứ đụng tới model là add lệnh này vào trang html.

_asp-for_="`Tên của cột trong database`"
=======================================================
=====method action Create post dùng để post data được tạo khi nhập và nhấn action create=======
<label asp-for="Name">Name</label>
<input asp-for="Name" class="form-control"/>

thêm _asp-for_="`Name`" ở thẻ dùng để nhập giá trị cho cột trong database.
=================================================
=======tạo valid kiểm tra data nhập vào database có đúng với ràng buộc không? cho dự án==========
<span asp-validation-for="Cột trong database" class="text-danger"></span>

_asp-validation-for_="`Cột trong database`" : chỉ định một thẻ trong html được sử dụng để báo lỗi valid khi nhập sai thông tin ràng buộc
=========================================================
=======tuỳ chỉnh kiểm tra valid==========
<div asp-validation-summary=All></div>

_asp-validation-summary_=`All` : hiển thị toàn bộ thông báo lỗi valid khi có lỗi nhập không đúng ràng buộc

====================================================
=======validation ở phía client==============
@section Scripts 
{
    <partial name ="_ValidationScriptsPartial" />
}
`_ValidationScriptsPartial` là một file nằm trong views/shared được tạo sẵn từ asp.net khi tạo project.
lệnh này sẽ giúp khi nhập dữ liệu không đúng với ràng buộc sẽ không báo lỗi về vscode mà sẽ chỉ báo lỗi ở web
=====================================================
======action Edit========
ở html nên thêm vào asp-action="Edit" ở thẻ chứa method="post" để trỏ đúng tới action Edit
<form method="post" asp-action="Edit">
</form>

===================================================
=========
