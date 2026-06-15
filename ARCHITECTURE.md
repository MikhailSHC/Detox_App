# Архитектура проекта: Minimal Launcher

## 1. Цель проекта
Создание минималистичного лаунчера для Android с фокусом на цифровое благополучие (Digital Wellbeing). Основные функции: текстовый интерфейс, список приложений, режим фокуса (таймер/помодоро) и строгий режим блокировки отвлекающих факторов.

## 2. Технологический стек (Modern Android Stack)
- **Язык:** Kotlin
- **UI:** Jetpack Compose + Material 3 (Dynamic Colors support)
- **Архитектура:** Clean Architecture + MVI (Model-View-Intent) / Unidirectional Data Flow (UDF)
- **Асинхронность:** Kotlin Coroutines + Flow (StateFlow/SharedFlow)
- **Внедрение зависимостей (DI):** Hilt (или Koin, если потребуется легковесность)
- **Хранение данных:** Jetpack DataStore (Preferences)
- **Навигация:** Jetpack Navigation Compose

## 3. Структура пакетов (Clean Architecture)
```text
com.yourname.minimallauncher
├── data            # Источники данных и реализация репозиториев
│   ├── local       # DataStore реализации
│   ├── remote      # (Если применимо, например, для обновлений)
│   ├── repository  # Реализации интерфейсов из domain
│   └── manager     # Обертки над системными API (AppManager, UsageStatsManager)
├── domain          # Чистая бизнес-логика (без зависимостей от Android SDK)
│   ├── model       # Data classes (AppInfo, FocusSession, UsageStats)
│   ├── repository  # Интерфейсы репозиториев
│   └── usecase     # Use cases (GetInstalledAppsUseCase, StartFocusUseCase)
├── presentation    # UI слой и ViewModel
│   ├── home        # Главный экран (Часы, избранные приложения)
│   ├── drawer      # App Drawer (список всех приложений + поиск)
│   ├── focus       # Экран режима фокуса
│   └── settings    # Экран настроек
└── di              # Модули внедрения зависимостей (Hilt Modules)