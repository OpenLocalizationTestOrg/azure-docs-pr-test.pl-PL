---
title: "aaaUse PowerShell tooCreate maszyny Wirtualnej z macierzysty tryb serwera raportów | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano i przedstawiono hello wdrażania i konfiguracji serwera raportów usług SQL Server Reporting Services w trybie macierzystym w maszynie wirtualnej platformy Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>Użyj programu PowerShell tooCreate Azure maszyny Wirtualnej z macierzysty tryb serwera raportów
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

W tym temacie opisano i przedstawiono hello wdrażania i konfiguracji serwera raportów usług SQL Server Reporting Services w trybie macierzystym w maszynie wirtualnej platformy Azure. Witaj kroków w tym dokumencie kombinacja maszyny wirtualnej hello toocreate ręczne i skrypt programu Windows PowerShell tooconfigure Reporting Services na powitania maszyny Wirtualnej. Skrypt konfiguracji Hello obejmuje otwierania portu zapory dla protokołu HTTP lub HTTPs.

> [!NOTE]
> Jeśli nie wymagają **HTTPS** na powitania serwera raportów, **pominąć krok 2**.
> 
> Po utworzeniu hello maszyny Wirtualnej w kroku 1, przejdź toohello sekcji Użyj skryptu tooconfigure hello raportu serwera i protokołu HTTP. Po uruchomieniu skryptu hello powitania serwera raportów jest gotowy toouse.

