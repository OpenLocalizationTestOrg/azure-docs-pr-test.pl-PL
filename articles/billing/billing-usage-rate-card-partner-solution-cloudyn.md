---
title: "aaaMicrosoft użycia Azure i Cloudyn Włącz interfejsy API RateCard tooProvide ITFM dla klientów | Dokumentacja firmy Microsoft"
description: "Zawiera unikatowy perspektywy od firmy Microsoft Azure Billing partnera Cloudyn, ich doświadczeń integrowanie hello interfejsów API usługi Azure rozliczeń ich produktu.  Jest to szczególnie przydatne dla platformy Azure i Cloudyn klientów, którzy chcą przy użyciu/próby Cloudyn dla usług Azure."
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
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a>Microsoft Azure użycia i Cloudyn Włącz interfejsy API RateCard tooProvide ITFM dla klientów
Cloudyn, programowanie partnera firmy Microsoft i głównym dostawcą możliwości zarządzania w chmurze, została wybrana prywatnej wersji zapoznawczej hello nowych interfejsów API RateCard i użycia zasobów usługi Microsoft Azure.  Hello użycia interfejsu API zapewnia dane dotyczące zużycia Azure tooestimated dostępu dla subskrypcji. Hello RateCard API zapewnia pełne informacje o cenach dla wszystkich usług platformy Azure dla klientów z systemem innym niż — Enterprise Umowa EA. Zintegrowany ze sobą, interfejsy API stanowią podstawę pełne informacje dla danych wejściowych do narzędzi IT zarządzanie finansowe (ITFM), takich jak udostępnianych przez Cloudyn.

## <a name="introduction"></a>Wprowadzenie
Witaj tak zwane "mnożenia" danych z hello użycia interfejsu API przy użyciu danych z hello RateCard interfejsu API (użycia [jednostki] ceny [$unit] = szczegółowe dane użycia i kosztów) tworzy hello najbardziej szczegółowego, dokładne i niezawodne informacji dotyczących rozliczeń dostępna dla platformy Azure dzisiaj.

![Omówienie ITFM][1]

