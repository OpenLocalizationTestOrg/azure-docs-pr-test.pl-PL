---
title: "aaaAzure terminologia usługi Data Catalog | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera wprowadzenie tooconcepts i terminów używanych w dokumentacji usługi Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Terminologia usługi Azure Data Catalog
## <a name="catalog"></a>Katalogu
Hello Azure Data Catalog to repozytorium metadanych opartych na chmurze danych może być zarejestrowany zasoby oraz źródeł danych. wykaz Hello służy jako lokalizację magazynu centralnego metadane strukturalne wyodrębnione ze źródeł danych oraz metadanych opisowych dodana przez użytkownika.

## <a name="data-source"></a>Źródło danych
Źródło danych jest system lub kontenera, który zarządza zasobów danych. Przykłady obejmują baz danych programu SQL Server, Oracle — bazy danych, bazy danych SQL Server Analysis Services, (wielowymiarowym lub tabelarycznym) i serwerów SQL Server Reporting Services.

## <a name="data-asset"></a>Zasobów danych
Zasoby danych są obiektów zawartych w źródeł danych, które mogą być rejestrowane w katalogu hello. Przykłady obejmują tabel programu SQL Server i widoków, Oracle tabel i widoków, SQL Server Analysis Services miar, wymiarów i wskaźników KPI i raportów usług SQL Server Reporting Services.

## <a name="data-asset-location"></a>Lokalizacja zasobów danych
Witaj w katalogu są przechowywane hello lokalizacji źródła danych lub zasobów danych, które mogą być używane tooconnect toohello źródła przy użyciu aplikacji klienckiej. Hello format i szczegółowe informacje o lokalizacji hello różnić w zależności od typu źródła danych hello. Na przykład tabeli programu SQL Server można zidentyfikować za pomocą czterech części nazwy — nazwa serwera, nazwa bazy danych, nazwę schematu, nazwa obiektu —, podczas gdy raport usług raportowania serwera SQL może zostać zidentyfikowane na podstawie jego adresu URL.

## <a name="structural-metadata"></a>Metadane strukturalne
Metadane strukturalne jest hello metadanych wyodrębnionych ze źródła danych, które opisano strukturę hello zasobów danych. W tym hello lokalizacji zasobów, jego nazwa obiektu i typu oraz dodatkowe właściwości określonego typu. Na przykład hello metadane strukturalne tabele i widoki zawiera hello nazwy i typy danych kolumn hello obiektu.

