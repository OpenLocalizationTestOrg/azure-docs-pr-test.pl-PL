---
title: "aaaBranding wytyczne dotyczące aplikacji | Dokumentacja firmy Microsoft"
description: "Zaawansowane przewodnik dotyczący toodeveloper zasobów dla usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 72f4e464-1352-4a49-a18f-c37f58e7d5c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: e43f884c736a0dcb2e6e51293962ef1e2636ad70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="branding-guidelines-for-applications"></a>Znakowania wytyczne dotyczące aplikacji
W tym temacie omówiono hello znakowania wskazówki, które powinny być używane podczas tworzenia aplikacji w usłudze Azure Active Directory (Azure AD). Te wskazówki pomogą, bezpośrednie klientów podczas toouse służbowym lub konta służbowego, zarządzane w usłudze Azure AD lub konta prywatnego tooyour rejestracji i logowania w aplikacji.

## <a name="personal-accounts-vs-work-or-school-accounts-from-microsoft"></a>Kont osobistych a pracy lub szkoły kont firmy Microsoft
Firma Microsoft zarządza dwa rodzaje kont użytkowników:

* **Konta osobiste** (znanego wcześniej jako identyfikator Windows Live ID). Te konta reprezentować hello relację między *poszczególnych* użytkowników i firmy Microsoft i są używane tooaccess urządzeń konsumenckich i usług firmy Microsoft. Te konta są przeznaczone do użytku osobistego.
* **Konta służbowe.** Te konta są zarządzane przez firmę Microsoft w imieniu organizacji, które używają usługi Azure Active Directory. Te konta są używane toosign tooOffice 365 i innych usług biznesowych firmy Microsoft.

Konta służbowe są zazwyczaj Microsoft przypisał organizacji (firmy, szkoły, agencji rządowych Stanów Zjednoczonych) użytkownicy tooend (pracowników, studentów, pracowników federalnych). Te konta są albo zarządzany bezpośrednio w chmurze hello, platforma hello Azure AD lub zsynchronizowanej tooAzure AD z katalogiem lokalnym, takie jak Windows Server Active Directory. Firma Microsoft dokłada hello *niejawnego* pracy hello lub kont służbowych, ale hello konta są własnością i kontrolowane przez organizację hello.

## <a name="referring-tooazure-ad-accounts-in-your-application"></a>Odwołuje się do innych kont tooAzure AD w aplikacji
Microsoft nie zapewnia toohello użytkownicy końcowi Azure lub hello usługi Active Directory firmowe i nie należy użytkownik.

* Po zalogowaniu użytkownicy należy używać nazwy i logo możliwie hello organizacji. To jest lepsze niż ogólny warunków, takich jak "organizacja".
* Gdy użytkownicy nie są zalogowani, należy zapoznać się kont tootheir jako "pracy lub kont służbowych" i użyj hello Microsoft logo tooconvey że te konta są zarządzane przez firmę Microsoft. Nie używaj warunków takich jak "enterprise konto", "konto firmowe" lub "konto firmowe", co spowoduje utworzenie użytkownika pomyłek.

## <a name="user-account-pictogram"></a>Piktogram konta użytkownika
We wcześniejszej wersji z tymi wytycznymi zaleca się przy użyciu piktogramu "badge niebieski". Na podstawie opinii użytkowników i deweloperów, teraz zalecamy użycie hello logo firmy Microsoft hello zamiast tego. Ułatwi to użytkownikom zrozumienie, że ich ponowne użycie hello konto, które korzystają z usługi Office 365 lub innych toosign usług biznesowych firmy Microsoft w tooyour aplikacji.

## <a name="signing-up-and-signing-in-with-azure-ad"></a>Rejestracji i logowania przy użyciu usługi Azure AD
Aplikacja może stanowić oddzielne ścieżki rejestracji i logowania i hello następujące sekcje zawierają visual wskazówki dotyczące oba scenariusze.

**Jeśli aplikacja obsługuje logowania użytkownika końcowego (np. wolne tootrial lub freemium model)**: można wyświetlić **logowania** przycisku, który umożliwia użytkownikom tooaccess aplikacji za pomocą konta służbowego lub osobistego konta. Usługi Azure AD zostaną wyświetlone po raz pierwszy będą uzyskiwać dostęp do aplikacji hello monitu o zgodę.

