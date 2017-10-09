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
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="44ca4-104">Zapisywanie raportów w usłudze Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="44ca4-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="44ca4-105">Dowiedz się, jak toosave raporty w usłudze Power BI embedded.</span><span class="sxs-lookup"><span data-stu-id="44ca4-105">Learn how toosave reports within Power BI embedded.</span></span> <span data-ttu-id="44ca4-106">Wymaga to odpowiednie uprawnienia w kolejności toowork pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="44ca4-106">This requires proper permissions in order toowork successfully.</span></span>

<span data-ttu-id="44ca4-107">W usłudze Power BI Embedded możesz edytować istniejących raportów i zapisz je.</span><span class="sxs-lookup"><span data-stu-id="44ca4-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="44ca4-108">Można również utworzyć nowy raport i Zapisz jako nowe toocreate raport, co.</span><span class="sxs-lookup"><span data-stu-id="44ca4-108">You can also create a new report and save as a new report toocreate one.</span></span>

<span data-ttu-id="44ca4-109">W kolejności toosave raportu należy najpierw toocreate token dla określonego raportu hello z zakresami prawo hello:</span><span class="sxs-lookup"><span data-stu-id="44ca4-109">In order toosave a report you first need toocreate a token for hello specific report with hello right scopes:</span></span>

* <span data-ttu-id="44ca4-110">tooenable Zapisz Report.ReadWrite zakres jest wymagany</span><span class="sxs-lookup"><span data-stu-id="44ca4-110">tooenable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="44ca4-111">tooenable Zapisz jako Report.Read i Workspace.Report.Copy zakresy są wymagane</span><span class="sxs-lookup"><span data-stu-id="44ca4-111">tooenable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="44ca4-112">Zapisz tooenable i Zapisz jako, Report.ReadWrite i Workspace.Report.Copy są requierd</span><span class="sxs-lookup"><span data-stu-id="44ca4-112">tooenable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="44ca4-113">Odpowiednio w kolejności tooenable hello prawo save/Zapisz jako przyciski w menu Plik muszą tooprovide hello prawym przyciskiem myszy uprawnienia w konfiguracji osadzania hello podczas hello możesz osadzania raportu:</span><span class="sxs-lookup"><span data-stu-id="44ca4-113">Respectively in order tooenable hello right save/save as buttons in file menu you need tooprovide hello right permission in hello Embed configuration when you Embed hello report:</span></span>

* <span data-ttu-id="44ca4-114">modele. Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="44ca4-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="44ca4-115">modele. Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="44ca4-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="44ca4-116">modele. Permissions.All</span><span class="sxs-lookup"><span data-stu-id="44ca4-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="44ca4-117">Token dostępu musi także hello odpowiednich zakresów.</span><span class="sxs-lookup"><span data-stu-id="44ca4-117">Your access token also needs hello appropriate scopes.</span></span> <span data-ttu-id="44ca4-118">Aby uzyskać więcej informacji, zobacz [zakresy](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="44ca4-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="44ca4-119">Osadzanie raportu w trybie edycji</span><span class="sxs-lookup"><span data-stu-id="44ca4-119">Embed report in edit mode</span></span>

<span data-ttu-id="44ca4-120">Załóżmy powiedz ma tooEmbed raport w trybie edycji wewnątrz aplikacji, toodo to po prostu Przekaż właściwości prawa hello w konfiguracji osadzania i Wywołaj powerbi.embed().</span><span class="sxs-lookup"><span data-stu-id="44ca4-120">Let's say you want tooEmbed a report in edit mode inside your app, toodo so just pass hello right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="44ca4-121">Konieczne będzie toosupply uprawnienia i viewMode w kolejności toosee hello Zapisz, a następnie Zapisz jako przyciski w trybie edycji.</span><span class="sxs-lookup"><span data-stu-id="44ca4-121">You will need toosupply permissions and a viewMode in order toosee hello save and save as buttons when in edit mode.</span></span> <span data-ttu-id="44ca4-122">Aby uzyskać więcej informacji, zobacz [osadzić szczegóły konfiguracji](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="44ca4-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="44ca4-123">Na przykład w języku JavaScript:</span><span class="sxs-lookup"><span data-stu-id="44ca4-123">For example in JavaScript:</span></span>

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

<span data-ttu-id="44ca4-124">Teraz raport zostanie osadzony w aplikacji w trybie edycji.</span><span class="sxs-lookup"><span data-stu-id="44ca4-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="44ca4-125">Zapisywanie raportu</span><span class="sxs-lookup"><span data-stu-id="44ca4-125">Save report</span></span>

<span data-ttu-id="44ca4-126">Embbeding hello raport w trybie i hello prawo tokenu edycji można zapisać raportu hello z menu Plik hello lub javascript:</span><span class="sxs-lookup"><span data-stu-id="44ca4-126">After Embbeding hello report in edit mode with hello right token and permissions you can save hello report from hello file menu or from javascript:</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="44ca4-127">Zapisz jako</span><span class="sxs-lookup"><span data-stu-id="44ca4-127">Save as</span></span>

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
> <span data-ttu-id="44ca4-128">Tylko po *Zapisz jako* jest utworzony nowy raport.</span><span class="sxs-lookup"><span data-stu-id="44ca4-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="44ca4-129">Po hello zapisać, kanwy hello jest nadal przedstawiający hello starego raportu w edycji trybu i nie hello nowy raport.</span><span class="sxs-lookup"><span data-stu-id="44ca4-129">After hello save, hello canvas is still showing hello old report in edit mode and not hello new report.</span></span> <span data-ttu-id="44ca4-130">Konieczne będzie tooembed hello nowy raport, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="44ca4-130">You will need tooembed hello new report that was created.</span></span> <span data-ttu-id="44ca4-131">Wymaga to nowy token dostępu tworzonych na raport.</span><span class="sxs-lookup"><span data-stu-id="44ca4-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="44ca4-132">Następnie należy tooload hello nowy raport po *Zapisz jako*.</span><span class="sxs-lookup"><span data-stu-id="44ca4-132">You will then need tooload hello new report after a *save as*.</span></span> <span data-ttu-id="44ca4-133">To jest podobne tooembedding żadnych raportów.</span><span class="sxs-lookup"><span data-stu-id="44ca4-133">This is similar tooembedding any report.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="44ca4-134">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="44ca4-134">See also</span></span>

[<span data-ttu-id="44ca4-135">Rozpoczęcie pracy z przykładem</span><span class="sxs-lookup"><span data-stu-id="44ca4-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
<span data-ttu-id="44ca4-136">[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)</span><span class="sxs-lookup"><span data-stu-id="44ca4-136">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="44ca4-137">Tworzenie nowego raportu przy użyciu zestawu danych</span><span class="sxs-lookup"><span data-stu-id="44ca4-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="44ca4-138">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="44ca4-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="44ca4-139">Program Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="44ca4-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="44ca4-140">Przykład osadzania skryptu JavaScript</span><span class="sxs-lookup"><span data-stu-id="44ca4-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="44ca4-141">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="44ca4-141">More questions?</span></span> [<span data-ttu-id="44ca4-142">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="44ca4-142">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

