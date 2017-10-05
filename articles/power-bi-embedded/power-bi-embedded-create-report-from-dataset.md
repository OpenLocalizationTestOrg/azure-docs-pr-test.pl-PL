---
title: "Tworzenie nowego raportu z zestawu danych w usłudze Azure Power BI Embedded | Dokumentacja firmy Microsoft"
description: "Teraz można tworzyć z zestawu danych w aplikacji Power BI Embedded raportów."
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
ms.openlocfilehash: 457f53aa76059dbb2faed6b264102f1f59b9918a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Tworzenie nowego raportu z zestawu danych w usłudze Power BI Embedded

Teraz można tworzyć z zestawu danych w aplikacji Power BI Embedded raportów. 

Metoda uwierzytelniania jest podobny do czy raportu osadzania. Jest on oparty na tokeny dostępu, które są specyficzne dla zestawu danych. Tokeny używane do witryny PowerBI.com są wydawane przez usługi Azure Active Directory (AAD) i tokenów Power BI Embedded są wystawiane przez własnej usługi.

Kiedy createing raport osadzone tokenów wystawionych są dla określonego zestawu danych. Tokeny powinna być skojarzona z osadzania adres URL w tym samym elemencie upewnij się, że każdy ma unikatowy tokenu. Aby utworzyć raport osadzone *Dataset.Read i Workspace.Report.Create* zakresy musi być wprowadzona w tokenie dostępu.

## <a name="create-access-token-needed-to-create-new-report"></a>Utwórz token dostępu potrzebne do utworzenia nowego raportu

Power BI Embedded korzystają osadzić token, który HMAC zalogowano tokenów sieci Web JSON. Tokeny są podpisane za pomocą klucza dostępu z kolekcji Azure Power BI Embedded obszaru roboczego. Osadzaj tokenów, domyślnie, są używane do zapewnienia odczytu dostępu tylko do raportu w celu osadzenia w aplikacji. Osadź tokeny są wydawane dla określonego raportu i powinna być skojarzona z adresem URL osadzania.

Tokeny dostępu należy utworzyć na serwerze jako klucze dostępu są używane do logowania/szyfrowania tokenów. Aby uzyskać informacje na temat tworzenia tokenu dostępu, zobacz [Authenticating i autoryzacji z Power BI Embedded](power-bi-embedded-app-token-flow.md). Można również przejrzeć [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metody. Oto przykład jak to będzie wyglądać przy użyciu zestawu .NET SDK dla usługi Power BI.

W tym przykładzie mamy naszych identyfikator zestawu danych, która ma być tworzenie nowego raportu na. Możemy też konieczne dodanie zakresów dla *Dataset.Read i Workspace.Report.Create*.

*Klasy PowerBIToken* wymaga zainstalowania [Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

**Instalacja pakietu NuGet**

```
Install-Package Microsoft.PowerBI.Core
```

**Kod w języku C#**

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a>Tworzenie nowego raportu puste

Aby utworzyć nowy raport, należy podać Tworzenie konfiguracji. Powinno to obejmować tokenu dostępu, embedURL i datasetID, który chcemy, aby utworzyć raport z. Wymaga to zainstalowania nuget [pakietu Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). EmbedUrl będą tylko https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Można użyć [próbki osadzić raport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) Aby przetestować funkcje. Udostępnia także przykłady kodu dla różnych operacji, które są dostępne.

**Instalacja pakietu NuGet**

```
Install-Package Microsoft.PowerBI.JavaScript
```

**Kod JavaScript**

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

Wywoływanie *powerbi.createReport()* będzie znajdować się w pustej kanwy w trybie edycji *div* elementu.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Zapisz nowe raporty

Raport nie zostanie faktycznie utworzone do czasu wywołania **Zapisz jako** operacji. Można to zrobić w menu Plik lub z poziomu języka JavaScript.

```
 // Get a reference to the embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> Nowy raport jest tworzony dopiero po **Zapisz jako** jest wywoływana. Po zapisaniu, obszar roboczy w dalszym ciągu będzie zestawu danych w trybie edycji i nie raportu. Należy załadować ponownie nowy raport, jak w przypadku innych raportów.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a>Ładowanie nowego raportu

Aby pracować interaktywnie z nowego raportu potrzebne do osadzenia go w taki sam sposób, w aplikacji osadza regularnych raportów, co oznacza, nowy token musi być wystawiony dla nowego raportu, a następnie wywołaj metodę osadzania.

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a>Nie można załadować nowego raportu za pomocą tego zdarzenia "zapisane" i zautomatyzować Zapisz

W celu automatyzacji procesu "Zapisz jako" i Trwa ładowanie nowego raportu, które można wprowadzić Użyj "zapisane" zdarzenia. To zdarzenie jest wywoływane podczas zapisywania operacja została zakończona i zwraca obiekt Json zawierające reportId nowe, nazwę raportu, stare reportId (jeśli wystąpił jeden z nich) i jeśli operacja zakończyła saveAs lub zapisać.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

Aby zautomatyzować proces, który można nasłuchiwać zdarzeń "zapisane", otrzymuje nowe reportId, Utwórz nowy token i osadzić nowy raport z nim.

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab the reference to the div HTML element that will host the report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints to Log window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that the application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide the wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a>Zobacz też

[Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)  
[Zapisywanie raportów](power-bi-embedded-save-reports.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Program Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[Power BI JavaScript pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
Masz więcej pytań? [Dołącz do społeczności użytkowników usługi Power BI](http://community.powerbi.com/)