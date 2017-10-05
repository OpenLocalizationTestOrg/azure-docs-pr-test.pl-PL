---
title: Azure AD w wersji 2 dla systemu iOS Getting Started - Test | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 4a88096d2b0a23708acdbc1798eac528599b4f71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
## <a name="test-querying-the-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="d4a7d-103">Testowanie zapytań interfejsu API programu Microsoft Graph z aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="d4a7d-103">Test querying the Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="d4a7d-104">Naciśnij klawisz `Command`  +  `R` na uruchamianie kodu w symulatorze.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-104">Press `Command` + `R` to run the code in the simulator.</span></span>

![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="d4a7d-106">Gdy wszystko jest gotowe do testowania, naciśnij przycisk *"Wywołaj Microsoft interfejsu API programu Graph"* i pojawi się monit o wpisanie nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-106">When you're ready to test, tap *‘Call Microsoft Graph API’* and you will be prompted to type your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="d4a7d-107">Zgody</span><span class="sxs-lookup"><span data-stu-id="d4a7d-107">Consent</span></span>
<span data-ttu-id="d4a7d-108">Podczas pierwszego logowania się do aplikacji, użytkownik zobaczy zgody ekran podobny do poniżej, gdzie należy jawnie akceptować:</span><span class="sxs-lookup"><span data-stu-id="d4a7d-108">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Zgoda ekranu](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="d4a7d-110">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="d4a7d-110">Expected results</span></span>
<span data-ttu-id="d4a7d-111">Powinny pojawić się informacje o profilu użytkownika zwracane przez interfejs API programu Microsoft Graph wywołanie w *rejestrowanie* sekcji.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-111">You should see user profile information returned by the Microsoft Graph API call in the *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="d4a7d-112">Więcej informacji o zakresach i uprawnień delegowanych</span><span class="sxs-lookup"><span data-stu-id="d4a7d-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="d4a7d-113">Wymaga interfejsu API programu Microsoft Graph `user.read` zakresu odczytać profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-113">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="d4a7d-114">Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="d4a7d-115">Niektóre inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych może wymagać dodatkowych zakresów.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="d4a7d-116">Na przykład dla programu Microsoft Graph, zakres `Calendars.Read` jest wymagana, aby wyświetlić listę kalendarzy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-116">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="d4a7d-117">Aby uzyskać dostęp do kalendarza użytkownika w kontekście aplikacji, musisz dodać `Calendars.Read` delegowane uprawnienia do informacji o rejestracji aplikacji, a następnie dodaj `Calendars.Read` zakres do `acquireTokenSilent` wywołania.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-117">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="d4a7d-118">Użytkownik może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę zakresów.</span><span class="sxs-lookup"><span data-stu-id="d4a7d-118">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



