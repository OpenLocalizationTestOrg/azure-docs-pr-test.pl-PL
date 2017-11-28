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
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="beda9-103">Konfigurowanie aplikacji biznesowej opartej na sieci Web w chmurze hybrydowej na potrzeby testowania</span><span class="sxs-lookup"><span data-stu-id="beda9-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="beda9-104">Ten temat zawiera kroki tworzenia środowiska Chmury symulowane hybrydowego testowania linii opartych na sieci web aplikacji biznesowej (LOB), hostowana na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="beda9-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="beda9-105">Oto wynikowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="beda9-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="beda9-106">Ta konfiguracja obejmuje:</span><span class="sxs-lookup"><span data-stu-id="beda9-106">This configuration consists of:</span></span>

* <span data-ttu-id="beda9-107">Sieć lokalną symulowane hostowana na platformie Azure (VNet laboratorium testowe).</span><span class="sxs-lookup"><span data-stu-id="beda9-107">A simulated on-premises network hosted in Azure (the TestLab VNet).</span></span>
* <span data-ttu-id="beda9-108">Między różnymi lokalizacjami sieć wirtualna hostowana na platformie Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="beda9-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="beda9-109">Połączenia sieci VPN do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="beda9-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="beda9-110">Serwer sieci web LOB, programu SQL server i dodatkowy kontroler domeny w sieci wirtualnej TestVNET.</span><span class="sxs-lookup"><span data-stu-id="beda9-110">A web-based LOB server, SQL server, and secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="beda9-111">Ta konfiguracja zapewnia podstawy i wspólny punkt początkowy z którego można:</span><span class="sxs-lookup"><span data-stu-id="beda9-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="beda9-112">Opracowanie i przetestowanie aplikacji biznesowych hostowanych na Internet Information Services (IIS) z programu SQL Server 2014 wewnętrznej bazie danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="beda9-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="beda9-113">Testowanie to symulowane hybrydowego oparte na chmurze IT obciążenie.</span><span class="sxs-lookup"><span data-stu-id="beda9-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="beda9-114">Istnieją trzy główne fazy do konfigurowania tego środowiska testowego chmury hybrydowej:</span><span class="sxs-lookup"><span data-stu-id="beda9-114">There are three major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="beda9-115">Konfigurowanie hybrydowego symulowane środowiska chmury.</span><span class="sxs-lookup"><span data-stu-id="beda9-115">Set up the simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="beda9-116">Skonfiguruj komputer serwera SQL (SQL1).</span><span class="sxs-lookup"><span data-stu-id="beda9-116">Configure the SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="beda9-117">Skonfiguruj serwer LOB (LOB1).</span><span class="sxs-lookup"><span data-stu-id="beda9-117">Configure the LOB server (LOB1).</span></span>

