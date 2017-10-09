---
title: "aaaGet wprowadzenie do usługi Azure Notification Hubs przy użyciu usługi Baidu | Dokumentacja firmy Microsoft"
description: "Z tego samouczka, dowiesz się, jak toouse usługi Azure Notification Hubs toopush powiadomienia tooAndroid urządzeń przy użyciu usługi Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="202ea-103">Rozpoczynanie pracy z usługą Azure Notification Hubs przy użyciu usługi Baidu</span><span class="sxs-lookup"><span data-stu-id="202ea-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="202ea-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="202ea-104">Overview</span></span>
<span data-ttu-id="202ea-105">Wypychane w chmurze Baidu to chińska usługa w chmurze czy można używać urządzeń toomobile powiadomień wypychanych toosend.</span><span class="sxs-lookup"><span data-stu-id="202ea-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="202ea-106">Ta usługa jest przydatna w Chinach, gdzie dostarczanie powiadomień wypychanych tooAndroid jest złożony z powodu obecności hello różnych sklepów z aplikacjami i wypychania usług, oprócz toohello dostępności urządzeń z systemem Android, które nie są zazwyczaj połączone tooGCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="202ea-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="202ea-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="202ea-107">Prerequisites</span></span>
<span data-ttu-id="202ea-108">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="202ea-108">This tutorial requires:</span></span>

