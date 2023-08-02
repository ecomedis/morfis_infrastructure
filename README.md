На GitHub планируется поддерживать 3 репозитория:

* **morfis_frontend**
* **morfis_backend**
* **morfis_docker**: будет использоваться для сборки проектов и скриптов автоматизации

Для `morfis_frontend` и `morfis_backend` планируется вести по 3 ветки:

* **DEV**
* **TEST**
* **PROD**

Предполагаемый поток кода по веткам:

1. В `dev` должны сливаться ветки с фичами по текущим задачам.
2. По каждому `push` или `merge` должны собираться image `morfis_backend:dev` или `morfis_frontend:dev` и деплоится на DEV сервер.
3. При необходимости может происходить test-релиз. При этом:
   * Должен ставиться `tag` коммиту ветки `dev`.
   * Код из ветки `dev` должен вливаться в ветку `test`.
   * Из ветки `test` должен строиться образ `morfis:test_{version}`. ***(Есть вопрос с организацией репозиториев для данный задачи)***
   * Из этих образов может запускаться неограниченное количество инстансов для проведения различных тестов.
   * Из ветки `test` код не может быть влит обратно в ветку `dev`.
4. При необходимости может происходить prod-релиз. При этом:
   * Должен ставиться `tag` коммиту ветки `test`.
   * Код из ветки `test` должен вливаться в ветку `prod`.
   * Из ветки `prod` должны строиться образы `morfis:prod_{version}`.  ***(Есть вопрос с организацией репозиториев для данный задачи)***

Итого требуются следующие площадки окружения:

* **DEV**.
* **TEST**: может подниматься с тестовыми данными (возможно, с подстановкой кастомных данных). **(Может быть несколько инстансов для запуска раличных тестов)**
* **PROD**: должен подниматься с тестовыми данными.
* **hub.morfis.ru**: репозиторий для хранения docker образов.
* **morfis.ru**: Демонстрационная версия, использовавшаяся для регистрации ПО. Пока планируется ее сохранить.

[Текущая схема организации инфраструктуры проекта morfis.](https://docs.google.com/drawings/d/1XzawCGajSu-M3E8ad7kEOzBWZUF6RxCC4U-uQkG-dfs/edit)

[Предполагаемая схема организации инфраструктуры проекта morfis.](https://docs.google.com/drawings/d/1KnaGMoC8A9a04N9IMFO9um5lylW4LhV_6VI_r7ImhMI/edit)
