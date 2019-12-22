#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["dotnet-sdk-ASP.NetCore-BlazorApp1/dotnet-sdk-ASP.NetCore-BlazorApp1.csproj", "dotnet-sdk-ASP.NetCore-BlazorApp1/"]
RUN dotnet restore "dotnet-sdk-ASP.NetCore-BlazorApp1/dotnet-sdk-ASP.NetCore-BlazorApp1.csproj"
COPY . .
WORKDIR "/src/dotnet-sdk-ASP.NetCore-BlazorApp1"
RUN dotnet build "dotnet-sdk-ASP.NetCore-BlazorApp1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dotnet-sdk-ASP.NetCore-BlazorApp1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dotnet-sdk-ASP.NetCore-BlazorApp1.dll"]