---
title: "aaaConstructing filtru ciągów dla projektanta tabel hello | Dokumentacja firmy Microsoft"
description: "Utworzenie filtru ciągów dla projektanta tabel hello"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a>Konstruowanie ciągach filtru dla hello projektanta tabel
## <a name="overview"></a>Omówienie
Visual Studio hello toofilter dane w tabeli platformy Azure, która jest wyświetlana w **projektanta tabel**, utworzyć ciąg filtru i wprowadzić go w polu filtru hello. Składnia ciągu filtru Hello jest definiowana za pomocą hello usługi danych WCF i jest podobne tooa klauzuli SQL WHERE, ale są wysyłane toohello usługi tabel za pomocą żądania HTTP. Witaj **projektanta tabel** dojść hello kodowanie odpowiednie dla Ciebie tak toofilter na wartość żądanej właściwości, należy wprowadzić tylko nazwa właściwości hello, operator porównania wartości kryteriów i opcjonalnie można filtrować operator logiczny w hello pole. Nie ma potrzeby opcji zapytania hello $filter tooinclude, jak w przypadku, jeśli zostały tworzenia tabeli hello tooquery adresu URL za pośrednictwem hello [dokumentacja interfejsu API REST usług magazynu](http://go.microsoft.com/fwlink/p/?LinkId=400447).

Usługi danych WCF Hello są oparte na powitania [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Szczegółowe informacje na temat opcji zapytania system filtru hello (**$filter**), zobacz hello [specyfikacji Konwencji identyfikatora URI OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Operatory porównania
Witaj następujące operatory logiczne są obsługiwane dla wszystkich typów właściwości:

| Operator logiczny | Opis | Przykład ciąg filtru |
| --- | --- | --- |
| EQ |Równości |Eq Miasto "Redmond" |
| gt |Więcej niż |Cena gt 20 |
| GE |Większe lub równe zbyt|Cena ge 10 |
| lt |Mniej niż |Cena lt 20 |
| le |Mniejsze niż lub równe |Cena le 100 |
| ne |Nie ma wartości |Ne Miasto "Londyn" |
| i |I |Cena le 200 i cen gt 3.5 |
| lub |Lub |Cena le 3.5 lub gt cen 200 |
| nie |nie |nie isAvailable |

Podczas konstruowania ciąg filtru, hello następujące reguły są ważne:

* Użyj hello operatorów logicznych toocompare tooa wartości właściwości. Należy pamiętać, że nie jest możliwe toocompare wartość dynamiczna tooa właściwości; po jednej stronie powitania wyrażenie musi być stałą.
* Wszystkie części hello ciąg filtru jest rozróżniana wielkość liter.
* musi być wartością stałą Hello hello tych samych danych typu jako właściwość hello aby hello filtru tooreturn prawidłowe wyniki. Aby uzyskać więcej informacji na temat typów obsługiwanych właściwości zobacz [hello opis modelu danych usługi tabel](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Filtrowanie właściwości ciągu
Podczas filtrowania na właściwości ciągów, ujmij stała ciąg hello w pojedynczy cudzysłów.

następujące przykładowe filtry na powitania Hello **PartitionKey** i **RowKey** właściwości; dodatkowe niekluczowych właściwości można również dodawać ciąg filtru toohello:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Każde wyrażenie filtru można ująć w nawiasach, chociaż nie jest to wymagane:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Zauważ, że hello usługi tabel nie obsługuje symboli wieloznacznych zapytań, i nie są obsługiwane w hello projektanta tabel albo. Można jednak wykonać Dopasowywanie przy użyciu operatorów na prefiksie żądaną hello prefiksów. Witaj poniższy przykład zwraca jednostki z nazwisko właściwość rozpoczynająca się od litery hello "A":

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Filtrowanie właściwości liczbowych
toofilter na liczbą całkowitą lub liczba zmiennoprzecinkowa, określ numer hello bez znaków cudzysłowu.

W tym przykładzie zwraca wszystkie jednostki z właściwością wieku, którego wartość jest większa niż 30:

    Age gt 30

W tym przykładzie zwraca wszystkie jednostki z właściwością AmountDue, którego wartość jest mniejsza niż lub równa too100.25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Filtrowanie operatory logiczne
Określ toofilter na wartość logiczną **true** lub **false** bez znaków cudzysłowu.

Witaj poniższy przykład zwraca wszystkie jednostki którym hello IsActive właściwości ustawiono zbyt**true**:

    IsActive eq true

Można również napisać tego wyrażenia filtru bez hello operatora logicznego. W hello poniższy przykład, hello usługi tabel zwrócone zostaną również wszystkie jednostki w przypadku IsActive **true**:

    IsActive

wszystkie jednostki, w którym IsActive ma wartość false, można użyć hello nie tooreturn operator:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>Filtrowanie właściwości daty i godziny
toofilter na wartość daty i godziny, określ hello **datetime** — słowo kluczowe, następuje hello Stała daty/godziny w pojedynczy cudzysłów. Stała daty/godziny Hello musi być w formacie UTC połączone, zgodnie z opisem w [formatowania wartości właściwości data/godzina](http://go.microsoft.com/fwlink/p/?LinkId=400449).

Hello poniższy przykład zwraca jednostki, w których właściwość CustomerSince hello jest tooJuly równy 10, 2008:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
