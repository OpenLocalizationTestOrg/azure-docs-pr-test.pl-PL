---
title: "aaaSQL grup dostępności serwera — maszyny wirtualne Azure — samouczek | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toocreate programu SQL Server zawsze w grupie dostępności na maszynach wirtualnych platformy Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Konfigurowanie zawsze włączonej grupy dostępności w maszynie Wirtualnej platformy Azure ręcznie

Ten samouczek pokazuje, jak toocreate programu SQL Server zawsze w grupie dostępności na maszynach wirtualnych platformy Azure. Samouczek pełną Hello tworzy grupy dostępności z repliki bazy danych na dwóch serwerach SQL.

**Szacowanie czasu**: trwa około 30 minut toocomplete po hello wymagania wstępne są spełnione.

Witaj diagramie kompilacji w samouczku hello.

![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Wymagania wstępne

Hello samouczka przyjęto założenie, że masz podstawową wiedzę na temat programu SQL Server zawsze włączonych grup dostępności. Aby uzyskać więcej informacji, zobacz [Omówienie programu zawsze włączonych grup dostępności (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Witaj poniższej tabeli wymieniono wymagania wstępne hello muszą toocomplete przed rozpoczęciem tego samouczka:

|  |Wymaganie |Opis |
|----- |----- |----- |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | Dwa serwery SQL | — W zestawie dostępności Azure <br/> — W jednej domenie <br/> -Z zainstalowaną funkcją klastra trybu Failover |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Udział plików dla monitora klastra |  
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Konto usługi programu SQL Server | Konto domeny |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Konto usługi programu SQL Server Agent | Konto domeny |  
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Otwórz porty zapory | — Program SQL Server: **1433** dla domyślnego wystąpienia <br/> -Dublowania bazy danych punktu końcowego: **5022** lub dowolny dostępny port <br/> -Sondę modułu równoważenia obciążenia azure: **59999** lub dowolny dostępny port |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Dodawanie obsługi klastrów pracy awaryjnej | Oba serwery SQL wymagają tej funkcji |
|![kwadratowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Konto domeny instalacji | -Lokalnego administratora na każdym serwerze SQL <br/> -Członek roli serwera sysadmin programu SQL Server dla każdego wystąpienia programu SQL Server  |


Przed rozpoczęciem powitalne samouczka należy zbyt[ukończyć wymagania wstępne dotyczące tworzenia zawsze włączonych grup dostępności w maszynach wirtualnych platformy Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md). Jeśli te wymagania wstępne są już wypełnione, można przejść za[tworzenia klastrów](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Tworzenie klastra hello

Po hello wymagania wstępne są zakończone, hello pierwszym krokiem jest toocreate klastra trybu Failover serwera systemu Windows, która zawiera dwa serwery SQL i serwer monitora.  

1. RDP toohello pierwszego programu SQL Server przy użyciu konta domeny, które jest kontem administratora na serwerach SQL i powitania serwera monitora.

   >[!TIP]
   >Po wykonaniu hello [dokumentu z wymaganiami wstępnymi](virtual-machines-windows-portal-sql-availability-group-prereq.md), zostało utworzone konto o nazwie **CORP\Install**. Użyj tego konta.

2. W hello **Menedżera serwera** pulpitu nawigacyjnego, wybierz opcję **narzędzia**, a następnie kliknij przycisk **Menedżera klastra trybu Failover**.
3. W okienku po lewej stronie powitania kliknij prawym przyciskiem myszy **Menedżera klastra trybu Failover**, a następnie kliknij przycisk **utworzyć klaster**.
   ![Tworzenie klastra](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. W hello Kreatora tworzenia klastra, tworzenie klastra z jednym węzłem przez krokowe hello stron z ustawieniami hello w hello w poniższej tabeli:

   | Strona | Ustawienia |
   | --- | --- |
   | Przed rozpoczęciem |Użyj wartości domyślnych |
   | Wybierz serwery |Witaj typu Nazwa pierwszego serwera SQL w **wprowadź nazwę serwera** i kliknij przycisk **Dodaj**. |
   | Ostrzeżenie dotyczące sprawdzania poprawności |Wybierz **testów nr nie jest wymagana obsługa firmy Microsoft dla tego klastra, a w związku z tym nie ma toorun hello weryfikacji. Po kliknięciu przycisku dalej kontynuować tworzenie klastra hello**. |
   | Punkt dostępu do hello administrowanie klastra |Wpisz nazwę klastra, na przykład **SQLAGCluster1** w **nazwy klastra**.|
   | Potwierdzenie |Użyj wartości domyślnych, chyba że w przypadku korzystania z funkcji miejsca do magazynowania. Patrz Uwaga hello poniżej tej tabeli. |

### <a name="set-hello-cluster-ip-address"></a>Ustaw adres IP klastra hello

1. W **Menedżera klastra trybu Failover**, przewiń w dół za**zasoby podstawowe klastra** i rozwiń hello szczegółów klastra. Powinny być widoczne oba hello **nazwa** i hello **adres IP** zasobów w hello **** stanu. Hello zasobu adresu IP nie może być przełączony w tryb online ponieważ klastra hello przypisano hello sam adres IP jako samej maszyny hello, dlatego jest zduplikowany adres.

2. Kliknij prawym przyciskiem myszy hello nie powiodło się **adres IP** zasobów, a następnie kliknij przycisk **właściwości**.

   ![Właściwości klastra](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Wybierz **statyczny adres IP** i określ adres podsieci hello programu SQL Server w przypadku w polu tekstowym adres hello. Następnie kliknij przycisk **OK**.
4. W hello **zasoby podstawowe klastra** sekcji, kliknij prawym przyciskiem myszy nazwę klastra i kliknij przycisk **przejdź do trybu Online**. Następnie zaczekaj, aż oba zasoby są w trybie online. Gdy zasób Nazwa hello klastra do trybu online, aktualizuje powitania serwera kontrolera domeny przy użyciu nowego konta komputera usługi AD. Użyj tego AD hello toorun konta grupy dostępności w klastrze usługi później.

### <a name="addNode"></a>Dodaj hello innych toocluster programu SQL Server

Dodaj hello innych klastra toohello programu SQL Server.

1. W drzewie przeglądarki hello, kliknij prawym przyciskiem myszy hello klastra, a następnie kliknij przycisk **Dodaj węzeł**.

    ![Dodaj toohello węzła klastra](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. W hello **Kreatora dodawania węzłów**, kliknij przycisk **dalej**. W hello **Wybieranie serwerów** Dodaj hello drugiego serwera SQL. Wpisz nazwę serwera hello w **wprowadź nazwę serwera** , a następnie kliknij przycisk **Dodaj**. Gdy wszystko będzie gotowe, kliknij przycisk **dalej**.

1. W hello **ostrzeżenie dotyczące sprawdzania poprawności** kliknij przycisk **nr** (w środowisku produkcyjnym należy przeprowadzić testy weryfikacyjne hello). Następnie kliknij przycisk **Dalej**.

8. W hello **potwierdzenie** strony, jeśli używasz funkcji miejsca do magazynowania, hello Usuń zaznaczenie pola wyboru z etykietą **Dodaj wszystkie odpowiednie magazyny toohello klastra.**

   ![Dodaj potwierdzenie węzła](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Jeśli używasz funkcji miejsca do magazynowania i nie Usuń zaznaczenie pola wyboru **Dodaj wszystkie odpowiednie magazyny toohello klaster**, Windows odłącza dyski wirtualne hello podczas hello klastrowanie procesu. W związku z tym są wyświetlane w Menedżerze dysków lub w Eksploratorze dopiero hello miejsca do magazynowania są usuwane z hello klastra i ponownie nałożona przy użyciu programu PowerShell. Funkcja miejsca do magazynowania grupuje wiele dysków w pule toostorage. Aby uzyskać więcej informacji, zobacz [miejsca do magazynowania](https://technet.microsoft.com/library/hh831739).

1. Kliknij przycisk **Dalej**.

1. Kliknij przycisk **Zakończ**.

   Menedżer klastra trybu failover pokazuje, czy klaster ma nowy węzeł i wyświetla go w hello **węzłów** kontenera.

10. Wyloguj się z hello sesji usług pulpitu zdalnego.

### <a name="add-a-cluster-quorum-file-share"></a>Dodaj udział plików kworum klastra

W tym przykładzie klastra systemu Windows hello używa toocreate udziału pliku kworum klastra. W tym samouczku używana kworum Większość węzłów i plików udziału. Aby uzyskać więcej informacji, zobacz [opis konfiguracji kworum w klastrze pracy awaryjnej](http://technet.microsoft.com/library/cc731739.aspx).

1. Serwer członkowski monitora udziału plików toohello Uzyskuj dostęp do sesji pulpitu zdalnego.

1. Na **Menedżera serwera**, kliknij przycisk **narzędzia**. Otwórz **Zarządzanie komputerem**.

1. Kliknij przycisk **foldery udostępnione**.

1. Kliknij prawym przyciskiem myszy **udziałów**i kliknij przycisk **nowy udział...** .

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Użyj **udostępnionych Kreator tworzenia folderu** toocreate udziału.

1. Na **ścieżka folderu**, kliknij przycisk **Przeglądaj** oraz znajdowanie lub utworzyć ścieżkę do folderu udostępnionego hello. Kliknij przycisk **Dalej**.

1. W **nazwę, opis i ustawienia** Sprawdź hello nazwy udziału i ścieżki. Kliknij przycisk **Dalej**.

1. Na **uprawnienia folderu udostępnionego** ustawić **Dostosuj uprawnienia**. Kliknij przycisk **niestandardowy...** .

1. Na **dostosowywanie uprawnień**, kliknij przycisk **Dodaj...** .

1. Upewnij się, hello konto używane toocreate hello klastra ma pełną kontrolę.

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. Kliknij przycisk **OK**.

1. W **uprawnienia folderu udostępnionego**, kliknij przycisk **Zakończ**. Kliknij przycisk **Zakończ** ponownie.  

1. Wyloguj się z powitania serwera

### <a name="configure-cluster-quorum"></a>Konfigurowanie kworum klastra

Następnie należy ustawić hello kworum klastra.

1. Połącz toohello na pierwszym węźle klastra przy użyciu pulpitu zdalnego.

1. W **Menedżera klastra trybu Failover**, kliknij prawym przyciskiem myszy klaster hello, wskaż zbyt**więcej akcji**i kliknij przycisk **Konfiguruj ustawienia kworum klastra...** .

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. W **Kreatora konfiguracji kworum klastra**, kliknij przycisk **dalej**.

1. W **Wybieranie opcji konfiguracji kworum**, wybierz **Wybieranie monitora kworum hello**i kliknij przycisk **dalej**.

1. Na **Wybieranie monitora kworum**, kliknij przycisk **Konfigurowanie monitora udziału plików**.

   >[!TIP]
   >Windows Server 2016 obsługuje monitora chmury. Jeśli wybierzesz tego typu monitora nie ma potrzeby pliku monitor udostępniania. Aby uzyskać więcej informacji, zobacz [wdrażania chmury monitora dla klastra trybu Failover](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). Ten samouczek używa monitora udziału plików, który jest obsługiwany przez wcześniejsze systemy operacyjne.

1. Na **Konfigurowanie monitora udostępniania plików**, wpisz ścieżkę hello udziału hello utworzony. Kliknij przycisk **Dalej**.

1. Sprawdź ustawienia hello na **potwierdzenie**. Kliknij przycisk **Dalej**.

1. Kliknij przycisk **Zakończ**.

Zasoby podstawowe klastra Hello są skonfigurowane z monitora udziału plików.

## <a name="enable-availability-groups"></a>Włącz grupy dostępności

Następnie włącz opcję hello **zawsze włączonych grup dostępności** funkcji. Wykonaj te kroki na obu serwerach SQL.

1. Z hello **Start** ekranu, uruchom **SQL Server Configuration Manager**.
2. W drzewie przeglądarki powitania kliknij **usług SQL Server**, kliknij prawym przyciskiem myszy hello **programu SQL Server (MSSQLSERVER)** usługi, a następnie kliknij przycisk **właściwości**.
3. Kliknij przycisk hello **wysokiej dostępności funkcji AlwaysOn** , a następnie wybierz **Włącz zawsze włączone grupy dostępności**w następujący sposób:

    ![Włącz zawsze włączone grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. Kliknij przycisk **Zastosuj**. Kliknij przycisk **OK** w wyskakującym oknie dialogowym hello.

5. Uruchom ponownie usługę SQL Server hello.

Powtórz te czynności na powitania innego serwera SQL.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Utwórz bazę danych na powitania pierwszego serwera SQL

1. Uruchamiania hello RDP pliku toohello pierwszego programu SQL Server z domeny konta będący członkiem roli sysadmin stałej roli serwera.
1. Otwórz program SQL Server Management Studio i połącz toohello pierwszego serwera SQL.
7. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy **baz danych** i kliknij przycisk **nową bazę danych**.
8. W **Nazwa bazy danych**, typ **MyDB1**, następnie kliknij przycisk **OK**.

### <a name="backupshare"></a>Tworzenie kopii zapasowej udziału

1. Na hello pierwszego serwera SQL w **Menedżera serwera**, kliknij przycisk **narzędzia**. Otwórz **Zarządzanie komputerem**.

1. Kliknij przycisk **foldery udostępnione**.

1. Kliknij prawym przyciskiem myszy **udziałów**i kliknij przycisk **nowy udział...** .

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Użyj **udostępnionych Kreator tworzenia folderu** toocreate udziału.

1. Na **ścieżka folderu**, kliknij przycisk **Przeglądaj** oraz znajdowanie lub utworzyć ścieżki dla kopii zapasowej folderu udostępnionego hello bazy danych. Kliknij przycisk **Dalej**.

1. W **nazwę, opis i ustawienia** Sprawdź hello nazwy udziału i ścieżki. Kliknij przycisk **Dalej**.

1. Na **uprawnienia folderu udostępnionego** ustawić **Dostosuj uprawnienia**. Kliknij przycisk **niestandardowy...** .

1. Na **dostosowywanie uprawnień**, kliknij przycisk **Dodaj...** .

1. Upewnij się, że hello konta usługi programu SQL Server i Agent serwera SQL dla obu serwerów mają pełną kontrolę.

   ![Nowy udział](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. Kliknij przycisk **OK**.

1. W **uprawnienia folderu udostępnionego**, kliknij przycisk **Zakończ**. Kliknij przycisk **Zakończ** ponownie.  

### <a name="take-a-full-backup-of-hello-database"></a>Utworzenia pełnej kopii zapasowej hello bazy danych

Należy tooback się hello nowej bazy danych tooinitialize hello łańcuch dziennika. Jeśli nie wykonuje kopię zapasową hello nową bazę danych, nie można uwzględnić w grupie dostępności.

1. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy hello bazy danych, wskaż zbyt**zadań...** , kliknij przycisk **kopię zapasową**.

1. Kliknij przycisk **OK** tootake pełnej kopii zapasowej toohello domyślnej lokalizacji kopii zapasowej.

## <a name="create-hello-availability-group"></a>Utwórz hello grupy dostępności
Wszystko jest teraz gotowy tooconfigure, które grupy dostępności przy użyciu hello następujące kroki:

* Utwórz bazę danych na powitania pierwszego serwera SQL.
* Przełączyć pełnej kopii zapasowej i kopii zapasowej dziennika transakcji bazy danych hello
* Pełna hello przywracania i drugie programu SQL Server z hello toohello kopii zapasowych dziennika **NORECOVERY** opcji
* Utwórz hello grupy dostępności (**AG1**) z zatwierdzanie synchroniczne, automatycznej pracy awaryjnej i do odczytu replikach pomocniczych

### <a name="create-hello-availability-group"></a>Utwórz hello grupy dostępności:

1. W sesji pulpitu zdalnego toohello pierwszego serwera SQL. W **Eksplorator obiektów** w programie SSMS, kliknij prawym przyciskiem myszy **wysokiej dostępności funkcji AlwaysOn** i kliknij przycisk **Kreatora nowej grupy dostępności**.

    ![Uruchom Kreatora nowej grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. W hello **wprowadzenie** kliknij przycisk **dalej**. W hello **Określ nazwę grupy dostępności** strony, na przykład wpisz nazwę grupy dostępności hello **AG1**w **Nazwa grupy dostępności**. Kliknij przycisk **Dalej**.

    ![Kreator nowego AG, określ nazwę grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. W hello **wybierz baz danych** , wybierz bazę danych i kliknij przycisk **dalej**.

   >[!NOTE]
   >Hello bazy danych spełnia wymagania wstępne powitania dla grupy dostępności, ponieważ co najmniej jedną pełną kopię zapasową wykonano na powitania zamierzone repliki podstawowej.

   ![Kreatora nowej grupy dostępności, wybierz baz danych](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. W hello **Określanie replik** kliknij przycisk **dodać repliki**.

   ![Kreator nowego AG, określ repliki](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Witaj **połączyć tooServer** wyskakującej okna dialogowego. Nazwa typu hello hello drugiego serwera w **nazwy serwera**. Kliknij przycisk **Połącz**.

   Po powrocie do hello **Określanie replik** strony, powinien zostać wyświetlony hello drugi serwer na liście **replik dostępności**. Konfigurowanie replik hello w następujący sposób.

   ![Kreator nowego AG, określ repliki (pełną)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Kliknij przycisk **punkty końcowe** bazy danych hello toosee punktu końcowego dublowania dla tej grupy dostępności. Użyj hello sam portu można używać po ustawieniu hello [reguły zapory dla punktów końcowych dublowania bazy danych](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Kreatora nowej grupy dostępności, wybierz początkową synchronizację danych](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. W hello **Wybierz początkową synchronizację danych** wybierz **pełne** i określ udostępnionej lokalizacji sieciowej. Dla lokalizacji hello Użyj hello [udziale kopii zapasowej utworzonego](#backupshare). W przykładzie hello został **\\\\\<pierwszy serwer SQL\>\Backup\**. Kliknij przycisk **Dalej**.

   >[!NOTE]
   >Pełna synchronizacja ma pełną kopię zapasową bazy danych hello na powitania pierwszego wystąpienia programu SQL Server i przywracania go toohello drugie wystąpienie. Pełna synchronizacja w przypadku dużych baz danych nie jest zalecane, ponieważ może zająć dużo czasu. Teraz można zmniejszyć ręcznie wykonywanie kopii zapasowej bazy danych hello i przywracania jej z `NO RECOVERY`. Jeśli baza danych hello już została przywrócona z `NO RECOVERY` na powitania drugie programu SQL Server przed rozpoczęciem konfigurowania hello grupy dostępności, wybierz **tylko Dołącz**. Kopia zapasowa hello tootake po skonfigurowaniu hello grupy dostępności, wybierz opcję **Pomiń początkową synchronizację danych**.

    ![Kreatora nowej grupy dostępności, wybierz początkową synchronizację danych](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. W hello **weryfikacji** kliknij przycisk **dalej**. Ta strona powinna wyglądać podobnie toohello po obrazu:

    ![Kreator nowego AG, sprawdzanie poprawności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Brak ostrzeżenia dla konfiguracji odbiornika hello ponieważ odbiornika grupy dostępności nie zostały skonfigurowane. Można zignorować to ostrzeżenie, ponieważ na maszynach wirtualnych Azure tworzenia odbiornika powitania po utworzeniu usługi równoważenia obciążenia Azure hello.

10. W hello **Podsumowanie** kliknij przycisk **Zakończ**, a następnie zaczekaj, aż Kreator hello konfiguruje hello nowej grupy dostępności. W hello **postępu** strony, możesz kliknąć **szczegółowe** tooview hello szczegółowe postępu. Po zakończeniu pracy Kreatora hello sprawdzić hello **wyniki** tooverify strony, która hello grupy dostępności została pomyślnie utworzona.

     ![Wyniki w Kreatorze nowej grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Kliknij przycisk **Zamknij** tooexit hello kreatora.

### <a name="check-hello-availability-group"></a>Sprawdź hello grupy dostępności

1. W **Eksplorator obiektów**, rozwiń węzeł **wysokiej dostępności funkcji AlwaysOn**, następnie rozwiń węzeł **grup dostępności**. Powinien zostać wyświetlony hello nowej grupy dostępności w tym kontenerze. Kliknij prawym przyciskiem myszy hello grupy dostępności, a następnie kliknij przycisk **Pokaż pulpit nawigacyjny**.

   ![Pokaż AG pulpitu nawigacyjnego](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   Twoje **pulpitu nawigacyjnego AlwaysOn** powinien wyglądać podobnie toothis.

   ![Pulpit nawigacyjny grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Widać hello replik, tryb pracy awaryjnej hello każdej repliki i hello stanu synchronizacji.

2. W **Menedżera klastra trybu Failover**, kliknij przycisk klastra. Wybierz **ról**. Nazwa grupy dostępności Hello, używanego to rola na powitania klastra. Tej grupy dostępności nie ma adresu IP dla połączeń klienckich, ponieważ nie może skonfigurować odbiornik. Skonfiguruj odbiornik powitania po utworzeniu usługi równoważenia obciążenia Azure.

   ![W Menedżerze klastra trybu Failover grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > Nie próbuj toofail za pośrednictwem hello grupy dostępności z hello Menedżera klastra trybu Failover. Należy wykonać wszystkie operacje trybu failover z poziomu **pulpitu nawigacyjnego AlwaysOn** w programie SSMS. Aby uzyskać więcej informacji, zobacz [ograniczenia dotyczące Using hello Menedżera klastra trybu Failover z grupami dostępności](https://msdn.microsoft.com/library/ff929171.aspx).
    >

W tym momencie masz grupę dostępności z replik na dwa wystąpienia programu SQL Server. Witaj grupy dostępności można przenosić między wystąpieniami. Nie można połączyć toohello grupy dostępności jeszcze, ponieważ nie masz odbiornik. W maszynach wirtualnych platformy Azure odbiornika hello wymaga usługi równoważenia obciążenia. Witaj następnym krokiem jest toocreate modułu równoważenia obciążenia hello na platformie Azure.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Tworzenie usługi równoważenia obciążenia Azure

Na maszynach wirtualnych Azure grupy dostępności programu SQL Server wymaga usługi równoważenia obciążenia. Moduł równoważenia obciążenia Hello przechowuje hello adresu IP dla odbiornika grupy dostępności hello. Ta sekcja zawiera podsumowanie, jak usługa równoważenia w portalu Azure hello obciążenia toocreate hello.

1. W hello portalu Azure, przejdź do pozycji toohello grupy zasobów, których są serwery SQL i kliknij przycisk **+ Dodaj**.
2. Wyszukaj **modułu równoważenia obciążenia**. Wybierz moduł równoważenia obciążenia hello opublikowane przez firmę Microsoft.

   ![W Menedżerze klastra trybu Failover grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  Kliknij przycisk **Utwórz**.
3. Skonfiguruj następujące parametry dla usługi równoważenia obciążenia hello hello.

   | Ustawienie | Pole |
   | --- | --- |
   | **Nazwa** |Użyj nazwy tekst hello modułu równoważenia obciążenia, na przykład **sqlLB**. |
   | **Typ** |wewnętrzny |
   | **Sieć wirtualna** |Użyj nazwy hello hello sieci wirtualnej platformy Azure. |
   | **Podsieć** |Użyj nazwy hello hello podsieci, która hello maszyny wirtualnej jest w.  |
   | **Przypisywanie adresów IP** |Statyczny |
   | **Adres IP** |Użyj dostępny adres podsieci. |
   | **Subskrypcja** |Użyj hello sam subskrypcji jako hello maszyny wirtualnej. |
   | **Lokalizacja** |Użyj hello sam lokalizacji co hello maszyny wirtualnej. |

   Witaj bloku portalu Azure powinna wyglądać następująco:

   ![Tworzenie usługi równoważenia obciążenia](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Kliknij przycisk **Utwórz**, usługi równoważenia obciążenia hello toocreate.

Moduł równoważenia obciążenia hello tooconfigure, należy toocreate puli wewnętrznej bazy danych, sondowania i reguły równoważenia obciążenia hello zestawu. Czy w hello portalu Azure.

### <a name="add-backend-pool"></a>Dodawanie puli wewnętrznej bazy danych

1. W hello portalu Azure Przejdź tooyour grupy dostępności. Może być konieczne równoważenia obciążenia hello nowo utworzony toosee toorefresh hello widoku.

   ![Znajdź moduł równoważenia obciążenia w grupie zasobów](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Kliknij hello modułu równoważenia obciążenia, kliknij przycisk **pul zaplecza**i kliknij przycisk **+ Dodaj**. Ustaw puli zaplecza hello w następujący sposób:

   | Ustawienie | Opis | Przykład
   | --- | --- |---
   | **Nazwa** | Wpisz nazwę tekstu | SQLLBBE
   | **Skojarzony z** | Wybierz z listy | Zestaw dostępności
   | **Zestaw dostępności** | Użyj nazwy zestawu dostępności hello, który maszyn wirtualnych programu SQL Server znajdują się w | sqlAvailabilitySet |
   | **Maszyny wirtualne** |Witaj dwie nazwy maszyny Wirtualnej Azure SQL Server | SQLServer-0, sqlserver 1

1. Wpisz nazwę hello hello puli zaplecza.

1. Kliknij przycisk **+ Dodaj maszynę wirtualną**.

1. Dla zestawu dostępności hello wybierz ten hello serwerami programu SQL Server znajdują się w zestawie dostępności hello.

1. W przypadku maszyn wirtualnych zawierają oba hello serwerów SQL. Nie dołączaj serwera monitora udziału plików hello.

1. Kliknij przycisk **OK** puli zaplecza hello toocreate.

### <a name="set-hello-probe"></a>Sonda zbioru hello

1. Kliknij hello modułu równoważenia obciążenia, kliknij przycisk **sondy kondycji**i kliknij przycisk **+ Dodaj**.

1. Ustaw sondy kondycji hello w następujący sposób:

   | Ustawienie | Opis | Przykład
   | --- | --- |---
   | **Nazwa** | Tekst | SQLAlwaysOnEndPointProbe |
   | **Protokół** | Wybierz protokół TCP | TCP |
   | **Port** | Wszelkie nieużywany port. | 59999 |
   | **Interwał**  | Witaj ilość czasu między sondowania prób w sekundach |5 |
   | **Próg złej kondycji** | Witaj liczbę kolejnych niepowodzeń sondy musi nastąpić toobe maszyny wirtualnej, określana jako Zła  | 2 |

1. Kliknij przycisk **OK** sondy kondycji hello tooset.

### <a name="set-hello-load-balancing-rules"></a>Ustaw reguły równoważenia obciążenia hello

1. Kliknij hello modułu równoważenia obciążenia, kliknij przycisk **reguły równoważenia obciążenia**i kliknij przycisk **+ Dodaj**.

1. Ustaw reguły były w następujący sposób równoważenia obciążenia hello.
   | Ustawienie | Opis | Przykład
   | --- | --- |---
   | **Nazwa** | Tekst | SQLAlwaysOnEndPointListener |
   | **Adres IP frontonu** | Wybierz adres |Użyj adresu hello, który został utworzony podczas tworzenia modułu równoważenia obciążenia hello. |
   | **Protokół** | Wybierz protokół TCP |TCP |
   | **Port** | Korzystając z portu hello hello wystąpienia programu SQL Server | 1433 |
   | **Port zaplecza** | To pole nie jest używany, gdy pływający adres IP jest wartość dla serwera bezpośredniego zwrotu | 1433 |
   | **Sondy** |Nazwa Hello hello sondy | SQLAlwaysOnEndPointProbe |
   | **Trwałość sesji** | Listy rozwijanej | **Brak** |
   | **Limit czasu bezczynności** | Otwórz połączenie TCP tookeep minut | 4 |
   | **Zmienny adres IP (bezpośredni zwrot serwera)** | |Enabled (Włączony) |

   > [!WARNING]
   > Bezpośredni zwrot serwera jest ustawiana podczas tworzenia. Nie można zmienić.

1. Kliknij przycisk **OK** reguły równoważenia obciążenia hello tooset.

## <a name="configure-listener"></a>Skonfiguruj odbiornik hello

dalej toodo operacją Hello jest tooconfigure odbiornika grupy dostępności w klastrze trybu failover hello.

> [!NOTE]
> Ten samouczek pokazuje, jak adres toocreate jednego odbiornika — jeden ILB protokołu IP. toocreate co najmniej jednego odbiornika za pomocą jednego lub więcej adresów IP, zobacz [odbiornika Create Availability Group, a moduł równoważenia obciążenia | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Port odbiornika zestawu

W programu SQL Server Management Studio Ustaw hello port odbiornika.

1. Uruchom program SQL Server Management Studio i połącz toohello repliki podstawowej.

1. Przejdź za**wysokiej dostępności funkcji AlwaysOn** | **grup dostępności** | **odbiorniki grupy dostępności**.

1. Powinna zostać wyświetlona nazwa odbiornika hello utworzonego w Menedżerze klastra trybu Failover. Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **właściwości**.

1. W hello **portu** Określ numer portu odbiornika grupy dostępności hello hello przy użyciu hello $EndpointPort użyto wcześniej (1433 była hello domyślna), następnie kliknij przycisk **OK**.

Masz teraz grupy dostępności programu SQL Server na maszynach wirtualnych Azure działających w trybie Menedżera zasobów.

## <a name="test-connection-toolistener"></a>Test połączenia toolistener

tootest hello połączenia:

1. RDP tooa programu SQL Server, który znajduje się w hello sam wirtualnych sieci, ale nie nie własnych hello repliki. Można użyć innego serwera SQL w klastrze hello hello.

1. Użyj **sqlcmd** narzędzie tootest hello połączenia. Na przykład ustanawia hello następującego skryptu **sqlcmd** repliki podstawowej toohello połączenia za pośrednictwem hello odbiornika z uwierzytelnianiem systemu Windows:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Jeśli odbiornik hello używa portu innego niż hello domyślnego portu (1433), określ hello port w parametrach połączenia hello. Na przykład hello następującego polecenia sqlcmd łączy odbiornika tooa portu 1435:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Witaj SQLCMD połączenia automatycznie łączy toowhichever wystąpienie programu SQL Server repliki podstawowej hello hostów.

> [!TIP]
> Upewnij się, że port hello określony jest otwarty na zaporze hello obu serwerów SQL. Oba serwery wymagają regułę ruchu przychodzącego dla portu TCP, którego używasz hello. Aby uzyskać więcej informacji, zobacz [Dodawanie lub edytowanie reguły zapory](http://technet.microsoft.com/library/cc753558.aspx).
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Następne kroki

- [Dodaj IP adres tooa Usługa równoważenia obciążenia w grupie dostępności drugi](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
