---
title: aaaLogic aplikacji limity i Konfiguracja | Dokumentacja firmy Microsoft
description: "Przegląd hello limity usług i wartości konfiguracji są dostępne dla usługi Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 739509afe5c9a7b7e946ba3571951264127e5297
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="logic-app-limits-and-configuration"></a>Limity i konfiguracja aplikacji logiki

Poniżej znajduje się informacji na temat limitów bieżącego hello oraz szczegóły dotyczące konfiguracji dla usługi Azure Logic Apps.

## <a name="limits"></a>Limity

### <a name="http-request-limits"></a>Limity żądań HTTP

Poniżej przedstawiono limity dla jednego żądania i/lub łącznika wywołania HTTP.

#### <a name="timeout"></a>Limit czasu

|Nazwa|Limit|Uwagi|
|----|----|----|
|Limit czasu żądania|120 sekund|[Wzorca asynchronicznego](../logic-apps/logic-apps-create-api-app.md) lub [do pętli](logic-apps-loops-and-scopes.md) można wyrównania w razie potrzeby|

#### <a name="message-size"></a>Rozmiar komunikatu

|Nazwa|Limit|Uwagi|
|----|----|----|
|Rozmiar komunikatu|100 MB|Niektóre łączniki i interfejsów API może nie obsługiwać 100 MB |
|Limit obliczania wyrażeń|131 072 znaków|`@concat()`, `@base64()`, `string` nie może być dłuższa niż to ograniczenie|

#### <a name="retry-policy"></a>Zasady ponawiania

