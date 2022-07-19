FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
CMD dotnet add package SkyAPM.Agent.AspNetCore

WORKDIR /app

COPY . ./
RUN dotnet publish Aspnetcoreapp -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build-env /app/Aspnetcoreapp/out .
CMD set ASPNETCORE_HOSTINGSTARTUPASSEMBLIES=SkyAPM.Agent.AspNetCore
CMD SKYWALKING__SERVICENAME=Aspnetcoreapp 
ENTRYPOINT ["dotnet", "Aspnetcoreapp.dll"]
