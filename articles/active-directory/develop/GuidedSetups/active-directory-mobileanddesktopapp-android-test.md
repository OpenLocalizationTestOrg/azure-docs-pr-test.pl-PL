---
title: "Pobieranie systemu Android w wersji 2 usługi Azure AD rozpoczęte — testowanie | Dokumentacja firmy Microsoft"
description: "Jak uzyskać token dostępu i wywołania interfejsu API programu Microsoft Graph lub interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory aplikacji systemu Android"
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="8f762-103">Testowanie kodu</span><span class="sxs-lookup"><span data-stu-id="8f762-103">Test your code</span></span>

1. <span data-ttu-id="8f762-104">Wdrażanie kodu na urządzeniu/emulatorze.</span><span class="sxs-lookup"><span data-stu-id="8f762-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="8f762-105">Gdy wszystko jest gotowe do testowania, Microsoft Azure Active Directory (konto organizacyjne) lub konta Account Microsoft (live.com, outlook.com) można używać do logowania.</span><span class="sxs-lookup"><span data-stu-id="8f762-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="8f762-106">![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="8f762-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="8f762-107">
![Logowanie](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="8f762-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="8f762-108">Zgody</span><span class="sxs-lookup"><span data-stu-id="8f762-108">Consent</span></span>
<span data-ttu-id="8f762-109">Użytkownik loguje się do aplikacji, po raz pierwszy one zobaczy zgody ekran podobny do poniżej, gdzie muszą zaakceptować jawnie:</span><span class="sxs-lookup"><span data-stu-id="8f762-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![Zgody](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="8f762-111">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="8f762-111">Expected results</span></span>
<span data-ttu-id="8f762-112">Powinny pojawić się wyniki wywołania interfejsu API programu Microsoft Graph 'me' do uzyskania profil użytkownika — https://graph.microsoft.com/v1.0/me używane do punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="8f762-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="8f762-113">Listę typowych Microsoft Graph punktów końcowych, zobacz to [artykułu](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="8f762-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="8f762-114">Więcej informacji o zakresach i uprawnień delegowanych</span><span class="sxs-lookup"><span data-stu-id="8f762-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="8f762-115">Wymaga interfejsu API programu Microsoft Graph `user.read` zakresu odczytać profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f762-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="8f762-116">Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="8f762-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="8f762-117">Niektóre inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych może wymagać dodatkowych zakresów.</span><span class="sxs-lookup"><span data-stu-id="8f762-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="8f762-118">Na przykład dla programu Microsoft Graph, zakres `Calendars.Read` jest wymagana, aby wyświetlić listę kalendarzy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f762-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="8f762-119">Aby uzyskać dostęp do kalendarza użytkownika w kontekście aplikacji, musisz dodać `Calendars.Read` delegowane uprawnienia do informacji o rejestracji aplikacji, a następnie dodaj `Calendars.Read` zakres do `acquireTokenSilentAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="8f762-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="8f762-120">Użytkownik może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę zakresów.</span><span class="sxs-lookup"><span data-stu-id="8f762-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
