# REST API

(Интерфейс — граница между двумя отдельными системами, через которую они взаимодействуют, требования к которой определяются 
стандартом)

__`API (Application Programming Interface)`__  — это интерфейс программирования, 
интерфейс создания приложений.

API - это программный интерфейс, это абстрактное место (в реальности - конкретный [URL](../URI,%20URL,%20URN.md)), в который 
приходят какие-то данные, с которыми мы можем что-то делать.

Под ***API*** практически всегда будет подразумеваться ***REST API*** - для нас это - 
**endpoint** (урл на который можно отправить запрос), который выполняет какие-либо действия, 
или возвращает нам какую либо информацию.

__`REST`__ - (Representational State Transfer — «передача состояния представления») — по сути,
это ***архитектурный стиль*** (рекомендации к разработке, идея того, как мы должны туда-суда бросаться данными).

REST представляет собой согласованный набор ограничений, учитываемых при проектировании распределённой гипермедиа-системы.

### Свойства REST архитектуры
Свойства архитектуры зависят от ограничений, наложенных на REST-системы:

1. __`Client-Server`__ <br>
Система должна быть разделена на **"клиенты"** и на **"сервер(ы)"**.<br>
Разделение интерфейсов означает, что, например, ***клиенты не связаны с хранением данных***, 
которое остается внутри каждого сервера, так что мобильность кода клиента улучшается.<br>
Серверы ***не связаны с интерфейсом пользователя или состоянием***, так что серверы могут быть 
проще и масштабируемы.<br>
Серверы и клиенты могут быть заменяемы и разрабатываться независимо, 
пока интерфейс не изменяется.

2. __`Stateless`__ <br>
Сервер не должен хранить какой-либо информации о клиентах. <br>
В запросе должна храниться ***вся необходимая информация*** для обработки запроса 
и если необходимо, идентификации клиента.

3. __`Cache`__<br>
Каждый ответ должен быть отмечен является ли он кэшируемым или нет, 
для предотвращения повторного использования клиентами устаревших или 
некорректных данных в ответ на дальнейшие запросы.

4. __`Uniform Interface`__<br>
Единый интерфейс определяет интерфейс между клиентами и серверами.<br>
Мы договариваемся в каком формате будем обмениваться данными. <br>
Это упрощает и отделяет архитектуру, которая позволяет каждой части развиваться самостоятельно.
 Четыре принципа единого интерфейса:

   4.1) __`Identification of resources`__ (основан на ресурсах).<br> В REST **ресурсом** является все то, чему можно дать имя.
   <br> Например, пользователь, изображение, предмет (майка, голодная собака, текущая погода) и т.д. <br> ***Каждый ресурс*** в REST
   должен быть ***идентифицирован*** посредством стабильного идентификатора, который не меняется при изменении состояния
   ресурса. <br> Идентификатором в REST является [URI](../URI,%20URL,%20URN.md).

   4.2) __`Manipulation of resources through representations`__ (Манипуляции над ресурсами через представления).<br>
    Всегда обращаем в один и тот же формат. Мало того, что есть отдельный URL, должен быть общедоговоренный формат (отправили Json - получили Json).
   Представление в REST используется для выполнения действий над ресурсами. <br> Представление ресурса представляет собой
   текущее или желаемое состояние ресурса. <br> Например, если ресурсом является пользователь, то представлением может
   являться XML или HTML описание этого пользователя.

   4.3) __`Self-descriptive messages`__ (само-документируемые сообщения)<br> Под само-описательностью имеется ввиду, что
   запрос и ответ должны хранить в себе ***всю необходимую информацию*** для их обработки. <br> Не должны быть дополнительные
   сообщения или кэши для обработки одного запроса. <br> Другими словами отсутствие состояния, сохраняемого между запросами к
   ресурсам. <br> Это очень важно для масштабирования системы.

   4.4) __`HATEOAS (hypermedia as the engine of application state`__. <br> Статус ресурса передается через содержимое body,
   параметры строки запроса, заголовки запросов и запрашиваемый URI (имя ресурса). <br> Это называется гипермедиа (или
   гиперссылки с гипертекстом). <br> HATEOAS также означает, что, в случае необходимости ссылки могут содержаться в теле
   ответа (или заголовках) для поддержки URI, извлечения самого объекта или запрошенных объектов.

5. __`Layered System`__ <br> В REST допускается разделить систему на иерархию слоев, но с условием, что каждый компонент может
   видеть компоненты только непосредственно следующего слоя. <br> Например, если вы вызываете службу PayPal, а он в свою
   очередь вызывает службу Visa, вы о вызове службы Visa ничего не должны знать.

6. __`Code-On-Demand`__ (опционально). <br> В REST позволяется загрузка и выполнение кода или программы на стороне клиента.

Если выполнены первые 4 пункта и не нарушены 5 и 6, такое приложение называется ***RESTful***

**Важно!** Сама архитектура REST не привязана к конкретным технологиям и протоколам, но в реалиях современного Веб,
построение RESTful API почти всегда подразумевает использование HTTP и каких-либо распространенных форматов
представления ресурсов, например JSON, или, менее популярного сегодня, XML.

### Идемпотентность

С точки зрения RESTful-сервиса, операция (или вызов сервиса) ***идемпотентна*** тогда, когда клиенты могут делать один и тот
же вызов неоднократно при одном и том же результате на сервере. 

Другими словами, создание большого количества идентичных
запросов имеет такой же эффект, как и один запрос. 

Заметьте, что в то время, как идемпотентные операции производят один
и тот же результат на сервере, ответ сам по себе может не быть тем же самым (например, состояние ресурса может
измениться между запросами).

Методы PUT и DELETE по определению идемпотентны. Тем не менее, есть один нюанс с методом DELETE. Проблема в том, что
успешный DELETE-запрос возвращает статус 200 (OK) или 204 (No Content), но для последующих запросов будет все время
возвращать 404 (Not Found), Состояние на сервере после каждого вызова DELETE то же самое, но ответы разные.

Методы GET, HEAD, OPTIONS и TRACE определены как безопасные. Это означает, что они предназначены только для получения
информации и не должны изменять состояние сервера. Они не должны иметь побочных эффектов, за исключением безобидных
эффектов, таких как: логирование, кеширование, показ баннерной рекламы или увеличение веб-счетчика.

По определению, безопасные операции идемпотентны, так как они приводят к одному и тому же результату на сервере.
Безопасные методы реализованы как операции только для чтения. Однако безопасность не означает, что сервер должен
возвращать тот же самый результат каждый раз.
