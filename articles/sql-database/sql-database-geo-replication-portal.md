---
title: 'Portalu Azure: replikacja geograficzna bazy danych SQL | Dokumentacja firmy Microsoft'
description: "Skonfiguruj — replikacja geograficzna bazy danych SQL Azure w hello portalu Azure i zainicjuj tryb failover"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Skonfiguruj aktywna replikacja geograficzna bazy danych SQL Azure w hello portalu Azure i zainicjuj tryb failover

W tym artykule opisano sposób tooconfigure aktywna replikacja geograficzna bazy danych SQL w hello [portalu Azure](http://portal.azure.com) i tooinitiate trybu failover.

tryb failover tooinitiate z hello portalu Azure, zobacz [zainicjować planowanego lub nieplanowanego trybu failover dla bazy danych SQL Azure z portalu Azure hello](sql-database-geo-replication-portal.md).

tooconfigure aktywna replikacja geograficzna przy użyciu hello portalu Azure, należy hello następujących zasobów:

* Baza danych Azure SQL: podstawowej bazy danych hello, które mają tooreplicate tooa inny region geograficzny.

> [!Note]
Aktywna replikacja geograficzna musi należeć do zakresu od baz danych w hello tej samej subskrypcji.

## <a name="add-a-secondary-database"></a>Dodać pomocniczą bazę danych
Hello następujące kroki tworzenia nowego pomocniczej bazy danych współpracują — replikacja geograficzna.  

tooadd pomocniczej bazy danych musi być właścicielem subskrypcji hello lub współwłaściciel.

Hello dodatkowej bazy danych ma takie same nazwy co podstawowa baza danych: hello hello i domyślnie ma hello tego samego poziomu usług. Witaj dodatkowej bazy danych może być pojedynczą bazę danych lub bazę danych w puli elastycznej. Aby uzyskać więcej informacji, zobacz [warstw usług](sql-database-service-tiers.md).
Po utworzeniu i rozpoczęta hello dodatkowej, rozpoczyna się danych replikacji z hello podstawowej bazy danych toohello nowe pomocnicze bazy danych.

> [!NOTE]
> (Na przykład w wyniku zakończenia dotychczasowej relacji replikacji geograficznej) istnieje już baza danych partnera hello hello polecenie kończy się niepowodzeniem.
> 

1. W hello [portalu Azure](http://portal.azure.com), Przeglądaj toohello bazy danych, które mają tooset dla replikacji geograficznej.
2. Na stronie bazy danych SQL hello zaznacz **— replikacja geograficzna**, a następnie wybierz hello region toocreate hello dodatkowej bazy danych. Można wybrać dowolny region niż region hello hosting hello podstawowej bazy danych, ale zaleca się hello [sparowanego region](../best-practices-availability-paired-regions.md).
   
    ![Konfigurowanie replikacji geograficznej](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Wybierz lub skonfiguruj serwer hello i warstwę cenową dla hello pomocniczej bazy danych.
   
    ![Konfigurowanie dodatkowej](./media/sql-database-geo-replication-portal/create-secondary.png)
4. Opcjonalnie można dodać puli elastycznej tooan dodatkowej bazy danych. toocreate hello dodatkowej bazy danych w puli, kliknij przycisk **puli elastycznej** i wybierz pulę na powitania serwera docelowego. Pula musi już istnieć na serwerze docelowym hello. Ten przepływ pracy nie powoduje utworzenia puli.
5. Kliknij przycisk **Utwórz** tooadd hello dodatkowej.
6. Witaj dodatkowej baza danych została utworzona i rozpocznie się hello wstępne wypełnianie procesu.
   
    ![Konfigurowanie dodatkowej](./media/sql-database-geo-replication-portal/seeding0.png)
7. Po zakończeniu hello wstępne wypełnianie procesu hello dodatkowej bazy danych wyświetla jego stan.
   
    ![Wstępne wypełnianie ukończone](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Zainicjuj tryb failover

Hello dodatkowej bazy danych mogą być wyłączone toobecome hello podstawowego.  

1. W hello [portalu Azure](http://portal.azure.com), Przeglądaj toohello podstawowej bazy danych w partnerstwie — replikacja geograficzna hello.
2. W bloku bazy danych SQL hello, wybierz **wszystkie ustawienia** > **— replikacja geograficzna**.
3. W hello **pomocniczych** listy, wybierz opcję hello bazy danych ma toobecome hello nową podstawową, a następnie kliknij przycisk **pracy awaryjnej**.
   
    ![tryb failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Kliknij przycisk **tak** toobegin hello w tryb failover.

polecenie Hello natychmiast przełącza hello dodatkowej bazy danych do roli podstawowego hello. 

Istnieje krótki okres, podczas którego obie bazy danych są niedostępne (w kolejności hello 0 sekund too25) podczas przełączania hello ról. Jeśli hello podstawowej bazy danych ma wiele baz danych w dodatkowej, polecenie hello automatycznie Rekonfiguruj hello innych pomocniczych tooconnect toohello nową podstawową. cała operacja Hello powinno zająć mniej niż minutę toocomplete w normalnych okolicznościach. 

> [!NOTE]
> To polecenie jest przeznaczona dla Szybkie odzyskiwanie bazy danych hello w razie awarii. Wyzwala trybu failover bez synchronizacji danych (wymuszone trybu failover).  Jeśli podstawowy hello jest w trybie online i zatwierdzania transakcji po wydaniu polecenia hello utratę danych mogą wystąpić. 
> 
> 

## <a name="remove-secondary-database"></a>Usuń z dodatkowej bazy danych
Ta operacja kończy trwale hello replikacji toohello dodatkowej bazy danych, i zmiany hello roli hello dodatkowej tooa zwykłej bazy danych do odczytu / zapisu. Jeśli hello łączności toohello dodatkowej bazy danych jest uszkodzona, polecenie hello zakończy się pomyślnie, ale hello dodatkowej ma staje się odczytu i zapisu do po przywróceniu łączności.  

1. W hello [portalu Azure](http://portal.azure.com), Przeglądaj toohello podstawowej bazy danych w partnerstwie — replikacja geograficzna hello.
2. Na stronie bazy danych SQL hello zaznacz **— replikacja geograficzna**.
3. W hello **pomocniczych** listy, wybierz hello bazy danych ma tooremove z hello — replikacja geograficzna powiązania.
4. Kliknij przycisk **Zatrzymaj replikację,**.
   
    ![Usuń pomocniczej](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. Zostanie wyświetlone okno potwierdzenia. Kliknij przycisk **tak** tooremove hello z bazy danych z hello — replikacja geograficzna powiązania. (Ustaw tooa Odczyt i zapis z bazy danych nie jest częścią replikacji.)

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat aktywna replikacja geograficzna, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md).
* Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).

