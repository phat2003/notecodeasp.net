_public class `nameclass` : DbContext_
{
    public `nameclass`(DbContextOptions<`nameclass`> options) : base(options) //đây là làm tạo
    {

    }
    public DbSet<`file class cấu trúc database trong thư mục models`> `tên tự đặt cho bảng database khi xài lệnh add-migration ApplicationDbContext để tạo file database` { get; set; }
}

_public class `ApplicationDbContext` : DbContext_
{
    public `ApplicationDbContext`(DbContextOptions<`ApplicationDbContext`> options) : base(options)
    {

    }
    public DbSet<`Category`> `Categories` { get; set; }
}

_DbContext_ : đóng vai trò là cầu nối giữa cơ sở dữ liệu và ứng dụng của bạn
_public `nameclass(ở ví dụ trên là ApplicationDbContext)`_ : là 1 contructor được tạo ra từ class cùng tên nameclass dùng để gọi đối tượng đó khi cần thiết.
Tham số _options_ là một đối tượng chứa các tùy chọn cấu hình cho DbContext, chẳng hạn như chuỗi kết nối đến cơ sở dữ liệu, loại cơ sở dữ liệu (SQL Server, SQLite, v.v.), và các tùy chọn khác.
_base(options)_ gọi `constructor` của lớp cha _DbContext_ và truyền các tùy chọn này lên để _DbContext_ có thể cấu hình chính xác.
_DbSet<Category(name class cấu trúc database nằm trong thư mục models)>_ đại diện cho một bảng trong cơ sở dữ liệu, nơi Category là một lớp mô tả cấu trúc của bảng đó (các cột và kiểu dữ liệu của chúng).
`Categories` là một thuộc tính cho phép bạn truy cập và thao tác với dữ liệu trong bảng này thông qua đối tượng ApplicationDbContext. Bạn có thể dùng `Categories` để thực hiện các thao tác như thêm, cập nhật, xóa hoặc truy vấn dữ liệu từ bảng Category trong cơ sở dữ liệu.