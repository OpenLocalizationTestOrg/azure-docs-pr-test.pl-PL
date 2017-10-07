---
title: "aaaRestrict zawartości Azure CDN według kraju | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toorestrict dostępu tooyour Azure CDN zawartości przy użyciu funkcji filtrowania Geo."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>Ogranicz zawartość sieci Azure CDN według kraju

## <a name="overview"></a>Omówienie
Gdy użytkownik zażąda zawartości, domyślnie, niezależnie od tego, w którym użytkownik hello wprowadzone tego żądania z obsługiwanej hello zawartości. W niektórych przypadkach może być toorestrict dostęp do tooyour zawartości według kraju. W tym temacie opisano sposób toouse hello **filtrowania geograficznie** funkcji w kolejności tooconfigure hello tooallow lub blokowanie dostępu do usługi według kraju.

> [!IMPORTANT]
> produkty Verizon i Akamai Hello Podaj hello tę samą funkcjonalność filtrowania geograficznie, ale ma niewielkie różnice w te numerów kierunkowych obsługują. Zobacz krok 3 różnic toohello łącza.


Informacje o kwestiach dotyczących tooconfiguring takiego ograniczenia, temacie hello [zagadnienia dotyczące](cdn-restrict-access-by-country.md#considerations) sekcji na końcu hello hello tematu.  

![Filtrowanie kraju](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>Krok 1: Definiowanie hello ścieżki katalogu
Wybierz punkt końcowy w portalu hello i znaleźć hello filtrowania geograficznie na karcie toofind nawigacji po lewej stronie powitania tę funkcję.

Konfigurując filtr kraju, należy określić hello ścieżki względnej toohello lokalizacji toowhich użytkowników ma być dozwolony lub zabroniony dostęp. Filtrowanie geograficznie można stosować dla wszystkich plików z "/" lub wybrane foldery, określając ścieżki katalogu "/ obrazy /". Można także zastosować filtrowanie geograficznie tooa pojedynczy plik przez określenie pliku hello i pomijając hello ukośnika "/ zdjęcia/miasto.png".

Przykładowy filtr ścieżki katalogu:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>Krok 2: Definiowanie akcji hello: blokowanie lub zezwalanie na
**Zablokuj:** użytkownikom hello określony krajów będą odrzucane tooassets dostępu zażąda tej ścieżki cyklicznego. Jeśli inne opcje filtrowania kraju zostały skonfigurowane dla tej lokalizacji, następnie wszyscy inni użytkownicy będą mieć dostęp.

**Zezwalaj na:** tylko użytkownicy z hello określony krajów może być tooassets dostępu zażąda tej ścieżki cyklicznego.

## <a name="step-3-define-hello-countries"></a>Krok 3: Definiowanie hello krajach
Wybierz krajach hello mają tooblock, lub zezwolić hello ścieżki. 

Na przykład hello reguły blokowania /Photos/Strasburgu/będzie filtrować pliki w tym:

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>Kod kraju
Witaj **filtrowania geograficznie** funkcja używa kraju kodów toodefine hello krajach z których będą dozwolone lub zablokowane żądania dla zabezpieczonych katalogu. Można znaleźć hello numerów kierunkowych w [Azure CDN numerów kierunkowych](https://msdn.microsoft.com/library/mt761717.aspx). 

## <a id="considerations"></a>Zagadnienia dotyczące
* Może potrwać too90 minut Verizon lub kilka minut z Akamai, zmiany tooyour kraju filtrowania konfiguracji tootake efektu.
* Ta funkcja nie obsługuje symboli wieloznacznych (na przykład "*").
* skojarzony ze ścieżką względną hello konfiguracji filtrowania geograficznie Hello będzie stosowane rekursywnie toothat ścieżki.
* Tylko jedna reguła może być zastosowane toohello tej samej ścieżce względnej (nie można utworzyć wiele filtrów kraju toohello tego punktu tej samej ścieżce względnej. Jednak folder może mieć wiele filtrów kraju. Jest to powodu toohello cykliczne rodzaj filtry kraju. Innymi słowy podfolderze folderu wcześniej skonfigurowane można przypisać filtru innego kraju.

