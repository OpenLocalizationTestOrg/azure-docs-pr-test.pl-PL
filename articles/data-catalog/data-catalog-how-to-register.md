---
title: "aaaRegister źródeł danych w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono sposób tooregister źródeł danych w wykazie danych Azure, w tym pól metadanych hello wyodrębnione podczas rejestracji."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>Rejestracja źródeł danych w wykazie danych Azure
## <a name="introduction"></a>Wprowadzenie
Wykaz danych Azure to usługa w chmurze pełni zarządzana, która służy jako system rejestracji i odnajdywania źródeł danych przedsiębiorstwa. Innymi słowy Data Catalog pomaga użytkownikom odnajdywania, zrozumienia i używania źródeł danych, a także pomaga organizacjom osiąganie większych zysków z ich istniejących danych. Witaj pierwszy krok toomaking źródła danych wykrywalny przez wykaz danych tooregister jest to źródło danych.

## <a name="register-data-sources"></a>Rejestrowanie źródeł danych (Rejestrowanie źródeł danych)
Rejestracja jest hello proces trwa wyodrębnianie metadanych ze źródła danych hello i kopiowanie tego toohello danych usługi Data Catalog. Witaj dane pozostaną gdzie ona się teraz znajduje i pozostaje pod kontrolą hello hello administratorów i zasady hello bieżącego systemu.

tooregister źródłem danych hello następujące:
1. W portalu Azure Data Catalog hello należy uruchomić narzędzia rejestracji źródła danych usługi Data Catalog hello. 
2. Zaloguj się przy użyciu konta służbowego z hello sam Użyj toosign w portalu toohello poświadczeń usługi Azure Active Directory.
3. Wybierz źródło danych hello ma tooregister.

Aby uzyskać bardziej szczegółowe informacje krok po kroku, zobacz hello [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md) samouczka.

Po hello źródła danych został zarejestrowany, katalogu hello śledzi lokalizacji i indeksuje jego metadanych. Użytkownicy mogą wyszukiwanie, przeglądanie i odnajdywanie źródła danych hello i następnie użyć jego tooit tooconnect lokalizacji za pomocą aplikacji hello lub ich wybranych narzędzi.

## <a name="supported-data-sources"></a>Obsługiwane źródła danych
Aby uzyskać listę aktualnie obsługiwanych źródeł danych, zobacz [DSR wykazu danych](data-catalog-dsr.md).

## <a name="structural-metadata"></a>Metadane strukturalne
Podczas rejestrowania źródła danych, narzędzie rejestracji hello wyodrębnia informacji na temat struktury hello hello obiektów, którą wybierzesz. Te informacje są metadane strukturalne tooas określony.

Dla wszystkich obiektów metadanych strukturalnych zawiera lokalizacji obiektu hello, dzięki czemu użytkownicy, którzy odnajdywanie hello danych mogą używać tego obiektu toohello tooconnect informacji w narzędziach klienckich hello wybranych przez nich. Inne metadane strukturalne zawiera nazwę obiektu i typu i wpisz nazwę atrybutu/kolumny i danych.

## <a name="descriptive-metadata"></a>Metadane opisowe
Ponadto toohello podstawowe metadane strukturalne, który został wyodrębniony z hello źródła danych, narzędzia rejestracji źródła danych hello wyodrębnia metadane opisowe. Dla usług SQL Server Analysis Services i SQL Server Reporting Services te metadane są pobierane z hello opis właściwości udostępniane przez te usługi. Dla programu SQL Server, wartości przy użyciu hello ms\_opis właściwości rozszerzonej jest wyodrębniana. W przypadku bazy danych Oracle hello źródła danych rejestracji narzędzie wyodrębnia hello komentarze kolumny z hello wszystkie\_kartę\_widoku komentarze.

