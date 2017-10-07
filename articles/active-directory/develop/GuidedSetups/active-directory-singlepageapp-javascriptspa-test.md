---
title: aaaAzure AD v2 JS SPA instrukcje konfiguracji - Test | Dokumentacja firmy Microsoft
description: "Jak aplikacje JavaScript SPA można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="6c867-103">Testowanie kodu</span><span class="sxs-lookup"><span data-stu-id="6c867-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="6c867-104">Testowanie za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6c867-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="6c867-105">Jeśli używasz programu Visual Studio, naciśnij klawisz `F5` toorun projektu: hello przeglądarki zostanie otwarty i kieruje użytkownika za*http://localhost: {port}* której występuje hello *wywołać Microsoft interfejsu API programu Graph* przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c867-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="6c867-106">Testowanie za pomocą języka Python lub inny serwer sieci web</span><span class="sxs-lookup"><span data-stu-id="6c867-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="6c867-107">Jeśli nie używasz programu Visual Studio, upewnij się, serwer sieci web jest uruchomiona i został on skonfigurowany toolisten tooa TCP port oparte na powitania folder zawierający Twoje *index.html* pliku.</span><span class="sxs-lookup"><span data-stu-id="6c867-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="6c867-108">Dla języka Python, może rozpocząć nasłuchiwania portu toohello uruchamiając hello w poleceniu hello monitu / terminali, z folderu aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="6c867-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="6c867-109">Następnie otwórz przeglądarkę hello i wpisz *adresem http://localhost: 8080* lub *http://localhost: {port}* — w przypadku gdy hello *portu* odpowiada toohello port serwera sieci web nasłuchiwanie.</span><span class="sxs-lookup"><span data-stu-id="6c867-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="6c867-110">Powinna zostać wyświetlona zawartość strony index.html z hello hello *wywołać Microsoft interfejsu API programu Graph* przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c867-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="6c867-111">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="6c867-111">Test your application</span></span>

<span data-ttu-id="6c867-112">Po przeglądarki hello ładuje Twojej *index.html*, kliknij hello *wywołać Microsoft interfejsu API programu Graph* przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c867-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="6c867-113">Jeśli hello po raz pierwszy, przekierowania przeglądarki hello możesz toohello v2 Microsoft Azure Active Directory punktu końcowego, gdzie są monit toosign w.</span><span class="sxs-lookup"><span data-stu-id="6c867-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![Zrzut ekranu przedstawiający przykładowy](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="6c867-115">Zgody</span><span class="sxs-lookup"><span data-stu-id="6c867-115">Consent</span></span>
<span data-ttu-id="6c867-116">Witaj pierwszego zalogowaniu w aplikacji tooyour prezentowany zgody ekran podobny toohello poniższe polecenie, wymagających tooaccept:</span><span class="sxs-lookup"><span data-stu-id="6c867-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![Zgoda ekranu](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="6c867-118">Oczekiwanych rezultatów</span><span class="sxs-lookup"><span data-stu-id="6c867-118">Expected results</span></span>
<span data-ttu-id="6c867-119">Powinny zostać wyświetlone informacje o profilu użytkownika zwracane przez hello odpowiedzi wywołań interfejsu API programu Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6c867-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![Wyniki](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="6c867-121">Zobacz też podstawowe informacje o token hello nabyte w hello *Token dostępu* i *identyfikator tokenu oświadczeń* pola.</span><span class="sxs-lookup"><span data-stu-id="6c867-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="6c867-122">Więcej informacji o zakresach i uprawnień delegowanych</span><span class="sxs-lookup"><span data-stu-id="6c867-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="6c867-123">Witaj interfejsu API programu Microsoft Graph wymaga hello `user.read` zakres tooread hello profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6c867-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="6c867-124">Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="6c867-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="6c867-125">Niektóre inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych może wymagać dodatkowych zakresów.</span><span class="sxs-lookup"><span data-stu-id="6c867-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="6c867-126">Na przykład dla programu Microsoft Graph hello zakresu `Calendars.Read` jest kalendarzy wymagane toolist hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6c867-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="6c867-127">W kolejności tooaccess hello kalendarza użytkownika w kontekście aplikacji hello należy tooadd hello `Calendars.Read` delegowane informacje rejestracyjne uprawnienia toohello aplikacji, a następnie dodaj hello `Calendars.Read` toohello zakres `acquireTokenSilent` wywołania.</span><span class="sxs-lookup"><span data-stu-id="6c867-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="6c867-128">Hello użytkownika może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę hello zakresów.</span><span class="sxs-lookup"><span data-stu-id="6c867-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="6c867-129">Jeśli interfejs API zaplecza nie wymaga zakresu (niezalecane), możesz użyć hello `clientId` jako zakres hello hello `acquireTokenSilent` i/lub `acquireTokenRedirect` wywołania.</span><span class="sxs-lookup"><span data-stu-id="6c867-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
