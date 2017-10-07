---
title: "aaaSupportability i wycofania przewodnik zasad dla systemu operacyjnego gościa Azure | Dokumentacja firmy Microsoft"
description: "Zawiera informacje o to, co będzie pomocy technicznej firmy Microsoft w zakresie toohello systemu operacyjnego gościa Azure używany przez usługi w chmurze."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Azure zasad obsługi i wycofania systemu operacyjnego gościa
informacje Hello na tej stronie dotyczą systemu operacyjnego gościa Azure toohello ([systemu operacyjnego gościa](cloud-services-guestos-update-matrix.md)) dla usługi w chmurze sieci web i proces roboczy ról (PaaS). Nie dotyczy maszyn tooVirtual (IaaS).

Firma Microsoft ma opublikowanej [zasady pomocy technicznej dla systemu operacyjnego gościa hello](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq). Strona Hello odczytywania opisuje teraz implementowania hello zasad.

zasada Hello jest

1. Firma Microsoft będzie obsługuje **co najmniej hello najnowsze dwóch rodzin hello systemu operacyjnego gościa**. Po wycofaniu rodzina klienci mają 12 miesięcy od hello oficjalnego wycofania Data tooupdate tooa nowszej obsługiwanych gościa rodziny systemów operacyjnych.
2. Firma Microsoft będzie obsługuje **hello co najmniej dwie wersje najnowsze hello obsługiwanych rodzin systemu operacyjnego gościa**.
3. Firma Microsoft będzie obsługuje **hello co najmniej dwóch najnowsze wersje hello Azure SDK**. Gdy wersja zestawu SDK jest wycofywany powitalne, klienci będą mieli 12 miesięcy od hello oficjalnego wycofania Data tooupdate tooa nowszej wersji.

W czasie więcej niż dwie grupy lub wersji może być obsługiwana. Oficjalna informacje pomocy technicznej systemu operacyjnego gościa będą wyświetlane na powitania [poszczególnych wersji systemu operacyjnego gościa Azure i zgodność pakietu SDK](cloud-services-guestos-update-matrix.md).

## <a name="when-a-guest-os-family-or-version-is-retired"></a>Po wycofaniu rodziny systemów operacyjnych gościa lub w wersji
Nowy system operacyjny gościa **rodziny** wprowadzono pewnego czasu po wydaniu hello oficjalnego nowej wersji systemu operacyjnego Windows Server hello. Zawsze wprowadzane nowej rodziny systemu operacyjnego gościa, Microsoft będzie wycofać hello najstarsze rodziny systemu operacyjnego gościa.

Nowy system operacyjny gościa **wersji** wprowadzono o co miesiąc tooincorporate hello MSRC najnowsze. Z powodu hello regularnych comiesięcznych aktualizacji wersja systemu operacyjnego gościa jest zazwyczaj wyłączona po 60 dniach od jego wersja. To działanie umożliwia zachowanie co najmniej dwie wersje systemu operacyjnego gościa, dla każdej rodziny, które są dostępne do użycia.

### <a name="process-during-a-guest-os-family-retirement"></a>Podczas wycofywania rodziny systemu operacyjnego gościa
Po ogłoszenia wycofania hello klienci mają okres 12 miesięcy "przejścia" hello starsze rodziny oficjalnie jest usuwane z usługi. Teraz przejście może zostać rozszerzona uznania hello firmy Microsoft. Aktualizacje zostaną opublikowane na powitania [poszczególnych wersji systemu operacyjnego gościa Azure i zgodność pakietu SDK](cloud-services-guestos-update-matrix.md).

Proces stopniowego wycofania rozpocznie sześciu (6) miesięcy w okresie przejściowym hello. W tym czasie:

1. Firma Microsoft będzie wysyłać klientom Witaj wycofania.
2. nowsza wersja Hello hello Azure SDK nie obsługuje rodziny systemów operacyjnych gościa hello wycofane.
3. Nowych wdrożeń i redeployments usługi w chmurze nie będą mogły rodziny hello wycofane

Firma Microsoft będzie toointroduce zawierających najnowsze aktualizacje MSRC hello do hello ostatni dzień okresu przejściowego hello, nazywany "Data wygaśnięcia" hello nowej wersji systemu operacyjnego gościa. Na powitania datę wygaśnięcia będą obsługiwane usługi w chmurze nadal działa w obszarze hello umowy SLA platformy Azure. Firma Microsoft ma hello uznania tooforce uaktualnienia, usuń lub Zatrzymaj usługi po tym dniu.

