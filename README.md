# @luca324/yandex-evershop-s3

[![npm version](https://badge.fury.io/js/%40luca324%2Fyandex-evershop-s3.svg)](https://badge.fury.io/js/%40luca324%2Fyandex-evershop-s3)

Пропатченная версия `@evershop/s3_file_storage` с поддержкой Yandex Cloud S3.

## Установка

```bash
npm install @luca324/yandex-evershop-s3
```

Или для Yarn:
```bash
yarn add @luca324/yandex-evershop-s3
```

## Что исправляет

Этот пакет автоматически применяет патч к `@evershop/s3_file_storage`:

1. **Поддержка Yandex Cloud S3 endpoint**
2. [Другие исправления, которые вы сделали]

## Использование

Используйте точно так же, как оригинальный пакет:
добавьте в файл .env следующие переменные:

```env
AWS_ACCESS_KEY_ID=your_access_key_id       # ID ключа доступа (в интерфейсе Yandex S3)
AWS_SECRET_ACCESS_KEY=your_secret_access_key      # Секретный ключ доступа
AWS_BUCKET_NAME=your_bucket_name        # Имя бакета
AWS_REGION=ru-central1       # Регион (для Yandex S3 работает `ru-central1`)
AWS_ENDPOINT=https://storage.yandexcloud.net        # Endpoint для Yandex S3 (`https://storage.yandexcloud.net`)
AWS_S3_FORCE_PATH_STYLE=true
```

## Как это работает

При установке `postinstall` скрипт автоматически применяет патч к установленной копии `@evershop/s3_file_storage`.

## Локальная разработка

```bash
# Клонируйте репозиторий
git clone https://github.com/Luca324/yandex-evershop-s3.git
cd yandex-evershop-s3

# Установите зависимости
npm install

# Создайте патч (если нужно обновить)
npx patch-package @evershop/s3_file_storage
```

## Лицензия

MIT © [Luca324](https://github.com/Luca324)

