---
title: 'Azure Active Directory B2C: rejestrowanie aplikacji | Microsoft Docs'
description: "Jak tooregister aplikacji przy użyciu usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: rejestrowanie aplikacji

Ten samouczek szybkiego startu pomaga zarejestrować aplikację w dzierżawie usługi Microsoft Azure Active Directory (Azure AD) B2C w ciągu kilku minut. Po zakończeniu aplikacji są rejestrowane w dzierżawie powitalnych Azure B2C.

## <a name="prerequisites"></a>Wymagania wstępne

toobuild aplikację, która akceptuje konsumenta rejestracji i logowania, należy najpierw aplikacji hello tooregister z dzierżawy usługi Azure Active Directory B2C. Utworzyć własną dzierżawę za pomocą hello czynności opisane w temacie [tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).

Musi być zarządzane aplikacje utworzone za pomocą bloku hello Azure AD B2C w portalu Azure hello z hello tej samej lokalizacji. Po zmodyfikowaniu aplikacji B2C hello przy użyciu programu PowerShell lub innego portalu stają się nieobsługiwane i nie działają usługi Azure AD B2C. Zobacz szczegóły w hello [wystąpił błąd aplikacji](#faulted-apps) sekcji. 

## <a name="navigate-toob2c-settings"></a>Przejdź do ustawień tooB2C

Zaloguj się za toohello [portalu Azure](https://portal.azure.com/) jako Administrator globalny dzierżawy hello B2C hello. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

Wybierz następne kroki na podstawie typu aplikacji hello, rejestrowany:

* [Rejestrowanie aplikacji internetowej](#register-a-web-app)
* [Rejestrowanie internetowego interfejsu API](#register-a-web-api)
* [Rejestrowanie aplikacji mobilnej lub natywnej](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>Rejestrowanie aplikacji internetowej

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

Jeśli Twoja aplikacja internetowa wywołuje internetowy interfejs API zabezpieczony przez usługę Azure AD B2C, wykonaj następujące kroki:
   1. Utwórz klucz tajny aplikacji przez przejście toohello **klucze** bloku i klikając hello **Wygeneruj klucz** przycisku. Zwróć uwagę na powitania **klucz aplikacji** wartość. Wartość hello są używane jako klucz tajny aplikacji hello w kodzie aplikacji.
   2. Kliknij pozycję **Dostęp do interfejsu API**, kliknij pozycję **Dodaj** i wybierz swój internetowy interfejs API oraz zakresy (uprawnienia).

> [!NOTE]
> **Klucz tajny aplikacji** jest ważnym poświadczeniem zabezpieczeń i powinien być odpowiednio zabezpieczony.
> 

[Przeskocz zbyt**następne kroki**](#next-steps)

## <a name="register-a-web-api"></a>Rejestrowanie internetowego interfejsu API

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

Kliknij przycisk **opublikowane zakresy** tooadd więcej zakresów niezbędne. Domyślnie zakresu "user_impersonation" hello jest zdefiniowany. zakres user_impersonation Hello daje innych aplikacji hello możliwości tooaccess ten interfejs api imieniu hello zalogowanego użytkownika. Jeśli chcesz, można usunąć hello user_impersonation zakresu.

[Przeskocz zbyt**następne kroki**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>Rejestrowanie aplikacji mobilnej lub natywnej

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[Przeskocz zbyt**następne kroki**](#next-steps)

## <a name="limitations"></a>Ograniczenia

### <a name="choosing-a-web-app-or-api-reply-url"></a>Wybieranie aplikacji internetowej lub adresu URL odpowiedzi interfejsu API

Obecnie aplikacje, które są zarejestrowane w usłudze Azure AD B2C są ograniczone tooa ograniczony zestaw wartości adresu URL odpowiedzi. Witaj odpowiedzi z adresu URL dla usług i aplikacji sieci web musi rozpoczynać się od schematu hello `https`, i wszystkich odpowiedzi wartości adres URL musi współdzielenie jednej domeny DNS. Na przykład nie można zarejestrować aplikacji internetowej z jednym z następujących adresów URL odpowiedzi:

`https://login-east.contoso.com`

`https://login-west.contoso.com`

system rejestracji Hello porównuje hello całego nazwę DNS hello istniejących odpowiedzi adresu URL toohello nazwy DNS hello adresu URL odpowiedzi, który dodajesz. Witaj żądania tooadd Witaj nazwy DNS zakończy się niepowodzeniem, jeśli jest spełniony dowolny z hello następujące warunki:

* Hello całą nazwę DNS hello nowy adres URL odpowiedzi jest niezgodny z nazwą DNS hello hello istniejący adres URL odpowiedzi.
* Hello całą nazwę DNS hello nowy adres URL odpowiedzi nie jest poddomeną hello istniejący adres URL odpowiedzi.

Na przykład jeśli hello aplikacji ma ten adres URL odpowiedzi:

`https://login.contoso.com`

Można dodać tooit w następujący sposób:

`https://login.contoso.com/new`

W takim przypadku nazwa DNS hello są dokładnie. Można też zrobić tak:

`https://new.login.contoso.com`

W takim przypadku odwołujesz poddomenie DNS tooa login.contoso.com. Jeśli chcesz toohave aplikację, która ma logowania east.contoso.com i west.contoso.com logowania jako adresy URL odpowiedzi, należy dodać te adresy URL odpowiedzi w następującej kolejności:

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Ponieważ są one poddomen hello pierwszy adres URL odpowiedzi, można dodać hello tych dwóch contoso.com.

### <a name="choosing-a-native-app-redirect-uri"></a>Wybieranie identyfikatora URI przekierowania aplikacji natywnej

Istnieją dwie ważne kwestie, które należy wziąć pod uwagę podczas wybierania identyfikatora URI przekierowania dla aplikacji mobilych/natywnych:

* **Unikatowy**: hello schemat identyfikatora URI przekierowania hello powinna być unikatowa dla każdej aplikacji. W naszym przykładzie (com.onmicrosoft.contoso.appname://redirect/path) używamy com.onmicrosoft.contoso.appname hello schemat. Zalecamy stosowanie się do tego wzorca. Jeśli dwie aplikacje korzystają hello sam schemat, hello użytkownik widzi okna dialogowego "Wybierz aplikacji". Użytkownik hello dokonuje nieprawidłowego wyboru, hello logowania nie powiedzie się.
* **Kompletność**: identyfikator URI przekierowania musi mieć schemat i ścieżkę. Ścieżka Hello musi zawierać co najmniej jeden ukośnik po hello domeny (na przykład działa //contoso/ i //contoso kończy się niepowodzeniem).

Upewnij się, czy nie ma żadnych znaków specjalnych, takich jak identyfikator uri przekierowania podkreślenia w hello.

### <a name="faulted-apps"></a>Uszkodzone aplikacje

NIE NALEŻY edytować aplikacji B2C:

* W innych portalach zarządzania aplikacjami, takich jak [klasyczna witryna Azure Portal](https://manage.windowsazure.com/) i [portal rejestracji aplikacji](https://apps.dev.microsoft.com/).
* Korzystanie z interfejsu API programu Graph lub programu PowerShell

Jeśli Edycja aplikacji hello B2C opisane powyżej, a następnie spróbuj tooedit hello go ponownie w bloku funkcji hello Azure AD B2C w portalu Azure, staje się błędnej aplikacji i aplikacja nie jest już możliwe z usługi Azure AD B2C. Aplikacja hello toodelete i utwórz go ponownie.

Aplikacja hello toodelete, przejdź toohello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/) i usuwania aplikacji hello istnieje. Aby toobe aplikacji hello jest widoczna należy toobe hello właściciel aplikacji hello (i nie tylko administrator dzierżawcy hello).

## <a name="next-steps"></a>Następne kroki

Teraz, po zarejestrowaniu aplikacji w usłudze Azure AD B2C można wykonać jedną z [naszych samouczków szybkiego startu](active-directory-b2c-overview.md#get-started) tooget do pracy.

> [!div class="nextstepaction"]
> [Tworzenie aplikacji internetowej platformy ASP.NET z rejestrowaniem, logowaniem i resetowaniem hasła](active-directory-b2c-devquickstarts-web-dotnet-susi.md)