---
title: aaaLimitations w bazie danych Azure dla programu MySQL | Dokumentacja firmy Microsoft
description: W tym artykule opisano ograniczenia wersji zapoznawczej w bazie danych Azure dla programu MySQL.
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a>Ograniczenia dotyczące bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)
Hello Azure bazy danych dla usługi MySQL znajduje się w publicznej wersji zapoznawczej. Witaj poniższych sekcjach opisano pojemności i limity funkcjonalności hello bazy danych usługi.

## <a name="service-tier-maximums"></a>Maksymalne wartości warstwy usługi
Bazy danych platformy Azure dla programu MySQL ma wiele warstw usług, które można wybrać podczas tworzenia serwera. Aby uzyskać więcej informacji, zobacz [zrozumieć, co jest dostępne w poszczególnych warstwach usług](concepts-service-tiers.md).  

Jest maksymalna liczba połączeń, jednostek obliczeniowych i magazynu w poszczególnych warstwach usług hello wersji zapoznawczej usługi, następująca: 

|                            |                   |
| :------------------------- | :---------------- |
| **Maksymalna liczba połączeń**        |                   |
| Podstawowe 50 obliczeniowe jednostki     | połączenia o szybkości 50    |
| Podstawowe 100 jednostek obliczeń    | połączenia o szybkości 100   |
| Standardowe jednostki 100 obliczeń | połączenia o szybkości 200   |
| Standardowa 200 obliczeniowe jednostki | 300 połączeń   |
| Standardowa 400 obliczeniowe jednostki | 400 połączeń   |
| Standardowa 800 obliczeniowe jednostki | połączenia o szybkości 500   |
| **Obliczeniowe maksymalna liczba jednostek**      |                   |
| Warstwa Podstawowa usług         | 100 jednostek obliczeń |
| Warstwa Standardowa usług      | 800 obliczeniowe jednostki |
| **Maksymalna liczba magazynu**            |                   |
| Warstwa Podstawowa usług         | 1 TB              |
| Warstwa Standardowa usług      | 1 TB              |

Po osiągnięciu zbyt wiele połączeń, może zostać wyświetlony następujący błąd hello:
> Błąd 1040 (08004): Zbyt wiele połączeń

## <a name="preview-functional-limitations"></a>Podgląd ograniczenia funkcjonalności:
### <a name="scale-operations"></a>Operacje skalowania:
1.  Dynamiczne skalowanie serwerów w warstwach usług nie jest obecnie obsługiwane. Oznacza to przełączaniu między Basic i Standard warstwy usług.
2.  Dynamiczne zwiększanie na żądanie magazynu na serwerze utworzone wcześniej nie jest obecnie obsługiwane.
3.  Zmniejszenie rozmiaru magazynu serwera nie jest obsługiwana.

### <a name="server-version-upgrades"></a>Uaktualnienia wersji serwera:
- Automatycznej migracji między wersjami aparatu bazy danych głównych nie jest obecnie obsługiwane.

### <a name="subscription-management"></a>Zarządzanie subskrypcją:
- Dynamicznie przenoszenie serwerów wstępnie utworzone w subskrypcji i grupy zasobów nie jest obecnie obsługiwane.

### <a name="point-in-time-restore"></a>Punkt w — czas — przywracanie:
1.  Przywracanie toodifferent warstwy usług i/lub jednostki obliczeniowe i rozmiaru magazynu nie jest dozwolone.
2.  Przywracanie usuniętej serwera nie jest obsługiwane.

## <a name="next-steps"></a>Następne kroki:
[Co to jest dostępne w poszczególnych warstwach usług](concepts-service-tiers.md)
[obsługiwane wersje bazy danych MySQL](concepts-supported-versions.md)
