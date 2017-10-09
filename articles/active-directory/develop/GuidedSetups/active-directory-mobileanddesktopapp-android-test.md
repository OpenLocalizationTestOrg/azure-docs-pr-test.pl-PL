---
title: aaaAzure AD w wersji 2 dla systemu Android wprowadzenie - Test | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="9b870-103">Testowanie kodu</span><span class="sxs-lookup"><span data-stu-id="9b870-103">Test your code</span></span>

1. <span data-ttu-id="9b870-104">Wdrażanie z kodu tooyour urządzeniu/emulatorze.</span><span class="sxs-lookup"><span data-stu-id="9b870-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="9b870-105">Gdy wszystko będzie gotowe tootest, za pomocą usługi Microsoft Azure Active Directory (konto organizacyjne) lub toosign konta Account Microsoft (live.com, outlook.com), w.</span><span class="sxs-lookup"><span data-stu-id="9b870-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="9b870-106">![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="9b870-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="9b870-107">
![Logowanie](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="9b870-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="9b870-108">Zgody</span><span class="sxs-lookup"><span data-stu-id="9b870-108">Consent</span></span>
<span data-ttu-id="9b870-109">Witaj po raz pierwszy użytkownik loguje się aplikacji tooyour one zostanie wyświetlone zgody ekran podobny toohello poniżej, gdzie muszą zaakceptować tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="9b870-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Zgody](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="9b870-111">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="9b870-111">Expected results</span></span>
<span data-ttu-id="9b870-112">Powinny pojawić się wyniki hello tooMicrosoft wywołania interfejsu API programu Graph 'me' punkt końcowy jest używany profil użytkownika hello tootooobtain — https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="9b870-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="9b870-113">Listę typowych Microsoft Graph punktów końcowych, zobacz to [artykułu](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="9b870-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="9b870-114">Więcej informacji o zakresach i uprawnień delegowanych</span><span class="sxs-lookup"><span data-stu-id="9b870-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="9b870-115">Witaj interfejsu API programu Microsoft Graph wymaga hello `user.read` zakres tooread hello profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b870-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="9b870-116">Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="9b870-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="9b870-117">Niektóre inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych może wymagać dodatkowych zakresów.</span><span class="sxs-lookup"><span data-stu-id="9b870-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="9b870-118">Na przykład dla programu Microsoft Graph hello zakresu `Calendars.Read` jest kalendarzy wymagane toolist hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b870-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="9b870-119">W kolejności tooaccess hello kalendarza użytkownika w kontekście aplikacji, należy tooadd hello `Calendars.Read` delegowane informacje rejestracyjne uprawnienia toohello aplikacji, a następnie dodaj hello `Calendars.Read` toohello zakres `acquireTokenSilentAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="9b870-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="9b870-120">Hello użytkownika może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę hello zakresów.</span><span class="sxs-lookup"><span data-stu-id="9b870-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
