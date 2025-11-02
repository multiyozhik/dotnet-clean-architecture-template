Microservice Api template.

Структура проектов:
- Capi.Domain - доменные модели, интерфейсы, entities - нет зависимостей
- Capi.Application - бизнес-логика, сервисы  - зависимости от Domain 
- Capi.Infrasructure - данные, внешние сервисы, repositories - зависимости от Application
- Capi.Api - Web.Api, контроллеры, точка входа - зависимости от Application, Infrastructure
