---
title: "Pojęcia dotyczące wysokiej dostępności w bazie danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera informacje o wysokiej dostępności, podczas korzystania z bazy danych platformy Azure dla programu MySQL"
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 10/31/2017
ms.openlocfilehash: 5b63a1ac666a14354b5b93f22722b624244a7aa2
ms.sourcegitcommit: 43c3d0d61c008195a0177ec56bf0795dc103b8fa
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2017
---
# <a name="high-availability-concepts-in-azure-database-for-mysql"></a>Pojęcia dotyczące wysokiej dostępności w bazie danych Azure dla programu MySQL
Baza danych Azure dla usługi MySQL zapewnia gwarantowane wysoki poziom dostępności. Finansowo kopii umowy dotyczącej poziomu usług (SLA) jest 99,99% po ogólnej dostępności. Nie ma praktycznie żadnej aplikacji czas przestoju podczas korzystania z tej usługi.

## <a name="high-availability"></a>Wysoka dostępność
Model o wysokiej dostępności (HA) opiera się na wbudowane mechanizmy awaryjnej po wystąpieniu przerwy poziomu węzła. Przerwanie węzeł na poziomie może wystąpić z powodu awarii sprzętu lub w odpowiedzi na wdrożenie usługi.

Przez cały czas zmiany wprowadzone do bazy danych Azure dla serwera bazy danych MySQL występuje w kontekście transakcji. Zmiany są rejestrowane w synchronicznie w magazynie Azure, gdy transakcja została przekazana. W przypadku przerwania węzeł na poziomie serwera bazy danych automatycznie tworzy nowy węzeł i dołącza magazynu danych do nowego węzła. Wszystkie aktywne połączenia są usuwane i wszystkich transakcji porządkowych nie są przekazywane.

## <a name="application-retry-logic-is-essential"></a>Ważne jest Logika ponawiania aplikacji
Jest MySQL aplikacje baz danych są przeznaczone do wykrywania i spróbuj ponownie usunąć połączenia i nie powiodło się transakcji. Ponawia próby aplikacji, połączenia aplikacji niewidocznie jest przekierowywany do nowo utworzone wystąpienie, które ma dla tego wystąpienia nie powiodło się.

Na platformie Azure, brama jest używana wewnętrznie przekierowywanie połączeń do nowego wystąpienia. Po przerwaniu cały proces awaryjnej zwykle trwa dziesiątki sekund. Ponieważ przekierowania jest obsługiwany wewnętrznie przez bramę, ciąg połączenia zewnętrzne jest taka sama dla aplikacji klienckich.

## <a name="scaling-up-or-down"></a>Skalowanie w górę lub w dół
Podobnie jak w modelu wysokiej dostępności bazy danych Azure dla programu MySQL skalowania w górę lub w dół, nowe wystąpienie serwera o określonym rozmiarze jest tworzony. Istniejący magazyn danych jest odłączona od oryginalnego wystąpienia i dołączona do nowego wystąpienia.

Podczas operacji skalowania odbywa się zakłócenia połączenia bazy danych. Aplikacje klienckie są odłączone i otwórz niezatwierdzone transakcje są anulowane. Gdy aplikacja kliencka ponowi próbę połączenia lub tworzy nowe połączenie, brama kieruje połączenia z wystąpieniem o nowym rozmiarze. 

## <a name="next-steps"></a>Następne kroki
- Aby zapoznać się z omówieniem usługi, zobacz [Azure bazy danych MySQL — omówienie](overview.md)
