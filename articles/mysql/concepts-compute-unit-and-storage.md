---
title: "Wyjaśniający obliczeniowe jednostki w bazie danych systemu Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Bazę danych systemu Azure dla programu MySQL: w tym artykule opisano pojęcia hello obliczeniowe jednostki i co się dzieje, gdy osiągnie obciążenie hello maksymalną liczbę jednostek obliczeniowe."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 751b4fff2760e55565e2bc80d49db17a57397779
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a>Wyjaśniający jednostki obliczeń w bazie danych systemu Azure dla programu MySQL
W tym artykule opisano pojęcia hello obliczeniowe jednostki i co się dzieje, gdy osiągnie Twoje obciążenie hello maksymalną liczbę jednostek obliczeniowe.

## <a name="what-are-compute-units"></a>Co to są jednostki obliczeniowe?
Obliczeniowe jednostki to miara przepływności przetwarzania procesora CPU, który jest gwarantowana tooa dostępne toobe pojedynczy MySQL serwera bazy danych Azure. Do obliczenia jest mieszanych pomiarach procesora CPU i zasobów pamięci. Ogólnie rzecz biorąc 50 jednostek obliczeniowe są równoważne toohalf rdzenia. 100 jednostek obliczeniowe są równoważne tooone core. 2000 jednostki obliczeniowe są równoważne rdzeni tootwenty gwarantowane przetwarzanie przepływności tooyour dostępności serwera.

Witaj ilość pamięci na jednostkę obliczeniowe jest zoptymalizowana pod kątem hello Basic i Standard warstw cenowych. Podwojenie hello obliczeniowe jednostki po podniesieniu poziomu wydajności hello oznacza zestaw hello toodoubling toothat dostępnych zasobów pojedyncze bazy danych platformy Azure dla programu MySQL.

Na przykład standardowe jednostki obliczeniowe 800 obejmuje 8 x więcej przepływności procesora CPU i pamięci niż konfiguracji jednostek Standard obliczeniowe 100. Jednak podczas zapewniają standardowe jednostki obliczeniowe 100 hello sama wydajność procesora CPU w porównaniu jednostki obliczeniowe tooBasic 100, double hello ilość pamięci skonfigurowanej dla warstwy cenowej Basic jest hello ilość pamięci, który jest wstępnie skonfigurowana w standardowej warstwie cenowej. W związku z tym warstwa cenowa standardowa zapewnia lepszą wydajność obciążeń i mniejsze opóźnienia transakcji niż podstawowa warstwy cenowej hello wybranych w tej samej jednostki obliczeniowe.

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>Jak ustalić, liczba hello jednostek obliczeniowe potrzebne do mojego obciążenie?
Jeśli szukasz toomigrate istniejącego serwera MySQL uruchamiane lokalnie lub na maszynie wirtualnej, można określić szacowaną liczbę rdzeni przepływności przetwarzania obciążenie musi hello liczbę jednostek obliczeniowe. 

Jeśli z istniejącym lokalnym lub serwerze maszyny wirtualnej jest obecnie przy użyciu 4 rdzenie (bez zliczanie hiperwątkowości Procesora), należy uruchomić konfigurując 400 jednostek obliczeniowe bazy danych Azure, aby serwer MySQL. Jednostki obliczeniowe można dynamicznie skalować w górę lub w dół w zależności od potrzeb obciążenia praktycznie bez przestojów aplikacji. 

Wykres metryki hello monitora w hello Azure zapisu lub portalu Azure CLI polecenia - toomeasure obliczeniowe jednostki. Toomonitor odpowiednich metryk są procent obliczeniowe jednostki hello i limit obliczeniowe jednostki.

>[!IMPORTANT]
> Odnalezienie magazynu IOPS nie są pełni wykorzystane maksymalna toohello należy rozważyć monitorowanie wykorzystania jednostki obliczeniowe hello również. Wywoływanie hello jednostki obliczeniowe mogą zezwalać na wyższej przepustowości we/wy przez zmniejszenie hello wąskie gardło toolimited procesora CPU lub pamięci.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>Co się stanie po naciśnięciu I Moje maksymalną liczbę jednostek obliczeniowe?
Poziomy wydajności są kalibrować i postanowieniom toorun zasobów tooprovide obciążenie się toohello max limitów hello wybrana warstwa cenowa i poziom wydajności bazy danych. 

Jeśli obciążenie osiągnie maksymalną wartością hello w albo hello obliczeniowe jednostki lub elastycznie limity liczby, można kontynuować tooutilize hello zasobów na powitania maksymalny dozwolony poziom, ale zapytań są prawdopodobnie toosee zwiększyć opóźnienia. Te limity nie powodują błędy, ale raczej spowolnienie obciążenia pracą hello, chyba że spowolnienie hello staje się tak poważne, który odpytuje upłynął limit czasu. 

Jeśli obciążenie osiągnie hello limity maksymalną liczbę połączeń, pojawienia się jawne błędy. Aby uzyskać więcej informacji na ograniczenia zasobów, zobacz [ograniczenia w bazie danych Azure dla programu MySQL](concepts-limits.md).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o cenach warstw, zobacz [bazy danych Azure dla programu MySQL warstw cenowych](./concepts-service-tiers.md).
