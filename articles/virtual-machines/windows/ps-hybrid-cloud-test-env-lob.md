---
title: "Środowisko testowe aplikacji LOB | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia opartych na sieci web wiersza aplikacji biznesowej w środowisku chmury hybrydowej dla IT pro lub programowanie testowania."
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
ms.openlocfilehash: 8e9a380458bfede80ed0fc1ee7e62b0caec09501
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Konfigurowanie aplikacji biznesowej opartej na sieci Web w chmurze hybrydowej na potrzeby testowania
Ten temat zawiera kroki tworzenia środowiska Chmury symulowane hybrydowego testowania linii opartych na sieci web aplikacji biznesowej (LOB), hostowana na platformie Microsoft Azure. Oto wynikowej konfiguracji.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Ta konfiguracja obejmuje:

* Sieć lokalną symulowane hostowana na platformie Azure (VNet laboratorium testowe).
* Między różnymi lokalizacjami sieć wirtualna hostowana na platformie Azure (TestVNET).
* Połączenia sieci VPN do wirtualnymi.
* Serwer sieci web LOB, programu SQL server i dodatkowy kontroler domeny w sieci wirtualnej TestVNET.

Ta konfiguracja zapewnia podstawy i wspólny punkt początkowy z którego można:

* Opracowanie i przetestowanie aplikacji biznesowych hostowanych na Internet Information Services (IIS) z programu SQL Server 2014 wewnętrznej bazie danych na platformie Azure.
* Testowanie to symulowane hybrydowego oparte na chmurze IT obciążenie.

Istnieją trzy główne fazy do konfigurowania tego środowiska testowego chmury hybrydowej:

1. Konfigurowanie hybrydowego symulowane środowiska chmury.
2. Skonfiguruj komputer serwera SQL (SQL1).
3. Skonfiguruj serwer LOB (LOB1).

