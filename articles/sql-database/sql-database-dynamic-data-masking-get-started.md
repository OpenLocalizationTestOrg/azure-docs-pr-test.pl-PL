---
title: Maskowanie danych dynamicznych bazy danych SQL aaaAzure | Dokumentacja firmy Microsoft
description: "Maskowanie danych dynamicznych bazy danych SQL ogranicza ujawnienie danych poufnych przez maskowania go toonon uprawnieniami użytkowników"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>Maskowanie danych dynamicznych bazy danych SQL

Maskowanie danych dynamicznych bazy danych SQL ogranicza ujawnienie danych poufnych przez maskowania go toonon uprawnieniami użytkowników. 

Maskowanie danych dynamicznych zapobiega danych toosensitive nieautoryzowanego dostępu, umożliwiając klientom toodesignate ile hello tooreveal poufnych danych przy minimalnym wpływie na warstwie aplikacji hello. Jest to funkcja zabezpieczeń opartych na zasadach, która ukrywa hello poufne dane zawarte w hello zestawu wyników zapytania za pośrednictwem pola wyznaczonych bazy danych, gdy hello danych w bazie danych hello nie ulega zmianie.

Na przykład z przedstawicielem w gnieździe wywołanie może identyfikować obiekty wywołujące kilka cyfry numeru karty kredytowej, ale te dane, które elementy nie powinny być całkowicie widoczne toohello działu obsługi. Czy wszystkie maski, ale hello cztery ostatnie cyfry żadnych numer karty kredytowej w zestawie wyników hello wszelkie zapytania można zdefiniować reguł maskowania. Inny przykład maska odpowiednie dane można tooprotect określonych danych osobowych (dane osobowe), dzięki czemu deweloper może wysyłać zapytania środowisk produkcyjnych w celu rozwiązywania problemów bez naruszania przepisy dotyczące zgodności.

## <a name="sql-database-dynamic-data-masking-basics"></a>Baza danych SQL dynamiczne maskowanie podstawowe informacje o danych
Należy skonfigurować dane dynamiczne maskowanie zasad w hello portalu Azure, wybierając hello dynamiczne maskowanie operacji w bloku konfiguracji bazy danych SQL lub bloku ustawienia danych.

### <a name="dynamic-data-masking-permissions"></a>Uprawnienia maskowania danych dynamicznych
Witaj, Administratorze bazy danych Azure, administrator serwera lub role zabezpieczeń urzędnika można skonfigurować maskowania danych dynamicznych.

### <a name="dynamic-data-masking-policy"></a>Zasady maskowania danych dynamicznych
* **Użytkownicy SQL wykluczeni z maskowania** — zestaw A użytkownicy SQL lub tożsamości usługi AAD, pobierające dane zamaskowana w hello SQL wyniki zapytania. Użytkownicy z uprawnieniami administratora są zawsze wykluczeni z maskowania i zobacz hello oryginalnych danych bez żadnych maski.
* **Maskowanie reguły** — zestaw reguł, które definiują Witaj wyznaczone toobe pola maskowane i hello maskowania funkcji, które jest używane. Witaj wyznaczone pól mogą być definiowane przy użyciu nazwy schematu bazy danych oraz nazwę tabeli i nazwę kolumny.
* **Funkcji maskowania** — zestaw metody, które kontrolują hello ujawnienia danych dla różnych scenariuszy.

| Funkcja maskowania | Logika maskowania |
| --- | --- |
| **Domyślne** |**Pełne maskowanie danych toohello zgodnie z typów hello wyznaczone pola**<br/><br/>• Użyj XXXX lub mniej Xs Jeśli hello rozmiar pola hello jest mniejszy niż 4 znaki dla danych typu ciąg (nchar, ntext, nvarchar).<br/>• Użyj wartości 0 dla typów danych liczbowych (bigint, bit, decimal, int, pieniądze, liczbowe, smallint, smallmoney, tinyint, float, rzeczywistym).<br/>• Użyj 01-01-1900 dla typów danych daty i godziny (Data, datetime2, datetime, datetimeoffset, smalldatetime, czas).<br/>• SQL variant, hello domyślne wartości bieżącego typu hello jest używany.<br/>• Dla dokumentu XML hello <masked/> jest używany.<br/>• Na użytek pustą wartość specjalne typy danych (tabeli sygnatury czasowej, hierarchyid, GUID, binary, obraz, typy przestrzenne varbinary). |
| **Karty kredytowej** |**Maskowanie metodę, która przedstawia hello cztery ostatnie cyfry Witaj wyznaczone pola** i dodaje ciąg stałej jako prefiksu w postaci hello karty kredytowej.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **Adres e-mail** |**Maskowanie metodę, która przedstawia hello pierwszą literę i zastępuje domeny hello XXX.com** przy użyciu prefiksu stałym ciągiem w postaci hello adresu e-mail.<br/><br/>aXX@XXXX.com |
| **Liczby losowe** |**Metoda, która generuje losową liczbę maskowania** zgodnie z toohello wybrane granice i typy danych rzeczywistych. Witaj wyznaczone granice są równe, funkcja maskowania hello jest stałej liczbowej.<br/><br/>![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **Niestandardowy tekst** |**Metoda, która ujawnia hello najpierw i ostatnich znaków maskowania** i dodaje ciąg niestandardowego dopełnienie w środku hello. Jeśli oryginalny ciąg hello jest krótszy niż hello widoczne prefiksu i sufiksu, tylko hello dopełnienie ciąg jest używany. <br/>sufiks prefiks [dopełnienie]<br/><br/>![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>Zalecane pola toomask
Witaj DDM aparat zalecenia, flagi pewnych pól z bazy danych jako potencjalnie poufnych pola, które mogą być odpowiednimi obiektami do maskowania. W hello blok dynamiczne maskowanie danych w portalu hello zobaczysz hello zalecane kolumny bazy danych. Toodo wystarczy kliknąć **Dodaj maskę** dla co najmniej jedną kolumnę, a następnie **zapisać** tooapply maskę dla tych pól.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>Konfigurowanie dynamiczne maskowanie danych dla bazy danych przy użyciu poleceń cmdlet programu Powershell
Zobacz [polecenia cmdlet bazy danych Azure SQL](https://msdn.microsoft.com/library/azure/mt574084.aspx).

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>Konfigurowanie maskowania danych dynamicznych dla bazy danych przy użyciu interfejsu API REST
Zobacz [operacje dla baz danych Azure SQL](https://msdn.microsoft.com/library/dn505719.aspx).

