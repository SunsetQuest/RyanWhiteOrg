FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 52257
EXPOSE 44344

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY RyanWhiteOrg/RyanWhiteOrg.csproj RyanWhiteOrg/
RUN dotnet restore RyanWhiteOrg/RyanWhiteOrg.csproj
COPY . .
WORKDIR /src/RyanWhiteOrg
RUN dotnet build RyanWhiteOrg.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish RyanWhiteOrg.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RyanWhiteOrg.dll"]
