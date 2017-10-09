---
title: "aaaTechnical wstępne dotyczące tworzenia usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Zrozumienie wymagań hello tworzenia toodeploy usługi danych i sprzedawać w hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Oferuje techniczne wymagania wstępne dotyczące tworzenia usługi danych dla hello Azure Marketplace
> [!IMPORTANT]
> **W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.** Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners). Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Proces hello dokładnie przed rozpoczęciem należy dokładnie zapoznać się gdzie i dlaczego jest wykonywane każdego kroku. Jak to możliwe, należy należy przygotować informacji o swojej firmie i innych danych, Pobierz niezbędne narzędzia i/lub tworzenia składników techniczne przed rozpoczęciem procesu tworzenia oferty hello.

Musisz mieć hello poniższych elementach gotowe przed rozpoczęciem procesu hello:

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>Podjęcie decyzji na technologii, które będzie używane toopublish tej oferty usługi danych
Wydawcą może wybór między wiele technologii podczas publikowania danych usługi w portalu Azure Marketplace. Witaj głównego technologie, które są obsługiwane opisane poniżej. Niezależnie od tego jaki technologia jest używane toopublish hello usługi danych, hello użytkownik końcowy używa hello danych za pośrednictwem hello **źródła strumieniowego OData** udostępnianych przez usługę Azure Marketplace. Pełne informacje dotyczące usługi OData, można znaleźć w [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>SQL bazy danych platformy Azure
Zestaw danych jest gotowy w usługach SQL Azure jest odpowiedzialność wydawcy. Będziesz potrzebować toosubscribe tooAzure udostępnić odpowiedni rozmiar bazy danych i przekazywanie danych do bazy danych SQL Azure. Wydawca jest również odpowiedzialne tookeep jego danych, które są zawsze aktualne. Więcej informacji o subskrypcji usług tooAzure można znaleźć w [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

Podczas przenoszenia danych hello do usługi SQL Azure, hello Azure Marketplace można ujawnić tabel i widoków. Witaj wydawcy można określić, które tabele i widoki i kolumny są uwidocznione toohello przez użytkownika końcowego. Dalsze hello dostawcy zawartości można również określić kolumny, które mogą być przeszukiwane przez użytkownika końcowego hello i zwracane są tylko te, które w ładunku hello. Dzięki temu wysokiego poziomu o tym, które powinny zostać ujawnione danych w bazie danych hello elastyczność. Kolumny, które mogą być przeszukiwane muszą toobe przez jeden lub więcej indeksów bazy danych.

## <a name="rest-based-web-service"></a>Usługi sieci web REST na podstawie
Obsługiwany protokół: **tylko protokołu HTTPS**

Istniejące usługi REST na podstawie można ujawnić za pośrednictwem hello Azure Marketplace. Ponieważ hello dataset jest zawsze toohello uwidocznione przez użytkownika końcowego, jako źródła danych OData, hello usługę Azure Marketplace wymaga toomap stanie toobe hello tooa usługi OData na podstawie usługi. toodo, dzięki czemu punkty końcowe REST na podstawie hello muszą tooexpose wszystkie parametry jako parametry HTTP.

ładunek Hello musi toobe w formularzu, które mogą być mapowane do odpowiedzi ATOM. Dlatego hello odpowiedzi z usług hello wymaga toobe w formacie XML oraz może zawierać tylko jeden element identycznych, zawierającą wartości ładunku hello (na przykład zestawu rekordów). Witaj usługę Azure Marketplace przypisze hello powtarzające się węzeł toohello wpis węzeł w wartości ładunku ATOM i hello w węzłach właściwość w węźle wpis hello.

Informacje dotyczące autoryzacji (np. interfejsu API klucza, uwierzytelniania tokenu, itp.) musi toobe podane jako parametr HTTP lub w nagłówku HTTP hello (para klucz-wartość) — obsługiwana jest również uwierzytelnianie podstawowe. Prawidłowy klucz musi toobe pod warunkiem, a wszystkie żądania za pośrednictwem portalu Azure Marketplace są wykonywane za pośrednictwem tego klucza. W warstwie Azure Marketplace hello odbywa się użytkownika, monitorowanie i fakturowania.

Błędy zwrócone przez usługę hello muszą toobe przypisywane do kody stanu HTTP. W przypadku, gdy usługa hello zwraca kod XML, który zawiera błąd hello te będą toobe zamapowany przez kody stanu tooHTTP hello Azure Marketplace usługi.

## <a name="soap-based-web-services"></a>Na podstawie protokołu SOAP usług sieci web
Protokół: **tylko protokołu HTTPS**

wymagania dotyczące Hello są hello takie same jak w sekcji usługi REST na podstawie hello. Witaj jedyna różnica polega na tym, że parametry można również podać w treści XML, która jest ogłaszany usługi toohello wydawcy z każde żądanie za pośrednictwem portalu Azure Marketplace. Oznacza to, że obejmuje użytkowników hello parametry HTTP w hello frontonu są trwa przetłumaczyć elementów XML dokumentu XML publikowanego z usługą sieci web hello żądania toohello dostawcy zawartości.

## <a name="odata-based-web-services"></a>Usługi sieci web OData na podstawie
Protokół: **tylko protokołu HTTPS**

Dane mogą być udostępniane jako tooAzure usługi OData Marketplace. Hello system jest toopass będzie hello usługi za pośrednictwem i zamienia hello katalog główny usługi hello podstawy usługi Azure Marketplace hello — tooensure, wszystkie kolejne wywołania przejdź za pośrednictwem portalu Azure Marketplace.

Usługi OData tylko niepotrzebne toogo w bazie danych w hello wewnętrznej bazy danych. OData obsługuje żadnego rodzaju magazynu lub business usługi hello toodrive logiki.

## <a name="next-steps"></a>Następne kroki
Po przejrzeniu hello wymagania wstępne i ukończyć powitalnych niezbędnych zadań można przenieść do przodu z hello tworzenia tej oferty usługi danych jako hello szczegółowe w [Podręcznik publikowania danych usługi](marketplace-publishing-data-service-creation.md).

Lub, jeśli chcesz hello tooreview ogólny proces i hello im artykułów dla każdej fazy publikowania hello, odwiedź stronę artykułu hello [wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
