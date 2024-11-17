_@RenderBody()_ : load các file html trong view/home
=====================================
_@model `nameModels`_ chỗ nào cần sử dụng tới Models nào thì add Models đó vào.
============================================
=======validation ở phía client==============
@section Scripts 
{
    <partial name ="_ValidationScriptsPartial" />
}
`_ValidationScriptsPartial` là một file nằm trong views/shared được tạo sẵn từ asp.net khi tạo project.
lệnh này sẽ giúp khi nhập dữ liệu không đúng với ràng buộc sẽ không báo lỗi về vscode mà sẽ chỉ báo lỗi ở web
================================================