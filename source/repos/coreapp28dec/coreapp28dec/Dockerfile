#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY ["coreapp28dec/coreapp28dec.csproj", "coreapp28dec/"]
RUN dotnet restore "coreapp28dec/coreapp28dec.csproj"
COPY . .
WORKDIR "/src/coreapp28dec"
RUN dotnet build "coreapp28dec.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "coreapp28dec.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "coreapp28dec.dll"]