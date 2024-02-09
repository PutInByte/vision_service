## [Маршрут API для обработки медиафайлов](../../../../web/media_handler/routers.py)

Данный код определяет маршрут API с использованием FastAPI для обработки медиафайлов, таких как изображения. Маршрут позволяет загружать изображения, обрабатывать их и сохранять полученные данные в базе данных.

### Маршрут `/api/v1/vision/detect/`

Этот маршрут позволяет загружать изображения и выполнять обнаружение атрибутов автомобиля на изображении.

### Параметры маршрута:

- `service`: Зависимость `MediaFormService`, которая используется для выполнения операций с базой данных.
- `file`: Файл с изображением для обработки (обязательный параметр).

### Описание действий:

1. Проверяет тип содержимого файла, убеждается, что загруженный файл является изображением.

2. Сохраняет файл на сервере и получает URL и путь к сохраненному файлу.

3. Обрабатывает изображение с помощью функции `process_image`, получая результат в виде словаря.

4. Проверяет результат обработки изображения. Если автомобиль не был обнаружен, возвращает сообщение "Car not detected".

5. Формирует данные об автомобиле из результатов обработки изображения и сохраняет их в базе данных с использованием сервиса `MediaFormService`.

6. Возвращает JSON-ответ с данными об автомобиле.

### Обработка ошибок:

- Если тип содержимого файла не соответствует изображению, возвращает ошибку HTTP 400 с соответствующим сообщением.

- Если произошла ошибка во время выполнения, возвращает ошибку HTTP 500 с деталями ошибки.

### Пример использования:

~~~python
# Загрузка изображения и обработка данных
response = await client.post("/api/v1/vision/detect/", files={"file": ("image.jpg", image_data)})
result = response.json()
~~~