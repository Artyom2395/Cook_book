# Поварская книга на Django

Это приложение "Поварская книга" разработано на фреймворке Django. Оно позволяет управлять рецептами и продуктами, а также отслеживать использование продуктов в рецептах.

## Основные Функции

- **Добавление продуктов и рецептов**: Пользователи могут добавлять продукты и рецепты в базу данных.
- **Добавление продуктов в рецепты**: Пользователи могут добавлять продукты к рецептам, указывая их вес.
- **Приготовление блюд**: Функция для учета количества раз, когда продукт был использован в приготовлении блюд.
- **Просмотр рецептов без определенного продукта**: Возможность просмотра рецептов, в которых определенный продукт отсутствует или его содержание менее 10 грамм.

## Технологии

- **Backend**: Django
- **Database**: SQLite (можно заменить на другую СУБД, поддерживаемую Django, проект мини, поэтому выбрана эта СУБД)

## Установка и Запуск

Чтобы запустить проект локально, выполните следующие шаги:

1. Клонировать репозиторий:
```
git clone <URL репозитория>
``` 
Шаг 3: Перейдите в каталог проекта
Перейдите в каталог вашего проекта:
```
cd <название-каталога-проекта>
```
2. Установить зависимости:
```
pip install -r requirements.txt
```
3. Выполнить миграции:
```
python manage.py migrate
```
4. Создать суперпользователя для доступа к админ-панели:
```
python manage.py createsuperuser
```
Данные для суперпозователя этого проекта
username: UserAdmin
password: Admin343

5. Основные запросы для проверки рабоыт проекта 
- http://localhost:8000/add_product_to_recipe/?recipe_id=1&product_id=1&weight=150 - Добавляет продукт к рецепту или обновляет его вес, если продукт уже присутствует в рецепте.
- http://127.0.0.1:8000/cook_recipe/?recipe_id=2 - Увеличивает счетчик использования каждого продукта, входящего в состав указанного рецепта.
- http://127.0.0.1:8000/show_recipes_without_product/?product_id=2 - Отображает страницу с рецептами, где указанный продукт отсутствует или присутствует в количестве менее 10 грамм.

## Комментарий по построению структуры БД:
Для связки двух таблиц была использована промежуточная таблица RecipeProduct

1.	Мы не можем напрямую добавить информацию о весе продукта в модель Recipe, потому что каждый продукт в рецепте имеет уникальный вес. Если мы храним вес в модели Recipe, это будет предполагать, что все продукты в рецепте имеют одинаковый вес, что не соответствует действительности.
2.	Использование промежуточной модели позволяет нормализовать данные. Это означает, что каждая единица информации хранится только один раз. Например, информация о продукте хранится в модели Product, а информация о рецепте — в модели Recipe. Промежуточная модель RecipeProduct связывает эти две сущности, сохраняя при этом уникальную информацию о весе продукта в каждом конкретном рецепте.
3.	Использование промежуточной модели также обеспечивает большую гибкость. Если в будущем мы захотим добавить дополнительные атрибуты к связи между рецептом и продуктом (например, способ обработки продукта), это будет проще сделать, расширив модель RecipeProduct.
