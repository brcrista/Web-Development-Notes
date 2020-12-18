# ASP.NET Core

## Weirdness from default status codes

While you can just return object model types from your API controllers and hope for the best, I've found that the automatic HTTP responses ASP.NET comes up with sometimes isn't what I want.
In general, I think it's best to return `IActionResult` and take control of what you return.

### GET

* Returning `null` will return `204`, not `404`.
   - See https://weblog.west-wind.com/posts/2020/Feb/24/Null-API-Responses-and-HTTP-204-Results-in-ASPNET-Core

**TODO** there's one other one I know we hit during the AzDevNext port.

## Differences in MSBuild

By default, `<Project Sdk="Microsoft.NET.Sdk.Web">` sets `<RunWorkingDirectory>$(MSBuildProjectDirectory)</RunWorkingDirectory>`.
`<Project Sdk="Microsoft.NET.Sdk">` does not.
This means that the working directory for `dotnet run` will be different for ASP.NET apps as for console apps.

## Gotchas

### Binding value types in controller methods

When implementing a controller method that takes an `int`: either depend on your data store to *not* respond to `0`, or (better) make the parameter `int?`.

Actually, add `[BindRequired]` to the parameter. Then, check `ModelState.IsValid`.
    - This removes the need for ad-hoc input validation in the code.
    - It also makes the code cleaner not to worry about nullable types.
    - I like specifying `[FromQuery]`, `[FromForm]`, etc., also.
    - In an `[ApiController]`, checking `ModelState.IsValid` happens automatically

### Tag helpers
When using anchor tag helpers (`asp-controller`, `asp-action`, `asp-route-`), the tag helper will fail **silently** if it can't match the route.
You'll just end up with an empty `href` in the generated HTML.

### Bundling and minifying

Unfortunately, it seems like the `dotnet bundle` CLI for [`BundlerMinifier`](https://github.com/madskristensen/BundlerMinifier) just doesn't work.
- It was working on my local Windows machine, but when I pushed and it ran CI on Ubuntu, it wouldn't work.
- When I cloned the project on my Debian WSL, it said:

```
It was not possible to find any compatible framework version
The framework 'Microsoft.NETCore.App', version '1.0.0' was not found.
The following frameworks were found:
    3.1.5 at [/usr/share/dotnet/shared/Microsoft.NETCore.App]

You can resolve the problem by installing the specified framework and/or SDK.

The specified framework can be found at:
https://aka.ms/dotnet-core-applaunch?framework=Microsoft.NETCore.App&framework_version=1.0.0&arch=x64&rid=debian.10-x64
```

 So, it seems like it's depending on an older .NET version. I cleaned a bunch of older .NET Core versions from my Windows machine, but I have .NET Framework on there, too.
- Sure enough, it seems like the CLI was [built on .NET Framework 4.6](https://github.com/madskristensen/BundlerMinifier/blob/8b1de34bd922377ce05cee5a1d9f85eb70dfcad5/src/BundlerMinifierConsole/BundlerMinifierConsole.csproj#L11).
- I could try installing an older version of .NET on my WSL Debian, but I don't feel like polluting it, or trying to troubleshoot this anymore.
    It seems like this just doesn't work and that running as a VS plugin or through Gulp are the intenced mechanisms.
    I'm just going to move on to more widely used bundling and minifying tools.
