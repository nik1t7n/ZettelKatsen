Created: 202402020953
Tags: #api-basics 

---
### Reference

Here we are going to create our first controller to use it in the Main file! 

>[!info] Controllers
>Controllers in C# are kind of "managers". When client sends some request to our application, the controller governs the process how to handle it properly. In other words, controller is the one who accept a request and says what to do with it.

To create controller we must create a folder and file for it. I have created 
**Controllers** -> **WeatherForecastController.cs**. 
It is important to use semantical rules here.

Then inside of the file a always I created namespace and started to configure the controller itself.

==CONTROLLER==

I am going to provide full code here and then explain it step by step:

```cs
using Microsoft.AspNetCore.Mvc;

namespace DotnetAPI.Controllers;

[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
    private readonly string[] _summaries = new[]
    {
        "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
    };


    [HttpGet("", Name = "GetWeatherForecast")]
    public IEnumerable<WeatherForecast> GiveFiveDaysForecast()
    {
        var forecast = Enumerable.Range(1, 5).Select(index =>
        new WeatherForecast
        (
            DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
            Random.Shared.Next(-20, 55),
            _summaries[Random.Shared.Next(_summaries.Length)]
        ))
        .ToArray();
        return forecast;
    }
}

public record WeatherForecast(DateOnly Date, int TemperatureC, string? Summary)
{
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
}
```
Finally, this code represents a simple **ASP.NET Core MVC** controller!

By using **\[ApiController\]**  attribute we tells to program that our class is controller. Also it provides some additional functionality to it.

**\[Route("\[controller]")]** attribute points that all URL routes to the controller will start from the *"/WeatherForecast"*.

Likewise, we inherit the **ControllerBase** class to use some controller functionalities.

The **\[HttpGet("", Name = "GetWeatherForecast")]** attribute indicates that further method will be processing *HTTP GET* requests. "" (empty quotation marks) at the beginning tells that it will use default URL address (*/WeatherForecast*).

Rest code is just logic of random weather forecast so I will not analyze it.

==MAIN FILE==

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}
else
{
    app.UseHttpsRedirection();
}

app.MapControllers();

app.Run();
```
Here the most important features to our controller are:

* **builder.Services.AddControllers();** - add all controllers to the main
* app.MapControllers(); - map them to use it

Likewise, the **Swagger** provides GUI for the testing and running API. ^bc3559

---
### Zero-Links

1. 

-------
### Links

1. 