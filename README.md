# PDFcoHttpClient
The correct way to use HttpClient in .NET applications


Install via NuGet
-----------------
To install PDFcoHttpClient, run the following command in the Package Manager Console:

```
PM> Install-Package PDFcoHttpClient
```

You can also view the [package page](http://www.nuget.org/packages/PDFcoHttpClient/) on NuGet.


Usage:
-----------------
Once you've got the HttpClientFactory defined, up next is registering the factory with your IoC container of choice.

```csharp
 ioc.For<IHttpClientFactory>() 
      .Singleton() 
      .Add<HttpClientFactory>();
```

Then declare your dependency using constructor injection and use the HttpClientFactory. 

```csharp
namespace Web.Controllers
{
    public class CustomerController : Controller
    {
        private readonly IHttpClientFactory _httpClientFactory;
        public CustomerController(IHttpClientFactory httpClientFactory)
        {
            _httpClientFactory = httpClientFactory;
        }

        public async Task<IActionResult> GetById(int id)
        {
            var httpClient = _httpClientFactory.GetOrCreate(new Uri("http://pdfco.ir/customers"));
            var response = await httpClient.GetAsync(...);
            ... 
        }
```




