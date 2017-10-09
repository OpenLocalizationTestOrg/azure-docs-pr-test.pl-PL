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
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="d1a07-103">Osadzanie raportu w usłudze Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d1a07-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="d1a07-104">Dowiedz się, jak tooembed raport, który znajduje się w usłudze Power BI Embedded do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1a07-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="d1a07-105">Przedstawiono sposób tooactually osadzanie raportu w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1a07-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="d1a07-106">Jest to zakładając, że masz już raport, który istnieje w obszarze roboczym w kolekcji obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="d1a07-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="d1a07-107">Jeśli jeszcze nie zostało to jeszcze zrobione tego kroku, zobacz [wprowadzenie w usłudze Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d1a07-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="d1a07-108">Możesz użyć hello .NET (C#) lub zestaw Node.js SDK oraz języka JavaScript, tooeasily skompilować aplikację z Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="d1a07-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="d1a07-109">Przy użyciu toouse klucze dostępu hello interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="d1a07-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="d1a07-110">W kolejności toocall hello interfejsu API REST należy przekazać hello klucza dostępu, który można pobrać z portalu Azure dla kolekcji danego obszaru roboczego hello.</span><span class="sxs-lookup"><span data-stu-id="d1a07-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="d1a07-111">Aby uzyskać więcej informacji, zobacz [wprowadzenie w usłudze Power BI Embedded](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d1a07-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="d1a07-112">Pobierz identyfikator raportu</span><span class="sxs-lookup"><span data-stu-id="d1a07-112">Get a report id</span></span>

<span data-ttu-id="d1a07-113">Każdy token dostępu jest oparty na raport.</span><span class="sxs-lookup"><span data-stu-id="d1a07-113">Every access token is based on a report.</span></span> <span data-ttu-id="d1a07-114">Konieczne będzie hello tooget podany identyfikator raportu dla raportu hello, które mają tooembed.</span><span class="sxs-lookup"><span data-stu-id="d1a07-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="d1a07-115">Można to zrobić na toohello wywołania podstawie [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="d1a07-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="d1a07-116">Spowoduje to przywrócenie raportu hello identyfikator i hello osadzić adresu url.</span><span class="sxs-lookup"><span data-stu-id="d1a07-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="d1a07-117">Można to zrobić za pomocą hello Power BI .NET SDK lub bezpośrednie wywoływanie hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="d1a07-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="d1a07-118">Przy użyciu hello Power BI .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d1a07-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="d1a07-119">Używając hello zestawu .NET SDK, konieczne będzie toocreate token poświadczenie opartym na powitania klucz dostępu, uzyskasz od hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d1a07-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="d1a07-120">Wymaga to zainstalowania hello [pakietu NuGet interfejsu API usługi Power BI](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="d1a07-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="d1a07-121">**Instalacja pakietu NuGet**</span><span class="sxs-lookup"><span data-stu-id="d1a07-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="d1a07-122">**Kod w języku C#**</span><span class="sxs-lookup"><span data-stu-id="d1a07-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="d1a07-123">Bezpośrednie wywoływanie hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="d1a07-123">Calling hello REST API directly</span></span>

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

## <a name="create-an-access-token"></a><span data-ttu-id="d1a07-124">Utwórz token dostępu</span><span class="sxs-lookup"><span data-stu-id="d1a07-124">Create an access token</span></span>

<span data-ttu-id="d1a07-125">Power BI Embedded korzystają osadzić token, który HMAC zalogowano tokenów sieci Web JSON.</span><span class="sxs-lookup"><span data-stu-id="d1a07-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="d1a07-126">tokeny Hello są podpisane za pomocą klucza dostępu hello z kolekcji Azure Power BI Embedded obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="d1a07-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="d1a07-127">Osadzaj tokenów, domyślnie, są używane tooprovide odczytać tylko dostęp tooa tooembed raport do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1a07-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="d1a07-128">Osadź tokeny są wydawane dla określonego raportu i powinna być skojarzona z adresem URL osadzania.</span><span class="sxs-lookup"><span data-stu-id="d1a07-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="d1a07-129">Tokeny dostępu należy utworzyć na serwerze hello klucze dostępu hello są używane toosign/szyfrowania tokenów hello.</span><span class="sxs-lookup"><span data-stu-id="d1a07-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="d1a07-130">Aby uzyskać informacje na temat toocreate tokenu dostępu, zobacz [Authenticating i autoryzacji z Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="d1a07-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="d1a07-131">Można również przejrzeć hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metody.</span><span class="sxs-lookup"><span data-stu-id="d1a07-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="d1a07-132">Oto przykład jak to będzie wyglądać przy użyciu hello zestawu .NET SDK dla usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="d1a07-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="d1a07-133">Użyjesz hello identyfikator raportu, który został wcześniej pobrany.</span><span class="sxs-lookup"><span data-stu-id="d1a07-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="d1a07-134">Po osadzić hello jest tworzony token, będzie używać tokenu hello toogenerate klucza dostępu hello, którego można użyć z punktu widzenia javascript hello.</span><span class="sxs-lookup"><span data-stu-id="d1a07-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="d1a07-135">Witaj *klasy PowerBIToken* wymaga zainstalowania hello [Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="d1a07-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="d1a07-136">**Instalacja pakietu NuGet**</span><span class="sxs-lookup"><span data-stu-id="d1a07-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="d1a07-137">**Kod w języku C#**</span><span class="sxs-lookup"><span data-stu-id="d1a07-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="d1a07-138">Dodawanie tokenów tooembed zakresy uprawnień</span><span class="sxs-lookup"><span data-stu-id="d1a07-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="d1a07-139">Tokeny osadzania można toorestrict użycia zasobów hello, który zapewnia dostęp do.</span><span class="sxs-lookup"><span data-stu-id="d1a07-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="d1a07-140">Z tego powodu można wygenerować token z zakresu uprawnień.</span><span class="sxs-lookup"><span data-stu-id="d1a07-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="d1a07-141">Aby uzyskać więcej informacji, zobacz [zakresów](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="d1a07-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="d1a07-142">Osadź przy użyciu języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="d1a07-142">Embed using JavaScript</span></span>

<span data-ttu-id="d1a07-143">Po hello token dostępu i identyfikator raportu hello, możemy osadzić raport hello przy użyciu języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d1a07-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="d1a07-144">Wymaga to zainstalowania hello nuget [pakietu Power BI JavaScript](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="d1a07-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="d1a07-145">Witaj embedUrl będą tylko https://embedded.powerbi.com/appTokenReportEmbed.</span><span class="sxs-lookup"><span data-stu-id="d1a07-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="d1a07-146">Można użyć hello [próbki osadzić raport JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest funkcji.</span><span class="sxs-lookup"><span data-stu-id="d1a07-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="d1a07-147">Udostępnia także przykłady kodu dla różnych operacji hello, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="d1a07-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="d1a07-148">**Instalacja pakietu NuGet**</span><span class="sxs-lookup"><span data-stu-id="d1a07-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="d1a07-149">**Kod JavaScript**</span><span class="sxs-lookup"><span data-stu-id="d1a07-149">**JavaScript code**</span></span>

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

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="d1a07-150">Ustaw rozmiar hello elementów osadzonych</span><span class="sxs-lookup"><span data-stu-id="d1a07-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="d1a07-151">Raport Hello zostanie automatycznie osadzony na podstawie rozmiaru hello swojego kontenera.</span><span class="sxs-lookup"><span data-stu-id="d1a07-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="d1a07-152">rozmiar domyślny hello toooverride hello osadza po prostu Dodaj klasy atrybutu lub wbudowane style CSS na szerokość i wysokość.</span><span class="sxs-lookup"><span data-stu-id="d1a07-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="d1a07-153">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d1a07-153">See also</span></span>

[<span data-ttu-id="d1a07-154">Rozpoczęcie pracy z przykładem</span><span class="sxs-lookup"><span data-stu-id="d1a07-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="d1a07-155">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="d1a07-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="d1a07-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="d1a07-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="d1a07-157">Przykład osadzania skryptu JavaScript</span><span class="sxs-lookup"><span data-stu-id="d1a07-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="d1a07-158">Power BI JavaScript pakietu</span><span class="sxs-lookup"><span data-stu-id="d1a07-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="d1a07-159">[Pakiet NuGet interfejsu API usługi BI zasilania](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut pakietu](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="d1a07-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="d1a07-160">Usługa Power BI CSharp repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="d1a07-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="d1a07-161">Repozytorium Git węzła usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="d1a07-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="d1a07-162">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="d1a07-162">More questions?</span></span> [<span data-ttu-id="d1a07-163">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="d1a07-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
