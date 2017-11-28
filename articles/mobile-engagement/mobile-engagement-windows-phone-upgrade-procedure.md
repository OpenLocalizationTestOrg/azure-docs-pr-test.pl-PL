---
title: aaaWindows procedur uaktualniania Phone Silverlight SDK
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
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="c7fba-103">Windows Phone Silverlight SDK procedur uaktualniania</span><span class="sxs-lookup"><span data-stu-id="c7fba-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="c7fba-104">Jeśli już jest zintegrowany starszej wersji naszego zestawu SDK do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c7fba-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="c7fba-105">Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="c7fba-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="c7fba-106">Na przykład w przypadku migracji z 0.10.1 too0.11.0 masz toofirst wykonaj hello "z 0.9.0 too0.10.1" procedury, a następnie hello "z 0.10.1 too0.11.0" procedury.</span><span class="sxs-lookup"><span data-stu-id="c7fba-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="c7fba-107">Z 2.0.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="c7fba-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="c7fba-108">Dzienniki testów</span><span class="sxs-lookup"><span data-stu-id="c7fba-108">Test logs</span></span>
<span data-ttu-id="c7fba-109">Dzienniki konsoli utworzonego przez zestaw SDK hello można teraz włączone/wyłączone/odfiltrowane.</span><span class="sxs-lookup"><span data-stu-id="c7fba-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="c7fba-110">toocustomize ta, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone hello wartość dostępna hello `EngagementTestLogLevel` wyliczenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="c7fba-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="c7fba-111">Z 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="c7fba-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="c7fba-112">Witaj poniżej opisano sposób toomigrate integracji zestawu SDK z hello Capptain usługi oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c7fba-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c7fba-113">Capptain i usługi Mobile Engagement nie hello tej samej usługi i procedury hello tylko podane poniżej prezentuje sposób toomigrate hello aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="c7fba-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="c7fba-114">Migrowanie hello zestawu SDK w aplikacji hello nie będą migrowane dane z hello Capptain serwerów toohello Mobile Engagement serwerów</span><span class="sxs-lookup"><span data-stu-id="c7fba-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="c7fba-115">W przypadku migracji z wcześniejszej wersji, należy najpierw zapoznaj się hello Capptain witryny sieci web toomigrate too1.1.1, zastosuj hello procedury</span><span class="sxs-lookup"><span data-stu-id="c7fba-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="c7fba-116">Pakiet Nuget</span><span class="sxs-lookup"><span data-stu-id="c7fba-116">Nuget package</span></span>
<span data-ttu-id="c7fba-117">Zastąp **Capptain.WindowsPhone** przez **MicrosoftAzure.MobileEngagement** pakietu Nuget.</span><span class="sxs-lookup"><span data-stu-id="c7fba-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="c7fba-118">Stosowanie usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c7fba-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="c7fba-119">Hello SDK używany termin hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="c7fba-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="c7fba-120">Należy tooupdate toomatch Twojego projektu tej zmiany.</span><span class="sxs-lookup"><span data-stu-id="c7fba-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="c7fba-121">Należy toouninstall bieżącego Capptain pakietu nuget.</span><span class="sxs-lookup"><span data-stu-id="c7fba-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="c7fba-122">Należy wziąć pod uwagę, że wszystkie zmiany w folderze Capptain zasoby zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="c7fba-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="c7fba-123">Jeśli tookeep tych plików, a następnie utworzyć ich kopię.</span><span class="sxs-lookup"><span data-stu-id="c7fba-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="c7fba-124">Po wykonaniu tej instalacji nowego pakietu nuget usługi Microsoft Azure Engagement hello w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c7fba-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="c7fba-125">Można go znaleźć bezpośrednio na [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="c7fba-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="c7fba-126">Zastępuje tej akcji, wszystkich plików zasobów używanych przez usługi Engagement i dodaje nowe tooyour DLL zaangażowania hello projektu odwołań.</span><span class="sxs-lookup"><span data-stu-id="c7fba-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="c7fba-127">Masz tooclean odwołania projektu o usunięcie odwołania do biblioteki DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="c7fba-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="c7fba-128">Jeśli nie wprowadzisz to, wersja hello Capptain spowoduje konflikt i nastąpi błędy.</span><span class="sxs-lookup"><span data-stu-id="c7fba-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="c7fba-129">Jeśli dostosowano Capptain zasobów, skopiuj stare pliki zawartości i wklej je w nowych plików zaangażowania hello.</span><span class="sxs-lookup"><span data-stu-id="c7fba-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="c7fba-130">Należy pamiętać, że pliku xaml, jak i cs toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7fba-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="c7fba-131">Po wykonaniu tych kroków wystarczy tooreplace stare odwołania Capptain przez hello nowych zaangażowania odwołań.</span><span class="sxs-lookup"><span data-stu-id="c7fba-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="c7fba-132">Wszystkie przestrzenie nazw Capptain ma toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="c7fba-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="c7fba-133">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="c7fba-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="c7fba-134">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="c7fba-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="c7fba-135">Wszystkie klasy Capptain, które zawierają "Capptain" powinien zawierać "Zaangażowania".</span><span class="sxs-lookup"><span data-stu-id="c7fba-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="c7fba-136">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="c7fba-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="c7fba-137">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="c7fba-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="c7fba-138">Pliki xaml Capptain przestrzeni nazw i atrybuty także zmienić.</span><span class="sxs-lookup"><span data-stu-id="c7fba-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="c7fba-139">Przed migracją:</span><span class="sxs-lookup"><span data-stu-id="c7fba-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="c7fba-140">Po zakończeniu migracji:</span><span class="sxs-lookup"><span data-stu-id="c7fba-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="c7fba-141">Dla hello innych zasobów, takich jak obrazy Capptain należy pamiętać, że również zostały toouse zmieniono nazwę "Zaangażowania".</span><span class="sxs-lookup"><span data-stu-id="c7fba-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="c7fba-142">Identyfikator aplikacji / klucz zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="c7fba-142">Application ID / SDK Key</span></span>
<span data-ttu-id="c7fba-143">Zaangażowania używa parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="c7fba-143">Engagement uses a connection string.</span></span> <span data-ttu-id="c7fba-144">Nie masz toospecify identyfikator i klucz zestawu SDK z usługi Mobile Engagement, wystarczy toospecify ciąg połączenia.</span><span class="sxs-lookup"><span data-stu-id="c7fba-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="c7fba-145">Możesz można skonfigurować go na plik EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="c7fba-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="c7fba-146">Konfiguracja zaangażowania Hello może zostać ustawiona Twojej `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c7fba-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="c7fba-147">Edytuj toospecify tego pliku:</span><span class="sxs-lookup"><span data-stu-id="c7fba-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="c7fba-148">Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="c7fba-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="c7fba-149">Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:</span><span class="sxs-lookup"><span data-stu-id="c7fba-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="c7fba-150">Parametry połączenia Hello aplikacji jest wyświetlany w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c7fba-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="c7fba-151">Zmiana nazwy elementów</span><span class="sxs-lookup"><span data-stu-id="c7fba-151">Items name change</span></span>
<span data-ttu-id="c7fba-152">Wszystkie elementy o nazwie *capptain* została nazwana *engagement*.</span><span class="sxs-lookup"><span data-stu-id="c7fba-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="c7fba-153">Podobnie dla *Capptain* za*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="c7fba-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="c7fba-154">Przykłady często używanych elementów Capptain:</span><span class="sxs-lookup"><span data-stu-id="c7fba-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="c7fba-155">CapptainConfiguration teraz nazwę EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="c7fba-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="c7fba-156">Teraz o nazwie EngagementAgent CapptainAgent</span><span class="sxs-lookup"><span data-stu-id="c7fba-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="c7fba-157">Teraz o nazwie EngagementReach CapptainReach</span><span class="sxs-lookup"><span data-stu-id="c7fba-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="c7fba-158">Teraz o nazwie EngagementHttpConfig CapptainHttpConfig</span><span class="sxs-lookup"><span data-stu-id="c7fba-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="c7fba-159">Teraz o nazwie GetEngagementPageName GetCapptainPageName</span><span class="sxs-lookup"><span data-stu-id="c7fba-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="c7fba-160">Należy pamiętać, że zmiany nazwy wpływa na przesłoniętej metody.</span><span class="sxs-lookup"><span data-stu-id="c7fba-160">Note that rename also affects overridden methods.</span></span>

