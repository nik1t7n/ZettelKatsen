Created: 202402032040
Tags: #api-basics 

---
### Reference

Before we start, let's configure the [[LaunchSettings.json]] file.


>[!tip] CORS (Cross-Origin Resource Sharing)
>**CORS** is a mechanism that allows a web page in one domain to request some data from another domain, at the same time providing safety of the browser mechanism *Same-Origin Policy*.

By default browsers uses a policy of the *Same-Origin* which restricts a possibility of data requests between different domains. When we need to circumvent these restrictions the CORS configuration becomes necessary. 

There are some reasons why do wee need to configure CORS:

>[!tip] CORS is needed when...
>1. If our web-application located on different domains (frontend and API).
>2. If we do local development. During the local development web-server can work on one port (4200 or 3000) while backend-server works on another port (for example, 5000). Browsers consider this as a *cross-domain* request so we need CORS here too.


In the Main file we can configure CORS like:

```cs
builder.Services.AddCors((options) => 
    {
        options.AddPolicy("DevCors", (corsBuilder) => 
            {
                corsBuilder.WithOrigins("http://localhost:4200", "http://localhost:3000", "http://localhost:8000")
                    .AllowAnyMethod()
                    .AllowAnyHeader()
                    .AllowCredentials();
            });

        options.AddPolicy("ProdCors", (corsBuilder) => 
            {
                corsBuilder.WithOrigins("https://MyProductionSite.com")
                    .AllowAnyMethod()
                    .AllowAnyHeader()
                    .AllowCredentials();
            });
    });
```

**builder.Services.AddCors((options) => { ... });** - here we add CORS services to the app

**options.AddPolicy("DevCors", (corsBuilder) => { ... });** - here we configure CORS policy with the "DevCors" name. This policy allows requests from certain origins for development (for example, local development services with the 4200, 3000 and 8000 ports).
Likewise, it allows to commit any of HTTP methods, all of headers and credentials.

**options.AddPolicy("ProdCors", (corsBuilder) => { ... });** - here we configure CORS policy with the "ProdCors" name. This policy allows requests only from the production-domain. 

>[!info] Summing up
>Thus, this code adds two CORS policies: "DevCors" for development and "ProdCors" for production. After this configuration, these policies can be applied to specific routes or by the controller in your ASP.NET The core application for determining which requests from which sources will be accepted.

Let's activate our CORS:

```cs
if (app.Environment.IsDevelopment())
{
    app.UseCors("DevCors");
    app.UseSwagger();
    app.UseSwaggerUI();
}
else
{
    app.UseCors("ProdCors");
    app.UseHttpsRedirection();
}
```

I think here everything is pretty self-explanatory ^\_^

---
### Zero-Links

1. 

-------
### Links

1. 