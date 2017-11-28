---
title: iOS v2 aaaAzure AD Getting Started - Test | Dokumentacja firmy Microsoft
description: "Jak aplikacje systemu iOS (Swift) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="7697f-103">Test zapytań hello Microsoft Graph API z poziomu aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="7697f-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="7697f-104">Naciśnij klawisz `Command`  +  `R` toorun hello kodu w symulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="7697f-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="7697f-106">Jeśli wszystko jest gotowe tootest, naciśnij przycisk *"Wywołaj Microsoft interfejsu API programu Graph"* i będzie tootype zostanie wyświetlony monit o nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="7697f-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="7697f-107">Zgody</span><span class="sxs-lookup"><span data-stu-id="7697f-107">Consent</span></span>
<span data-ttu-id="7697f-108">Hello po raz pierwszy zalogować stosując tooyour, zostaną wyświetlone z ekranu zgody o poniżej podobne toohello, gdzie należy zaakceptować tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="7697f-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Zgoda ekranu](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="7697f-110">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="7697f-110">Expected results</span></span>
<span data-ttu-id="7697f-111">Powinny być widoczne informacje o profilu użytkownika zwrócony przez wywołanie interfejsu API Graph usługi Microsoft hello w hello *rejestrowanie* sekcji.</span><span class="sxs-lookup"><span data-stu-id="7697f-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="7697f-112">Więcej informacji o zakresach i uprawnień delegowanych</span><span class="sxs-lookup"><span data-stu-id="7697f-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="7697f-113">Witaj interfejsu API programu Microsoft Graph wymaga hello `user.read` zakres tooread hello profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7697f-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="7697f-114">Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="7697f-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="7697f-115">Niektóre inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych może wymagać dodatkowych zakresów.</span><span class="sxs-lookup"><span data-stu-id="7697f-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="7697f-116">Na przykład dla programu Microsoft Graph hello zakresu `Calendars.Read` jest kalendarzy wymagane toolist hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7697f-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="7697f-117">W kolejności tooaccess hello kalendarza użytkownika w kontekście aplikacji, należy tooadd hello `Calendars.Read` delegowane informacje rejestracyjne uprawnienia toohello aplikacji, a następnie dodaj hello `Calendars.Read` toohello zakres `acquireTokenSilent` wywołania.</span><span class="sxs-lookup"><span data-stu-id="7697f-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="7697f-118">Hello użytkownika może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę hello zakresów.</span><span class="sxs-lookup"><span data-stu-id="7697f-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



