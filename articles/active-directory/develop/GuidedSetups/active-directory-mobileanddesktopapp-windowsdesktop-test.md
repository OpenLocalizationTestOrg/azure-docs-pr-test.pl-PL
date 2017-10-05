---
title: "Usługi Azure AD v2 Windows Desktop pobieranie rozpoczęte — testowanie | Dokumentacja firmy Microsoft"
description: "Jak aplikacje .NET pulpitu systemu Windows (XAML) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="8e00f-103">Testowanie kodu</span><span class="sxs-lookup"><span data-stu-id="8e00f-103">Test your code</span></span>

<span data-ttu-id="8e00f-104">Aby przetestować aplikację, naciśnij klawisz `F5` do uruchomienia projektu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e00f-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="8e00f-105">Powinna zostać wyświetlona okno główne:</span><span class="sxs-lookup"><span data-stu-id="8e00f-105">Your Main Window should appear:</span></span>

![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="8e00f-107">Gdy wszystko jest gotowe do testowania, kliknij przycisk *wywołać Microsoft interfejsu API programu Graph* i używane do logowania Microsoft Azure Active Directory (konto organizacyjne) lub konta Account Microsoft (live.com, outlook.com).</span><span class="sxs-lookup"><span data-stu-id="8e00f-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="8e00f-108">Jego jest po raz pierwszy, zostanie wyświetlone okno z zapytaniem logowanie użytkownika:</span><span class="sxs-lookup"><span data-stu-id="8e00f-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![Logowanie](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="8e00f-110">Zgody</span><span class="sxs-lookup"><span data-stu-id="8e00f-110">Consent</span></span>
<span data-ttu-id="8e00f-111">Podczas pierwszego logowania się do aplikacji, użytkownik zobaczy zgody ekran podobny do poniżej, gdzie należy jawnie akceptować:</span><span class="sxs-lookup"><span data-stu-id="8e00f-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Zgoda ekranu](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="8e00f-113">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="8e00f-113">Expected results</span></span>
<span data-ttu-id="8e00f-114">Powinny zostać wyświetlone informacje o profilu użytkownika zwrócony przez wywołanie interfejsu API programu Microsoft Graph na ekranie wyniki wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="8e00f-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="8e00f-115">Podstawowe informacje o tokenie nabyte za pośrednictwem powinno również zostać wyświetlone `AcquireTokenAsync` lub `AcquireTokenSilentAsync` w polu informacji o tokenie:</span><span class="sxs-lookup"><span data-stu-id="8e00f-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="8e00f-116">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8e00f-116">Property</span></span>  |<span data-ttu-id="8e00f-117">Format</span><span class="sxs-lookup"><span data-stu-id="8e00f-117">Format</span></span>  |<span data-ttu-id="8e00f-118">Opis</span><span class="sxs-lookup"><span data-stu-id="8e00f-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="8e00f-119">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8e00f-119">Name</span></span> | <span data-ttu-id="8e00f-120">{Pełna nazwa użytkownika}</span><span class="sxs-lookup"><span data-stu-id="8e00f-120">{User Full name}</span></span> |<span data-ttu-id="8e00f-121">Użytkownik miał na imię i nazwisko</span><span class="sxs-lookup"><span data-stu-id="8e00f-121">The user’s first and last name</span></span>|
|<span data-ttu-id="8e00f-122">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="8e00f-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="8e00f-123">Nazwa użytkownika używana do identyfikacji użytkownika</span><span class="sxs-lookup"><span data-stu-id="8e00f-123">The username used to identify the user</span></span>|
|<span data-ttu-id="8e00f-124">Wygaśnięcia tokenu</span><span class="sxs-lookup"><span data-stu-id="8e00f-124">Token Expires</span></span> |<span data-ttu-id="8e00f-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="8e00f-125">{DateTime}</span></span>         |<span data-ttu-id="8e00f-126">Czas wygaśnięcia tokenu.</span><span class="sxs-lookup"><span data-stu-id="8e00f-126">The time on which the token expires.</span></span> <span data-ttu-id="8e00f-127">MSAL będzie przedłużyć datę wygaśnięcia dla Ciebie odnowienie token, gdy jest to konieczne</span><span class="sxs-lookup"><span data-stu-id="8e00f-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="8e00f-128">Token dostępu</span><span class="sxs-lookup"><span data-stu-id="8e00f-128">Access token</span></span> |<span data-ttu-id="8e00f-129">{Ciąg}</span><span class="sxs-lookup"><span data-stu-id="8e00f-129">{String}</span></span>         |<span data-ttu-id="8e00f-130">Ciąg tokena wysłane który będą wysyłane na żądania HTTP, które wymagają nagłówek autoryzacji</span><span class="sxs-lookup"><span data-stu-id="8e00f-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="8e00f-131">Więcej informacji o zakresach i uprawnień delegowanych</span><span class="sxs-lookup"><span data-stu-id="8e00f-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="8e00f-132">Interfejs API Graph wymaga `user.read` zasięg odczytuj profil użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e00f-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="8e00f-133">Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="8e00f-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="8e00f-134">Niektóre inne interfejsy API Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych wymaga dodatkowych zakresów.</span><span class="sxs-lookup"><span data-stu-id="8e00f-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="8e00f-135">Na przykład do wykresu `Calendars.Read` jest wymagany do listy kalendarzach.</span><span class="sxs-lookup"><span data-stu-id="8e00f-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="8e00f-136">Aby uzyskać dostęp do kalendarza użytkownika w kontekście aplikacji, musisz dodać `Calendars.Read` delegowane informacji o rejestracji aplikacji, a następnie dodaj `Calendars.Read` do `AcquireTokenAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="8e00f-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="8e00f-137">Użytkownik może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę zakresów.</span><span class="sxs-lookup"><span data-stu-id="8e00f-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



