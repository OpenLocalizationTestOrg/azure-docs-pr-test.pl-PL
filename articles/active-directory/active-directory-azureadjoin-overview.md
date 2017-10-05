---
title: "Rozszerzanie funkcji chmury na urządzeniach z systemem Windows 10 za pomocą usługi Azure Active Directory Join | Dokumentacja firmy Microsoft"
description: "Zawiera szczegółowe omówienie sposobu urządzeń z systemem Windows 10 mogą korzystać z usługi Azure AD Join Aby zarejestrować się w usłudze Azure Active Directory."
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
ms.openlocfilehash: d3a3d3efe1c43caff3b8d2956c14e8c90d05d22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="extending-cloud-capabilities-to-windows-10-devices-through-azure-active-directory-join"></a>Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join
## <a name="what-is-azure-active-directory-join"></a>Czym jest usługa Azure Active Directory Join?
Azure Active Directory Join (Azure AD Join) jest funkcją, która rejestruje urządzenia należące do firmy w usłudze Azure Active Directory umożliwia scentralizowane zarządzanie urządzeniem. Umożliwia ono dla użytkowników, takich jak pracowników i studentów do nawiązania połączenia chmury przedsiębiorstwa za pomocą usługi Azure Active Directory. Dzięki temu uproszczonego wdrażania systemu Windows i dostęp do zasobów i aplikacji organizacji z dowolnego urządzenia z systemem Windows, zarówno firmowych i osobistych (BYOD).

Azure AD Join jest przeznaczony dla przedsiębiorstw, które są najpierw/chmury — tylko w chmurze — zwykle małych i średnich firm, które nie mają infrastruktury lokalnej usługi Active Directory systemu Windows Server. Inaczej mówiąc, Azure AD Join i zostanie również być używane przez dużych organizacjach na urządzeniach, które mogą podczas przyłączania do domeny tradycyjnych (urządzeń przenośnych, na przykład) lub dla użytkowników wymagających przede wszystkim do dostępu do usługi Office 365 lub innych SaaS aplikacji zintegrowane z usługą Azure AD.

Mimo że przyłączania do domeny tradycyjnych nadal oferuje najlepsze lokalną wystąpić na urządzeniach, które są w stanie przyłączania domeny, Azure AD Join jest odpowiednia dla urządzeń, które nie przyłączania do domeny. Azure AD Join jest również odpowiedniego do zarządzania użytkownikami w chmurze. Robi to przy użyciu możliwości zarządzania urządzeniami przenośnymi, a nie przy użyciu narzędzi zarządzania tradycyjnych domeny, takich jak zasady grupy i System Center Configuration Manager (SCCM).