**Jeśli aplikacja wymaga uprawnień, które tylko administratorzy mogą wyrazić zgodę na, czy aplikacja wymaga licencjonowania w organizacji**: należy oddzielić nabycia administratora z logowaniem użytkownika. Witaj **przycisk "Pobierz tę aplikację"** będzie przekierowywać toosign Administratorzy w następnie poproś zgody toogrant w imieniu użytkowników w organizacji. Ma to hello zaletę, że użytkownicy końcowi zgody monity tooyour aplikacji z pominięciem.

## <a name="visual-guidance-for-app-acquisition"></a>Visual wskazówki dotyczące pozyskiwania aplikacji
Łącze "get aplikacji hello" należy kierować hello użytkownika toohello usługi Azure AD Udziel dostępu (autoryzować) strony, tooallow tooauthorize administratora organizacji toohave Twojej aplikacji dostęp do danych tootheir organizacji, która jest hostowana przez firmę Microsoft. Szczegóły dotyczące sposobu dostępu toorequest zostały omówione w hello [integracji aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md) artykułu.

Po Administratorzy zgody tooyour aplikacji, mogą wybrać tooadd go środowisko uruchamiania aplikacji usługi Office 365 użytkowników tootheir (dostępny z hello waffle i [https://portal.office.com/myapps](https://portal.office.com/myapps)). Jeśli chcesz tooadvertise tej funkcji, można użyć warunków, takich jak "Dodaj tej organizacji tooyour aplikacji" Pokaż przycisk następująco:

![Typy aplikacji i scenariusze](./media/active-directory-branding-guidelines/add-to-my-org.png)

Jednak zaleca się, czy zapisać tekst objaśnienia zamiast polegania na przyciskach. Na przykład:

> *Jeśli już używasz usługi Office 365 lub innych usług biznesowych firmy Microsoft, po prostu można przyznać < your_app_name > dostępu tooyour danych organizacji. Pozwoli to tooaccess Twojego użytkowników < your_app_name > z istniejącego konta służbowego.*
> 
> 

## <a name="visual-guidance-for-sign-in"></a>Visual dotyczące logowania
Aplikacji znak powinien być wyświetlany na przycisku, który przekierowuje użytkowników toohello logowania punktu końcowego, który odpowiada protokołu toohello Użyj toointegrate z usługą Azure AD. powitania po sekcja zawiera szczegółowe informacje na co ten przycisk powinien wyglądać następująco.

### <a name="pictogram-and-sign-in-with-microsoft"></a>Piktogram i "Zaloguj się przy użyciu Microsoft"
Tego skojarzenia hello hello logo firmy Microsoft i warunki "Logowania w with Microsoft" hello unikatowy sposób identyfikuje usługi Azure AD wśród innych dostawców tożsamości, który może obsługiwać aplikacji. Jeśli nie masz za mało miejsca na "Logowania w with Microsoft", jest ok tooshorten on zbyt "Zaloguj się".

![Typy aplikacji i scenariusze](./media/active-directory-branding-guidelines/sign-in-with-microsoft-light.png)

![Typy aplikacji i scenariusze](./media/active-directory-branding-guidelines/sign-in-light.png)

Umożliwia także schemat kolorów ciemny hello przycisków.

![Typy aplikacji i scenariusze](./media/active-directory-branding-guidelines/sign-in-with-microsoft-dark.png)

![Typy aplikacji i scenariusze](./media/active-directory-branding-guidelines/sign-in-dark.png)

## <a name="branding-dos-and-donts"></a>Znakowanie porady
**CZY** Użyj "konto służbowe" w połączeniu z "Logowania w with Microsoft" hello przycisk dodatkowe objaśnienia tooprovide toohelp użytkownicy końcowi rozpoznaje, czy mogą go używać. **Nie** używać inne postanowienia, takie jak "enterprise konto", "konto firmowe" lub "konta firmowego."

**Nie** Użyj "Office 365 identyfikator" lub "Azure". Usługi Office 365 jest również nazwa hello konsumenta produkt firmy Microsoft, które nie są używane do uwierzytelniania usługi Azure AD.

**Nie** alter hello logo firmy Microsoft.

**Nie** udostępnić użytkownikom końcowym toohello marek Azure lub usługi Active Directory. Ok jest jednak toouse te terminy deweloperów, specjalistów IT i administratorów.

## <a name="navigation-dos-and-donts"></a>Porady nawigacji
**CZY** umożliwiają użytkownikom toosign się i przełączanie tooanother konta użytkownika. Chociaż większość osób jednego konta osobistego od firmy Microsoft/Facebook/Google/Twitter, użytkownicy często są skojarzone z więcej niż jednej z organizacji. Obsługa wielu zalogowanych użytkowników będzie dostępna wkrótce.

