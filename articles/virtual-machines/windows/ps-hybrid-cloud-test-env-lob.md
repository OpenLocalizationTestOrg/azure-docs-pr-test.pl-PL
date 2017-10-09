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
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="24caa-103">Konfigurowanie aplikacji biznesowej opartej na sieci Web w chmurze hybrydowej na potrzeby testowania</span><span class="sxs-lookup"><span data-stu-id="24caa-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="24caa-104">Ten temat zawiera kroki tworzenia środowiska Chmury symulowane hybrydowego testowania linii opartych na sieci web aplikacji biznesowej (LOB), hostowana na platformie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="24caa-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="24caa-105">Oto hello Wynikowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="24caa-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="24caa-106">Ta konfiguracja obejmuje:</span><span class="sxs-lookup"><span data-stu-id="24caa-106">This configuration consists of:</span></span>

* <span data-ttu-id="24caa-107">Sieć lokalną symulowane hostowana na platformie Azure (hello sieci wirtualnej laboratorium testowe).</span><span class="sxs-lookup"><span data-stu-id="24caa-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="24caa-108">Między różnymi lokalizacjami sieć wirtualna hostowana na platformie Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="24caa-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="24caa-109">Połączenia sieci VPN do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="24caa-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="24caa-110">Serwer sieci web LOB, programu SQL server i dodatkowy kontroler domeny w sieci wirtualnej TestVNET hello.</span><span class="sxs-lookup"><span data-stu-id="24caa-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="24caa-111">Ta konfiguracja zapewnia podstawy i wspólny punkt początkowy z którego można:</span><span class="sxs-lookup"><span data-stu-id="24caa-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="24caa-112">Opracowanie i przetestowanie aplikacji biznesowych hostowanych na Internet Information Services (IIS) z programu SQL Server 2014 wewnętrznej bazie danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="24caa-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="24caa-113">Testowanie to symulowane hybrydowego oparte na chmurze IT obciążenie.</span><span class="sxs-lookup"><span data-stu-id="24caa-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="24caa-114">Istnieją trzy główne fazy toosetting zapasową środowiska testowego hybrydowe chmury:</span><span class="sxs-lookup"><span data-stu-id="24caa-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="24caa-115">Konfigurowanie środowiska chmury hello symulowane hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="24caa-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="24caa-116">Skonfiguruj komputer serwera SQL hello (SQL1).</span><span class="sxs-lookup"><span data-stu-id="24caa-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="24caa-117">Skonfiguruj serwer LOB hello (LOB1).</span><span class="sxs-lookup"><span data-stu-id="24caa-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="24caa-118">To obciążenie wymaga subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="24caa-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="24caa-119">Jeśli masz subskrypcję MSDN lub Visual Studio, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="24caa-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="24caa-120">Na przykład produkcyjnym aplikacji LOB hostowanej na platformie Azure, zobacz hello **aplikacje biznesowe** plan architektury w [diagramów architektury oprogramowania firmy Microsoft i plany](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="24caa-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="24caa-121">Faza 1: Konfigurowanie środowiska chmury hello symulowane hybrydowego</span><span class="sxs-lookup"><span data-stu-id="24caa-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="24caa-122">Utwórz hello [środowiska testowego chmura hybrydowa symulowane](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24caa-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="24caa-123">Ponieważ to środowisko testowe nie wymaga obecności hello hello APP1 serwera na powitania podsiecią Corpnet, można go zamknąć teraz.</span><span class="sxs-lookup"><span data-stu-id="24caa-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="24caa-124">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24caa-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="24caa-125">Faza 2: Skonfiguruj komputer serwera SQL hello (SQL1)</span><span class="sxs-lookup"><span data-stu-id="24caa-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="24caa-126">Z hello portalu Azure uruchom komputer DC2 hello, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="24caa-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="24caa-127">Następnie utwórz maszynę wirtualną na komputerze SQL1 przy użyciu następujących poleceń w wierszu polecenia programu Azure PowerShell na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="24caa-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="24caa-128">Toorunning poprzedniego polecenia, wypełnij hello wartości zmiennych i Usuń hello < i > znaków.</span><span class="sxs-lookup"><span data-stu-id="24caa-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

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

