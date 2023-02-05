FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app
COPY *.csproj ./
RUN dotnet restore
COPY . ./
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /app/out .
EXPOSE 80
ENTRYPOINT [ "dotnet", "ItemService.dll"]
LABEL version="1.0"
HEALTHCHECK --interval=5s \
            --timeout=5s \
            CMD curl --fail http://localhost/health || exit 1
STOPSIGNAL SIGINT
USER 1001
VOLUME /app/data
SHELL [ "/bin/ash", "-c" ]
ENV LANG=pt_BR.UTF-8
ENV DOTNET_RUNTIME_ID=alpine-x64