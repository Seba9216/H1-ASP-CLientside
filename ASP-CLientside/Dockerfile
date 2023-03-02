#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ASP-CLientside/ASP-CLientside.csproj", "ASP-CLientside/"]
RUN dotnet restore "ASP-CLientside/ASP-CLientside.csproj"
COPY . .
WORKDIR "/src/ASP-CLientside"
RUN dotnet build "ASP-CLientside.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASP-CLientside.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASP-CLientside.dll"]