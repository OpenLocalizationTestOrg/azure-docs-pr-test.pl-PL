---
title: "Użycie platformy Microsoft Azure i Włącz interfejsy API RateCard Cloudyn zapewnienie ITFM dla klientów | Dokumentacja firmy Microsoft"
description: "Zawiera unikatowy perspektywy od firmy Microsoft Azure Billing partnera Cloudyn, ich doświadczeń integrowanie rozliczeń interfejsów API usługi Azure ich produktu.  Jest to szczególnie przydatne dla platformy Azure i Cloudyn klientów, którzy chcą przy użyciu/próby Cloudyn dla usług Azure."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: fac0ee2e9cbc87c8b3d04675551bba61f7a532b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-to-provide-itfm-for-customers"></a>Użycie platformy Microsoft Azure i RateCard interfejsów API umożliwiają Cloudyn zapewnienie ITFM dla klientów
Cloudyn, programowanie partnera firmy Microsoft i głównym dostawcą możliwości zarządzania w chmurze, została wybrana w prywatnej wersji zapoznawczej nowe Obciążenie zasobów usługi Microsoft Azure i interfejsów API RateCard.  Interfejs API użycia zapewnia dostęp do danych szacowany wykorzystania platformy Azure dla subskrypcji. Interfejs API RateCard zapewnia pełne informacje o cenach dla wszystkich usług platformy Azure dla klientów z systemem innym niż — Enterprise Umowa EA. Zintegrowany ze sobą, interfejsy API stanowią podstawę pełne informacje dla danych wejściowych do narzędzi IT zarządzanie finansowe (ITFM), takich jak udostępnianych przez Cloudyn.

## <a name="introduction"></a>Wprowadzenie
Tak zwane "mnożenia" danych z użycia interfejsu API z danymi z interfejsu API RateCard (użycia [jednostki] ceny [$unit] = szczegółowe dane użycia i kosztów) tworzy najbardziej szczegółowego, dokładne i niezawodne informacji dotyczących rozliczeń dostępna dla platformy Azure dzisiaj.

![Omówienie ITFM][1]

Korzystanie z tych interfejsów API zawiera klucza informacje dotyczące użycia i kosztów, umożliwiając Cloudyn do analizowania kont klientów w sposób programowego, proste i wykonywania różnych zadań ITFM klientom klientów.

