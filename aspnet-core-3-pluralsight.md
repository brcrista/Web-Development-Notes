# ASP.NET Core 3.x Pluralsight course

Course: <https://app.pluralsight.com/library/courses/understanding-aspdotnet-core-3x/table-of-contents>
Project code: <https://github.com/brcrista/Globomantics>

## What did I learn?
* The project type in Visual Studio (the icon next to the project name) is determined by the value of the `Sdk` attribute in the `<Project>` element.
* ASP.NET 3 can no longer be used with .NET Framework.  It can only be used with .NET Core.
* Configuration vs. Convention
    - The appsettings.json is a little of both.  It's the default settings file, but there's an option to change it.
    - The Startup class is pure convention.  There's no statically type-checked interface here.
    - You can actually have separate `Configure()` and `ConfigureServices()` methods for each environment (development, staging, and production).
    - Convention: the `wwwroot` directory is where static files live.
    - Convention: when making a strongly-typed settings object, you need to have a property with the same name as the property in the appsettings.json JSON object.
    - Convention: MVC looks for ViewComponents in a folder with the name "ViewComponents"
    - Convention: in an API controller, you can prefix method names with "Get" or "Post" and they will respond to the corresponding verbs.
* "Services" is a dependency injection term.  Services live in a "container," meaning an "inversion of control container."
* Service lifetimes
    - Transient: new instance every time the object is asked for
    - Scoped: new instance for each request
    - Singleton: one instance for the lifetime of the application
* `AddControllersWithViews()` adds full MVC to the application (without Razor pages).  It replaces `AddMvc()` from ASP.NET Core 2.
    - If it's just an API application, you just need `AddControllers()`
    - Also, routing has become its own middleware that you add with `UseRouting()`.  Previously, this was part of MVC.
    - An ASP.NET Core app can support MVC endpoints, Razor pages, and SignalR endpoints all side-by-side at different endpoints.
* Paths don't need to have anything to do with physical resources.  The app really just reads the paths and decides what to do with them.
    - In fact, you can even just call `MapGet()` in `UseEndpoints()` to call an arbitrary function based on a path.  No controllers needed!
* The order of middleware is important!  For example, when you add authentication, you should do that early on.
* If you look at the launch profiles in VS, you'll see that you can run the app with IIS Express (the default), or you can just run it as a command-line app.
    - You can run it as a command-line app because very ASP.NET Core app has an embedded web server called Kestrel.
    - These launch profiles are saved in launchSettings.json.
* Why rely on a 3rd-party CDN?  The browser may have already cached the file from another site using the same CDN.
* Controller actions: The convention with ASP.NET Core 3 is to return `IActionResult`.
* Razor pages offer an alternative to MVC.  You trade separation of concerns for simplicity.  The "views" become completely self-contained, encapsulating the business logic and routing.  They become known as "pages" instead of "views."
    - Razor pages are modeled after the way static files are served by path.  The route for the page is simply its path under the `Pages/` directory, minus the `.cshtml` extension.
    - To be honest, I don't like Razor pages that much, because it doesn't give you much room to grow.
    - I also just don't like Razor / server-side rendering in ASP.NET either.  It's very convention-based, with the complicated folder hierarchy and special file names in the `Views/` or `Pages/` directory.
    - I don't like the complexity added by the C#-spinoff syntax of Razor.  And, the VS support seems a little half-baked too.  I forgot to include a @using and then I couldn't put a breakpoint in my code.  I didn't get any error or anything, though.
    - Client-side rendering just seems more flexible.  For example, in the case where I wanted to style an element differently based on the number of conference attendees, you would have to refresh the page to get an update doing it statically.  Also, it takes load off your server to have clients do their own rendering.
    - That said, you don't have to choose either-or.  You can use Razor Pages and MVC side-by-side.
* Blazor lets you write single-page applications with .NET.
    - Normally, all of the client-side functionality of a single-page app would have to be in JavaScript.  With Blazor, you can use .NET, using the same Razor syntax you use for server-side rendering in Razor pages.
    - There are two "hosting models" to choose from.
        - In the first, a Mono interpreter compiled to WebAssembly is sent down along with the .NET assemblies to run on the client side.
        - In the second, all of the rendering is done server-side, and then chunks of HTML are sent down over a SignalR connection.
* For REST APIs, the action name shouldn't be included in the route (e.g., "Index").  Instead, use HTTP verbs.
* In fact, for REST APIs controllers (i.e. using `ApiControllerAttribute`), you can't use a routing table.
* `ApiControllerAttribute`
    - Model validation for `POST` and `PUT` requests.  You don't have to check `ModelState.IsValid` and return 400 -- that will happen automatically.
    - Binding source inference (`FromBodyAttribute`, `FromFormAttribute`, `FromRouteAttribute`, `FromQueryAttribute`, etc.)
* gRPC
* .NET Core
    - The CoreFX library is for types that are useful in any application.  Types that are specific to Web apps or desktop apps go in other libraries, such as ASP.NET Core.
    - .NET Core and .NET Framework are eventually going to be replaced by the next major version of .NET Core, which will just be called .NET.  (I remember reading about this at PyCon about a year ago.)
    - The .NET runtime is hosted by the dotnet CLI.  It used to be hosted by Windows itself.
    - An assembly compiled for .NET Core won't run on .NET Framework.  But, you can target multiple frameworks, including other frameworks like Unity and Xamarin, through .NET Standard.  The assembly will have to be recompiled for the other frameworks.
* Kestrel
    - When deploying with IIS, Kestrel is still running.  IIS just sends the requests to Kestrel.
    - `ConfigureWebHostDefaults()` sets up Kestrel with some default settings.  You can override them with `UseKestrel()`.
    - Kestrel is lightweight, and doesn't do much more than handle requests.  In production, you probably want something with more features that can handle things such as caching, compression, and process monitoring.
    - **Process monitoring** means restarting the app if it crashes.
* When deploying a .NET Core app, you have the option to make it **framework-dependent** or **self-contained**.
    - **Framework-dependent** means the machine you're deploying to needs to have the right version of the .NET Core runtime pre-installed.  But, you can deploy to any machine and any OS that has that runtime.
    - **Self-contained** means the whole .NET runtime, libraries, and a native executable are produced for a target OS and platform.  But, you need to target a specific OS and platform up front, and it takes up a lot more disk space.
* IIS
    - IIS and your application will run in the same process.
    - On Windows, you configure IIS with a web.config.
    - You need an additional package called `AspNetCoreModule`.  It facilitates communication between IIS and Kestrel.
* nginx
    - By default, process monitoring is turned off.
