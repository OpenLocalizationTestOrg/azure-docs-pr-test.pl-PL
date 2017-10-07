---
title: tooAzure aaaIntroduction Data Catalog | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera omówienie programu Microsoft Azure Data Catalog, w tym funkcje i hello problemów, które spełnia. Wykaz danych umożliwia tooregister dowolnego użytkownika, odnajdywania, zrozumienia i używania źródeł danych."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: cc733907-17ec-4153-9f0c-5b3754b2db19
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 82144c440b5692d3608af08208f36ee8e6dfdc93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-data-catalog"></a>Co to jest usługa Azure Data Catalog?
Wykaz danych Azure to usługa w chmurze w pełni zarządzana użytkowników, którzy mogą odnajdować źródła danych hello potrzebnych i zrozumieć hello źródeł danych, który znajduje się. Na powitania sam czasu, Data Catalog pomaga organizacjom get, więcej wartości z ich istniejących inwestycji. 

Za pomocą usługi Data Catalog każdy użytkownik (analityk, badacz danych lub deweloper) może odnaleźć, zrozumieć i używać źródła danych. Usługa Data Catalog korzysta z crowdsourcingowego modelu metadanych i adnotacji. Jest jednym, centralnym miejscu wszystkie toocontribute użytkowników w organizacji swoją wiedzę i tworzenia społeczności i kultury danych.

## <a name="discovery-challenges-for-data-consumers"></a>Wyzwania dotyczące odnajdywania dla konsumentów danych
Tradycyjnie wykrywanie firmowych źródeł danych było organicznym procesem opartym na wiedzy pochodzącej z wewnątrz firmy. Dla firm, które mają tooget hello największych korzyści ze swoimi zasobami informacyjnymi to rozwiązanie przedstawia wiele wyzwań przed:

* Użytkownicy mogą nie mieć świadomości, że źródło danych istnieje, dopóki nie natrafią na nie w ramach innego procesu. Brak lokalizacji centralnej rejestracji źródła danych.
* Jeśli użytkownicy wiedzą hello lokalizację źródła danych, nie można połączyć toohello danych za pomocą aplikacji klienckiej. Środowisko konsumowania danych wymaga parametrów połączenia hello tooknow użytkowników lub ścieżki.
* Jeśli użytkownicy wiedzą hello lokalizacji dokumentacji źródła danych, nie może zrozumieć hello przeznaczone używa hello danych. Źródła danych i dokumentacja mogą znajdować się w różnych miejscach i być używane w różny sposób.
* Jeśli użytkownicy mają pytania dotyczące zasobu informacyjnego, musi zlokalizować hello specjalistę lub zespół, który jest odpowiedzialny za hello danych i Uwzględnij je w tryb offline. Nie istnieje jawne połączenie między danymi a osobami, które mają specjalistyczne spojrzenie na ich użycie.
* Bez użytkowników zrozumienia procesu hello żądanych źródła danych programu access toohello, odnajdywanie źródła danych hello i jego dokumentacji nadal nie pozwalają uzyskać dostęp do danych hello.

## <a name="discovery-challenges-for-data-producers"></a>Wyzwania dotyczące odnajdywania dla producentów danych
Mimo że hello krój konsumenci danych powyżej problemy, użytkownicy, którzy są odpowiedzialni za tworzenie i utrzymywanie zasobów informacyjnych mają własne inne:

* Dodawanie adnotacji do źródeł danych z opisowymi metadanymi jest często niepotrzebnym wysiłkiem. Aplikacje klienckie zwykle ignorują opisy, które są przechowywane w źródle danych hello.
* Tworzenie dokumentacji dla źródeł danych jest często niepotrzebnym wysiłkiem. Synchronizacja dokumentacji ze źródłami danych jest ciągłym procesem, a użytkownicy mogą wykazywać brak zaufania do dokumentacji, która jest traktowana jako nieaktualna.
* Tworzenie i utrzymywanie dokumentacji źródeł danych to złożony i czasochłonny proces. Wprowadzanie tej dokumentacji tooeveryone łatwo dostępne, używający hello źródła danych może okazać się bardziej tak.
* Ograniczanie dostępu toodata źródeł i zapewnienie, że konsumenci danych wiedzą, jak dostęp toorequest nieustanne wyzwanie stanowi.

