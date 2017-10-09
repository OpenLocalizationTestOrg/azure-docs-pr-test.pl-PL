---
title: "aaaAccessing aplikacji z dowolnego urządzenia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie klientów są obsługiwane w przypadku usługi Azure RemoteApp i w jaki sposób tooaccess aplikacji."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 15985b40d870e3155d4132063bf5b9677ff9afed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="e2483-103">Uzyskiwanie dostępu do aplikacji w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e2483-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e2483-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="e2483-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e2483-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="e2483-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e2483-106">Jednym z beauties hello Azure RemoteApp jest, że mają dostęp do aplikacji z dowolnego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e2483-106">One of hello beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="e2483-107">Można nawet lepiej zaczął działać na jednym urządzeniu i bezproblemowe przejście drugiego urządzenia tooa i odebrania prawo pracę.</span><span class="sxs-lookup"><span data-stu-id="e2483-107">Even better, you can start working on one device and then seamlessly transition tooa second device and pick up right where you left off.</span></span> <span data-ttu-id="e2483-108">tooget uruchomiona zostanie muszą toodownload hello odpowiedniego klienta urządzenia i zaloguj się w usłudze toohello.</span><span class="sxs-lookup"><span data-stu-id="e2483-108">tooget started you need toodownload hello appropriate client for your device and sign in toohello service.</span></span>

<span data-ttu-id="e2483-109">W tym temacie firma Microsoft analizuje klientom Witaj obecnie obsługiwane i w jaki sposób toodownload je przed I przedstawia sposób toosign w tooRemoteApp z każdego powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="e2483-109">In this topic, we'll review hello clients currently supported and how toodownload them before I show you how toosign in tooRemoteApp from each of hello clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="e2483-110">Obsługiwani klienci</span><span class="sxs-lookup"><span data-stu-id="e2483-110">Supported clients</span></span>
<span data-ttu-id="e2483-111">Aby dostęp do usługi RemoteApp przy użyciu hello czynności, jeśli urządzenie działa jeden z następujących systemów operacyjnych:</span><span class="sxs-lookup"><span data-stu-id="e2483-111">You can access RemoteApp using hello steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="e2483-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="e2483-112">Windows 10</span></span> 
* <span data-ttu-id="e2483-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="e2483-113">Windows 8.1</span></span>
* <span data-ttu-id="e2483-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="e2483-114">Windows 8</span></span>
* <span data-ttu-id="e2483-115">Windows 7 z dodatkiem Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="e2483-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="e2483-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="e2483-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="e2483-117">iOS</span><span class="sxs-lookup"><span data-stu-id="e2483-117">iOS</span></span>
* <span data-ttu-id="e2483-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="e2483-118">Mac OS X</span></span>
* <span data-ttu-id="e2483-119">Android</span><span class="sxs-lookup"><span data-stu-id="e2483-119">Android</span></span>

 <span data-ttu-id="e2483-120">Co zubożonych klientów? obsługiwane są powitania po zubożonych klientów Windows Embedded:</span><span class="sxs-lookup"><span data-stu-id="e2483-120">What about thin clients? hello following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="e2483-121">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="e2483-121">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="e2483-122">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="e2483-122">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="e2483-123">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="e2483-123">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="e2483-124">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="e2483-124">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-hello-client"></a><span data-ttu-id="e2483-125">Pobieranie powitania klienta</span><span class="sxs-lookup"><span data-stu-id="e2483-125">Downloading hello client</span></span>