## <a name="descriptive-metadata"></a>Metadane opisowe
Metadane opisowe jest metadane opisujące przeznaczenie hello lub celem zasobów danych. Zwykle opisowymi metadanymi jest dodawany przez użytkowników katalogu za pomocą portalu wykazu danych Azure hello, ale jego może również zostać wyodrębniony z hello źródła danych podczas rejestracji. Na przykład narzędzie rejestracji usługi Azure Data Catalog hello wyodrębni opisy z hello właściwości Description usług SQL Server Analysis Services i SQL Server Reporting Services i hello [ms_description rozszerzona właściwość](https://technet.microsoft.com/library/ms190243.aspx)w bazach danych programu SQL Server, jeśli te właściwości są wypełnione wartościami.

## <a name="request-access"></a>Żądania dostępu
Metadane opisowe zasobu danych może zawierać informacji na temat sposobu toorequest dostępu toohello danych zasobów lub źródła danych. Te informacje są prezentowane z lokalizacji zasobów danych hello i może zawierać co najmniej jeden hello następujące opcje:

* Witaj adres e-mail użytkownika hello lub zespół odpowiedzialny za udzielanie dostępu toohello danych źródła.
* adres URL Hello hello opisano proces, użytkownicy muszą skorzystaj z źródła danych toohello dostępu toogain.
* adres URL Hello tożsamościami i dostępem narzędzia do zarządzania (takich jak Microsoft Identity Manager), który może być źródłem danych toohello dostępu toogain używane.
* Wpis niezależnej w tym artykule opisano, jak użytkownicy będą mogli uzyskać źródła danych toohello dostępu.

## <a name="preview"></a>Wersja zapoznawcza
Podgląd w usłudze Azure Data Catalog jest migawką too20 rekordów, które mogą być wyodrębnione ze źródła danych hello podczas rejestracji i przechowywane w katalogu hello metadanymi hello danych zasobów. Podgląd Hello może pomóc użytkowników, którzy odnajdywania zasobów danych lepiej zrozumieć jego funkcji i celów. Innymi słowy wyświetlać dane przykładowe przydatne może być więcej niż zobaczenia właśnie hello nazwy kolumn i typy danych.
Podglądy są obsługiwane tylko dla tabel i widoków, a musi być w sposób jawny wybrany przez użytkownika hello podczas rejestracji.

## <a name="data-profile"></a>Dane profilu
Profil danych w usłudze Azure Data Catalog jest migawką tabeli i na poziomie kolumny metadanych dotyczących zasobów zarejestrowanych danych, która może być wyodrębnione ze źródła danych hello podczas rejestracji i przechowywane w katalogu hello metadanymi hello danych zasobów. pomaga Hello danych profilu użytkowników, którzy odnajdywania zasobów danych lepiej zrozumieć jego funkcji i celów. Podobne toopreviews, profile danych musi być w sposób jawny wybrany przez użytkownika hello podczas rejestracji.

> [!NOTE]
> Wyodrębnianie profilu danych może być kosztowna operacja dla dużych tabel i widoków, a może znacznie zwiększyć hello tooregister czasu wymaganego źródła danych.
>
>

## <a name="user-perspective"></a>Perspektywy użytkownika.
W wykazie danych Azure dowolny użytkownik zapewnia metadane opisowe dla zasobu zarejestrowanych danych. Każdy użytkownik ma różne perspektywą danych hello i jego użycia. Na przykład administrator hello jest odpowiedzialny za serwer może podać szczegóły hello Umowa dotycząca poziomu usług (SLA) lub kopia zapasowa systemu windows; steward danych może zapewnić toodocumentation łącza dla firm hello przetwarza hello danych obsługuje; i analityka może podać opis hello warunków, które są najbardziej odpowiednie tooother analityków, a co jest najbardziej przydatna toothose użytkownicy muszą toodiscover i zrozumieć hello danych.

Każdy z perspektywy te są z założenia cenne i w wykazie danych Azure każdy użytkownik może dostarczyć informacji hello, który jest łatwy do rozpoznania toothem podczas wszyscy użytkownicy mogą używać tych informacji toounderstand hello danych i jej celem.

## <a name="expert"></a>Ekspert
Ekspert jest użytkownik, który został zidentyfikowany jako mający świadomych perspektywy "ekspertów" dla zasobu danych. Każdy użytkownik, można dodać siebie lub inny użytkownik jako ekspert dla zasobu. Są wyświetlane jako eksperta nie daje żadnych dodatkowych uprawnień w wykazie danych Azure; Umożliwia użytkownikom tooeasily zlokalizować tych perspektywy, które są najbardziej prawdopodobną toobe przydatne podczas przeglądania metadane opisowe zasobów.

## <a name="owner"></a>Właściciel
Właściciel jest użytkownik, który ma dodatkowe uprawnienia do zarządzania zasobu danych w wykazie danych Azure. Użytkownicy mogą przejąć prawo własności zarejestrowanych zasobów danych i właścicieli można dodać innym użytkownikom jako współwłaściciele. Aby uzyskać więcej informacji, zobacz [jak toomanage zasobów danych](data-catalog-how-to-manage.md)  

> [!NOTE]
> Prawo własności i zarządzania są dostępne tylko w hello Standard Edition usługi Azure Data Catalog.
>
>

## <a name="registration"></a>Rejestracja
Rejestracja jest hello czynność wyodrębniania danych zasobów metadanych źródła danych oraz go kopiować toohello usługi Azure Data Catalog. Następnie można adnotacji i odnalezionych zasobów danych, które zostały zarejestrowane.

## <a name="see-also"></a>Zobacz też
* [Co to jest usługa Azure Data Catalog?](data-catalog-what-is-data-catalog.md) — Ten artykuł zawiera omówienie usługi Azure Data Catalog hello, hello wartość, która zapewnia i scenariusze hello, który go obsługuje.
* [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md) — w tym artykule przedstawiono samouczek end-to-end, który pokazuje, jak toouse, wykazu danych Azure, dla odnajdywanie źródła danych.  
