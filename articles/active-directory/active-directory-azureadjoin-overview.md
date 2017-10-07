---
title: "aaaExtending chmury możliwości tooWindows 10 urządzeń za pomocą usługi Azure Active Directory Join | Dokumentacja firmy Microsoft"
description: "Zawiera szczegółowe omówienie sposobu urządzeń z systemem Windows 10 mogą korzystać z usługi Azure AD Join tooget zarejestrowany w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: db9ae9caeb3951d1fdd1d2477827012fd10ace60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="extending-cloud-capabilities-toowindows-10-devices-through-azure-active-directory-join"></a>Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join
## <a name="what-is-azure-active-directory-join"></a>Czym jest usługa Azure Active Directory Join?
Azure Active Directory Join (Azure AD Join) jest funkcją hello, który rejestruje urządzenia należące do firmy w usłudze Azure Active Directory tooenable scentralizowane zarządzanie urządzeniem hello. Umożliwia ono dla użytkowników, takich jak pracowników i studentów tooconnect toohello enterprise chmury za pomocą usługi Azure Active Directory. Dzięki temu uproszczonego wdrażania systemu Windows i dostęp tooorganizational aplikacje i zasoby na dowolnym urządzeniu z systemem Windows, zarówno firmowych i osobistych (BYOD).

Azure AD Join jest przeznaczony dla przedsiębiorstw, które są najpierw/chmury — tylko w chmurze — zwykle małych i średnich firm, które nie mają infrastruktury lokalnej usługi Active Directory systemu Windows Server. Wspomniane, Azure AD Join może i zostanie również posłużyć dużych organizacjach na urządzeniach, które mogą podczas przyłączania do domeny tradycyjnych (urządzeń przenośnych, na przykład), albo dla użytkowników wymagających głównie tooaccess usługi Office 365 lub innych aplikacji SaaS zintegrowanych z usługą Azure AD.

Przyłączanie do domeny tradycyjnych hello nadal oferuje hello lokalnego najlepsze środowisko na urządzeniach, które są w stanie przyłączania domeny, Azure AD Join jest odpowiednia dla urządzeń, które nie przyłączania do domeny. Azure AD Join jest również odpowiedniego do zarządzania użytkownikami w chmurze hello. Robi to przy użyciu możliwości zarządzania urządzeniami przenośnymi, a nie przy użyciu narzędzi zarządzania tradycyjnych domeny, takich jak zasady grupy i System Center Configuration Manager (SCCM).

