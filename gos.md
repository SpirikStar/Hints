# Документация API

## Раздел - Преимущества


**Прямая ссылка:** _https://api.govcarpets.ru/get-api/advantages_

**Тип запроса:** _GET_

**Параметры GET:** _отсутствуют_

**Описание:** _Ключ "list" по умолчанию отфильтрован по порядковому номеру(порядковый номер настраивается в admin)._

![Изображение](https://i.postimg.cc/fbL7FwYW/2024-08-26-09-46-09.png)

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
