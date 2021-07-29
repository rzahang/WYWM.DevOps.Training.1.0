#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["WYWM.DevOps.Training.1.0/WYWM.DevOps.Training.1.0.csproj", "WYWM.DevOps.Training.1.0/"]
RUN dotnet restore "WYWM.DevOps.Training.1.0/WYWM.DevOps.Training.1.0.csproj"
COPY . .
WORKDIR "/src/WYWM.DevOps.Training.1.0"
RUN dotnet build "WYWM.DevOps.Training.1.0.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WYWM.DevOps.Training.1.0.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WYWM.DevOps.Training.1.0.dll"]