---
title: aaaAzure AD v2 Windows Desktop wprowadzenie - Test | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="5be70-103">Testowanie kodu</span><span class="sxs-lookup"><span data-stu-id="5be70-103">Test your code</span></span>

<span data-ttu-id="5be70-104">W celu tootest aplikacji, naciśnij klawisz `F5` toorun projektu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5be70-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="5be70-105">Powinna zostać wyświetlona okno główne:</span><span class="sxs-lookup"><span data-stu-id="5be70-105">Your Main Window should appear:</span></span>

![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="5be70-107">Jeśli wszystko jest gotowe tootest, kliknij przycisk *wywołać Microsoft interfejsu API programu Graph* i za pomocą usługi Microsoft Azure Active Directory (konto organizacyjne) lub toosign konta Account Microsoft (live.com, outlook.com), w.</span><span class="sxs-lookup"><span data-stu-id="5be70-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="5be70-108">Go powitania po raz pierwszy, zostanie wyświetlone okno z zapytaniem toosign użytkownika w:</span><span class="sxs-lookup"><span data-stu-id="5be70-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![Logowanie](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="5be70-110">Zgody</span><span class="sxs-lookup"><span data-stu-id="5be70-110">Consent</span></span>
<span data-ttu-id="5be70-111">Hello po raz pierwszy zalogować stosując tooyour, zostaną wyświetlone z ekranu zgody o poniżej podobne toohello, gdzie należy zaakceptować tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="5be70-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Zgoda ekranu](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="5be70-113">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="5be70-113">Expected results</span></span>
<span data-ttu-id="5be70-114">Informacje o profilu użytkownika zwrócony przez wywołanie interfejsu API Graph usługi Microsoft hello na ekranie wyniki wywołania interfejsu API hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="5be70-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="5be70-115">Podstawowe informacje o nabyte za pośrednictwem tokenu hello powinno również zostać wyświetlone `AcquireTokenAsync` lub `AcquireTokenSilentAsync` w polu informacji o tokenie hello:</span><span class="sxs-lookup"><span data-stu-id="5be70-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="5be70-116">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5be70-116">Property</span></span>  |<span data-ttu-id="5be70-117">Format</span><span class="sxs-lookup"><span data-stu-id="5be70-117">Format</span></span>  |<span data-ttu-id="5be70-118">Opis</span><span class="sxs-lookup"><span data-stu-id="5be70-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="5be70-119">Nazwa</span><span class="sxs-lookup"><span data-stu-id="5be70-119">Name</span></span> | <span data-ttu-id="5be70-120">{Pełna nazwa użytkownika}</span><span class="sxs-lookup"><span data-stu-id="5be70-120">{User Full name}</span></span> |<span data-ttu-id="5be70-121">Użytkownik Hello na imię i nazwisko</span><span class="sxs-lookup"><span data-stu-id="5be70-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="5be70-122">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="5be70-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="5be70-123">używana nazwa Hello tooidentify hello użytkownika</span><span class="sxs-lookup"><span data-stu-id="5be70-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="5be70-124">Wygaśnięcia tokenu</span><span class="sxs-lookup"><span data-stu-id="5be70-124">Token Expires</span></span> |<span data-ttu-id="5be70-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="5be70-125">{DateTime}</span></span>         |<span data-ttu-id="5be70-126">czas Hello, na które hello wygaśnięcia tokenu.</span><span class="sxs-lookup"><span data-stu-id="5be70-126">hello time on which hello token expires.</span></span> <span data-ttu-id="5be70-127">MSAL rozszerzy Data wygaśnięcia hello za odnowienie hello token, gdy jest to konieczne</span><span class="sxs-lookup"><span data-stu-id="5be70-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="5be70-128">Token dostępu</span><span class="sxs-lookup"><span data-stu-id="5be70-128">Access token</span></span> |<span data-ttu-id="5be70-129">{Ciąg}</span><span class="sxs-lookup"><span data-stu-id="5be70-129">{String}</span></span>         |<span data-ttu-id="5be70-130">ciąg tokenu Hello wysłane który będą wysyłane żądania tooHTTP, które wymagają nagłówek autoryzacji</span><span class="sxs-lookup"><span data-stu-id="5be70-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="5be70-131">Więcej informacji o zakresach i uprawnień delegowanych</span><span class="sxs-lookup"><span data-stu-id="5be70-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="5be70-132">Interfejs API Graph wymaga hello `user.read` zakres tooread profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5be70-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="5be70-133">Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="5be70-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="5be70-134">Niektóre inne interfejsy API Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych wymaga dodatkowych zakresów.</span><span class="sxs-lookup"><span data-stu-id="5be70-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="5be70-135">Na przykład do wykresu `Calendars.Read` jest wymagane toolist kalendarzach.</span><span class="sxs-lookup"><span data-stu-id="5be70-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="5be70-136">W kolejności tooaccess hello kalendarza użytkownika w kontekście aplikacji, należy tooadd `Calendars.Read` delegowane informacji o rejestracji aplikacji, a następnie dodaj `Calendars.Read` toohello `AcquireTokenAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="5be70-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="5be70-137">Użytkownik może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę hello zakresów.</span><span class="sxs-lookup"><span data-stu-id="5be70-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



