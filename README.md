# Поле боя — сборка для APK

В папке `www/` лежит `index.html` — это и есть вся игра (один файл, HTML+JS, рендер на Three.js с CDN).

## Как превратить это в APK (вариант через Capacitor, бесплатно, без своего сервера)

Нужен компьютер с установленным Node.js и Android Studio (с Android SDK).

1. Установить инструменты (один раз):
   ```
   npm install -g @capacitor/cli
   ```
2. В пустой папке рядом с этой:
   ```
   npm init -y
   npm install @capacitor/core @capacitor/android
   npx cap init "Поле боя" "com.example.polebooya" --web-dir=www
   ```
3. Скопировать содержимое папки `www/` из этого архива в `www/` новосозданного проекта (заменить index.html).
4. Добавить платформу Android и открыть проект:
   ```
   npx cap add android
   npx cap sync
   npx cap open android
   ```
5. В открывшемся Android Studio собрать APK: `Build → Build Bundle(s) / APK(s) → Build APK(s)`.
   Готовый файл будет в `android/app/build/outputs/apk/debug/app-debug.apk`.

## Важно про интернет

Игра грузит библиотеку Three.js и шрифт с CDN (cdnjs.cloudflare.com, fonts.googleapis.com).
В APK это тоже будет работать, но устройству нужен интернет при запуске.
Если нужна версия, которая работает совсем без интернета (офлайн APK), скажи —
я соберу вариант, где Three.js и шрифт зашиты внутрь файла, и тогда интернет для запуска не понадобится.

## Онлайн-режим (игра с другом)

Онлайн-режим использует системную функцию Claude-чата (window.claude.use('room')) и работает
только когда страница открыта внутри приложения Claude. В обычном APK (вне Claude) кнопка
«Онлайн» работать не будет — отображаться будет сообщение «Онлайн недоступен». Одиночная игра
и сложность ботов будут работать как обычно.
