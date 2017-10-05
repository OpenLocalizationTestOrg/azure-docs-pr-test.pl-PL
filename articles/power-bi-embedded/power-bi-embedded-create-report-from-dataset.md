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
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="7ede8-103">Tworzenie nowego raportu z zestawu danych w usłudze Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7ede8-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="7ede8-104">Teraz można tworzyć z zestawu danych w aplikacji Power BI Embedded raportów.</span><span class="sxs-lookup"><span data-stu-id="7ede8-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="7ede8-105">Metoda uwierzytelniania jest podobny do czy raportu osadzania.</span><span class="sxs-lookup"><span data-stu-id="7ede8-105">The authentication method is similar to that of report embed.</span></span> <span data-ttu-id="7ede8-106">Jest on oparty na tokeny dostępu, które są specyficzne dla zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="7ede8-106">It is based on access tokens that are specific to a dataset.</span></span> <span data-ttu-id="7ede8-107">Tokeny używane do witryny PowerBI.com są wydawane przez usługi Azure Active Directory (AAD) i tokenów Power BI Embedded są wystawiane przez własnej usługi.</span><span class="sxs-lookup"><span data-stu-id="7ede8-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="7ede8-108">Kiedy createing raport osadzone tokenów wystawionych są dla określonego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="7ede8-108">When createing an Embedded report, the tokens issued are for a specific dataset.</span></span> <span data-ttu-id="7ede8-109">Tokeny powinna być skojarzona z osadzania adres URL w tym samym elemencie upewnij się, że każdy ma unikatowy tokenu.</span><span class="sxs-lookup"><span data-stu-id="7ede8-109">Tokens should be associated with the embed URL on the same element to ensure each has a unique token.</span></span> <span data-ttu-id="7ede8-110">Aby utworzyć raport osadzone *Dataset.Read i Workspace.Report.Create* zakresy musi być wprowadzona w tokenie dostępu.</span><span class="sxs-lookup"><span data-stu-id="7ede8-110">In order to create an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in the access token.</span></span>

## <a name="create-access-token-needed-to-create-new-report"></a><span data-ttu-id="7ede8-111">Utwórz token dostępu potrzebne do utworzenia nowego raportu</span><span class="sxs-lookup"><span data-stu-id="7ede8-111">Create access token needed to create new report</span></span>

<span data-ttu-id="7ede8-112">Power BI Embedded korzystają osadzić token, który HMAC zalogowano tokenów sieci Web JSON.</span><span class="sxs-lookup"><span data-stu-id="7ede8-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="7ede8-113">Tokeny są podpisane za pomocą klucza dostępu z kolekcji Azure Power BI Embedded obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="7ede8-113">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="7ede8-114">Osadzaj tokenów, domyślnie, są używane do zapewnienia odczytu dostępu tylko do raportu w celu osadzenia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7ede8-114">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="7ede8-115">Osadź tokeny są wydawane dla określonego raportu i powinna być skojarzona z adresem URL osadzania.</span><span class="sxs-lookup"><span data-stu-id="7ede8-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="7ede8-116">Tokeny dostępu należy utworzyć na serwerze jako klucze dostępu są używane do logowania/szyfrowania tokenów.</span><span class="sxs-lookup"><span data-stu-id="7ede8-116">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="7ede8-117">Aby uzyskać informacje na temat tworzenia tokenu dostępu, zobacz [Authenticating i autoryzacji z Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="7ede8-117">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="7ede8-118">Można również przejrzeć [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metody.</span><span class="sxs-lookup"><span data-stu-id="7ede8-118">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="7ede8-119">Oto przykład jak to będzie wyglądać przy użyciu zestawu .NET SDK dla usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="7ede8-119">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="7ede8-120">W tym przykładzie mamy naszych identyfikator zestawu danych, która ma być tworzenie nowego raportu na.</span><span class="sxs-lookup"><span data-stu-id="7ede8-120">In this example, we have our dataset id that we want to creat the new report on.</span></span> <span data-ttu-id="7ede8-121">Możemy też konieczne dodanie zakresów dla *Dataset.Read i Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="7ede8-121">We also need to add the scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="7ede8-122">*Klasy PowerBIToken* wymaga zainstalowania [Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="7ede8-122">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="7ede8-123">**Instalacja pakietu NuGet**</span><span class="sxs-lookup"><span data-stu-id="7ede8-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="7ede8-124">**Kod w języku C#**</span><span class="sxs-lookup"><span data-stu-id="7ede8-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="7ede8-125">Tworzenie nowego raportu puste</span><span class="sxs-lookup"><span data-stu-id="7ede8-125">Create a new blank report</span></span>

<span data-ttu-id="7ede8-126">Aby utworzyć nowy raport, należy podać Tworzenie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7ede8-126">In order to create a new report, the create configuration should be provided.</span></span> <span data-ttu-id="7ede8-127">Powinno to obejmować tokenu dostępu, embedURL i datasetID, który chcemy, aby utworzyć raport z.</span><span class="sxs-lookup"><span data-stu-id="7ede8-127">This should include the access token, the embedURL and the datasetID that we want to create the report against.</span></span> <span data-ttu-id="7ede8-128">Wymaga to zainstalowania nuget [pakietu Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="7ede8-128">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="7ede8-129">EmbedUrl będą tylko https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="7ede8-129">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="7ede8-130">Można użyć [próbki osadzić raport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) Aby przetestować funkcje.</span><span class="sxs-lookup"><span data-stu-id="7ede8-130">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="7ede8-131">Udostępnia także przykłady kodu dla różnych operacji, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="7ede8-131">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="7ede8-132">**Instalacja pakietu NuGet**</span><span class="sxs-lookup"><span data-stu-id="7ede8-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="7ede8-133">**Kod JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ede8-133">**JavaScript code**</span></span>

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

