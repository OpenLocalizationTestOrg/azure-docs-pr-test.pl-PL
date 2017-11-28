---
title: "Wprowadzenie do usługi Azure Mobile Engagement na potrzeby wdrożenia aplikacji platformy Unity na urządzeniu z systemem Android"
description: "Dowiedz się, jak używać usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami wypychanymi na potrzeby aplikacji platformy Unity wdrażanych na urządzeniach z systemem iOS."
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
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="eb198-103">Wprowadzenie do usługi Azure Mobile Engagement na potrzeby wdrożenia aplikacji platformy Unity na urządzeniu z systemem Android</span><span class="sxs-lookup"><span data-stu-id="eb198-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="eb198-104">W tym temacie pokazano, w jaki sposób za pomocą usługi Azure Mobile Engagement można określić sposób użycia aplikacji oraz wysyłać powiadomienia wypychane do segmentowanych użytkowników aplikacji platformy Unity podczas wdrażania w urządzeniu z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="eb198-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="eb198-105">W tym samouczku jako punkt startowy został użyty klasyczny samouczek Roll a Ball dla platformy Unity.</span><span class="sxs-lookup"><span data-stu-id="eb198-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="eb198-106">Należy postępować zgodnie z krokami w tym [samouczku](mobile-engagement-unity-roll-a-ball.md) przed kontynuowaniem integracji usługi Mobile Engagement, która została przedstawiona w samouczku poniżej.</span><span class="sxs-lookup"><span data-stu-id="eb198-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="eb198-107">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="eb198-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="eb198-108">Edytor platformy Unity</span><span class="sxs-lookup"><span data-stu-id="eb198-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="eb198-109">Zestaw SDK platformy Unity usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="eb198-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="eb198-110">Zestaw SDK systemu Google Android</span><span class="sxs-lookup"><span data-stu-id="eb198-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="eb198-111">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb198-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="eb198-112">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="eb198-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="eb198-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="eb198-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="eb198-114"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="eb198-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="eb198-115"><a id="connecting-app"></a>Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="eb198-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="eb198-116">Importowanie pakietu Unity</span><span class="sxs-lookup"><span data-stu-id="eb198-116">Import the Unity package</span></span>
1. <span data-ttu-id="eb198-117">Pobierz [pakiet Unity usługi Mobile Engagement](https://aka.ms/azmeunitysdk) i zapisz go na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="eb198-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="eb198-118">Wybierz pozycję **Assets -> Import Package -> Custom Package** (Zasoby -> Importuj pakiet -> Pakiet niestandardowy), a następnie wybierz pakiet, który został pobrany w kroku powyżej.</span><span class="sxs-lookup"><span data-stu-id="eb198-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="eb198-119">Upewnij się, że są zaznaczone wszystkie pliki, a następnie kliknij przycisk **Import** (Importuj).</span><span class="sxs-lookup"><span data-stu-id="eb198-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="eb198-120">Gdy import zakończy się pomyślnie, w projekcie będą widoczne zaimportowane pliki zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="eb198-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="eb198-121">Aktualizowanie pliku skryptu EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="eb198-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="eb198-122">Otwórz pliku skryptu **EngagementConfiguration** z folderu zestawu SDK, a następnie zaktualizuj zmienną **ANDROID\_CONNECTION\_STRING** parametrami połączenia uzyskanymi wcześniej z witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="eb198-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="eb198-123">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="eb198-123">Save the file</span></span> 
3. <span data-ttu-id="eb198-124">Wykonaj polecenie **File -> Engagement -> Generate Android Manifest** (Plik -> Engagement -> Generowanie manifestu systemu Android).</span><span class="sxs-lookup"><span data-stu-id="eb198-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="eb198-125">Jest to wtyczka dodana przez zestaw SDK usługi Mobile Engagement i kliknięcie jej spowoduje automatyczne zaktualizowanie ustawień projektu.</span><span class="sxs-lookup"><span data-stu-id="eb198-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="eb198-126">Upewnij się, że to polecenie będzie wykonywane za każdym razem, gdy plik **EngagementConfiguration** zostanie zaktualizowany — w przeciwnym razie zmiany nie zostaną odzwierciedlone w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb198-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="eb198-127">Konfigurowanie aplikacji na potrzeby śledzenia podstawowego</span><span class="sxs-lookup"><span data-stu-id="eb198-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="eb198-128">Otwórz do edycji skrypt **PlayerController** dołączony do obiektu Player.</span><span class="sxs-lookup"><span data-stu-id="eb198-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="eb198-129">Dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="eb198-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="eb198-130">Dodaj następujący kod do metody `Start()`:</span><span class="sxs-lookup"><span data-stu-id="eb198-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="eb198-131">Wdrażanie i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="eb198-131">Deploy and run the app</span></span>
<span data-ttu-id="eb198-132">Przed próbą wdrożenia tej aplikacji platformy Unity na urządzeniu upewnij się, że na komputerze jest zainstalowany zestaw SDK systemu Android.</span><span class="sxs-lookup"><span data-stu-id="eb198-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="eb198-133">Podłącz urządzenie z systemem Android do swojego komputera.</span><span class="sxs-lookup"><span data-stu-id="eb198-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="eb198-134">Wybierz pozycję **File -> Build Settings** (Plik -> Ustawienia kompilacji).</span><span class="sxs-lookup"><span data-stu-id="eb198-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="eb198-135">Wybierz pozycję **Android** a następnie kliknij pozycję **Switch Platform** (Przełącz platformę).</span><span class="sxs-lookup"><span data-stu-id="eb198-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="eb198-136">Kliknij pozycję **Player settings** (Ustawienia odtwarzacza) i podaj prawidłowy identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb198-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="eb198-137">Na koniec kliknij pozycję **Build And Run** (Kompiluj i uruchom).</span><span class="sxs-lookup"><span data-stu-id="eb198-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="eb198-138">Może pojawić się monit o podanie nazwy folderu do przechowywania pakietu systemu Android.</span><span class="sxs-lookup"><span data-stu-id="eb198-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="eb198-139">Jeśli wszystko odbędzie się poprawnie, pakiet zostanie wdrożony na podłączonym urządzeniu i na telefonie będzie widoczna Twoja gra na platformie Unity.</span><span class="sxs-lookup"><span data-stu-id="eb198-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="eb198-140"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="eb198-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="eb198-141"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="eb198-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="eb198-142">Aktualizowanie pliku skryptu EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="eb198-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="eb198-143">Otwórz plik skryptu **EngagementConfiguration** z folderu zestawu SDK i zaktualizuj zmienną **ANDROID\_GOOGLE\_NUMBER** **numerem projektu Google** uzyskanym wcześniej z portalu Google Cloud Developer.</span><span class="sxs-lookup"><span data-stu-id="eb198-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="eb198-144">Jest to wartość ciągu, więc upewnij się, że została ujęta w cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="eb198-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="eb198-145">Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="eb198-145">Save the file.</span></span> 
3. <span data-ttu-id="eb198-146">Wykonaj polecenie **File -> Engagement -> Generate Android Manifest** (Plik -> Engagement -> Generowanie manifestu systemu Android).</span><span class="sxs-lookup"><span data-stu-id="eb198-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="eb198-147">Jest to wtyczka dodana przez zestaw SDK usługi Mobile Engagement i kliknięcie jej spowoduje automatyczne zaktualizowanie ustawień projektu.</span><span class="sxs-lookup"><span data-stu-id="eb198-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="eb198-148">Konfigurowanie aplikacji na potrzeby otrzymywania powiadomień</span><span class="sxs-lookup"><span data-stu-id="eb198-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="eb198-149">Otwórz do edycji skrypt **PlayerController** dołączony do obiektu Player.</span><span class="sxs-lookup"><span data-stu-id="eb198-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="eb198-150">Dodaj następujący kod do metody `Start()`:</span><span class="sxs-lookup"><span data-stu-id="eb198-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="eb198-151">Teraz, gdy aplikacja jest zaktualizowana, wdróż i uruchom aplikację na urządzeniu zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="eb198-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

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
