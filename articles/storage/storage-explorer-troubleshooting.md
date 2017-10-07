---
title: "Przewodnik rozwiązywania problemów aaaAzure Eksploratora usługi Storage | Dokumentacja firmy Microsoft"
description: "Omówienie funkcji debugowania Witaj dwie platformy Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="2ae18-103">Podręczniku rozwiązywania problemów z Eksploratora usługi Storage platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2ae18-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="2ae18-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="2ae18-104">Introduction</span></span>

<span data-ttu-id="2ae18-105">Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza) jest autonomiczną aplikację, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemie Windows, system macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="2ae18-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="2ae18-106">Aplikacja Hello można połączyć kont toStorage hostowanych na Azure, suwerenne chmur i stosu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ae18-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="2ae18-107">Ten przewodnik zawiera podsumowanie rozwiązania dla typowe problemy występujące w Eksploratorze usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="2ae18-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="2ae18-108">Problemy z rejestracją</span><span class="sxs-lookup"><span data-stu-id="2ae18-108">Sign in issues</span></span>

<span data-ttu-id="2ae18-109">Obsługiwane są tylko konta usługi Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="2ae18-109">Only Azure Active Directory (AAD) accounts are supported.</span></span> <span data-ttu-id="2ae18-110">Jeśli używasz konta usług AD FS, można oczekiwać podpisywania tooStorage Explorer nie będzie działać.</span><span class="sxs-lookup"><span data-stu-id="2ae18-110">If you use an ADFS account, it’s expected that signing in tooStorage Explorer would not work.</span></span> <span data-ttu-id="2ae18-111">Przed kontynuowaniem, spróbuj ponownie uruchomić aplikację i zobacz, czy hello problemy mogą zostać usunięte.</span><span class="sxs-lookup"><span data-stu-id="2ae18-111">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="2ae18-112">Błąd: Certyfikat z podpisem własnym w łańcuchu certyfikatów</span><span class="sxs-lookup"><span data-stu-id="2ae18-112">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="2ae18-113">Istnieje kilka przyczyn, dlaczego błąd może się pojawić i hello dwie najbardziej typowe przyczyny są następujące:</span><span class="sxs-lookup"><span data-stu-id="2ae18-113">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="2ae18-114">Aplikacja Hello jest połączony za pośrednictwem "przezroczystego obiektu pośredniczącego", co oznacza przechwycenia ruchu HTTPS, odszyfrowywania go i następnie szyfrowania za pomocą certyfikatu z podpisem własnym serwera (takich jak serwer firmy).</span><span class="sxs-lookup"><span data-stu-id="2ae18-114">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="2ae18-115">Używasz aplikacji, takich jak oprogramowanie antywirusowe, które wprowadza certyfikatu SSL z podpisem własnym do wiadomości powitania HTTPS, które otrzymujesz.</span><span class="sxs-lookup"><span data-stu-id="2ae18-115">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="2ae18-116">Gdy Eksploratora usługi Storage napotka jeden z problemów hello, go już wiadomo, czy została naruszona hello odebrał komunikat protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2ae18-116">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="2ae18-117">Jeśli masz kopię certyfikatu z podpisem własnym hello, możesz pozwolić, Eksploratora usługi Storage zaufania temu certyfikatowi.</span><span class="sxs-lookup"><span data-stu-id="2ae18-117">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="2ae18-118">Jeśli nie wiesz, kto jest wprowadzenia hello certyfikatu, wykonaj te kroki toofind go:</span><span class="sxs-lookup"><span data-stu-id="2ae18-118">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="2ae18-119">Zainstaluj Otwórz protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="2ae18-119">Install Open SSL</span></span>

    - <span data-ttu-id="2ae18-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (hello wersje światła powinno wystarczyć)</span><span class="sxs-lookup"><span data-stu-id="2ae18-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="2ae18-121">Mac i Linux: powinien być dołączony do systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="2ae18-121">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="2ae18-122">Uruchom Otwórz protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="2ae18-122">Run Open SSL</span></span>

    - <span data-ttu-id="2ae18-123">System Windows: Otwórz katalog instalacyjny hello, kliknij pozycję **/bin/**, a następnie kliknij dwukrotnie **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="2ae18-123">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="2ae18-124">Mac i Linux: Uruchom **openssl** z terminalu.</span><span class="sxs-lookup"><span data-stu-id="2ae18-124">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="2ae18-125">Wykonanie s_client - showcerts-Połącz microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="2ae18-125">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="2ae18-126">Poszukaj certyfikaty z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="2ae18-126">Look for self-signed certificates.</span></span> <span data-ttu-id="2ae18-127">Jeśli nie wiesz, które są podpisem, poszukaj dowolnym hello podmiotu ("s:") i wystawcy ("i") są takie same hello.</span><span class="sxs-lookup"><span data-stu-id="2ae18-127">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="2ae18-128">Znalezione wszystkie certyfikaty z podpisem własnym dla każdego z nich, skopiować i wkleić wszystkie elementy z tym **---BEGIN CERTIFICATE---** za**---END CERTIFICATE---** tooa nowy plik cer.</span><span class="sxs-lookup"><span data-stu-id="2ae18-128">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="2ae18-129">Otwórz Eksploratora usługi Storage, kliknij pozycję **Edytuj** > **certyfikaty SSL** > **importu certyfikatów**, a następnie użyj hello pliku selektora toofind, wybierz, i otwierać pliki .cer hello, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="2ae18-129">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="2ae18-130">Jeśli nie można znaleźć żadnych certyfikatów z podpisem własnym za pomocą hello powyżej czynności, skontaktuj się z nami za pomocą narzędzia opinii hello, aby uzyskać dalszą pomoc.</span><span class="sxs-lookup"><span data-stu-id="2ae18-130">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="2ae18-131">Nie można tooretrieve subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2ae18-131">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="2ae18-132">Jeśli tooretrieve subskrypcji po pomyślnym zalogowaniu w, wykonaj te kroki tootroubleshoot ten problem:</span><span class="sxs-lookup"><span data-stu-id="2ae18-132">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="2ae18-133">Sprawdź, czy Twoje konto ma subskrypcje toohello dostęp po zalogowaniu się do hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ae18-133">Verify that your account has access toohello subscriptions by signing into hello Azure portal.</span></span>

- <span data-ttu-id="2ae18-134">Upewnij się, że zalogowano się za pomocą hello poprawne środowisko (Azure, chińskiej wersji platformy Azure, platformy Azure w Niemczech, Azure instytucji rządowych Stanów Zjednoczonych lub niestandardowe stosu środowiska/Azure).</span><span class="sxs-lookup"><span data-stu-id="2ae18-134">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="2ae18-135">Jeśli używasz serwera proxy, upewnij się, poprawnie skonfigurowany serwer proxy Eksploratora usługi Storage hello.</span><span class="sxs-lookup"><span data-stu-id="2ae18-135">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="2ae18-136">Spróbuj usunąć i ponowne dodawanie hello konta.</span><span class="sxs-lookup"><span data-stu-id="2ae18-136">Try removing and readding hello account.</span></span>

- <span data-ttu-id="2ae18-137">Spróbuj usuwanie hello następujące pliki z katalogu głównego (czyli C:\Users\ContosoUser), a następnie ponowne dodanie konta hello:</span><span class="sxs-lookup"><span data-stu-id="2ae18-137">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="2ae18-138">.adalcache</span><span class="sxs-lookup"><span data-stu-id="2ae18-138">.adalcache</span></span>

    - <span data-ttu-id="2ae18-139">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="2ae18-139">.devaccounts</span></span>

    - <span data-ttu-id="2ae18-140">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="2ae18-140">.extaccounts</span></span>

- <span data-ttu-id="2ae18-141">Obejrzyj hello developer narzędzia konsoli (naciskając klawisz F12) Jeśli logujesz dla komunikatów o błędach:</span><span class="sxs-lookup"><span data-stu-id="2ae18-141">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![Narzędzia dla deweloperów](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="2ae18-143">Strona uwierzytelniania hello toosee</span><span class="sxs-lookup"><span data-stu-id="2ae18-143">Unable toosee hello authentication page</span></span>

<span data-ttu-id="2ae18-144">Jeśli strony uwierzytelniania hello toosee, wykonaj te kroki tootroubleshoot ten problem:</span><span class="sxs-lookup"><span data-stu-id="2ae18-144">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="2ae18-145">W zależności od prędkości połączenia hello może potrwać hello tooload strony logowania, zaczekaj co najmniej jedną minutę przed zamknięciem okno dialogowe hello uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="2ae18-145">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="2ae18-146">Jeśli używasz serwera proxy, upewnij się, poprawnie skonfigurowany serwer proxy Eksploratora usługi Storage hello.</span><span class="sxs-lookup"><span data-stu-id="2ae18-146">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="2ae18-147">Widok hello konsoli dla deweloperów, naciskając klawisz F12 hello.</span><span class="sxs-lookup"><span data-stu-id="2ae18-147">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="2ae18-148">Obejrzyj hello odpowiedzi z konsoli dla deweloperów hello i zobacz, czy można znaleźć żadnych clue Dlaczego uwierzytelniania nie działa.</span><span class="sxs-lookup"><span data-stu-id="2ae18-148">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="2ae18-149">Nie można usunąć konta</span><span class="sxs-lookup"><span data-stu-id="2ae18-149">Cannot remove account</span></span>

<span data-ttu-id="2ae18-150">Jeśli jesteś tooremove konta lub łącze Uwierzytelnij ponownie hello wykonywać żadnych czynności, wykonaj te kroki tootroubleshoot ten problem:</span><span class="sxs-lookup"><span data-stu-id="2ae18-150">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="2ae18-151">Spróbuj usuwanie hello następujące pliki z katalogu głównego, a następnie ponowne dodawanie konta hello:</span><span class="sxs-lookup"><span data-stu-id="2ae18-151">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="2ae18-152">.adalcache</span><span class="sxs-lookup"><span data-stu-id="2ae18-152">.adalcache</span></span>

    - <span data-ttu-id="2ae18-153">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="2ae18-153">.devaccounts</span></span>

    - <span data-ttu-id="2ae18-154">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="2ae18-154">.extaccounts</span></span>

- <span data-ttu-id="2ae18-155">Jeśli chcesz tooremove SAS dołączony zasobów magazynu, należy usunąć hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="2ae18-155">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="2ae18-156">Folder %appdata%/StorageExplorer dla systemu Windows</span><span class="sxs-lookup"><span data-stu-id="2ae18-156">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="2ae18-157">/Users/ < twoje_imie >/biblioteki/komputerze Obsługa/StorageExplorer dla komputerów Mac</span><span class="sxs-lookup"><span data-stu-id="2ae18-157">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="2ae18-158">~/.config/StorageExplorer dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="2ae18-158">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="2ae18-159">Konieczne będzie tooreenter swoje poświadczenia po usunięciu tych plików.</span><span class="sxs-lookup"><span data-stu-id="2ae18-159">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="2ae18-160">Problemy z serwera proxy</span><span class="sxs-lookup"><span data-stu-id="2ae18-160">Proxy issues</span></span>

<span data-ttu-id="2ae18-161">Najpierw upewnij się, ten powitania po wprowadzone informacje są wszystkie prawidłowe:</span><span class="sxs-lookup"><span data-stu-id="2ae18-161">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="2ae18-162">Witaj, adres URL serwera proxy i port numer</span><span class="sxs-lookup"><span data-stu-id="2ae18-162">hello proxy URL and port number</span></span>

- <span data-ttu-id="2ae18-163">Nazwa użytkownika i hasło, jeśli jest to wymagane przez serwer proxy hello</span><span class="sxs-lookup"><span data-stu-id="2ae18-163">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="2ae18-164">Typowe rozwiązania</span><span class="sxs-lookup"><span data-stu-id="2ae18-164">Common solutions</span></span>

<span data-ttu-id="2ae18-165">Jeśli nadal występują problemy, wykonaj te kroki tootroubleshoot je:</span><span class="sxs-lookup"><span data-stu-id="2ae18-165">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="2ae18-166">Jeśli łączysz toohello Internet bez użycia serwera proxy, sprawdź, czy Eksploratora usługi Storage działa bez włączone ustawienia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2ae18-166">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="2ae18-167">Jeśli hello tak jest, może istnieć problem z ustawieniami serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2ae18-167">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="2ae18-168">Współpraca z problemów hello tooidentify administratora serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="2ae18-168">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="2ae18-169">Sprawdź, czy inne aplikacje korzystające z serwera proxy hello działają zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="2ae18-169">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="2ae18-170">Sprawdź, czy masz połączenie toohello portalu Microsoft Azure za pomocą przeglądarki sieci web</span><span class="sxs-lookup"><span data-stu-id="2ae18-170">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="2ae18-171">Sprawdź, czy możesz odbierać odpowiedzi z punktami końcowymi usługi.</span><span class="sxs-lookup"><span data-stu-id="2ae18-171">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="2ae18-172">Wprowadź jeden z adresami URL punktu końcowego w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="2ae18-172">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="2ae18-173">Jeśli można połączyć, powinien zostać wyświetlony InvalidQueryParameterValue lub podobne odpowiedzi XML.</span><span class="sxs-lookup"><span data-stu-id="2ae18-173">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="2ae18-174">Jeśli ktoś inny korzysta również Eksploratora usługi Storage z serwerem proxy, sprawdź, czy można połączyć.</span><span class="sxs-lookup"><span data-stu-id="2ae18-174">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="2ae18-175">Jeśli można się połączyć, może być toocontact administratorem serwera proxy</span><span class="sxs-lookup"><span data-stu-id="2ae18-175">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="2ae18-176">Narzędzia do diagnozowania problemów</span><span class="sxs-lookup"><span data-stu-id="2ae18-176">Tools for diagnosing issues</span></span>

<span data-ttu-id="2ae18-177">Jeśli masz sieci narzędzi, takich jak Fiddler dla systemu Windows może toodiagnose hello problemy mogą się następująco:</span><span class="sxs-lookup"><span data-stu-id="2ae18-177">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="2ae18-178">Jeśli masz toowork za pośrednictwem serwera proxy, może być tooconfigure Twojego sieci tooconnect narzędzia za pośrednictwem serwera proxy hello.</span><span class="sxs-lookup"><span data-stu-id="2ae18-178">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="2ae18-179">Sprawdź hello numeru portu używanego przez narzędzie do sieci.</span><span class="sxs-lookup"><span data-stu-id="2ae18-179">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="2ae18-180">Wprowadź adres URL hosta lokalnego hello i hello sieci jako ustawienia serwera proxy w Eksploratorze usługi Storage narzędzia numer portu.</span><span class="sxs-lookup"><span data-stu-id="2ae18-180">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="2ae18-181">Jeśli odbywa się prawidłowo, narzędzie sieci uruchamia rejestrowanie żądań sieci przez punkty końcowe usług i toomanagement Eksploratora usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="2ae18-181">If this is done correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="2ae18-182">Na przykład wprowadź https://cawablobgrs.blob.core.windows.net/ dla punktu końcowego obiektu blob w przeglądarce, a otrzymasz odpowiedź podobne następującego hello, które sugeruje hello zasób istnieje, mimo że nie można do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="2ae18-182">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![Przykładowy kod](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="2ae18-184">Skontaktuj się z administratorem serwera proxy</span><span class="sxs-lookup"><span data-stu-id="2ae18-184">Contact proxy server admin</span></span>

<span data-ttu-id="2ae18-185">Jeśli ustawienia serwera proxy są prawidłowe, może być toocontact administratora serwera proxy i</span><span class="sxs-lookup"><span data-stu-id="2ae18-185">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="2ae18-186">Upewnij się, że serwer proxy blokuje ruch tooAzure zarządzania lub zasobu punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="2ae18-186">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="2ae18-187">Sprawdź hello protokół uwierzytelniania używany przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="2ae18-187">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="2ae18-188">Eksplorator usługi Storage aktualnie nie obsługuje serwerów proxy NTLM.</span><span class="sxs-lookup"><span data-stu-id="2ae18-188">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="2ae18-189">Komunikat o błędzie "tooRetrieve dzieci"</span><span class="sxs-lookup"><span data-stu-id="2ae18-189">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="2ae18-190">Jeśli jesteś tooAzure połączonych za pośrednictwem serwera proxy, sprawdź, czy ustawienia serwera proxy są poprawne.</span><span class="sxs-lookup"><span data-stu-id="2ae18-190">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="2ae18-191">Jeśli dostęp do zasobów tooa zostały przyznane przez właściciela hello hello subskrypcji lub konta, sprawdź, czy znasz, lub listę uprawnień dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="2ae18-191">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="2ae18-192">Problemy z adresem URL SAS</span><span class="sxs-lookup"><span data-stu-id="2ae18-192">Issues with SAS URL</span></span>
<span data-ttu-id="2ae18-193">W przypadku łączenia tooa usługi przy użyciu adresu URL SAS i występuje błąd:</span><span class="sxs-lookup"><span data-stu-id="2ae18-193">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="2ae18-194">Upewnij się, że adres URL hello dostarcza niezbędne uprawnienia hello tooread lub listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2ae18-194">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="2ae18-195">Sprawdź powitalne tego adresu URL nie wygasł.</span><span class="sxs-lookup"><span data-stu-id="2ae18-195">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="2ae18-196">Jeśli adres URL SAS hello jest oparta na zasadach dostępu, sprawdź, czy zasady dostępu hello nie został odwołany.</span><span class="sxs-lookup"><span data-stu-id="2ae18-196">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ae18-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ae18-197">Next steps</span></span>

<span data-ttu-id="2ae18-198">Jeśli hello rozwiązania nie działają dla Ciebie, przesłać problem za pomocą narzędzia opinii hello z poczty e-mail i szczegółów o problemie hello uwzględnione podczas można tak, aby firma Microsoft może skontaktować się z Tobą ustalania hello problem.</span><span class="sxs-lookup"><span data-stu-id="2ae18-198">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="2ae18-199">toodo tego, kliknij **pomocy** menu, a następnie kliknij przycisk **Prześlij opinię**.</span><span class="sxs-lookup"><span data-stu-id="2ae18-199">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Opinia](./media/storage-explorer-troubleshooting/4022503_en_1.png)
