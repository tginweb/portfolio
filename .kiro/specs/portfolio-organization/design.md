# Design Document

## Overview

Дизайн портфолио-репозитория основан на использовании git submodules для создания вложенных репозиториев. Каждый проект становится отдельным репозиторием, который подключается как submodule к основному портфолио-репозиторию. Это обеспечивает правильное отображение README файлов на GitHub и позволяет каждому проекту иметь собственную историю коммитов.

## Architecture

### Repository Structure

```
portfolio-repo/                  # Основной репозиторий
├── README.md                   # Корневой README с обзором всех проектов
├── .gitmodules                 # Конфигурация submodules
├── ais-abiturient/            # Git submodule → отдельный репозиторий
│   ├── README.md              # README проекта (отображается на GitHub)
│   └── [код проекта]
├── ogirk-news-portal/         # Git submodule → отдельный репозиторий
│   ├── README.md              # README проекта (отображается на GitHub)
│   └── [код проекта]
├── sushi-commerce-app/        # Git submodule → отдельный репозиторий
│   ├── README.md              # README проекта (отображается на GitHub)
│   └── [код проекта]
└── sushi-commerce-site/       # Git submodule → отдельный репозиторий
    ├── README.md              # README проекта (отображается на GitHub)
    └── [код проекта]
```

### Core Components

#### 1. Git Submodules Configuration

Файл `.gitmodules` содержит конфигурацию всех подключенных проектов:

```ini
[submodule "ais-abiturient"]
    path = ais-abiturient
    url = https://github.com/username/ais-abiturient.git

[submodule "ogirk-news-portal"]
    path = ogirk-news-portal
    url = https://github.com/username/ogirk-news-portal.git
```

#### 2. Individual Project Repositories

Каждый проект становится отдельным репозиторием с:

- Собственной историей коммитов
- Отдельными issues и pull requests
- Независимым управлением версиями
- Автоматическим отображением README на GitHub

#### 3. Main Portfolio README

Статический корневой README файл с:

- Обзором всех проектов
- Ссылками на submodule репозитории
- Кратким описанием технологий
- Контактной информацией

## Components and Interfaces

### 1. Submodule Management

```bash
# Команды для управления submodules
git submodule add <repository-url> <path>
git submodule update --init --recursive
git submodule foreach git pull origin main
```

### 2. Repository Structure

Каждый проект-репозиторий содержит:

- `README.md` - детальное описание проекта
- Исходный код проекта
- Документацию и скриншоты
- Собственную историю разработки

### 3. Main README Structure

Корневой README включает:

- Заголовок портфолио
- Таблицу проектов с описаниями
- Технологический стек
- Инструкции по клонированию с submodules

## Data Models

### Individual Repository Structure

```
project-repository/
├── README.md              # Детальное описание проекта (отображается на GitHub)
├── assets/               # Ресурсы проекта
│   ├── screenshots/      # Скриншоты интерфейса
│   └── diagrams/         # Архитектурные диаграммы
└── [исходный код]        # Код проекта
```

### Main Portfolio README Structure

1. **Header** - Заголовок портфолио и краткое описание
2. **Projects Overview** - Таблица проектов с ссылками на submodules
3. **Technologies** - Используемые технологии
4. **Setup Instructions** - Инструкции по клонированию с submodules
5. **Contact Information** - Контактные данные

## Error Handling

### Submodule Synchronization

- Проверка доступности удаленных репозиториев
- Обработка конфликтов при обновлении submodules
- Fallback к локальным копиям при недоступности remote

### Repository Access

- Обработка приватных репозиториев
- Управление правами доступа к submodules
- Валидация URL репозиториев

### GitHub Display Issues

- Проверка корректности отображения README в submodules
- Обработка проблем с кодировкой
- Валидация Markdown разметки

## Testing Strategy

### Repository Structure Tests

- Проверка корректности .gitmodules конфигурации
- Валидация путей к submodules
- Тестирование клонирования с --recursive флагом

### Submodule Integration Tests

- Проверка синхронизации с удаленными репозиториями
- Тестирование обновления submodules
- Валидация ссылок между репозиториями

### GitHub Display Tests

- Проверка отображения README в каждом submodule
- Тестирование навигации между проектами
- Валидация корректности ссылок

### Manual Verification

- Проверка отображения на GitHub веб-интерфейсе
- Тестирование клонирования третьими лицами
- Валидация пользовательского опыта

## Implementation Phases

### Phase 1: Repository Setup

- Создание отдельных репозиториев для каждого проекта
- Перенос кода и README файлов в новые репозитории
- Настройка правильной структуры каждого проекта

### Phase 2: Submodule Integration

- Создание основного портфолио-репозитория
- Добавление проектов как git submodules
- Настройка .gitmodules конфигурации

### Phase 3: Main README Creation

- Создание корневого README с обзором проектов
- Добавление ссылок на каждый submodule
- Оформление единообразного стиля

### Phase 4: Testing & Refinement

- Проверка отображения на GitHub
- Тестирование клонирования с submodules
- Финальные доработки и оптимизация
