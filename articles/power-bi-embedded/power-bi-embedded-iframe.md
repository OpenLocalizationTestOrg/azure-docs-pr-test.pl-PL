---
title: "Power BI Embedded z POZOSTAŁĄ toouse aaaHow | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Power BI Embedded z REST "
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a>Jak toouse Power BI Embedded z REST

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a>Power BI Embedded: Co to jest i co to jest

Omówienie Power BI Embedded jest opisana w oficjalne hello [Power BI Embedded lokacji](https://azure.microsoft.com/services/power-bi-embedded/), ale Spójrzmy szybkie przed uzyskujemy hello uzyskać szczegółowe informacje o użyciu REST.

Jest bardzo proste naprawdę. może być wizualizacje danych dynamicznych hello toouse [usługi Power BI](https://powerbi.microsoft.com) w swojej aplikacji.

Większość aplikacji niestandardowych potrzebują toodeliver hello danych do ich własnych klientów, niekoniecznie użytkowników w ich własnej organizacji. Na przykład jeśli programową niektóre usługi dla firmy A i B firmy, użytkownicy w firmie, A powinien przeglądać tylko te dane własnych firmy A. Oznacza to wielodostępność hello jest potrzebne w celu dostarczania hello.

Hello niestandardową aplikację może również oferty własnej metody uwierzytelniania, takie jak uwierzytelnianie formularzy, uwierzytelnianie podstawowe, itp... Następnie hello osadzanie rozwiązania należy współpracować z tej metody uwierzytelniania bezpiecznie. Jest również dla użytkowników toobe stanie toouse tych aplikacji niezależnego dostawcy oprogramowania bez hello dodatkowe zakupu lub korzystania z subskrypcji usługi Power BI.

 **Power BI Embedded** zaprojektowano pod kątem dokładnie tego rodzaju scenariusze. Tak teraz, gdy mamy tego szybkie wprowadzenie poza sposób hello Załóż do niektórych szczegółów

Można użyć hello .NET \(C#) lub Node.js SDK, tooeasily skompilować aplikację z Power BI Embedded. Jednak w tym artykule wyjaśniamy o przepływie HTTP \(z uwzględnieniem uwierzytelniania) z usługi Power BI bez zestawów SDK. Opis tego przepływu, można skompilować aplikację **z żadnego języka programowania**, i można zrozumieć głęboko właśnie hello Power BI Embedded.

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a>Tworzenie usługi Power BI kolekcji obszarów roboczych i klucz dostępu get \(inicjowania obsługi administracyjnej)

Power BI Embedded jest jednym z hello usług platformy Azure. Tylko hello niezależnego dostawcy oprogramowania, który korzysta z portalu Azure są naliczane opłaty dotyczące opłaty za użycie \(co godzinę sesji użytkownika), i użytkownik hello widoków hello raport nie obciążona lub nawet wymagają subskrypcji platformy Azure.
Przed rozpoczęciem rozwój aplikacji, możemy utworzyć hello **kolekcji obszarów roboczych usługi Power BI** przy użyciu portalu Azure.

Każdego obszaru roboczego programu Power BI Embedded jest obszarem roboczym powitania dla poszczególnych klientów (dzierżawców), a można dodać wiele obszarów roboczych w każdej kolekcji obszarów roboczych. Witaj, tym samym kluczem dostępu jest używana w każdej kolekcji obszarów roboczych. W efekt, kolekcji obszarów roboczych hello jest hello granicy zabezpieczeń Power BI Embedded.

![](media/power-bi-embedded-iframe/create-workspace.png)

Gdy trwa tworzenie kolekcji obszarów roboczych hello, skopiuj klucz dostępu hello z portalu Azure.

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> Możemy również udostępnić hello kolekcji obszarów roboczych i uzyskiwanie dostępu do klucza za pomocą interfejsu API REST. toolearn więcej, zobacz [Power BI zasobów dostawcy API](https://msdn.microsoft.com/library/azure/mt712306.aspx).

## <a name="create-pbix-file-with-power-bi-desktop"></a>Utwórz plik pbix z Power BI Desktop

Następnie możemy utworzyć hello połączenie danych i raportów toobe osadzonych.
Dla tego zadania nie jest dostępna programowania ani kodu. Używamy właśnie Power BI Desktop.
W tym artykule, nie możemy przejść przez hello szczegółowe informacje na temat toouse Power BI Desktop. Aby uzyskać niektóre pomoc w tym miejscu, zobacz [wprowadzenie Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/). W naszym przykładzie tylko użyjemy hello [Retail Analysis próbki](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a>Tworzenie obszaru roboczego usługi Power BI

Teraz, gdy hello Inicjowanie obsługi wszystkich czynności Rozpocznijmy Tworzenie obszaru roboczego klienta w kolekcji obszarów roboczych hello za pośrednictwem interfejsów API REST. Hello następujące HTTP POST żądania (REST) jest utworzenie nowego obszaru roboczego hello w naszym istniejącej kolekcji obszarów roboczych. Jest to hello [POST obszaru roboczego API](https://msdn.microsoft.com/library/azure/mt711503.aspx). W naszym przykładzie nazwa kolekcji obszaru roboczego hello jest **mypbiapp**. Firma Microsoft hello klawisz dostępu, które możemy wcześniej skopiować, Ustaw jako **AppKey**. Jest bardzo prosty uwierzytelniania!

**Żądania HTTP**

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

**Odpowiedź HTTP**

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

Witaj zwrócił **workspaceId** służy do powitania po kolejnych wywołań interfejsu API. Naszej aplikacji muszą zachować tę wartość.

## <a name="import-pbix-file-into-hello-workspace"></a>Importowanie pliku pbix do obszaru roboczego hello

Każdy raport w obszarze roboczym odpowiada tooa pojedynczy plik Power BI Desktop z zestawu danych \(w tym ustawienia źródła danych). Można zaimportować naszych pbix pliku toohello obszaru roboczego jak pokazano w poniższym kodzie hello. Jak widać, można przekazać hello binarną plików pbix przy użyciu wiadomości wieloczęściowej MIME w protokole http.

fragmentu identyfikatora uri Hello **32960a09-6366-4208-a8bb-9e0678cdbb9d** hello workspaceId, a parametr zapytania **datasetDisplayName** jest toocreate nazwę zestawu danych hello. Hello utworzony zestaw danych zawiera wszystkie dane związane z artefaktów w pliku pbix, takich jak importowanych danych hello źródła danych toohello wskaźnika itp...

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

To zadanie importu może działać przez pewien czas. Po zakończeniu naszej aplikacji można zadawać hello stanu zadania za pomocą identyfikatora importu. W naszym przykładzie jest identyfikator importu hello **4eec64dd-533b-47c3-a72c-6508ad854659**.

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

następujące Hello jest zapytaniem stanu przy użyciu tego identyfikatora importu:

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

Jeśli zadanie hello nie jest pełną, hello odpowiedzi HTTP może być następująco:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

Jeśli hello zadanie zostało zakończone, hello odpowiedzi HTTP może być więcej następująco:

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a>Źródła danych połączenia \(i wielodostępność danych)

Gdy prawie wszystkie artefakty hello w pliku pbix są importowane do naszej obszar roboczy, nie są hello poświadczenia dla źródeł danych. W rezultacie, korzystając z **trybu zapytania bezpośredniego**, hello osadzonego raportu nie można wyświetlić poprawnie. Jednak przy użyciu **trybu importu**, możemy wyświetlić hello raportu przy użyciu hello istniejących importowanych danych. W takim przypadku możemy ustawić poświadczenia hello przy użyciu hello za pośrednictwem wywołania REST wykonaj następujące kroki.

Firma Microsoft musi najpierw Pobierz hello gateway datasource. Wiemy, zestaw danych hello **identyfikator** jest hello wcześniej zwróciła identyfikator.

**Żądania HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

**Odpowiedź HTTP**

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

Przy użyciu hello zwrócony identyfikator bramy i identyfikator źródła danych \(Zobacz poprzednie hello **gatewayId** i **identyfikator** w hello zwrócił wynik), firma Microsoft hello poświadczenia tego źródła danych można zmienić w następujący sposób:

**Żądania HTTP**

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

**Odpowiedź HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

W środowisku produkcyjnym możemy ustawić hello ciąg innego połączenia dla każdego obszaru roboczego przy użyciu interfejsu API REST. \(tj, można oddzielić hello bazy danych dla poszczególnych odbiorców.)

następujące Hello jest zmiana hello parametry połączenia źródła danych za pośrednictwem interfejsu REST.

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

Możemy użyć zabezpieczenia na poziomie wiersza w usłudze Power BI Embedded, a można oddzielić hello danych dla poszczególnych użytkowników w jednym raporcie. As a result, umożliwia obsługę każdego klienta raportu o tej samej pbix \(interfejsu użytkownika, itp.) i różnych źródeł danych.

> [!NOTE]
> Jeśli używasz **trybu importu** zamiast **trybu zapytania bezpośredniego**, żadnych modeli toorefresh sposób za pomocą interfejsu API nie istnieje. I lokalnych źródeł danych za pośrednictwem bramy usługi Power BI nie jest jeszcze obsługiwana w usłudze Power BI Embedded. Jednak naprawdę należy tookeep oka na powitania [blogu usługi Power BI](https://powerbi.microsoft.com/blog/) nowości i wkrótce w przyszłych wersjach.

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a>Uwierzytelnianie i hosting (osadzania) raportów w naszej strony sieci web

W hello poprzedniej interfejsu API REST, możemy użyć klucza dostępu hello **AppKey** siebie jako hello nagłówek autoryzacji. Ponieważ te wywołania można obsłużyć po stronie serwera wewnętrznej bazy danych hello, jest bezpieczne.

Ale możemy osadzenia raportu hello w naszej strony sieci web, czy obsługiwane tego rodzaju informacje dotyczące zabezpieczeń przy użyciu języka JavaScript \(frontonu). Następnie wartość nagłówka uwierzytelnienia hello musi być zabezpieczona. Nasze klucz dostępu po odnalezieniu przez złośliwego użytkownika lub złośliwy kod, po wywołują wszystkie operacje przy użyciu tego klucza.

Możemy osadzić raport hello w naszą stronę sieci web, możemy należy używać tokenu obliczona hello zamiast klucza dostępu **AppKey**. Naszej aplikacji należy utworzyć hello OAuth Json Web Token \(JWT) który składa się z hello oświadczeń i hello obliczona podpisu cyfrowego. Jak przedstawiono poniżej, to JWT OAuth jest tokeny rozdzielanych kropkami zaszyfrowanym ciągiem.

![](media/power-bi-embedded-iframe/oauth-jwt.png)

Firma Microsoft musi najpierw przygotować wartości wejściowej hello, który jest podpisany później. Ta wartość jest ciągiem zakodowane w adresie url (rfc4648) base64 hello hello następującego formatu json, a te są rozdzielane kropka hello \(.) znaków. Później wyjaśniamy sposób tooget hello identyfikator raportu.

> [!NOTE]
> Jeśli chcemy toouse wiersza poziom zabezpieczeń kontrola dostępu z Power BI Embedded, firma Microsoft musi również określać **username** i **ról** hello oświadczenia.

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

Następnie należy utworzyć ciąg kodowany w standardzie base64 hello HMAC \(hello podpisu) z algorytm SHA256. Ta podpisem wartość wejściowa jest poprzedni ciąg hello.

Ostatnio, musi połączono wartości wejściowej hello ciągu podpisu za pomocą okres \(.) znaków. ciąg Hello ukończone jest tokenu aplikacji hello do osadzania raportu hello. Nawet jeśli tokenu aplikacji hello został odnaleziony przez złośliwego użytkownika, nie mogą przejść hello oryginalnego klucza dostępu. Ten token aplikacji wygaśnie szybko.

Oto przykład PHP następujące kroki:

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is hello apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-hello-report-into-hello-web-page"></a>Na koniec osadzanie raportu hello w hello strony sieci web

Do osadzania raportu naszych, będziemy mieć hello osadzić raport i adres url **identyfikator** przy użyciu powitania po interfejsu API REST.

**Żądania HTTP**

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

**Odpowiedź HTTP**

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

Możemy osadzić raport hello w naszej aplikacji sieci web przy użyciu poprzedniej tokenu aplikacji hello.
Jeśli przyjrzymy hello dalej przykładowy kod jest hello jak w poprzednim przykładzie hello hello wcześniejsze części. W dalszej części hello, w tym przykładzie pokazano hello **embedUrl** \(zobacz poprzedni wynik hello) w hello elementu iframe i jest przesyłanie tokenu aplikacji hello na powitania iframe.

> [!NOTE]
> Będziesz potrzebować toochange hello raportu identyfikator wartość tooone własny. Ponadto powodu tooa usterkę w naszym systemie zarządzania zawartością, hello tag iframe w przykładowym kodzie hello jest do odczytu jako literału. Usunięcie tekst hello ograniczone z tagu hello skopiuj i wklej ten przykładowy kod.

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

A Oto nasze wyników:

![](media/power-bi-embedded-iframe/view-report.png)

W tej chwili Power BI Embedded wyświetla tylko hello raportu w hello iframe. Jednak śledzą hello [Power BI blogu](https://powerbi.microsoft.com/blog/). Przyszłe ulepszenia można używać po stronie klienta nowych interfejsów API, które będą Daj nam wysyłania informacji do hello iframe, a także otrzymywać. Ciekawe rzeczy!

## <a name="see-also"></a>Zobacz też
* [Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)

Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)

