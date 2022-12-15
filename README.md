# Web-сервис прямого и обратного геокодирования "GeocodingService"

#### Небходимые ПО
* Docker
* Postman
* IntelliJ IDEA (в случае необходимости)

#### Используемые технологии
* Java
* Spring Boot
* Maven
* Redis (для кэширования)

#### Интеграция внешнего API: электронный справочник карт "2GIS" (Geocoder API):  ````https://docs.2gis.com/ru/api/search/geocoder/overview````

#### Инструкция по запуску приложения
1. git clone https://github.com/Meggi9/GeocodingService.git
2. В директории проекта выполнить следующие команды:

   * Сборка проекта maven: ````./mvnw package````

   * Запуск приложения (в случае необходимости): ````java -jar target/GeocodingService-0.0.1-SNAPSHOT.jar````

2. Создание образа Docker: ````docker build -t geocoding-service-docker:0.1.0 .````
5. Запуск контейнера Docker: ````docker run -p 8080:8080 geocoding-service-docker:0.1.0 .````

#### Инструкция по работе с приложением
1. Для выполнения прямого геокодирования, следует выполнить следующий GET запрос:

````localhost:8080/api/geocoder````

При этом в тело запроса передать адрес в формате JSON:
```json
{
  "address": "Адрес"
}
````

2. Для выполнения обратного геокодирования, следует выполнить следующий GET запрос:

````localhost:8080/api/geocoder````

При этом в тело запроса передать координаты в формате JSON:
```json
{
    "lat": Значение широты,
    "lon": Значение долготы
}
````
### Результаты работы приложения

1. Прямое геокодирование:

![image](https://user-images.githubusercontent.com/75883965/207918674-5923c1c5-c828-43e4-8162-2441e82966b3.png)

#### Полученный ответ (Response):

```json
{
    "result": {
        "items": [
            {
                "building_name": "Воронежский государственный технический университет (ВГТУ)",
                "full_name": "Воронеж, Воронежский государственный технический университет (ВГТУ)",
                "purpose_name": "ВУЗ",
                "name": "Воронежский государственный технический университет (ВГТУ)",
                "address_name": "20-летия Октября, 84",
                "id": "4363497794194056",
                "type": "building",
                "point": {
                    "lat": 51.652127,
                    "lon": 39.192714
                }
            }
        ],
        "total": "1"
    }
}
````

2. Обратное геокодирование:

![image](https://user-images.githubusercontent.com/75883965/207918880-24784c91-8b7f-46e7-bcf8-af60e1ae02cc.png)

#### Полученный ответ (Response):

```json
{
    "result": {
        "items": [
            {
                "building_name": "Воронежский государственный технический университет (ВГТУ)",
                "full_name": "Воронеж, Воронежский государственный технический университет (ВГТУ)",
                "purpose_name": "ВУЗ",
                "name": "Воронежский государственный технический университет (ВГТУ)",
                "address_name": "20-летия Октября, 84",
                "id": "4363497794194056",
                "type": "building",
                "point": {
                    "lat": 51.652127,
                    "lon": 39.192714
                }
            },
            {
                "full_name": "Воронеж, Ленинский",
                "subtype": "district",
                "name": "Ленинский",
                "id": "4363472024371202",
                "type": "adm_div",
                "point": {
                    "lat": 51.640025,
                    "lon": 39.194786
                }
            },
            {
                "full_name": "Воронеж",
                "subtype": "city",
                "name": "Воронеж",
                "id": "4363484909273106",
                "type": "adm_div",
                "point": {
                    "lat": 51.660548,
                    "lon": 39.199775
                }
            },
            {
                "full_name": "Воронеж городской округ",
                "subtype": "district_area",
                "name": "Воронеж городской округ",
                "id": "70030076118167065",
                "type": "adm_div",
                "point": {
                    "lat": 51.61521,
                    "lon": 39.193904
                }
            },
            {
                "full_name": "Воронежская область",
                "subtype": "region",
                "name": "Воронежская область",
                "id": "1267655302447150",
                "type": "adm_div",
                "point": {
                    "lat": 51.134329,
                    "lon": 40.022274
                }
            }
        ],
        "total": "5"
    }
}
````
