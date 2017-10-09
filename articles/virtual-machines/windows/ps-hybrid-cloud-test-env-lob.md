---
title: "środowisko testowe aplikacji aaaLOB | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate opartą na sieci web, aplikacji biznesowej w hybrydowego chmury środowisko IT pro lub programowanie testowania."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Konfigurowanie aplikacji biznesowej opartej na sieci Web w chmurze hybrydowej na potrzeby testowania
Ten temat zawiera kroki tworzenia środowiska Chmury symulowane hybrydowego testowania linii opartych na sieci web aplikacji biznesowej (LOB), hostowana na platformie Microsoft Azure. Oto hello Wynikowa konfiguracja.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Ta konfiguracja obejmuje:

* Sieć lokalną symulowane hostowana na platformie Azure (hello sieci wirtualnej laboratorium testowe).
* Między różnymi lokalizacjami sieć wirtualna hostowana na platformie Azure (TestVNET).
* Połączenia sieci VPN do wirtualnymi.
* Serwer sieci web LOB, programu SQL server i dodatkowy kontroler domeny w sieci wirtualnej TestVNET hello.

Ta konfiguracja zapewnia podstawy i wspólny punkt początkowy z którego można:

* Opracowanie i przetestowanie aplikacji biznesowych hostowanych na Internet Information Services (IIS) z programu SQL Server 2014 wewnętrznej bazie danych na platformie Azure.
* Testowanie to symulowane hybrydowego oparte na chmurze IT obciążenie.

Istnieją trzy główne fazy toosetting zapasową środowiska testowego hybrydowe chmury:

1. Konfigurowanie środowiska chmury hello symulowane hybrydowego.
2. Skonfiguruj komputer serwera SQL hello (SQL1).
3. Skonfiguruj serwer LOB hello (LOB1).

