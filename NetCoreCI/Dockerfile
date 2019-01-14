FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["NetCoreCI/NetCoreCI.csproj", "NetCoreCI/"]
RUN dotnet restore "NetCoreCI/NetCoreCI.csproj"
COPY . .
WORKDIR "/src/NetCoreCI"
RUN dotnet build "NetCoreCI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NetCoreCI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NetCoreCI.dll"]