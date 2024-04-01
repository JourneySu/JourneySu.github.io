+++
author = "Hailey"
title = "AspNetCoreRegisterDI"
date = "2024-02-27"
description = "…"
tags = [
    "",
    "",
]
categories = [
    "",
    "",
]
series = [""]
aliases = ["migrate-from-jekyl"]
+++



### 新增一個ASP.NET CORE MVC(.Net 6)專案
* 使用VS新增此專案，起始註冊內容會如下  
  說明：  
  1. `var builder = WebApplication.CreateBuilder(args);`  
    會先使用CreateBuilder建立一個WebApplicationBuilder，再使用該builder進行其他動作(待學習有哪些)
  2. `var app = builder.Build();`
    使用.Build()方法，將builder建置成一個WebApplication，再使用該app進行其他動作(待學習有哪些)



```c# {.line-numbers}
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllersWithViews();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
    // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

app.Run();
```

### 設定Json檔
* 設定Json檔使用的builder會是<font color="	#02C874">ConfigurationBuilder</font>

```c#
    var IConfig = new ConfigurationBuilder();
    var settingName = "appsettings";
    var config = IConfig
        .AddJsonFile(path: $"appsettings.json", optional: true)
        .AddJsonFile(path: "DisplaySettings.json", optional: true)
        .AddEnvironmentVariables()
        .Build();
```





### 大型專案註冊作法建議

* 使用Extension方式註冊  
 1. 於整個專案的起始Program.cs：

```c#
var builder = WebApplication.CreateBuilder(args);
// ...中間省略
builder.Services.AddLibs();
// ...後面省略
```
  2. 於Lib專案下新增DIHelper.cs檔，將與Lib專案有關的註冊都放在這，會較clean
```c#
   public static class DIHelper
    {
        public static IServiceCollection AddLibs(this IServiceCollection services)
        {
            services.AddScoped<IConfigHelper, ConfigHelper>();
            services.AddScoped<IProxyBiz, ProxyBiz>();
            services.AddScoped<IRobinHelper, RobinHelper>();
            services.AddScoped<ILogHelper, LogHelper>();
            return services;
        }
    }

```












(Ps)學習方式：查看現有專案有註冊的，一一去了解用途
