#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["SampleDockerWebApp/SampleDockerWebApp.csproj", "SampleDockerWebApp/"]
RUN dotnet restore "SampleDockerWebApp/SampleDockerWebApp.csproj"
COPY . .
WORKDIR "/src/SampleDockerWebApp"
RUN dotnet build "SampleDockerWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SampleDockerWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SampleDockerWebApp.dll"]