# present-register
create new project with lower dotnet 7 and "individual user identification"
   dotnet new mvc --framework net7.0 --auth Individual 
<delete existing migration files 0000..00_Create.../>
add nuget package Pomelo.EntityFrameworkCore.MySql
remove nuget package sqlite
create mysql connection in mysql workbench, if trouble:
  > ALTER USER 'root'@'localhost' IDENTIFIED BY '<password>';
add in Program.cs
  > // DB Service
    builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseMySql(identityConnectionString, serverVersion));
    builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseMySql(presentelConnectionString, serverVersion));
