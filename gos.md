# Документация API

## Доступ в admin
**Прямая ссылка:** _https://api.govcarpets.ru_
(P.S -> redirect _admin_) 

**Логин:** _GovAddcarRf_

**Пароль:** _g@!2009rf_


# Эндпоинт: Получение преимуществ и фото дорожек

Этот эндпоинт предоставляет список преимуществ и связанных с ними фотографий ковровых дорожек.

**Метод:** `GET`

**Параметры Метода:** `отсутствуют`

**URL:** `/api/v1/advantages/`

**Конечная ссылка:** `https://api.govcarpets.ru/get-api/advantages`

#### Описание
Эндпоинт возвращает два набора данных:
1. Список преимуществ ковровых дорожек, отсортированных по порядковому номеру.
2. Список фотографий ковровых дорожек.


Данные собираются параллельно, что позволяет повысить производительность и уменьшить время ожидания.

#### Пример запроса

```json
{
  "status": "success",
  "data": {
    "list": [
      {
        "carpet_runners__title": "Название преимущества",
        "description": "Описание преимущества"
      }
    ],
    "photos": [
      {
        "title": "Название фото",
        "photo_path": "https://example.com/media/photo.jpg"
      }
    ]
  }
}
```

## Раздел - Информация компании (footer)

**Прямая ссылка:** _https://api.govcarpets.ru/get-api/footer-info_

**Тип запроса:** _GET_

**Параметры GET:** _отсутствуют_

**Описание:** _Ключ "file_doc_path" если файл отсутсвует, значение будет пустым_

![Изображение](https://i.postimg.cc/nzSZD3S2/2024-08-26-12-55-08.png)


## ФИЛЬТР - Цветовые элементы для продуктов

**Прямая ссылка:** _https://api.govcarpets.ru/get-api/products/colors_

**Тип запроса:** _GET_

**Параметры GET:** _отсутствуют_

**Описание:** _Ключ "file_doc_path" если файл отсутсвует, значение будет пустым_

![Изображение](https://i.postimg.cc/nzSZD3S2/2024-08-26-12-55-08.png)

## ФИЛЬТР - Доступные категории

**Прямая ссылка:** _https://api.govcarpets.ru/get-api/categories_

**Тип запроса:** _GET_

**Параметры GET:** _отсутствуют_

**Описание:** _отсутствует_

![Изображение](https://i.postimg.cc/63Sk4h5F/2024-08-27-11-49-05.png)


## Акционные позиции в наличии - отображение продуктов на главной странице

**Прямая ссылка:** _https://api.govcarpets.ru/get-api/promot-items_

**Тип запроса:** _GET_

**Параметры GET:** _отсутствуют_

**Описание:** _настраивается в admin отобраение_

![Изображение](https://i.postimg.cc/nLLYPD0k/2024-08-29-16-24-58.png)


## Список продуктов

**Прямая ссылка:** _https://api.govcarpets.ru/get-api/products_

**Тип запроса:** _GET_

**Параметры GET:** _есть_

> Доступные параметры get: color, category, select_filter, page, page_size

**Описание:** _по умолчанию, если нет переданных параметров, выдится полный список продуктов с ограничениями: первая страница, 20 записей, всего показано_

![Изображение](https://i.postimg.cc/3Jncf7vB/2024-08-29-12-09-19.png)


### Получение продуктов по цвету
> http://api.govcarpets.ru/get-api/products?color=ff0000


### Получение продуктов по категории
> http://api.govcarpets.ru/get-api/products?category=2

_Чтобы узнать id категории обратитесь к api https://api.govcarpets.ru/get-api/categories_

### Получение продуктов по фильтру
> http://api.govcarpets.ru/get-api/products?select_filter=new

#### Список доступных фильтров
```python
('recommend', 'Рекомендуемые'),
('popular', 'Популярные'),
('new', 'Новые'),
('hit', 'Хиты'),
('other', 'Другое')
```

### Комбинирование параметров
> http://api.govcarpets.ru/get-api/products?color=ff0000&category=2

### Получение следующей страницы списка продуктов
> http://api.govcarpets.ru/get-api/products?page=2

### Изменить кол-во отображения продуктов
> http://api.govcarpets.ru/get-api/products?page_size=2
