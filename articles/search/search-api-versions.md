---
title: "aaaAPI wersje usługi Azure Search | Dokumentacja firmy Microsoft"
description: "Zasady dot. wersji API REST usługi Azure Search i hello biblioteki klienta w hello zestawu .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>Wersje interfejsu API w usłudze Azure Search
Usługa Azure Search regularnie zbiera i wydaje aktualizacje funkcji. Czasami, ale nie zawsze, te aktualizacje wymagają nam toopublish nowej wersji naszych interfejsu API toopreserve zgodności z poprzednimi wersjami. Publikowania nowej wersji można toocontrol podczas i jak integrować aktualizacje usługi wyszukiwania w kodzie.

Zgodnie z zasadą spróbujemy toopublish nowe wersje tylko wtedy, gdy jest to konieczne, ponieważ może dotyczyć niektórych tooupgrade nakładu wersji toouse nowy interfejs API kodu. Nowa wersja firma Microsoft opublikuje tylko jeśli potrzebujemy toochange pewien aspekt hello interfejsu API w sposób, który dzieli zgodności z poprzednimi wersjami. Może to nastąpić z powodu funkcji tooexisting poprawki lub z powodu nowe funkcje, które spowodują zmianę istniejących powierzchni interfejsu API.

Firma Microsoft wykonaj hello same reguły aktualizacje zestawu SDK. Witaj zestawu SDK usługi Azure Search następuje hello [wersjonowania semantycznego](http://semver.org/) reguł, które oznacza, że wersja ma trzy części: główne, pomocnicze i kompilacji (na przykład 1.1.0). Firma Microsoft opublikuje nową wersję główną hello SDK tylko w przypadku zmiany, które Podziel zgodności z poprzednimi wersjami. W przypadku twardej funkcji aktualizacji możemy powoduje zwiększenie hello wersji pomocniczej, a dla poprawki możemy tylko zwiększy hello wersji kompilacji.

> [!NOTE]
> Wystąpienia usługi Azure Search obsługuje kilka wersji interfejsu API REST, w tym hello najnowszy numer. Można kontynuować toouse wersji, gdy nie jest już hello najnowszego, ale zaleca się przeprowadzenie migracji kodu toouse hello najnowszej wersji. Korzystając z hello interfejsu API REST, należy określić wersję interfejsu API hello w każde żądanie za pośrednictwem parametru api-version hello. Używając hello zestawu .NET SDK, wersja hello hello używasz zestawu SDK określa hello odpowiedniej wersji hello interfejsu API REST. Jeśli używasz starszej zestawu SDK można kontynuować toorun kodu bez zmian, nawet jeśli usługa hello jest wersja uaktualniona toosupport nowszej interfejsu API.

## <a name="snapshot-of-current-versions"></a>Migawkę bieżącej wersji.
Poniżej znajduje się migawkę hello bieżące wersje tooAzure wszystkich interfejsów programowania wyszukiwania.

| Interfejsy | Najnowszą wersją główną | Stan |
| --- | --- | --- |
| [Zestaw SDK platformy .NET](https://aka.ms/search-sdk) |3.0 |Ogólnie dostępne, wydane listopada 2016 |
| [Wersja zapoznawcza zestawu SDK .NET](https://aka.ms/search-sdk-preview) |Wersja zapoznawcza 2.0 |Podgląd wydane sierpnia 2016 |
| [Interfejs API REST usługi](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |Ogólnie dostępna |
| [Podgląd interfejsu API REST usługi](search-api-2015-02-28-preview.md) |2015-02-28-preview |Wersja zapoznawcza |
| [Zarządzanie .NET SDK](https://aka.ms/search-mgmt-sdk) |2015-08-19 |Ogólnie dostępna |
| [Interfejsu API REST zarządzania](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |Ogólnie dostępna |

Dla interfejsów API REST, w tym hello hello `api-version` na każde wywołanie jest wymagane. Dzięki temu można łatwo tootarget określonej wersji, np. interfejsu API w wersji zapoznawczej. Witaj poniższy przykład przedstawia sposób hello `api-version` określony parametr:

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> Mimo że każdego żądania ma `api-version`, zalecane jest użycie hello tej samej wersji dla wszystkich żądań interfejsu API. Jest to szczególnie istotne podczas wprowadzenia nowych wersji interfejsu API atrybuty lub operacje, które nie są rozpoznawane przez poprzednie wersje. Mieszanie wersji interfejsu API może mieć niezamierzone skutki i należy unikać.
>
> Witaj interfejsu API REST usługi i interfejsu API REST zarządzania są numerów wersji niezależnie od siebie nawzajem. Przypadkowe jest wszelkie podobieństwa numerów wersji.

Ogólnie dostępne (lub GA) interfejsy API mogą być używane w środowisku produkcyjnym i są tooAzure podmiotu umów dotyczących poziomu usług. Wersji zapoznawczych ma eksperymentalną, które nie zawsze są migrowane tooa GA wersji. **Zdecydowanie odradzamy przy użyciu podglądu interfejsów API w aplikacji produkcyjnych.**

## <a name="about-preview-and-generally-available-versions"></a>Informacje dotyczące wersji Preview i ogólnie dostępna
Usługa Azure Search zawsze wstępnie zwalnia eksperymentalną za pośrednictwem interfejsu API REST hello najpierw, następnie za pomocą wersji wstępnej hello zestawu .NET SDK.

Funkcje w wersji zapoznawczej nie ma gwarancji toobe migracji tooa GA wersji. Funkcje w wersji GA są traktowane jako stabilny i nieprzeznaczona toochange z wyjątkiem hello małych poprawki zapewniającej i ulepszenia, funkcje w wersji zapoznawczej są dostępne do testowania i eksperymenty z celem zbierania opinii na powitania Funkcja projektowanie i wdrażanie.

Jednak ponieważ funkcje w wersji zapoznawczej toochange podmiotu, zaleca się przed pisania kodu produkcyjnego ma zależności w wersji zapoznawczej. Jeśli używasz starszej wersji zapoznawczej firma Microsoft zaleca migracji toohello ogólnie dostępna wersja (GA).

Dla zestawu .NET SDK hello: wskazówki dotyczące migracji kodu można znaleźć w folderze [uaktualnienia hello zestawu .NET SDK](search-dotnet-sdk-migration.md).

Ogólnie oznacza, że usługi Azure Search ma teraz w obszarze hello Umowa dotycząca poziomu usług (SLA). Witaj SLA można znaleźć w [umowy dotyczące poziomu usług wyszukiwanie Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