Takie problemy są połączone, ich stanowią dużą przeszkodę dla przedsiębiorstw, które mają tooencourage i wspierania hello wykorzystania i zrozumienia danych przedsiębiorstwa.

## <a name="azure-data-catalog-can-help"></a>Usługa Azure Data Catalog może pomóc
Wykaz danych jest zaprojektowana tooaddress te problemy i toohelp przedsiębiorstw get hello najbardziej wartość z istniejących zasobów informacyjnych. Wykaz danych powoduje, że źródła danych łatwo odnaleźć i zrozumieć hello użytkownicy, którzy zarządzają danymi hello.

Usługa Data Catalog udostępnia usługę w chmurze, w której można zarejestrować źródło danych. Witaj dane pozostają w istniejącej lokalizacji, ale kopia metadanych jest dodawana tooData katalogu, wraz z lokalizacją referencyjną toohello źródła danych. Witaj metadanych jest również indeksowane toomake każdego źródła danych ułatwieniu za pomocą wyszukiwania i toohello zrozumiały dla użytkowników, którzy go odnaleźć.

Po zarejestrowaniu źródła danych jego metadane mogą zostać następnie wzbogacone przez użytkownika hello, który zarejestrował go lub przez innych użytkowników w przedsiębiorstwie hello. Każdy użytkownik może dodawać adnotacje do źródła danych, podając opisy, tagi lub inne metadane, takie jak dokumentacja i procesy służące do żądania dostępu do źródła danych. Te metadane opisowe uzupełniają hello metadane strukturalne (np. Kolumna nazwy i typy danych), zarejestrowany z hello źródła danych.

Odnajdywanie i zrozumienie źródeł danych i ich użycie jest główny cel hello rejestrowania źródeł hello. Użytkownicy w organizacji mogą być wymagane danych do analizy biznesowej, projektowania aplikacji, analizy danych lub wszystkich innych zadań, w których wymagane są odpowiednie dane hello. Użytkownicy mogą korzystać odnajdywania usługi Data Catalog hello środowisko tooquickly Znajdź dane, które odpowiada jego potrzebom zrozumienia tooevaluate danych hello jego przydatności do celu hello i używania danych hello przez otwarcie źródła danych hello w wybranym narzędziu. 

At hello sam czas, użytkownicy mogą przyczynić się katalogu toohello znakowanie, dokumentowania i dodawanie adnotacji do źródeł danych, które zostały już zarejestrowane. Można również zarejestrować nowe źródła danych, które można następnie być wykryte, _rozumiem i używane przez hello społeczności użytkowników wykazu.

![Możliwości usługi Data Catalog](./media/data-catalog-what-is-data-catalog/data-catalog-capabilities.png)

## <a name="learn-more-about-data-catalog"></a>Dowiedz się więcej na temat usługi Data Catalog
toolearn więcej informacji na temat możliwości hello usługi Data Catalog, zobacz:

* [Jak tooregister źródeł danych](data-catalog-how-to-register.md)
* [Jak toodiscover źródeł danych](data-catalog-how-to-discover.md)
* [Jak tooannotate źródeł danych](data-catalog-how-to-annotate.md)
* [Jak toodocument źródeł danych](data-catalog-how-to-documentation.md)
* [Jak tooconnect toodata źródeł](data-catalog-how-to-connect.md)
* [Jak toowork z danymi big data](data-catalog-how-to-big-data.md)
* [Jak toomanage zasobów danych](data-catalog-how-to-manage.md)
* [Jak tooset się hello słownik biznesowy](data-catalog-how-to-business-glossary.md)
* [Często zadawane pytania](data-catalog-frequently-asked-questions.md)

## <a name="next-steps"></a>Następne kroki
wprowadzenie do usługi Data Catalog tooget przejdź do:
* [Microsoft Azure Data Catalog](https://www.azuredatacatalog.com)
* [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md)
