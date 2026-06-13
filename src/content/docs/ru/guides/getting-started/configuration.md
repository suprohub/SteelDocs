---
title: Конфигурация
description: Как настроить ваш сервер Steel.
---

Steel использует файл конфигурации в формате JSON5, который поддерживает комментарии и висячие запятые.

## Файл конфигурации

При первом запуске Steel создаёт `config/steel_config.json5` со значениями по умолчанию.

## Параметры конфигурации

### Настройки сервера

```json5
{
  // Порт, который слушает сервер (1-65000)
  server_port: 25565,

  // Сид мира (пустая строка для случайного)
  seed: "",

  // Максимальное количество одновременных игроков
  max_players: 20,

  // Дальность обзора в чанках (1-32)
  view_distance: 10,

  // Дистанция симуляции в чанках (1-32, должна быть ≤ view_distance)
  simulation_distance: 10,

  // Требовать аутентификацию Mojang
  online_mode: true,

  // Включить шифрование клиент-сервер
  encryption: true,

  // Сообщение в списке серверов
  motd: "A Steel Server",

  // Принудительно использовать криптографические подписи чата
  // Требует, чтобы online_mode и encryption были true
  enforce_secure_chat: false,
}
```

### Фавиконка

```json5
{
  // Включить пользовательскую иконку сервера
  use_favicon: true,

  // Путь к изображению иконки (должно быть 64x64 PNG)
  favicon: "config/favicon.png",
}
```

Поместите изображение PNG размером 64x64 в `config/favicon.png`, чтобы отобразить пользовательскую иконку в списке серверов.

### Сжатие

```json5
{
  compression: {
    // Минимальный размер пакета для сжатия (минимум 256 байт)
    threshold: 256,

    // Уровень сжатия Zlib (0-9, выше = меньше размер, но медленнее)
    level: 6,
  },
}
```

### Ссылки сервера

Ссылки сервера отображаются в меню паузы игрока:

```json5
{
  server_links: {
    enable: true,
    links: [
      // Встроенные типы меток
      {
        label: "bug_report",
        url: "https://github.com/Steel-Foundation/SteelMC/issues",
      },

      // Пользовательские стилизованные метки
      {
        label: { text: "Discord", color: "blue", bold: true },
        url: "https://discord.gg/MwChEHnAbh",
      },
    ],
  },
}
```

## Полный пример

```json5
{
  server_port: 25565,
  seed: "my_world_seed",
  max_players: 50,
  view_distance: 12,
  simulation_distance: 10,
  online_mode: true,
  encryption: true,
  motd: "Welcome to my Steel server!",
  enforce_secure_chat: false,
  use_favicon: true,
  favicon: "config/favicon.png",
  compression: {
    threshold: 256,
    level: 6,
  },
  server_links: {
    enable: true,
    links: [
      {
        label: "bug_report",
        url: "https://github.com/Steel-Foundation/SteelMC/issues",
      },
    ],
  },
}
```

## Правила валидации

Steel проверяет вашу конфигурацию при запуске:

| Параметр                | Ограничение                                        |
| ----------------------- | -------------------------------------------------- |
| `server_port`           | 1-65000                                            |
| `view_distance`         | 1-32                                               |
| `simulation_distance`   | 1-32, должно быть ≤ `view_distance`                |
| `compression.threshold` | ≥ 256                                              |
| `compression.level`     | 0-9                                                |
| `enforce_secure_chat`   | Требует `online_mode` и `encryption` равными `true` |

Если валидация не пройдена, сервер завершит работу с сообщением об ошибке.

## Дальнейшие шаги

Настроив сервер, вы готовы [запустить его](/SteelDocs/getting-started/running/).