#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Api/Write/EmergingBookingApiWrite/EmergingBookingApiWrite.csproj", "Api/Write/EmergingBookingApiWrite/"]
RUN dotnet restore "Api/Write/EmergingBookingApiWrite/EmergingBookingApiWrite.csproj"
COPY . .
WORKDIR "/src/Api/Write/EmergingBookingApiWrite"
RUN dotnet build "EmergingBookingApiWrite.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EmergingBookingApiWrite.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EmergingBookingApiWrite.dll"]