# Clean Architecture Template

### Назначение шаблона

Готовый к использованию шаблон для создания микросервисов на .NET с архитектурой Clean Architecture.
Irina Sviridova  GitHub: [@multiyozhik](https://github.com/multiyozhik)

При использовании команды `dotnet new Capi -n MyProject` создаётся следующая структура MyProject:
- README.md - инструкции по проекту
- MyProject.Api - слой Web Api
- MyProject.Application - бизнес-логика
- MyProject.Domain - доменные модели
- MyProject.Infrasructure - данные, внешние сервисы


### Команды для создания нового проекта MyMicroservice с использованием шаблона Capi 

##### 1. Добавить источник GitHub Packages
Создайте Personal Access Token на GitHub с правами read:packages и выполните команду по шаблону:

```bash
dotnet nuget add source https://nuget.pkg.github.com/<GITHUB_USERNAME>/index.json \
  --name <CUSTOM_NUGET_NAME> \
  --username <YOUR_GITHUB_USERNAME> \
  --password <YOUR_PERSONAL_ACCESS_TOKEN> \
  --store-password-in-clear-text
```

##### 2. Установить шаблон

```bash
dotnet new install multiyozhik.cleanarchitecture.template
```

##### 3. Использовать шаблон

```bash
# Создать новый проект
dotnet new Capi -n MyMicroservice

# Перейти в проект и запустить
cd MyMicroservice
dotnet build
dotnet run --project MyMicroservice.API
```


### Команды для управления шаблоном

```bash
# Проверить установку шаблона
dotnet new list
# Обновить шаблон
dotnet new install multiyozhik.cleanarchitecture.template --force
# Удалить шаблон
dotnet new uninstall multiyozhik.cleanarchitecture.template
# Удалить источник
dotnet nuget remove source github-multiyozhik
# Посмотреть все источники NuGet
dotnet nuget list source
```


### Публикация новых версий (для автора)

1. Внесите изменения в шаблон:
   - Отредактируйте файлы в `working/content/Capi/`
   - Обновите `PackageVersion` в `Template.csproj`

2. Закоммитьте и создайте тег версии:

   ```bash
   git add .
   git commit -m "Update template: добавлена новая функциональность"
   git push origin main


   git tag v1.0.0
   git push origin v1.0.0
   ```

3. GitHub Actions автоматически опубликует пакет в GitHub Packages при создании тега.
   Проверить публикацию: **Actions** → статус workflow, **Packages** → новая версия.


### Команды для локальной разработки и тестирования шаблона Capi

```bash
# Клонировать репозиторий
git clone https://github.com/multiyozhik/dotnet-clean-architecture-template.git
cd dotnet-clean-architecture-template

# Установить локально для тестирования
cd working
dotnet new install .

# Тестировать изменения
dotnet new Capi -n TestProject

# Удалить локальную версию
dotnet new uninstall "/полный/путь/к/working"
```


### Используемые команды для создания проекта шаблона Capi и его зависимостей

```bash
dotnet version   # 9.0.102

# В папке шаблона (Capi)
dotnet new web -n "Capi.API"   
dotnet new classlib -n "Capi.Domain"  
dotnet new classlib -n "Capi.Application"  
dotnet new classlib -n "Capi.Infrastructure"

# В корне репозитория
dotnet new gitignore   

# Из проекта Capi.API
dotnet add reference "../Capi.Application"
dotnet add reference "../Capi.Infrastructure"

# Из проекта Capi.Application
dotnet add reference "../Capi.Domain" 

# Проект Capi.Domain не имеет внешних зависимостей

# Из проекта Capi.Infrastructure
dotnet add reference "../Capi.Application"

# Используемые в Capi зависимости
dotnet add package "Swashbuckle.AspNetCore" --version "9.0.3"
dotnet add package "Microsoft.Extensions.DependencyInjection.Abstractions" --version "9.0.7"
dotnet add package "Microsoft.Extensions.Configuration" --version "9.0.7"
```