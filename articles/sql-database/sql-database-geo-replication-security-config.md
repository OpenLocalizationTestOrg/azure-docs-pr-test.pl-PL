---
title: "aaaConfigure zabezpieczeń bazy danych SQL Azure dla odzyskiwania po awarii | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano zagadnienia dotyczące zabezpieczeń dotyczące konfigurowania i zarządzania zabezpieczeniami po Przywracanie bazy danych lub serwera pomocniczego tooa trybu failover w przypadku hello awarii centrum danych lub innych po awarii"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>Konfigurowanie i zarządzanie nimi zabezpieczenia bazy danych SQL Azure geograficzne lub trybu failover 

> [!NOTE]
> [Aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) jest teraz dostępna dla wszystkich baz danych w warstwach wszystkich usług.
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>Przegląd wymagań uwierzytelniania dla odzyskiwania po awarii
W tym temacie opisano hello uwierzytelniania wymogi tooconfigure i kontroli [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) i hello kroki wymagane tooset użytkownika dostępu toohello pomocniczej bazy danych. Opisano również sposób włączenia odzyskanej bazy danych programu access toohello po użyciu [geograficzne](sql-database-recovery-using-backups.md#geo-restore). Aby uzyskać więcej informacji na temat opcji odzyskiwania, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).

## <a name="disaster-recovery-with-contained-users"></a>Odzyskiwanie po awarii z zawartych użytkowników
W przeciwieństwie do tradycyjnych użytkowników, które muszą być mapowane toologins w bazie danych master hello, zawartego użytkownika zarządza całkowicie hello bazy danych. Ma to dwie korzyści. W przypadku odzyskiwania po awarii hello hello użytkownicy nadal tooconnect toohello nowe głównej bazy danych lub hello odzyskane przy użyciu przywracaniem geograficznym bez przeprowadzania dodatkowej konfiguracji, ponieważ użytkownicy hello zarządza hello bazy danych. Istnieją również potencjalne skalowalności i wydajności korzysta z tej konfiguracji z punktu widzenia logowania. Aby uzyskać więcej informacji, zobacz artykuł [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx) (Użytkownicy zawartej bazy danych — tworzenie przenośnej bazy danych). 

optymalne rozwiązania w zakresie głównym Hello jest zarządzanie hello proces odzyskiwania po awarii na dużą skalę trudniejsza. Jeśli masz wiele baz danych tego powitalne Użyj zawartych w tej samej logowania, obsługa przy użyciu poświadczeń hello użytkowników w wielu baz danych może odwrócić hello zalet zawartych użytkowników. Na przykład hello obrotu zasady haseł wymagają że można wprowadzać zmian stale w wielu baz danych, zamiast zmiany hasła hello logowania hello raz w bazie danych master hello. Z tego powodu, jeśli masz wiele baz danych tego hello Użyj tej samej nazwy użytkownika i hasła, używanie zawartych użytkowników nie jest zalecane. 

## <a name="how-tooconfigure-logins-and-users"></a>Jak tooconfigure logowania i użytkowników
Jeśli używasz logowania i użytkowników (zamiast zawartych użytkowników), należy wykonać dodatkowe kroki tooinsure hello, że istnieje w tej samej nazwy logowania w bazie danych master hello. Witaj poniższych sekcjach podano hello zagadnienia związane i dodatkowe kroki.

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>Konfigurowanie dostępu tooa dodatkowej lub odzyskanej bazy danych użytkowników
Aby hello dodatkowej bazy danych toobe można używać tylko do odczytu dodatkowej i baza danych tooensure właściwy dostęp toohello nowe głównej bazy danych lub hello odzyskane przy użyciu przywracaniem geograficznym hello wzorca bazy danych serwera obiektów docelowych hello musi mieć hello Konfiguracja zabezpieczeń odpowiednich na miejscu przed hello odzyskiwania.

Witaj określonych uprawnień dla każdego kroku są opisane w dalszej części tego tematu.

Przygotowywanie tooa dostępu użytkownika pomocniczy — replikacja geograficzna należy wykonać w ramach konfigurowania — replikacja geograficzna. Przygotowywanie bazy danych toohello przywrócone z magazynu geograficznie dostępu użytkowników, należy wykonać w dowolnej chwili, gdy hello oryginalny serwer jest w trybie online (np. w ramach hello DR Przechodzenie do szczegółów).

> [!NOTE]
> Jeśli nie zostanie over lub geograficzne serwer tooa, który nie ma poprawnego skonfigurowania logowania tooit dostępu będzie kontem administratora serwera toohello ograniczone.
> 
> 

Konfigurowanie logowania na serwerze docelowym hello obejmuje trzy kroki przedstawione poniżej:

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1. Określ nazwy logowania z podstawowej bazy danych programu access toohello:
pierwszym krokiem procesu hello Hello jest toodetermine logowania, które musi zostać skopiowane na serwer docelowy hello. Jest to realizowane przy użyciu pary instrukcji "SELECT", co w hello logicznej głównej bazy danych na serwerze źródłowym hello i w hello głównej bazy danych.

Witaj tylko administrator serwera lub członek hello **LoginManager** roli serwera można określić hello logowania na serwerze źródłowym hello, powitania po instrukcji SELECT. 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

Tylko członek roli bazy danych db_owner hello, hello użytkownika dbo lub administratorem serwera, można określić wszystkich podmiotów użytkownika bazy danych hello w hello podstawowej bazy danych.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2. Znajdź hello identyfikatora SID dla logowania hello w kroku 1:
Na podstawie porównania ilości danych wyjściowych hello hello zapytań z poprzedniej sekcji hello i hello pasujące identyfikatory SID, możesz mapować powitania serwera logowania toodatabase użytkownika. Nazwy logowania, w których użytkownik bazy danych ze zgodnym identyfikatorem SID ma toothat dostępu użytkownika do bazy danych jako główny użytkownik bazy danych. 

Witaj następujące zapytanie może być używane toosee wszystkich podmiotów zabezpieczeń użytkownika hello i ich identyfikatorów SID w bazie danych. Tylko członek hello db_owner bazy danych roli lub serwera administracyjnego można uruchomić tego zapytania.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> Witaj **INFORMATION_SCHEMA** i **sys** użytkownicy mają *NULL* identyfikatorów SID i hello **gościa** identyfikator SID jest **0x00**. Witaj **dbo** identyfikator SID może rozpoczynać się *0x01060000000001648000000000048454*, jeśli hello twórcy bazy danych serwera Witaj, Administratorze zamiast członkiem **dbmanager:**.
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3. Tworzenie identyfikatorów logowania hello na serwerze docelowym hello:
Hello ostatnim krokiem jest serwer docelowy toohello toogo lub serwerów i generować hello logowania z hello odpowiednie identyfikatory SID. Witaj podstawowa ma następującą składnię.

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> Jeśli chcesz toohello dostępu użytkownika toogrant dodatkowej, ale nie toohello podstawowe, możesz to zrobić, zmieniając hello dane logowania użytkownika na serwerze podstawowym hello przy użyciu składni hello.
> 
> ALTER LOGIN <login name> WYŁĄCZ
> 
> Wyłącz nie powoduje zmiany hasła hello, włączyć go zawsze, jeśli to konieczne.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat zarządzania dostęp do bazy danych i logowania do, zobacz [zabezpieczeń bazy danych SQL: Zarządzanie zabezpieczeniami dostępu i nazwy logowania bazy danych](sql-database-manage-logins.md).
* Aby uzyskać więcej informacji dotyczących użytkowników zawartej bazy danych, zobacz [zawarte bazy danych użytkowników — co Twojej bazy danych przenośne](https://msdn.microsoft.com/library/ff929188.aspx).
* Aby uzyskać informacje o użyciu i skonfigurowaniu aktywna replikacja geograficzna, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)
* Informacje o korzystaniu z przywracaniem geograficznym, zobacz [geograficzne](sql-database-recovery-using-backups.md#geo-restore)

