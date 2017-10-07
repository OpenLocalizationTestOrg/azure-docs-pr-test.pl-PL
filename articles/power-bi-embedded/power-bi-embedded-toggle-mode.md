---
title: "aaaToggle między trybem wyświetlanie i edytowanie raportów w usłudze Azure Power BI Embedded | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootoggle między trybem wyświetlanie i edytowanie dla raportów w usłudze Power BI Embedded."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a>Przełącz między widokami i edytować tryb raportów w usłudze Power BI Embedded

Dowiedz się, jak tootoggle między trybem wyświetlanie i edytowanie dla raportów w usłudze Power BI Embedded.

## <a name="creating-an-access-token"></a>Tworzenie token dostępu

Konieczne będzie toocreate tokenu dostępu, który zapewnia hello możliwości tooboth wyświetlanie i edytowanie raportu. tooedit i Zapisz raport, konieczne będzie hello **Report.ReadWrite** token uprawnień. Aby uzyskać więcej informacji, zobacz [Authenticating i autoryzacji w usłudze Power BI Embedded](power-bi-embedded-app-token-flow.md).

> [!NOTE]
> To pozwala tooedit i Zapisz zmiany tooan istniejącego raportu. Jeśli chcesz również hello funkcji obsługi **Zapisz jako**, konieczne będzie toosupply dodatkowe uprawnienia. Aby uzyskać więcej informacji, zobacz [zakresy](power-bi-embedded-app-token-flow.md#scopes).

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a>Osadź konfiguracji

Konieczne będzie toosupply uprawnienia i viewMode w kolejności toosee hello Zapisz przycisku w trybie edycji. Aby uzyskać więcej informacji, zobacz [osadzić szczegóły konfiguracji](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

Wskazuje tooembed hello raport w trybie widoku na podstawie **viewMode** ustawiany za**modeli. ViewMode.View**.

## <a name="view-mode"></a>Tryb wyświetlania

Możesz użyć powitania po JavaScript tooswitch w trybie widoku, jeśli jesteś w trybie edycji.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a>Tryb edycji

Jeśli jesteś w trybie, można użyć powitania po JavaScript tooswitch w trybie edycji.

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a>Zobacz też

[Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Usługa Power BI CSharp repozytorium Git](https://github.com/Microsoft/PowerBI-CSharp)  
[Repozytorium Git węzła usługi Power BI](https://github.com/Microsoft/PowerBI-Node)  
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)
