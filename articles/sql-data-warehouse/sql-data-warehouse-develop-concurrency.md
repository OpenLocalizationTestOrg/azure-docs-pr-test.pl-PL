---
title: "Zarządzanie aaaConcurrency i obciążenia w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Zrozumienie zarządzania współbieżności i obciążenia w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>Zarządzanie współbieżności i obciążenia w usłudze SQL Data Warehouse
toodeliver przewidywalnej wydajności na dużą skalę, Magazyn danych SQL Microsoft Azure ułatwia kontrolowanie poziomy współbieżności i alokacji zasobów pamięci i procesora CPU priorytetyzacji. W tym artykule przedstawiono pojęcia toohello współbieżności i obciążenia zarządzania informacjami o tym, jak obie funkcje zostały wdrożone i sposób ich kontroli w magazynie danych. Zarządzanie obciążenie SQL Data Warehouse jest zamierzone toohelp obsługuje środowisku wielu użytkowników. Nie jest przeznaczony dla wielu dzierżawców obciążeń.

## <a name="concurrency-limits"></a>Limity współbieżności
Magazyn danych SQL pozwala się too1, 024 równoczesnych połączeń. Wszystkie połączenia 1024 może przesłać kwerendy jednocześnie. Jednak toooptimize przepustowości, usługa SQL Data Warehouse może kolejka tooensure niektórych zapytań, że każda kwerenda otrzyma grant minimalnej pamięci. Usługi kolejkowania wiadomości występuje w czasie wykonywania zapytania. W zapytaniach kolejkowania podczas współbieżności, które osiągnięciu limitu magazyn danych SQL można zwiększyć ogólnej przepustowości przez zapewnienie, że aktywnych kwerend uzyskać dostęp toocritically potrzebne zasobów pamięci.  

Limity współbieżności są regulowane przez dwa pojęcia: *zapytania jednoczesne* i *współbieżności miejsc*. Dla tooexecute zapytanie należy wykonać w ramach zarówno limit współbieżności zapytania hello i hello współbieżności miejsca alokacji.

