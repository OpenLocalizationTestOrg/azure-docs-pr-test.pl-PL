---
title: "aaaUnderstand Azure szczegółowe użycia | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooread i zrozumieć hello części szczegółowe użycie woluminów CSV dla subskrypcji platformy Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>Zrozumienie warunki na opłaty za programu Microsoft Azure szczegółowe dane użycia 
Hello szczegółowe dane użycia znajdujących się w pliku CSV opłat codziennie i licznika użycia poziomu opłaty za hello bieżącego okresu rozliczeniowego. 

tooget szczegółowe dane użycia pliku, zobacz [jak tooget Azure rozliczeniowego faktury i dziennego użycia danych](billing-download-azure-invoice-daily-usage-date.md).
Jest ona dostępna w formacie wartości rozdzielanych przecinkami (CSV), który można otworzyć w aplikacji arkusza kalkulacyjnego. Jeśli zobaczysz dostępne dwie wersje, Pobierz w wersji 2. To hello najbardziej bieżącego formatu pliku.

Opłaty za użycie są hello całkowita **miesięczne** opłat w ramach subskrypcji. Opłaty za użycie nie uwzględniać żadnych środków ani rabatów.

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>Szczegółowe warunki i opisy szczegółowe dane użycia pliku
Witaj poniższych sekcjach opisano ważne pojęcia hello wyświetlany w wersji 2 hello szczegółowe dane użycia pliku.

### <a name="statement"></a>— Instrukcja
Pierwsza sekcja hello Hello szczegółowe użycia CSV pokazuje hello usług plików używane w okresie rozliczeniowym hello miesiąca. Witaj poniższej tabeli wymieniono warunki hello i opisy w tej sekcji.

| Termin | Opis |
| --- | --- |
|Okres rozliczeniowy |Witaj okresie rozliczeniowym stosowania hello liczników |
|Kategoria miernika |Identyfikuje hello usługi najwyższego poziomu do użycia hello |
|Podkategoria miernika |Definiuje typ hello Azure usługi, które mogą wpływać na szybkość hello |
|Nazwa miernika |Identyfikuje hello jednostka miary dla pomiaru hello są używane |
|Region miernika |Określa lokalizację hello datacenter hello niektórych usług, które kosztują na podstawie lokalizacji centrum danych |
|SKU |Identyfikuje hello systemu Unikatowy identyfikator dla każdego licznika Azure |
|Jednostka |Identyfikuje hello jednostki, dla której usługa hello jest rozliczana w. Na przykład, GB, godziny, 10 000 s. |
|Zużyta ilość |Kwota Hello miernika hello używane podczas hello okresie rozliczeniowym |
|Uwzględniona ilość |Kwota Hello miernika hello dostępnej za darmo w Twojej bieżącego okresu rozliczeniowego |
|Ilość nadwyżkowego użycia |Pokazuje hello różnica między hello ilości zużytego i hello uwzględniona ilość. Opłaty są naliczane na tę kwotę. W przypadku ofert płatność za rzeczywiste użycie nie ilością uwzględnione z ofertą hello hello jest to całkowita liczba tak samo jak hello ilości zużytego. |
|W ramach zobowiązania |Pokazuje hello miernika opłat, które jest odejmowany od kwota zobowiązania skojarzonych z Twoją ofertę 6 i 12-miesięczny. Licznik opłaty są odejmować w kolejności chronologicznej. |
|Waluta |Waluta Hello używana w Twojej bieżącego okresu rozliczeniowego |
|Nadwyżka |Pokazuje hello miernika opłat, które przekraczają kwota zobowiązania skojarzonych z Twoją ofertę 6 i 12-miesięczny |
|Stawka ze zobowiązania |Pokazuje szybkość zobowiązań hello na podstawie hello całkowita zobowiązania skojarzonych z Twoją ofertę 6 i 12-miesięczny |
|Stawka |szybkość Hello, które są pobierane na jednostkę rozliczeniowy |
|Wartość |Przedstawia wynik hello multiplikujący hello ilość nadwyżkowe kolumnami hello szybkości. Jeśli powitalne nie przekracza ilość używane hello uwzględniona ilość, Brak bez dodatkowych opłat w tej kolumnie. |