![Przegląd urządzeń firmowych i osobistych urządzeń z lokalnej usługi Active Directory i Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a>Dlaczego przedsiębiorstwa powinna przyjąć Azure AD Join?
* **Firm, które znajdują się głównie w chmurze**: Jeśli zostały przeniesione lub przechodzenia do modelu, w którym są zmniejszenie rozmiaru sieci lokalnej i chcesz działać więcej w chmurze Azure AD Join można korzyści. Może być konta usługi Azure AD został utworzony ręcznie lub za pośrednictwem synchronizacji lokalnej usługi Active Directory. W obu przypadkach musisz mieć konto w usłudze Azure AD i służy do logowania do systemu Windows 10. Użytkownicy może dołączać swoje komputery z usługą Azure AD za pomocą obu out-of-box experience (OOBE) lub z menu ustawień. Po dołączeniu, użytkownicy będą korzystać z jednego logowania jednokrotnego (SSO) dostęp do zasobów w chmurze jak usługi Office 365 w przeglądarce lub w aplikacjach pakietu Office.
* **Instytucji edukacyjnych**: jednego ze scenariuszy Otrzymaliśmy o często jest instytucji edukacyjnych dwa typy użytkownika: pracowników i studentów. Elementy członkowskie nauczycieli lub wykładowców są traktowane jako długoterminowego członków organizacji, dlatego tworzenie lokalnych kont dla nich jest pożądane. Jednak studenci są shorter-term członków organizacji i w związku z tym można zarządzać w usłudze Azure AD. Oznacza to, że katalog skali może zostać umieszczony w chmurze zamiast przechowywanego lokalnie. Oznacza to również studentów może Zaloguj się do systemu Windows za pomocą ich kont usługi Azure AD i uzyskać dostęp do zasobów usługi Office 365, w przeglądarce lub w aplikacjach pakietu Office.
* **W sieci sprzedaży firmy**: inny scenariusz otrzymujemy informacje od klientów jest ich chęć łatwiej zarządzać okresach pracowników.  Ponownie konta dla długoterminowego, pełnoetatowych pracowników są zwykle tworzone jako lokalnych kont na komputerach przyłączonych do domeny. Ale okresach pracowników shorter-term członków organizacji, więc jest konieczne zarządzanie nimi gdzie licencji użytkownika można łatwo przenosić wokół. Tworzenie tych kont użytkowników w chmurze za pomocą licencji usługi Office 365 umożliwia użytkownikom korzystania z zalet logowanie do systemu Windows i aplikacji pakietu Office przy użyciu konta usługi Azure AD. W tym samym czasie większą elastyczność z licencjami na ich zachowanie w sytuacji, po ich działania.
* **Innych firm**: mimo że obsługa użytkowników w lokalnej usługi Active Directory, możesz nadal skorzystać z użytkowników być przyłączony do usługi AD platformy Azure. Wynika to z usługi Azure AD oferuje uproszczone środowisko łącząca, zarządzanie urządzeniami wydajne, rejestracji zarządzania automatyczne urządzeń przenośnych i możliwość rejestracji jednokrotnej dla usługi Azure AD i zasobów lokalnych.  

## <a name="what-capabilities-does-azure-ad-join-offer"></a>Jakie funkcje usługi Azure AD Join oferuje?
Z usługi Azure AD Join można uzyskać następujące czynności:

* **Własnym inicjowania obsługi urządzeń należących do firmy**: Z systemem Windows 10, użytkownicy mogą konfigurować urządzenia całkowicie nowe, porządnie zapakowane w środowisko out-of-box bez udziału IT.
* **Obsługa nowoczesnego rozmiarach**: Azure AD Join działa na urządzeniach, które nie mają tradycyjnych domeny, Dołącz możliwości.  
* **Obsługa istniejącego konta organizacyjne**: użytkownicy nie muszą już tworzyć i obsługiwać osobistego konta Microsoft, aby uzyskać najlepsze środowisko na urządzeniach, wystawiony przez firmę, tak samo jak z systemem Windows 8. Ich użyć istniejącego konta służbowego w usłudze Azure AD. W przypadku wielu organizacji oznacza to, zasadniczo czy użytkownicy mogą skonfigurować i zaloguj się do systemu Windows za pomocą tych samych poświadczeń, które używają do dostępu do usługi Office 365.
* **Urządzenia przenośne automatycznego zarządzania rejestracji**: urządzenia mogą być automatycznie rejestrowane w zarządzania urządzeniami przenośnymi w przypadku połączenia z usługą Azure AD. Ten proces działa z rozwiązaniami do zarządzania urządzeniami przenośnymi Intune firmy Microsoft i jej partnerów. Zarządzanie urządzeniami odbywa się przy użyciu usługi Intune, Administratorzy IT mogą monitor/zarządzać Azure urządzeń przyłączonych do usługi AD obok urządzeń przyłączonych do domeny, w konsoli zarządzania programu SCCM.
* **Logowanie jednokrotne do zasobów firmy**: użytkownicy korzystali rejestracji jednokrotnej z pulpitu systemu Windows do aplikacji i zasobów w chmurze, takich jak usługi Office 365 i tysiące aplikacji biznesowych, które zależą od usługi Azure AD do uwierzytelniania za pośrednictwem [ Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md). Urządzenia należące do firmy, które dołączyły do usługi Azure AD mają również logowania jednokrotnego do zasobów lokalnych, gdy urządzenie jest w sieci firmowej i z dowolnego miejsca, jeśli te zasoby są udostępniane za pośrednictwem funkcji [serwera Proxy aplikacji usługi Azure AD](https://msdn.microsoft.com/library/azure/Dn768219.aspx).
* **Roaming stanu systemu operacyjnego**: ustawienia ułatwień dostępu, witryn sieci Web, sieci Wi-Fi hasła i inne ustawienia są synchronizowane między urządzeniami firmowymi bez konieczności osobistego konta Microsoft.
* **Sklep Windows gotowe Enterprise**: W Sklepie Windows obsługuje nabycia aplikacji i licencji z konta usługi Azure AD. Organizacje mogą aplikacje licencji zbiorczej i udostępnić je użytkownikom w organizacji.

## <a name="how-do-different-devices-work-with-azure-ad-join"></a>Jak działają różne urządzenia z usługi Azure AD Join
| Urządzenia firmowe (przyłączony do domeny lokalnej) | Urządzenia firmowe (połączone w chmurze) | Urządzenie osobiste |
| --- | --- | --- |
| Użytkownicy mogą rejestrować w systemie Windows przy użyciu poświadczeń pracy (tak samo, jak obecnie). |Użytkownicy mogą Zaloguj się do systemu Windows z poświadczenia służbowe, które są zarządzane w usłudze Azure AD. Jest to istotne dla firmowych urządzeń w trzech przypadkach: <ol><li>Organizacja nie ma usługi Active Directory w miejscu (na przykład małych firmach).</li><li>Organizacja nie tworzy wszystkich kont użytkowników w usłudze Active Directory (na przykład konta dla uczniów lub studentów, konsultantów lub pracowników okresach nie są tworzone w usłudze Active Directory).</li><li>Organizacja ma firmowych urządzeń, których nie można przyłączyć do domeny (lokalnego), takich jak telefony i tablety z systemem Mobile jednostki SKU (na przykład urządzenia dodatkowego podjąć w celu floor fabryki detalicznych).</li></ol> Azure AD Join obsługuje dołączanie urządzeń firmowych dla organizacji, zarządzane i federacyjnych. |Logowania się do systemu Windows przy użyciu poświadczeń konta Microsoft osobiste (bez zmian). |
| Użytkownicy mają dostęp do ustawień roamingu i enterprise Sklepu Windows. Te usługi pracować z konta służbowego i nie wymagają osobistego konta Microsoft. Wymaga to organizacjom łączenia ich usługi lokalnej Active Directory do usługi Azure AD. |Użytkownicy mogą wykonywać samoobsługi Instalatora. Mogą one za pośrednictwem pierwszego uruchomienia komputera (FRX) za pomocą konta służbowego alternatywą wobec których świadczenie IT urządzeń, mimo że obie metody są obsługiwane. |Użytkownicy mogą łatwo dodawać konta służbowego, który jest zarządzany w usłudze Active Directory lub Azure AD. |
| Użytkownicy mieli możliwości logowania jednokrotnego z pulpitu pracy aplikacji, witryn sieci Web i zasobów — w tym zarówno lokalnie, jak i aplikacje w chmurze, które używają usługi Azure AD do uwierzytelniania. |Urządzenia są automatycznie rejestrowane w katalogu organizacji (Azure AD) i automatycznie rejestrowane w zarządzaniu urządzeniami przenośnymi. (Funkcja usługi azure AD Premium). |Użytkownicy mają możliwość logowania jednokrotnego w aplikacjach i witryn sieci Web/zasobów z tym kontem służbowym. |
| Użytkownicy mogą dodawać ich osobistych kont Microsoft na dostęp do swoich własnych obrazów i plików bez wpływu na dane przedsiębiorstwa. (Roaming ustawień kontynuować pracę z konta służbowego.) Konto Microsoft umożliwia logowania jednokrotnego i nie jest już dyski, roaming ustawień. |Użytkownicy mogą wykonywać samoobsługowego resetowania hasła (SSPR) na usługi winlogon, co oznacza, że ich zresetować zapomniane hasło. (Funkcja usługi azure AD Premium). |Użytkownicy mają dostęp do przedsiębiorstwa Sklepu Windows, dzięki czemu mogą uzyskać i korzystanie z aplikacji — biznesowych na urządzeniach osobistych. |

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

