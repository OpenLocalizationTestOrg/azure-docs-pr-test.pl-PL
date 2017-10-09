---
title: "aaaGet Started with Azure Mobile Engagement Unity Android wdrożenia"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji platformy Unity wdrażanych tooiOS urządzeń."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="de9d4-103">Wprowadzenie do usługi Azure Mobile Engagement na potrzeby wdrożenia aplikacji platformy Unity na urządzeniu z systemem Android</span><span class="sxs-lookup"><span data-stu-id="de9d4-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="de9d4-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji oraz jak toosend wypychanie powiadomień toosegmented użytkowników aplikacji platformy Unity podczas wdrażania tooan urządzenia z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="de9d4-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="de9d4-105">Ten samouczek używa hello klasycznego Przywróć Unity samouczek piłka jako punkt początkowy hello.</span><span class="sxs-lookup"><span data-stu-id="de9d4-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="de9d4-106">Należy wykonać kroki hello na tym [samouczek](mobile-engagement-unity-roll-a-ball.md) przed kontynuowaniem hello integracji usługi Mobile Engagement, która została przedstawiona w samouczku hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="de9d4-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="de9d4-107">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="de9d4-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="de9d4-108">Edytor platformy Unity</span><span class="sxs-lookup"><span data-stu-id="de9d4-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="de9d4-109">Zestaw SDK platformy Unity usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="de9d4-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="de9d4-110">Zestaw SDK systemu Google Android</span><span class="sxs-lookup"><span data-stu-id="de9d4-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="de9d4-111">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de9d4-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="de9d4-112">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="de9d4-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="de9d4-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="de9d4-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="de9d4-114"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="de9d4-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="de9d4-115"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="de9d4-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="de9d4-116">Importowanie pakietu Unity hello</span><span class="sxs-lookup"><span data-stu-id="de9d4-116">Import hello Unity package</span></span>
1. <span data-ttu-id="de9d4-117">Pobierz hello [pakiet Unity usługi Mobile Engagement](https://aka.ms/azmeunitysdk) i zapisz go tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="de9d4-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="de9d4-118">Przejdź za**zasoby -> Importuj pakiet -> Pakiet niestandardowy** i wybierz hello pakietu pobranego w hello powyżej kroku.</span><span class="sxs-lookup"><span data-stu-id="de9d4-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="de9d4-119">Upewnij się, że są zaznaczone wszystkie pliki, a następnie kliknij przycisk **Import** (Importuj).</span><span class="sxs-lookup"><span data-stu-id="de9d4-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="de9d4-120">Gdy Import zakończy się pomyślnie, zobaczysz hello zaimportowane pliki zestawu SDK w projekcie.</span><span class="sxs-lookup"><span data-stu-id="de9d4-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="de9d4-121">Aktualizacja hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="de9d4-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="de9d4-122">Otwórz hello **EngagementConfiguration** pliku skryptu z zestawu SDK hello hello folderu i zaktualizuj **ANDROID\_połączenia\_ciąg** parametrami połączenia hello uzyskanymi wcześniej z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="de9d4-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="de9d4-123">Zapisz plik hello</span><span class="sxs-lookup"><span data-stu-id="de9d4-123">Save hello file</span></span> 
3. <span data-ttu-id="de9d4-124">Wykonaj polecenie **File -> Engagement -> Generate Android Manifest** (Plik -> Engagement -> Generowanie manifestu systemu Android).</span><span class="sxs-lookup"><span data-stu-id="de9d4-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="de9d4-125">Jest to hello wtyczka dodana przez zestaw SDK usługi Mobile Engagement hello i kliknięcie jej automatycznie spowoduje zaktualizowanie ustawień projektu.</span><span class="sxs-lookup"><span data-stu-id="de9d4-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="de9d4-126">Upewnij się, że tooexecute to za każdym razem, gdy hello **EngagementConfiguration** pliku, w przeciwnym razie zmiany nie zostaną odzwierciedlone w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="de9d4-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="de9d4-127">Konfigurowanie aplikacji hello na potrzeby śledzenia podstawowego</span><span class="sxs-lookup"><span data-stu-id="de9d4-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="de9d4-128">Otwórz hello **PlayerController** skrypt dołączony obiektu Player toohello.</span><span class="sxs-lookup"><span data-stu-id="de9d4-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="de9d4-129">Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="de9d4-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="de9d4-130">Dodaj następujące toohello hello `Start()` — metoda</span><span class="sxs-lookup"><span data-stu-id="de9d4-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="de9d4-131">Wdrażanie i uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="de9d4-131">Deploy and run hello app</span></span>
<span data-ttu-id="de9d4-132">Upewnij się, że zestaw SDK systemu Android zainstalowane na komputerze przed podjęciem próby wykonania toodeploy to urządzenie tooyour aplikacji platformy Unity.</span><span class="sxs-lookup"><span data-stu-id="de9d4-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="de9d4-133">Podłącz urządzenie z systemem Android tooyour maszynę.</span><span class="sxs-lookup"><span data-stu-id="de9d4-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="de9d4-134">Wybierz pozycję **File -> Build Settings** (Plik -> Ustawienia kompilacji).</span><span class="sxs-lookup"><span data-stu-id="de9d4-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="de9d4-135">Wybierz pozycję **Android** a następnie kliknij pozycję **Switch Platform** (Przełącz platformę).</span><span class="sxs-lookup"><span data-stu-id="de9d4-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="de9d4-136">Kliknij pozycję **Player settings** (Ustawienia odtwarzacza) i podaj prawidłowy identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="de9d4-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="de9d4-137">Na koniec kliknij pozycję **Build And Run** (Kompiluj i uruchom).</span><span class="sxs-lookup"><span data-stu-id="de9d4-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="de9d4-138">Może być zadawane tooprovide folderu nazwa toostore hello pakietu systemu Android.</span><span class="sxs-lookup"><span data-stu-id="de9d4-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="de9d4-139">Jeśli wszystko odbędzie poprawnie, pakiet hello zostaną wdrożone tooyour połączone urządzenia i powinien być widoczny gry środowiska Unity w telefonie!</span><span class="sxs-lookup"><span data-stu-id="de9d4-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="de9d4-140"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="de9d4-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="de9d4-141"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="de9d4-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="de9d4-142">Aktualizacja hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="de9d4-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="de9d4-143">Otwórz hello **EngagementConfiguration** pliku skryptu z zestawu SDK hello hello folderu i zaktualizuj **ANDROID\_GOOGLE\_numer** z hello **projektu Google Numer** uzyskanymi wcześniej z portalu Google Cloud Developer hello.</span><span class="sxs-lookup"><span data-stu-id="de9d4-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="de9d4-144">Jest to ciąg wartości, dlatego upewnij się, że tooenclose ją w podwójny cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="de9d4-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="de9d4-145">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="de9d4-145">Save hello file.</span></span> 
3. <span data-ttu-id="de9d4-146">Wykonaj polecenie **File -> Engagement -> Generate Android Manifest** (Plik -> Engagement -> Generowanie manifestu systemu Android).</span><span class="sxs-lookup"><span data-stu-id="de9d4-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="de9d4-147">Jest to hello wtyczka dodana przez zestaw SDK usługi Mobile Engagement hello i kliknięcie jej automatycznie spowoduje zaktualizowanie ustawień projektu.</span><span class="sxs-lookup"><span data-stu-id="de9d4-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="de9d4-148">Konfigurowanie powiadomień tooreceive aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="de9d4-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="de9d4-149">Otwórz hello **PlayerController** skrypt dołączony obiektu Player toohello.</span><span class="sxs-lookup"><span data-stu-id="de9d4-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="de9d4-150">Dodaj następujące toohello hello `Start()` — metoda</span><span class="sxs-lookup"><span data-stu-id="de9d4-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="de9d4-151">Teraz, gdy hello aplikacja jest zaktualizowana, wdrażanie i uruchamianie aplikacji hello na urządzeniu na powitania poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="de9d4-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