### <a name="daily-usage"></a>Dzienne dane użycia

Hello codziennego użycia części pliku CSV hello przedstawia szczegóły użycia, które mają wpływ na powitania rozliczeń stawki. Witaj poniższej tabeli wymieniono warunki hello i opisy w tej sekcji.

| Termin | Opis |
| --- | --- |
|Data wykorzystania |Data Hello stosowania hello licznika |
|Kategoria miernika |Identyfikuje hello usługi najwyższego poziomu, dla którego należy to użycie |
|Identyfikator miernika |Witaj rozliczane identyfikator licznika, który został użyty tooprice użycia rozliczeń |
|Podkategoria miernika |Definiuje typ usługi Azure hello, które mogą wpływać na szybkość hello |
|Nazwa miernika |Identyfikuje hello jednostka miary dla pomiaru hello są używane |
|Region miernika |Określa lokalizację hello datacenter hello niektórych usług, które kosztują na podstawie lokalizacji centrum danych |
|Jednostka |Identyfikuje jednostki hello tego miernika hello jest rozliczana w. Na przykład, GB, godziny, 10 000 s. |
|Zużyta ilość |Kwota Hello miernika hello zużyto za ten dzień |
|Lokalizacja zasobu |Identyfikuje hello centrum danych, gdzie działa hello licznika |
|Użyta usługa |Witaj usługi platformy Azure, który został użyty |
|Grupa zasobów |w których hello wdrożonej miernika jest uruchomiony w grupie zasobów Hello. <br/><br/>Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
|Identyfikator wystąpienia | Identyfikator Hello hello miernika. <br/><br/> Identyfikator Hello zawiera hello nazwa określona dla licznika hello podczas jej tworzenia. To albo nazwa hello zasobu hello lub hello w pełni kwalifikowany identyfikator zasobu. Aby uzyskać więcej informacji, zobacz [interfejsu API usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). |
|Tagi | Tag przypisać toohello miernika. Użyj tagów toogroup rozliczeń rekordów.<br/><br/>Na przykład można użyć tagów toodistribute kosztów działu hello używa hello miernika. Usługi obsługujące emisji tagi są maszyny wirtualne, magazynu i usług sieciowych udostępnione przy użyciu hello [interfejsu API usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). Aby uzyskać więcej informacji, zobacz [organizowania zasobów na platformie Azure przy użyciu tagów](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/). |
|Dodatkowe informacje |Metadane specyficzne dla usługi. Na przykład typ obrazu dla maszyny wirtualnej. |
|Informacje o usłudze 1 |Nazwa projektu Hello hello usługi należy tooon subskrypcji |
|Informacje o usłudze 2 |Starszych pola, który przechwytuje opcjonalne metadane specyficzne dla usługi |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>Jak utworzyć się, że opłaty hello w szczegółowe dane użycia pliku są poprawne?
Jeśli w pliku szczegółowe dane użycia, które mają więcej szczegółów na znajduje się opłat, zobacz [zrozumieć rachunku platformy Microsoft Azure.](./billing-understand-your-bill.md)

## <a name="external"></a>Informacje o zewnętrznych opłaty za usługę?
Usług zewnętrznych (znanej także jako zamówienia witryny Marketplace) są dostarczane przez dostawców usługi niezależne i są rozliczane oddzielnie. Witaj opłaty nie pojawiać się na hello Azure faktury. toolearn więcej, zobacz [zrozumieć sieci Azure koszty usługi zewnętrzne](billing-understand-your-azure-marketplace-charges.md).

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?) uzyskać szybkie rozwiązanie problemu.
