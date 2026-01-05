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

```javascript
const { S3FileStorage } = require('@luca324/yandex-evershop-s3');

const storage = new S3FileStorage({
  region: 'ru-central1',
  endpoint: 'https://storage.yandexcloud.net',
  credentials: {
    accessKeyId: 'YOUR_KEY',
    secretAccessKey: 'YOUR_SECRET'
  },
  bucket: 'your-bucket'
});
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

