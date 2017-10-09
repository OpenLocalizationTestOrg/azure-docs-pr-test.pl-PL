---
title: "Witaj aaaConfigure zawsze włączone grupy dostępności, na maszynie Wirtualnej platformy Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Ten samouczek używa zasobów, które zostały utworzone za pomocą hello klasycznego modelu wdrażania. Za pomocą programu PowerShell toocreate zawsze włączonej grupy dostępności w Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>Skonfiguruj hello zawsze włączone grupy dostępności na maszynie Wirtualnej platformy Azure przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Klasycznym: interfejsu użytkownika](../classic/portal-sql-alwayson-availability-groups.md)
> * [Klasycznym: środowiska PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Przed rozpoczęciem należy wziąć pod uwagę może teraz ukończyć tego zadania w modelu Menedżera zasobów Azure. Firma Microsoft zaleca model Menedżera zasobów Azure dla nowych wdrożeń. Zobacz [programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT]
> Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager hello. Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.

Azure maszynach wirtualnych (VM) ułatwia kosztu hello toolower administratorów bazy danych systemu wysokiej dostępności programu SQL Server. Ten samouczek pokazuje, jak tooimplement dostępności grupy za pomocą programu SQL Server AlwaysOn end-to-end wewnątrz środowiska platformy Azure. Końcem hello samouczka hello rozwiązania programu SQL Server zawsze na platformie Azure będzie składać się z hello następujące elementy:

* Sieć wirtualna zawiera wiele podsieci, w tym frontonu i zaplecza podsieci.
* Kontroler domeny z domeny usługi Active Directory.
* Dwa SQL Server maszyny wirtualne, które są wdrożone toohello zaplecza podsieci i toohello przyłączone do domeny usługi Active Directory.
* Trzy węzeł klastra pracy awaryjnej systemu Windows z modelu kworum Większość węzłów hello.
* Grupa dostępności o dwóch replik z zatwierdzaniem synchronicznym bazy danych dostępności.

Ten scenariusz jest dobrym rozwiązaniem dla uproszczenia jej na platformie Azure, a nie dla jego efektywność kosztowa lub innych czynników. Na przykład można zminimalizować hello liczbę maszyn wirtualnych dla toosave grupy dostępności dwóch replik na godziny obliczeń na platformie Azure przy użyciu kontrolera domeny hello jako monitor udziału plików hello kworum w klastrze trybu failover z dwoma węzłami. Ta metoda zmniejsza liczbę maszyn wirtualnych hello przez jeden z hello powyżej konfiguracji.

Ten samouczek ma się, że tooshow hello kroki, które są wymagane tooset się hello opisano rozwiązania powyżej, bez opracowanie na powitania szczegóły każdego kroku. W związku z tym zamiast zapewniające kroków konfiguracji hello graficznego interfejsu użytkownika, używa tootake skryptów środowiska PowerShell możesz szybko za pomocą każdego kroku. Ten samouczek zakłada hello następujące czynności:

* Masz już konto platformy Azure z subskrypcją maszyny wirtualnej hello.
* Po zainstalowaniu hello [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).
* Masz już pełny opis zawsze włączonych grup dostępności dla rozwiązań lokalnych. Aby uzyskać więcej informacji, zobacz [zawsze włączonych grup dostępności (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Łączenie tooyour subskrypcji platformy Azure i tworzenie sieci wirtualnej hello
1. W oknie programu PowerShell na komputerze lokalnym zaimportować hello modułu platformy Azure, pobieranie hello maszyny tooyour pliku ustawień publikowania i połączyć tooyour sesji programu PowerShell subskrypcji platformy Azure przez zaimportowanie hello pobrać ustawień publikowania.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    Witaj **Get AzurePublishSettingsFile** polecenie automatycznie generuje certyfikat zarządzania platformy Azure i pobiera go tooyour maszyny. Przeglądarką jest automatycznie otwierane i masz poświadczeń konta Microsoft hello zostanie wyświetlony monit o tooenter dla subskrypcji platformy Azure. Witaj pobrane **.publishsettings** plik zawiera wszystkie informacje hello muszą toomanage subskrypcji platformy Azure. Po zapisaniu tego pliku tooa lokalnego katalogu, zaimportuj go za pomocą hello **AzurePublishSettingsFile importu** polecenia.

   > [!NOTE]
   > plik .publishsettings Hello zawiera swoje poświadczenia (Niezakodowane), które są używane tooadminister subskrypcji platformy Azure i usługi. Hello ze względów bezpieczeństwa dla tego pliku jest toostore go tymczasowo poza katalogów źródła (na przykład w folderze Libraries\Documents hello), a następnie usuń, po zakończeniu importowania hello. Złośliwy użytkownik uzyska dostęp toohello .publishsettings plik można edytować, tworzenia i usuwania usług Azure.

2. Zdefiniuj szereg zmiennych czy użyjesz toocreate chmury infrastruktury IT.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    Należy zwrócić uwagę toohello po tooensure, który poleceniach powiedzie się później:

   * Zmienne **$storageAccountName** i **$dcServiceName** musi być unikatowa, ponieważ są one używane tooidentify Twojego konta magazynu w chmurze i serwera chmurowego, odpowiednio na powitania Internet.
   * Witaj nazw określonych dla zmiennych **$affinityGroupName** i **$virtualNetworkName** są skonfigurowane w dokumencie hello konfiguracji sieci wirtualnej, który będzie potrzebny później.
   * **$sqlImageName** Określa nazwę hello zaktualizowane hello obrazu maszyny Wirtualnej, która zawiera SQL Server 2012 Service Pack 1 Enterprise Edition.
   * Dla uproszczenia **Contoso! 000** jest hello samo hasło, które jest używane w całej samouczek hello.

3. Utwórz grupę koligacji.

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. Tworzenie sieci wirtualnej przez zaimportowanie pliku konfiguracji.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    plik konfiguracji Hello zawiera powitania po dokumentu XML. Krótko mówiąc, określa sieć wirtualną o nazwie **ContosoNET** w grupie koligacji hello o nazwie **ContosoAG**. Ma przestrzeń adresowa hello **10.10.0.0/16** i ma dwie podsieci **10.10.1.0/24** i **10.10.2.0/24**, które są podsieci frontonu hello wstecz podsieci odpowiednio. podsieci frontonu Hello jest umieszczane aplikacji klienckich, takich jak Microsoft SharePoint. Hello wstecz podsieci będą umieszczane są hello maszynach wirtualnych serwera SQL. Jeśli zmienisz hello **$affinityGroupName** i **$virtualNetworkName** zmienne wcześniej, należy również zmienić hello odpowiadającego poniższe nazwy.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Utwórz konto magazynu, który został skojarzony z grupą koligacji hello utworzone i jest ustawiony jako hello bieżącego konta magazynu w ramach subskrypcji.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Utwórz serwer kontrolera domeny hello w hello nowe chmury usługi i zestawu dostępności.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    Te polecenia gazociągami hello następujących czynności:

   * **Nowy AzureVMConfig** tworzy konfiguracji maszyny Wirtualnej.
   * **Dodaj AzureProvisioningConfig** zapewnia hello parametry konfiguracji autonomicznej systemu Windows Server.
   * **Dodaj AzureDataDisk** dodaje hello dysk danych, które będzie używane do przechowywania danych usługi Active Directory z hello buforowanie tooNone zestawu opcji.
   * **Nowy AzureVM** tworzy nową usługę w chmurze oraz hello nowej maszyny Wirtualnej platformy Azure w hello nową usługę w chmurze.

7. Poczekaj, aż hello nowej maszyny Wirtualnej toobe w pełni zaaprowizowanym i Pobierz katalog roboczy tooyour hello w pliku pulpitu zdalnego. Ponieważ hello nowej maszyny Wirtualnej Azure ma tooprovision dużo czasu, hello `while` Pętla kontynuuje toopoll hello nowej maszyny Wirtualnej, dopóki nie jest gotowa do użycia.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

Serwer kontrolera domeny Hello pomyślnie jest teraz udostępniony. Następnie należy skonfigurować domeny usługi Active Directory hello na tym serwerze kontrolera domeny. Pozostaw otwarte okno programu PowerShell hello na komputerze lokalnym. Służy on ponownie nowsze toocreate hello dwóch maszyn wirtualnych programu SQL Server.

## <a name="configure-hello-domain-controller"></a>Konfiguracja kontrolera domeny hello
1. Połącz serwer kontrolera domeny toohello uruchamiając hello pliku pulpitu zdalnego. Użyj administrator maszyny hello AzureAdmin nazwy użytkownika i hasła **Contoso! 000**, która została określona podczas tworzenia hello nowej maszyny Wirtualnej.
2. Otwórz okno programu PowerShell w trybie administratora.
3. Uruchom następujące hello **DCPROMO. EXE** tooset polecenia zapasowej hello **corp.contoso.com** domeny z katalogów hello danych znajdujących się na dysku M.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Po zakończeniu działania polecenia hello hello maszyny Wirtualnej powoduje automatyczne ponowne uruchomienie.

4. Połącz serwer kontrolera domeny toohello ponownie uruchamiając hello pliku pulpitu zdalnego. Teraz, zaloguj się jako **CORP\Administrator**.
5. Otwórz okno programu PowerShell w trybie administratora i zaimportować moduł środowiska PowerShell usługi Active Directory hello przy użyciu hello następujące polecenie:

        Import-Module ActiveDirectory

6. Uruchom następujące polecenia tooadd trzech użytkowników toohello domeny hello.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** wszystko, co jest używane tooconfigure związane z wystąpień usługi programu SQL Server toohello hello klastra pracy awaryjnej i hello grupy dostępności. **CORP\SQLSvc1** i **CORP\SQLSvc2** są używane jako konto usługi programu SQL Server hello hello dwóch maszyn wirtualnych z serwera SQL.
7. Witaj dalej, uruchom następujące polecenia toogive **CORP\Install** hello uprawnienia toocreate obiektów typu komputer w domenie hello.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    Witaj GUID wymienione powyżej jest hello identyfikatora GUID dla typu obiektu komputera hello. Witaj **CORP\Install** konto musi hello **Odczyt wszystkich właściwości** i **tworzenia obiektów komputerów** Active bezpośredniego hello toocreate uprawnień obiektów na powitania trybu failover klaster. Witaj **Odczyt wszystkich właściwości** już pozwolono tooCORP\Install domyślnie, więc nie trzeba toogrant go jawnie. Aby uzyskać więcej informacji dotyczących uprawnień, które są potrzebne klastra pracy awaryjnej hello toocreate, zobacz [przewodnik krok po kroku klastra pracy awaryjnej: Konfigurowanie kont w usłudze Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).

    Teraz, po zakończeniu konfigurowania usługi Active Directory i obiektów użytkowników hello, będzie utworzyć dwóch maszyn wirtualnych programu SQL Server i dołącz je toothis domeny.

## <a name="create-hello-sql-server-vms"></a>Tworzenie maszyn wirtualnych hello programu SQL Server
1. Nadal okno programu PowerShell hello toouse, który jest otwarty na komputerze lokalnym. Zdefiniuj hello następujące dodatkowe zmienne:

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    Witaj adres IP **10.10.0.4** zwykle przypisano toohello pierwsza maszyna wirtualna, które są tworzone w hello **10.10.0.0/16** podsieci sieci wirtualnej platformy Azure. Należy sprawdzić, czy jest hello adres serwera kontrolera domeny, uruchamiając **IPCONFIG**.
2. O nazwie maszyny Wirtualnej w klastrze pracy awaryjnej hello hello uruchom następujące polecenia gazociągami toocreate hello najpierw **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    Należy uwzględnić następujące hello dotyczące hello polecenie powyżej:

   * **Nowy AzureVMConfig** tworzy konfiguracji maszyny Wirtualnej o nazwie zestaw żądaną dostępności hello. Witaj kolejnych maszyn wirtualnych zostanie utworzony z hello sama nazwa zbioru dostępności, dzięki czemu są one przyłączone toohello tego samego zestawu dostępności.
   * **Dodaj AzureProvisioningConfig** sprzężenia hello domeny usługi Active Directory toohello maszyny Wirtualnej został utworzony.
   * **Zestaw AzureSubnet** miejsca hello maszyn wirtualnych w podsieci wstecz hello.
   * **Nowy AzureVM** tworzy nową usługę w chmurze oraz hello nowej maszyny Wirtualnej platformy Azure w hello nową usługę w chmurze. Witaj **DnsSettings** parametr określa tego serwera DNS hello hello serwerów w hello nową usługę w chmurze ma adres IP hello **10.10.0.4**. Jest to adres IP serwera kontrolera domeny hello hello. Ten parametr jest potrzebny tooenable hello nowych maszyn wirtualnych w domenie usługi Active Directory toohello toojoin hello chmury usługi pomyślnie. Bez tego parametru należy ręcznie ustawić hello ustawieniami adresu IPv4 na serwerze kontrolera domeny hello toouse maszyny Wirtualnej jako podstawowy serwer DNS powitania po hello maszyny Wirtualnej jest udostępniane, a następnie dołącz do domeny usługi Active Directory toohello wirtualna hello.
3. Uruchom powitania po gazociągami polecenia hello toocreate maszynach wirtualnych serwera SQL o nazwie **ContosoSQL1** i **ContosoSQL2**.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    Należy uwzględnić następujące hello dotyczące powyższych poleceń hello:

   * **Nowy AzureVMConfig** używa hello tego samego nazwa zbioru dostępności jako serwer kontrolera domeny hello i SQL Server 2012 Service Pack 1 Enterprise Edition obraz w galerii maszyn wirtualnych hello hello używa. Ustawia również hello działania systemu dysku tooread buforowania tylko (nie buforowania zapisu). Zaleca się przeprowadzenie migracji hello dysku bazy danych plików tooa odrębne dołączyć toohello maszyny Wirtualnej i skonfigurować go odczytu lub buforowanie zapisu. Następnym krokiem hello jest jednak Read tooremove buforowanie zapisu na dysku systemu operacyjnego hello, ponieważ nie można usunąć buforowanie na powitania dysku systemu operacyjnego.
   * **Dodaj AzureProvisioningConfig** sprzężenia hello domeny usługi Active Directory toohello maszyny Wirtualnej został utworzony.
   * **Zestaw AzureSubnet** miejsca hello maszyn wirtualnych w podsieci wstecz hello.
   * **Dodaj AzureEndpoint** dodaje punkty końcowe dostępu, dzięki czemu aplikacje klienckie mogą uzyskiwać dostęp do tych wystąpień usługi programu SQL Server na powitania Internet. Inne porty są podane tooContosoSQL1 i ContosoSQL2.
   * **Nowy AzureVM** tworzy hello nową maszynę Wirtualną programu SQL Server w hello sama usługa w chmurze jako ContosoQuorum. Maszyny wirtualne hello należy umieścić w hello sama usługa w chmurze należy je toobe w hello na tym samym zestawie dostępności.
4. Poczekaj dla każdego toobe maszyny Wirtualnej, w pełni zaaprowizowanym i dla każdej maszyny Wirtualnej toodownload katalog roboczy tooyour jego pliku pulpitu zdalnego. Witaj `for` pętli przełączanie po kolei hello trzech nowych maszyn wirtualnych i wykonuje polecenia hello wewnątrz nawiasów klamrowych hello najwyższego poziomu dla każdego z nich.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    teraz udostępnieniu Hello maszynach wirtualnych serwera SQL i uruchomiona, ale są zainstalowane z programem SQL Server z opcji domyślnych.

## <a name="initialize-hello-failover-cluster-vms"></a>Inicjowanie hello klastra trybu failover maszyny wirtualne
W tej sekcji należy toomodify hello trzy serwery będą używane w hello klastra pracy awaryjnej i hello instalacji programu SQL Server. W szczególności:

* Wszystkie serwery: należy tooinstall hello **klaster pracy awaryjnej** funkcji.
* Wszystkie serwery: należy tooadd **CORP\Install** jako maszyna hello **administratora**.
* ContosoSQL1 i ContosoSQL2 tylko: należy tooadd **CORP\Install** jako **sysadmin** roli w hello domyślnej bazy danych.
* ContosoSQL1 i ContosoSQL2 tylko: należy tooadd **NT AUTHORITY\System** jako logowanie z hello następujących uprawnień:

  * Instrukcja ALTER żadnej grupy dostępności
  * Połączenia SQL
  * Widok stanu serwera
* ContosoSQL1 i ContosoSQL2 tylko: hello **TCP** na powitania maszyny Wirtualnej programu SQL Server jest już włączony protokół. Jednak nadal potrzebujesz tooopen hello zapory dla dostępu zdalnego programu SQL Server.

Teraz możesz toostart gotowe. Począwszy od **ContosoQuorum**, wykonaj poniższe kroki hello:

1. Połącz za**ContosoQuorum** uruchamiając hello pliki pulpitu zdalnego. Użyj nazwy użytkownika administrator maszyny hello **AzureAdmin** i hasło **Contoso! 000**, określony podczas tworzenia maszyn wirtualnych hello.
2. Sprawdź, czy hello komputery zostały pomyślnie dołączono zbyt**corp.contoso.com**.
3. Poczekaj, aż toofinish instalacji programu SQL Server hello uruchomionych zadań inicjowania automatycznego hello przed kontynuowaniem.
4. Otwórz okno programu PowerShell w trybie administratora.
5. Zainstaluj funkcję Klaster pracy awaryjnej systemu Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Dodaj **CORP\Install** jako administrator lokalny.

        net localgroup administrators "CORP\Install" /Add
7. Wyloguj ContosoQuorum. Gotowe z tym serwerem teraz.

        logoff.exe

Następnie należy zainicjować **ContosoSQL1** i **ContosoSQL2**. Wykonaj hello poniższe czynności, które są identyczne dla obu maszynach wirtualnych serwera SQL.

1. Połącz toohello dwóch maszyn wirtualnych z serwera SQL, uruchamiając hello pliki pulpitu zdalnego. Użyj nazwy użytkownika administrator maszyny hello **AzureAdmin** i hasło **Contoso! 000**, określony podczas tworzenia maszyn wirtualnych hello.
2. Sprawdź, czy hello komputery zostały pomyślnie dołączono zbyt**corp.contoso.com**.
3. Poczekaj, aż toofinish instalacji programu SQL Server hello uruchomionych zadań inicjowania automatycznego hello przed kontynuowaniem.
4. Otwórz okno programu PowerShell w trybie administratora.
5. Zainstaluj funkcję Klaster pracy awaryjnej systemu Windows hello.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Dodaj **CORP\Install** jako administrator lokalny.

        net localgroup administrators "CORP\Install" /Add
7. Importuj hello dostawcy programu PowerShell programu SQL Server.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. Dodaj **CORP\Install** jako hello roli administratora systemu dla hello domyślnego wystąpienia programu SQL Server.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. Dodaj **NT AUTHORITY\System** jako logowanie z uprawnieniami hello trzech opisanych powyżej.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. Otwórz zaporę Windows hello dla dostępu zdalnego programu SQL Server.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. Wyloguj obie maszyny wirtualne.

         logoff.exe

Na koniec wszystko jest gotowe tooconfigure hello dostępności grupy. Użyjesz tooperform dostawcy programu PowerShell programu SQL Server hello całe hello pracować w **ContosoSQL1**.

## <a name="configure-hello-availability-group"></a>Skonfiguruj grupy dostępności hello
1. Połącz za**ContosoSQL1** ponownie, uruchamiając hello pliki pulpitu zdalnego. Zamiast logowanie się przy użyciu konta komputera hello, zaloguj się przy użyciu **CORP\Install**.
2. Otwórz okno programu PowerShell w trybie administratora.
3. Zdefiniuj hello następujące zmienne:

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. Importuj hello dostawcy programu PowerShell programu SQL Server.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. Zmień hello konta usługi programu SQL Server dla ContosoSQL1 tooCORP\SQLSvc1.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. Zmień hello konta usługi programu SQL Server dla ContosoSQL2 tooCORP\SQLSvc2.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. Pobierz **CreateAzureFailoverCluster.ps1** z [Tworzenie klastra trybu Failover dla zawsze włączonych grup dostępności w maszynie Wirtualnej platformy Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello lokalny katalog roboczy. Użyjesz tego toohelp skryptu tworzenia klastra trybu failover funkcjonalności. Ważne informacje na jak klaster pracy awaryjnej systemu Windows współdziała z hello Azure sieciowy, zobacz [wysokiej dostępności i odzyskiwania po awarii dla programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).
8. Zmień katalog roboczy tooyour i utworzyć klaster trybu failover hello ze skryptem hello pobrane.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Włącz zawsze włączone grupy dostępności dla wystąpień programu SQL Server domyślne hello **ContosoSQL1** i **ContosoSQL2**.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. Utwórz katalog kopii zapasowej i przydziel uprawnienia dla kont usług programu SQL Server hello. Użyjesz bazy danych dostępności tego katalogu tooprepare hello na powitania repliki pomocniczej.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. Utwórz bazę danych na **ContosoSQL1** o nazwie **MyDB1**przełączyć pełnej kopii zapasowej i kopii zapasowej dziennika i przywróci je na **ContosoSQL2** z hello **WITH NORECOVERY** opcji.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Utwórz punkty końcowe grupy dostępności hello na powitania maszynach wirtualnych serwera SQL i ustaw hello odpowiednie uprawnienia na powitania punktów końcowych.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Utwórz hello replik dostępności.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. Na koniec Utwórz hello grupy dostępności i grupy dostępności toohello sprzężenia hello repliki pomocniczej.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>Następne kroki
Możesz teraz pomyślnie zaimplementowano program SQL Server AlwaysOn przez utworzenie grupy dostępności na platformie Azure. tooconfigure odbiornika dla tej grupy dostępności, zobacz [skonfigurować odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-int-listener.md).

Aby uzyskać inne informacje o korzystaniu z programu SQL Server na platformie Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
