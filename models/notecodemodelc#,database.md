_[Key]_ //set trường nào đó làm khoá chính trong database

_[Required]_ //muốn trường nào đó không được phép null(rỗng) thì thêm dòng này

_[Required(ErrorMessage = "`Mời bạn nhập username`")]_ :
_ErrorMessage_ để hiển thị thông báo lỗi khi bỏ trống trường yêu cầu not null.

_[Display(Name = "`Display Order`")]_ Tùy chỉnh hiển thị và giá trị biến, ở đây đang là tuỳ chỉnh giá trị Name của DisplayOrder thay vì hiển thị DisplayOrder thì hiển thị Display Order(ở đây thật ra chỉ thêm dấu cách chứ muốn ghi gì thì ghi).

[_Range_(`1`, `100`, 
        _ErrorMessage_ = "Value for {0} must be between {1} and {2}.")]
_Range_ : giới hạn độ dài ký tự(chữ,...) của trường được nhập vào (ở đây đang là 1-100)