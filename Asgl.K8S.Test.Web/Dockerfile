FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["Asgl.K8S.Test.Web/Asgl.K8S.Test.Web.csproj", "Asgl.K8S.Test.Web/"]

RUN dotnet restore "Asgl.K8S.Test.Web/Asgl.K8S.Test.Web.csproj"
COPY . .
WORKDIR "/src/Asgl.K8S.Test.Web"
RUN dotnet build "Asgl.K8S.Test.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Asgl.K8S.Test.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Asgl.K8S.Test.Web.dll"]