![Przegląd urządzeń firmowych i osobistych urządzeń z lokalnej usługi Active Directory i Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Dlaczego przedsiębiorstwa powinna przyjąć Azure AD Join?
* **Firm, które znajdują się w dużej mierze hello chmury**: Jeśli zostały przeniesione lub przenosisz tooa modelu, w którym są zmniejszenie rozmiaru sieci lokalnej i chcesz toooperate więcej w chmurze hello Azure AD Join można korzyści. Może być konta usługi Azure AD został utworzony ręcznie lub za pośrednictwem synchronizacji lokalnej usługi Active Directory. W obu przypadkach musisz mieć konto w usłudze Azure AD i można go toosign w tooWindows 10. Użytkownicy mogą dołączać ich komputerów tooAzure AD za pomocą albo hello out-of-box experience (OOBE) lub z menu ustawień hello. Po dołączeniu, użytkownicy będą korzystać z jednego logowania jednokrotnego (SSO) dostępu toocloud zasobów, takich jak usługi Office 365 w przeglądarce lub w aplikacjach pakietu Office.
* **Instytucji edukacyjnych**: jednego ze scenariuszy hello Otrzymaliśmy o często jest instytucji edukacyjnych dwa typy użytkownika: pracowników i studentów. Elementy członkowskie nauczycieli lub wykładowców są traktowane jako długoterminowego członków organizacji hello, dlatego tworzenie lokalnych kont dla nich jest pożądane. Jednak studenci są shorter-term członków organizacji hello i w związku z tym można zarządzać w usłudze Azure AD. Oznacza to, może zostać umieszczony chmury toohello zamiast przechowywanego lokalnie katalog skali. Oznacza to również studentów może zarejestrować tooWindows z konta usługi Azure AD i uzyskać dostęp tooOffice 365 zasobów, w przeglądarce lub w aplikacjach pakietu Office.
* **W sieci sprzedaży firmy**: inny scenariusz otrzymujemy informacje od klientów jest łatwiej ich desire toomanage okresach pracowników.  Ponownie konta dla długoterminowego, pełnoetatowych pracowników są zwykle tworzone jako lokalnych kont na komputerach przyłączonych do domeny. Ale okresach pracowników należą shorter-term hello organizacji, dlatego jest pożądane toomanage ich gdzie licencji użytkownika można łatwo przenosić wokół. Tworzenie tych kont użytkowników w chmurze hello z licencjami usługi Office 365 umożliwia hello użytkowników tooget hello zalet podpisywania tooWindows i aplikacje pakietu Office przy użyciu konta usługi Azure AD. W tym samym czasie większą elastyczność z licencjami na ich zachowanie w sytuacji, po ich działania.
* **Innych firm**: mimo że obsługa użytkowników w lokalnej usługi Active Directory, możesz nadal skorzystać z użytkowników być przyłączony do usługi AD platformy Azure. Wynika to z usługi Azure AD oferuje uproszczone środowisko łącząca, zarządzanie urządzeniami wydajne, rejestracji zarządzania automatyczne urządzeń przenośnych i możliwość rejestracji jednokrotnej dla usługi Azure AD i zasobów lokalnych.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Jakie funkcje usługi Azure AD Join oferuje?
Z usługi Azure AD Join możesz uzyskać hello następujące czynności:

* **Własnym inicjowania obsługi urządzeń należących do firmy**: Z systemem Windows 10, użytkownicy mogą konfigurować urządzenia całkowicie nowe, porządnie zapakowane w hello out-of-box experience, bez udziału IT.
* **Obsługa nowoczesnego rozmiarach**: Azure AD Join działa na urządzeniach, które nie mają domeny tradycyjnych hello join możliwości.  
* **Obsługa istniejącego konta organizacyjne**: użytkownicy nie muszą toocreate i obsługa osobistych tooget konta Microsoft hello najlepsze środowisko na urządzeniach, wystawiony przez firmę, tak samo jak z systemem Windows 8. Ich użyć istniejącego konta służbowego w usłudze Azure AD. W przypadku wielu organizacji, oznacza to, zasadniczo użytkowników może skonfigurować i zarejestrować tooWindows z hello sam poświadczenia użycia tooaccess usługi Office 365.
* **Urządzenia przenośne automatycznego zarządzania rejestracji**: urządzenia mogą być automatycznie rejestrowane w zarządzania urządzeniami przenośnymi w przypadku połączenia tooAzure AD. Ten proces działa z rozwiązaniami do zarządzania urządzeniami przenośnymi Intune firmy Microsoft i jej partnerów. Zarządzanie urządzeniami odbywa się przy użyciu usługi Intune, Administratorzy IT mogą monitor/zarządzać Azure urządzeń przyłączonych do usługi AD obok urządzeń przyłączonych do domeny w konsoli zarządzania programu SCCM hello.
* **Pojedynczy zasobów logowania jednokrotnego toocompany**: użytkownicy korzystali rejestracji jednokrotnej z tooapps pulpitu systemu Windows hello i zasobów w chmurze hello, takie jak usługi Office 365 i tysiące aplikacji biznesowych, które zależą od usługi Azure AD do uwierzytelniania za pośrednictwem [Programu azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Firmowe urządzenia, które są przyłączone do tooAzure AD korzystają również zasoby lokalne tooon logowania jednokrotnego gdy urządzenia hello jest podłączony do sieci firmowej i z dowolnego miejsca, gdy te zasoby są dostępne za pośrednictwem hello [serwera Proxy aplikacji usługi Azure AD](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **Roaming stanu systemu operacyjnego**: ustawienia ułatwień dostępu, witryn sieci Web, sieci Wi-Fi hasła i inne ustawienia są synchronizowane między urządzeniami firmowymi bez konieczności osobistego konta Microsoft.
* **Sklep Windows gotowe Enterprise**: hello Sklepu Windows obsługuje nabycia aplikacji i licencji z konta usługi Azure AD. Organizacje mogą aplikacje licencji zbiorczej i były dostępne toohello użytkownicy w organizacji.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Jak działają różne urządzenia z usługi Azure AD Join
| Urządzenia firmowe (lokalnego tooon przyłączone do domeny) | Urządzenia firmowe (toohello połączonych w chmurze) | Urządzenie osobiste |
| --- | --- | --- |
| Użytkownicy mogą rejestrować w systemie Windows przy użyciu poświadczeń pracy (tak samo, jak obecnie). |Użytkownicy mogą się zalogować w tooWindows o poświadczenia służbowe, które są zarządzane w usłudze Azure AD. Jest to istotne dla firmowych urządzeń w trzech przypadkach: <ol><li>Witaj organizacja nie ma usługi Active Directory w miejscu (na przykład małych firmach).</li><li>Witaj organizacji nie tworzy wszystkich kont użytkowników w usłudze Active Directory (na przykład konta dla uczniów lub studentów, konsultantów lub pracowników okresach nie są tworzone w usłudze Active Directory).</li><li>Witaj organizacja ma firmowych urządzeń, które nie mogą być przyłączone do tooan (lokalnego) domeny, takich jak telefony i tablety z systemem Mobile jednostki SKU (na przykład urządzenie pomocnicze podjęte tooa detalicznych fabryki piętra).</li></ol> Azure AD Join obsługuje dołączanie urządzeń firmowych dla organizacji, zarządzane i federacyjnych. |Logowania tooWindows z ich osobistych poświadczeń konta Microsoft (bez zmian). |
| Użytkownicy mają dostęp tooroaming ustawienia i enterprise hello Sklepu Windows. Te usługi pracować z konta służbowego i nie wymagają osobistego konta Microsoft. Wymaga to tooconnect organizacje ich lokalnej usługi Active Directory tooAzure AD. |Użytkownicy mogą wykonywać samoobsługi Instalatora. Mogą one za pośrednictwem hello pierwszego uruchomienia (FRX) za pomocą konta służbowego jako alternatywne toohaving IT zainicjować obsługę administracyjną urządzeń hello, obie metody są obsługiwane. |Użytkownicy mogą łatwo dodawać konta służbowego, który jest zarządzany w usłudze Active Directory lub Azure AD. |
| Użytkownicy mają możliwość rejestracji Jednokrotnej z hello pulpitu toowork aplikacji, witryn sieci Web i zasobów — w tym zarówno lokalnie, jak i aplikacje w chmurze, które używają usługi Azure AD do uwierzytelniania. |Urządzenia są automatycznie rejestrowane w katalogu organizacji hello (Azure AD) i automatycznie rejestrowane w zarządzaniu urządzeniami przenośnymi. (Funkcja usługi azure AD Premium). |Użytkownicy mają możliwość logowania jednokrotnego w aplikacjach i toowebsites/zasoby z tym kontem służbowym. |
| Użytkownicy mogą dodawać ich osobistych tooaccess kont Microsoft ich własnych obrazów i plików bez wpływu na dane przedsiębiorstwa. (Roaming ustawień nadal toowork z konta służbowego). Hello konto Microsoft umożliwia logowanie Jednokrotne i nie jest już dyski hello roaming ustawień. |Użytkownicy mogą wykonywać samoobsługowego resetowania hasła (SSPR) na usługi winlogon, co oznacza, że ich zresetować zapomniane hasło. (Funkcja usługi azure AD Premium). |Użytkownicy mają Sklepu Windows enterprise toohello dostępu, dzięki czemu mogą uzyskać i korzystanie z aplikacji — biznesowych na ich osobistych urządzeniach. |

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