<span data-ttu-id="e2483-126">Niezależnie od tego, jakie platformy są używane, należy tooaccess RemoteApp można znaleźć na powitania klienta hello [pobierania klienta pulpitu zdalnego](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="e2483-126">No matter what platform you are using, hello client you need tooaccess RemoteApp can be found on hello [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="e2483-127">Kliknięcie przycisku hello różnych łączy albo bezpośrednio rozpocznie pobieranie powitania klienta lub wyśle strony pobierania klienta toohello w sklepie z aplikacjami powitania dla tej platformy.</span><span class="sxs-lookup"><span data-stu-id="e2483-127">Clicking hello different links will either directly start downloading hello client or will send you toohello client download page in hello app store for that platform.</span></span> <span data-ttu-id="e2483-128">Zainstaluj klienta na powitania, wykonując instrukcje hello na ekranie powitania.</span><span class="sxs-lookup"><span data-stu-id="e2483-128">Install hello client by following hello instructions on hello screen.</span></span>

<span data-ttu-id="e2483-129">Po zainstalowaniu powitania klienta na urządzeniu i uruchomić go, przejście toohello odpowiedniej sekcji poniżej toolearn jak toosign w tooRemoteApp z tego klienta.</span><span class="sxs-lookup"><span data-stu-id="e2483-129">Once you have installed hello client on your device and launched it, jump toohello corresponding section below toolearn how toosign in tooRemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="e2483-130">Android</span><span class="sxs-lookup"><span data-stu-id="e2483-130">Android</span></span>
<span data-ttu-id="e2483-131">Po zainstalowaniu aplikacji pulpitu zdalnego firmy Microsoft hello z hello sklepu Google Play, możesz go znaleźć na liście aplikacji w obszarze **pulpitu zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="e2483-131">Once you have installed hello Microsoft Remote Desktop app from hello Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="e2483-132">Uruchamiania aplikacji hello łączy tooan pusty Centrum połączeń, jeśli już korzystasz aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e2483-132">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="e2483-133">wprowadzenie do usługi Azure RemoteApp tooget, hello naciśnij przycisk Dodaj **"" +""** i wybierz **usługi Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="e2483-133">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Pusta Centrum połączeń](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="e2483-135">Należy toosign się przy użyciu usługi hello tooaccess adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="e2483-135">You need toosign in with your email address tooaccess hello service.</span></span> <span data-ttu-id="e2483-136">Wybierz **wprowadzenie**.</span><span class="sxs-lookup"><span data-stu-id="e2483-136">Tap **Get started**.</span></span>
   
    ![Zaloguj się w wierszu](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="e2483-138">Na następnej stronie powitania, wpisz w Twojej **adres e-mail** i wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e2483-138">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="e2483-139">To rozpoczyna hello procesu logowania przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2483-139">This begins hello sign-in process using Azure Active Directory.</span></span>
   
    ![Pierwsza strona usługi Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="e2483-141">Wykonaj instrukcje hello na powitania ekranu toosign się przy użyciu konta Microsoft (wcześniej nazywane "Identyfikator LiveID") lub identyfikator organizacji.</span><span class="sxs-lookup"><span data-stu-id="e2483-141">Follow hello instructions on hello screen toosign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="e2483-142">Po zalogowaniu może wyświetlone wszystkie zaproszenia hello otrzymanych stronę.</span><span class="sxs-lookup"><span data-stu-id="e2483-142">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="e2483-143">Jeśli jesteś, wybierz zaproszenia hello ufasz, a następnie naciśnij pozycję **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e2483-143">If you are, select hello invitations you trust and tap **Done**.</span></span>    
   
    ![Strona zaproszenia](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="e2483-145">Po zaakceptowaniu Twojego zaproszenia, hello listę aplikacji, masz urządzenie pobrany tooyour toowill dostępu i udostępniona w hello Centrum połączeń.</span><span class="sxs-lookup"><span data-stu-id="e2483-145">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="e2483-146">Wybierz jedną z toostart aplikacji hello przy jej użyciu.</span><span class="sxs-lookup"><span data-stu-id="e2483-146">Tap one of hello apps toostart using it.</span></span>
   
    ![Centrum połączeń z źródła danych](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="e2483-148">Jeśli nie masz jeszcze zaproszenia, nadal można wypróbować hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e2483-148">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="e2483-149">tak, naciśnij przycisk toodo **Przejdź wersji próbnej toofree** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="e2483-149">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Wersja demonstracyjna dla źródła danych w wierszu](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="e2483-151">Zapewni to dostęp do podstawowego zestawu tooa tooget aplikacji wprowadzenie do usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e2483-151">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Wersja demonstracyjna dla usługi Azure RemoteApp](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="e2483-153">iOS</span><span class="sxs-lookup"><span data-stu-id="e2483-153">iOS</span></span>
<span data-ttu-id="e2483-154">Po zainstalowaniu aplikacji pulpitu zdalnego firmy Microsoft hello hello ze sklepu z aplikacjami, możesz go znaleźć na liście aplikacji w obszarze **klienta usług pulpitu zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="e2483-154">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="e2483-155">Uruchamiania aplikacji hello łączy tooan pusty Centrum połączeń, jeśli już korzystasz aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e2483-155">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="e2483-156">tooget wprowadzenie do usługi Azure RemoteApp, hello naciśnij przycisk Dodaj **"" +""** i wybierz **dodać usługę Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="e2483-156">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Pusta Centrum połączeń](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="e2483-158">Należy toosign za pomocą wiadomości e-mail adres tooaccess hello usługi toostart tego procesu typu w Twojej **adres e-mail** i wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e2483-158">You need toosign in with your email address tooaccess hello service, toostart that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Zaloguj się w wierszu](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="e2483-160">Wykonaj instrukcje hello na toosign ekranie powitania się za pomocą konta Microsoft (identyfikator Live ID) lub nazwę organizacji.</span><span class="sxs-lookup"><span data-stu-id="e2483-160">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="e2483-161">Po zalogowaniu może wyświetlone wszystkie zaproszenia hello otrzymanych stronę.</span><span class="sxs-lookup"><span data-stu-id="e2483-161">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="e2483-162">Jeśli jesteś, wybierz zaproszenia hello ufasz, a następnie naciśnij pozycję **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e2483-162">If you are, select hello invitations you trust and tap **Done**.</span></span>
   
    ![Strona zaproszenia](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="e2483-164">Po zaakceptowaniu Twojego zaproszenia, hello listę aplikacji, masz urządzenie pobrany tooyour toowill dostępu i udostępniona w hello Centrum połączeń.</span><span class="sxs-lookup"><span data-stu-id="e2483-164">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="e2483-165">Wybierz jedną z toolaunch aplikacji hello, go i rozpoczęcia korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="e2483-165">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centrum połączeń z źródła danych](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="e2483-167">Jeśli nie masz jeszcze zaproszenia, nadal można wypróbować hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e2483-167">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="e2483-168">tak, naciśnij przycisk toodo **Przejdź wersji próbnej toofree** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="e2483-168">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Wersja demonstracyjna dla źródła danych w wierszu](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="e2483-170">Zapewni to dostęp do podstawowego zestawu tooa tooget aplikacji wprowadzenie do usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e2483-170">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Wersja demonstracyjna dla usługi Azure RemoteApp](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="e2483-172">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="e2483-172">Mac OS X</span></span>
<span data-ttu-id="e2483-173">Po zainstalowaniu aplikacji pulpitu zdalnego firmy Microsoft hello hello ze sklepu z aplikacjami, możesz go znaleźć na liście aplikacji w obszarze **pulpitu zdalnego firmy Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="e2483-173">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="e2483-174">Uruchamiania aplikacji hello łączy tooan pusty Centrum połączeń, jeśli już korzystasz aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e2483-174">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="e2483-175">tooget wprowadzenie do usługi Azure RemoteApp, kliknij przycisk hello **usługi Azure RemoteApp** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e2483-175">tooget started with Azure RemoteApp, click hello **Azure RemoteApp** button.</span></span>
   
    ![Pusta Centrum połączeń](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="e2483-177">Należy toosign za pomocą wiadomości e-mail adres tooaccess hello usługi toostart przetwarzające, naciśnij przycisk **wprowadzenie**.</span><span class="sxs-lookup"><span data-stu-id="e2483-177">You need toosign in with your email address tooaccess hello service, toostart that process, tap **Get Started**.</span></span>
   
    ![Zaloguj się w wierszu](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="e2483-179">Na następnej stronie powitania, wpisz w Twojej **adres e-mail** i wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e2483-179">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="e2483-180">To rozpoczyna hello logowania procesu przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2483-180">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Pierwsza strona usługi Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="e2483-182">Wykonaj instrukcje hello na toosign ekranie powitania się za pomocą konta Microsoft (identyfikator Live ID) lub nazwę organizacji.</span><span class="sxs-lookup"><span data-stu-id="e2483-182">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="e2483-183">Po zalogowaniu może wyświetlone wszystkie zaproszenia hello otrzymanych stronę.</span><span class="sxs-lookup"><span data-stu-id="e2483-183">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="e2483-184">Jeśli jesteś, wybierz zaproszenia hello zaufania i zamknąć okno dialogowe hello.</span><span class="sxs-lookup"><span data-stu-id="e2483-184">If you are, select hello invitations you trust and close hello dialog.</span></span>
   
    ![Strona zaproszenia](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="e2483-186">Po zaakceptowaniu Twojego zaproszenia, hello listę aplikacji, masz urządzenie pobrany tooyour toowill dostępu i udostępniona w hello Centrum połączeń.</span><span class="sxs-lookup"><span data-stu-id="e2483-186">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="e2483-187">Kliknij dwukrotnie jeden toolaunch aplikacji hello go i rozpoczęcia korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="e2483-187">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centrum połączeń z źródła danych](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="e2483-189">Jeśli nie masz jeszcze zaproszenia, nadal można wypróbować hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e2483-189">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="e2483-190">tak, kliknij przycisk toodo **Przejdź wersji próbnej toofree** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="e2483-190">toodo so, click **Go toofree trial** when prompted.</span></span>
   
    ![Wersja demonstracyjna dla źródła danych w wierszu](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="e2483-192">Zapewni to dostęp do podstawowego zestawu tooa tooget aplikacji wprowadzenie do usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e2483-192">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Wersja demonstracyjna dla usługi Azure RemoteApp](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="e2483-194">Systemu Windows (wszystkie obsługiwane wersje z wyjątkiem Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="e2483-194">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="e2483-195">Witaj klienta jest uruchamiane automatycznie po zakończeniu instalacji należy jednak gdy będziesz potrzebować tooaccess go ponownie później można je znaleźć na liście aplikacji w obszarze nazwy hello **usługi Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="e2483-195">hello client launches automatically after it finishes installing, however when you need tooaccess it again later it can be found in your app list under hello name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="e2483-196">Ater uruchamianie powitania klienta, hello pierwszej strony, którą możesz zobaczyć zaprasza tooAzure programów RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e2483-196">Ater launching hello client, hello first page you see welcomes you tooAzure RemoteApp.</span></span> <span data-ttu-id="e2483-197">tooproceed, kliknij przycisk **wprowadzenie**.</span><span class="sxs-lookup"><span data-stu-id="e2483-197">tooproceed, click on **Get Started**.</span></span>
   
    ![Strona powitalna powitania klienta usługi Azure RemoteApp](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="e2483-199">Witaj następnej strony rozpoczyna się znak hello w procesie usługi Azure RemoteApp przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2483-199">hello next page starts hello sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="e2483-200">Ten proces powinna wyglądać znajomo, jeśli używasz usług firmy Microsoft w przeszłości hello.</span><span class="sxs-lookup"><span data-stu-id="e2483-200">This process should look familiar if you have used Microsoft services in hello past.</span></span> <span data-ttu-id="e2483-201">Uruchom, wpisując Twojej **adres e-mail** i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e2483-201">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Pierwszy monit usługi Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="e2483-203">Wykonaj instrukcje hello na toosign ekranie powitania się za pomocą konta Microsoft (identyfikator Live ID) lub nazwę organizacji.</span><span class="sxs-lookup"><span data-stu-id="e2483-203">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="e2483-204">Po zalogowaniu może wyświetlone wszystkie zaproszenia hello otrzymanych stronę.</span><span class="sxs-lookup"><span data-stu-id="e2483-204">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="e2483-205">Jeśli jesteś, wybierz zaproszenia hello zaufania i kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="e2483-205">If you are, select hello invitations you trust and click **Done**.</span></span>
   
    ![Strona zaproszenia powitania klienta usługi Azure RemoteApp](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="e2483-207">Po zaakceptowaniu Twojego zaproszenia, hello listę aplikacji, masz urządzenie pobrany tooyour toowill dostępu i udostępniona w hello Centrum połączeń.</span><span class="sxs-lookup"><span data-stu-id="e2483-207">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="e2483-208">Kliknij dwukrotnie jeden toolaunch aplikacji hello go i rozpoczęcia korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="e2483-208">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centrum połączeń powitania klienta usługi Azure RemoteApp](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="e2483-210">Jeśli nikt nie przesłał możesz jeszcze zaproszenia, nie martw się będzie mamy!</span><span class="sxs-lookup"><span data-stu-id="e2483-210">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="e2483-211">Nadal będziesz mieć dostępu tooa pokaz kolekcji, aby można było sprawdzić limit hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e2483-211">You'll still have access tooa demo collection so you can test out hello service.</span></span>
   
    ![Wersja demonstracyjna dla usługi Azure RemoteApp](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="e2483-213">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="e2483-213">Windows Phone 8.1</span></span>
<span data-ttu-id="e2483-214">Po zainstalowaniu aplikacji pulpitu zdalnego firmy Microsoft hello ze Sklepu Windows Phone 8.1 hello, możesz go znaleźć na liście aplikacji w obszarze **pulpitu zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="e2483-214">Once you have installed hello Microsoft Remote Desktop app from hello Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="e2483-215">Uruchamiania aplikacji hello łączy możesz bezpośrednio tooan pusty Centrum połączeń, jeśli już korzystasz aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e2483-215">Launching hello app brings you directly tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="e2483-216">wprowadzenie do usługi Azure RemoteApp tooget, hello naciśnij przycisk Dodaj **"" +""** u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="e2483-216">tooget started with Azure RemoteApp, tap hello add button **""+""** at hello bottom of hello screen.</span></span>
   
    ![Pusta Centrum połączeń](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="e2483-218">Następnie wybierz **usługi Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="e2483-218">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Dodaj stronę elementu](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="e2483-220">Należy toosign za pomocą wiadomości e-mail adres tooaccess hello usługi toostart przetwarzające, naciśnij przycisk **połączyć**.</span><span class="sxs-lookup"><span data-stu-id="e2483-220">You need toosign in with your email address tooaccess hello service, toostart that process, tap **connect**.</span></span>
   
    ![Zaloguj się w wierszu](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="e2483-222">Na następnej stronie powitania, wpisz w Twojej **adres e-mail** i wybierz **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="e2483-222">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="e2483-223">To rozpoczyna hello logowania procesu przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2483-223">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Pierwsza strona usługi Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="e2483-225">Wykonaj instrukcje hello na toosign ekranie powitania się za pomocą konta Microsoft (identyfikator Live ID) lub nazwę organizacji.</span><span class="sxs-lookup"><span data-stu-id="e2483-225">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="e2483-226">Po zalogowaniu może wyświetlone wszystkie zaproszenia hello otrzymanych stronę.</span><span class="sxs-lookup"><span data-stu-id="e2483-226">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="e2483-227">Jeśli jesteś, wybierz zaproszenia hello ufasz, a następnie naciśnij pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e2483-227">If you are, select hello invitations you trust and tap **save**.</span></span>
   
    ![Strona zaproszenia](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="e2483-229">Po zaakceptowaniu Twojego zaproszenia, hello listę aplikacji, masz urządzenie pobrany tooyour toowill dostępu i udostępniona w hello Centrum połączeń.</span><span class="sxs-lookup"><span data-stu-id="e2483-229">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="e2483-230">Wybierz jedną z toolaunch aplikacji hello, go i rozpoczęcia korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="e2483-230">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centrum połączeń z źródła danych](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="e2483-232">Jeśli nie masz jeszcze zaproszenia, nadal można wypróbować hello usługi.</span><span class="sxs-lookup"><span data-stu-id="e2483-232">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="e2483-233">tak, naciśnij przycisk toodo **tak** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="e2483-233">toodo so, tap **yes** when prompted.</span></span>
   
    ![Wersja demonstracyjna dla źródła danych w wierszu](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="e2483-235">Zapewni to dostęp do podstawowego zestawu tooa tooget aplikacji wprowadzenie do usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e2483-235">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Wersja demonstracyjna dla usługi Azure RemoteApp](./media/remoteapp-clients/WinPhone8.png)

