---
title: "aaaEmbed raportu w usłudze Azure Power BI Embedded | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooembed raport, który znajduje się w usłudze Power BI Embedded do aplikacji."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a>Osadzanie raportu w usłudze Power BI Embedded

Dowiedz się, jak tooembed raport, który znajduje się w usłudze Power BI Embedded do aplikacji.

Przedstawiono sposób tooactually osadzanie raportu w aplikacji. Jest to zakładając, że masz już raport, który istnieje w obszarze roboczym w kolekcji obszaru roboczego. Jeśli jeszcze nie zostało to jeszcze zrobione tego kroku, zobacz [wprowadzenie w usłudze Power BI Embedded](power-bi-embedded-get-started.md).

Możesz użyć hello .NET (C#) lub zestaw Node.js SDK oraz języka JavaScript, tooeasily skompilować aplikację z Power BI Embedded. 

## <a name="using-hello-access-keys-toouse-rest-apis"></a>Przy użyciu toouse klucze dostępu hello interfejsów API REST

W kolejności toocall hello interfejsu API REST należy przekazać hello klucza dostępu, który można pobrać z portalu Azure dla kolekcji danego obszaru roboczego hello. Aby uzyskać więcej informacji, zobacz [wprowadzenie w usłudze Power BI Embedded](power-bi-embedded-get-started.md).

## <a name="get-a-report-id"></a>Pobierz identyfikator raportu

Każdy token dostępu jest oparty na raport. Konieczne będzie hello tooget podany identyfikator raportu dla raportu hello, które mają tooembed. Można to zrobić na toohello wywołania podstawie [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) interfejsu API REST. Spowoduje to przywrócenie raportu hello identyfikator i hello osadzić adresu url. Można to zrobić za pomocą hello Power BI .NET SDK lub bezpośrednie wywoływanie hello interfejsu API REST.

### <a name="using-hello-power-bi-net-sdk"></a>Przy użyciu hello Power BI .NET SDK

Używając hello zestawu .NET SDK, konieczne będzie toocreate token poświadczenie opartym na powitania klucz dostępu, uzyskasz od hello portalu Azure. Wymaga to zainstalowania hello [pakietu NuGet interfejsu API usługi Power BI](https://www.nuget.org/profiles/powerbi).

**Instalacja pakietu NuGet**

```
Install-Package Microsoft.PowerBI.Api
```

**Kod w języku C#**

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a>Bezpośrednie wywoływanie hello interfejsu API REST

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a>Utwórz token dostępu

Power BI Embedded korzystają osadzić token, który HMAC zalogowano tokenów sieci Web JSON. tokeny Hello są podpisane za pomocą klucza dostępu hello z kolekcji Azure Power BI Embedded obszaru roboczego. Osadzaj tokenów, domyślnie, są używane tooprovide odczytać tylko dostęp tooa tooembed raport do aplikacji. Osadź tokeny są wydawane dla określonego raportu i powinna być skojarzona z adresem URL osadzania.

Tokeny dostępu należy utworzyć na serwerze hello klucze dostępu hello są używane toosign/szyfrowania tokenów hello. Aby uzyskać informacje na temat toocreate tokenu dostępu, zobacz [Authenticating i autoryzacji z Power BI Embedded](power-bi-embedded-app-token-flow.md). Można również przejrzeć hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metody. Oto przykład jak to będzie wyglądać przy użyciu hello zestawu .NET SDK dla usługi Power BI.

Użyjesz hello identyfikator raportu, który został wcześniej pobrany. Po osadzić hello jest tworzony token, będzie używać tokenu hello toogenerate klucza dostępu hello, którego można użyć z punktu widzenia javascript hello. Witaj *klasy PowerBIToken* wymaga zainstalowania hello [Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Instalacja pakietu NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Kod w języku C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a>Dodawanie tokenów tooembed zakresy uprawnień

Tokeny osadzania można toorestrict użycia zasobów hello, który zapewnia dostęp do. Z tego powodu można wygenerować token z zakresu uprawnień. Aby uzyskać więcej informacji, zobacz [zakresów](power-bi-embedded-app-token-flow.md#scopes)

## <a name="embed-using-javascript"></a>Osadź przy użyciu języka JavaScript

Po hello token dostępu i identyfikator raportu hello, możemy osadzić raport hello przy użyciu języka JavaScript. Wymaga to zainstalowania hello nuget [pakietu Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Witaj embedUrl będą tylko https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Można użyć hello [próbki osadzić raport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funkcji. Udostępnia także przykłady kodu dla różnych operacji hello, które są dostępne.

**Instalacja pakietu NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Kod JavaScript**

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a>Ustaw rozmiar hello elementów osadzonych

Raport Hello zostanie automatycznie osadzony na podstawie rozmiaru hello swojego kontenera. rozmiar domyślny hello toooverride hello osadza po prostu Dodaj klasy atrybutu lub wbudowane style CSS na szerokość i wysokość.

## <a name="see-also"></a>Zobacz też

[Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI JavaScript pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
[Pakiet NuGet interfejsu API usługi BI zasilania](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Usługa Power BI CSharp repozytorium Git](https://github.com/Microsoft/PowerBI-CSharp)  
[Repozytorium Git węzła usługi Power BI](https://github.com/Microsoft/PowerBI-Node)  
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)