Korzystanie z tych interfejsów API zawiera klucza informacje dotyczące użycia i kosztów, stosowanie kont klientów tooanalyze Cloudyn w sposób programowego, proste i tooperform różnych zadań ITFM klientom klientów.

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a>Integrowanie Cloudyn z hello RateCard i interfejsów API użycia
Witaj RateCard interfejsu API wymaga kilku parametrów wejściowych — jak informacje o region, waluty i ustawień regionalnych — ale hello najważniejszych w taki sposób, że jest ona OfferDurableID, która określa, czy typ hello Azure wysyłania ofert klienta hello jest używany (płatności obejmujące, starsze 6 i 12 miesięcy zadeklarowanej plany, MSDN oferty, MPN oferty, oferty promocyjne i inne). Witaj OfferDurableID można znaleźć w hello [portal rozliczeń i użycia usługi Azure](https://account.windowsazure.com/Subscriptions), w obszarze hello "Oferują identyfikator" hello podanej subskrypcji.

Po rejestracji dla [Cloudyn dla platformy Azure](https://www.cloudyn.com/microsoft-azure/) usług, klientów można dodać ich kod OfferDurableID, dzięki czemu Cloudyn toopull ich odpowiednie informacje o cenach za pośrednictwem hello RateCard interfejsu API.  Informacje dotyczące różnych typów ofert hello znajduje się jeden hello [szczegółach oferty usługi Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/) strony.

![Przegląd aparatu Cloudyn ITFM][2]

Używa Cloudyn zarówno hello użycia i interfejsów API RateCard, dodanie toohello wydajności interfejsu API Azure, toocreate dodatkowych warstw wizualizację, analizowanie, alertów raportowania, kosztów zarządzania i praktyczne zalecenia, zapewniając klientów platformy Azure to niezawodne Narzędzie ITFM chmury przedsiębiorstwa.

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a>Przypadki użycia Cloudyn ITFM włączane przez użycie i interfejsu API RateCard integracji
ITFM Cloudyn typowych zastosowań włączane przez użycie i interfejsów API RateCard obejmują:

* **Koszt analizy** — umożliwia chmury koszty toobe podziale tooany natywnego identyfikowanie wymiaru (dostawcy, usługi, konto, region itp.). Hello Azure użycia i interfejsów API RateCard Uczyń tę łatwe zadań, dostarczając hello będącego podział danych użycia i kosztów dla konta, które są następnie grupowane i filtrowane według Cloudyn i przedstawione użytkownika toohello w postaci graficzne lub tabelarycznych.

![Wykres kołowy analizy kosztów][3]

* **Koszt 360 alokacji** — zapewnia finance i hello toouncover menedżerów IT rzeczywisty koszt podziału, sterowników i trendów ich wdrożenia w chmurze. Dodatkowo umożliwia menedżerów kosztów wdrożenia Skojarz tooeasily z jednostkami biznesowymi, działów, regiony i inne, zapewniając Niespotykana wgląd w chmurze, koszty i ułatwianie obciążeń zwrotnych w przedsiębiorstwie i showbacks. Hello Azure użycia i interfejsów API RateCard służyć jako wejściowych tooCloudyn koszt alokacji aparat, które uzupełnia hello interfejsów API, definiując metod i logiki biznesowej na potrzeby przydzielania zasobów nieoznakowanego lub untaggable.

![Alokacja kosztu 360 wykresu][4]

* **Ekonomiczne rozmiaru** — zawiera zalecenia dotyczące doboru wielkości niedostatecznie maszyn wirtualnych, co zmniejsza koszty powitania klienta na komputerach zbyt duży lub zbyt elastycznie. Robi to przez sprawdzenie maszyny wirtualnej procesora CPU i pamięci RAM metryki (za pomocą interfejsu API wydajność), godziny, czasu wykonywania (za pośrednictwem interfejsu API użycia) i kosztów (za pośrednictwem interfejsu API RateCard). Cloudyn następnie zawiera zalecenia dotyczące doboru wielkości niedostatecznie zasobów procesora CPU lub pamięci RAM (wydajność) i oblicza szacowany oszczędności mnożąc różnica cen hello (RateCard) między maszynami wirtualnymi hello przez hello Rzeczywista godzina wykorzystanie (użycie) hello niedostatecznie maszyny.

![Ekonomiczne zmiany rozmiaru][5]

* **Eksportowanie zalecenia w chmurze** — udostępnia finansowych porady dotyczące chmury eksportowanie. Sprawdza, czy bieżący kosztów zasobów w chmurze, które są wdrażane w chmurze głównych dostawców użytkownika i porównuje go koszt toohello równoważne wdrożenia na platformie Azure. Zawiera on szczegółowe, na ilością zasobów, finansowo na podstawie eksportowanie tooAzure zalecenia. Po przeprowadzeniu oceny wdrożenia równoważne hello wymagane na platformie Azure (na podstawie wydajności metryki i użytkownika preferencji), Cloudyn używa hello RateCard API tooevaluate hello koszt wdrożenia równoważne hello na platformie Azure.
* **Raporty wydajności** -włączane przez wydajności platformy Azure, interfejsu API, te raporty zapewniają tablica funkcji od wykorzystanie Procesora i pamięci RAM toooptimization zalecenia. Poniżej przedstawiono przykładowy wystąpienia wykorzystania raportu, przedstawiający podział wystąpienia przez średnie wykorzystanie procesora CPU.

![Raporty wydajności][6]

* **Menedżer kategorii** -zaawansowaną funkcją Cloudyn wprowadzający kolejności toounorganized zasobów w chmurze. Zapewnia użytkowników hello swobodę toocreate własne kategorie unikatowy (tagów) skuteczne pomiaru i raportów, która jest zgodna z działalności biznesowej. Ponadto użytkownicy mogą łatwo regulowania i kategoryzowanie niespójne znakowanie (np. błędów pisowni i inne niezgodności) i automatycznie Wykryj nieoznakowanego zasobów dla kosztu precyzyjne autorstwa.

![Menedżer kategorii][7]

## <a name="video"></a>Połączenia wideo
Poniżej przedstawiono krótki klip wideo pokazuje, jak Azure klienta za pomocą Cloudyn platformy Azure i hello rozliczeń interfejsów API usługi Azure, toogain wgląd w dane dotyczące ich dane wykorzystania platformy Azure.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a>Następne kroki
* Uruchom bezpłatny [Cloudyn dla platformy Azure](https://www.cloudyn.com/microsoft-azure/) toosee wersji próbnej, jak można uzyskać koszt przezroczystość z dostosowanych raportowania i analiz dla danego wdrożenia w chmurze Microsoft Azure.
* Zobacz [uzyskać wgląd w Microsoft Azure użycia zasobów](billing-usage-rate-card-overview.md) omówienie API RateCard i hello użycia zasobów Azure.
* Zapoznaj się z hello [dokumentacja interfejsu API REST rozliczenia Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) uzyskać więcej informacji na obu interfejsów API, które są częścią hello zestaw interfejsów API dostarczonych przez hello Azure Resource Manager.
* Jeśli chcesz toodive bezpośrednio w hello przykładowy kod, wyewidencjonuj naszych Microsoft Azure Billing interfejsu API przykłady kodu na [przykłady kodu Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

## <a name="learn-more"></a>Dowiedz się więcej
* odwiedź stronę toolearn więcej informacji na temat usługi Microsoft Azure Enterprise Agreement (EA) oferty, [licencjonowania platformy Azure i hello Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/)
* Zobacz hello [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) więcej informacji na temat usługi Azure Resource Manager hello toolearn artykułu.
* Aby uzyskać dodatkowe informacje na powitania pakiet narzędzi spędzają na potrzeby toohelp w uzyskiwaniu zrozumienia chmury, można znaleźć za artykułu Gartner [rynku przewodnik dla narzędzi IT zarządzanie finansowe (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
