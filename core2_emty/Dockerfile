FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 65169
EXPOSE 44314

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["core2_emty/core2_emty.csproj", "core2_emty/"]
RUN dotnet restore "core2_emty/core2_emty.csproj"
COPY . .
WORKDIR "/src/core2_emty"
RUN dotnet build "core2_emty.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "core2_emty.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "core2_emty.dll"]