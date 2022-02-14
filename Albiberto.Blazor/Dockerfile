#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Albiberto.Blazor/Albiberto.Blazor.csproj", "Albiberto.Blazor/"]
RUN dotnet restore "Albiberto.Blazor/Albiberto.Blazor.csproj"
COPY . .
WORKDIR "/src/Albiberto.Blazor"
RUN dotnet build "Albiberto.Blazor.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Albiberto.Blazor.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Albiberto.Blazor.dll"]
