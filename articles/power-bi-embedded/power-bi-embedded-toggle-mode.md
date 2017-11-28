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
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="fef40-103">Przełącz między widokami i edytować tryb raportów w usłudze Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="fef40-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="fef40-104">Dowiedz się, jak tootoggle między trybem wyświetlanie i edytowanie dla raportów w usłudze Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="fef40-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="fef40-105">Tworzenie token dostępu</span><span class="sxs-lookup"><span data-stu-id="fef40-105">Creating an access token</span></span>

<span data-ttu-id="fef40-106">Konieczne będzie toocreate tokenu dostępu, który zapewnia hello możliwości tooboth wyświetlanie i edytowanie raportu.</span><span class="sxs-lookup"><span data-stu-id="fef40-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="fef40-107">tooedit i Zapisz raport, konieczne będzie hello **Report.ReadWrite** token uprawnień.</span><span class="sxs-lookup"><span data-stu-id="fef40-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="fef40-108">Aby uzyskać więcej informacji, zobacz [Authenticating i autoryzacji w usłudze Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="fef40-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fef40-109">To pozwala tooedit i Zapisz zmiany tooan istniejącego raportu.</span><span class="sxs-lookup"><span data-stu-id="fef40-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="fef40-110">Jeśli chcesz również hello funkcji obsługi **Zapisz jako**, konieczne będzie toosupply dodatkowe uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="fef40-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="fef40-111">Aby uzyskać więcej informacji, zobacz [zakresy](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="fef40-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="fef40-112">Osadź konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fef40-112">Embed configuration</span></span>

<span data-ttu-id="fef40-113">Konieczne będzie toosupply uprawnienia i viewMode w kolejności toosee hello Zapisz przycisku w trybie edycji.</span><span class="sxs-lookup"><span data-stu-id="fef40-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="fef40-114">Aby uzyskać więcej informacji, zobacz [osadzić szczegóły konfiguracji](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="fef40-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="fef40-115">Na przykład w języku JavaScript:</span><span class="sxs-lookup"><span data-stu-id="fef40-115">For example in JavaScript:</span></span>

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

<span data-ttu-id="fef40-116">Wskazuje tooembed hello raport w trybie widoku na podstawie **viewMode** ustawiany za**modeli. ViewMode.View**.</span><span class="sxs-lookup"><span data-stu-id="fef40-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="fef40-117">Tryb wyświetlania</span><span class="sxs-lookup"><span data-stu-id="fef40-117">View mode</span></span>

<span data-ttu-id="fef40-118">Możesz użyć powitania po JavaScript tooswitch w trybie widoku, jeśli jesteś w trybie edycji.</span><span class="sxs-lookup"><span data-stu-id="fef40-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="fef40-119">Tryb edycji</span><span class="sxs-lookup"><span data-stu-id="fef40-119">Edit mode</span></span>

<span data-ttu-id="fef40-120">Jeśli jesteś w trybie, można użyć powitania po JavaScript tooswitch w trybie edycji.</span><span class="sxs-lookup"><span data-stu-id="fef40-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="fef40-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="fef40-121">See also</span></span>

[<span data-ttu-id="fef40-122">Rozpoczęcie pracy z przykładem</span><span class="sxs-lookup"><span data-stu-id="fef40-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
<span data-ttu-id="fef40-123">[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)</span><span class="sxs-lookup"><span data-stu-id="fef40-123">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="fef40-124">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="fef40-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="fef40-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="fef40-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="fef40-126">Przykład osadzania skryptu JavaScript</span><span class="sxs-lookup"><span data-stu-id="fef40-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="fef40-127">Usługa Power BI CSharp repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="fef40-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="fef40-128">Repozytorium Git węzła usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="fef40-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="fef40-129">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="fef40-129">More questions?</span></span> [<span data-ttu-id="fef40-130">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="fef40-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
