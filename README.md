# present-register
create new project with lower dotnet 7 and "individual user identification"
   `dotnet new mvc --framework net7.0 --auth Individual`
delete existing migration files 0000..00_Create...
add nuget package Pomelo.EntityFrameworkCore.MySql
remove nuget package sqlite
create mysql connection in mysql workbench, if trouble:
   `ALTER USER 'root'@'localhost' IDENTIFIED BY '<password>';`
replace the sql DB Service in Program.cs:
   `// Add services to the container.
    var identityConnectionString = builder.Configuration.GetConnectionString("IdentityConnection") ?? throw new InvalidOperationException("Connection string    'DefaultConnection' not found.");
    var presentelConnectionString = builder.Configuration.GetConnectionString("PresentelConnection") ?? throw new InvalidOperationException("Connection string 'DefaultConnection' not found.");
    var serverVersion = new MySqlServerVersion(new Version(8,0,36));
    builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseMySql(identityConnectionString, serverVersion));
    builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseMySql(presentelConnectionString, serverVersion));`
