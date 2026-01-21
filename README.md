# @luca324/yandex-evershop-s3

[![npm version](https://badge.fury.io/js/%40luca324%2Fyandex-evershop-s3.svg)](https://badge.fury.io/js/%40luca324%2Fyandex-evershop-s3)

Патч для пакета `@evershop/s3_file_storage` с поддержкой Yandex Cloud S3.

## Описание

Этот пакет предоставляет патч-файл, который модифицирует `@evershop/s3_file_storage` для работы с Yandex Cloud Object Storage (S3-совместимое хранилище). Патч добавляет поддержку кастомного endpoint и исправляет генерацию URL для корректной работы с Yandex Cloud.

## Требования

- Node.js проект с установленным `@evershop/s3_file_storage`
- `patch-package` должен быть установлен в вашем проекте как зависимость разработки
- Скрипт `postinstall` должен быть настроен в `package.json` для автоматического применения патчей

## Установка

### Шаг 1: Установите пакет

Установите пакет через npm или yarn:

```bash
npm install @luca324/yandex-evershop-s3
```

или

```bash
yarn add @luca324/yandex-evershop-s3
```

### Шаг 2: Скопируйте патч в корень проекта

После установки пакета, патч-файл будет находиться в `node_modules/@luca324/yandex-evershop-s3/patches/`. Вам нужно скопировать его в папку `patches/` в корне вашего проекта.

**Для Linux/Mac:**
```bash
mkdir -p patches
cp node_modules/@luca324/yandex-evershop-s3/patches/@evershop+s3_file_storage+2.0.0.patch patches/
```

### Шаг 3: Убедитесь, что patch-package настроен

Убедитесь, что в вашем `package.json` есть:

1. `patch-package` в `devDependencies`:
```json
{
  "devDependencies": {
    "patch-package": "^8.0.1"
  }
}
```

2. Скрипт `postinstall` в секции `scripts`:
```json
{
  "scripts": {
    "postinstall": "patch-package"
  }
}
```

Если их нет, установите и добавьте:

```bash
npm install --save-dev patch-package
```

И добавьте скрипт в `package.json`:
```json
{
  "scripts": {
    "postinstall": "patch-package"
  }
}
```

### Шаг 4: Примените патч

Патч будет применен автоматически при следующей установке зависимостей:

```bash
npm install
```

Или примените патч вручную:

```bash
npx patch-package
```

## Что изменяет патч

Патч модифицирует следующие файлы в `@evershop/s3_file_storage`:

### 1. **Конфигурация S3Client**
   - Добавляет поддержку кастомного `endpoint` (для Yandex Cloud S3)
   - Включает `forcePathStyle: true` для корректной работы с Yandex Cloud

### 2. **Генерация URL файлов**
   - Изменяет формат URL с AWS-стиля (`https://bucket.s3.amazonaws.com/path`) на path-style (`https://storage.yandexcloud.net/bucket/path`)
   - Использует переменную окружения `AWS_ENDPOINT` для формирования URL

### 3. **Парсинг URL**
   - Исправляет извлечение имени бакета и ключа объекта из URL для Yandex Cloud формата
   - Корректно обрабатывает path-style URLs

### Измененные файлы:
- `dist/services/awsFileBrowser.js` - просмотр файлов
- `dist/services/awsFileDeleter.js` - удаление файлов
- `dist/services/awsFileUploader.js` - загрузка файлов
- `dist/services/awsFolderCreator.js` - создание папок
- `dist/subscribers/product_image_added/awsGenerateProductImageVariant.js` - генерация вариантов изображений
- Соответствующие TypeScript исходники в `src/`

## Переменные окружения

Для работы с Yandex Cloud S3 добавьте следующие переменные в ваш `.env` файл:

```env
# ID ключа доступа (можно получить в интерфейсе Yandex Cloud)
AWS_ACCESS_KEY_ID=your_access_key_id

# Секретный ключ доступа
AWS_SECRET_ACCESS_KEY=your_secret_access_key

# Имя бакета в Yandex Cloud
AWS_BUCKET_NAME=your_bucket_name

# Регион (для Yandex Cloud всегда используйте ru-central1)
AWS_REGION=ru-central1

# Endpoint для Yandex Cloud S3
AWS_ENDPOINT=https://storage.yandexcloud.net

# Обязательно для Yandex Cloud S3
AWS_S3_FORCE_PATH_STYLE=true
```

### Где получить ключи доступа

1. Перейдите в [Yandex Cloud Console](https://console.cloud.yandex.ru/)
2. Откройте раздел "Сервисные аккаунты"
3. Создайте сервисный аккаунт или используйте существующий
4. Создайте статический ключ доступа для сервисного аккаунта
5. Скопируйте `Access Key ID` и `Secret Access Key`

## Проверка работы

После применения патча убедитесь, что:

1. Патч применен успешно (проверьте вывод `npm install` или `npx patch-package`)
2. Переменные окружения настроены корректно
3. Бакет существует и доступен с указанными ключами
4. Приложение корректно загружает и отображает файлы из Yandex Cloud S3

## Обновление патча

Если вы обновили версию `@evershop/s3_file_storage`, вам может потребоваться обновить патч:

1. Удалите старый патч из папки `patches/`
2. Установите новую версию `@evershop/s3_file_storage`
3. Скопируйте новый патч из `node_modules/@luca324/yandex-evershop-s3/patches/` (если версия патча обновлена)
4. Примените патч снова

## Устранение неполадок

### Патч не применяется

- Убедитесь, что `patch-package` установлен и скрипт `postinstall` настроен
- Проверьте, что патч находится в папке `patches/` в корне проекта
- Проверьте, что имя патча соответствует версии установленного `@evershop/s3_file_storage`

### Ошибки при работе с S3

- Проверьте правильность переменных окружения
- Убедитесь, что ключи доступа имеют необходимые права
- Проверьте, что бакет существует и доступен
- Убедитесь, что `AWS_ENDPOINT` указан как `https://storage.yandexcloud.net`

## Лицензия

MIT © [Luca324](https://github.com/Luca324)

## Репозиторий

[https://github.com/Luca324/yandex-evershop-s3](https://github.com/Luca324/yandex-evershop-s3)
