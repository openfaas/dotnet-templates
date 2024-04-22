# dotnet-templates

Templates for .NET

## dotnet8-csharp

This template uses the ASP.net minimal API style, and exposes a static function to register HTTP handlers. It is multi-arch, and supports Linux for amd64 and Arm64 via `faas-cli publish` or `faas-cli up --publish`.

Register a `/hello` as an endpoint:

```csharp
    public static void MapEndpoints(WebApplication app) {
        app.MapGet("/hello", () => "Hello, world!");
    }

```

The `RegisterServices` method can be used to configure any WebApplication services such as Swagger generators.

```csharp
    public static void MapServices(IServiceCollection services)
    {
        services.AddEndpointsApiExplorer();
        services.AddSwaggerGen();
    }
```

Pull the template:

```bash
faas-cli template pull https://github.com/openfaas/dotnet-templates
```

Create a new function using the template:

```bash
export PREFIX="ttl.sh"
faas-cli new --lang dotnet8-csharp $PREFIX hello-world
```

## Adding static files

If a folder named static is found in the root of your function's source code, **it will be copied** into the final image published for your function.

To serve the contents of the static folder you can setup the file server in `Handler.cs`.

```c#
    public static void MapEndpoints(WebApplication app) {
        app.UseStaticFiles();
    }
```