* Zapytania jednoczesne są hello zapytań wykonywanych w hello sam czas. Magazyn danych SQL obsługuje zapytania jednoczesne too32 na powitania o większych rozmiarach DWU.
* Współbieżność gniazda są przydzielane oparte na wartości DWU. Każdy 100 DWU zawiera 4 gniazda współbieżności. Na przykład DW100 przydziela 4 gniazda współbieżności i DW1000 przydziela 40. Każde zapytanie zużywa jeden lub więcej współbieżności gniazda, zależy od hello [klasy zasobów](#resource-classes) hello zapytania. Zapytań wykonywanych w klasie zasobu smallrc hello korzystać z jednego gniazda współbieżności. Zapytań wykonywanych w klasie zasobu wyższej zużywać więcej miejsc współbieżności.

Hello poniższej tabeli opisano limity powitania dla zapytania jednoczesne i gniazd współbieżności na powitania różnych rozmiarach DWU.

### <a name="concurrency-limits"></a>Limity współbieżności
| DWU | Maksymalna liczba równoczesnych zapytań | Współbieżność gniazd przydzielonych |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

Po spełnieniu jednego z tych progów, nowego zapytania są umieszczone w kolejce i wykonywane na podstawie FIFO pierwszy w.  Kończy zapytania i hello liczba zapytań i gniazda spadnie poniżej limity hello, są wydawane w kolejce zapytań. 

> [!NOTE]  
> *Wybierz* kwerendy wykonywanie wyłącznie na dynamiczne zarządzanie widoków (widoków DMV) lub widoków wykazu nie podlegają za pomocą dowolnej hello limitów współbieżności. Można monitorować system hello bez uwzględniania hello zapytań wykonywanych na nim.
> 
> 

## <a name="resource-classes"></a>Klasy zasobów
Zasób klas umożliwiają kontrolę alokacją pamięci i cykle procesora CPU podane tooa zapytania. Można przypisać dwa typy zasobów klasy tooa użytkownika w postaci hello ról bazy danych. dwa typy klasy zasobu Hello są następujące:
1. Dynamiczne klasy zasobu (**smallrc, mediumrc, largerc, xlargerc**) przydzielić zmiennej ilość pamięci w zależności od hello bieżącej wartości DWU. Oznacza to, że skalowanie w górę tooa większych DWU zapytań automatycznie pobrać więcej pamięci. 
2. Klasy statyczne zasobów (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) przydzielić hello tego samego ilość pamięci, niezależnie od tego hello bieżącej wartości DWU (pod warunkiem, że hello DWU sam ma za mało pamięci). Oznacza to, że na większą liczbę jednostek dwu, można uruchomić zapytania więcej w każdej klasie zasobów jednocześnie.

Użytkownicy w **smallrc** i **staticrc10** podano mniejszą ilość pamięci i można korzystać z wyższej współbieżności. Z kolei użytkownicy przypisani zbyt**xlargerc** lub **staticrc80** podano duże ilości pamięci, i w związku z tym mniej kwerendy można uruchamiać jednocześnie.

Domyślnie każdy użytkownik jest elementem członkowskim klasy zasobu małych hello **smallrc**. Witaj procedury `sp_addrolemember` jest używana klasa zasobów hello tooincrease i `sp_droprolemember` jest używane klasy zasobu hello toodecrease. Na przykład to polecenie zwiększy klasy zasobu hello loaduser zbyt**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>Zapytania, które nie uznają klasy zasobu

Istnieje kilka typów zapytań, które nie korzystają z większą alokacji pamięci. Hello system ignoruje ich alokacji klasy zasobów i zawsze należy zamiast tego uruchomić te zapytania w klasie zasobu małych hello. Jeśli te zapytania są zawsze uruchamiane w klasie zasobu małych hello, można uruchomić po współbieżności miejsca są wykorzystanie i nie wykorzystują one więcej miejsca niż jest to potrzebne. Zobacz [wyjątki klasy zasobu](#query-exceptions-to-concurrency-limits) Aby uzyskać więcej informacji.

## <a name="details-on-resource-class-assignment"></a>Szczegółowe informacje o przypisanie klasy zasobu


Kilka więcej informacji na temat klasy zasobów:

* *Instrukcja ALTER roli* wymagane jest uprawnienie klasy zasobów hello toochange użytkownika.
* Mimo że można dodawać tooone użytkownika lub więcej hello wyższych klas zasobów, klasy zasobu dynamicznego mają pierwszeństwo przed klas statycznych zasobów. Oznacza to, że jeśli użytkownik jest przypisany tooboth **mediumrc**(dynamiczny) i **staticrc80**(statyczny), **mediumrc** jest klasa zasobu hello jest przestrzegana.
 * Gdy użytkownik jest przypisany toomore niż jeden zasób klasy w typie klasy określonego zasobu (więcej niż jedną klasę zasobu dynamicznego lub więcej niż jednej klasy statyczne zasobów), jest uznawane hello najwyższej klasy zasobów. Oznacza to jeśli użytkownik jest przypisany tooboth mediumrc i largerc, jest uznawane hello wyższej klasy zasobów (largerc). A jeśli użytkownik jest przypisany tooboth **staticrc20** i **statirc80**, **staticrc80** jest go uznać.
* Nie można zmienić klasy zasobu Hello użytkownika administracyjnego hello systemu.

Na przykład szczegółowe, zobacz [przykład klasy zasobów użytkownika Zmiana](#changing-user-resource-class-example).

## <a name="memory-allocation"></a>Alokacja pamięci
Brak tooincreasing zalet i wad klasy zasobów użytkownika. Zwiększanie zasobów klasy dla użytkownika, zapewnia kwerendy dostępu toomore pamięci, co może oznaczać, że szybsze wykonywanie zapytań.  Jednak wyższych klas zasobów również zmniejszyć hello liczby równoczesnych zapytań, które można uruchomić. Jest to hello kompromis między przydzielanie dużych ilości pamięci tooa pojedynczego zapytania lub dopuszczeniem inne zapytania, których alokacji pamięci, jednocześnie toorun może też być konieczne. Jeśli jeden użytkownik otrzymuje wysokiej alokacji pamięci dla zapytania, inne użytkownicy nie będą mieć dostępu toothat toorun pamięci tego samego zapytania.

Witaj w poniższej tabeli mapuje hello pamięci przydzielony dystrybucji tooeach przez klasę DWU i zasobów.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>Alokacje pamięci na dystrybucji dla klasy zasobu dynamicznego (MB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1,600 |
| DW500 |100 |400 |800 |1,600 |
| DW600 |100 |400 |800 |1,600 |
| DW1000 |100 |800 |1,600 |3,200 |
| DW1200 |100 |800 |1,600 |3,200 |
| DW1500 |100 |800 |1,600 |3,200 |
| DW2000 |100 |1,600 |3,200 |6,400 |
| DW3000 |100 |1,600 |3,200 |6,400 |
| DW6000 |100 |3,200 |6,400 |12,800 |

Witaj w poniższej tabeli mapuje hello pamięci przydzielony tooeach dystrybucji przez DWU i klasy statyczne zasobów. Należy pamiętać, że ich pamięci hello wyższych klas zasobów zmniejszona toohonor hello globalne DWU limity.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>Alokacje pamięci na dystrybucji dla klas statycznych zasobów (MB)
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW500 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW600 |100 |200 |400 |800 |1,600 |1,600 |1,600 |1,600 |
| DW1000 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1200 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW1500 |100 |200 |400 |800 |1,600 |3,200 |3,200 |3,200 |
| DW2000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW3000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |6,400 |
| DW6000 |100 |200 |400 |800 |1,600 |3,200 |6,400 |12,800 |

Z powyższej tabeli hello, można stwierdzić, że zapytanie systemem DW2000 w hello **xlargerc** musi too6 dostępu, 400 MB pamięci w każdej z baz danych rozproszonych 60 hello klasy zasobów.  W magazynie danych SQL istnieją dystrybucje 60. W związku z tym toocalculate hello całkowitej ilości pamięci alokacji dla zapytania w klasie zasobu, hello powyżej wartości powinna być pomnożona przez 60.

### <a name="memory-allocations-system-wide-gb"></a>Pamięć alokacji systemowe (GB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

Z tej tabeli alokacji pamięci systemowe widać, że zapytanie systemem DW2000 w klasie zasobu xlargerc hello jest przydzielany łącznie 375 GB pamięci (MB 6400 * 60 dystrybucje / 1024 tooconvert tooGB) w całości hello SQL Data Warehouse.

Witaj te same obliczenia stosuje toostatic klasy zasobów.
 
## <a name="concurrency-slot-consumption"></a>Użycie miejsca współbieżności  
Usługa SQL Data Warehouse przyznaje więcej tooqueries pamięci w wyższej klasy zasobów. Ilość pamięci jest stały zasobów.  W związku z tym hello więcej pamięci przydzielona dla kwerendy, powitalne mniejszej liczby równoczesnych zapytań można wykonać. Witaj poniższej tabeli powtórnie wszystkie poprzednie koncepcji hello w ramach jednego widoku, który pokazuje liczbę hello współbieżności dostępnych przez DWU i gniazda hello wykorzystanych w ramach każdej klasy zasobów.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>Alokacja i użycie gniazd współbieżności dla klasy zasobu dynamicznego  
| DWU | Maksymalna liczba jednoczesnych kwerend | Współbieżność gniazd przydzielonych | Używane przez smallrc gniazd | Używane przez mediumrc gniazd | Używane przez largerc gniazd | Używane przez xlargerc gniazd |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 |20 |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>Alokacja i użycie gniazd współbieżności dla klas statycznych zasobów  
| DWU | Maksymalna liczba jednoczesnych kwerend | Współbieżność gniazd przydzielonych |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

Z tych tabel widać z systemem SQL Data Warehouse jako DW1000 przydziela maksymalnie 32 zapytania jednoczesne i całkowitej 40 gniazd współbieżności. Jeśli wszyscy użytkownicy są uruchomione w smallrc, 32 zapytania jednoczesne będzie dozwolone, ponieważ każde zapytanie będzie używać 1 gniazdo współbieżności. Jeśli wszyscy użytkownicy na DW1000 były uruchomione w mediumrc, każdego zapytania będą przydzielone 800 MB na dystrybucji całkowitej ilości pamięci alokacji 47 GB dla kwerendy i współbieżności będzie ograniczona too5 użytkowników (40 miejsc współbieżności 8 gniazd dla każdego użytkownika mediumrc /).

## <a name="selecting-proper-resource-class"></a>Wybieranie klasy odpowiednich zasobów  
Dobrym rozwiązaniem jest klasa zasobów tooa toopermanently Przypisz użytkowników zamiast zmieniać ich klasy zasobów. Na przykład obciążeń tooclustered magazynu kolumn tabel utworzyć indeksy wyższej jakości przy nadawaniu więcej pamięci. tooensure obciążeń pamięci toohigher dostępu, Utwórz użytkownika specjalnie z myślą o podczas ładowania danych i stałe przypisać ten wyższej klasy zasobów użytkownika tooa.
Istnieje kilka najlepszych toofollow rozwiązań w tym miejscu. Jak wspomniano powyżej, magazynu danych SQL obsługuje dwa rodzaje typu klasy zasobu: klasy statyczne zasobów i klasy zasobu dynamicznego.
### <a name="loading-best-practices"></a>Ładowanie najlepsze rozwiązania
1.  Jeżeli oczekiwania hello obciążeń z regularnych ilość danych, klasy statyczne zasobów jest dobrym rozwiązaniem. Później kiedy skalowaniu tooget więcej moc obliczeniową, Magazyn danych hello będą mogli toorun więcej jednoczesnych wysyła zapytanie out-of--box, jako użytkownik obciążenia hello nie korzystać z większej ilości pamięci.
2.  Jeżeli oczekiwania hello większych obciążeń w niektórych przypadkach, klasa zasobu dynamicznego jest dobrym rozwiązaniem. Później, podczas skalowania w górę tooget więcej mocy obliczeniowej, hello obciążenia użytkownik otrzyma więcej pamięci out-of--box, dlatego stosowanie tooperform obciążenia hello szybciej.

Hello obciążeń tooprocess pamięci potrzebnej wydajnie zależy od charakteru hello tabeli hello załadowany i hello ilości danych przetwarzanych. Na przykład ładowanie danych do tabel WIK wymaga niektórych rowgroups WIK toolet pamięci osiągnąć optymalizacji. Aby uzyskać więcej informacji zobacz indeksy magazynu kolumn hello — wskazówki dotyczące ładowania danych.

Najlepszym rozwiązaniem, zalecamy toouse co najmniej 200MB pamięci dla obciążenia.

### <a name="querying-best-practices"></a>Wykonywanie zapytania najlepsze rozwiązania
Zapytania mają różne wymagania w zależności od złożoności. Zwiększenie ilości pamięci na zapytanie, lub zwiększyć współbieżność hello są obie tooaugment prawidłowe metody ogólną przepustowość w zależności od potrzeb zapytania hello.
1.  Jeżeli oczekiwania hello regularne, złożonych kwerend (na przykład toogenerate dziennego i tygodniowego raportów) i nie ma potrzeby tootake zaletą współbieżności, dobrym rozwiązaniem jest klasa zasobu dynamicznego. Jeśli hello system więcej tooprocess danych, skalowaniu hello hurtowni danych w związku z tym automatycznie zapewni więcej pamięci toohello użytkownika hello kwerendy.
2.  Jeżeli oczekiwania hello wzorców współbieżności dobowej lub zmienna (dla wystąpienia Jeśli hello bazy danych jest poddawany kwerendzie za pośrednictwem interfejsu użytkownika szeroko dostępne w sieci web), klasy statyczne zasobów jest dobrym rozwiązaniem. Później, podczas skalowania toodata magazynowych, hello użytkownika skojarzonego z klasą zasobów statycznych hello zostanie automatycznie można toorun stanie więcej jednoczesnych zapytania.

Wybór przydział pamięci odpowiednie w zależności od potrzeby hello kwerendy jest nieuproszczony, ponieważ zależy on od wielu czynników, takich jak hello ilość danych pobieranych, rodzaj hello hello tabeli schematów i różnych sprzężenia, zaznaczenia i predykaty grupy. Z punktu widzenia ogólne, przydzielenie większej ilości pamięci będą toocomplete zapytania szybsze, ale ograniczy hello ogólną współbieżności. Jeśli współbieżności nie stanowi to problemu, nadmierne przydzielanie pamięci nie uszkodzić. Przepływność strojenia toofine różnych odmian klasy zasobów w trakcie mogą być wymagane.

Można użyć następujących hello przechowywane procedury toofigure limit pamięci i współbieżność grant na klasy zasobów w danej SLO i hello najbliższego najlepsze klasy zasobu operacje o znacznym wykorzystaniu WIK pamięci niepartycjonowany WIK tabeli w klasie zasobu:

#### <a name="description"></a>Opis:  
Oto hello celem tej procedury składowanej:  
1. toohelp użytkownika ustalenie potrzebnej pamięci i współbieżność grant dla klasy zasobu w danym celu SLO. Użytkownik musi tooprovide NULL tablename i schematu, w tym, jak pokazano w poniższym przykładzie hello.  
2. toohelp użytkownika zorientować się hello najbliższego najlepsze klasy zasobu intensed pamięci hello WIK operacji (obciążenia, tabelę kopiowania odbudować indeksu, itp.) z systemem innym niż partycjonowanej tabeli WIK w klasie zasobu. Procedura przechowywana Hello używa toofind schematu tabeli limit hello przydział pamięci wymagana dla tego.

#### <a name="dependencies--restrictions"></a>Zależności i ograniczeń:
- Ten przechowywanej nie jest wymagana ilość pamięci toocalculate zaprojektowane dla WIK podzielona na partycje tabeli.    
- To przechowywanej nie przyjmuje wymagania dotyczące pamięci pod uwagę dla części SELECT hello CTAS/INSERT-wybierz przyjęto założenie, jego toobe wybierz proste.
- Ta przechowywanej używa tabeli tymczasowej, dlatego może być używany w sesji hello której utworzono to przechowywanej.    
- To przechowywanej zależy od bieżącego ofert hello (Konfiguracja sprzętu, konfiguracji DMS) i w przypadku zmiany dowolnego tego następnie tego przechowywanej nie będzie działało poprawnie.  
- Ta przechowywanej zależy od istniejących limit oferowany współbieżności i jeśli zmieni się który następnie tego przechowywanej nie będzie działało poprawnie.  
- Ta przechowywanej zależy od istniejących ofert klasy zasobów i jeśli która zmieni się następnie to przechowywane bezzasadnie proces roboczy nie poprawnie.  

>  [!NOTE]  
>  Jeśli użytkownik nie otrzymuje dane wyjściowe po wykonaniu procedury składowanej z parametrami dostarczonego, może być dwa. <br />1. Parametr albo DW zawiera nieprawidłową wartość SLO <br />2. ALBO nie nie zgodnej klasy zasobu dla operacji WIK Jeśli podano nazwę tabeli. <br />Na przykład w DW100, najwyższy dostępny przydział pamięci to 400MB, a jeśli schemat tabeli jest szeroka za mało toocross hello wymaganie 400MB.
      
#### <a name="usage-example"></a>Przykład użycia:
Składnia:  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Podaj wartość NULL parametru tooextract hello bieżącej wartości DWU z hello bazie danych Magazynu danych lub podaj obsługiwane wszystkie wartości DWU w postaci "DW100" hello
2. @SCHEMA_NAME:Podaj nazwę schematu tabeli hello
3. @TABLE_NAME:Podaj nazwę tabeli hello zainteresowań

Przykłady wykonywania tej procedury przechowywanej:  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

Używane w hello powyżej przykłady Tabela1 mógł zostać utworzony zgodnie z poniższymi instrukcjami:  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Oto Definicja procedury przechowywane hello:
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>Znaczenie zapytania
Usługa SQL Data Warehouse implementuje klasy zasobów za pomocą grupy obciążenia. Brak łącznie osiem obciążenia grupach kontrolujących zachowanie hello klasy zasobu hello między hello różnych rozmiarach DWU. Dla dowolnego DWU usługa SQL Data Warehouse używa tylko czterech hello osiem grup obciążenia. To rozwiązanie ma sens, ponieważ każda grupa obciążenia przypisano tooone cztery klasy zasobu: smallrc mediumrc, largerc, lub xlargerc. Witaj znaczenie opis grup obciążenia hello jest niektóre z tych grup obciążenia ustawiono toohigher *znaczenie*. Znaczenie jest używany dla Procesora planowania. Uruchom o wysokiej ważności zapytania pobierze trzy razy więcej cykli Procesora niż jednostki o średnim znaczeniu. W związku z tym mapowania miejsca współbieżności również określić priorytet procesora CPU. Jeśli zapytanie wykorzystuje co najmniej 16 miejsc, jest on uruchamiany jako wysokiej ważności.

Witaj poniższej tabeli przedstawiono hello mapowania znaczenie dla każdej grupy obciążenia.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>Obciążenie grupy mapowania tooconcurrency gniazda i ważność
| Grupy obciążenia | Mapowanie miejsca współbieżności | MB / dystrybucji | Mapowanie znaczenie |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |Medium |
| SloDWGroupC01 |2 |200 |Medium |
| SloDWGroupC02 |4 |400 |Medium |
| SloDWGroupC03 |8 |800 |Medium |
| SloDWGroupC04 |16 |1,600 |Wysoka |
| SloDWGroupC05 |32 |3,200 |Wysoka |
| SloDWGroupC06 |64 |6,400 |Wysoka |
| SloDWGroupC07 |128 |12,800 |Wysoka |

Z hello **alokacja i użycie gniazd współbieżności** wykresu, można sprawdzić, czy DW500 używa 1, 4, 8 i współbieżność 16 miejsc dla smallrc, mediumrc largerc i xlargerc, odpowiednio. Te wartości można wyszukiwać, w hello poprzedzających wykresu toofind hello znaczenie dla każdej klasy zasobów.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>Mapowanie DW500 tooimportance klasy zasobu
| Klasa zasobów | Grupy obciążenia | Używać miejsc współbieżności | MB / dystrybucji | Znaczenie |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |Medium |
| mediumrc |SloDWGroupC02 |4 |400 |Medium |
| largerc |SloDWGroupC03 |8 |800 |Medium |
| xlargerc |SloDWGroupC04 |16 |1,600 |Wysoka |
| staticrc10 |SloDWGroupC00 |1 |100 |Medium |
| staticrc20 |SloDWGroupC01 |2 |200 |Medium |
| staticrc30 |SloDWGroupC02 |4 |400 |Medium |
| staticrc40 |SloDWGroupC03 |8 |800 |Medium |
| staticrc50 |SloDWGroupC03 |16 |1,600 |Wysoka |
| staticrc60 |SloDWGroupC03 |16 |1,600 |Wysoka |
| staticrc70 |SloDWGroupC03 |16 |1,600 |Wysoka |
| staticrc80 |SloDWGroupC03 |16 |1,600 |Wysoka |

Możesz użyć powitania po toolook zapytania DMV na powitania różnice w alokacji zasobów pamięci szczegółowo z perspektywy hello zarządcy zasobów hello lub tooanalyze active i historyczne użycia grup obciążenia hello podczas rozwiązywania problemów.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>Zapytania, które uwzględnić limity współbieżności
Większość zapytań podlegają klasy zasobów. Te zapytania musi mieścić się w zarówno hello równoczesnych zapytań i progi miejsca współbieżności. Użytkownik nie można wybrać tooexclude zapytania z hello współbieżności miejsca modelu.

tooreiterate, hello następujące instrukcje honorować klasy zasobu:

* WYBIERZ OPCJĘ WSTAWIANIA
* AKTUALIZACJA
* USUŃ
* Wybierz (podczas wykonywania zapytania tabele użytkownika)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* ALTER TABLE REBUILD
* TWORZENIE INDEKSU
* UTWÓRZ KLASTROWANY INDEKS MAGAZYNU KOLUMN
* UTWÓRZ TABLE AS SELECT (CTAS)
* Ładowanie danych
* Operacje przenoszenia danych przeprowadzonych przez hello usługi przenoszenia danych (DMS)

## <a name="query-exceptions-tooconcurrency-limits"></a>Limity tooconcurrency wyjątki zapytania
Niektóre kwerendy, nie uznają zasobów hello klasy toowhich hello użytkownik jest przypisany. Te limity współbieżności toohello wyjątki są wysyłane w przypadku hello zasoby pamięci wymagane dla określonego polecenia jest niskie, często ponieważ polecenie hello jest operacja metadanych. Celem Hello tych wyjątków jest tooavoid większych alokacji pamięci dla zapytań, które nigdy nie będzie je. W takich przypadkach domyślna hello klasy zasobów małe (smallrc) jest zawsze używane niezależnie od klasy zasobów rzeczywistych hello przypisany użytkownik toohello. Na przykład `CREATE LOGIN` zawsze będą uruchamiane w smallrc. toofulfill zasoby wymagane Hello tej operacji są bardzo niskie, więc nie powoduje znaczeniu tooinclude hello zapytania w modelu miejsca współbieżności hello.  Te zapytania również nie są ograniczone limit współbieżności użytkownika hello 32, nieograniczoną liczbę tych zapytań można uruchomić się limit sesji toohello 1024 sesji.

Witaj następujące instrukcje, nie uznają klasy zasobu:

* Utwórz lub DROP TABLE
* INSTRUKCJA ALTER TABLE... PRZEŁĄCZNIK, podziału lub SCALENIA PARTYCJI
* ALTER INDEX WYŁĄCZ
* INDEKS
* Utwórz, aktualizacji lub DROP STATISTICS
* OBCIĄĆ TABELI
* INSTRUKCJA ALTER AUTORYZACJI
* UTWÓRZ DANE LOGOWANIA
* CREATE, ALTER i DROP USER
* CREATE, ALTER i DROP procedury
* Utwórz lub PORZUĆ widok
* WSTAW WARTOŚCI
* Wybierz z widoków systemowych i widoków DMV
* WYJAŚNIĆ
* POLECENIE DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a>Zmiany w przykładzie klasa zasobów użytkownika
1. **Utwórz dane logowania:** Otwórz tooyour połączenia **wzorca** bazy danych na powitania serwera SQL server hostującego bazę danych magazynu danych SQL i wykonywanie hello następujące polecenia.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > W bazie danych master powitania dla użytkowników usługi Azure SQL Data Warehouse jest dobrze toocreate użytkownika. Tworzenie użytkownika w głównym umożliwia toologin użytkownika, za pomocą takich narzędzi jak SSMS bez podawania nazwy bazy danych.  Umożliwia także toouse hello obiektu explorer tooview wszystkich baz danych na serwerze SQL.  Aby uzyskać więcej informacji o tworzeniu i zarządzanie użytkownikami, zobacz [Zabezpieczanie bazy danych w usłudze SQL Data Warehouse][Secure a database in SQL Data Warehouse].
   > 
   > 
2. **Utwórz użytkownika usługi SQL Data Warehouse:** Otwórz toohello połączenia **SQL Data Warehouse** bazy danych i wykonaj następujące polecenie hello.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **Udzielanie uprawnień:** hello następujący przykład przyznaje `CONTROL` na powitania **SQL Data Warehouse** bazy danych. `CONTROL`na powitania poziom bazy danych jest hello równoważne roli db_owner w programie SQL Server.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **Zwiększ klasy zasobów:** Użyj hello następujące zapytanie tooadd tooa wyższe obciążenie Zarządzanie rolą użytkownika.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **Zmniejsz klasy zasobów:** Użyj hello następujące zapytanie tooremove użytkownika z rolą zarządzania obciążenia.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > Nie jest możliwe tooremove użytkownika z smallrc.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>Zapytania w kolejce wykrywania i innych widoków DMV
Można użyć hello `sys.dm_pdw_exec_requests` DMV tooidentify zapytań, które czekają w kolejce współbieżności. Wysyła zapytanie oczekiwanie na gnieździe współbieżności będzie mieć stan **zawieszone**.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

Role związane z zarządzaniem obciążenia mogą być wyświetlane z `sys.database_principals`.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

następujące zapytanie Hello Pokazuje każdy użytkownik jest przypisany do roli.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

Magazyn danych SQL ma następujące hello oczekiwania typów:

* **LocalQueriesConcurrencyResourceType**: zapytania, które znajdują się poza hello współbieżności miejsca framework. Zapytania DMV i systemu, takich jak funkcje `SELECT @@VERSION` przedstawiono przykłady lokalnego zapytań.
* **UserConcurrencyResourceType**: zapytania, które znajdują się wewnątrz hello współbieżności miejsca framework. Zapytania dotyczące tabel użytkownika końcowego przedstawiają przykłady używających tego typu zasobu.
* **DmsConcurrencyResourceType**: czeka, wynikające z operacji przenoszenia danych.
* **BackupConcurrencyResourceType**: ten oczekiwania wskazuje, że bazy danych jest tworzona kopia zapasowa. Witaj maksymalna wartość dla tego typu zasobu to 1. Jeśli zażądano wiele kopii zapasowych na powitania tym samym czasie, hello innych może umieścić w kolejce.

Witaj `sys.dm_pdw_waits` DMV może być toosee używanych zasobów, do których żądanie oczekuje.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

Witaj `sys.dm_pdw_resource_waits` DMV pokazuje tylko zasobów hello czeka używane przez określonego zapytania. Czas oczekiwania zasobu tylko środków hello czasu oczekiwania na zasoby toobe pod warunkiem, jak min. toosignal oczekiwania czas, który określa czas hello zajmuje hello podstawowej SQL serwerów tooschedule hello kwerendy na powitania Procesora.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

Witaj `sys.dm_pdw_wait_stats` DMV może służyć do analizy trendów historycznych oczekiwania.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o zarządzaniu bazy danych użytkowników i zabezpieczeń, zobacz [Zabezpieczanie bazy danych w usłudze SQL Data Warehouse][Secure a database in SQL Data Warehouse]. Aby uzyskać więcej informacji na temat sposobu większe grupy zasobów może zwiększyć jakość indeksu klastrowanego magazynu kolumn, zobacz [odbudowywania indeksów tooimprove segmentu jakości].

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[odbudowywania indeksów tooimprove segmentu jakości]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
