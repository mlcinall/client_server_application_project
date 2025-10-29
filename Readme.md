# Codex Sync — платформа для совместного редактирования кода

## Схема системы совместного редактирования кода
![image](https://github.com/user-attachments/assets/95fb8a09-ae3d-4fe4-badc-0e85e72ef618)
Архитектура описывает, как клиенты подключаются к веб-сокетам, обмениваются событиями редактирования и сохраняют изменения в хранилище данных с низкой задержкой.

## Схема системы компиляции кода
![image](https://github.com/user-attachments/assets/830b079a-b63b-4762-b63c-eaff53f1950f)
Отдельные сервисы принимают задания на компиляцию, помещают их в очередь и обрабатывают рабочими процессами, возвращая результаты фронтенду.

## Запуск проекта
1. Клонируйте репозиторий и перейдите в каталог проекта:
   ```bash
   git clone https://github.com/mlcinall/client_server_application_project.git
   cd client_server_application_project
   ```
2. Запустите Redis через Docker Compose и убедитесь, что контейнер активен:
   ```bash
   docker compose up -d
   docker ps
   ```
   Если увидите сообщение о том, что порт 6379 уже занят, остановите предыдущий контейнер и повторите запуск:
   ```bash
   docker rm -f redis-stack
   docker compose up -d
   ```
3. Установите зависимости, обходя ограничение PowerShell на выполнение скриптов:
   ```bash
   & "$env:ProgramFiles\nodejs\npm.cmd" install
   ```
4. Скомпилируйте серверные пакеты при помощи TypeScript:
   ```bash
   & "$env:ProgramFiles\nodejs\npx.cmd" tsc -p apps\express-server
   & "$env:ProgramFiles\nodejs\npx.cmd" tsc -p apps\websocket-server
   & "$env:ProgramFiles\nodejs\npx.cmd" tsc -p apps\worker
   ```
   После успешной компиляции в каждом пакете появится каталог `dist` с файлом `index.js`.
   Если TypeScript не установлен, добавьте его в зависимости и повторите команды выше:
   ```bash
   & "$env:ProgramFiles\nodejs\npm.cmd" i -D typescript
   ```
5. Запустите все сервисы в режиме разработки и откройте интерфейс:
   ```bash
   & "$env:ProgramFiles\nodejs\npm.cmd" run dev
   ```
   После запуска сервисов интерфейс будет доступен по адресу `http://localhost:5173`.
