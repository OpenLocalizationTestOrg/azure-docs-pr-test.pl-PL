---
title: "aaaGet Started with Azure Mobile Engagement dla wdrożenia iOS Unity"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji platformy Unity wdrażanych tooiOS urządzeń."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="f7c15-103">Wprowadzenie do usługi Azure Mobile Engagement na potrzeby wdrożenia aplikacji platformy Unity na urządzeniu z systemem iOS</span><span class="sxs-lookup"><span data-stu-id="f7c15-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="f7c15-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji oraz jak toosend wypychanie powiadomień toosegmented użytkowników aplikacji platformy Unity podczas wdrażania tooan urządzenie z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="f7c15-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="f7c15-105">Ten samouczek używa hello klasycznego Przywróć Unity samouczek piłka jako punkt początkowy hello.</span><span class="sxs-lookup"><span data-stu-id="f7c15-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="f7c15-106">Należy wykonać kroki hello na tym [samouczek](mobile-engagement-unity-roll-a-ball.md) przed kontynuowaniem hello integracji usługi Mobile Engagement, która została przedstawiona w samouczku hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="f7c15-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="f7c15-107">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="f7c15-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="f7c15-108">Edytor platformy Unity</span><span class="sxs-lookup"><span data-stu-id="f7c15-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="f7c15-109">Zestaw SDK platformy Unity usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f7c15-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="f7c15-110">Edytor XCode</span><span class="sxs-lookup"><span data-stu-id="f7c15-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="f7c15-111">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7c15-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f7c15-112">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f7c15-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f7c15-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="f7c15-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="f7c15-114"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="f7c15-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="f7c15-115"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7c15-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="f7c15-116">Importowanie pakietu Unity hello</span><span class="sxs-lookup"><span data-stu-id="f7c15-116">Import hello Unity package</span></span>
1. <span data-ttu-id="f7c15-117">Pobierz hello [pakiet Unity usługi Mobile Engagement](https://aka.ms/azmeunitysdk) i zapisz go tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f7c15-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="f7c15-118">Przejdź za**zasoby -> Importuj pakiet -> Pakiet niestandardowy** i wybierz hello pakietu pobranego w hello powyżej kroku.</span><span class="sxs-lookup"><span data-stu-id="f7c15-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="f7c15-119">Upewnij się, że są zaznaczone wszystkie pliki, a następnie kliknij przycisk **Import** (Importuj).</span><span class="sxs-lookup"><span data-stu-id="f7c15-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="f7c15-120">Gdy Import zakończy się pomyślnie, zobaczysz hello zaimportowane pliki zestawu SDK w projekcie.</span><span class="sxs-lookup"><span data-stu-id="f7c15-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="f7c15-121">Aktualizacja hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="f7c15-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="f7c15-122">Otwórz hello **EngagementConfiguration** pliku skryptu z zestawu SDK hello hello folderu i zaktualizuj **IOS\_połączenia\_ciąg** z hello parametry połączenia uzyskanymi wcześniej z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f7c15-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="f7c15-123">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="f7c15-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="f7c15-124">Konfigurowanie aplikacji hello na potrzeby śledzenia podstawowego</span><span class="sxs-lookup"><span data-stu-id="f7c15-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="f7c15-125">Otwórz hello **PlayerController** skrypt dołączony obiektu Player toohello.</span><span class="sxs-lookup"><span data-stu-id="f7c15-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="f7c15-126">Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="f7c15-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="f7c15-127">Dodaj następujące toohello hello `Start()` — metoda</span><span class="sxs-lookup"><span data-stu-id="f7c15-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="f7c15-128">Wdrażanie i uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f7c15-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="f7c15-129">Podłącz maszynę tooyour urządzenia z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="f7c15-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="f7c15-130">Wybierz pozycję **File -> Build Settings** (Plik -> Ustawienia kompilacji).</span><span class="sxs-lookup"><span data-stu-id="f7c15-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="f7c15-131">Wybierz pozycję **iOS**, a następnie kliknij pozycję **Switch Platform** (Przełącz platformę).</span><span class="sxs-lookup"><span data-stu-id="f7c15-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="f7c15-132">Kliknij pozycję **Player settings** (Ustawienia odtwarzacza) i podaj prawidłowy identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="f7c15-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="f7c15-133">Na koniec kliknij pozycję **Build And Run** (Kompiluj i uruchom).</span><span class="sxs-lookup"><span data-stu-id="f7c15-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="f7c15-134">Może być zadawane tooprovide pakietu systemu iOS hello toostore nazwę folderu.</span><span class="sxs-lookup"><span data-stu-id="f7c15-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="f7c15-135">Jeśli wszystko odbędzie się poprawnie, hello projekt zostanie skompilowany i należy otwierać w aplikacji XCode.</span><span class="sxs-lookup"><span data-stu-id="f7c15-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="f7c15-136">Upewnij się, że hello **identyfikator pakietu** jest prawidłowa w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="f7c15-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="f7c15-137">Teraz uruchamianie aplikacji hello w środowisku XCode, dzięki czemu pakietów hello jest tooyour wdrożony na podłączonym urządzeniu i na telefonie będzie widoczna gry środowiska Unity!</span><span class="sxs-lookup"><span data-stu-id="f7c15-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="f7c15-138"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="f7c15-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="f7c15-139"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7c15-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="f7c15-140">Usługa Mobile Engagement umożliwia toointeract z użytkownikami i ZASIĘGU z powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7c15-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="f7c15-141">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="f7c15-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="f7c15-142">Nie można znaleźć toodo żadnej dodatkowej konfiguracji powiadomienia tooreceive aplikacji i jest już skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="f7c15-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
