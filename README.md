# Коннектор BSLLS для EDT

Плагин позволяет использовать функциональность BSL LS в EDT.

**Состояние проекта**: в глубокой разработке. Плановая дата выхода релиза - `первая половина декабря 2020`.

## Возможности

* Проверки кода [ + ]
* Быстрые исправления [  ]
* Произвольные ссылки [  ]

## Установка

Для разработки в Eclipse требуется:
* Eclipse for Committer 2020-06 / 2020-09
* Плагин lombok (https://projectlombok.org/setup/eclipse)
* Java 11

### Установка из архива

Порядок действий:
* Качаем архив со страницы релизов.
* В EDT открываем меню `Справка` -> `Установить новое ПО`. Далее нужно указать путь к архиву через кнопку `Добавить` (в диалоговом окне кнопка `Архив`).
* Установить флажок на `BSL LS connector for EDT`. Затем `Далее` -> `Готово`. После установки плагина требуется перезапустить EDT.
    **Важно:** обязательно должен быть указан флаг "Обращаться во время инсталяции ко всем сайтам обновления для поиска требуемого ПО".
* При первом запуске нужно загрузить BSL LS. Для этого открываем настройки `Окно` -> `Параметры` и закладку `Коннектор BSLLS`. Автоматически будет запущено задание "Загрузка BSL LS" (в каталог `%USER_HOME%/.bsl-connector-for-edt/bsl-language-server`).

Теперь при открытии модуля будет запущена проверка кода, в том числе с помощью BSL LS. Поиск файла `.bsl-language-server.json` (для настройки BSL LS) ведется в каталоге проекта workspace.

## Разработчикам
### Локальная сборка плагина на Windows

Учитывая при сборке lombok (https://projectlombok.org/setup/ecj), порядок действий из каталога `build` следующий:

1. Очищаем переменную среды MAVEN_OPTS от javaagent (пункт 3)

```
set MAVEN_OPTS=
```

2. Скачиваем lombok:

```
mvn clean dependency:copy@get-lombok
```

3. Назначаем javaagent в переменных среды

```
set MAVEN_OPTS=-javaagent:target/lombok.jar=ECJ
```

4. Проверяем и собираем проект

```
mvn verify -PSDK,find-bugs -Dtycho.localArtifacts=ignore
```