To obciążenie wymaga subskrypcji platformy Azure. Jeśli masz subskrypcję MSDN lub Visual Studio, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Na przykład produkcyjnym aplikacji LOB hostowanej na platformie Azure, zobacz **aplikacje biznesowe** plan architektury w [diagramów architektury oprogramowania firmy Microsoft i plany](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-the-simulated-hybrid-cloud-environment"></a>Faza 1: Konfigurowanie środowiska Chmury symulowane hybrydowego
Utwórz [środowiska testowego chmura hybrydowa symulowane](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Ponieważ to środowisko testowe nie wymaga obecności serwera APP1 w podsieci Corpnet, można go zamknąć teraz.

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-the-sql-server-computer-sql1"></a>Faza 2: Skonfiguruj komputer serwera SQL (SQL1)
W portalu Azure uruchom komputer DC2, w razie potrzeby.

Następnie utwórz maszynę wirtualną na komputerze SQL1 przy użyciu następujących poleceń w wierszu polecenia programu Azure PowerShell na komputerze lokalnym. Przed uruchomieniem tych poleceń, wypełnij wartości zmiennych i Usuń < i > znaków.

    $rgName="<your resource group name>"
    $locName="<the Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type the name and password of the local administrator account for the SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Użyj portalu Azure, aby nawiązać połączenie komputera SQL1 przy użyciu konta administratora lokalnego komputera SQL1.

Następnie można skonfigurować reguł zapory systemu Windows, aby umożliwić testowanie podstawowej łączności i ruchu programu SQL Server. Z wiersza polecenia środowiska Windows PowerShell uprawnień administratora na komputerze SQL1 uruchom następujące polecenia.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

Polecenie ping powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 192.168.0.4.

Następnie dodaj jako nowy wolumin z literą dysku F: dysku dodatkowe dane SQL1.

1. W lewym okienku w Menedżerze serwera kliknij **usług plików i magazynowania**, a następnie kliknij przycisk **dysków**.
2. W okienku Zawartość w **dysków** kliknij przycisk **dysk 2** (z **partycji** ustawioną **nieznany**).
3. Kliknij przycisk **zadania**, a następnie kliknij przycisk **nowy wolumin**.
4. Na stronie zanim rozpoczniesz Kreator nowego woluminu, kliknij przycisk **dalej**.
5. Na stronie wybierz serwer i strona dysku kliknij **Disk 2**, a następnie kliknij przycisk **dalej**. Po wyświetleniu monitu kliknij przycisk **OK**.
6. Na stronie Określ rozmiar strony wolumin, kliknij przycisk **dalej**.
7. Przypisz do strony dysku litery lub folderu, wybierz polecenie **dalej**.
8. Na stronie Wybieranie pliku ustawień systemu kliknij **dalej**.
9. Na stronie Potwierdzanie opcji kliknij przycisk **Utwórz**.
10. Po zakończeniu kliknij przycisk **Zamknij**.

Uruchom następujące polecenia w wierszu polecenia programu Windows PowerShell na komputerze SQL1:

    md f:\Data
    md f:\Log
    md f:\Backup

Następnie należy dołączyć komputer SQL1 do domeny CORP Windows Server Active Directory przy użyciu następujących poleceń w wierszu polecenia programu Windows PowerShell na komputerze SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Użyj konta corp\użytkownik1 po wyświetleniu monitu o podanie poświadczeń konta domeny dla **Add-Computer** polecenia.

Po ponownym uruchomieniu, użyj portalu Azure do nawiązania połączenia SQL1 *z konta administratora lokalnego komputera SQL1*.

Skonfiguruj program SQL Server 2014 do użytku F: dysku dla nowych baz danych oraz uprawnień konta użytkownika.

1. Na ekranie startowym wpisz **programu SQL Server Management**, a następnie kliknij przycisk **SQL Server 2014 Management Studio**.
2. W **Połącz z serwerem**, kliknij przycisk **Connect**.
3. W okienku drzewa Eksploratora obiektów kliknij prawym przyciskiem myszy **SQL1**, a następnie kliknij przycisk **właściwości**.
4. W **właściwości serwera** okna, kliknij przycisk **ustawienia bazy danych**.
5. Zlokalizuj **bazy danych domyślne lokalizacje** i ustaw następujące wartości: 
   * Aby uzyskać **danych**, wpisz ścieżkę **f:\Data**.
   * Aby uzyskać **dziennika**, wpisz ścieżkę **f:\Log**.
   * Aby uzyskać **kopii zapasowej**, wpisz ścieżkę **f:\Backup**.
   * Uwaga: Tylko nowych baz danych użyć tych lokalizacjach.
6. Kliknij przycisk **OK** aby zamknąć okno.
7. W **Eksplorator obiektów** okienku drzewa, otwórz **zabezpieczeń**.
8. Kliknij prawym przyciskiem myszy **logowania** , a następnie kliknij przycisk **nowe dane logowania**.
9. W **nazwa logowania**, typ **CORP\User1**.
10. Na **ról serwera** kliknij przycisk **sysadmin**, a następnie kliknij przycisk **OK**.
11. Zamknij program Microsoft SQL Server Management Studio.

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-the-lob-server-lob1"></a>Faza 3: Konfigurowanie serwera LOB (LOB1)
Najpierw utwórz maszynę wirtualną LOB1 przy użyciu następujących poleceń w wierszu polecenia programu Azure PowerShell na komputerze lokalnym.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Następnie użyj portalu Azure, aby nawiązać połączenie przy użyciu poświadczeń konta administratora lokalnego LOB1 LOB1.

Skonfiguruj regułę zapory systemu Windows, aby zezwolić na ruch do testowania podstawowej łączności. Z wiersza polecenia środowiska Windows PowerShell uprawnień administratora na LOB1 uruchom następujące polecenia.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

Polecenie ping powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 192.168.0.4.

Następnie dołącz LOB1 do domeny usługi Active Directory CORP, przy użyciu następujących poleceń w wierszu polecenia programu Windows PowerShell.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Użyj konta corp\użytkownik1 po wyświetleniu monitu o podanie poświadczeń konta domeny dla **Add-Computer** polecenia.

Po ponownym uruchomieniu, użyj portalu Azure nawiązać LOB1 CORP\User1 konto i hasło.

Następnie skonfiguruj LOB1 dla usług IIS i przetestować dostęp z komputera KLIENT1.

1. W Menedżerze serwera kliknij **Dodaj role i funkcje**.
2. Na **przed rozpoczęciem** kliknij przycisk **dalej**.
3. Na **Wybieranie typu instalacji** kliknij przycisk **dalej**.
4. Na **serwera docelowego wybierz** kliknij przycisk **dalej**.
5. Na **ról serwera** kliknij przycisk **serwer sieci Web (IIS)** na liście **ról**.
6. Po wyświetleniu monitu kliknij przycisk **Dodaj funkcje**, a następnie kliknij przycisk **dalej**.
7. Na **wybierz funkcje** kliknij przycisk **dalej**.
8. Na **serwer sieci Web (IIS)** kliknij przycisk **dalej**.
9. Na **Wybieranie usług ról** , wybierz lub wyczyść pola wyboru dla usług potrzebne do testowania aplikacji biznesowych, a następnie kliknij przycisk **dalej**.
10. Na **Potwierdź wybrane opcje instalacji** kliknij przycisk **zainstalować**.
11. Zaczekać na ukończenie instalacji składników, a następnie kliknij przycisk **Zamknij**.
12. W portalu Azure Połącz do komputera CLIENT1 przy użyciu poświadczeń konta corp\użytkownik1, a następnie uruchom program Internet Explorer.
13. Na pasku adresu wpisz **http://lob1/** , a następnie naciśnij klawisz ENTER. Powinny pojawić domyślnej strony sieci web IIS 8.

Jest to z bieżącą konfiguracją użytkownika.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

To środowisko jest teraz gotowe do wdrożenia aplikacji sieci web na LOB1 i przetestować funkcje z komputera CLIENT1 w podsieci Corpnet.

## <a name="next-step"></a>Następny krok
* Dodawanie nowej maszyny wirtualnej przy użyciu [portalu Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

