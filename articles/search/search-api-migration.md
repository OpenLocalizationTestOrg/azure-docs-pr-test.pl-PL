---
title: "toohello aaaUpgrading interfejsu API REST usługi wyszukiwanie Azure w wersji 2016-09-01 | Dokumentacja firmy Microsoft"
description: "Uaktualnianie toohello interfejsu API REST usługi wyszukiwanie Azure w wersji 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>Uaktualnianie toohello interfejsu API REST usługi wyszukiwanie Azure w wersji 2016-09-01
Jeśli używasz wersji 2015-02-28 lub 2015-02-28-Podgląd hello [interfejsu API REST usługi Azure Search](https://msdn.microsoft.com/library/azure/dn798935.aspx), ten artykuł pomoże Ci uaktualnienie aplikacji toouse hello dalej ogólnie dostępna wersją interfejsu API, 2016-09-01.

Wersja 2016-09-01 hello interfejsu API REST zawiera pewne zmiany z wcześniejszych wersji. Są to przede wszystkim zgodne z poprzednimi wersjami, tak więc zmiana kodu powinny wymagać tylko minimalnym wysiłku, w zależności od instalowanej wersji używanego wcześniej. Zobacz [tooupgrade kroki](#UpgradeSteps) instrukcje na temat toochange kodu toouse hello nowe wersją interfejsu API.

> [!NOTE]
> Wystąpienia usługi Azure Search obsługuje kilka wersji interfejsu API REST, w tym hello najnowszy numer. Można kontynuować toouse wersji, gdy nie jest już hello najnowszego, ale zaleca się przeprowadzenie migracji kodu toouse hello najnowszej wersji.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>Nowości w wersji 2016-09-01
Wersja 2016-09-01 jest hello drugi ogólnie dostępna wersja hello interfejsu API REST usługi Azure Search. Nowe funkcje w tej wersji interfejsu API:

* [Niestandardowe analizatorów](https://aka.ms/customanalyzers), co pozwala użytkownikowi tootake kontrolę nad hello proces konwersji tekstu na tokeny można indeksować i wyszukiwanie.
* [Magazyn obiektów Blob Azure](search-howto-indexing-azure-blob-storage.md) i [Azure Table Storage](search-howto-indexing-azure-tables.md) indeksatorów, które pozwalają tooeasily importowanie danych z magazynu Azure do usługi Azure Search na harmonogram lub na żądanie.
* [Pole — mapowanie](search-indexer-field-mappings.md), co pozwala użytkownikowi toocustomize jak indeksatory importowania danych do usługi Azure Search.
* Elementy etag, pozwalają tooupdate hello definicje indeksów, indeksatorów i źródeł danych w sposób bezpieczny współbieżności. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Kroki tooupgrade
Jeśli uaktualniasz z wersji 2015-02-28, prawdopodobnie nie będziesz mieć toomake żadnego kodu tooyour zmiany, innego niż numer wersji hello toochange. Hello tylko sytuacji, w których może być konieczne toochange kodu są:

* Kod kończy się niepowodzeniem, nierozpoznany właściwości są zwracane w odpowiedzi interfejsu API. Domyślnie aplikacja ignorować właściwości, których nie zna.
* Kod będzie się powtarzał żądania interfejsu API i próbuje tooresend ich toohello nowej wersji interfejsu API. Na przykład może się zdarzyć, aplikacja będzie nadal występował tokeny kontynuacji zwrócony z interfejsu API Search hello (Aby uzyskać więcej informacji, poszukaj `@search.nextPageParameters` w hello [odwołanie wyszukiwania do interfejsu API](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Jeśli jeden z tych sytuacji zastosować tooyou, może wymagać toochange kodu odpowiednio. W przeciwnym razie żadne zmiany jeśli są niezbędne, chyba że chcesz toostart przy użyciu hello [nowe funkcje](#WhatsNew) wersji 2016-09-01.

Uaktualniania z wersji 2015-02-28-Preview hello powyżej ma również zastosowanie, ale należy wziąć pod uwagę, że niektóre funkcje wersji zapoznawczej nie są dostępne w wersji 2016-09-01:

* Magazyn obiektów Blob indeksatora pomocy technicznej platformy Azure dla plików CSV i obiektów blob zawierający tablice notacji JSON.
* Synonimy
* Zapytania "Więcej postać"

Jeśli kod korzysta z tych funkcji, nie będzie możliwe tooupgrade too2016-09-01 bez usuwania użycie ich.

> [!IMPORTANT]
> Należy pamiętać, Podgląd interfejsy API są przeznaczone do testowania i ocenie, a nie powinna być używana w środowisku produkcyjnym.
> 
> 

## <a name="conclusion"></a>Podsumowanie
Aby uzyskać więcej informacji na temat używania hello interfejsu API REST usługi Azure Search, zobacz hello niedawno aktualizowana [dokumentacja interfejsu API](https://msdn.microsoft.com/library/azure/dn798935.aspx) w witrynie MSDN.

Chętnie poznamy Twoją opinię w usłudze Azure Search. Jeśli wystąpią problemy, możesz wolnego tooask nam Aby uzyskać pomoc dotyczącą hello [forum usługi Azure Search w witrynie MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) lub [StackOverflow](http://stackoverflow.com/). Jeśli pytanie o Azure będzie wyszukiwać w witrynie StackOverflow, upewnij się, że tootag z `azure-search`.

Dziękujemy za skorzystanie z usługi Azure Search!