<span data-ttu-id="24caa-129">Użyj hello tooSQL1 tooconnect portalu Azure przy użyciu konta administratora lokalnego hello SQL1.</span><span class="sxs-lookup"><span data-stu-id="24caa-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="24caa-130">Skonfiguruj ruchu programu SQL Server i testowania podstawowej łączności tooallow reguł zapory systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="24caa-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="24caa-131">Z wiersza polecenia środowiska Windows PowerShell uprawnień administratora na komputerze SQL1 uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="24caa-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="24caa-132">polecenie ping Hello powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="24caa-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="24caa-133">Następnie dodaj hello dodatkowe dane dysku na komputerze SQL1 jako nowy wolumin z literą dysku hello F:.</span><span class="sxs-lookup"><span data-stu-id="24caa-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="24caa-134">W okienku po lewej stronie powitania w Menedżerze serwera, kliknij przycisk **usług plików i magazynowania**, a następnie kliknij przycisk **dysków**.</span><span class="sxs-lookup"><span data-stu-id="24caa-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="24caa-135">W okienku Zawartość hello w hello **dysków** kliknij przycisk **dysk 2** (z hello **partycji** ustawić także**nieznany**).</span><span class="sxs-lookup"><span data-stu-id="24caa-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="24caa-136">Kliknij przycisk **zadania**, a następnie kliknij przycisk **nowy wolumin**.</span><span class="sxs-lookup"><span data-stu-id="24caa-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="24caa-137">Na powitania przed rozpoczęciem strony hello Kreatora nowych woluminów kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="24caa-138">Na serwerze wybierz hello hello i strona dysku, kliknij przycisk **Disk 2**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="24caa-139">Po wyświetleniu monitu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="24caa-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="24caa-140">Na hello Określ rozmiar hello hello woluminu strony, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="24caa-141">Na powitania Przypisz tooa dysku litery lub folderu stronie kliknij pozycję **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="24caa-142">Na stronie Ustawienia systemu wybierz Plik powitania kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="24caa-143">Na stronie opcji Potwierdź powitania kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="24caa-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="24caa-144">Po zakończeniu kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="24caa-144">When complete, click **Close**.</span></span>

<span data-ttu-id="24caa-145">Uruchom następujące polecenia w wierszu polecenia programu Windows PowerShell hello na komputerze SQL1:</span><span class="sxs-lookup"><span data-stu-id="24caa-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="24caa-146">Następnie należy przyłączyć do domeny CORP Windows Server Active Directory toohello SQL1 przy użyciu następujących poleceń w wierszu polecenia programu Windows PowerShell hello na komputerze SQL1.</span><span class="sxs-lookup"><span data-stu-id="24caa-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="24caa-147">Użyj konta corp\użytkownik1 powitania po wyświetleniu monitu toosupply poświadczenia konta domeny dla hello **Add-Computer** polecenia.</span><span class="sxs-lookup"><span data-stu-id="24caa-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="24caa-148">Po ponownym uruchomieniu, użyj hello Azure portalu tooconnect tooSQL1 *z konta administratora lokalnego hello SQL1*.</span><span class="sxs-lookup"><span data-stu-id="24caa-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="24caa-149">Skonfiguruj program SQL Server 2014 toouse hello F: dysku dla nowych baz danych i uprawnień konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24caa-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="24caa-150">Na ekranie startowym hello wpisz **programu SQL Server Management**, a następnie kliknij przycisk **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="24caa-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="24caa-151">W **połączyć tooServer**, kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="24caa-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="24caa-152">W okienku drzewa Eksploratora obiektów hello, kliknij prawym przyciskiem myszy **SQL1**, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="24caa-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="24caa-153">W hello **właściwości serwera** okna, kliknij przycisk **ustawienia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="24caa-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="24caa-154">Zlokalizuj hello **bazy danych domyślne lokalizacje** i ustaw następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="24caa-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="24caa-155">Aby uzyskać **danych**, wpisz ścieżkę hello **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="24caa-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="24caa-156">Aby uzyskać **dziennika**, wpisz ścieżkę hello **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="24caa-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="24caa-157">Aby uzyskać **kopii zapasowej**, wpisz ścieżkę hello **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="24caa-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="24caa-158">Uwaga: Tylko nowych baz danych użyć tych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="24caa-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="24caa-159">Kliknij przycisk hello **OK** tooclose hello okna.</span><span class="sxs-lookup"><span data-stu-id="24caa-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="24caa-160">W hello **Eksplorator obiektów** okienku drzewa, otwórz **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="24caa-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="24caa-161">Kliknij prawym przyciskiem myszy **logowania** , a następnie kliknij przycisk **nowe dane logowania**.</span><span class="sxs-lookup"><span data-stu-id="24caa-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="24caa-162">W **nazwa logowania**, typ **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="24caa-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="24caa-163">Na powitania **ról serwera** kliknij przycisk **sysadmin**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="24caa-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="24caa-164">Zamknij program Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="24caa-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="24caa-165">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24caa-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="24caa-166">Faza 3: Konfigurowanie serwera LOB hello (LOB1)</span><span class="sxs-lookup"><span data-stu-id="24caa-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="24caa-167">Najpierw utwórz maszynę wirtualną LOB1 przy użyciu następujących poleceń w wierszu polecenia programu Azure PowerShell hello na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="24caa-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

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

