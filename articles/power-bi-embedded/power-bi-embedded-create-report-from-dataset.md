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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="b0012-103">Tworzenie nowego raportu z zestawu danych w usłudze Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b0012-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="b0012-104">Teraz można tworzyć z zestawu danych w aplikacji Power BI Embedded raportów.</span><span class="sxs-lookup"><span data-stu-id="b0012-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="b0012-105">Witaj metoda uwierzytelniania to podobne osadzić toothat raportu.</span><span class="sxs-lookup"><span data-stu-id="b0012-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="b0012-106">Jest on oparty na tokeny dostępu, które są tooa określonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="b0012-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="b0012-107">Tokeny używane do witryny PowerBI.com są wydawane przez usługi Azure Active Directory (AAD) i tokenów Power BI Embedded są wystawiane przez własnej usługi.</span><span class="sxs-lookup"><span data-stu-id="b0012-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="b0012-108">Witaj createing raport osadzone tokenów wystawionych są dla określonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="b0012-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="b0012-109">Tokeny powinna być skojarzona z hello osadzić adres URL na powitania tego samego tooensure elementu, każdy ma unikatowy token.</span><span class="sxs-lookup"><span data-stu-id="b0012-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="b0012-110">W celu toocreate raport osadzone *Dataset.Read i Workspace.Report.Create* zakresy musi być wprowadzona w hello tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b0012-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="b0012-111">Tworzenie nowego raportu toocreate wymagane token dostępu</span><span class="sxs-lookup"><span data-stu-id="b0012-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="b0012-112">Power BI Embedded korzystają osadzić token, który HMAC zalogowano tokenów sieci Web JSON.</span><span class="sxs-lookup"><span data-stu-id="b0012-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="b0012-113">tokeny Hello są podpisane za pomocą klucza dostępu hello z kolekcji Azure Power BI Embedded obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="b0012-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="b0012-114">Osadzaj tokenów, domyślnie, są używane tooprovide odczytać tylko dostęp tooa tooembed raport do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0012-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="b0012-115">Osadź tokeny są wydawane dla określonego raportu i powinna być skojarzona z adresem URL osadzania.</span><span class="sxs-lookup"><span data-stu-id="b0012-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="b0012-116">Tokeny dostępu należy utworzyć na serwerze hello klucze dostępu hello są używane toosign/szyfrowania tokenów hello.</span><span class="sxs-lookup"><span data-stu-id="b0012-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="b0012-117">Aby uzyskać informacje na temat toocreate tokenu dostępu, zobacz [Authenticating i autoryzacji z Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="b0012-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="b0012-118">Można również przejrzeć hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metody.</span><span class="sxs-lookup"><span data-stu-id="b0012-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="b0012-119">Oto przykład jak to będzie wyglądać przy użyciu hello zestawu .NET SDK dla usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="b0012-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="b0012-120">W tym przykładzie mamy naszych identyfikator zestawu danych, która ma toocreat hello nowego raportu na.</span><span class="sxs-lookup"><span data-stu-id="b0012-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="b0012-121">Potrzebujemy zakresów hello tooadd *Dataset.Read i Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="b0012-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="b0012-122">Witaj *klasy PowerBIToken* wymaga zainstalowania hello [Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="b0012-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="b0012-123">**Instalacja pakietu NuGet**</span><span class="sxs-lookup"><span data-stu-id="b0012-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="b0012-124">**Kod w języku C#**</span><span class="sxs-lookup"><span data-stu-id="b0012-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="b0012-125">Tworzenie nowego raportu puste</span><span class="sxs-lookup"><span data-stu-id="b0012-125">Create a new blank report</span></span>

<span data-ttu-id="b0012-126">W kolejności toocreate nowy raport, Utwórz hello podawać konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b0012-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="b0012-127">Powinno to obejmować hello tokenu dostępu, hello embedURL i hello datasetID które chcemy toocreate hello raport z.</span><span class="sxs-lookup"><span data-stu-id="b0012-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="b0012-128">Wymaga to zainstalowania hello nuget [pakietu Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="b0012-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="b0012-129">Witaj embedUrl będą tylko https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="b0012-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="b0012-130">Można użyć hello [próbki osadzić raport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funkcji.</span><span class="sxs-lookup"><span data-stu-id="b0012-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="b0012-131">Udostępnia także przykłady kodu dla różnych operacji hello, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b0012-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="b0012-132">**Instalacja pakietu NuGet**</span><span class="sxs-lookup"><span data-stu-id="b0012-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="b0012-133">**Kod JavaScript**</span><span class="sxs-lookup"><span data-stu-id="b0012-133">**JavaScript code**</span></span>

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

<span data-ttu-id="b0012-134">Wywoływanie *powerbi.createReport()* spowoduje, że są wyświetlane w hello pustej kanwy w trybie edycji *div* elementu.</span><span class="sxs-lookup"><span data-stu-id="b0012-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="b0012-135">Zapisz nowe raporty</span><span class="sxs-lookup"><span data-stu-id="b0012-135">Save new reports</span></span>

<span data-ttu-id="b0012-136">Witaj raport nie zostanie faktycznie utworzone do czasu wywołania hello **Zapisz jako** operacji.</span><span class="sxs-lookup"><span data-stu-id="b0012-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="b0012-137">Można to zrobić w menu Plik lub z poziomu języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b0012-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="b0012-138">Nowy raport jest tworzony dopiero po **Zapisz jako** jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="b0012-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="b0012-139">Po zapisaniu, kanwy hello w dalszym ciągu będzie hello zestawu danych w raporcie trybu i nie hello edycji.</span><span class="sxs-lookup"><span data-stu-id="b0012-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="b0012-140">Podobnie jak każdy inny raport, należy tooreload hello nowy raport.</span><span class="sxs-lookup"><span data-stu-id="b0012-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="b0012-141">Nowy raport hello obciążenia</span><span class="sxs-lookup"><span data-stu-id="b0012-141">Load hello new report</span></span>

<span data-ttu-id="b0012-142">W kolejności toointeract z hello nowego raportu należy tooembed osadzić w aplikacji hello osadza regularnych raportów, co oznacza, nowy token tak samo musi być wystawiony dla nowego raportu hello powitalne, a następnie wywołania hello — metoda.</span><span class="sxs-lookup"><span data-stu-id="b0012-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="b0012-143">Nie można załadować nowego raportu przy użyciu hello "zapisane" zdarzeń i zautomatyzować Zapisz</span><span class="sxs-lookup"><span data-stu-id="b0012-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="b0012-144">W procesie hello tooautomate kolejność "Zapisz jako" i podczas ładowania hello nowy raport możesz wprowadzić użycie hello "zapisane" zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b0012-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="b0012-145">To zdarzenie jest wywoływane po zakończeniu hello operacji zapisywania i zwraca obiekt Json zawierające hello reportId nowe, nazwę raportu, reportId starego hello (jeśli wystąpił jeden z nich) i jeśli saveAs jest operacja hello lub zapisać.</span><span class="sxs-lookup"><span data-stu-id="b0012-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="b0012-146">proces hello tooAutomate możesz nasłuchiwania zdarzeń "zapisane" hello, pobrać hello reportId nowe, Utwórz nowy token hello i osadzić nowy raport hello z nim.</span><span class="sxs-lookup"><span data-stu-id="b0012-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="b0012-147">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b0012-147">See also</span></span>

[<span data-ttu-id="b0012-148">Rozpoczęcie pracy z przykładem</span><span class="sxs-lookup"><span data-stu-id="b0012-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="b0012-149">Zapisywanie raportów</span><span class="sxs-lookup"><span data-stu-id="b0012-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
<span data-ttu-id="b0012-150">[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)</span><span class="sxs-lookup"><span data-stu-id="b0012-150">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="b0012-151">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="b0012-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b0012-152">Program Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b0012-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="b0012-153">Przykład osadzania skryptu JavaScript</span><span class="sxs-lookup"><span data-stu-id="b0012-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="b0012-154">Power BI Core NuGut pakietu</span><span class="sxs-lookup"><span data-stu-id="b0012-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="b0012-155">Power BI JavaScript pakietu</span><span class="sxs-lookup"><span data-stu-id="b0012-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="b0012-156">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="b0012-156">More questions?</span></span> [<span data-ttu-id="b0012-157">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="b0012-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