* <span data-ttu-id="202ea-109">Zestaw SDK systemu android (założono, że używane jest środowisko Eclipse), który można pobrać z hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">witryny systemu Android</a></span><span class="sxs-lookup"><span data-stu-id="202ea-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="202ea-110">[Zestaw SDK usługi Mobile Services dla systemu Android]</span><span class="sxs-lookup"><span data-stu-id="202ea-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="202ea-111">[Baidu Push zestawu SDK systemu Android]</span><span class="sxs-lookup"><span data-stu-id="202ea-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="202ea-112">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="202ea-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="202ea-113">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="202ea-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="202ea-114">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="202ea-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="202ea-115">Tworzenia konta usługi Baidu</span><span class="sxs-lookup"><span data-stu-id="202ea-115">Create a Baidu account</span></span>
<span data-ttu-id="202ea-116">toouse Baidu, musisz mieć konto Baidu.</span><span class="sxs-lookup"><span data-stu-id="202ea-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="202ea-117">Jeśli masz już konto, zaloguj się za toohello [portalu Baidu] i pominąć toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="202ea-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="202ea-118">W przeciwnym razie zobacz następujące instrukcje na temat hello toocreate konta usługi Baidu.</span><span class="sxs-lookup"><span data-stu-id="202ea-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="202ea-119">Przejdź toohello [portalu Baidu] i kliknij przycisk hello**登录**(**logowania**) łącza.</span><span class="sxs-lookup"><span data-stu-id="202ea-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="202ea-120">Kliknij przycisk**立即注册**procesu rejestracji konta hello toostart.</span><span class="sxs-lookup"><span data-stu-id="202ea-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="202ea-121">Wprowadź szczegóły hello wymagane — phone/poczta e-mail adres, hasło i kod weryfikacyjny — i kliknij przycisk **Signup**.</span><span class="sxs-lookup"><span data-stu-id="202ea-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="202ea-122">Powoduje wysłanie adresu e-mail toohello e-mail wprowadzony z tooactivate łącze konta usługi Baidu.</span><span class="sxs-lookup"><span data-stu-id="202ea-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="202ea-123">Zaloguj się za tooyour konto e-mail, Otwórz wiadomość hello Baidu i kliknij tooactivate link aktywacji hello konta usługi Baidu.</span><span class="sxs-lookup"><span data-stu-id="202ea-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="202ea-124">Po aktywowaniu konta usługi Baidu Zaloguj toohello [portalu Baidu].</span><span class="sxs-lookup"><span data-stu-id="202ea-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="202ea-125">Rejestrowanie się jako deweloper usługi Baidu</span><span class="sxs-lookup"><span data-stu-id="202ea-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="202ea-126">Po zalogowaniu toohello [portalu Baidu], kliknij przycisk**更多 >>** (**więcej**).</span><span class="sxs-lookup"><span data-stu-id="202ea-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="202ea-127">Przewiń w dół w hello**站长与开发者服务 (Webmaster i usług deweloperskich)** sekcji, a następnie kliknij przycisk**百度开放云平台**(**Baidu otwartej platformy chmury**).</span><span class="sxs-lookup"><span data-stu-id="202ea-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="202ea-128">Na następnej stronie powitania kliknij**开发者服务**(**usług deweloperskich**) na powitania prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="202ea-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="202ea-129">Na następnej stronie powitania kliknij**注册开发者**(**zarejestrowany deweloperzy**) z menu hello na powitania prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="202ea-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="202ea-130">Wprowadź imię i nazwisko, opis oraz numer telefonu komórkowego do odebrania weryfikacyjnej wiadomości tekstowej, a następnie kliknij pozycję **送验证码** (**Wyślij kod weryfikacyjny**).</span><span class="sxs-lookup"><span data-stu-id="202ea-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="202ea-131">Międzynarodowych numerów telefonów należy tooenclose numer kierunkowy kraju hello w nawiasach.</span><span class="sxs-lookup"><span data-stu-id="202ea-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="202ea-132">Na przykład numer dla Stanów Zjednoczonych ma postać **(1)1234567890**.</span><span class="sxs-lookup"><span data-stu-id="202ea-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="202ea-133">Otrzymasz wiadomość SMS zawierającą numer weryfikacyjny, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="202ea-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="202ea-134">Wprowadź numer weryfikacyjny hello z wiadomość hello w**验证码**(**kod potwierdzenia**).</span><span class="sxs-lookup"><span data-stu-id="202ea-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="202ea-135">Na koniec Ukończ hello developer rejestracja akceptowania hello Baidu umowę, a następnie klikając polecenie**提交**(**przesyłania**).</span><span class="sxs-lookup"><span data-stu-id="202ea-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="202ea-136">Zostanie wyświetlony hello następujące strony w pomyślnym ukończeniu rejestracji:</span><span class="sxs-lookup"><span data-stu-id="202ea-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="202ea-137">Tworzenie projektu powiadomień wypychanych w chmurze Baidu</span><span class="sxs-lookup"><span data-stu-id="202ea-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="202ea-138">Podczas tworzenia projektu powiadomień wypychanych w chmurze Baidu otrzymasz identyfikator aplikacji, klucz interfejsu API i klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="202ea-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="202ea-139">Po zalogowaniu toohello [portalu Baidu], kliknij przycisk**更多 >>** (**więcej**).</span><span class="sxs-lookup"><span data-stu-id="202ea-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="202ea-140">Przewiń w dół w hello**站长与开发者服务**(**Webmaster i usług deweloperskich**) i kliknij pozycję**百度开放云平台**(**Baidu otwartej platformy chmury**).</span><span class="sxs-lookup"><span data-stu-id="202ea-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="202ea-141">Na następnej stronie powitania kliknij**开发者服务**(**usług deweloperskich**) na powitania prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="202ea-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="202ea-142">Na następnej stronie powitania kliknij**云推送**(**Cloud Push**) z hello**云服务**(**usługi w chmurze**) sekcji.</span><span class="sxs-lookup"><span data-stu-id="202ea-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="202ea-143">Gdy jesteś deweloperem zarejestrowany, zostanie wyświetlony**管理控制台**(**konsoli zarządzania**) w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="202ea-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="202ea-144">Kliknij pozycję **开发者服务管理** (**Zarządzanie usługami dla deweloperów**).</span><span class="sxs-lookup"><span data-stu-id="202ea-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="202ea-145">Na następnej stronie powitania kliknij**创建工程**(**tworzenia projektu**).</span><span class="sxs-lookup"><span data-stu-id="202ea-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="202ea-146">Wprowadź nazwę aplikacji, a następnie kliknij pozycję **创建** (**Utwórz**).</span><span class="sxs-lookup"><span data-stu-id="202ea-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="202ea-147">Po pomyślnym utworzeniu projektu powiadomień wypychanych w chmurze Baidu zostanie wyświetlona strona zawierająca następujące dane: **AppID** (Identyfikator aplikacji), **API Key** (Klucz interfejsu API) i **Secret Key** (Klucz tajny).</span><span class="sxs-lookup"><span data-stu-id="202ea-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="202ea-148">Zanotuj klucz interfejsu API hello i klucz tajny, który zostanie wykorzystany później.</span><span class="sxs-lookup"><span data-stu-id="202ea-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="202ea-149">Konfigurowanie hello projektu powiadomień wypychanych, klikając**云推送**(**wypychane w chmurze**) w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="202ea-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="202ea-150">Na następnej stronie powitania kliknij hello**推送设置**(**Push ustawienia**) przycisku.</span><span class="sxs-lookup"><span data-stu-id="202ea-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="202ea-151">Na stronie konfiguracji hello Dodaj hello nazwy pakietu, który będzie używany w projekcie systemu Android w hello**应用包名**(**pakiet aplikacji**) do pola, a następnie kliknij przycisk**保存设置**() **Zapisać**).</span><span class="sxs-lookup"><span data-stu-id="202ea-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="202ea-152">Zobacz hello**保存成功!** (**Zapisano pomyślnie!**).</span><span class="sxs-lookup"><span data-stu-id="202ea-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="202ea-153">Konfigurowanie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="202ea-153">Configure your notification hub</span></span>
1. <span data-ttu-id="202ea-154">Zaloguj się toohello [klasycznego portalu Azure], a następnie kliknij przycisk **+ nowy** u dołu ekranu hello hello.</span><span class="sxs-lookup"><span data-stu-id="202ea-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="202ea-155">Kliknij pozycję **App Services**, pozycję **Service Bus** i pozycję **Centrum powiadomień**, a następnie kliknij pozycję **Szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="202ea-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="202ea-156">Podaj nazwę użytkownika **Centrum powiadomień**, wybierz pozycję hello **Region** i hello **Namespace** gdzie zostanie utworzone Centrum powiadomień, a następnie kliknij  **Tworzenie nowego centrum powiadomień**.</span><span class="sxs-lookup"><span data-stu-id="202ea-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="202ea-157">Kliknij przestrzeń nazw hello, w której utworzono Centrum powiadomień, a następnie kliknij przycisk **usługi Notification Hubs** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="202ea-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="202ea-158">Centrum powiadomień hello wybierz utworzony, a następnie kliknij przycisk **Konfigurowanie** z górnego menu hello.</span><span class="sxs-lookup"><span data-stu-id="202ea-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="202ea-159">Przewiń w dół toohello **ustawienia powiadomień baidu** i wprowadź klucz hello interfejsu API i klucz tajny uzyskany z konsoli Baidu hello wcześniej dla projektu wypychania w chmurze Baidu.</span><span class="sxs-lookup"><span data-stu-id="202ea-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="202ea-160">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="202ea-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="202ea-161">Kliknij przycisk hello **pulpitu nawigacyjnego** u góry hello hello Centrum powiadomień, a następnie kliknij pozycję **Wyświetl parametry połączenia**.</span><span class="sxs-lookup"><span data-stu-id="202ea-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="202ea-162">Zanotuj hello **DefaultListenSharedAccessSignature** i **DefaultFullSharedAccessSignature** z hello **dostęp do informacji o połączeniu** okna.</span><span class="sxs-lookup"><span data-stu-id="202ea-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="202ea-163">Łączenie aplikacji toohello Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="202ea-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="202ea-164">W środowisku Eclipse ADT utwórz nowy projekt dla systemu Android: **File** > **New** > **Android Application Project** (Plik — Nowy — Projekt aplikacji dla systemu Android).</span><span class="sxs-lookup"><span data-stu-id="202ea-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="202ea-165">Wprowadź **Nazwa aplikacji** i upewnij się, że hello **SDK wymagane Minimum** wersja jest ustawiana za**API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="202ea-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="202ea-166">Kliknij przycisk **dalej** i kontynuować hello kreatora po do hello **tworzenie działania** zostanie wyświetlone okno.</span><span class="sxs-lookup"><span data-stu-id="202ea-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="202ea-167">Upewnij się, że **puste działanie** jest wybrany, a następnie wybierz przycisk **Zakończ** toocreate nową aplikację systemu Android.</span><span class="sxs-lookup"><span data-stu-id="202ea-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="202ea-168">Upewnij się, że hello **docelowym kompilacji projektu** została poprawnie ustawiona.</span><span class="sxs-lookup"><span data-stu-id="202ea-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="202ea-169">Pobierz plik notification-hubs-0.4.jar hello z hello **pliki** kartę hello [Notification-Hubs-Android-SDK w serwisie Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="202ea-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="202ea-170">Dodaj hello pliku toohello **libs** folderu projektu Eclipse i Odśwież hello *biblioteki* folderu.</span><span class="sxs-lookup"><span data-stu-id="202ea-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="202ea-171">Pobierz i Rozpakuj hello [Baidu Push zestawu SDK systemu Android], otwórz hello **libs** folder, a następnie hello kopiowania **pushservice-x.y.z** jar plików i hello **armeabi**  &  **mips** folderów w hello **biblioteki** folderu aplikacji systemu Android.</span><span class="sxs-lookup"><span data-stu-id="202ea-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="202ea-172">Otwórz hello **AndroidManifest.xml** dla systemu android projektu i dodać hello uprawnienia, które są wymagane przez hello zestaw SDK usługi Baidu.</span><span class="sxs-lookup"><span data-stu-id="202ea-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="202ea-173">Dodaj hello **android: name** tooyour właściwości **aplikacji** element **AndroidManifest.xml**, zastępując *yourprojectname* (dla przykład **com.przyklad.baidutest**).</span><span class="sxs-lookup"><span data-stu-id="202ea-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="202ea-174">Upewnij się, że ta nazwa projektu jest zgodna hello jedną skonfigurowaną w konsoli Baidu hello.</span><span class="sxs-lookup"><span data-stu-id="202ea-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="202ea-175">Dodaj powitania po konfiguracji w elemencie aplikacji hello po hello **. MainActivity** elementu działania, zastępując *yourprojectname* (na przykład **com.przyklad.baidutest**):</span><span class="sxs-lookup"><span data-stu-id="202ea-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="202ea-176">Dodaj nową klasę o nazwie **ConfigurationSettings.java** toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="202ea-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="202ea-177">Dodaj powitania po tooit kodu:</span><span class="sxs-lookup"><span data-stu-id="202ea-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="202ea-178">Ustaw wartość hello **API_KEY** o co został z projektu w chmurze Baidu hello wcześniej pobrany, **NotificationHubName** z nazwą Centrum powiadomień z hello klasycznego portalu Azure i  **NotificationHubConnectionString** wartość defaultlistensharedaccesssignature z hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="202ea-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="202ea-179">Dodaj nową klasę o nazwie **DemoApplication.java**i Dodaj powitania po tooit kodu:</span><span class="sxs-lookup"><span data-stu-id="202ea-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="202ea-180">Dodaj nową klasę o nazwie **MyPushMessageReceiver.java**i Dodaj powitania po tooit kodu.</span><span class="sxs-lookup"><span data-stu-id="202ea-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="202ea-181">Jest klasą hello, który uchwytów hello powiadomienia wypychane, które są odbierane z serwera powiadomień wypychanych Baidu hello.</span><span class="sxs-lookup"><span data-stu-id="202ea-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="202ea-182">Otwórz **MainActivity.java**i dodaj następujące toohello hello **onCreate** metody:</span><span class="sxs-lookup"><span data-stu-id="202ea-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="202ea-183">Otwórz następujące instrukcje import u góry hello hello:</span><span class="sxs-lookup"><span data-stu-id="202ea-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="202ea-184">Wyślij powiadomienia tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="202ea-184">Send notifications tooyour app</span></span>
<span data-ttu-id="202ea-185">Możesz szybko przetestować odbieranie powiadomień w aplikacji, wysyłając powiadomienia w hello [portalu Azure](https://portal.azure.com/) przy użyciu hello **wysyłania** znajdującego się na powitania Centrum powiadomień, jak pokazano w po ekranie powitania:</span><span class="sxs-lookup"><span data-stu-id="202ea-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="202ea-186">Powiadomienia wypychane są zwykle wysyłane za pośrednictwem usługi zaplecza, takiej jak Mobile Services czy ASP.NET, z użyciem zgodnej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="202ea-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="202ea-187">Jeśli biblioteka nie jest dostępna dla Twojej zaplecza, można użyć interfejsu API REST hello bezpośrednio toosend komunikaty powiadomień.</span><span class="sxs-lookup"><span data-stu-id="202ea-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="202ea-188">W tym samouczku będziemy Zachowaj prostotę i przedstawiono testowanie aplikacji klienckiej przez wysyłanie powiadomień dotyczących usługi notification hubs w aplikacji konsoli usługi zaplecza przy użyciu hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="202ea-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="202ea-189">Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) samouczka jako hello następnego kroku do wysyłania powiadomień z zaplecza ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="202ea-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="202ea-190">Jednak po podejścia hello może służyć do wysyłania powiadomień:</span><span class="sxs-lookup"><span data-stu-id="202ea-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="202ea-191">**Interfejs REST**: powiadomienia mogą być obsługiwane na dowolnej platformie zaplecza za pomocą hello [interfejsu REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="202ea-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="202ea-192">**Microsoft Azure powiadomień koncentratory .NET SDK**: W hello Menedżera pakietów Nuget dla programu Visual Studio, uruchom [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="202ea-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="202ea-193">**Node.js**: [jak toouse centra powiadomień w oprogramowaniu Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="202ea-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="202ea-194">**Aplikacje mobilne**: na przykład jak toosend powiadomień z zaplecza Azure App Service Mobile Apps, który jest zintegrowany z usługą Notification Hubs, zobacz [aplikacji mobilnej tooyour powiadomień wypychanych Dodaj](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="202ea-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="202ea-195">**Java / PHP**: przykład sposobu toosend powiadomienia za pomocą hello interfejsów API REST, zobacz "jak toouse usługi Notification Hubs za pomocą języka Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="202ea-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="202ea-196">(Opcjonalnie) Wysyłanie powiadomień z poziomu aplikacji konsolowej .NET</span><span class="sxs-lookup"><span data-stu-id="202ea-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="202ea-197">W tej sekcji przedstawiono sposób wysyłania powiadomienia za pomocą aplikacji konsolowej .NET.</span><span class="sxs-lookup"><span data-stu-id="202ea-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="202ea-198">Utwórz nową aplikację konsoli języka Visual C#:</span><span class="sxs-lookup"><span data-stu-id="202ea-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="202ea-199">W oknie konsoli Menedżera pakietów hello, ustaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="202ea-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="202ea-200">Ta instrukcja dodaje toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="202ea-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="202ea-201">Witaj Otwórz plik **Program.cs** i dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="202ea-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="202ea-202">W Twojej `Program` klasy, Dodaj następujące metody hello i Zastąp *DefaultFullSharedAccessSignatureSASConnectionString* i *NotificationHubName* z wartościami hello.</span><span class="sxs-lookup"><span data-stu-id="202ea-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="202ea-203">Dodaj hello następujące wiersze w Twojej **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="202ea-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="202ea-204">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="202ea-204">Test your app</span></span>
<span data-ttu-id="202ea-205">tootest połączyć tę aplikację przy użyciu rzeczywistego telefonu, po prostu hello phone tooyour komputera za pomocą kabla USB.</span><span class="sxs-lookup"><span data-stu-id="202ea-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="202ea-206">Ta akcja spowoduje załadowanie aplikacji na telefon hello dołączony.</span><span class="sxs-lookup"><span data-stu-id="202ea-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="202ea-207">tootest tę aplikację w emulatorze hello na powitania Eclipse górnym pasku narzędzi, kliknij przycisk **Uruchom**, a następnie wybierz aplikację: uruchamia hello emulatora, obciążenia, i działa hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="202ea-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="202ea-208">Aplikacja Hello pobiera hello "userId" i "channelId" z hello usługi powiadomień wypychanych Baidu i rejestruje hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="202ea-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="202ea-209">toosend powiadomienie testowe, można użyć karty debugowania hello hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="202ea-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="202ea-210">Jeśli utworzono hello aplikacji konsoli .NET dla programu Visual Studio, wystarczy nacisnąć klawisz F5 hello w aplikacji hello toorun programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="202ea-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="202ea-211">Aplikacja Hello wysyła powiadomienie, które pojawia się w hello górnym obszarze powiadomień urządzenia lub emulatora.</span><span class="sxs-lookup"><span data-stu-id="202ea-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Zestaw SDK usługi Mobile Services dla systemu Android]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push zestawu SDK systemu Android]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[klasycznego portalu Azure]: https://manage.windowsazure.com/
[portalu Baidu]: http://www.baidu.com/
