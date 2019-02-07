# CRM-YII1-MySQL
WebServices-YII1-MySQL
Задача: получать данные (GetSupply) с торгового сервера с помощью "веб-сервисов" и затем разместить заказ на покупку (PutOrder) на выбранную позицию.
Объём получаемых в SupplyResponse по SupplyRequest данных: 25+ тыс. позиций, 300+ Мбайт.
Структура запрашиваемых и отправляемых данных описана в WSDL и имеет сложную струтуру (до 7 уровней иерархии и т.д.). 
- Размер описания WSDL для SupplyRequest - 44.5 kB.
- Размер описания WSDL для SupplyResponse - 12.2 kB.

Из за сложности описаний WSDL, PHP SoapClient не смог обеспечить решение этой задачи.
Предлагаемое (реализованное) решение:
- использовать для формирования корректного (работающего) синтаксиса запроса пакет SoapUI.
- сформированный в SoapUI разместить как текстовую строку, в переменную "$xml_post_string" и затем использовать её в "curl_init()", опция "curl_setopt($ch, CURLOPT_POSTFIELDS, $xml_post_string)" 
- затем используя "curl_exec" получить ответ с удалённого сервера, преобразовать (с помощью "xml_parser") полученный ответ в формат массива, затем аккуратного его разобрать и записать полученные данные в соответствующие таблицы БД.
 