<span data-ttu-id="7ede8-134">Wywoływanie *powerbi.createReport()* będzie znajdować się w pustej kanwy w trybie edycji *div* elementu.</span><span class="sxs-lookup"><span data-stu-id="7ede8-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within the *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="7ede8-135">Zapisz nowe raporty</span><span class="sxs-lookup"><span data-stu-id="7ede8-135">Save new reports</span></span>

<span data-ttu-id="7ede8-136">Raport nie zostanie faktycznie utworzone do czasu wywołania **Zapisz jako** operacji.</span><span class="sxs-lookup"><span data-stu-id="7ede8-136">The report will not actually be created until you call the **save as** operation.</span></span> <span data-ttu-id="7ede8-137">Można to zrobić w menu Plik lub z poziomu języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7ede8-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="7ede8-138">Nowy raport jest tworzony dopiero po **Zapisz jako** jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="7ede8-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="7ede8-139">Po zapisaniu, obszar roboczy w dalszym ciągu będzie zestawu danych w trybie edycji i nie raportu.</span><span class="sxs-lookup"><span data-stu-id="7ede8-139">After you save, the canvas will still show the dataset in edit mode and not the report.</span></span> <span data-ttu-id="7ede8-140">Należy załadować ponownie nowy raport, jak w przypadku innych raportów.</span><span class="sxs-lookup"><span data-stu-id="7ede8-140">You will need to reload the new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-the-new-report"></a><span data-ttu-id="7ede8-141">Ładowanie nowego raportu</span><span class="sxs-lookup"><span data-stu-id="7ede8-141">Load the new report</span></span>

<span data-ttu-id="7ede8-142">Aby pracować interaktywnie z nowego raportu potrzebne do osadzenia go w taki sam sposób, w aplikacji osadza regularnych raportów, co oznacza, nowy token musi być wystawiony dla nowego raportu, a następnie wywołaj metodę osadzania.</span><span class="sxs-lookup"><span data-stu-id="7ede8-142">In order to interact with the new report you need to embed it in the same way the application embeds a regular report, meaning, a new token must be issued specifically for the new report and then call the embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-the-saved-event"></a><span data-ttu-id="7ede8-143">Nie można załadować nowego raportu za pomocą tego zdarzenia "zapisane" i zautomatyzować Zapisz</span><span class="sxs-lookup"><span data-stu-id="7ede8-143">Automate save and load of a new report using the "saved" event</span></span>

<span data-ttu-id="7ede8-144">W celu automatyzacji procesu "Zapisz jako" i Trwa ładowanie nowego raportu, które można wprowadzić Użyj "zapisane" zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7ede8-144">In order to automate the process of "save as" and then loading the new report you can make use of the "saved" Event.</span></span> <span data-ttu-id="7ede8-145">To zdarzenie jest wywoływane podczas zapisywania operacja została zakończona i zwraca obiekt Json zawierające reportId nowe, nazwę raportu, stare reportId (jeśli wystąpił jeden z nich) i jeśli operacja zakończyła saveAs lub zapisać.</span><span class="sxs-lookup"><span data-stu-id="7ede8-145">This event is fired when the save operation is complete and it returns a Json object containing the new reportId, report name, the old reportId(if there was one) and if the operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="7ede8-146">Aby zautomatyzować proces, który można nasłuchiwać zdarzeń "zapisane", otrzymuje nowe reportId, Utwórz nowy token i osadzić nowy raport z nim.</span><span class="sxs-lookup"><span data-stu-id="7ede8-146">To Automate the process you can listen on the "saved" event, take the new reportId, create the new token and embed the new report with it.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="7ede8-147">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="7ede8-147">See also</span></span>

[<span data-ttu-id="7ede8-148">Rozpoczęcie pracy z przykładem</span><span class="sxs-lookup"><span data-stu-id="7ede8-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="7ede8-149">Zapisywanie raportów</span><span class="sxs-lookup"><span data-stu-id="7ede8-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
<span data-ttu-id="7ede8-150">[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)</span><span class="sxs-lookup"><span data-stu-id="7ede8-150">[Embed a report](power-bi-embedded-embed-report.md)</span></span>  
[<span data-ttu-id="7ede8-151">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7ede8-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="7ede8-152">Program Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7ede8-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="7ede8-153">Przykład osadzania skryptu JavaScript</span><span class="sxs-lookup"><span data-stu-id="7ede8-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="7ede8-154">Power BI Core NuGut pakietu</span><span class="sxs-lookup"><span data-stu-id="7ede8-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="7ede8-155">Power BI JavaScript pakietu</span><span class="sxs-lookup"><span data-stu-id="7ede8-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="7ede8-156">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="7ede8-156">More questions?</span></span> [<span data-ttu-id="7ede8-157">Dołącz do społeczności użytkowników usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="7ede8-157">Try the Power BI Community</span></span>](http://community.powerbi.com/)