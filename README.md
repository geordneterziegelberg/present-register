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
    var identityConnectionString = builder.Configuration.GetConnectionString("IdentityConnection") ?? throw new InvalidOperationException("Connection string                     'DefaultConnection' not found.");
    var registerConnectionString = builder.Configuration.GetConnectionString("RegisterConnection") ?? throw new InvalidOperationException("Connection string                   'DefaultConnection' not found.");
    var serverVersion = new MySqlServerVersion(new Version(8,0,36));
    builder.Services.AddDbContext<ApplicationDbContext>(options =>
        options.UseMySql(identityConnectionString, serverVersion));
    builder.Services.AddDbContext<AppDbContext>(options =>
        options.UseMySql(presentelConnectionString, serverVersion));`
add connection strings to appsettings.json
   `"ConnectionStrings": {
    "IdentityConnection": "server=localhost;user=<user>;password=<password>;database=Identity",
    "RegisterConnection": "server=localhost;user=<user>;password=<password>;database=Register"}`
create Model Register.cs
   `namespace present_register;
    public class Register
    {
    public int ID {get;set;}
    public string Title {get;set;} = "";
    }`
create appDbContext.cs file in folder Data
   `using Microsoft.EntityFrameworkCore;
    namespace present_register.Data;
    public class AppDbContext : DbContext
    {
    public DbSet<Register> Register { get; set; }
    public AppDbContext(DbContextOptions<AppDbContext> options)
        : base(options) {}}`

