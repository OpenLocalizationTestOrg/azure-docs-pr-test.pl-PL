---
title: "Power BI Embedded — połączenia źródła danych tooa aaaMicrosoft"
description: "Power BI Embedded, Połącz toodata źródeł"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Łączenie ze źródłem danych tooa
Z **Power BI Embedded**, raporty można osadzić w aplikacji. Po osadzeniu raportu usługi Power BI w swojej aplikacji hello raport łączy toohello bazowy danych przez **importowania** kopii danych hello lub przez **połączenie bezpośrednio** toohello źródła danych przy użyciu  **Zapytania bezpośredniego**.

Poniżej przedstawiono różnice hello przy użyciu **importu** i **DirectQuery**.

| Import | Tryb DirectQuery |
| --- | --- |
| Tabele, kolumny, *i dane* są importowane lub kopiowane do raportu hello zestawu danych. toosee zmiany danych podstawowych toohello wystąpił, należy odświeżyć lub zaimportować pełny bieżący zestaw danych ponownie. |Tylko *tabel i kolumn* są importowane lub kopiowane do raportu hello zestawu danych. Zawsze Przeglądaj hello najbardziej aktualne dane. |

Z Power BI Embedded możesz za pomocą zapytania bezpośredniego źródeł danych w chmurze, ale nie lokalnych źródeł danych w tej chwili.

> [!NOTE]
> Hello bramy danych lokalnych jest nieobsługiwane w przypadku używania Power BI Embedded w tej chwili. Oznacza to, że nie można użyć zapytania bezpośredniego z lokalnych źródeł danych.

## <a name="supported-data-sources"></a>Obsługiwane źródła danych

**Zapytania bezpośredniego**
* Baza danych SQL Azure
* Azure SQL Data Warehouse

**Importowanie**

Możesz zaimportować przy użyciu wszystkich hello dostępnych źródeł danych w ramach Power BI Desktop. Będzie **nie** być stanie toorefresh danych w usłudze Power BI Embedded. Konieczne będzie tooupload zmiany tooPower BI Embedded plików tooyour PBIX. Jest to powodu toono dostępnej bramy. 

## <a name="benefits-of-using-directquery"></a>Zalety używania zapytania bezpośredniego
Istnieją dwie podstawowe zalety, korzystając z **DirectQuery**:

* **Zapytania bezpośredniego** umożliwia kompilacja z wizualizacji w bardzo dużych zestawów danych, gdzie w przeciwnym razie byłoby importu toofirst będzie niemożliwe, na wszystkich hello danych.
* Bazowy zmian danych może wymagać odświeżenia danych, a w przypadku niektórych raportów hello muszą toodisplay bieżące dane mogą wymagać dużych transferów danych, co będzie niemożliwe ponownego importowania danych. Z kolei **DirectQuery** raporty zawsze używać bieżących danych.

## <a name="limitations-of-directquery"></a>Ograniczenia DirectQuery
   Istnieje kilka ograniczeń toousing **DirectQuery**:

* Wszystkie tabele muszą pochodzić z jednej bazy danych.
* Jeśli zapytanie hello jest zbyt skomplikowane, zostanie przeprowadzona wystąpił błąd. Błąd hello tooremedy musi Refaktoryzuj hello zapytania, jest mniej złożona. Jeśli zapytanie hello musi być złożony, konieczne będzie tooimport hello danych zamiast **DirectQuery**.
* Filtrowanie relacji jest ograniczona tooa w jednym kierunku, a nie w obu kierunkach.
* Nie można zmienić hello typu danych kolumny.
* Domyślnie ograniczenia są umieszczane na dozwolone w miarach wyrażenia języka DAX. Zobacz [zapytania bezpośredniego i środków](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>Zapytania bezpośredniego i miary
zapytania tooensure wysyłane toohello źródła danych ma akceptowalną wydajność, ograniczenia nakłada się na miary. Korzystając z **Power BI Desktop**zaawansowanego użytkownicy mogą wybrać toobypass to ograniczenie, wybierając **Plik > Opcje i Ustawienia > Opcje**. W hello **opcje** okno dialogowe, wybierz **DirectQuery**i wybierz opcję hello **Zezwalaj na nieograniczoną środki w trybie zapytania bezpośredniego**. Gdy ta opcja jest wybrana, można dowolne wyrażenie języka DAX, który jest prawidłowy dla miary. Użytkownicy muszą być świadome; jednak, że niektóre wyrażenia które wykonują bardzo dobrze podczas importowania danych hello może spowodować zacznie działać bardzo wolno zapytania toohello wewnętrznej bazy danych w czasie źródła **DirectQuery** tryb. 

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie do programu Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Program Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)