## <a name="prerequisites-and-assumptions"></a>Wymagania wstępne i założenia
* **Subskrypcja platformy Azure**: Sprawdź hello liczba rdzeni dostępne w Twojej subskrypcji platformy Azure. Jeśli utworzysz zalecany rozmiar maszyny Wirtualnej hello **A3**, należy **4** dostępne rdzenie. Jeśli używasz rozmiar maszyny Wirtualnej **A2**, należy **2** dostępne rdzenie.
  
  * w menu u góry hello tooverify hello limit rdzeni w subskrypcji w hello klasycznego portalu Azure, kliknij w okienku po lewej stronie powitania, a następnie kliknij przycisk użycia ustawienia.
  * tooincrease hello limit przydziału rdzeni, skontaktuj się z pomocą [pomocą techniczną platformy Azure](https://azure.microsoft.com/support/options/). Uzyskać rozmiaru maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych na platformie Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* **Windows PowerShell do obsługi skryptów**: hello temacie założono, że masz podstawową wiedzę na temat pracy programu Windows PowerShell. Aby uzyskać więcej informacji o korzystaniu z programu Windows PowerShell zobacz następujące hello:
  
  * [Uruchamianie środowiska Windows PowerShell w systemie Windows Server](https://technet.microsoft.com/library/hh847814.aspx)
  * [Wprowadzenie do korzystania z programu Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>Krok 1: Udostępnić maszynie wirtualnej platformy Azure
1. Przeglądaj toohello klasycznego portalu Azure.
2. Kliknij przycisk **maszyn wirtualnych** w okienku po lewej stronie powitania.
   
    ![maszyny wirtualne Microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. Kliknij przycisk **Nowy**.
   
    ![Przycisk Nowy](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. Kliknij przycisk **z galerii**.
   
    ![Nowa maszyna wirtualna z galerii](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. Kliknij przycisk **SQL Server 2014 RTM Standard — Windows Server 2012 R2** a następnie kliknij przycisk hello toocontinue strzałki.
   
    ![Dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Jeśli potrzebujesz danych usług Reporting Services hello zmiennych funkcji subskrypcji, wybierz **programu SQL Server 2014 RTM Enterprise — Windows Server 2012 R2**. Aby uzyskać więcej informacji o wersjach programu SQL Server i obsługę funkcji, zobacz [funkcje obsługiwane przez wersje programu SQL Server 2012 hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).
6. Na powitania **konfiguracji maszyny wirtualnej** Edytuj hello następujące pola:
   
   * Jeśli istnieje więcej niż jeden **Data wydania wersji**, wybierz hello najnowszej wersji.
   * **Nazwa maszyny wirtualnej**: Nazwa komputera hello jest również używany na następnej stronie konfiguracji hello jako hello domyślną nazwę DNS usługi w chmurze. Nazwa DNS Hello musi być unikatowa w hello usługi Azure. Rozważ skonfigurowanie hello maszyny Wirtualnej przy użyciu nazwy komputera, który opisuje jakie hello maszyna wirtualna jest używana do. Na przykład ssrsnativecloud.
   * **Warstwa**: standardowy
   * **Rozmiar: A3** hello zaleca się rozmiar maszyny Wirtualnej dla obciążeń programu SQL Server. Jeśli maszyna wirtualna jest używana tylko jako serwer raportów maszyny Wirtualnej o rozmiarze A2 jest wystarczająca, chyba że serwer raportów hello napotyka duże obciążenie. Dla maszyny Wirtualnej, informacje o cenach, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/).
   * **Nową nazwę użytkownika**: należy podać nazwę hello jest tworzony jako administrator na powitania maszyny Wirtualnej.
   * **Nowe hasło** i **potwierdzić**. To hasło służy do nowego konta administratora hello i zaleca się, że używasz silne hasło.
   * Kliknij przycisk **Dalej**. ![dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. Na następnej stronie powitania edytować hello następujące pola:
   
   * **Usługi w chmurze**: Wybierz **Utwórz nową usługę w chmurze**.
   * **Nazwa DNS usługi w chmurze**: jest to hello publicznej nazwy DNS hello usługę Chmurową, która jest skojarzona z hello maszyny Wirtualnej. Hello domyślna nazwa jest hello wpisane hello nazwy maszyny Wirtualnej. Jeśli w kolejnych krokach tematu hello, utworzysz zaufany certyfikat SSL, a następnie nazwy DNS hello jest używany dla wartości hello hello "**wystawiony dla**" hello certyfikatu.
   * **Region/koligacji grupy/wirtualnej sieci**: Wybierz hello region najbliższy tooyour użytkowników.
   * **Konto magazynu**: Użyj konta magazynu wygenerowanej automatycznie.
   * **Zestaw dostępności**: Brak.
   * **Punkty końcowe** hello Zachowaj **pulpitu zdalnego** i **PowerShell** punktów końcowych, a następnie dodaj końcowy HTTP lub HTTPS, w zależności od środowiska.
     
     * **HTTP**: hello domyślne porty publiczne i prywatne są **80**. Należy pamiętać, że jeśli korzystanie z prywatnych portu innego niż 80, zmodyfikuj **$HTTPport = 80** hello http skryptu.
     * **HTTPS**: hello domyślne porty publiczne i prywatne są **443**. Ze względów bezpieczeństwa jest port prywatny hello toochange i skonfigurować zapory i hello raportu server toouse hello prywatnych portów. Aby uzyskać więcej informacji dotyczących punktów końcowych, zobacz [jak tooSet komunikacji się z maszyną wirtualną](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Należy pamiętać, że jeśli użyjesz portu innego niż 443, Zmień parametr hello **$HTTPsport = 443** w hello skryptu HTTPS.
   * Kliknij przycisk Dalej. ![Dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. Na powitania ostatniej stronie kreatora hello, zachowaj domyślne hello **instalacji agenta maszyny Wirtualnej hello** wybrane. Witaj kroki opisane w tym temacie, nie będą korzystać hello agenta maszyny Wirtualnej, ale jeśli planujesz tookeep tej maszyny Wirtualnej, agent maszyny Wirtualnej hello i rozszerzenia pozwoli tooenhance he CM.  Aby uzyskać więcej informacji na powitania agenta maszyny Wirtualnej, zobacz [agenta maszyny Wirtualnej i rozszerzenia — część 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/). Jeden AD zainstalowanych rozszerzeń domyślne hello uruchomiona jest rozszerzenie "BGINFO" hello, który wyświetla na pulpicie maszyny Wirtualnej hello, informacje o systemie, takie jak wewnętrznym adresem IP i free dysków miejsca.
9. Kliknij polecenie ukończone. ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. Hello **stan** z maszyny Wirtualnej będzie wyświetlany jako hello **uruchamianie (inicjowania obsługi administracyjnej)** podczas procesu udostępniania hello i następnie wyświetlana **systemem** gdy hello maszyny Wirtualnej jest zainicjowana i gotowa toouse.

## <a name="step-2-create-a-server-certificate"></a>Krok 2: Utworzenie certyfikatu serwera
> [!NOTE]
> Jeśli nie wymagają protokołu HTTPS na powitania serwera raportów, możesz **pominąć krok 2** i przejdź do sekcji toohello **używać serwera raportów hello tooconfigure skryptu i HTTP**. Użyj hello HTTP skryptu tooquickly skonfigurować powitania serwera raportów i raportu hello się, że serwer będzie gotowy toouse.

W kolejności toouse HTTPS na powitania maszyny Wirtualnej należy zaufany certyfikat SSL. W zależności od scenariusza należy użyć hello następujących dwóch metod:

* Prawidłowy certyfikat SSL wystawiony przez urząd certyfikacji (CA) i zaufany przez firmę Microsoft. certyfikaty głównego urzędu certyfikacji Hello są wymagane toobe dystrybuowane za pośrednictwem hello programu certyfikatów głównych firmy Microsoft. Aby uzyskać więcej informacji na temat tego programu, zobacz [systemu Windows i Windows Phone 8 SSL programu certyfikatów głównych (elementu członkowskiego CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) i [toohello wprowadzenie programu certyfikatów głównych firmy Microsoft](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).
* Certyfikatu z podpisem własnym. Certyfikaty z podpisem własnym nie jest zalecana dla środowisk produkcyjnych.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse certyfikat, który został utworzony przez zaufany urząd certyfikacji
1. **Żądanie certyfikatu serwera dla witryny sieci Web powitania od urzędu certyfikacji**. 
   
    Możesz użyć hello Kreator certyfikatu serwera sieci Web albo toogenerate pliku żądania certyfikatu (Certreq.txt) wysłanie tooa urzędu certyfikacji lub toogenerate żądania dla urzędu certyfikacji w trybie online. Na przykład usług certyfikatów firmy Microsoft w systemie Windows Server 2012. W zależności od poziomu hello wiarygodności identyfikacji oferowanego przez dany certyfikat serwera jest kilku miesięcy tooseveral dni tooapprove urzędu certyfikacji hello żądania i wysłać do użytkownika plik certyfikatu. 
   
    Aby uzyskać więcej informacji na temat żądania certyfikatów serwera zobacz następujące hello: 
   
   * Użyj [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).
   * TooAdminister narzędzi zabezpieczeń systemu Windows Server 2012.
     
     [TooAdminister narzędzi zabezpieczeń systemu Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > Witaj **wystawiony dla** pola hello zaufany certyfikat SSL powinien być hello sam jako hello **nazwa DNS usługi w chmurze** użyte do hello nowej maszyny Wirtualnej.

2. **Instalowanie certyfikatu serwera hello na powitania serwera sieci Web**. serwer sieci Web Hello jest w tym przypadku hello maszyny Wirtualnej, że hosty hello serwera raportów i hello witryna internetowa jest tworzona w kolejnych krokach, podczas konfigurowania usług Reporting Services. Aby uzyskać więcej informacji dotyczących instalowania certyfikatu serwera hello na powitania serwera sieci Web za pomocą przystawki MMC certyfikatów hello, zobacz [zainstalować certyfikat serwera](https://technet.microsoft.com/library/cc740068).
   
    Jeśli chcesz, aby skrypt hello toouse uwzględnionych w tym temacie tooconfigure powitania serwera raportów, hello wartość certyfikatów hello **odcisk palca** są wymagane jako parametr hello skryptu. Zobacz hello następnej sekcji, aby uzyskać szczegółowe informacje na jak tooobtain hello odcisk palca certyfikatu hello.
3. Przypisz raportów hello server certyfikatu toohello. Hello przydziałów zakończeniu w następnej sekcji hello podczas konfigurowania serwera raportów hello.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>Witaj toouse certyfikatu z podpisem własnym maszyny wirtualne
Certyfikatu z podpisem własnym został utworzony na powitania maszyny Wirtualnej podczas przydzielania został hello maszyny Wirtualnej. Witaj certyfikat ma hello takie same nazwy jako hello nazwę DNS maszyny Wirtualnej. W kolejności tooavoid błędów certyfikatów, jest wymagany certyfikat hello jest zaufany, na powitania samej maszyny Wirtualnej, a także przez wszystkich użytkowników hello lokacji.

1. tootrust hello głównego urzędu certyfikacji certyfikatu hello na powitania lokalnej maszyny Wirtualnej, dodać hello certyfikatu toohello **zaufane główne urzędy certyfikacji**. Hello poniżej znajduje się podsumowanie hello czynności. Aby uzyskać szczegółowe instrukcje na jak tootrust hello urzędu certyfikacji, zobacz [zainstalować certyfikat serwera](https://technet.microsoft.com/library/cc740068).
   
   1. Z hello klasycznego portalu Azure, wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk Połącz. W zależności od konfiguracji przeglądarki może być toosave zostanie wyświetlony monit o plik RDP do połączenia toohello maszyny Wirtualnej.
      
       ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Użyj nazwy maszyny Wirtualnej użytkownika hello, nazwę użytkownika i hasła skonfigurowanego podczas tworzenia hello maszyny Wirtualnej. 
      
       Na przykład w hello po obraz, Nazwa maszyny Wirtualnej hello jest **ssrsnativecloud** i nazwa użytkownika hello jest **testuser**.
      
       ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. Uruchom mmc.exe. Aby uzyskać więcej informacji, zobacz [porady: wyświetlanie certyfikatów z hello przystawka programu MMC](https://msdn.microsoft.com/library/ms788967.aspx).
   3. W aplikacji konsoli hello **pliku** menu Dodaj hello **certyfikaty** przystawki, wybierz pozycję **konto komputera** po wyświetleniu monitu, a następnie kliknij przycisk **dalej**.
   4. Wybierz **komputera lokalnego** toomanage, a następnie kliknij przycisk **Zakończ**.
   5. Kliknij przycisk **Ok** , a następnie rozwiń węzeł hello **certyfikaty - osobiste** węzłów, a następnie kliknij przycisk **certyfikaty**. Witaj certyfikatu jest nosi nazwę DNS hello hello maszyny Wirtualnej i kończy **cloudapp.net**. Kliknij prawym przyciskiem myszy nazwę certyfikatu hello, a następnie kliknij przycisk **kopiowania**.
   6. Rozwiń węzeł hello **zaufane główne urzędy certyfikacji** węzła, a następnie kliknij prawym przyciskiem myszy **certyfikaty** , a następnie kliknij przycisk **Wklej**.
   7. toovalidate dwa razy kliknij nazwę certyfikatu hello w obszarze **zaufane główne urzędy certyfikacji** i sprawdź, czy nie ma żadnych błędów i wyświetlić certyfikat. Jeśli chcesz, aby skrypt HTTPS hello toouse uwzględnionych w tym temacie tooconfigure powitania serwera raportów, hello wartość certyfikatów hello **odcisk palca** są wymagane jako parametr hello skryptu. **wartość odcisku palca hello tooget**, wykonaj następujące czynności hello. W sekcji również jest odcisk palca programu PowerShell próbki tooretrieve hello [użyć skryptu tooconfigure hello raportu serwera i protokołu HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).
      
      1. Kliknij dwukrotnie nazwę hello hello certyfikatu, na przykład ssrsnativecloud.cloudapp.net.
      2. Kliknij przycisk hello **szczegóły** kartę.
      3. Kliknij przycisk **odcisk palca**. wartość Hello odcisk palca hello jest wyświetlana w polu Szczegóły hello, na przykład a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.
      4. Skopiuj odcisk palca hello i Zapisz wartość hello na później lub edycji skryptu hello teraz.
      5. (*) Przed uruchomieniem skryptu hello Usuń spacje hello Between hello par wartości. Na przykład odcisk palca hello zauważyć przed będzie teraz a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.
      6. Przypisz raportów hello server certyfikatu toohello. Hello przydziałów zakończeniu w następnej sekcji hello podczas konfigurowania serwera raportów hello.

Jeśli używasz certyfikatu SSL z podpisem własnym hello nazwa certyfikatu hello już zgodna hello hosta hello maszyny Wirtualnej. W związku z tym hello DNS maszyny hello jest już zarejestrowany globalnie i jest możliwy za pomocą dowolnego klienta.

## <a name="step-3-configure-hello-report-server"></a>Krok 3: Konfigurowanie powitania serwera raportów
Ta sekcja przeprowadzi Cię przez konfigurację hello maszyny Wirtualnej jako serwera raportów usług Reporting Services w trybie macierzystym. Można użyć jednego powitania po serwera raportów hello tooconfigure metod:

* Korzystać z serwera raportów hello hello skryptu tooconfigure
* Witaj tooConfigure Użyj Menedżera konfiguracji serwera raportów.

Aby uzyskać bardziej szczegółowe kroki, zobacz sekcję hello [toohello Connect maszyny wirtualnej, a następnie rozpocznij hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).

**Uwierzytelnianie Uwaga:** hello zalecana metoda uwierzytelniania jest uwierzytelnianie systemu Windows i jest hello domyślne uwierzytelnianie usług Reporting Services. Tylko użytkownicy, które są skonfigurowane na powitania maszyny Wirtualnej mogą uzyskiwać dostęp do usług Reporting Services i przypisane tooReporting usług ról.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>Użyj skryptu tooconfigure hello raportu serwera i HTTP
toouse hello środowiska Windows PowerShell skryptu tooconfigure powitania serwera raportów, pełną hello następujące kroki. Konfiguracja Hello obejmuje protokołu HTTP, a nie HTTPS:

1. Z hello klasycznego portalu Azure, wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk Połącz. W zależności od konfiguracji przeglądarki może być toosave zostanie wyświetlony monit o plik RDP do połączenia toohello maszyny Wirtualnej.
   
    ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Użyj nazwy maszyny Wirtualnej użytkownika hello, nazwę użytkownika i hasła skonfigurowanego podczas tworzenia hello maszyny Wirtualnej. 
   
    Na przykład w hello po obraz, Nazwa maszyny Wirtualnej hello jest **ssrsnativecloud** i nazwa użytkownika hello jest **testuser**.
   
    ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Na powitania maszyny Wirtualnej, otwórz **programu Windows PowerShell ISE** z uprawnieniami administracyjnymi. Witaj PowerShell ISE jest instalowany domyślnie w systemie Windows server 2012. Zaleca się, że używasz hello ISE zamiast standardowego okna programu Windows PowerShell, aby można wkleić skryptu hello hello ISE, zmodyfikuj skrypt hello, a następnie uruchom skrypt hello.
3. W środowisku Windows PowerShell ISE, kliknij przycisk hello **widoku** menu, a następnie kliknij przycisk **Pokaż okienko skryptu**.
4. Hello następującego skryptu skopiuj i Wklej hello skryptu w okienku skryptów programu Windows PowerShell ISE hello.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. Jeśli utworzono hello maszyny Wirtualnej z portem HTTP innych niż 80, zmodyfikuj parametr hello $HTTPport = 80.
6. skrypt Hello jest obecnie skonfigurowany dla usług Reporting Services. Toorun hello skryptów dla usług Reporting Services, zmodyfikować części wersji hello hello ścieżki toohello nazw zbyt "v11" w instrukcji hello Get-WmiObject.
7. Uruchom skrypt hello.

**Sprawdzanie poprawności**: tooverify, który hello podstawowy raport serwera działania, zobacz hello [konfiguracji hello Sprawdź](#verify-the-configuration) później w tym temacie.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>Użyj skryptu tooconfigure hello raportu serwera i protokołu HTTPS
toouse programu Windows PowerShell tooconfigure powitania serwera raportów, pełną hello następujące kroki. Konfiguracja Hello obejmuje protokołu HTTPS, a nie HTTP.

1. Z hello klasycznego portalu Azure, wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk Połącz. W zależności od konfiguracji przeglądarki może być toosave zostanie wyświetlony monit o plik RDP do połączenia toohello maszyny Wirtualnej.
   
    ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Użyj nazwy maszyny Wirtualnej użytkownika hello, nazwę użytkownika i hasła skonfigurowanego podczas tworzenia hello maszyny Wirtualnej. 
   
    Na przykład w hello po obraz, Nazwa maszyny Wirtualnej hello jest **ssrsnativecloud** i nazwa użytkownika hello jest **testuser**.
   
    ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Na powitania maszyny Wirtualnej, otwórz **programu Windows PowerShell ISE** z uprawnieniami administracyjnymi. Witaj PowerShell ISE jest instalowany domyślnie w systemie Windows server 2012. Zaleca się, że używasz hello ISE zamiast standardowego okna programu Windows PowerShell, aby można wkleić skryptu hello hello ISE, zmodyfikuj skrypt hello, a następnie uruchom skrypt hello.
3. uruchamianie skryptów, uruchom następujące polecenia programu Windows PowerShell hello tooenable:
   
        Set-ExecutionPolicy RemoteSigned
   
    Następnie możesz uruchomić następujące zasady hello tooverify hello:
   
        Get-ExecutionPolicy
4. W **programu Windows PowerShell ISE**, kliknij przycisk hello **widoku** menu, a następnie kliknij przycisk **Pokaż okienko skryptu**.
5. Skopiuj hello następujący skrypt i wklej go w okienku skryptów programu Windows PowerShell ISE hello.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Modyfikowanie hello **$certificatehash** parametru w skrypcie hello:
   
   * Jest to **wymagane** parametru. Jeśli nie została zapisana wartość certyfikatu hello z poprzednich kroków hello, użyj jednej z poniższych wartość skrótu certyfikatu hello toocopy metody z odciskiem palca certyfikatów hello hello.:
     
       Na hello maszyny Wirtualnej Otwórz program Windows PowerShell ISE i uruchom następujące polecenie hello:
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       dane wyjściowe Hello będzie wyglądać podobnie następujące toohello. Jeśli skrypt hello zwraca pusty wiersz, hello maszyny Wirtualnej nie ma certyfikatu skonfigurowanego na przykład, zobacz sekcję hello [toouse hello certyfikatu z podpisem własnym maszyn wirtualnych](#to-use-the-virtual-machines-self-signed-certificate).
     
     LUB
   * Na hello mmc.exe uruchomienia maszyny Wirtualnej, a następnie dodaj hello **certyfikaty** przystawki.
   * W obszarze hello **zaufane główne urzędy certyfikacji** węzła kliknij dwukrotnie nazwę certyfikatu. Jeśli używasz certyfikatu z podpisem własnym hello z hello maszyny Wirtualnej, certyfikat hello jest nosi nazwę DNS hello hello maszyny Wirtualnej i kończy się wyrazem **cloudapp.net**.
   * Kliknij przycisk hello **szczegóły** kartę.
   * Kliknij przycisk **odcisk palca**. wartość Hello odcisk palca hello jest wyświetlana w polu Szczegóły hello, na przykład af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48
   * **Przed uruchomieniem skryptu hello**, Usuń spacje hello Between hello par wartości. Na przykład af1160b64b288d890a8212ff6ba9c3664f319048
7. Modyfikowanie hello **$httpsport** parametru: 
   
   * Jeśli dla punktu końcowego HTTPS hello jest używany port 443, następnie nie trzeba tooupdate tego parametru w skrypcie hello. W przeciwnym razie użyj wartości portu hello, wybranej podczas konfigurowania prywatnej punkt końcowy HTTPS hello na powitania maszyny Wirtualnej.
8. Modyfikowanie hello **$DNSName** parametru: 
   
   * Witaj skrypt został skonfigurowany certyfikat wieloznaczny $DNSName = "+". Jeśli nie chcesz, aby tooconfigure jest nie w powiązanie certyfikatu symboli wieloznacznych, komentarz $DNSName = "+"i Włącz po wierszu hello $DNSNAme pełna dokumentacja ## $DNSName="$server.cloudapp.net hello".
     
       Zmień wartość hello $DNSName, jeśli nie chcesz, aby toouse hello maszyny wirtualnej na nazwy DNS dla usług Reporting Services. Jeśli parametr hello hello certyfikatu należy również użyć tej nazwy i zarejestrowaniu nazwy hello globalnie na serwerze DNS.
9. skrypt Hello jest obecnie skonfigurowany dla usług Reporting Services. Toorun hello skryptów dla usług Reporting Services, zmodyfikować części wersji hello hello ścieżki toohello nazw zbyt "v11" w instrukcji hello Get-WmiObject.
10. Uruchom skrypt hello.

**Sprawdzanie poprawności**: tooverify, który hello podstawowy raport serwera działania, zobacz hello [konfiguracji hello Sprawdź](#verify-the-connection) później w tym temacie. powiązanie certyfikatu hello tooverify Otwórz wiersz polecenia z uprawnieniami administracyjnymi, a następnie uruchom następujące polecenie hello:

    netsh http show sslcert

Witaj wynik będzie zawierać następujące hello:

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>Witaj tooConfigure Użyj Menedżera konfiguracji serwera raportów
Jeśli nie chcesz, aby serwer raportów hello tooconfigure skryptu toorun hello programu PowerShell, wykonaj kroki hello w tej sekcji toouse hello usług Reporting Services w trybie macierzystym tooconfigure hello raportu serwera programu configuration manager.

1. Z hello klasycznego portalu Azure, wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk Połącz. Użyj hello nazwy użytkownika i hasła skonfigurowanego podczas tworzenia hello maszyny Wirtualnej.
   
    ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Uruchom usługę Windows update i zainstaluj aktualizacje toohello maszyny Wirtualnej. Jeśli wymagane jest ponowne uruchomienie hello maszyny Wirtualnej, uruchom ponownie hello maszyny Wirtualnej, a następnie ponownie toohello maszyny Wirtualnej z hello klasycznego portalu Azure.
3. W menu Start hello na powitania maszyny Wirtualnej, wpisz **usług Reporting Services** , a następnie otwórz **Reporting Services Configuration Manager**.
4. Pozostaw wartości domyślne hello **nazwy serwera** i **wystąpienie serwera raportów**. Kliknij przycisk **Połącz**.
5. W okienku po lewej stronie powitania kliknij **adres URL usługi sieci Web**.
6. Domyślnie RS jest skonfigurowany dla protokołu HTTP portu 80 z adresem IP "Wszystkie przypisane". tooadd HTTPS:
   
   1. W **certyfikat SSL**: hello wybierz certyfikat toouse, na przykład [Nazwa maszyny Wirtualnej]. cloudapp.net. Jeśli żadne certyfikaty nie są wyświetlane, zobacz sekcję hello **krok 2: Utworzenie certyfikatu serwera** Aby uzyskać informacje dotyczące sposobu tooinstall i zaufania hello certyfikatu na powitania maszyny Wirtualnej.
   2. W obszarze **SSL Port**: Wybierz 443. Jeśli skonfigurowano prywatnej punkt końcowy HTTPS hello w hello maszyny Wirtualnej z inną port prywatny, w tym miejscu użycie tej wartości.
   3. Kliknij przycisk **Zastosuj** i poczekaj, aż hello toocomplete operacji.
7. W okienku po lewej stronie powitania kliknij **bazy danych**.
   
   1. Kliknij przycisk **zmienić baza danych**e.
   2. Kliknij przycisk **Utwórz nową bazę danych serwera raportów** , a następnie kliknij przycisk **dalej**.
   3. Pozostaw domyślną hello **nazwy serwera**: hello wirtualna Nazwij i pozostaw domyślną hello **typ uwierzytelniania** jako **bieżącego użytkownika** — **zintegrowane zabezpieczenia**. Kliknij przycisk **Dalej**.
   4. Pozostaw domyślną hello **Nazwa bazy danych** jako **ReportServer** i kliknij przycisk **dalej**.
   5. Pozostaw domyślną hello **typ uwierzytelniania** jako **poświadczenia usługi** i kliknij przycisk **dalej**.
   6. Kliknij przycisk **dalej** na powitania **Podsumowanie** strony.
   7. Po zakończeniu konfiguracji powitania kliknij przycisk **Zakończ**.
8. W okienku po lewej stronie powitania kliknij **adres URL Menedżera raportów**. Pozostaw domyślną hello **katalogu wirtualnego** jako **raporty** i kliknij przycisk **Zastosuj**.
9. Kliknij przycisk **zakończenia** tooclose hello Reporting Services Configuration Manager.

## <a name="step-4-open-windows-firewall-port"></a>Krok 4: Port zapory systemu Windows otwórz
> [!NOTE]
> Jeśli użyto jednego serwera raportów hello hello skrypty tooconfigure, możesz pominąć tę sekcję. skrypt Hello uwzględnione port zapory hello tooopen kroku. domyślne Hello jest port 80 dla protokołu HTTP i 443 dla protokołu HTTPS.
> 
> 

tooconnect zdalnie tooReport Manager lub hello raportu Server na maszynie wirtualnej hello, punkt końcowy protokołu TCP jest wymagany na powitania maszyny Wirtualnej. Jest wymagane tooopen hello sam port w zaporze hello maszyny Wirtualnej. punkt końcowy Hello został utworzony podczas zainicjowano obsługę administracyjną hello maszyny Wirtualnej.

Ta sekcja zawiera podstawowe informacje na jak tooopen hello portu zapory. Aby uzyskać więcej informacji, zobacz [konfigurowania zapory dla dostępu do serwera raportów](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> Jeśli używasz serwera raportów hello hello skryptu tooconfigure, możesz pominąć tę sekcję. skrypt Hello uwzględnione port zapory hello tooopen kroku.
> 
> 

Jeśli port prywatny jest skonfigurowany do obsługi protokołu HTTPS innego niż 443, zmodyfikuj hello odpowiednio następującego skryptu. tooopen port **443** na powitania zapory systemu Windows, wykonaj następujące czynności hello:

1. Otwórz okno programu Windows PowerShell z uprawnieniami administracyjnymi.
2. Jeśli użyto portu innego niż 443 podczas konfigurowania punktu końcowego HTTPS hello na powitania maszyny Wirtualnej, Aktualizuj port hello w hello następujące polecenie, a następnie uruchom polecenie hello:
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Po zakończeniu wykonywania polecenia hello **Ok** jest wyświetlany w wierszu polecenia hello.

tooverify czy hello port jest otwarty, Otwórz okno programu Windows PowerShell i hello uruchom następujące polecenie:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Sprawdź konfigurację hello
tooverify, które funkcje serwera podstawowy raport hello działa, otwórz przeglądarkę z uprawnieniami administracyjnymi i przeglądania toohello następujące raportować Menedżera raportów ad serwera adresów URL:

* Na powitania maszyny Wirtualnej Przejdź toohello adres URL serwera raportów:
  
        http://localhost/reportserver
* Na powitania maszyny Wirtualnej Przejdź adres URL Menedżera raportów toohello:
  
        http://localhost/Reports
* Z komputera lokalnego Przeglądaj toohello **zdalnego** raport menedżera na powitania maszyny Wirtualnej. Aktualizacja nazwy DNS hello w hello poniższy przykład zależnie od potrzeb. Po wyświetleniu monitu o podanie hasła, Użyj poświadczeń administratora hello, utworzony zainicjowano obsługę administracyjną hello maszyny Wirtualnej. Nazwa użytkownika Hello jest hello [domena]\[nazwa użytkownika] format, w którym hello domeny jest nazwa komputera maszyny Wirtualnej hello, na przykład ssrsnativecloud\testuser. Jeśli nie używasz HTTP**S**, Usuń hello **s** w adresie URL hello. Zobacz hello następnej sekcji, aby uzyskać informacje na temat tworzenia dodatkowych użytkowników na maszynie Wirtualnej.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* Przeglądaj, adres URL serwera raportów zdalnego toohello z komputera lokalnego. Aktualizacja nazwy DNS hello w hello poniższy przykład zależnie od potrzeb. Jeśli nie używasz protokołu HTTPS, należy usunąć hello s w adresie URL hello.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>Tworzenie użytkowników i przypisywania ról
Po konfigurowania i weryfikowania hello raport serwera typowych zadań administracyjnych jest toocreate co najmniej jednego użytkownika i Przypisz użytkowników tooReporting usług ról. Aby uzyskać więcej informacji zobacz następujące hello:

* [Utwórz konto użytkownika lokalnego](https://technet.microsoft.com/library/cc770642.aspx)
* [Udziel dostępu użytkownika tooa serwer raportów (Menedżer raportów)](https://msdn.microsoft.com/library/ms156034.aspx))
* [Tworzenie i zarządzanie nimi przypisań ról](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate i opublikować raporty toohello maszyny wirtualnej platformy Azure
Witaj poniższej tabeli przedstawiono niektóre istniejące raporty toopublish dostępne opcje hello z komputera lokalnego toohello serwera raportów hostowanych na powitania maszyny wirtualnej platformy Microsoft Azure:

* **Skrypt RS.exe**: elementy raportu toocopy RS.exe Użyj skryptu z i istniejącego raportu server tooyour maszyny wirtualnej platformy Microsoft Azure. Aby uzyskać więcej informacji, zobacz sekcję hello "w trybie macierzystym tooNative tryb — maszyny wirtualnej platformy Microsoft Azure" w [próbki Reporting Services rs.exe skryptu tooMigrate zawartości między serwerami raport](https://msdn.microsoft.com/library/dn531017.aspx).
* **Report Builder**: hello maszyny wirtualnej zawiera powitania kliknij — raz wersji programu Microsoft SQL Server Report Builder. toostart raport konstruktora powitania po raz pierwszy na maszynie wirtualnej hello:
  
  1. Uruchom przeglądarkę z uprawnieniami administracyjnymi.
  2. Przeglądaj Menedżera tooreport hello maszyny wirtualnej, a następnie kliknij przycisk **Report Builder** hello Wstążce.
     
     Aby uzyskać więcej informacji, zobacz [instalowanie, odinstalowywanie i obsługa programu Report Builder](https://technet.microsoft.com/library/dd207038.aspx).
* **Programu SQL Server Data Tools: Maszyna wirtualna**: Jeśli hello maszyny Wirtualnej zostały utworzone z programu SQL Server 2012, SQL Server Data Tools jest zainstalowany na maszynie wirtualnej hello i mogą być używane toocreate **projektów serwera raportów** i raporty na powitania wirtualnego maszyny. SQL Server Data Tools można opublikować serwera raportów toohello raporty hello hello maszyny wirtualnej.
  
    Jeśli utworzono hello maszyny Wirtualnej z programem SQL server 2014, należy zainstalować Biznesowej programu SQL Server Data Tools — dla programu visual Studio. Aby uzyskać więcej informacji zobacz następujące hello:
  
  * [Microsoft SQL Server Data Tools - Business Intelligence dla programu Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools - Business Intelligence dla programu Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server Data Tools i SQL Server Business Intelligence (SSDT BI)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **Program SQL Server Data Tools: Zdalny**: na komputerze lokalnym, Utwórz projekt usług Reporting Services w programie SQL Server Data Tools, który zawiera raporty usług Reporting Services. Skonfiguruj tooconnect projektu hello toohello URL usługi sieci web.
  
    ![Właściwości projektu narzędzia SSDT dla projektu usług SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **Użyj skryptu**: Użyj zawartości serwera raportów toocopy skryptu. Aby uzyskać więcej informacji, zobacz [próbki Reporting Services rs.exe skryptu tooMigrate zawartości między serwerami raport](https://msdn.microsoft.com/library/dn531017.aspx).

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>Zminimalizować koszty, jeśli nie używasz hello maszyny Wirtualnej
> [!NOTE]
> opłaty toominimize dla maszyn wirtualnych platformy Azure nieużywane, zamknij hello maszyny Wirtualnej z hello klasycznego portalu Azure. Jeśli używasz Opcje zasilania systemu Windows hello wewnątrz tooshut maszyny Wirtualnej, dół hello maszyny Wirtualnej, są nadal naliczane hello sama kwota hello maszyny Wirtualnej. tooreduce opłat, należy tooshut dół hello maszyny Wirtualnej w hello klasycznego portalu Azure. Jeśli hello maszyny Wirtualnej nie są już potrzebne, pamiętaj hello toodelete maszyny Wirtualnej i hello VHD skojarzone opłaty za magazyn tooavoid dla plików. Aby uzyskać więcej informacji, zobacz sekcję hello — często zadawane pytania na [maszyny wirtualne — cennik](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="more-information"></a>Więcej informacji
### <a name="resources"></a>Zasoby
* Podobne zawartości związane z wdrożenia pojedynczego serwera tooa analizy biznesowej programu SQL Server i SharePoint 2013, zobacz [tooCreate Użyj środowiska Windows PowerShell Azure maszyny Wirtualnej z Biznesowej programu SQL Server i programu SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).
* Dla podobnych tooa powiązane zawartości wdrożenia wielu serwerów programu SQL Server Business Intelligence i programu SharePoint 2013, zobacz [wdrożenia programu SQL Server Business Intelligence w maszynach wirtualnych platformy Azure](https://msdn.microsoft.com/library/dn321998.aspx).
* Ogólne informacje pokrewne toodeployments analizy biznesowej programu SQL Server w maszynach wirtualnych platformy Azure, zobacz [analizy biznesowej programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).
* Aby uzyskać więcej informacji o hello koszt opłat obliczeń platformy Azure, zobacz karty maszyny wirtualnej hello [Azure Kalkulator cen](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).

### <a name="community-content"></a>Zawartość społeczności
* Aby uzyskać instrukcje krok po kroku w sposób zgłaszania toocreate tryb macierzysty usług raportowania serwera bez użycia skryptu, zobacz [Hosting usług SQL Reporting Services na maszynie wirtualnej platformy Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Łącza tooother zasoby dla programu SQL Server na maszynach wirtualnych Azure
[Program SQL Server na maszynach wirtualnych platformy Azure — omówienie](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

