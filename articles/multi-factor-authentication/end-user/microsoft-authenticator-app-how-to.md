---
title: "aaaMicrosoft Authenticator dla telefonów komórkowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupgrade toohello najnowszej wersji Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a><span data-ttu-id="42cb0-103">Wprowadzenie do aplikacji Microsoft Authenticator hello</span><span class="sxs-lookup"><span data-stu-id="42cb0-103">Get started with hello Microsoft Authenticator app</span></span>
<span data-ttu-id="42cb0-104">Witaj aplikacji Authenticator firmy Microsoft zapewnia dodatkowy poziom zabezpieczeń w ramach Twojego konta służbowego (na przykład bsimon@contoso.com) lub konta Microsoft (na przykład bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="42cb0-104">hello Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="42cb0-105">Aplikacja Hello działa w jednym z dwóch sposobów:</span><span class="sxs-lookup"><span data-stu-id="42cb0-105">hello app works in one of two ways:</span></span>

* <span data-ttu-id="42cb0-106">**Powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-106">**Notification**.</span></span> <span data-ttu-id="42cb0-107">Aplikacja Hello pomaga zapobiec tooaccounts nieautoryzowanym dostępem i Zatrzymaj fałszywe transakcje przez wypychanie powiadomień tooyour smartfonie lub tablecie.</span><span class="sxs-lookup"><span data-stu-id="42cb0-107">hello app can help prevent unauthorized access tooaccounts and stop fraudulent transactions by pushing a notification tooyour smartphone or tablet.</span></span> <span data-ttu-id="42cb0-108">Wystarczy wyświetlić powiadomienie hello, a jeśli jest to uzasadnione, wybierz **Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-108">Simply view hello notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="42cb0-109">W przeciwnym razie można wybrać **Odmów**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="42cb0-110">**Kod weryfikacyjny**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-110">**Verification code**.</span></span> <span data-ttu-id="42cb0-111">Aplikacja Hello może służyć jako oprogramowania token toogenerate kod weryfikacyjny OAuth.</span><span class="sxs-lookup"><span data-stu-id="42cb0-111">hello app can be used as a software token toogenerate an OAuth verification code.</span></span> <span data-ttu-id="42cb0-112">Po wprowadzeniu nazwy użytkownika i hasła, należy wprowadzić kod hello podał aplikacji hello na powitania ekranu logowania.</span><span class="sxs-lookup"><span data-stu-id="42cb0-112">After you enter your username and password, you enter hello code provided by hello app into hello sign-in screen.</span></span> <span data-ttu-id="42cb0-113">kod weryfikacyjny Hello zapewnia drugiej formy uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="42cb0-113">hello verification code provides a second form of authentication.</span></span>

<span data-ttu-id="42cb0-114">Aplikacja Microsoft Authenticator Hello zastępuje hello aplikacji Azure Authenticator.</span><span class="sxs-lookup"><span data-stu-id="42cb0-114">hello Microsoft Authenticator app replaces hello Azure Authenticator app.</span></span> <span data-ttu-id="42cb0-115">Aplikacja Azure Authenticator Hello wciąż działać, ale jeśli zdecydujesz się nową aplikację Microsoft Authenticator toomove toohello, w tym artykule mogą pomóc.</span><span class="sxs-lookup"><span data-stu-id="42cb0-115">hello Azure Authenticator app still works, but if you decide toomove toohello new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="42cb0-116">Zgódź się na potrzeby weryfikacji dwuetapowej</span><span class="sxs-lookup"><span data-stu-id="42cb0-116">Opt in for two-step verification</span></span>

<span data-ttu-id="42cb0-117">Aplikacja Microsoft Authenticator Hello nie działa przez samego siebie.</span><span class="sxs-lookup"><span data-stu-id="42cb0-117">hello Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="42cb0-118">Skonfiguruj każdy z tooprompt kont dla drugiego metodę weryfikacji po zalogowaniu się nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="42cb0-118">Configure each of your accounts tooprompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="42cb0-119">Dla konta służbowego nie zwykle otrzymasz toochoose tej funkcji dla siebie.</span><span class="sxs-lookup"><span data-stu-id="42cb0-119">For a work or school account, you don't usually get toochoose this feature for yourself.</span></span> <span data-ttu-id="42cb0-120">Zamiast tego administrator zabezpieczeń zdecyduje się w Twoim imieniu i następnie powiadamia tooregister metody weryfikacji dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="42cb0-120">Instead, a security administrator opts in on your behalf and then notifies you tooregister verification methods for your account.</span></span> <span data-ttu-id="42cb0-121">Jeśli ten scenariusz dotyczy tooyou, zapoznaj się z [co oznacza Azure Multi-Factor Authentication dla mnie](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="42cb0-121">If this scenario applies tooyou, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="42cb0-122">Dla konta osobistego należy tooset się weryfikacji dwuetapowej dla siebie.</span><span class="sxs-lookup"><span data-stu-id="42cb0-122">For a personal account, you need tooset up two-step verification for yourself.</span></span> <span data-ttu-id="42cb0-123">Jeśli masz konto Microsoft, te kroki są dostępne w [o weryfikacji dwuetapowej](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="42cb0-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="42cb0-124">Można również używać hello Authenticator firmy Microsoft z kont innych niż Microsoft.</span><span class="sxs-lookup"><span data-stu-id="42cb0-124">You can also use hello Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="42cb0-125">Funkcja hello one wywołać inną niż weryfikację dwuetapową, ale powinien być toofind mogli go w obszarze Ustawienia zabezpieczeń lub logowania.</span><span class="sxs-lookup"><span data-stu-id="42cb0-125">They may call hello feature something other than two-step verification, but you should be able toofind it under security or sign-in settings.</span></span> 

## <a name="install-hello-app"></a><span data-ttu-id="42cb0-126">Instalowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="42cb0-126">Install hello app</span></span>
<span data-ttu-id="42cb0-127">Aplikacja Microsoft Authenticator Hello jest dostępna dla [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), i [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="42cb0-127">hello Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-toohello-app"></a><span data-ttu-id="42cb0-128">Dodaj aplikację toohello kont</span><span class="sxs-lookup"><span data-stu-id="42cb0-128">Add accounts toohello app</span></span>
<span data-ttu-id="42cb0-129">Dla każdego konta, które mają aplikacji Microsoft Authenticator toohello tooadd użyj jednej z hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="42cb0-129">For each account that you want tooadd toohello Microsoft Authenticator app, use one of hello following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-toohello-app"></a><span data-ttu-id="42cb0-130">Dodaj aplikację toohello osobistego konta Microsoft</span><span class="sxs-lookup"><span data-stu-id="42cb0-130">Add a personal Microsoft account toohello app</span></span>

<span data-ttu-id="42cb0-131">Do osobistego konta Microsoft (jeden użycie toosign w tooOutlook.com, Xbox, Skype, itp.), wszystkie mają toodo jest, zaloguj się na koncie tooyour w aplikacji Microsoft Authenticator hello.</span><span class="sxs-lookup"><span data-stu-id="42cb0-131">For a personal Microsoft account (one that you use toosign in tooOutlook.com, Xbox, Skype, etc.), all you have toodo is sign in tooyour account in hello Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a><span data-ttu-id="42cb0-132">Dodaj służbowego lub szkolnego konta toohello aplikacji przy użyciu skaner kodów QR hello</span><span class="sxs-lookup"><span data-stu-id="42cb0-132">Add a work or school account toohello app using hello QR code scanner</span></span>
1. <span data-ttu-id="42cb0-133">Przejdź na ekran ustawień weryfikacji zabezpieczeń toohello.</span><span class="sxs-lookup"><span data-stu-id="42cb0-133">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="42cb0-134">Aby uzyskać informacje na temat tooget toothis ekranu, zobacz [zmiana ustawień zabezpieczeń](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="42cb0-134">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="42cb0-135">Witaj pole wyboru obok zbyt**aplikacji uwierzytelniania** następnie wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-135">Check hello box next too**Authenticator app** then select **Configure**.</span></span>

    ![przycisk Konfiguruj Hello na ekranie Ustawienia weryfikacji zabezpieczeń hello](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="42cb0-137">Spowoduje to wyświetlenie ekranu kod QR.</span><span class="sxs-lookup"><span data-stu-id="42cb0-137">This brings up a screen with a QR code on it.</span></span>

    ![Ekran, który zawiera kod QR hello](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="42cb0-139">Otwórz hello aplikacji Authenticator firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="42cb0-139">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="42cb0-140">Na powitania **kont** ekranu wybierz  **+** , a następnie określ, które mają tooadd konta firmowego lub szkolnego.</span><span class="sxs-lookup"><span data-stu-id="42cb0-140">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>
4. <span data-ttu-id="42cb0-141">Użyj hello aparatu tooscan hello QR kodu, a następnie wybierz **gotowe** tooclose hello QR kodu ekranu.</span><span class="sxs-lookup"><span data-stu-id="42cb0-141">Use hello camera tooscan hello QR code, and then select **Done** tooclose hello QR code screen.</span></span>

    <span data-ttu-id="42cb0-142">Jeśli aparatu nie działa prawidłowo, możesz [ręcznie wprowadzić kod hello QR i adres URL](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="42cb0-142">If your camera is not working properly, you can [enter hello QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="42cb0-143">Gdy aplikacja hello zawiera nazwę konta z sześciocyfrowy kod podrzędne, wszystko będzie gotowe.</span><span class="sxs-lookup"><span data-stu-id="42cb0-143">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Ekran kont](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a><span data-ttu-id="42cb0-145">Ręcznie dodaj aplikację toohello konta</span><span class="sxs-lookup"><span data-stu-id="42cb0-145">Add an account toohello app manually</span></span>
1. <span data-ttu-id="42cb0-146">Przejdź na ekran ustawień weryfikacji zabezpieczeń toohello.</span><span class="sxs-lookup"><span data-stu-id="42cb0-146">Go toohello security verification settings screen.</span></span>  <span data-ttu-id="42cb0-147">Aby uzyskać informacje na temat tooget toothis ekranu, zobacz [zmiana ustawień zabezpieczeń](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="42cb0-147">For information on how tooget toothis screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="42cb0-148">Wybierz **skonfigurować**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-148">Select **Configure**.</span></span>

    ![przycisk Konfiguruj Hello na ekranie Ustawienia weryfikacji zabezpieczeń hello](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="42cb0-150">Spowoduje to wyświetlenie ekranu kod QR.</span><span class="sxs-lookup"><span data-stu-id="42cb0-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="42cb0-151">Uwaga hello kod i adres URL.</span><span class="sxs-lookup"><span data-stu-id="42cb0-151">Note hello code and URL.</span></span>

    ![Ekran, który zawiera kod hello QR i adres URL](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="42cb0-153">Otwórz hello aplikacji Authenticator firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="42cb0-153">Open hello Microsoft Authenticator app.</span></span> <span data-ttu-id="42cb0-154">Na powitania **kont** ekranu wybierz  **+** , a następnie określ, które mają tooadd konta firmowego lub szkolnego.</span><span class="sxs-lookup"><span data-stu-id="42cb0-154">On hello **accounts** screen, select **+**, and then specify that you want tooadd a work or school account.</span></span>

4. <span data-ttu-id="42cb0-155">Skaner hello wybierz **ręcznie wprowadzić kod**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-155">In hello scanner, select **enter code manually**.</span></span>

    ![Ekran skanowania kod QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="42cb0-157">Wprowadź w odpowiednich polach hello w aplikacji hello hello kod i adres URL hello, a następnie wybierz **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-157">Enter hello code and hello URL in hello appropriate boxes in hello app, then select **Finish**.</span></span>

    ![Ekran wprowadzić kod i adres URL](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="42cb0-159">Gdy aplikacja hello zawiera nazwę konta z sześciocyfrowy kod podrzędne, wszystko będzie gotowe.</span><span class="sxs-lookup"><span data-stu-id="42cb0-159">When hello app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Ekran kont](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a><span data-ttu-id="42cb0-161">Dodaj aplikację toohello konta przy użyciu funkcji Touch ID</span><span class="sxs-lookup"><span data-stu-id="42cb0-161">Add an account toohello app using Touch ID</span></span>
<span data-ttu-id="42cb0-162">Aplikacja Microsoft Authenticator Hello w systemie iOS obsługuje użycia funkcji Touch ID.</span><span class="sxs-lookup"><span data-stu-id="42cb0-162">hello Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="42cb0-163">Usługa Azure Multi-Factor Authentication umożliwia organizacjom toorequire numeru PIN dla urządzeń.</span><span class="sxs-lookup"><span data-stu-id="42cb0-163">Azure Multi-Factor Authentication allows organizations toorequire a PIN for devices.</span></span> <span data-ttu-id="42cb0-164">Touch ID użytkownicy systemu iOS nie wymagają tooenter numeru PIN.</span><span class="sxs-lookup"><span data-stu-id="42cb0-164">With Touch ID, iOS users don’t need tooenter a PIN.</span></span> <span data-ttu-id="42cb0-165">Zamiast tego można skanować ich odcisk palca i wybierz **Zatwierdź**.</span><span class="sxs-lookup"><span data-stu-id="42cb0-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="42cb0-166">Konfigurowanie funkcji Touch ID z Authenticator firmy Microsoft jest proste.</span><span class="sxs-lookup"><span data-stu-id="42cb0-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="42cb0-167">Można wykonać żądanie normalne weryfikacji przy użyciu numeru PIN.</span><span class="sxs-lookup"><span data-stu-id="42cb0-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="42cb0-168">Jeśli urządzenie obsługuje funkcję Touch ID, Microsoft Authenticator konfiguruje ją automatycznie dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="42cb0-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Weryfikacja instalacji funkcji Touch ID](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="42cb0-170">Od tego punktu do przodu, gdy użytkownik jest wymagane tooverify logowanie, wybierz hello otrzymał powiadomienie wypychane i skanowania odcisku palca zamiast wprowadzania numeru PIN.</span><span class="sxs-lookup"><span data-stu-id="42cb0-170">From that point forward, when you're required tooverify your sign-in, you select hello received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Powiadomienia wypychane](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a><span data-ttu-id="42cb0-172">Po zalogowaniu się przy użyciu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="42cb0-172">Use hello app when you sign in</span></span>

<span data-ttu-id="42cb0-173">Po dodaniu konta toohello aplikacji może być zostanie wyświetlony monit o toodo testu toomake weryfikacji, czy wszystko zostało poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="42cb0-173">Once your account is added toohello app, you may be prompted toodo a test verification toomake sure everything was configured correctly.</span></span> <span data-ttu-id="42cb0-174">Po wykonaniu tej gotowe!</span><span class="sxs-lookup"><span data-stu-id="42cb0-174">After that, you're done!</span></span> <span data-ttu-id="42cb0-175">Nie trzeba toodo inaczej dopóki hello następnym logowaniu.</span><span class="sxs-lookup"><span data-stu-id="42cb0-175">You don't need toodo anything else until hello next time you sign in.</span></span>

<span data-ttu-id="42cb0-176">Jeśli została wybrana opcja toouse kodów weryfikacji w aplikacji hello, uruchom toosee ich na powitania strony głównej.</span><span class="sxs-lookup"><span data-stu-id="42cb0-176">If you chose toouse verification codes in hello app, you start toosee them on hello home page.</span></span> <span data-ttu-id="42cb0-177">Ich zmiana co 30 sekund, aby zawsze mieć nowy kod gdy będziesz potrzebować.</span><span class="sxs-lookup"><span data-stu-id="42cb0-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="42cb0-178">Ale nie ma potrzeby toodo niczego z nimi dopóki Zaloguj się i są tooenter zostanie wyświetlony monit o kod weryfikacyjny.</span><span class="sxs-lookup"><span data-stu-id="42cb0-178">But you don't need toodo anything with them until you sign in and are prompted tooenter a verification code.</span></span>  
