---
title: "aaaAzure kopii zapasowej dla obciążeń programu SQL Server za pomocą programu DPM | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toobacking zapasową baz danych programu SQL Server przy użyciu usługi Kopia zapasowa Azure hello"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli
editor: 
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: ba78dbf1c7934a259a7bd0bdb7d4467ac75d05a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-as-a-dpm-workload"></a>Tworzenie kopii zapasowej programu SQL Server tooAzure jako obciążenia programu DPM
W tym artykule poprowadzi Cię przez kroki konfiguracji hello do utworzenia kopii zapasowej bazy danych programu SQL Server przy użyciu usługi Kopia zapasowa Azure.

tooback się tooAzure baz danych programu SQL Server, należy konta platformy Azure. Jeśli nie masz konta, możesz utworzyć bezpłatne konto próbne w tylko kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

Zarządzanie Hello tooAzure kopii zapasowej bazy danych programu SQL Server i odzyskiwania z platformy Azure obejmuje trzy kroki:

1. Utwórz tooAzure baz danych programu SQL Server dotyczących tooprotect zasad tworzenia kopii zapasowej.
2. Tworzenie kopii zapasowych na żądanie tooAzure.
3. Odzyskiwanie bazy danych hello z platformy Azure.

## <a name="before-you-start"></a>Przed rozpoczęciem
Przed rozpoczęciem upewnij się, że wszystkie hello [wymagania wstępne](backup-azure-dpm-introduction.md#prerequisites) dotyczące korzystania z programu Kopia zapasowa Microsoft Azure zostały spełnione tooprotect obciążeń. wymagania wstępne Hello obejmują zadania, takie jak: Tworzenie magazynu kopii zapasowych, pobrać poświadczenia magazynu, zainstalowanie hello Agent usługi Kopia zapasowa Azure i rejestracji serwera hello w magazynie hello.

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>Utwórz tooAzure baz danych programu SQL Server dotyczących tooprotect zasad tworzenia kopii zapasowej
1. Na powitania serwera DPM, kliknij przycisk hello **ochrony** obszaru roboczego.
2. Na wstążce narzędzi hello, kliknij przycisk **nowy** toocreate nowej grupy ochrony.

    ![Tworzenie grupy ochrony](./media/backup-azure-backup-sql/protection-group.png)
3. Program DPM wyświetla ekranu startowego hello hello wskazówek dotyczących tworzenia **grupy ochrony**. Kliknij przycisk **Dalej**.
4. Wybierz **serwerów**.

    ![Wybierz typ grupy ochrony — "Serwery"](./media/backup-azure-backup-sql/pg-servers.png)
5. Rozszerzenia hello maszyn programu SQL Server, gdzie znajdują się hello toobe baz danych kopii zapasowej. Program DPM Wyświetla różnych źródeł danych, których kopię zapasową można z tego serwera. Rozwiń węzeł hello **wszystkie udziały SQL** i wybrać hello bazy danych (w tym przypadku Wybraliśmy ReportServer$ MSDPM2012 i ReportServer$ MSDPM2012TempDB) toobe kopii zapasowej. Kliknij przycisk **Dalej**.

    ![Wybierz bazy danych SQL.](./media/backup-azure-backup-sql/pg-databases.png)
6. Podaj nazwę grupy ochrony hello i wybierz hello **chcę uzyskać ochronę online** wyboru.

    ![Metodę ochrony danych - dysku krótkoterminowa & Online Azure](./media/backup-azure-backup-sql/pg-name.png)
7. W hello **Określ cele krótkoterminowe** ekranu, obejmują hello niezbędnych składników toocreate punktów kopii zapasowej toodisk.

    Tutaj przedstawiono który **zakres przechowywania** ustawiono zbyt*5 dni*, **częstotliwość synchronizacji** ustawiono tooonce co *15 minut* czyli hello częstotliwość, przy którym wykonywana jest kopia zapasowa. **Ekspresowa pełna kopia zapasowa** ustawiono zbyt*godzinach od 8:00*.

    ![Cele krótkoterminowe](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > Od 8:00 PM (zgodnie z danych wejściowych ekranu toohello) punktu kopii zapasowej jest tworzona codziennie przez przeniesienie danych hello, który został zmodyfikowany z hello punktu kopii zapasowej poprzedniego dnia 8:00 PM. Ten proces jest nazywany **Express pełnej kopii zapasowej**. Podczas dzienników transakcji hello są synchronizowane co 15 minut, w przypadku bazy danych należy toorecover hello na 21:00:00 –, a następnie punktu hello jest tworzony przez odtwarzanie hello dzienniki hello express ostatniego punktu pełnej kopii zapasowej (20: 00 w tym przypadku).
   >
   >

8. Kliknij przycisk **Dalej**

    Program DPM Wyświetla hello ogólną dostępnego miejsca w magazynie i hello potencjalnych wykorzystanie miejsca na dysku.

    ![Przydział dysku](./media/backup-azure-backup-sql/pg-storage.png)

    Domyślnie program DPM tworzy jednego woluminu dla źródła danych (bazy danych programu SQL Server), używanej do hello początkowej kopii zapasowej. W ten sposób hello Menedżera dysków logicznych (LDM) limity źródeł danych too300 ochrony programu DPM (baz danych programu SQL Server). toowork wokół to ograniczenie, wybierz hello **kolokuj dane w puli magazynu DPM**, opcja. Użycie tej opcji, program DPM używa pojedynczy wolumin wiele źródeł danych, dzięki czemu tooprotect DPM zapasowych too2000 baz danych SQL.

    Jeśli **automatycznie rozszerzaj woluminy hello** wybrano opcję, program DPM może uwzględnić hello zwiększyć kopii zapasowej woluminu wraz z rozwojem hello danych produkcyjnych. Jeśli **automatycznie rozszerzaj woluminy hello** nie wybrano opcji, program DPM limity źródeł danych toohello hello magazynu kopii zapasowych używane w grupie ochrony hello.
9. Umożliwia nadanie administratorom wybór hello transferowania tej początkowej kopii zapasowej ręcznie (Wyłącz sieciowych) tooavoid przeciążenie przepustowości lub za pośrednictwem sieci hello. Można również skonfigurować hello czasu, w którym hello początkowy transfer może się zdarzyć. Kliknij przycisk **Dalej**.

    ![Replikacja początkowa — metoda](./media/backup-azure-backup-sql/pg-manual.png)

    Początkowa kopia zapasowa Hello wymaga transfer hello całego źródła danych (bazy danych programu SQL Server) z serwera programu DPM toohello (komputer serwera SQL) serwera produkcyjnego. Te dane mogą być duże i przesyłania danych hello za pośrednictwem sieci hello może przekroczyć przepustowości. Z tego powodu, Administratorzy mogą wybrać początkowa kopia zapasowa tootransfer hello: **ręcznie** (przy użyciu nośnika wymiennego) tooavoid przeciążenie przepustowości, lub **automatycznie przez sieć hello** (o określonej czas).

    Po zakończeniu tworzenia początkowej kopii zapasowej hello hello pozostałe kopie zapasowe hello są przyrostowe kopie zapasowe na powitania początkowej kopii zapasowej. Przyrostowe kopie zapasowe często małych toobe i łatwo są transferowane za pośrednictwem sieci hello.
10. Wybierz, kiedy zechcesz toorun sprawdzania spójności hello i kliknij przycisk **dalej**.

    ![Sprawdzanie spójności](./media/backup-azure-backup-sql/pg-consistent.png)

    Program DPM może wykonywać spójności wyboru toocheck hello integralności hello punktu kopii zapasowej. Obliczanie sum kontrolnych hello pliku kopii zapasowej hello na serwerze produkcyjnym hello (SQL Server maszyny w tym scenariuszu) i hello kopia zapasowa danych dla tego pliku na program DPM. W przypadku hello konflikt, zakłada się, że hello pliku kopii zapasowej programu DPM jest uszkodzona. Program DPM rectifies hello kopię zapasową danych, wysyłając bloki hello odpowiadającego toohello błąd sumy kontrolnej. Hello Sprawdzanie spójności jest operacją intensywnie wydajności, Administratorzy mają możliwość hello Planowanie sprawdzania spójności hello lub automatycznemu uruchamianiu.
11. toospecify ochrony w trybie online hello źródeł danych, wybierz hello toobe baz danych chronionych tooAzure, a następnie kliknij przycisk **dalej**.

    ![Wybierz źródła danych](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. Administratorzy mogą określić harmonogramy tworzenia kopii zapasowej i zasady przechowywania, które wskazują ich zasady organizacji.

    ![Harmonogram i przechowywania](./media/backup-azure-backup-sql/pg-schedule.png)

    W tym przykładzie kopie zapasowe są przyjmowane raz dziennie na 12:00 a 20: 00 (dolnej części ekranu hello)

    > [!NOTE]
    > Toohave dobrym rozwiązaniem jest kilka punktów odzyskiwania krótkoterminowego na dysku, aby uzyskać szybkie odzyskiwanie. Te punkty odzyskiwania są używane do "operacyjnych dotyczących odzyskiwania". Azure służy jako lokalizacji dobrej poza siedzibą firmy o wyższych SLA i gwarancji dostępności.
    >
    >

    **Najlepsze praktyki**: Upewnij się, że zaplanowane kopie zapasowe Azure po zakończeniu hello kopii zapasowych na dysku lokalnym za pomocą programu DPM. Dzięki temu hello najnowsze tooAzure kopii zapasowej toobe skopiowane dysku.

13. Wybierz harmonogram zasad przechowywania hello. Witaj szczegóły dotyczące sposobu działania zasad przechowywania hello są udostępniane na [tooreplace użycie usługi Kopia zapasowa Azure artykuł infrastruktury taśmy](backup-azure-backup-cloud-as-tape.md).

    ![Zasady przechowywania](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    W tym przykładzie:

    * Kopie zapasowe są przyjmowane raz dziennie na 12:00 a 20: 00 (dolnej części ekranu hello) i są przechowywane przez 180 dni.
    * Kopia zapasowa Hello na sobotę o godzinie 12:00 w dniu został zachowany na potrzeby 104 tygodni
    * Kopia zapasowa Hello na ostatnich sobotę o godzinie 12:00 w dniu są przechowywane przez 60 miesięcy
    * Kopia zapasowa Hello na Ostatnia sobota marca, 12:00 w dniu jest zachowywana 10 lat
14. Kliknij przycisk **dalej** i wybierz hello odpowiednią opcję transferowania hello tooAzure początkowej kopii zapasowej. Możesz wybrać **automatycznie przez sieć hello** lub **w trybie Offline z kopii zapasowej**.

    * **Automatycznie przez sieć hello** transferów hello tooAzure dane kopii zapasowej zgodnie z harmonogramem hello wybrany dla kopii zapasowej.
    * Jak **w trybie Offline z kopii zapasowej** works opisanej w [przepływu pracy w trybie Offline z kopii zapasowej w programie Kopia zapasowa Azure](backup-azure-backup-import-export.md).

    Wybierz odpowiednie transfer hello mechanizm toosend hello początkowa kopia zapasowa tooAzure, a następnie kliknij przycisk **dalej**.
15. Po Przejrzyj szczegóły zasad hello w hello **Podsumowanie** kliknij na powitania **Utwórz grupę** przycisk toocomplete hello w przepływie pracy. Możesz kliknąć hello **Zamknij** przycisk i monitorowanie postępu zadania hello w monitorowaniu obszaru roboczego.

    ![Tworzenie grupy ochrony w toku](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>Na żądanie kopii zapasowej bazy danych programu SQL Server
Witaj poprzednie kroki tworzenia zasad tworzenia kopii zapasowej, "punkt odzyskiwania" jest tworzony tylko wtedy, gdy występuje hello pierwszej kopii zapasowej. Zamiast oczekiwania na powitania tookick harmonogramu w, hello kroki tworzenia hello wyzwalania odzyskiwania punktu ręcznie.

1. Poczekaj, aż stan grupy ochrony hello **OK** hello bazy danych, przed utworzeniem punktu odzyskiwania hello.

    ![Członkowie grupy ochrony](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Kliknij prawym przyciskiem myszy na powitania bazy danych i wybierz **Utwórz punkt odzyskiwania**.

    ![Tworzenie punktu odzyskiwania Online](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. Wybierz **ochrony w trybie Online** w menu rozwijanym hello i kliknij **OK**. Spowoduje to uruchomienie hello Tworzenie punktu odzyskiwania na platformie Azure.

    ![Utwórz punkt odzyskiwania](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. Można wyświetlić postęp zadania hello w hello **monitorowanie** obszaru roboczego, gdzie można znaleźć w toku zadania, takie jak jedną przedstawione na rysunku dalej hello hello.

    ![Konsola monitorowania](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>Odzyskiwanie bazy danych programu SQL Server z platformy Azure
Witaj poniższe kroki są wymagane toorecover jednostki chronionej (baza danych programu SQL Server) z platformy Azure.

1. Serwer DPM hello Otwórz konsolę zarządzania. Przejdź za**odzyskiwania** obszaru roboczego, gdzie można zobaczyć serwery hello kopii zapasowej przez program DPM. Przeglądaj hello wymaganej bazy danych (w tym przypadku ReportServer$ MSDPM2012). Wybierz **odzyskanie** czas, który kończy się **Online**.

    ![Wybierz punkt odzyskiwania](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Kliknij prawym przyciskiem myszy hello Nazwa bazy danych, a następnie kliknij przycisk **odzyskać**.

    ![Odzyskiwanie z platformy Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. Program DPM Wyświetla szczegóły hello hello punktu odzyskiwania. Kliknij przycisk **Dalej**. toooverwrite hello bazy danych typu odzyskiwania wybierz hello **Odzyskaj toooriginal wystąpienia programu SQL Server**. Kliknij przycisk **Dalej**.

    ![Odzyskaj tooOriginal lokalizacji](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    W tym przykładzie program DPM umożliwia odzyskiwanie wystąpienia programu SQL Server tooanother bazy danych hello lub folderu sieciowego autonomiczny tooa.
4. W hello **opcji odzyskiwania określ** ekranu, można wybrać opcje odzyskiwania hello jak ograniczenie przepustowości toothrottle hello przepustowość dla odzyskiwania. Kliknij przycisk **Dalej**.
5. W hello **Podsumowanie** ekranu, zobacz wszystkie konfiguracje odzyskiwania hello dostarczony do tej pory. Kliknij przycisk **odzyskać**.

    Witaj stanu odzyskiwania zawiera hello bazy danych ma zostać przeprowadzone odzyskiwanie. Możesz kliknąć **Zamknij** tooclose hello kreatora i widoku hello postęp w hello **monitorowanie** obszaru roboczego.

    ![Zainicjuj proces odzyskiwania](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Po ukończeniu odzyskiwania hello hello przywrócona baza danych jest zgodny.

### <a name="next-steps"></a>Następne kroki:
• [Azure często zadawane pytania dotyczące tworzenia kopii zapasowej](backup-azure-backup-faq.md)