<span data-ttu-id="beda9-118">To obciążenie wymaga subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="beda9-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="beda9-119">Jeśli masz subskrypcję MSDN lub Visual Studio, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="beda9-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="beda9-120">Na przykład produkcyjnym aplikacji LOB hostowanej na platformie Azure, zobacz **aplikacje biznesowe** plan architektury w [diagramów architektury oprogramowania firmy Microsoft i plany](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="beda9-120">For an example of a production LOB application hosted in Azure, see the **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-the-simulated-hybrid-cloud-environment"></a><span data-ttu-id="beda9-121">Faza 1: Konfigurowanie środowiska Chmury symulowane hybrydowego</span><span class="sxs-lookup"><span data-stu-id="beda9-121">Phase 1: Set up the simulated hybrid cloud environment</span></span>
<span data-ttu-id="beda9-122">Utwórz [środowiska testowego chmura hybrydowa symulowane](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="beda9-122">Create the [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="beda9-123">Ponieważ to środowisko testowe nie wymaga obecności serwera APP1 w podsieci Corpnet, można go zamknąć teraz.</span><span class="sxs-lookup"><span data-stu-id="beda9-123">Because this test environment does not require the presence of the APP1 server on the Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="beda9-124">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="beda9-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-the-sql-server-computer-sql1"></a><span data-ttu-id="beda9-125">Faza 2: Skonfiguruj komputer serwera SQL (SQL1)</span><span class="sxs-lookup"><span data-stu-id="beda9-125">Phase 2: Configure the SQL server computer (SQL1)</span></span>
<span data-ttu-id="beda9-126">W portalu Azure uruchom komputer DC2, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="beda9-126">From the Azure portal, start the DC2 computer if needed.</span></span>

<span data-ttu-id="beda9-127">Następnie utwórz maszynę wirtualną na komputerze SQL1 przy użyciu następujących poleceń w wierszu polecenia programu Azure PowerShell na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="beda9-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="beda9-128">Przed uruchomieniem tych poleceń, wypełnij wartości zmiennych i Usuń < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="beda9-128">Prior to running these commands, fill in the variable values and remove the < and > characters.</span></span>

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

<span data-ttu-id="beda9-129">Użyj portalu Azure, aby nawiązać połączenie komputera SQL1 przy użyciu konta administratora lokalnego komputera SQL1.</span><span class="sxs-lookup"><span data-stu-id="beda9-129">Use the Azure portal to connect to SQL1 using the local administrator account of SQL1.</span></span>

<span data-ttu-id="beda9-130">Następnie można skonfigurować reguł zapory systemu Windows, aby umożliwić testowanie podstawowej łączności i ruchu programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="beda9-130">Next, configure Windows Firewall rules to allow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="beda9-131">Z wiersza polecenia środowiska Windows PowerShell uprawnień administratora na komputerze SQL1 uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="beda9-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="beda9-132">Polecenie ping powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="beda9-132">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="beda9-133">Następnie dodaj jako nowy wolumin z literą dysku F: dysku dodatkowe dane SQL1.</span><span class="sxs-lookup"><span data-stu-id="beda9-133">Next, add the extra data disk on SQL1 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="beda9-134">W lewym okienku w Menedżerze serwera kliknij **usług plików i magazynowania**, a następnie kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="beda9-134">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="beda9-135">W okienku Zawartość w **dysków** kliknij przycisk **dysk 2** (z **partycji** ustawioną **nieznany**).</span><span class="sxs-lookup"><span data-stu-id="beda9-135">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="beda9-136">Kliknij przycisk **zadania**, a następnie kliknij przycisk **nowy wolumin**.</span><span class="sxs-lookup"><span data-stu-id="beda9-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="beda9-137">Na stronie zanim rozpoczniesz Kreator nowego woluminu, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-137">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="beda9-138">Na stronie wybierz serwer i strona dysku kliknij **Disk 2**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-138">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="beda9-139">Po wyświetleniu monitu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="beda9-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="beda9-140">Na stronie Określ rozmiar strony wolumin, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-140">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="beda9-141">Przypisz do strony dysku litery lub folderu, wybierz polecenie **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-141">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="beda9-142">Na stronie Wybieranie pliku ustawień systemu kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-142">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="beda9-143">Na stronie Potwierdzanie opcji kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="beda9-143">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="beda9-144">Po zakończeniu kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="beda9-144">When complete, click **Close**.</span></span>

<span data-ttu-id="beda9-145">Uruchom następujące polecenia w wierszu polecenia programu Windows PowerShell na komputerze SQL1:</span><span class="sxs-lookup"><span data-stu-id="beda9-145">Run these commands at the Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="beda9-146">Następnie należy dołączyć komputer SQL1 do domeny CORP Windows Server Active Directory przy użyciu następujących poleceń w wierszu polecenia programu Windows PowerShell na komputerze SQL1.</span><span class="sxs-lookup"><span data-stu-id="beda9-146">Next, join SQL1 to the CORP Windows Server Active Directory domain with these commands at the Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="beda9-147">Użyj konta corp\użytkownik1 po wyświetleniu monitu o podanie poświadczeń konta domeny dla **Add-Computer** polecenia.</span><span class="sxs-lookup"><span data-stu-id="beda9-147">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="beda9-148">Po ponownym uruchomieniu, użyj portalu Azure do nawiązania połączenia SQL1 *z konta administratora lokalnego komputera SQL1*.</span><span class="sxs-lookup"><span data-stu-id="beda9-148">After restarting, use the Azure portal to connect to SQL1 *with the local administrator account of SQL1*.</span></span>

<span data-ttu-id="beda9-149">Skonfiguruj program SQL Server 2014 do użytku F: dysku dla nowych baz danych oraz uprawnień konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="beda9-149">Next, configure SQL Server 2014 to use the F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="beda9-150">Na ekranie startowym wpisz **programu SQL Server Management**, a następnie kliknij przycisk **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="beda9-150">From the Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="beda9-151">W **Połącz z serwerem**, kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="beda9-151">In **Connect to Server**, click **Connect**.</span></span>
3. <span data-ttu-id="beda9-152">W okienku drzewa Eksploratora obiektów kliknij prawym przyciskiem myszy **SQL1**, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="beda9-152">In the Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="beda9-153">W **właściwości serwera** okna, kliknij przycisk **ustawienia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="beda9-153">In the **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="beda9-154">Zlokalizuj **bazy danych domyślne lokalizacje** i ustaw następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="beda9-154">Locate the **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="beda9-155">Aby uzyskać **danych**, wpisz ścieżkę **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="beda9-155">For **Data**, type the path **f:\Data**.</span></span>
   * <span data-ttu-id="beda9-156">Aby uzyskać **dziennika**, wpisz ścieżkę **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="beda9-156">For **Log**, type the path **f:\Log**.</span></span>
   * <span data-ttu-id="beda9-157">Aby uzyskać **kopii zapasowej**, wpisz ścieżkę **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="beda9-157">For **Backup**, type the path **f:\Backup**.</span></span>
   * <span data-ttu-id="beda9-158">Uwaga: Tylko nowych baz danych użyć tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="beda9-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="beda9-159">Kliknij przycisk **OK** aby zamknąć okno.</span><span class="sxs-lookup"><span data-stu-id="beda9-159">Click the **OK** to close the window.</span></span>
7. <span data-ttu-id="beda9-160">W **Eksplorator obiektów** okienku drzewa, otwórz **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="beda9-160">In the **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="beda9-161">Kliknij prawym przyciskiem myszy **logowania** , a następnie kliknij przycisk **nowe dane logowania**.</span><span class="sxs-lookup"><span data-stu-id="beda9-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="beda9-162">W **nazwa logowania**, typ **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="beda9-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="beda9-163">Na **ról serwera** kliknij przycisk **sysadmin**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="beda9-163">On the **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="beda9-164">Zamknij program Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="beda9-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="beda9-165">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="beda9-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-the-lob-server-lob1"></a><span data-ttu-id="beda9-166">Faza 3: Konfigurowanie serwera LOB (LOB1)</span><span class="sxs-lookup"><span data-stu-id="beda9-166">Phase 3: Configure the LOB server (LOB1)</span></span>
<span data-ttu-id="beda9-167">Najpierw utwórz maszynę wirtualną LOB1 przy użyciu następujących poleceń w wierszu polecenia programu Azure PowerShell na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="beda9-167">First, create a virtual machine for LOB1 with these commands at the Azure PowerShell command prompt on your local computer.</span></span>

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

<span data-ttu-id="beda9-168">Następnie użyj portalu Azure, aby nawiązać połączenie przy użyciu poświadczeń konta administratora lokalnego LOB1 LOB1.</span><span class="sxs-lookup"><span data-stu-id="beda9-168">Next, use the Azure portal to connect to LOB1 with the credentials of the local administrator account of LOB1.</span></span>

<span data-ttu-id="beda9-169">Skonfiguruj regułę zapory systemu Windows, aby zezwolić na ruch do testowania podstawowej łączności.</span><span class="sxs-lookup"><span data-stu-id="beda9-169">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="beda9-170">Z wiersza polecenia środowiska Windows PowerShell uprawnień administratora na LOB1 uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="beda9-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="beda9-171">Polecenie ping powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="beda9-171">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="beda9-172">Następnie dołącz LOB1 do domeny usługi Active Directory CORP, przy użyciu następujących poleceń w wierszu polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="beda9-172">Next, join LOB1 to the CORP Active Directory domain with these commands at the Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="beda9-173">Użyj konta corp\użytkownik1 po wyświetleniu monitu o podanie poświadczeń konta domeny dla **Add-Computer** polecenia.</span><span class="sxs-lookup"><span data-stu-id="beda9-173">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="beda9-174">Po ponownym uruchomieniu, użyj portalu Azure nawiązać LOB1 CORP\User1 konto i hasło.</span><span class="sxs-lookup"><span data-stu-id="beda9-174">After restarting, use the Azure portal to connect to LOB1 with the CORP\User1 account and password.</span></span>

<span data-ttu-id="beda9-175">Następnie skonfiguruj LOB1 dla usług IIS i przetestować dostęp z komputera KLIENT1.</span><span class="sxs-lookup"><span data-stu-id="beda9-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="beda9-176">W Menedżerze serwera kliknij **Dodaj role i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="beda9-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="beda9-177">Na **przed rozpoczęciem** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-177">On the **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="beda9-178">Na **Wybieranie typu instalacji** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-178">On the **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="beda9-179">Na **serwera docelowego wybierz** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-179">On the **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="beda9-180">Na **ról serwera** kliknij przycisk **serwer sieci Web (IIS)** na liście **ról**.</span><span class="sxs-lookup"><span data-stu-id="beda9-180">On the **Server roles** page, click **Web Server (IIS)** in the list of **Roles**.</span></span>
6. <span data-ttu-id="beda9-181">Po wyświetleniu monitu kliknij przycisk **Dodaj funkcje**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="beda9-182">Na **wybierz funkcje** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-182">On the **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="beda9-183">Na **serwer sieci Web (IIS)** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-183">On the **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="beda9-184">Na **Wybieranie usług ról** , wybierz lub wyczyść pola wyboru dla usług potrzebne do testowania aplikacji biznesowych, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="beda9-184">On the **Select role services** page, select or clear the check boxes for the services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="beda9-185">Na **Potwierdź wybrane opcje instalacji** kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="beda9-185">On the **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="beda9-186">Zaczekać na ukończenie instalacji składników, a następnie kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="beda9-186">Wait until the installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="beda9-187">W portalu Azure Połącz do komputera CLIENT1 przy użyciu poświadczeń konta corp\użytkownik1, a następnie uruchom program Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="beda9-187">From the Azure portal, connect to the CLIENT1 computer with the CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="beda9-188">Na pasku adresu wpisz **http://lob1/** , a następnie naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="beda9-188">In the Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="beda9-189">Powinny pojawić domyślnej strony sieci web IIS 8.</span><span class="sxs-lookup"><span data-stu-id="beda9-189">You should see the default IIS 8 web page.</span></span>

<span data-ttu-id="beda9-190">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="beda9-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="beda9-191">To środowisko jest teraz gotowe do wdrożenia aplikacji sieci web na LOB1 i przetestować funkcje z komputera CLIENT1 w podsieci Corpnet.</span><span class="sxs-lookup"><span data-stu-id="beda9-191">This environment is now ready for you to deploy your web-based application on LOB1 and test functionality from CLIENT1 on the Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="beda9-192">Następny krok</span><span class="sxs-lookup"><span data-stu-id="beda9-192">Next step</span></span>
* <span data-ttu-id="beda9-193">Dodawanie nowej maszyny wirtualnej przy użyciu [portalu Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="beda9-193">Add a new virtual machine using the [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

