---
title: "Azure Active Directory B2C: Siedziby dostępności & dane regionu | Dokumentacja firmy Microsoft"
description: "Temat dotyczący hello typów dzierżaw usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a>Azure Active Directory B2C: Siedziby dostępności & dane regionu
Dostępność w danym regionie i siedziby danych są dwa bardzo różnych zagadnienia dotyczące inaczej tooAzure AD B2C z resztą hello Azure. W tym artykule opisano hello różnice między te dwa pojęcia, a następnie porównaj sposobów ich zastosowania tooAzure i usługi Azure AD B2C.

## <a name="summary"></a>Podsumowanie
Usługa Azure AD B2C jest **ogólnie dostępna na całym świecie** z opcją hello **danych siedzibę w Stanach Zjednoczonych lub w Europie**.

## <a name="concepts"></a>Pojęcia
* **Dostępność w danym regionie** odwołuje się toowhere usługa jest dostępna do użycia.
* **Siedziby danych** odwołuje się toowhere użytkownika są przechowywane dane.

## <a name="region-availability"></a>Dostępność w danym regionie
Usługa Azure AD B2C jest dostępna na całym świecie za pośrednictwem hello Azure chmury publicznej. 

To różni się od modelu hello wykonaj większości innych usług platformy Azure, której połączenie z siedziby danych dostępności. Zawiera przykłady tego, w obu Azure [produktów dostępna w regionie](https://azure.microsoft.com/regions/services/) strony i hello [Kalkulator cen Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).

## <a name="data-residency"></a>Rezydencja danych
Usługa Azure AD B2C są przechowywane dane użytkownika w Stanach Zjednoczonych lub w Europie.

Siedziby danych jest określana według kraju/regionu, którego wybrano po [tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md).

![Zrzut ekranu przedstawiający dzierżawy w wersji zapoznawczej](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

Dane znajdują się w Stanach Zjednoczonych hello na powitania po krajów i regionów:

> Stany Zjednoczone, Kanada, Kostaryka, Republika Dominikańska, Salwador, Gwatemala, Meksyk, Panama, Portoryko i Trynidad

Dane znajdują się w Europie dla powitania po krajów i regionów:

> Algierii, Austrii, Azerbejdżanu, Bahrajn, Białorusi, Belgii, Bułgarii, Chorwacji, Cypru, Czechy, Dania, Egiptu, Estonii, Finlandia, Francja, Niemcy, Grecja, Węgierskiej, Islandii, Irlandii, Izrael, Włochy, Jordania, Kazachstanu, Kenii, Kuwejt, Lativa, Liban, Liechtenstein, Lituania, Luksemburg, Macedonia Była Jugosłowiańska Republika, m Alta, Czarnogóry, Maroka, Holandia, Nigerii, Norwegia, Oman, Pakistanu, Polski, Portugalia, Katar, Rumunii, Rosji, Arabia Saudyjska, Serbii, Słowacji, Słowenii, Republika Południowej Afryki, Hiszpanii, Szwecja, Szwajcarii, Tunezji, Turcja, Ukrainy, Zjednoczone Emiraty Arabskie i Zjednoczone Królestwo.

Hello pozostałych krajach znajdują się w proces hello dodawany toohello listy.  Obecnie można nadal używać usługi Azure AD B2C, wybierając żadnego hello krajach powyżej.

> Afganistanu, Argentyny, Australii, Brazylia, podrzędnej lokacji, Kolumbii, Ekwadoru, Hongkong SAR, Indie, Indonezji, Iraku, Japonii, Korei, Malezji, Nowa Zelandia, Paragwaju, Peru, Filipiny, Singapur, Sri Lanka, Tajwan, Tajlandii, Urugwaju i Wenezueli.

## <a name="preview-tenant"></a>Dzierżawy w wersji zapoznawczej
Jeśli dzierżawy B2C została utworzona w okresie wersji zapoznawczej usługi Azure AD B2C, istnieje duże prawdopodobieństwo, że Twoje **dzierżawy typu** mówi **dzierżawy w wersji zapoznawczej**. Jeśli przypadku hello tylko w przypadku projektowania i testowania, a nie dla aplikacji produkcyjnych możesz korzystać dzierżawy.

> [!IMPORTANT]
> Brak nie ścieżki migracji z dzierżawy B2C skali produkcji tooa dzierżawy B2C w wersji zapoznawczej. Należy pamiętać, że istnieją znane problemy po usunięciu dzierżawy B2C w wersji zapoznawczej i ponownie utwórz dzierżawy B2C produkcji skali z hello tą samą nazwą domeny. Masz toocreate dzierżawę B2C skali produkcji o nazwie innej domeny.


![Zrzut ekranu przedstawiający dzierżawy w wersji zapoznawczej](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
