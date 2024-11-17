@if (TempData["Sucess"] != null)
{
    <h2>@TempData["Sucess"]</h2>
}

_TempData_ được truyền vào với điều kiện khác null là hiển thị ra thẻ tiêu đề h2 nhưng vốn dĩ _TempData_ được truyền vào giá `Category Delete sucessfully` nên không thể nào có chuyện nó nul được
cho nên `Category Delete sucessfully` sẽ được hiển thị khi được chuyển hướng từ action chứa _TempData_ đến View được truyền vào _TempData_.
và khi làm mới lại trang View đó thì _TempData_ sẽ biến mất.