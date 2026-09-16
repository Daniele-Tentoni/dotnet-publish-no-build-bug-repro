# Repro

Reproduction for [dotnet issue](https://github.com/dotnet/sdk/issues/56323).

## Commands

```
dotnet new webapi --output Api
dotnet new classlib --output Api.Model
dotnet new slnx Api
dotnet sln Api.slnx add Api
dotnet sln Api.slnx add Api.Model
dotnet restore --use-lock-file
dotnet build Api --no-restore --output ./app/build
dotnet publish .\Api\Api.csproj --no-restore --output ./app/publish <-- This works

dotnet publish .\Api\Api.csproj --no-build -p:OutDir="./app/build" --output ./app/publish <!-- This fails

  Api net10.0 failed with 2 error(s) and 1 warning(s) (0.3s)
    C:\work\IR\repro\Api\Api.csproj : warning NU1903: Package 'Microsoft.OpenApi' 2.0.0 has a known high severity vulnerability, https://github.com/advisories/GHSA-v5pm-xwqc-g5wc
    C:\Program Files\dotnet\sdk\10.0.302\Sdks\Microsoft.NET.Sdk\targets\Microsoft.NET.Publish.targets(372,5): error MSB3030: Could not copy the file "C:\work\IR\repro\Api\app\build\Api.deps.json" because it was not found.
    C:\Program Files\dotnet\sdk\10.0.302\Sdks\Microsoft.NET.Sdk\targets\Microsoft.NET.Publish.targets(372,5): error MSB3030: Could not copy the file "C:\work\IR\repro\Api\app\build\Api.runtimeconfig.json" because it was not found.

Build failed with 2 error(s) and 1 warning(s) in 0.5s
```
