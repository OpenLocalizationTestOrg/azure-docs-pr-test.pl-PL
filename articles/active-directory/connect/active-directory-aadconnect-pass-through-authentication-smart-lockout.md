---
title: 'Azure AD Connect: Uwierzytelniania przekazywanego - blokady inteligentnej | Dokumentacja firmy Microsoft'
description: "W tym artykule opisano, jak Azure Active Directory (Azure AD) przekazywanego uwierzytelniania przed atakami siłowymi haseł w chmurze hello chroni konta lokalnego."
services: active-directory
keywords: "Azure AD Connect przekazywanego uwierzytelniania, instalacji usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Uwierzytelniania przekazywanego usługi Azure Active Directory: Blokady inteligentnej

## <a name="overview"></a>Omówienie

Usługi Azure AD chroni przed atakami siłowymi hasła i uniemożliwia użytkownikom oryginalnego blokowanie poza ich usługi Office 365 i aplikacji SaaS. Ta funkcja o nazwie **blokady inteligentnej**, jest obsługiwana w przypadku korzystania z uwierzytelniania przekazywanego jako metodę logowania. Blokady inteligentnej jest domyślnie włączona dla wszystkich dzierżawców i ochrony kont użytkowników cały czas hello; nie konieczności tooturn nie istnieje on w.

Blokady inteligentnej działa przez śledzenie nieudanych prób logowania i po pewnym **próg blokady**, rozpoczynając **czas trwania blokady**. Wszelkich prób logowania z atakująca hello podczas hello czas trwania blokady są odrzucane. Jeśli atak powitania będzie nadal występować, hello kolejnych nieudanych prób zalogowania po zakończeniu hello czas trwania blokady wynik w dłuższym czasie trwania blokady.

>[!NOTE]
>Domyślna Hello progu blokady konta to 10 nieudanych prób i domyślnego hello czas trwania blokady wynosi 60 sekund.

Blokady inteligentnej rozróżnia również logowania z oryginalnego użytkowników i osoby atakujące i tylko blokowane osoby atakujące hello w większości przypadków. Ta funkcja zapobiega osoby atakujące złośliwie zablokowania oryginalnego użytkowników. Używamy poza logowania zachowanie użytkowników urządzeń & przeglądarek i innych toodistinguish sygnały między użytkownikami oryginalny i osoby atakujące. Firma Microsoft stale umożliwiają zwiększenie nasze algorytmy.

