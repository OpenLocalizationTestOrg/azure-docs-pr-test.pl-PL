---
title: "aaaCreate maszyny Wirtualnej systemu Windows przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Tworzenie maszyn wirtualnych z systemem Windows przy użyciu programu Azure PowerShell i hello klasycznego modelu wdrażania."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>Utwórz maszynę wirtualną systemu Windows z programu PowerShell i hello klasycznego modelu wdrażania
> [!div class="op_single_selector"]
> * [Portal Azure — systemu Windows](tutorial.md)
> * [PowerShell — systemu Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Te kroki pokazują, jak toocustomize zestaw programu Azure PowerShell polecenia, który utworzyć i wstępnie skonfigurować maszyny wirtualnej opartych na systemie Windows Azure przy użyciu podejścia bloku konstrukcyjnego. Można użyć tego procesu tooquickly utworzyć zestaw poleceń dla nowej maszyny wirtualnej z systemem Windows i rozwiń istniejącego wdrożenia lub toocreate polecenia wiele zestawów szybkiego tworzenia i testowania niestandardowych lub środowisku specjalista IT.

Te kroki należy wykonać podejście wypełniania-w — przeznaczone do bezpośredniego tworzenia zestawy poleceń programu PowerShell systemu Azure. Takie podejście może być przydatna, jeśli są nowe tooPowerShell lub chcesz tooknow toospecify jakie wartości dla Konfiguracja zakończyła się pomyślnie. Użytkownicy zaawansowani programu PowerShell można wykonać polecenia hello i podstaw wartości zmiennych hello (hello wiersze rozpoczynające się od "$").

Jeśli jeszcze tego nie zrobiono tego wcześniej, użyj instrukcji hello w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) tooinstall programu Azure PowerShell na komputerze lokalnym. Następnie należy otworzyć wiersz polecenia programu Windows PowerShell.

## <a name="step-1-add-your-account"></a>Krok 1: Dodaj swoje konto
1. W wierszu polecenia programu PowerShell hello, wpisz **Add-AzureAccount** i kliknij przycisk **Enter**. 
2. Wpisz adres e-mail hello skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**. 
3. Wpisz hasło powitania dla Twojego konta. 
4. Kliknij przycisk **Zaloguj**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Krok 2: Ustaw subskrypcji i konto magazynu
Ustaw Twojej subskrypcji platformy Azure i konto magazynu, uruchamiając następujące polecenia w wierszu polecenia programu Windows PowerShell hello. Zamień wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, hello poprawne nazwy.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Nazwa subskrypcji poprawne hello można pobrać z hello Właściwość Nazwa subskrypcji hello dane wyjściowe hello **Get-AzureSubscription** polecenia. Można uzyskać nazwy konta magazynu poprawne hello hello właściwości Label hello dane wyjściowe hello **Get-AzureStorageAccount** polecenia po uruchomieniu hello **AzureSubscription wybierz** polecenia.

## <a name="step-3-determine-hello-imagefamily"></a>Krok 3: Określanie hello ImageFamily
Następnie należy toodetermine hello ImageFamily lub wartość etykiety dla odpowiedniego toohello określony obraz powitania ma toocreate maszyny wirtualnej platformy Azure. Możesz uzyskać hello listę dostępnych wartości ImageFamily za pomocą tego polecenia.

    Get-AzureVMImage | select ImageFamily -Unique

Poniżej przedstawiono przykładowe wartości ImageFamily dla komputerów z systemem Windows:

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1
* Windows Server 2016 Technical Preview 4
* SQL Server 2012 z dodatkiem SP1 Enterprise w systemie Windows Server 2012

Jeśli okaże się obraz powitania, którego szukasz, otwórz wystąpienie świeże hello edytora tekstu, wybór lub hello PowerShell Integrated Scripting Environment (ISE). Skopiuj następujące hello do nowego pliku tekstowego hello lub hello PowerShell ISE, zastępując wartości ImageFamily hello.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

W niektórych przypadkach hello nazwa obrazu jest hello zamiast hello ImageFamily wartość właściwości etykiety. Jeśli nie możesz znaleźć hello obrazu, który chcesz uzyskać za pomocą właściwości ImageFamily hello, listy obrazów hello za ich właściwości Label, przy użyciu tego polecenia.

    Get-AzureVMImage | select Label -Unique

