FROM microsoft/dotnet:2.1-sdk AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Byteauthor.Servoise.sln ./
COPY Byteauthor.Servoise.Web/Byteauthor.Servoise.Web.csproj Byteauthor.Servoise.Web/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/Byteauthor.Servoise.Web
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM microsoft/dotnet:2.1-aspnetcore-runtime AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Byteauthor.Servoise.Web.dll"]
