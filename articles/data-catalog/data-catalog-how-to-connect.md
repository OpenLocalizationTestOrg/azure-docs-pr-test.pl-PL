---
title: "aaaHow tooconnect toodata źródeł | Dokumentacja firmy Microsoft"
description: "Tooarticle jak wyróżnianie jak źródeł toodata tooconnect odnalezione w wykazie danych Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>Jak tooconnect toodata źródeł
## <a name="introduction"></a>Wprowadzenie
**Microsoft Azure Data Catalog** to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i system odnajdowania źródeł danych przedsiębiorstwa. Innymi słowy **Azure Data Catalog** wszystkie o osobach myśl odnajdywania, zrozumienia i używania źródeł danych, a także pomaga organizacjom tooget więcej wartość z ich istniejących danych. Kluczowym aspektem w tym scenariuszu używa hello źródła danych — po użytkownika umożliwia odnalezienie danych i zrozumienie jego przeznaczenie, hello następnym krokiem jest źródła danych toohello tooconnect tooput toouse jej danych.

## <a name="data-source-locations"></a>Lokalizacje źródeł danych
Podczas rejestrowania źródła danych **Azure Data Catalog** otrzymuje metadane dotyczące hello źródła danych. Te metadane zawiera szczegóły hello źródła danych hello lokalizacji. Szczegóły Hello lokalizacji hello różnią się od źródła toodata źródła danych, ale zawsze będzie zawierać hello tooconnect informacje potrzebne. Na przykład hello lokalizacji dla tabeli programu SQL Server zawiera hello nazwę serwera, nazwa bazy danych, nazwy schematu i nazwy tabeli, natomiast hello lokalizacji raportu usług SQL Server Reporting Services zawiera hello nazwę serwera i hello ścieżki toohello raportu. Inne typy źródeł danych będą mieć lokalizacje, które odzwierciedlać hello struktury i możliwości systemu źródłowego hello.

## <a name="integrated-client-tools"></a>Narzędzia zintegrowanego klienta
Witaj najprostszy sposób tooconnect tooa źródło danych jest toouse hello "Otwórz w..." menu w hello **Azure Data Catalog** portalu. W tym menu wyświetla listę możliwości podłączenia toohello wybranego zasobu danych.
Korzystając z widoku tile hello domyślne, to menu jest dostępne na hello każdego kafelka.

 ![Otwarcie tabeli programu SQL Server w programie Excel z hello danych zasobów kafelka](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Korzystając z widoku listy hello, hello menu jest dostępne w pasku wyszukiwania hello u góry okna portalu hello hello.

 ![Otwarcie raportu usług SQL Server Reporting Services w Menedżerze raportów z hello pasek wyszukiwania](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Obsługiwany klient aplikacji
Korzystając z hello "Otwórz w..." menu danych źródła w portalu Azure Data Catalog hello, powitania klienta poprawne aplikacja musi zostać zainstalowana na komputerze klienckim hello.

| Otwórz w aplikacji | Rozszerzenie pliku / protokołu | Obsługiwana aplikacja wersji |
| --- | --- | --- |
| Excel |odc |Excel 2010 lub nowszej. |
| Program Excel (pierwszych 1000) |odc |Excel 2010 lub nowszej. |
| Dodatek Power Query |xlsx |Zainstalowany program Excel 2016 lub Excel 2010 lub Excel 2013 z hello dodatku Power Query dla dodatek programu Excel |
| Power BI Desktop |pbix |Power BI Desktop lipca 2016 lub nowszy |
| SQL Server Data Tools |vsweb: / / |Visual Studio 2013 Update 4 lub nowszym z narzędzi programu SQL Server zainstalowana |
| Menedżer raportów |http:// |Zobacz [wymagania przeglądarki do programu SQL Server Reporting Services](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Dane, narzędziami
Witaj opcje dostępne w hello menu zależy od typu hello wybranego zasobu danych. Oczywiście nie wszystkie możliwe narzędzia zostaną uwzględnione w hello "Otwórz w..." menu, ale jest źródłem danych toohello tooconnect wciąż łatwe przy użyciu dowolnego narzędzia klienta. Po wybraniu zasobu danych w hello **Azure Data Catalog** portalu, lokalizacji pełną hello jest wyświetlana w okienku właściwości hello.

 ![Informacje o połączeniu dla tabeli programu SQL Server](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

informacje o połączeniu Hello się, że szczegóły będą się różnić od typu źródłowego toodata typu źródła danych, ale hello informacje zawarte w portalu hello zapewni wszystko, co potrzebne źródła danych toohello tooconnect w narzędziu dowolnego klienta. Użytkownicy mogą kopiować hello szczegóły połączenia dla źródeł danych hello, które zostały odnalezione, za pomocą **Azure Data Catalog**, umożliwiając im toowork z danymi hello w wybranym narzędziu.

## <a name="connecting-and-data-source-permissions"></a>Uprawnienia źródeł danych i łączenie
Mimo że **Azure Data Catalog** temu źródeł danych wykrywalny, dostęp do nich samych danych toohello pozostaje pod kontrolą hello hello danych źródła właściciel lub administrator. Odnajdywanie źródła danych w **Azure Data Catalog** nie daje użytkownikowi żadnych uprawnień tooaccess hello źródło danych.

toomake go łatwiejsze dla użytkowników, którzy odnajdywanie danych źródłowych, ale nie ma uprawnień tooaccess swoje dane, użytkownicy mogą podać informacje w hello żądania dostępu do właściwości podczas Dodawanie adnotacji do źródła danych. Podane tu — takie jak proces toohello łącza lub punkt kontaktu dla uzyskania dostępu do źródła danych — informacje są prezentowane obok informacji o lokalizacji źródła danych hello w portalu hello.

 ![Informacje o połączeniu z żądania dostępu do instrukcji](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Podsumowanie
Rejestrowanie źródła danych z **Azure Data Catalog** sprawia, że dane wykrywalny przez skopiowanie metadanych strukturalnych i opisowy ze źródła danych hello na powitania usługi katalogu. Gdy źródło danych zostało zarejestrowane i odnalezione, użytkownicy mogą łączyć toohello źródła danych z hello **Azure Data Catalog** portal "Otwórz w..." " menu lub przy użyciu ich narzędzi danych wyboru.

## <a name="see-also"></a>Zobacz też
* [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md) samouczek krok po kroku szczegółowe informacje dotyczące tooconnect toodata źródeł.
