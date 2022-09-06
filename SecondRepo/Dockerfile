FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["SecondRepo/SecondRepo.csproj", "SecondRepo/"]
RUN dotnet restore "SecondRepo/SecondRepo.csproj"
COPY . .
WORKDIR "/src/SecondRepo"
RUN dotnet build "SecondRepo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SecondRepo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SecondRepo.dll"]