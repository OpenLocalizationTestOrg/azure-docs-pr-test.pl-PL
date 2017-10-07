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
## <a name="test-your-code"></a>Testowanie kodu

> ### <a name="testing-with-visual-studio"></a>Testowanie za pomocą programu Visual Studio
> Jeśli używasz programu Visual Studio, naciśnij klawisz `F5` toorun projektu: hello przeglądarki zostanie otwarty i kieruje użytkownika za*http://localhost: {port}* której występuje hello *wywołać Microsoft interfejsu API programu Graph* przycisku.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Testowanie za pomocą języka Python lub inny serwer sieci web
> Jeśli nie używasz programu Visual Studio, upewnij się, serwer sieci web jest uruchomiona i został on skonfigurowany toolisten tooa TCP port oparte na powitania folder zawierający Twoje *index.html* pliku. Dla języka Python, może rozpocząć nasłuchiwania portu toohello uruchamiając hello w poleceniu hello monitu / terminali, z folderu aplikacji hello:
> 
> ```bash
> python -m http.server 8080
> ```
>  Następnie otwórz przeglądarkę hello i wpisz *adresem http://localhost: 8080* lub *http://localhost: {port}* — w przypadku gdy hello *portu* odpowiada toohello port serwera sieci web nasłuchiwanie. Powinna zostać wyświetlona zawartość strony index.html z hello hello *wywołać Microsoft interfejsu API programu Graph* przycisku.

## <a name="test-your-application"></a>Testowanie aplikacji

Po przeglądarki hello ładuje Twojej *index.html*, kliknij hello *wywołać Microsoft interfejsu API programu Graph* przycisku. Jeśli hello po raz pierwszy, przekierowania przeglądarki hello możesz toohello v2 Microsoft Azure Active Directory punktu końcowego, gdzie są monit toosign w.
 
![Zrzut ekranu przedstawiający przykładowy](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>Zgody
Witaj pierwszego zalogowaniu w aplikacji tooyour prezentowany zgody ekran podobny toohello poniższe polecenie, wymagających tooaccept:

 ![Zgoda ekranu](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>Oczekiwanych rezultatów
Powinny zostać wyświetlone informacje o profilu użytkownika zwracane przez hello odpowiedzi wywołań interfejsu API programu Microsoft Graph.
 
 ![Wyniki](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

Zobacz też podstawowe informacje o token hello nabyte w hello *Token dostępu* i *identyfikator tokenu oświadczeń* pola.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Więcej informacji o zakresach i uprawnień delegowanych

Witaj interfejsu API programu Microsoft Graph wymaga hello `user.read` zakres tooread hello profilu użytkownika. Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji. Niektóre inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych może wymagać dodatkowych zakresów. Na przykład dla programu Microsoft Graph hello zakresu `Calendars.Read` jest kalendarzy wymagane toolist hello użytkownika. W kolejności tooaccess hello kalendarza użytkownika w kontekście aplikacji hello należy tooadd hello `Calendars.Read` delegowane informacje rejestracyjne uprawnienia toohello aplikacji, a następnie dodaj hello `Calendars.Read` toohello zakres `acquireTokenSilent` wywołania. Hello użytkownika może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę hello zakresów.

Jeśli interfejs API zaplecza nie wymaga zakresu (niezalecane), możesz użyć hello `clientId` jako zakres hello hello `acquireTokenSilent` i/lub `acquireTokenRedirect` wywołania.

<!--end-collapse-->
