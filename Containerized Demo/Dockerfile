FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Containerized Demo/Containerized Demo.csproj", "Containerized Demo/"]
RUN dotnet restore "Containerized Demo/Containerized Demo.csproj"
COPY . .
WORKDIR "/src/Containerized Demo"
RUN dotnet build "Containerized Demo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Containerized Demo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Containerized Demo.dll"]