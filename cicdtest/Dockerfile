FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["cicdtest.csproj", "cicdtest/"]
RUN dotnet restore "cicdtest/cicdtest.csproj"
COPY . .
WORKDIR "/src/cicdtest"
RUN dotnet build "cicdtest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "cicdtest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "cicdtest.dll"]
