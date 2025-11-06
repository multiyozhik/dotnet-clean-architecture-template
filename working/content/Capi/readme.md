# Capi Project - Clean Architecture Template.


Микросервис построен по принципам Clean Architecture с четким разделением слоев и зависимостей:
- README.md - инструкции по проекту
- Capi.Api - слой Web Api - зависимости от Application, Infrastructure
- Capi.Application - бизнес-логика  - зависимости от Domain
- Capi.Domain - доменные модели - нет зависимостей 
- Capi.Infrasructure - данные, внешние сервисы - зависимости от Application


### Команды для использования шаблона для создания проекта с использованием шаблона Capi 

Создать папку src и в ней пустой файл решения, например, `ProjectStore.sln`:
`dotnet new sln -n "ProjectStore"`

В src-папке создать Services-папку и из нее проект, например, Catalog по Capi-шаблону:
`dotnet new Capi -n Catalog`

Добавить все проекты в solution:
`dotnet sln add **/*.csproj` (для Mac OS)
`Get-ChildItem -Recurse -Filter *.csproj | ForEach-Object { dotnet sln add $_.FullName }` (для Windows)

Или каждый проект по отдельности:
`dotnet sln add "src/Services/Capi/Capi.API/Capi.API.csproj"`
`dotnet sln add "src/Services/Capi/Capi.Application/Capi.Application.csproj"`
`dotnet sln add "src/Services/Capi/Capi.Domain/Capi.Domain.csproj"`
`dotnet sln add "src/Services/Capi/Capi.Infrastructure/Capi.Infrastructure.csproj"`

Сборка проекта и запуск API
`dotnet build`
`dotnet run --project src/Services/Capi/Capi.API`