<span data-ttu-id="24caa-168">Następnie użyj hello tooLOB1 tooconnect portalu Azure przy użyciu hello poświadczeń konta administratora lokalnego hello LOB1.</span><span class="sxs-lookup"><span data-stu-id="24caa-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="24caa-169">Skonfiguruj ruchu tooallow reguły zapory systemu Windows, do testowania podstawowej łączności.</span><span class="sxs-lookup"><span data-stu-id="24caa-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="24caa-170">Z wiersza polecenia środowiska Windows PowerShell uprawnień administratora na LOB1 uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="24caa-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="24caa-171">polecenie ping Hello powinno spowodować cztery pomyślnej odpowiedzi z adresu IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="24caa-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="24caa-172">Następnie należy przyłączyć do domeny CORP usługi Active Directory toohello LOB1 przy użyciu następujących poleceń w wierszu polecenia programu Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="24caa-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="24caa-173">Użyj konta corp\użytkownik1 powitania po wyświetleniu monitu toosupply poświadczenia konta domeny dla hello **Add-Computer** polecenia.</span><span class="sxs-lookup"><span data-stu-id="24caa-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="24caa-174">Po ponownym uruchomieniu komputera, należy użyć hello Azure tooconnect portalu tooLOB1 hello CORP\User1 konto i hasło.</span><span class="sxs-lookup"><span data-stu-id="24caa-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="24caa-175">Następnie skonfiguruj LOB1 dla usług IIS i przetestować dostęp z komputera KLIENT1.</span><span class="sxs-lookup"><span data-stu-id="24caa-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="24caa-176">W Menedżerze serwera kliknij **Dodaj role i funkcje**.</span><span class="sxs-lookup"><span data-stu-id="24caa-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="24caa-177">Na powitania **przed rozpoczęciem** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="24caa-178">Na powitania **Wybieranie typu instalacji** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="24caa-179">Na powitania **serwera docelowego wybierz** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="24caa-180">Na powitania **ról serwera** kliknij przycisk **serwer sieci Web (IIS)** liście hello **ról**.</span><span class="sxs-lookup"><span data-stu-id="24caa-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="24caa-181">Po wyświetleniu monitu kliknij przycisk **Dodaj funkcje**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="24caa-182">Na powitania **wybierz funkcje** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="24caa-183">Na powitania **serwer sieci Web (IIS)** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="24caa-184">Na powitania **Wybieranie usług ról** , wybierz lub wyczyść pola wyboru hello hello usługi niezbędne do testowania aplikacji biznesowych, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="24caa-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="24caa-185">Na powitania **Potwierdź wybrane opcje instalacji** kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="24caa-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="24caa-186">Zaczekać na ukończenie instalacji hello składników, a następnie kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="24caa-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="24caa-187">Z hello portalu Azure Podłącz komputer CLIENT1 toohello o poświadczenia konta corp\użytkownik1 hello, a następnie uruchom program Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="24caa-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="24caa-188">Na pasku adresu hello, wpisz **http://lob1/** , a następnie naciśnij klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="24caa-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="24caa-189">Powinna zostać wyświetlona hello domyślnej strony sieci web IIS 8.</span><span class="sxs-lookup"><span data-stu-id="24caa-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="24caa-190">Jest to z bieżącą konfiguracją użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24caa-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="24caa-191">To środowisko jest teraz gotowe do toodeploy możesz opartych na sieci web aplikacji na LOB1 i badania funkcji KLIENT1 na powitania podsiecią Corpnet.</span><span class="sxs-lookup"><span data-stu-id="24caa-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="24caa-192">Następny krok</span><span class="sxs-lookup"><span data-stu-id="24caa-192">Next step</span></span>
* <span data-ttu-id="24caa-193">Dodaj maszynę wirtualną przy użyciu hello [portalu Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24caa-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