To obciążenie wymaga subskrypcji platformy Azure. Jeśli masz subskrypcję MSDN lub Visual Studio, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Na przykład produkcyjnym aplikacji LOB hostowanej na platformie Azure, zobacz hello **aplikacje biznesowe** plan architektury w [diagramów architektury oprogramowania firmy Microsoft i plany](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>Faza 1: Konfigurowanie środowiska chmury hello symulowane hybrydowego
Utwórz hello [środowiska testowego chmura hybrydowa symulowane](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Ponieważ to środowisko testowe nie wymaga obecności hello hello APP1 serwera na powitania podsiecią Corpnet, można go zamknąć teraz.

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>Faza 2: Skonfiguruj komputer serwera SQL hello (SQL1)
Z hello portalu Azure uruchom komputer DC2 hello, jeśli to konieczne.

Następnie utwórz maszynę wirtualną na komputerze SQL1 przy użyciu następujących poleceń w wierszu polecenia programu Azure PowerShell na komputerze lokalnym. Toorunning poprzedniego polecenia, wypełnij hello wartości zmiennych i Usuń hello < i > znaków.

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Użyj hello tooSQL1 tooconnect portalu Azure przy użyciu konta administratora lokalnego hello SQL1.

Skonfiguruj ruchu programu SQL Server i testowania podstawowej łączności tooallow reguł zapory systemu Windows. Z wiersza polecenia środowiska Windows PowerShell uprawnień administratora na komputerze SQL1 uruchom następujące polecenia.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

polecenie ping Hello powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 192.168.0.4.

Następnie dodaj hello dodatkowe dane dysku na komputerze SQL1 jako nowy wolumin z literą dysku hello F:.

1. W okienku po lewej stronie powitania w Menedżerze serwera, kliknij przycisk **usług plików i magazynowania**, a następnie kliknij przycisk **dysków**.
2. W okienku Zawartość hello w hello **dysków** kliknij przycisk **dysk 2** (z hello **partycji** ustawić także**nieznany**).
3. Kliknij przycisk **zadania**, a następnie kliknij przycisk **nowy wolumin**.
4. Na powitania przed rozpoczęciem strony hello Kreatora nowych woluminów kliknij **dalej**.
5. Na serwerze wybierz hello hello i strona dysku, kliknij przycisk **Disk 2**, a następnie kliknij przycisk **dalej**. Po wyświetleniu monitu kliknij przycisk **OK**.
6. Na hello Określ rozmiar hello hello woluminu strony, kliknij przycisk **dalej**.
7. Na powitania Przypisz tooa dysku litery lub folderu stronie kliknij pozycję **dalej**.
8. Na stronie Ustawienia systemu wybierz Plik powitania kliknij **dalej**.
9. Na stronie opcji Potwierdź powitania kliknij **Utwórz**.
10. Po zakończeniu kliknij przycisk **Zamknij**.

Uruchom następujące polecenia w wierszu polecenia programu Windows PowerShell hello na komputerze SQL1:

    md f:\Data
    md f:\Log
    md f:\Backup

Następnie należy przyłączyć do domeny CORP Windows Server Active Directory toohello SQL1 przy użyciu następujących poleceń w wierszu polecenia programu Windows PowerShell hello na komputerze SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Użyj konta corp\użytkownik1 powitania po wyświetleniu monitu toosupply poświadczenia konta domeny dla hello **Add-Computer** polecenia.

Po ponownym uruchomieniu, użyj hello Azure portalu tooconnect tooSQL1 *z konta administratora lokalnego hello SQL1*.

Skonfiguruj program SQL Server 2014 toouse hello F: dysku dla nowych baz danych i uprawnień konta użytkownika.

1. Na ekranie startowym hello wpisz **programu SQL Server Management**, a następnie kliknij przycisk **SQL Server 2014 Management Studio**.
2. W **połączyć tooServer**, kliknij przycisk **Connect**.
3. W okienku drzewa Eksploratora obiektów hello, kliknij prawym przyciskiem myszy **SQL1**, a następnie kliknij przycisk **właściwości**.
4. W hello **właściwości serwera** okna, kliknij przycisk **ustawienia bazy danych**.
5. Zlokalizuj hello **bazy danych domyślne lokalizacje** i ustaw następujące wartości: 
   * Aby uzyskać **danych**, wpisz ścieżkę hello **f:\Data**.
   * Aby uzyskać **dziennika**, wpisz ścieżkę hello **f:\Log**.
   * Aby uzyskać **kopii zapasowej**, wpisz ścieżkę hello **f:\Backup**.
   * Uwaga: Tylko nowych baz danych użyć tych lokalizacjach.
6. Kliknij przycisk hello **OK** tooclose hello okna.
7. W hello **Eksplorator obiektów** okienku drzewa, otwórz **zabezpieczeń**.
8. Kliknij prawym przyciskiem myszy **logowania** , a następnie kliknij przycisk **nowe dane logowania**.
9. W **nazwa logowania**, typ **CORP\User1**.
10. Na powitania **ról serwera** kliknij przycisk **sysadmin**, a następnie kliknij przycisk **OK**.
11. Zamknij program Microsoft SQL Server Management Studio.

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>Faza 3: Konfigurowanie serwera LOB hello (LOB1)
Najpierw utwórz maszynę wirtualną LOB1 przy użyciu następujących poleceń w wierszu polecenia programu Azure PowerShell hello na komputerze lokalnym.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Następnie użyj hello tooLOB1 tooconnect portalu Azure przy użyciu hello poświadczeń konta administratora lokalnego hello LOB1.

Skonfiguruj ruchu tooallow reguły zapory systemu Windows, do testowania podstawowej łączności. Z wiersza polecenia środowiska Windows PowerShell uprawnień administratora na LOB1 uruchom następujące polecenia.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

polecenie ping Hello powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 192.168.0.4.

Następnie należy przyłączyć do domeny CORP usługi Active Directory toohello LOB1 przy użyciu następujących poleceń w wierszu polecenia programu Windows PowerShell hello.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Użyj konta corp\użytkownik1 powitania po wyświetleniu monitu toosupply poświadczenia konta domeny dla hello **Add-Computer** polecenia.

Po ponownym uruchomieniu komputera, należy użyć hello Azure tooconnect portalu tooLOB1 hello CORP\User1 konto i hasło.

Następnie skonfiguruj LOB1 dla usług IIS i przetestować dostęp z komputera KLIENT1.

1. W Menedżerze serwera kliknij **Dodaj role i funkcje**.
2. Na powitania **przed rozpoczęciem** kliknij przycisk **dalej**.
3. Na powitania **Wybieranie typu instalacji** kliknij przycisk **dalej**.
4. Na powitania **serwera docelowego wybierz** kliknij przycisk **dalej**.
5. Na powitania **ról serwera** kliknij przycisk **serwer sieci Web (IIS)** liście hello **ról**.
6. Po wyświetleniu monitu kliknij przycisk **Dodaj funkcje**, a następnie kliknij przycisk **dalej**.
7. Na powitania **wybierz funkcje** kliknij przycisk **dalej**.
8. Na powitania **serwer sieci Web (IIS)** kliknij przycisk **dalej**.
9. Na powitania **Wybieranie usług ról** , wybierz lub wyczyść pola wyboru hello hello usługi niezbędne do testowania aplikacji biznesowych, a następnie kliknij przycisk **dalej**.
10. Na powitania **Potwierdź wybrane opcje instalacji** kliknij przycisk **zainstalować**.
11. Zaczekać na ukończenie instalacji hello składników, a następnie kliknij przycisk **Zamknij**.
12. Z hello portalu Azure Podłącz komputer CLIENT1 toohello o poświadczenia konta corp\użytkownik1 hello, a następnie uruchom program Internet Explorer.
13. Na pasku adresu hello, wpisz **http://lob1/** , a następnie naciśnij klawisz ENTER. Powinna zostać wyświetlona hello domyślnej strony sieci web IIS 8.

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

To środowisko jest teraz gotowe do toodeploy możesz opartych na sieci web aplikacji na LOB1 i badania funkcji KLIENT1 na powitania podsiecią Corpnet.

## <a name="next-step"></a>Następny krok
* Dodaj maszynę wirtualną przy użyciu hello [portalu Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