### <a name="process-during-a-guest-os-version-retirement"></a>Podczas wycofywania wersji systemu operacyjnego gościa
Jeśli klienci ich aktualizacji tooautomatically systemu operacyjnego gościa, nie są nigdy tooworry dotyczące wersji systemu operacyjnego gościa. Mogą zawsze używać najnowszej wersji systemu operacyjnego gościa hello.

Wersje systemu operacyjnego gościa są wydawane co miesiąc. Ze względu na częstotliwość hello regularne wersji każda wersja ma stały czas działania.

W ciągu 60 dni do czasu działania hello, wersji, która jest "*wyłączone*". "Wyłączone" oznacza, że ta wersja hello zostanie usunięte z portalu hello. Nie można ustawić Hello wersji z pliku konfiguracji CSCFG hello. Istniejące wdrożenia pozostają uruchomione. Jednak nowych wdrożeń i kod i Konfiguracja wdrożenia tooexisting aktualizacje nie będą dozwolone.

Wersja systemu operacyjnego gościa hello pewien czas po przekształceniu "wyłączone", "*wygasa*" i życie uaktualniony i ustaw tooautomatically hello aktualizacji systemu operacyjnego gościa w hello przyszłych są wszystkie instalacje nadal działa w tej wersji. Wygaśnięcie odbywa się w partiach tak terminie powitania od tooexpiration niepełnosprawność może się różnić.

Okresy te mogą wydłużać na przejścia klienta tooease uznania firmy Microsoft. Wszelkie zmiany zostaną przekazane na powitania [poszczególnych wersji systemu operacyjnego gościa Azure i zgodność pakietu SDK](cloud-services-guestos-update-matrix.md).

### <a name="notifications-during-retirement"></a>Powiadomienia podczas wycofywania
* **Wycofanie rodziny** <br>Firma Microsoft będzie używać blogach i powiadomieniu portalu. Klienci, którzy nadal używają wycofane rodziny systemu operacyjnego gościa zostanie powiadomiony przez administratorów usługi tooassigned bezpośrednia komunikacja (poczty e-mail, wiadomości portalu, połączenie telefoniczne). Wszystkie zmiany zostaną opublikowane toothis strony i hello źródło danych RSS wymienione na początku hello tej strony.
* **Wycofywania wersji** <br>Wszystkie zmiany i daty hello występowania zostaną opublikowane toothis strony i hello źródło danych RSS wymienione na początku tej strony, w tym wersja, wyłączona i wygaśnięcia hello. Administratorzy usług będziesz otrzymywać wiadomości e-mail, jeśli mają wdrożeń uruchomionych na wyłączone wersji systemu operacyjnego gościa lub rodziny. czas Hello te wiadomości e-mail mogą się różnić. Zazwyczaj są co najmniej miesiąc przed inwalidztwo, chociaż ten czas nie jest oficjalną umowy SLA.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
**Jak można ograniczyć wpływ na powitania migracji?**

Zalecane jest użycie najnowszej rodziny systemów operacyjnych gościa za projektowanie usługi w chmurze.

1. Rozpocznij, wczesne planowanie rodziny nowszej tooa migracji.
2. Konfigurowanie tymczasowego testu tootest wdrożenia usługi w chmurze systemem hello nowej rodziny.
3. Ustawianie wersji systemu operacyjnego gościa za**automatyczne** (osVersion = * w hello [.cscfg](cloud-services-model-and-package.md#cscfg) pliku), wersji systemu operacyjnego gościa toonew migracji hello odbywa się automatycznie.

**Co zrobić, jeśli Moja aplikacja sieci web wymaga lepsza integracja z hello systemu operacyjnego?**

Jeśli architektury aplikacji sieci web jest zależny od funkcji systemu operacyjnego hello, użyj platformy obsługiwane funkcje takie jak [uruchamiania zadań](cloud-services-startup-tasks.md) lub innych mechanizmów rozszerzalności. Alternatywnie można również użyć [maszyny wirtualne Azure](https://azure.microsoft.com/documentation/scenarios/virtual-machines/) (IaaS — infrastruktura jako usługa), gdzie jest odpowiedzialny za konserwację hello podstawowego systemu operacyjnego.

## <a name="next-steps"></a>Następne kroki
Przejrzyj hello najnowszych [wersje systemu operacyjnego gościa](cloud-services-guestos-update-matrix.md).
