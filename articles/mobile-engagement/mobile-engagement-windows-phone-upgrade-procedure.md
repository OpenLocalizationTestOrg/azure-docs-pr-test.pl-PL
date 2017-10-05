---
title: Windows Phone Silverlight SDK procedur uaktualniania
description: "Windows Phone Silverlight SDK procedur uaktualniania dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="337a4-103">Windows Phone Silverlight SDK procedur uaktualniania</span><span class="sxs-lookup"><span data-stu-id="337a4-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="337a4-104">Jeśli już jest zintegrowany starszej wersji naszego zestawu SDK do aplikacji, należy wziąć pod uwagę następujące kwestie, podczas uaktualniania zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="337a4-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="337a4-105">Należy wykonać kilka procedur, jeśli pominięte kilka wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="337a4-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="337a4-106">Na przykład w przypadku migrowania z 0.10.1 do 0.11.0, należy najpierw wykonać procedurę "od 0.9.0 do 0.10.1" następnie procedury "od 0.10.1 do 0.11.0".</span><span class="sxs-lookup"><span data-stu-id="337a4-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="337a4-107">Z 2.0.0 do 3.3.0</span><span class="sxs-lookup"><span data-stu-id="337a4-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="337a4-108">Dzienniki testów</span><span class="sxs-lookup"><span data-stu-id="337a4-108">Test logs</span></span>
<span data-ttu-id="337a4-109">Dzienniki konsoli utworzonego przez zestaw SDK można teraz włączone/wyłączone/odfiltrowane.</span><span class="sxs-lookup"><span data-stu-id="337a4-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="337a4-110">Aby dostosować to, zaktualizuj właściwość `EngagementAgent.Instance.TestLogEnabled` do jednej z dostępnych wartości `EngagementTestLogLevel` wyliczenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="337a4-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="337a4-111">Z 1.1.1 do 2.0.0</span><span class="sxs-lookup"><span data-stu-id="337a4-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="337a4-112">Poniżej opisano sposób migracji integracji zestawu SDK usługi Capptain oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="337a4-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="337a4-113">Capptain i usługi Mobile Engagement nie są takie same usługi i procedury przedstawionej poniżej tylko prezentuje sposób migracji aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="337a4-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="337a4-114">Migrowanie zestawu SDK w aplikacji wiadomości nie będzie migrację danych z serwerów Capptain do serwerów usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="337a4-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="337a4-115">W przypadku migracji z wcześniejszej wersji, przejrzyj witrynę sieci web Capptain do pierwszej kolejności przeprowadzenie migracji 1.1.1, zastosuj następującą procedurę</span><span class="sxs-lookup"><span data-stu-id="337a4-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="337a4-116">Pakiet Nuget</span><span class="sxs-lookup"><span data-stu-id="337a4-116">Nuget package</span></span>
<span data-ttu-id="337a4-117">Zastąp **Capptain.WindowsPhone** przez **MicrosoftAzure.MobileEngagement** pakietu Nuget.</span><span class="sxs-lookup"><span data-stu-id="337a4-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="337a4-118">Stosowanie usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="337a4-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="337a4-119">Zestaw SDK używany jest termin `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="337a4-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="337a4-120">Musisz zaktualizować projektu do dopasowania tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="337a4-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="337a4-121">Konieczne jest odinstalowanie bieżącego Capptain pakietu nuget.</span><span class="sxs-lookup"><span data-stu-id="337a4-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="337a4-122">Należy wziąć pod uwagę, że wszystkie zmiany w folderze Capptain zasoby zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="337a4-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="337a4-123">Jeśli chcesz zachować te pliki, a następnie utworzyć ich kopię.</span><span class="sxs-lookup"><span data-stu-id="337a4-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="337a4-124">Po tym należy zainstalować pakiet nuget usługi Microsoft Azure Engagement w projekcie.</span><span class="sxs-lookup"><span data-stu-id="337a4-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="337a4-125">Można go znaleźć bezpośrednio na [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="337a4-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="337a4-126">Ta akcja zastępuje wszystkie pliki zasoby używane przez usługi Engagement i dodaje nowe DLL zaangażowania do odwołania projektu.</span><span class="sxs-lookup"><span data-stu-id="337a4-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="337a4-127">Należy wyczyścić przez usunięcie odwołania do biblioteki DLL Capptain odwołania projektu.</span><span class="sxs-lookup"><span data-stu-id="337a4-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="337a4-128">Jeśli nie wprowadzisz to, wersja Capptain spowoduje konflikt i nastąpi błędy.</span><span class="sxs-lookup"><span data-stu-id="337a4-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="337a4-129">Jeśli dostosowano Capptain zasobów, skopiuj stare pliki zawartości i wklej je w nowych plików zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="337a4-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="337a4-130">Należy pamiętać, że można zaktualizować pliku xaml, jak i cs.</span><span class="sxs-lookup"><span data-stu-id="337a4-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="337a4-131">Po wykonaniu tych kroków należy tylko zastąpić starego odwołania Capptain przez nowego odwołania zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="337a4-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="337a4-132">Wszystkie przestrzenie nazw Capptain wymagają aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="337a4-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="337a4-133">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="337a4-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="337a4-134">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="337a4-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="337a4-135">Wszystkie klasy Capptain, które zawierają "Capptain" powinien zawierać "Zaangażowania".</span><span class="sxs-lookup"><span data-stu-id="337a4-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="337a4-136">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="337a4-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="337a4-137">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="337a4-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="337a4-138">Pliki xaml Capptain przestrzeni nazw i atrybuty także zmienić.</span><span class="sxs-lookup"><span data-stu-id="337a4-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="337a4-139">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="337a4-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="337a4-140">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="337a4-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="337a4-141">Dla innych zasobów, takich jak obrazy Capptain należy pamiętać, że one również zmieniono za pomocą "Engagement".</span><span class="sxs-lookup"><span data-stu-id="337a4-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="337a4-142">Identyfikator aplikacji / klucz zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="337a4-142">Application ID / SDK Key</span></span>
<span data-ttu-id="337a4-143">Zaangażowania używa parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="337a4-143">Engagement uses a connection string.</span></span> <span data-ttu-id="337a4-144">Nie trzeba określić identyfikator i klucz zestawu SDK usługi Mobile Engagement, wystarczy tylko określić parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="337a4-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="337a4-145">Możesz można skonfigurować go na plik EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="337a4-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="337a4-146">Konfiguracja usługi Engagement może zostać ustawiona Twojej `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="337a4-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="337a4-147">Edytuj ten plik, aby określić:</span><span class="sxs-lookup"><span data-stu-id="337a4-147">Edit this file to specify:</span></span>