|Nazwa|Limit|Uwagi|
|----|----|----|
|Liczba ponownych prób|10| Domyślna to 4. Można skonfigurować za pomocą hello [ponów parametr zasad](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|
|Spróbuj ponownie Maksymalne opóźnienie|1 godzina|Można skonfigurować za pomocą hello [ponów parametr zasad](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|
|Min. opóźnienie ponowienia próby|5 s|Można skonfigurować za pomocą hello [ponów parametr zasad](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|

### <a name="run-duration-and-retention"></a>Czas trwania testu i przechowywania

Poniżej przedstawiono limity hello aplikacji logiki pojedynczego uruchomienia.

|Nazwa|Limit|Uwagi|
|----|----|----|
|Czas trwania testu|90 dni||
|Magazyn przechowywania|90 dni|Począwszy od hello czas rozpoczęcia wykonywania|
|Interwał cyklu min|1 s|| 15 sekund dla aplikacji logiki z planu usługi App Service
|Maksymalny interwał cyklu|500 dni||

Jeśli planujesz tooexceed Uruchom czasu trwania lub magazynu limity przechowywania przepływu normalnego przetwarzania [skontaktuj się z nami](mailto://logicappsemail@microsoft.com) , dzięki czemu możemy pomóc z wymaganiami.


### <a name="looping-and-debatching-limits"></a>Powtarzanie i debatching limity

Poniżej przedstawiono limity aplikacji logiki pojedynczego uruchomienia.

|Nazwa|Limit|Uwagi|
|----|----|----|
|Elementy ForEach|100,000|Można użyć hello [zapytania akcji](../connectors/connectors-native-query.md) tablice większych toofilter zgodnie z potrzebami|
|Do iteracji|5,000||
|Elementy SplitOn|100,000||
|Równoległość ForEach|50| Domyślna to 20. Można ustawić foreach sekwencyjnych tooa przez dodanie `"operationOptions": "Sequential"` toohello `foreach` działania lub określonego poziomu przy użyciu równoległości`runtimeConfiguration`|


### <a name="throughput-limits"></a>Limity przepustowości

Poniżej przedstawiono limity dla logiki pojedynczego wystąpienia aplikacji. 

|Nazwa|Limit|Uwagi|
|----|----|----|
|Wykonania akcji na 5 minut |100,000|Można rozpowszechniać obciążenia pracą wielu aplikacjom w razie potrzeby|
|Akcje równoczesnych połączeń wychodzących |~2,500|Zmniejsz liczbę jednoczesnych żądań lub Zmniejsz czas trwania hello, w razie potrzeby|
|Środowisko uruchomieniowe punktu końcowego przychodzące wywołania |~1,000|Zmniejsz liczbę jednoczesnych żądań lub Zmniejsz czas trwania hello, w razie potrzeby|
|Punkt końcowy środowiska uruchomieniowego odczytu wywołań na 5 minut |60,000|Można rozpowszechniać obciążenia pracą wielu aplikacjom w razie potrzeby|
|Punkt końcowy środowiska uruchomieniowego wywołania wywołań na 5 minut |45,000|Można rozpowszechniać obciążenia pracą wielu aplikacjom w razie potrzeby|

Jeśli planujesz tooexceed ten limit w normalnego przetwarzania lub testów obciążenia toorun chcą, która przekracza ten limit w danym okresie czasu, [skontaktuj się z nami](mailto://logicappsemail@microsoft.com) , dzięki czemu możemy pomóc z wymaganiami.

### <a name="definition-limits"></a>Limity definicji

Poniżej przedstawiono limity dla definicji aplikacji logiki pojedynczego.

|Nazwa|Limit|Uwagi|
|----|----|----|
|Akcje dla przepływu pracy|500|Tooextend zagnieżdżonych przepływów pracy można dodać ten limit, w razie potrzeby|
|Dozwolona liczba poziomów zagnieżdżenia akcji|8|Tooextend zagnieżdżonych przepływów pracy można dodać ten limit, w razie potrzeby|
|Przepływy pracy na region na subskrypcję|1000||
|Wyzwalaczy na przepływu pracy|10||
|Limit przypadków zakresu przełącznika|25||
|Liczba zmiennych dla przepływu pracy|250||
|Maksymalna liczba znaków w wyrażeniu|8192||
|Maksymalna liczba `trackedProperties` w znakach rozmiarze|16,000|
|`action`/`trigger`limit nazwy|80||
|`description`limit długości|256||
|`parameters`limit|50||
|`outputs`limit|10||

### <a name="integration-account-limits"></a>Limity konta integracji

Oto limity artefakty dodane toointegration konta

|Nazwa|Limit|Uwagi|
|----|----|----|
|Schemat|8 MB|Można użyć [identyfikator URI obiektu blob](logic-apps-enterprise-integration-schemas.md) tooupload pliki o rozmiarze większym niż 2 MB |
|Mapy (plik XSLT)|2 MB| |
|Punkt końcowy środowiska uruchomieniowego odczytu wywołań na 5 minut |60,000|Można rozdzielania pracy między wiele kont w razie potrzeby|
|Punkt końcowy środowiska uruchomieniowego wywołania wywołań na 5 minut |45,000|Można rozdzielania pracy między wiele kont w razie potrzeby|
|Punkt końcowy środowiska uruchomieniowego śledzenia wywołań na 5 minut |45,000|Można rozdzielania pracy między wiele kont w razie potrzeby|
|Punkt końcowy środowiska uruchomieniowego blokuje równoczesnych wywołań |~1,000|Zmniejsz liczbę jednoczesnych żądań lub Zmniejsz czas trwania hello, w razie potrzeby|

### <a name="b2b-protocols-as2-x12-edifact-message-size"></a>Rozmiar wiadomości protokoły B2B (AS2, X12, EDIFACT)

Poniżej przedstawiono limity hello protokoły B2B

|Nazwa|Limit|Uwagi|
|----|----|----|
|AS2|50 MB|Zastosowanie toodecode i kodowania|
|X12|50 MB|Zastosowanie toodecode i kodowania|
|EDIFACT|50 MB|Zastosowanie toodecode i kodowania|

## <a name="configuration"></a>Konfiguracja

### <a name="ip-address"></a>Adres IP

#### <a name="logic-app-service"></a>Usługi aplikacji logiki

Wywołania wykonane bezpośrednio z aplikacji logiki (oznacza to, za pomocą [HTTP](../connectors/connectors-native-http.md) lub [HTTP + Swagger](../connectors/connectors-native-http-swagger.md)) lub innych żądaniach HTTP pochodzą z hello adresu IP określonego w hello następującej listy:

|Region aplikacji logiki|Wychodzącego|
|-----|----|
|Australia Wschodnia|13.75.153.66, 104.210.89.222, 104.210.89.244, 13.75.149.4, 104.210.91.55, 104.210.90.241|
|Australia Południowo-Wschodnia|13.73.115.153, 40.115.78.70, 40.115.78.237, 13.73.114.207, 13.77.3.139, 13.70.159.205|
|Brazylia Południowa|191.235.86.199, 191.235.95.229, 191.235.94.220, 191.235.82.221, 191.235.91.7, 191.234.182.26|
|Kanada Środkowa|52.233.29.92, 52.228.39.241, 52.228.39.244|
|Kanada Wschodnia|52.232.128.155, 52.229.120.45, 52.229.126.25|
|Indie Środkowe|52.172.157.194, 52.172.184.192, 52.172.191.194, 52.172.154.168, 52.172.186.159, 52.172.185.79|
|Środkowe stany USA|13.67.236.76, 40.77.111.254, 40.77.31.87, 13.67.236.125, 104.208.25.27, 40.122.170.198|
|Azja Wschodnia|168.63.200.173, 13.75.89.159, 23.97.68.172, 13.75.94.173, 40.83.127.19, 52.175.33.254|
|Wschodnie stany USA|137.135.106.54, 40.117.99.79, 40.117.100.228, 13.92.98.111, 40.121.91.41, 40.114.82.191|
|Wschodnie stany USA 2|40.84.25.234, 40.79.44.7, 40.84.59.136, 40.84.30.147, 104.208.155.200, 104.208.158.174|
|Japonia Wschodnia|13.71.146.140, 13.78.84.187, 13.78.62.130, 13.71.158.3, 13.73.4.207, 13.71.158.120|
|Japonia Zachodnia|40.74.140.173, 40.74.81.13, 40.74.85.215, 40.74.140.4, 104.214.137.243, 138.91.26.45|
|Środkowo-północne stany USA|168.62.249.81, 157.56.12.202, 65.52.211.164, 168.62.248.37, 157.55.210.61, 157.55.212.238|
|Europa Północna|13.79.173.49, 52.169.218.253, 52.169.220.174, 40.113.12.95, 52.178.165.215, 52.178.166.21|
|Środkowo-południowe stany USA|13.65.98.39, 13.84.41.46, 13.84.43.45, 104.210.144.48, 13.65.82.17, 13.66.52.232|
|Azja Południowo-Wschodnia|52.163.93.214, 52.187.65.81, 52.187.65.155, 13.76.133.155, 52.163.228.93, 52.163.230.166|
|Indie Południowe|52.172.9.47, 52.172.49.43, 52.172.51.140, 52.172.50.24, 52.172.55.231, 52.172.52.0|
|Europa Zachodnia|13.95.155.53, 52.174.54.218, 52.174.49.6, 40.68.222.65, 40.68.209.23, 13.95.147.65|
|Indie Zachodnie|104.211.164.112, 104.211.165.81, 104.211.164.25, 104.211.164.80, 104.211.162.205, 104.211.164.136|
|Zachodnie stany USA|52.160.90.237, 138.91.188.137, 13.91.252.184, 52.160.92.112, 40.118.244.241, 40.118.241.243|
|Południowe Zjednoczone Królestwo|51.140.74.14, 51.140.73.85, 51.140.78.44|
|Zachodnie Zjednoczone Królestwo|51.141.54.185, 51.141.45.238, 51.141.47.136|

#### <a name="connectors"></a>Łączniki

Wywołania z [łącznik](../connectors/apis-list.md) pochodzą z hello adresu IP określonego w hello następującej listy:

|Region aplikacji logiki|Wychodzącego|
|-----|----|
|Australia Wschodnia|40.126.251.213|
|Australia Południowo-Wschodnia|40.127.80.34|
|Brazylia Południowa|191.232.38.129|
|Kanada Środkowa|52.233.31.197, 52.228.42.205, 52.228.33.76, 52.228.34.13|
|Kanada Wschodnia|52.229.123.98, 52.229.120.178, 52.229.126.202, 52.229.120.52|
|Indie Środkowe|104.211.98.164|
|Środkowe stany USA|40.122.49.51|
|Azja Wschodnia|23.99.116.181|
|Wschodnie stany USA|191.237.41.52|
|Wschodnie stany USA 2|104.208.233.100|
|Japonia Wschodnia|40.115.186.96|
|Japonia Zachodnia|40.74.130.77|
|Środkowo-północne stany USA|65.52.218.230|
|Europa Północna|104.45.93.9|
|Środkowo-południowe stany USA|104.214.70.191|
|Azja Południowo-Wschodnia|13.76.231.68|
|Indie Południowe|104.211.227.225|
|Europa Zachodnia|40.115.50.13|
|Indie Zachodnie|104.211.161.203|
|Zachodnie stany USA|104.40.51.248|
|Południowe Zjednoczone Królestwo|51.140.80.51|
|Zachodnie Zjednoczone Królestwo|51.141.47.105|


## <a name="next-steps"></a>Następne kroki  

- tooget pracy z usługą Logic Apps, wykonaj hello [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) samouczka.  
- [Wyświetlanie typowych przykładów i scenariuszy](../logic-apps/logic-apps-examples-and-scenarios.md)
- [Dzięki usłudze Logic Apps możesz automatyzować procesy biznesowe](http://channel9.msdn.com/Events/Build/2016/T694) 
- [Dowiedz się, jak tooIntegrate systemy z usługą Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
