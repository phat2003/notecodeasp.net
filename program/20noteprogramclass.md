
_builder.Services.AddDbContext_<`ApplicationDbContext(nameclass lấy từ folder data)`>(
    options => options.UseSqlServer(
        builder.Configuration.GetConnectionString(_"DefaultConnection(lấy connection string từ file appsettings.json)"_)
        ));
        