## <a name="integrating-cloudyn-with-the-ratecard-and-usage-apis"></a>Integrowanie Cloudyn z RateCard i interfejsów API użycia
Interfejs API RateCard wymaga kilku parametrów wejściowych — takie jak informacje o regionu, waluty i ustawień regionalnych —, ale OfferDurableID, który określa, że typ Azure oferty klient używa płatność za rzeczywiste (użycie, plany starszych 6 i 12 miesięcy zadeklarowanej jest jednym z najważniejszych MSDN oferuje, MPN oferty, oferty promocyjne i inne). OfferDurableID można znaleźć w [portal rozliczeń i użycia Azure](https://account.windowsazure.com/Subscriptions), w obszarze "Oferują identyfikator" dla danej subskrypcji.

Po rejestracji dla [Cloudyn dla platformy Azure](https://www.cloudyn.com/microsoft-azure/) usługi, klienci mogą dodać ich kodu OfferDurableID, dzięki czemu Cloudyn ściągania ich odpowiednie informacje o cenach za pośrednictwem interfejsu API RateCard.  Informacje na temat różnych typów oferty można znaleźć jednego [szczegółach oferty usługi Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) strony.

![Przegląd aparatu Cloudyn ITFM][2]

Cloudyn używa użycia i interfejsów API RateCard, oprócz wydajności interfejsu API Azure do utworzenia dodatkowych warstw wizualizacji, analytics, alertów, raportowanie, kosztów zarządzania i praktyczne zalecenia, zapewniając klientów platformy Azure to niezawodne Narzędzie ITFM chmury przedsiębiorstwa.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Przypadki użycia Cloudyn ITFM włączane przez użycie i interfejsu API RateCard integracji
ITFM Cloudyn typowych zastosowań włączane przez użycie i interfejsów API RateCard obejmują:

* **Koszt analizy** — umożliwia chmury kosztów podzielone żadnego natywnego wymiaru identyfikujące (dostawcy, usługi, konto, region itp.). Użycia Azure i interfejsów API RateCard Uczyń tę łatwe zadanie, podając będącego podział użycia i danych na konto, które są następnie grupowane i filtrowane według Cloudyn i prezentowane w postaci graficzne lub tabelarycznym użytkownikowi kosztów.

![Wykres kołowy analizy kosztów][3]

* **Koszt 360 alokacji** — zapewnia finance i menedżerów do ujawniania podział rzeczywisty koszt, sterowników i trendów ich wdrożenie chmury. Umożliwia dalsze menedżerów łatwo skojarzyć z jednostek biznesowych, działów, regiony i inne, zapewniając Niespotykana wgląd w chmurze, koszty i ułatwianie obciążeń zwrotnych w przedsiębiorstwie i showbacks koszty wdrożenia. Użycie Azure i interfejsów API RateCard służyć jako dane wejściowe do aparatu alokacji koszt Cloudyn firmy, które uzupełnia interfejsy API, definiując metod i logiki biznesowej na potrzeby przydzielania zasobów nieoznakowanego lub untaggable.

![Alokacja kosztu 360 wykresu][4]

* **Ekonomiczne rozmiaru** — zawiera zalecenia dotyczące doboru wielkości niedostatecznie maszyn wirtualnych, co zmniejsza koszty klienta na komputerach zbyt duży lub zbyt elastycznie. Robi to przez sprawdzenie maszyny wirtualnej procesora CPU i pamięci RAM metryki (za pomocą interfejsu API wydajność), godziny, czasu wykonywania (za pośrednictwem interfejsu API użycia) i kosztów (za pośrednictwem interfejsu API RateCard). Cloudyn następnie zawiera zalecenia dotyczące doboru wielkości niedostatecznie zasobów procesora CPU lub pamięci RAM (wydajność) i oblicza szacowany oszczędności mnożąc delta cen (RateCard) między maszynami wirtualnymi Rzeczywista godzina-wykorzystania (użycie) niedostatecznie maszyny.

![Ekonomiczne zmiany rozmiaru][5]

* **Eksportowanie zalecenia w chmurze** — udostępnia finansowych porady dotyczące chmury eksportowanie. Sprawdza, czy bieżący kosztów zasobów w chmurze, które są wdrażane w chmurze głównych dostawców użytkownika i porównuje go do kosztów równoważne wdrażania na platformie Azure. Zawiera on szczegółowe, na ilością zasobów, finansowo na podstawie eksportowanie zalecenia na platformie Azure. Po przeprowadzeniu oceny równoważne wdrożenia wymagane na platformie Azure (na podstawie wydajności metryki i użytkownika preferencji), Cloudyn korzysta RateCard API oceniania kosztów równoważne wdrażania na platformie Azure.
* **Raporty wydajności** -włączane przez wydajności platformy Azure, interfejsu API, te raporty zapewniają tablica funkcji od wykorzystanie Procesora i pamięci RAM do optymalizacji zalecenia. Poniżej przedstawiono przykładowy wystąpienia wykorzystania raportu, przedstawiający podział wystąpienia przez średnie wykorzystanie procesora CPU.

![Raporty wydajności][6]

* **Menedżer kategorii** -zaawansowaną funkcją Cloudyn wprowadzający kolejności do zasobów w chmurze unorganized. Oferuje ono użytkownikom swobodę do tworzenia własnych unikatowy kategorii (tagów) skuteczne pomiaru i raportowania, który jest zgodny z działalności biznesowej. Ponadto użytkownicy mogą łatwo regulowania i kategoryzowanie niespójne znakowanie (np. błędów pisowni i inne niezgodności) i automatycznie Wykryj nieoznakowanego zasobów dla kosztu precyzyjne autorstwa.

![Menedżer kategorii][7]

## <a name="video"></a>Połączenia wideo
Poniżej przedstawiono krótki klip wideo pokazuje, jak klienta Azure mogą używać Cloudyn platformy Azure i rozliczeń interfejsów API usługi Azure, w celu uzyskania szczegółowych informacji z danych ich wykorzystania platformy Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Następne kroki
* Uruchom bezpłatny [Cloudyn dla platformy Azure](https://www.cloudyn.com/microsoft-azure/) próbę, aby sprawdzić, jak można uzyskać koszt przezroczystość z dostosowanych raportowania i analiz dla danego wdrożenia w chmurze Microsoft Azure.
* Zobacz [uzyskać wgląd w Microsoft Azure użycia zasobów](billing-usage-rate-card-overview.md) omówienie API RateCard i użycia zasobów Azure.
* Zapoznaj się z [dokumentacja interfejsu API REST rozliczenia Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) uzyskać więcej informacji na obu interfejsów API, które są częścią zestawu interfejsów API dostarczonych przez Menedżera zasobów Azure.
* Jeśli chcesz przejść bezpośrednio do przykładowy kod, zobacz nasze Microsoft Azure Billing interfejsu API przykłady kodu na [przykłady kodu Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Dowiedz się więcej
* Aby dowiedzieć się więcej o ofertach usług Microsoft Azure Enterprise Agreement (EA), przejdź na stronę [licencjonowania platformy Azure dla przedsiębiorstw](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) artykuł, aby dowiedzieć się więcej na temat usługi Azure Resource Manager.
* Aby uzyskać dodatkowe informacje na temat zestawu narzędzi, które są niezbędne pomóc w uzyskaniu zrozumienia chmury wydatków, można znaleźć w artykule Gartner [rynku przewodnik dla narzędzi IT zarządzanie finansowe (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