Dodanie toohello opisową metadanych, które są wyodrębniane z hello źródła danych użytkownicy mogą wprowadzać metadane opisowe przy użyciu narzędzia rejestracji źródła danych hello. Użytkownicy mogą dodawać tagi i mogą identyfikować ekspertów dla obiektów hello jest zarejestrowany. Wszystkie te metadane opisowe jest kopiowana toohello usługi Data Catalog wraz z hello metadane strukturalne.

## <a name="include-previews"></a>Obejmują podglądy
Domyślnie tylko metadane są wyodrębniane z źródeł danych i skopiowany toohello usługi Data Catalog, ale opis, którego źródłem danych jest często łatwiejsza po wyświetleniu próbkę danych hello, które zawiera.

Za pomocą narzędzia rejestracji hello źródłem danych Data Catalog, mogą obejmować Podgląd migawki danych hello w każdej tabeli i widoku, który jest zarejestrowany. Jeśli wybierzesz podglądy tooinclude podczas rejestracji, narzędzia rejestracji hello obejmuje too20 rekordów z każdym tabel i widoków. Ta migawka jest następnie skopiowana toohello wykazu wraz z hello metadanych strukturalnych i opisowy.

> [!NOTE]
> Szerokie tabele z dużą liczbą kolumn może mieć mniej niż 20 rekordy w ich podglądu.
>
>

## <a name="include-data-profiles"></a>Dołącz profile danych
Zgodnie z tym podglądy zapewniają cenne kontekst dla użytkowników, którzy wyszukiwania źródeł danych w katalogu danych, w tym profilu danych można tworzyć i łatwiejsze źródeł danych toounderstand odnalezione.

Za pomocą narzędzia rejestracji hello źródłem danych Data Catalog, mogą obejmować dane profilu dla każdej tabeli i widoku, który jest zarejestrowany. Jeśli wybierzesz tooinclude profilu danych podczas rejestracji, narzędzie rejestracji hello zawiera zagregowanych danych statystycznych dotyczących danych hello w poszczególnych tabel i widoków, w tym:

* Hello liczba wierszy i rozmiar danych hello w obiekcie hello.
* Data Hello hello ostatniej aktualizacji danych hello i hello obiektu schematu.
* Liczba Hello null rekordów i różne wartości w kolumnach.
* Witaj minimum, maksimum średnią i odchylenie standardowe wartości dla kolumny.

Te statystyki są następnie kopiowane toohello wykazu wraz z hello metadanych strukturalnych i opisowy.

> [!NOTE]
> Tekst i Data kolumny nie dołączaj statystyki średniej lub odchylenie standardowe w swoim profilu danych.
>
>

## <a name="update-registrations"></a>Aktualizacja rejestracji
Rejestrowanie źródła danych dzięki wykrywalny w wykazie danych podczas korzystania z metadanych hello i opcjonalnie Podgląd wyodrębnione podczas rejestracji. Jeśli źródło danych hello musi toobe zaktualizowane w katalogu hello (na przykład jeśli hello schematu obiektu został zmieniony, tabele pierwotnie wykluczone mają zostać uwzględnione lub dane hello tooupdate, który znajduje się w wersji zapoznawczych hello), narzędzia rejestracji źródła danych hello można uruchomić ponownie.

Ponowne rejestrowanie źródła danych już zarejestrowany wykonuje operację "upsert" merge: istniejące obiekty są aktualizowane i nowych obiektów. Wszystkie metadane udostępniane użytkownikom za pomocą portalu wykazu danych hello są zachowywane.

## <a name="summary"></a>Podsumowanie
Ponieważ metadanych strukturalnych i opisowy są kopiowane z usługi wykaz toohello źródła danych, rejestrowania źródła danych hello w wykazie danych powoduje toodiscover łatwiejsze hello danych i zrozumienie. Po zarejestrowaniu źródła danych hello można dodawać adnotacje, zarządzanie i go odnaleźć za pomocą portalu wykazu danych hello.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat rejestrowania źródeł danych, zobacz hello [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md) samouczka.
