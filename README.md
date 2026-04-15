# Lexi Buddy Infrastructure

### Где мы работаем 
 - обычно все команды выполняются в папке инфраструктуры: 
     + /root/lexi-buddy-infra
 - посмотреть все файлы в папке:
     + ls -la

### Базовые команды Docker
 - Посмотреть только запущенные контейнеры: 
     + docker ps
 - Посмотреть вообще все контейнеры:
     + docker ps -a
 - Посмотреть все compose-проекты:
     + docker compose ls
 - Посмотреть последние 100 строк логов контейнера (на примере lexi_buddy_staging_api):
     + docker logs lexi_buddy_staging_api --tail 100
 - Смотреть логи контейнера в реальном времени (на примере lexi_buddy_staging_api):
     + docker logs -f lexi_buddy_staging_api
 - Посмотреть последние 100 строк логов через compose: 
     + docker compose -p lexi-buddy-staging -f docker-compose.staging.yml logs --tail 100 
     + docker compose -p lexi-buddy-prod -f docker-compose.prod.yml logs --tail 100
 - Смотреть логи в реальном времени:
     + docker compose -p lexi-buddy-staging -f docker-compose.staging.yml logs -f
     + docker compose -p lexi-buddy-prod -f docker-compose.prod.yml logs -f
 - Перезапуск одного контейнера:
     + docker restart lexi_buddy_staging_api 

### Работа с prod
 - Посмотреть статус prod-сервисов: docker compose -p lexi-buddy-prod -f docker-compose.prod.yml ps
 - Поднять prod: docker compose -p lexi-buddy-prod -f docker-compose.prod.yml up -d
 - Перезапустить prod: docker compose -p lexi-buddy-prod -f docker-compose.prod.yml up -d 
 - Остановить prod: docker compose -p lexi-buddy-prod -f docker-compose.prod.yml down

### Работа с staging
- Посмотреть статус staging-сервисов: docker compose -p lexi-buddy-staging -f docker-compose.staging.yml ps
- Поднять staging: docker compose -p lexi-buddy-staging -f docker-compose.staging.yml up -d
- Перезапустить staging: docker compose -p lexi-buddy-prod -f docker-compose.prod.yml up -d
- Остановить staging: docker compose -p lexi-buddy-staging -f docker-compose.staging.yml down
- Посмотреть, какие сервисы вообще описаны в staging-файле: docker compose -f docker-compose.staging.yml config --services

### Самые частые полезные проверки: 
 - Убедиться, что staging и prod не перепутались: 
    + docker compose ls
 - Увидеть все контейнеры по имени: 
    + docker ps -a
 - Проверить, открыт ли нужный порт:
    + docker ps

### Если что-то непонятно, почти всегда порядок такой:
 - docker compose ls
 - docker ps -a
 - docker compose -p lexi-buddy-staging -f docker-compose.staging.yml ps
 - docker compose -p lexi-buddy-staging -f docker-compose.staging.yml logs --tail 100

То есть:
- понять, что поднято
- понять, какие контейнеры живы
- понять, какой именно сервис сломан
- открыть его логи