* <span data-ttu-id="337a4-148">Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="337a4-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="337a4-149">Jeśli chcesz określić je w czasie wykonywania, należy wywołać metodę następujące przed zainicjowaniem agenta usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="337a4-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="337a4-150">Ciąg połączenia dla aplikacji jest wyświetlany w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="337a4-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="337a4-151">Zmiana nazwy elementów</span><span class="sxs-lookup"><span data-stu-id="337a4-151">Items name change</span></span>
<span data-ttu-id="337a4-152">Wszystkie elementy o nazwie *capptain* została nazwana *engagement*.</span><span class="sxs-lookup"><span data-stu-id="337a4-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="337a4-153">Podobnie dla *Capptain* do *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="337a4-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="337a4-154">Przykłady często używanych elementów Capptain:</span><span class="sxs-lookup"><span data-stu-id="337a4-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="337a4-155">CapptainConfiguration teraz nazwę EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="337a4-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="337a4-156">Teraz o nazwie EngagementAgent CapptainAgent</span><span class="sxs-lookup"><span data-stu-id="337a4-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="337a4-157">Teraz o nazwie EngagementReach CapptainReach</span><span class="sxs-lookup"><span data-stu-id="337a4-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="337a4-158">Teraz o nazwie EngagementHttpConfig CapptainHttpConfig</span><span class="sxs-lookup"><span data-stu-id="337a4-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="337a4-159">Teraz o nazwie GetEngagementPageName GetCapptainPageName</span><span class="sxs-lookup"><span data-stu-id="337a4-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="337a4-160">Należy pamiętać, że zmiany nazwy wpływa na przesłoniętej metody.</span><span class="sxs-lookup"><span data-stu-id="337a4-160">Note that rename also affects overridden methods.</span></span>

