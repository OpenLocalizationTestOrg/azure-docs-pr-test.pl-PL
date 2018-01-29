---
title: "Minimalizująca przestoje migracji do bazy danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób przeprowadzenia migracji minimalnym czasem przestojów bazy danych programu MySQL do bazy danych platformy Azure dla programu MySQL i konfigurowanie ładowania początkowego i synchronizacji danych ciągłego źródłowej bazy danych do docelowej bazy danych przy użyciu replikacji Attunity firmy Microsoft Migracji."
services: mysql
author: HJToland3
ms.author: jtoland
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 01/04/2018
ms.openlocfilehash: d23628fd8446f6e7e0e5ed14b98da13c09b2d592
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/24/2018
---
# <a name="minimal-downtime-migration-to-azure-database-for-mysql"></a>Minimalizująca przestoje migracji do bazy danych Azure dla programu MySQL
Przy użyciu replikacji Attunity Migrations Microsoft istniejącej bazy danych MySQL można migrować do bazy danych platformy Azure dla programu MySQL. Replikacja Attunity jest wspólnego z Attunity i firmy Microsoft. Wraz z usługi migracji bazy danych Azure jest uwzględniony bez ponoszenia dodatkowych kosztów do klientów firmy Microsoft. 

Replikacja Attunity minimalizuje czas przestoju podczas migracji bazy danych, a źródłowa baza danych zachowuje operacyjne całego procesu.

Replikacja Attunity to narzędzie replikacji danych, które umożliwia synchronizacji danych między z różnych źródeł i obiektów docelowych. Propaguje on skrypcie tworzenia schematu i dane skojarzone z każdej tabeli bazy danych. Replikacja Attunity nie są propagowane innych artefakty (na przykład SP, wyzwalacze, funkcje i tak dalej) lub konwersji, na przykład, kod PL/SQL, który znajduje się w takich artefaktów do T-SQL.

> [!NOTE]
> Mimo że replikacja Attunity obsługuje szeroką gamę scenariuszy migracji, koncentruje się na obsługę konkretnego podzestawu par źródłowy i docelowy.

Zawiera omówienie procesu migracji minimalnym czasem przestojów:

* **Migrowanie schematu źródła MySQL** bazą danych Azure dla programu MySQL zarządzane usługi bazy danych przy użyciu [MySQL Workbench](https://www.mysql.com/products/workbench/).

* **Ustawienie ładowania początkowego i przeprowadź synchronizację z ciągłymi danymi ze źródłowej bazy danych do docelowej bazy danych** przy użyciu replikacji Attunity Migrations firmy Microsoft. Dzięki temu minimalizuje czas, który źródłowej bazy danych musi być ustawiona jako tylko do odczytu podczas przygotowywania do przełączania aplikacji docelowej bazy danych MySQL na platformie Azure.

Aby uzyskać więcej informacji o replikacji Attunity Migrations Microsoft oferty zobacz następujące zasoby:
 - Przejdź do [replikacja Attunity Migrations Microsoft](https://aka.ms/attunity-replicate) strony sieci Web.
 - Pobierz [Attunity replikacji dla migracji w programie Microsoft](http://discover.attunity.com/download-replicate-microsoft-lp6657.html).
 - Przejdź do [Attunity replikować społeczności](https://aka.ms/attunity-community) Przewodnik Szybki Start, samouczki i pomocy technicznej.
 - Aby uzyskać instrukcje na temat używania replikowania Attunity migrację bazy danych MySQL do bazy danych platformy Azure dla programu MySQL, zobacz [Przewodnik po migracji bazy danych](https://datamigration.microsoft.com/scenario/mysql-to-azuremysql).