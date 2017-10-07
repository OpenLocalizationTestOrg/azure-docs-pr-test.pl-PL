---
title: "Nowy raport z zestawu danych w usłudze Azure Power BI Embedded aaaCreate | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a>Tworzenie nowego raportu z zestawu danych w usłudze Power BI Embedded

Teraz można tworzyć z zestawu danych w aplikacji Power BI Embedded raportów. 

Witaj metoda uwierzytelniania to podobne osadzić toothat raportu. Jest on oparty na tokeny dostępu, które są tooa określonego zestawu danych. Tokeny używane do witryny PowerBI.com są wydawane przez usługi Azure Active Directory (AAD) i tokenów Power BI Embedded są wystawiane przez własnej usługi.

Witaj createing raport osadzone tokenów wystawionych są dla określonego zestawu danych. Tokeny powinna być skojarzona z hello osadzić adres URL na powitania tego samego tooensure elementu, każdy ma unikatowy token. W celu toocreate raport osadzone *Dataset.Read i Workspace.Report.Create* zakresy musi być wprowadzona w hello tokenu dostępu.

## <a name="create-access-token-needed-toocreate-new-report"></a>Tworzenie nowego raportu toocreate wymagane token dostępu

Power BI Embedded korzystają osadzić token, który HMAC zalogowano tokenów sieci Web JSON. tokeny Hello są podpisane za pomocą klucza dostępu hello z kolekcji Azure Power BI Embedded obszaru roboczego. Osadzaj tokenów, domyślnie, są używane tooprovide odczytać tylko dostęp tooa tooembed raport do aplikacji. Osadź tokeny są wydawane dla określonego raportu i powinna być skojarzona z adresem URL osadzania.

Tokeny dostępu należy utworzyć na serwerze hello klucze dostępu hello są używane toosign/szyfrowania tokenów hello. Aby uzyskać informacje na temat toocreate tokenu dostępu, zobacz [Authenticating i autoryzacji z Power BI Embedded](power-bi-embedded-app-token-flow.md). Można również przejrzeć hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metody. Oto przykład jak to będzie wyglądać przy użyciu hello zestawu .NET SDK dla usługi Power BI.

W tym przykładzie mamy naszych identyfikator zestawu danych, która ma toocreat hello nowego raportu na. Potrzebujemy zakresów hello tooadd *Dataset.Read i Workspace.Report.Create*.

Witaj *klasy PowerBIToken* wymaga zainstalowania hello [Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).

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

W kolejności toocreate nowy raport, Utwórz hello podawać konfiguracji. Powinno to obejmować hello tokenu dostępu, hello embedURL i hello datasetID które chcemy toocreate hello raport z. Wymaga to zainstalowania hello nuget [pakietu Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/). Witaj embedUrl będą tylko https://embedded.powerbi.com/appTokenReportEmbed.

> [!NOTE]
> Można użyć hello [próbki osadzić raport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funkcji. Udostępnia także przykłady kodu dla różnych operacji hello, które są dostępne.

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
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

Wywoływanie *powerbi.createReport()* spowoduje, że są wyświetlane w hello pustej kanwy w trybie edycji *div* elementu.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a>Zapisz nowe raporty

Witaj raport nie zostanie faktycznie utworzone do czasu wywołania hello **Zapisz jako** operacji. Można to zrobić w menu Plik lub z poziomu języka JavaScript.

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> Nowy raport jest tworzony dopiero po **Zapisz jako** jest wywoływana. Po zapisaniu, kanwy hello w dalszym ciągu będzie hello zestawu danych w raporcie trybu i nie hello edycji. Podobnie jak każdy inny raport, należy tooreload hello nowy raport.

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a>Nowy raport hello obciążenia

W kolejności toointeract z hello nowego raportu należy tooembed osadzić w aplikacji hello osadza regularnych raportów, co oznacza, nowy token tak samo musi być wystawiony dla nowego raportu hello powitalne, a następnie wywołania hello — metoda.

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a>Nie można załadować nowego raportu przy użyciu hello "zapisane" zdarzeń i zautomatyzować Zapisz

W procesie hello tooautomate kolejność "Zapisz jako" i podczas ładowania hello nowy raport możesz wprowadzić użycie hello "zapisane" zdarzeń. To zdarzenie jest wywoływane po zakończeniu hello operacji zapisywania i zwraca obiekt Json zawierające hello reportId nowe, nazwę raportu, reportId starego hello (jeśli wystąpił jeden z nich) i jeśli saveAs jest operacja hello lub zapisać.

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

proces hello tooAutomate możesz nasłuchiwania zdarzeń "zapisane" hello, pobrać hello reportId nowe, Utwórz nowy token hello i osadzić nowy raport hello z nim.

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
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
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)
