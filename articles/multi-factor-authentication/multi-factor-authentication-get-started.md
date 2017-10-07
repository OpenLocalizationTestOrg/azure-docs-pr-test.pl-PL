---
title: "aaaChoose między chmury Azure MFA lub serwera | Dokumentacja firmy Microsoft"
description: "Wybieranie hello uwierzytelnianie wieloskładnikowe zabezpieczeń rozwiązania, które jest odpowiednie dla Ciebie pytając, jakie am I próby toosecure oraz gdy są Moi użytkownicy znajdujący się.  Następnie wybierz chmurę lub serwer usługi MFA albo usługi AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Wybierz hello Azure Multi-Factor Authentication rozwiązania
Ponieważ istnieje kilka odmian systemu Azure Multi-Factor Authentication (MFA), firma Microsoft musi odpowiedzieć w kilku toofigure pytania używaną wersję jest hello prawidłowego toouse jeden.  Oto te pytania:

* [Co mam próby toosecure](#what-am-i-trying-to-secure)
* [Gdzie znajdują się użytkownicy hello](#where-are-the-users-located)
* [Jakich funkcji potrzebujesz?](#what-featured-do-i-need)

Witaj poniższe sekcje zawierają wskazówki na temat określania każdego z tych odpowiedzi.

## <a name="what-am-i-trying-toosecure"></a>Co mam próby toosecure?
rozwiązanie weryfikacji dwuetapowej poprawne hello toodetermine, najpierw możemy musi odpowiedzieć hello pytanie, jakie są w trakcie toosecure za pomocą drugiego metody uwierzytelniania.  Czy jest to aplikacja na platformie Azure?  Czy może system z dostępem zdalnym?  Przez określenie, jakie próbujemy toosecure, firma Microsoft pozwala uzyskać odpowiedzi na pytanie hello, którym usługa Multi-Factor Authentication musi toobe włączone.  

| Co to są w trakcie toosecure | Uwierzytelniania MFA w chmurze hello | Serwer MFA |
| --- |:---:|:---:|
| Aplikacje firmy Microsoft |● |● |
| Aplikacji SaaS w galerii aplikacji hello |● |  |
| Aplikacje sieci Web opublikowane za pośrednictwem serwera proxy aplikacji usługi Azure AD |● |  |
| Aplikacje usług IIS, które nie zostały opublikowane za pośrednictwem serwera proxy aplikacji usługi Azure AD | |● |
| Dostęp zdalny, np. sieć VPN lub brama usług pulpitu zdalnego | ● | ● |

## <a name="where-are-hello-users-located"></a>Gdzie znajdują się użytkownicy hello
Następnie spojrzenie na którym znajdują się użytkownicy pomaga toodetermine hello właściwym rozwiązaniem toouse, czy w chmurze hello lub lokalnie za pomocą hello serwera usługi MFA.

| Lokalizacja użytkowników | Uwierzytelniania MFA w chmurze hello | Serwer MFA |
| --- |:---:|:---:|
| Usługa Azure Active Directory |● | |
| Usługa Azure AD i lokalna usługa AD przy użyciu federacji z usługami AD FS |● |● |
| Usługa Azure AD i lokalna usługa AD używana z narzędziem DirSync, Azure AD Sync, Azure AD Connect — brak synchronizacji haseł |● |● |
| Usługa Azure AD i lokalna usługa AD używana z narzędziem DirSync, Azure AD Sync, Azure AD Connect — z synchronizacją haseł |● | |
| Lokalna usługa Active Directory | |● |

## <a name="what-features-do-i-need"></a>Jakich funkcji potrzebujesz?
Witaj poniższej tabeli porównano funkcje hello, które są dostępne z usługi Multi-Factor Authentication w chmurze hello i powitania serwera Multi-Factor Authentication.

| Funkcja | Uwierzytelniania MFA w chmurze hello | Serwer MFA |
| --- |:---:|:---:|
| Powiadomienie w aplikacji mobilnej jako drugi składnik | ● | ● |
| Kod weryfikacyjny w aplikacji mobilnej jako drugi składnik | ● | ● |
| Połączenie telefoniczne jako drugi składnik | ● | ● |
| Jednokierunkowa wiadomość SMS jako drugi składnik | ● | ● |
| Dwukierunkowa wiadomość SMS jako drugi składnik | | ● |
| Tokeny sprzętowe jako drugi składnik | | ● |
| Hasła aplikacji dla usługi w przypadku klientów usługi Office 365, którzy nie obsługują usługi MFA | ● | |
| Kontrola administracyjna nad metodami uwierzytelniania | ● | ● |
| Tryb numeru PIN | | ● |
| Alert dotyczący wykrycia oszustwa |● | ● |
| Raporty usługi MFA |● | ● |
| Jednorazowe obejście | | ● |
| Niestandardowe powitania dla połączeń telefonicznych | ● | ● |
| Możliwość dostosowania identyfikacji numeru dla połączeń telefonicznych | ● | ● |
| Zaufane adresy IP | ● | ● |
| Pamiętanie uwierzytelniania MFA w przypadku zaufanych urządzeń | ● | |
| Dostęp warunkowy | ● | ● |
| Pamięć podręczna |  | ● |

## <a name="next-steps"></a>Następne kroki

Teraz, Ustaliliśmy, czy toouse w chmurze usługi Multi-Factor authentication lub powitania serwera usługi MFA lokalnie, firma Microsoft może rozpocząć konfigurowania i korzystania z usługi Azure Multi-Factor Authentication. **Wybierz ikonę hello danego scenariusza**

<center>




[![Chmura](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Serwer](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  </center>
