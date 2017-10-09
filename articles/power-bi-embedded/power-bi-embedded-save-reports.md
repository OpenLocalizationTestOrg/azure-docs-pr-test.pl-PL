---
title: Raporty aaaSave na platformie Azure Power BI Embedded | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toosave raporty w usłudze Power BI embedded. Wymaga to odpowiednie uprawnienia w kolejności toowork pomyślnie."
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
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a>Zapisywanie raportów w usłudze Power BI Embedded

Dowiedz się, jak toosave raporty w usłudze Power BI embedded. Wymaga to odpowiednie uprawnienia w kolejności toowork pomyślnie.

W usłudze Power BI Embedded możesz edytować istniejących raportów i zapisz je. Można również utworzyć nowy raport i Zapisz jako nowe toocreate raport, co.

W kolejności toosave raportu należy najpierw toocreate token dla określonego raportu hello z zakresami prawo hello:

* tooenable Zapisz Report.ReadWrite zakres jest wymagany
* tooenable Zapisz jako Report.Read i Workspace.Report.Copy zakresy są wymagane
* Zapisz tooenable i Zapisz jako, Report.ReadWrite i Workspace.Report.Copy są requierd

Odpowiednio w kolejności tooenable hello prawo save/Zapisz jako przyciski w menu Plik muszą tooprovide hello prawym przyciskiem myszy uprawnienia w konfiguracji osadzania hello podczas hello możesz osadzania raportu:

* modele. Permissions.ReadWrite
* modele. Permissions.Copy
* modele. Permissions.All

> [!NOTE]
> Token dostępu musi także hello odpowiednich zakresów. Aby uzyskać więcej informacji, zobacz [zakresy](power-bi-embedded-app-token-flow.md#scopes).

## <a name="embed-report-in-edit-mode"></a>Osadzanie raportu w trybie edycji

Załóżmy powiedz ma tooEmbed raport w trybie edycji wewnątrz aplikacji, toodo to po prostu Przekaż właściwości prawa hello w konfiguracji osadzania i Wywołaj powerbi.embed(). Konieczne będzie toosupply uprawnienia i viewMode w kolejności toosee hello Zapisz, a następnie Zapisz jako przyciski w trybie edycji. Aby uzyskać więcej informacji, zobacz [osadzić szczegóły konfiguracji](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

Na przykład w języku JavaScript:

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

Teraz raport zostanie osadzony w aplikacji w trybie edycji.

## <a name="save-report"></a>Zapisywanie raportu

Embbeding hello raport w trybie i hello prawo tokenu edycji można zapisać raportu hello z menu Plik hello lub javascript:

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a>Zapisz jako

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
> Tylko po *Zapisz jako* jest utworzony nowy raport. Po hello zapisać, kanwy hello jest nadal przedstawiający hello starego raportu w edycji trybu i nie hello nowy raport. Konieczne będzie tooembed hello nowy raport, który został utworzony. Wymaga to nowy token dostępu tworzonych na raport.

Następnie należy tooload hello nowy raport po *Zapisz jako*. To jest podobne tooembedding żadnych raportów.

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

## <a name="see-also"></a>Zobacz też

[Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)  
[Tworzenie nowego raportu przy użyciu zestawu danych](power-bi-embedded-create-report-from-dataset.md)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Program Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)