Ponieważ uwierzytelniania przekazywanego przekazuje żądania weryfikacji haseł na lokalnej usługi Active Directory (AD), należy atakującym tooprevent blokowania kont usługi AD użytkowników. Ponieważ masz zasad blokady konta AD (w szczególności [ **próg blokady konta** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) i [ **Zresetuj licznik blokady konta po zasady** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), należy próg blokady tooconfigure usługi Azure AD i czas trwania blokady odpowiednio wartości toofilter limit ataków w chmurze hello przed dotarciem lokalnej usługi AD.

>[!NOTE]
>funkcji blokady inteligentnej Hello jest wolny i jest _na_ domyślnie dla wszystkich klientów. Modyfikowanie progu blokady konta usługi Azure AD i czas trwania blokady wartości przy użyciu interfejsu API programu Graph musi jednak licencji dzierżawy toohave co najmniej jednej usługi Azure AD Premium P2. Nie wymagają licencji usługi Azure AD Premium P2 _dla każdego użytkownika_ funkcji blokady inteligentnej hello tooget przy użyciu uwierzytelniania przekazywanego.

tooensure czy użytkowników lokalnych kont usługi AD są również chronione, należy tooensure który:

1.  Progu blokady konta usługi Azure AD jest _mniej_ niż próg blokady konta przez usługi AD. Firma Microsoft zaleca ustawienie wartości hello próg blokady konta przez usługi AD jest co najmniej dwie lub trzy razy progu blokady konta usługi Azure AD.
2.  Czas trwania blokady usługi Azure AD (reprezentowane w sekundach) jest _dłużej_ niż Directory resetowania konta blokady licznika po (reprezentowane w minutach).

## <a name="verify-your-ad-account-lockout-policies"></a>Sprawdź zasad blokady konta usługi AD

Użyj zasad blokady konta AD hello następujące instrukcje tooverify:

1.  Narzędzia do zarządzania zasadami grupy Otwórz hello.
2.  Edytuj hello zasady grupy zastosowane tooall użytkowników, na przykład hello domyślne zasady domeny.
3.  Przejdź tooComputer Konfiguracja komputera\Zasady\Ustawienia systemu Windows\Ustawienia zabezpieczeń\Zasady konta\Zasady blokady zasady.
4.  Sprawdź wartości progu blokady konta i zresetuj licznik blokady konta po.

![Zasady blokowania kont usługi AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>Użyj toomanage interfejsu API programu Graph hello wartości blokady inteligentnej Twojej dzierżawy

>[!IMPORTANT]
>Modyfikowanie progu blokady konta i czas trwania blokady wartości przy użyciu interfejsu API programu Graph usługi Azure AD to funkcja usługi Azure AD Premium P2. On również wymaga od Ciebie toobe administratora globalnego w dzierżawie.

Można użyć [Explorer wykres](https://developer.microsoft.com/graph/graph-explorer) tooread, ustaw i zaktualizuj wartości blokady inteligentnej usługi Azure AD. Jednak możesz również wykonać te operacje programowo.

### <a name="read-smart-lockout-values"></a>Inteligentne blokady odczytu wartości

Wykonaj te kroki tooread wartości blokady inteligentnej Twojej dzierżawy:

1. Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy. Jeśli zostanie wyświetlony monit, Udziel dostępu dla hello wymagane uprawnienia.
2. Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All" hello.
3. Żądania interfejsu API programu Graph hello należy skonfigurować następująco: Ustaw wersję zbyt "BETA", typ żądania zbyt "GET" i adresu URL za`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Kliknij przycisk "Uruchom kwerendę" toosee wartości blokady inteligentnej swojej dzierżawy. Jeśli nie zdefiniowano wartości Twojej dzierżawy przed, pojawi się pusty zestaw.

### <a name="set-smart-lockout-values"></a>Ustaw wartości inteligentne blokady

Wykonaj te kroki tooset wartości blokady inteligentnej Twojej dzierżawy (na powitania tylko po raz pierwszy):

1. Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy. Jeśli zostanie wyświetlony monit, Udziel dostępu dla hello wymagane uprawnienia.
2. Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All" hello.
3. Żądania interfejsu API programu Graph hello należy skonfigurować następująco: Ustaw wersję zbyt "BETA", typ żądania zbyt "POST" i adresu URL za`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Skopiuj i Wklej hello następujące żądania JSON w polu "Treści żądania" hello. Zmień wartości blokady inteligentnej hello zgodnie z potrzebami i użyj losowy identyfikator GUID dla `templateId`.
5. Kliknij przycisk "Uruchom kwerendę" tooset wartości blokady inteligentnej swojej dzierżawy.

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>Jeśli nie są używane, można pozostawić hello **BannedPasswordList** i **EnableBannedPasswordCheck** wartości jako pusty ("") i "false" odpowiednio.

Sprawdź, czy ma ustawiony prawidłowo przy użyciu wartości blokady inteligentnej Twojej dzierżawy [te kroki](#read-smart-lockout-values).

### <a name="update-smart-lockout-values"></a>Aby zaktualizować inteligentne blokady

Wartości blokady inteligentnej Twojej dzierżawy (jeśli zostały skonfigurowane je przed) wykonaj tooupdate te kroki:

1. Zaloguj się do Eksploratora wykresu jako Administrator globalny dzierżawy. Jeśli zostanie wyświetlony monit, Udziel dostępu dla hello wymagane uprawnienia.
2. Kliknij polecenie "Modyfikuj uprawnienia" i wybierz uprawnienie "Directory.ReadWrite.All" hello.
3. [Wykonaj te kroki tooread Twojej dzierżawy blokady inteligentnej wartości](#read-smart-lockout-values). Kopiuj hello `id` wartość (GUID) elementu hello o nazwie "wyświetlanej" jako "PasswordRuleSettings".
4. Skonfiguruj hello żądania interfejsu API programu Graph w następujący sposób: Ustaw wersję za "BETA" typ żądania za "Poprawka" i adresu URL za`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -Użyj hello identyfikatora GUID z kroku 3 dla `<id>`.
5. Skopiuj i Wklej hello następujące żądania JSON w polu "Treści żądania" hello. Zmień wartości blokady inteligentnej hello zależnie od potrzeb.
6. Kliknij przycisk "Uruchom kwerendę" tooupdate wartości blokady inteligentnej swojej dzierżawy.

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

Sprawdź zaktualizowano poprawnie przy użyciu wartości blokady inteligentnej Twojej dzierżawy [te kroki](#read-smart-lockout-values).

## <a name="next-steps"></a>Następne kroki
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