Jeśli okaże się hello prawy obraz za pomocą tego polecenia, otwórz wystąpienie świeże hello edytora tekstu, wybór lub hello PowerShell ISE. Skopiuj następujące hello do nowego pliku tekstowego hello lub hello PowerShell ISE, zastępując wartość etykiety hello.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>Krok 4: Utwórz zestaw poleceń
Tworzenie rest hello polecenia ustawione przez kopiowanie hello odpowiedni zestaw bloków poniżej do nowego pliku tekstowego lub hello ISE i następnie wypełnianie hello wartości zmiennych i usuwanie hello < i > znaków. Zobacz hello dwa [przykłady](#examples) na końcu hello ten artykuł, aby pomysł hello wynik końcowy.

Uruchom polecenie ustawić, wybierając jedną z tych bloków dwa polecenia (wymagane).

Opcja 1: Określ nazwę maszyny wirtualnej i rozmiarze.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Opcja 2: Określ nazwę, rozmiar i nazwa zbioru dostępności.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

Witaj InstanceSize wartości dla D, DS lub G serii maszyn wirtualnych, zobacz [maszyny wirtualnej i rozmiary usługi chmury Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

> [!NOTE]
> Jeśli masz umowy Enterprise Agreement z Software Assurance i mają tootake zaletą hello systemu Windows Server [korzyści Użyj hybrydowego](https://azure.microsoft.com/pricing/hybrid-use-benefit/), Dodaj **- LicenseType** toohello parametru  **Nowy AzureVMConfig** polecenia cmdlet, przekazanie wartości hello **Windows_Server** hello typowy przypadek użycia.  Upewnij się, że używasz obrazu, które zostały przekazane; Nie można używać standardowy obraz z galerii hello hello korzyści użyć hybrydowego.
> 
> 

Opcjonalnie na autonomicznym komputerze z systemem Windows Określ hello konta administratora lokalnego i hasło.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

Wybierz silne hasło. toocheck jego siły, zobacz [narzędzie do sprawdzania haseł: używanie silnych haseł](https://www.microsoft.com/security/pc-security/password-checker.aspx).

Opcjonalnie hello tooadd Windows komputera tooan istniejącej domeny usługi Active Directory, określ hello konta administratora lokalnego i hasło, hello domeny i hello nazwę i hasło konta domeny.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Dla dodatkowych opcji konfiguracji wstępnej dla maszyn wirtualnych z systemem Windows, zobacz składnię hello hello **Windows** i **WindowsDomain** zestawy parametrów [ Dodaj AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).

Określony adres IP, znany jako statyczny adres DIP opcjonalnie przypisać hello maszyny wirtualnej.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

Można sprawdzić, czy określony adres IP jest dostępna w programie:

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

Opcjonalnie można przypisać określonej podsieci tooa hello maszyny wirtualnej w sieci wirtualnej platformy Azure.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

Opcjonalnie dodaj maszynę wirtualną toohello danych jednego dysku.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Kontroler domeny usługi Active Directory, ustawić $hcaching także "None".

Opcjonalnie dodaj hello maszyny wirtualnej tooan istniejącego zestawu równoważeniem obciążenia dla zewnętrznego ruchu.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

Na koniec wybierz jedną z tych bloków polecenia wymagane do utworzenia maszyny wirtualnej hello.

Opcja 1: Utworzenie maszyny wirtualnej hello w istniejącej usługi w chmurze.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

Krótka nazwa usługi w chmurze hello Hello jest nazwą hello jest widoczna na liście hello usługi w chmurze w portalu Azure hello lub liście hello grup zasobów w portalu Azure hello.

Opcja 2: Utworzenie maszyny wirtualnej hello w istniejącej usługi chmury i sieci wirtualnej.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>Krok 5: Uruchom polecenie zestawu
Przejrzyj zestaw poleceń programu Azure PowerShell hello, które zostały utworzone w edytorze tekstu lub hello PowerShell ISE składające się z wielu bloków poleceń z kroku 4. Upewnij się określono wszystkie zmienne hello potrzebne i mają poprawne wartości hello. Upewnij się, że zostały usunięte wszystkie znaki hello < i > również.

Jeśli korzystasz z edytora tekstów, polecenie hello kopiowania ustawić toohello Schowka i kliknij prawym przyciskiem myszy Otwórz wiersz polecenia programu Windows PowerShell. To wystawiać zestaw poleceń hello jako serię poleceń programu PowerShell i utworzyć maszyny wirtualnej platformy Azure. Alternatywnie Uruchom polecenie hello w hello PowerShell ISE.

Jeśli zostanie utworzony ponownie tę maszynę wirtualną lub podobne jeden, możesz:

* Zapisz to polecenie Ustaw jako plik skryptu programu PowerShell (*.ps1).
* Zapisz to polecenie Ustaw jako element runbook usługi Automatyzacja Azure w hello **kont automatyzacji** sekcji hello portalu Azure.

## <a id="examples"></a>Przykłady
Poniżej przedstawiono dwa przykłady użycia hello powyższą toobuild zestawy poleceń programu Azure PowerShell, utworzonych opartych na systemie Windows Azure maszyny wirtualnej.

### <a name="example-1"></a>Przykład 1
Potrzebuję programu PowerShell polecenia set toocreate hello początkowej maszyny wirtualnej do kontrolera domeny usługi Active Directory:

* Używa hello obrazu systemu Windows Server 2012 R2 Datacenter.
* Ma nazwę hello AZDC1.
* Jest komputerem autonomicznym.
* Ma dysk danych dodatkowych 20 GB.
* Ma statyczny adres IP hello 192.168.244.4.
* Znajduje się w podsieci wewnętrznej bazy danych hello hello AZDatacenter wirtualnej sieci.
* Jest hello Azure TailspinToys w usłudze w chmurze.

Oto hello odpowiedniego programu Azure PowerShell polecenia set toocreate tej maszyny wirtualnej z puste wiersze między każdy blok dla czytelności.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>Przykład 2
Potrzebuję programu PowerShell zestawu poleceń toocreate maszyny wirtualnej dla serwera biznesowych — które:

* Używa hello obrazu systemu Windows Server 2012 R2 Datacenter.
* Ma nazwę hello LOB1.
* Jest elementem członkowskim domeny corp.contoso.com hello.
* Ma dysk danych dodatkowych 200 GB.
* Znajduje się w podsieci frontonu hello hello AZDatacenter wirtualnej sieci.
* Jest hello Azure TailspinToys w usłudze w chmurze.

Oto hello odpowiedniego programu Azure PowerShell polecenia set toocreate tej maszyny wirtualnej.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>Następne kroki
Jeśli potrzebujesz dysk systemu operacyjnego, który jest większy niż 127 GB, możesz [rozwiń dysk systemu operacyjnego hello](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

