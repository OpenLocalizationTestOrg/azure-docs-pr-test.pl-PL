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
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="af9c1-104">Skonfiguruj hello zawsze włączone grupy dostępności na maszynie Wirtualnej platformy Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="af9c1-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af9c1-105">Klasycznym: interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="af9c1-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="af9c1-106">[Klasycznym: środowiska PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="af9c1-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="af9c1-107">Przed rozpoczęciem należy wziąć pod uwagę może teraz ukończyć tego zadania w modelu Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="af9c1-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="af9c1-108">Firma Microsoft zaleca model Menedżera zasobów Azure dla nowych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="af9c1-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="af9c1-109">Zobacz [programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af9c1-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af9c1-110">Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="af9c1-111">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="af9c1-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="af9c1-112">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="af9c1-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="af9c1-113">Azure maszynach wirtualnych (VM) ułatwia kosztu hello toolower administratorów bazy danych systemu wysokiej dostępności programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="af9c1-114">Ten samouczek pokazuje, jak tooimplement dostępności grupy za pomocą programu SQL Server AlwaysOn end-to-end wewnątrz środowiska platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af9c1-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="af9c1-115">Końcem hello samouczka hello rozwiązania programu SQL Server zawsze na platformie Azure będzie składać się z hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="af9c1-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="af9c1-116">Sieć wirtualna zawiera wiele podsieci, w tym frontonu i zaplecza podsieci.</span><span class="sxs-lookup"><span data-stu-id="af9c1-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="af9c1-117">Kontroler domeny z domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="af9c1-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="af9c1-118">Dwa SQL Server maszyny wirtualne, które są wdrożone toohello zaplecza podsieci i toohello przyłączone do domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="af9c1-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="af9c1-119">Trzy węzeł klastra pracy awaryjnej systemu Windows z modelu kworum Większość węzłów hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="af9c1-120">Grupa dostępności o dwóch replik z zatwierdzaniem synchronicznym bazy danych dostępności.</span><span class="sxs-lookup"><span data-stu-id="af9c1-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="af9c1-121">Ten scenariusz jest dobrym rozwiązaniem dla uproszczenia jej na platformie Azure, a nie dla jego efektywność kosztowa lub innych czynników.</span><span class="sxs-lookup"><span data-stu-id="af9c1-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="af9c1-122">Na przykład można zminimalizować hello liczbę maszyn wirtualnych dla toosave grupy dostępności dwóch replik na godziny obliczeń na platformie Azure przy użyciu kontrolera domeny hello jako monitor udziału plików hello kworum w klastrze trybu failover z dwoma węzłami.</span><span class="sxs-lookup"><span data-stu-id="af9c1-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="af9c1-123">Ta metoda zmniejsza liczbę maszyn wirtualnych hello przez jeden z hello powyżej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="af9c1-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="af9c1-124">Ten samouczek ma się, że tooshow hello kroki, które są wymagane tooset się hello opisano rozwiązania powyżej, bez opracowanie na powitania szczegóły każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="af9c1-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="af9c1-125">W związku z tym zamiast zapewniające kroków konfiguracji hello graficznego interfejsu użytkownika, używa tootake skryptów środowiska PowerShell możesz szybko za pomocą każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="af9c1-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="af9c1-126">Ten samouczek zakłada hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="af9c1-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="af9c1-127">Masz już konto platformy Azure z subskrypcją maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="af9c1-128">Po zainstalowaniu hello [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="af9c1-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="af9c1-129">Masz już pełny opis zawsze włączonych grup dostępności dla rozwiązań lokalnych.</span><span class="sxs-lookup"><span data-stu-id="af9c1-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="af9c1-130">Aby uzyskać więcej informacji, zobacz [zawsze włączonych grup dostępności (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="af9c1-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="af9c1-131">Łączenie tooyour subskrypcji platformy Azure i tworzenie sieci wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="af9c1-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="af9c1-132">W oknie programu PowerShell na komputerze lokalnym zaimportować hello modułu platformy Azure, pobieranie hello maszyny tooyour pliku ustawień publikowania i połączyć tooyour sesji programu PowerShell subskrypcji platformy Azure przez zaimportowanie hello pobrać ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="af9c1-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="af9c1-133">Witaj **Get AzurePublishSettingsFile** polecenie automatycznie generuje certyfikat zarządzania platformy Azure i pobiera go tooyour maszyny.</span><span class="sxs-lookup"><span data-stu-id="af9c1-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="af9c1-134">Przeglądarką jest automatycznie otwierane i masz poświadczeń konta Microsoft hello zostanie wyświetlony monit o tooenter dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af9c1-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="af9c1-135">Witaj pobrane **.publishsettings** plik zawiera wszystkie informacje hello muszą toomanage subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af9c1-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="af9c1-136">Po zapisaniu tego pliku tooa lokalnego katalogu, zaimportuj go za pomocą hello **AzurePublishSettingsFile importu** polecenia.</span><span class="sxs-lookup"><span data-stu-id="af9c1-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="af9c1-137">plik .publishsettings Hello zawiera swoje poświadczenia (Niezakodowane), które są używane tooadminister subskrypcji platformy Azure i usługi.</span><span class="sxs-lookup"><span data-stu-id="af9c1-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="af9c1-138">Hello ze względów bezpieczeństwa dla tego pliku jest toostore go tymczasowo poza katalogów źródła (na przykład w folderze Libraries\Documents hello), a następnie usuń, po zakończeniu importowania hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="af9c1-139">Złośliwy użytkownik uzyska dostęp toohello .publishsettings plik można edytować, tworzenia i usuwania usług Azure.</span><span class="sxs-lookup"><span data-stu-id="af9c1-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="af9c1-140">Zdefiniuj szereg zmiennych czy użyjesz toocreate chmury infrastruktury IT.</span><span class="sxs-lookup"><span data-stu-id="af9c1-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

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

    <span data-ttu-id="af9c1-141">Należy zwrócić uwagę toohello po tooensure, który poleceniach powiedzie się później:</span><span class="sxs-lookup"><span data-stu-id="af9c1-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="af9c1-142">Zmienne **$storageAccountName** i **$dcServiceName** musi być unikatowa, ponieważ są one używane tooidentify Twojego konta magazynu w chmurze i serwera chmurowego, odpowiednio na powitania Internet.</span><span class="sxs-lookup"><span data-stu-id="af9c1-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="af9c1-143">Witaj nazw określonych dla zmiennych **$affinityGroupName** i **$virtualNetworkName** są skonfigurowane w dokumencie hello konfiguracji sieci wirtualnej, który będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="af9c1-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="af9c1-144">**$sqlImageName** Określa nazwę hello zaktualizowane hello obrazu maszyny Wirtualnej, która zawiera SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="af9c1-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="af9c1-145">Dla uproszczenia **Contoso! 000** jest hello samo hasło, które jest używane w całej samouczek hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="af9c1-146">Utwórz grupę koligacji.</span><span class="sxs-lookup"><span data-stu-id="af9c1-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="af9c1-147">Tworzenie sieci wirtualnej przez zaimportowanie pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="af9c1-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="af9c1-148">plik konfiguracji Hello zawiera powitania po dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="af9c1-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="af9c1-149">Krótko mówiąc, określa sieć wirtualną o nazwie **ContosoNET** w grupie koligacji hello o nazwie **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="af9c1-150">Ma przestrzeń adresowa hello **10.10.0.0/16** i ma dwie podsieci **10.10.1.0/24** i **10.10.2.0/24**, które są podsieci frontonu hello wstecz podsieci odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="af9c1-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="af9c1-151">podsieci frontonu Hello jest umieszczane aplikacji klienckich, takich jak Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="af9c1-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="af9c1-152">Hello wstecz podsieci będą umieszczane są hello maszynach wirtualnych serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="af9c1-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="af9c1-153">Jeśli zmienisz hello **$affinityGroupName** i **$virtualNetworkName** zmienne wcześniej, należy również zmienić hello odpowiadającego poniższe nazwy.</span><span class="sxs-lookup"><span data-stu-id="af9c1-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

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

5. <span data-ttu-id="af9c1-154">Utwórz konto magazynu, który został skojarzony z grupą koligacji hello utworzone i jest ustawiony jako hello bieżącego konta magazynu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="af9c1-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="af9c1-155">Utwórz serwer kontrolera domeny hello w hello nowe chmury usługi i zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="af9c1-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

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

    <span data-ttu-id="af9c1-156">Te polecenia gazociągami hello następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="af9c1-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="af9c1-157">**Nowy AzureVMConfig** tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af9c1-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="af9c1-158">**Dodaj AzureProvisioningConfig** zapewnia hello parametry konfiguracji autonomicznej systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="af9c1-159">**Dodaj AzureDataDisk** dodaje hello dysk danych, które będzie używane do przechowywania danych usługi Active Directory z hello buforowanie tooNone zestawu opcji.</span><span class="sxs-lookup"><span data-stu-id="af9c1-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="af9c1-160">**Nowy AzureVM** tworzy nową usługę w chmurze oraz hello nowej maszyny Wirtualnej platformy Azure w hello nową usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="af9c1-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="af9c1-161">Poczekaj, aż hello nowej maszyny Wirtualnej toobe w pełni zaaprowizowanym i Pobierz katalog roboczy tooyour hello w pliku pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="af9c1-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="af9c1-162">Ponieważ hello nowej maszyny Wirtualnej Azure ma tooprovision dużo czasu, hello `while` Pętla kontynuuje toopoll hello nowej maszyny Wirtualnej, dopóki nie jest gotowa do użycia.</span><span class="sxs-lookup"><span data-stu-id="af9c1-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

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

<span data-ttu-id="af9c1-163">Serwer kontrolera domeny Hello pomyślnie jest teraz udostępniony.</span><span class="sxs-lookup"><span data-stu-id="af9c1-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="af9c1-164">Następnie należy skonfigurować domeny usługi Active Directory hello na tym serwerze kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="af9c1-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="af9c1-165">Pozostaw otwarte okno programu PowerShell hello na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="af9c1-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="af9c1-166">Służy on ponownie nowsze toocreate hello dwóch maszyn wirtualnych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="af9c1-167">Konfiguracja kontrolera domeny hello</span><span class="sxs-lookup"><span data-stu-id="af9c1-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="af9c1-168">Połącz serwer kontrolera domeny toohello uruchamiając hello pliku pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="af9c1-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="af9c1-169">Użyj administrator maszyny hello AzureAdmin nazwy użytkownika i hasła **Contoso! 000**, która została określona podczas tworzenia hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af9c1-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="af9c1-170">Otwórz okno programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="af9c1-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="af9c1-171">Uruchom następujące hello **DCPROMO. EXE** tooset polecenia zapasowej hello **corp.contoso.com** domeny z katalogów hello danych znajdujących się na dysku M.</span><span class="sxs-lookup"><span data-stu-id="af9c1-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

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

    <span data-ttu-id="af9c1-172">Po zakończeniu działania polecenia hello hello maszyny Wirtualnej powoduje automatyczne ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="af9c1-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="af9c1-173">Połącz serwer kontrolera domeny toohello ponownie uruchamiając hello pliku pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="af9c1-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="af9c1-174">Teraz, zaloguj się jako **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="af9c1-175">Otwórz okno programu PowerShell w trybie administratora i zaimportować moduł środowiska PowerShell usługi Active Directory hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="af9c1-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="af9c1-176">Uruchom następujące polecenia tooadd trzech użytkowników toohello domeny hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-176">Run hello following commands tooadd three users toohello domain.</span></span>

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

    <span data-ttu-id="af9c1-177">**CORP\Install** wszystko, co jest używane tooconfigure związane z wystąpień usługi programu SQL Server toohello hello klastra pracy awaryjnej i hello grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="af9c1-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="af9c1-178">**CORP\SQLSvc1** i **CORP\SQLSvc2** są używane jako konto usługi programu SQL Server hello hello dwóch maszyn wirtualnych z serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="af9c1-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="af9c1-179">Witaj dalej, uruchom następujące polecenia toogive **CORP\Install** hello uprawnienia toocreate obiektów typu komputer w domenie hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="af9c1-180">Witaj GUID wymienione powyżej jest hello identyfikatora GUID dla typu obiektu komputera hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="af9c1-181">Witaj **CORP\Install** konto musi hello **Odczyt wszystkich właściwości** i **tworzenia obiektów komputerów** Active bezpośredniego hello toocreate uprawnień obiektów na powitania trybu failover klaster.</span><span class="sxs-lookup"><span data-stu-id="af9c1-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="af9c1-182">Witaj **Odczyt wszystkich właściwości** już pozwolono tooCORP\Install domyślnie, więc nie trzeba toogrant go jawnie.</span><span class="sxs-lookup"><span data-stu-id="af9c1-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="af9c1-183">Aby uzyskać więcej informacji dotyczących uprawnień, które są potrzebne klastra pracy awaryjnej hello toocreate, zobacz [przewodnik krok po kroku klastra pracy awaryjnej: Konfigurowanie kont w usłudze Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="af9c1-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="af9c1-184">Teraz, po zakończeniu konfigurowania usługi Active Directory i obiektów użytkowników hello, będzie utworzyć dwóch maszyn wirtualnych programu SQL Server i dołącz je toothis domeny.</span><span class="sxs-lookup"><span data-stu-id="af9c1-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="af9c1-185">Tworzenie maszyn wirtualnych hello programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="af9c1-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="af9c1-186">Nadal okno programu PowerShell hello toouse, który jest otwarty na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="af9c1-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="af9c1-187">Zdefiniuj hello następujące dodatkowe zmienne:</span><span class="sxs-lookup"><span data-stu-id="af9c1-187">Define hello following additional variables:</span></span>

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

    <span data-ttu-id="af9c1-188">Witaj adres IP **10.10.0.4** zwykle przypisano toohello pierwsza maszyna wirtualna, które są tworzone w hello **10.10.0.0/16** podsieci sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af9c1-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="af9c1-189">Należy sprawdzić, czy jest hello adres serwera kontrolera domeny, uruchamiając **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="af9c1-190">O nazwie maszyny Wirtualnej w klastrze pracy awaryjnej hello hello uruchom następujące polecenia gazociągami toocreate hello najpierw **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="af9c1-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

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

    <span data-ttu-id="af9c1-191">Należy uwzględnić następujące hello dotyczące hello polecenie powyżej:</span><span class="sxs-lookup"><span data-stu-id="af9c1-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="af9c1-192">**Nowy AzureVMConfig** tworzy konfiguracji maszyny Wirtualnej o nazwie zestaw żądaną dostępności hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="af9c1-193">Witaj kolejnych maszyn wirtualnych zostanie utworzony z hello sama nazwa zbioru dostępności, dzięki czemu są one przyłączone toohello tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="af9c1-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="af9c1-194">**Dodaj AzureProvisioningConfig** sprzężenia hello domeny usługi Active Directory toohello maszyny Wirtualnej został utworzony.</span><span class="sxs-lookup"><span data-stu-id="af9c1-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="af9c1-195">**Zestaw AzureSubnet** miejsca hello maszyn wirtualnych w podsieci wstecz hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="af9c1-196">**Nowy AzureVM** tworzy nową usługę w chmurze oraz hello nowej maszyny Wirtualnej platformy Azure w hello nową usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="af9c1-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="af9c1-197">Witaj **DnsSettings** parametr określa tego serwera DNS hello hello serwerów w hello nową usługę w chmurze ma adres IP hello **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="af9c1-198">Jest to adres IP serwera kontrolera domeny hello hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="af9c1-199">Ten parametr jest potrzebny tooenable hello nowych maszyn wirtualnych w domenie usługi Active Directory toohello toojoin hello chmury usługi pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="af9c1-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="af9c1-200">Bez tego parametru należy ręcznie ustawić hello ustawieniami adresu IPv4 na serwerze kontrolera domeny hello toouse maszyny Wirtualnej jako podstawowy serwer DNS powitania po hello maszyny Wirtualnej jest udostępniane, a następnie dołącz do domeny usługi Active Directory toohello wirtualna hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="af9c1-201">Uruchom powitania po gazociągami polecenia hello toocreate maszynach wirtualnych serwera SQL o nazwie **ContosoSQL1** i **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

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

    <span data-ttu-id="af9c1-202">Należy uwzględnić następujące hello dotyczące powyższych poleceń hello:</span><span class="sxs-lookup"><span data-stu-id="af9c1-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="af9c1-203">**Nowy AzureVMConfig** używa hello tego samego nazwa zbioru dostępności jako serwer kontrolera domeny hello i SQL Server 2012 Service Pack 1 Enterprise Edition obraz w galerii maszyn wirtualnych hello hello używa.</span><span class="sxs-lookup"><span data-stu-id="af9c1-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="af9c1-204">Ustawia również hello działania systemu dysku tooread buforowania tylko (nie buforowania zapisu).</span><span class="sxs-lookup"><span data-stu-id="af9c1-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="af9c1-205">Zaleca się przeprowadzenie migracji hello dysku bazy danych plików tooa odrębne dołączyć toohello maszyny Wirtualnej i skonfigurować go odczytu lub buforowanie zapisu.</span><span class="sxs-lookup"><span data-stu-id="af9c1-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="af9c1-206">Następnym krokiem hello jest jednak Read tooremove buforowanie zapisu na dysku systemu operacyjnego hello, ponieważ nie można usunąć buforowanie na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="af9c1-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="af9c1-207">**Dodaj AzureProvisioningConfig** sprzężenia hello domeny usługi Active Directory toohello maszyny Wirtualnej został utworzony.</span><span class="sxs-lookup"><span data-stu-id="af9c1-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="af9c1-208">**Zestaw AzureSubnet** miejsca hello maszyn wirtualnych w podsieci wstecz hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="af9c1-209">**Dodaj AzureEndpoint** dodaje punkty końcowe dostępu, dzięki czemu aplikacje klienckie mogą uzyskiwać dostęp do tych wystąpień usługi programu SQL Server na powitania Internet.</span><span class="sxs-lookup"><span data-stu-id="af9c1-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="af9c1-210">Inne porty są podane tooContosoSQL1 i ContosoSQL2.</span><span class="sxs-lookup"><span data-stu-id="af9c1-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="af9c1-211">**Nowy AzureVM** tworzy hello nową maszynę Wirtualną programu SQL Server w hello sama usługa w chmurze jako ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="af9c1-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="af9c1-212">Maszyny wirtualne hello należy umieścić w hello sama usługa w chmurze należy je toobe w hello na tym samym zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="af9c1-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="af9c1-213">Poczekaj dla każdego toobe maszyny Wirtualnej, w pełni zaaprowizowanym i dla każdej maszyny Wirtualnej toodownload katalog roboczy tooyour jego pliku pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="af9c1-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="af9c1-214">Witaj `for` pętli przełączanie po kolei hello trzech nowych maszyn wirtualnych i wykonuje polecenia hello wewnątrz nawiasów klamrowych hello najwyższego poziomu dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="af9c1-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

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

    <span data-ttu-id="af9c1-215">teraz udostępnieniu Hello maszynach wirtualnych serwera SQL i uruchomiona, ale są zainstalowane z programem SQL Server z opcji domyślnych.</span><span class="sxs-lookup"><span data-stu-id="af9c1-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="af9c1-216">Inicjowanie hello klastra trybu failover maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="af9c1-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="af9c1-217">W tej sekcji należy toomodify hello trzy serwery będą używane w hello klastra pracy awaryjnej i hello instalacji programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="af9c1-218">W szczególności:</span><span class="sxs-lookup"><span data-stu-id="af9c1-218">Specifically:</span></span>

* <span data-ttu-id="af9c1-219">Wszystkie serwery: należy tooinstall hello **klaster pracy awaryjnej** funkcji.</span><span class="sxs-lookup"><span data-stu-id="af9c1-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="af9c1-220">Wszystkie serwery: należy tooadd **CORP\Install** jako maszyna hello **administratora**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="af9c1-221">ContosoSQL1 i ContosoSQL2 tylko: należy tooadd **CORP\Install** jako **sysadmin** roli w hello domyślnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="af9c1-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="af9c1-222">ContosoSQL1 i ContosoSQL2 tylko: należy tooadd **NT AUTHORITY\System** jako logowanie z hello następujących uprawnień:</span><span class="sxs-lookup"><span data-stu-id="af9c1-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="af9c1-223">Instrukcja ALTER żadnej grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="af9c1-223">Alter any availability group</span></span>
  * <span data-ttu-id="af9c1-224">Połączenia SQL</span><span class="sxs-lookup"><span data-stu-id="af9c1-224">Connect SQL</span></span>
  * <span data-ttu-id="af9c1-225">Widok stanu serwera</span><span class="sxs-lookup"><span data-stu-id="af9c1-225">View server state</span></span>
* <span data-ttu-id="af9c1-226">ContosoSQL1 i ContosoSQL2 tylko: hello **TCP** na powitania maszyny Wirtualnej programu SQL Server jest już włączony protokół.</span><span class="sxs-lookup"><span data-stu-id="af9c1-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="af9c1-227">Jednak nadal potrzebujesz tooopen hello zapory dla dostępu zdalnego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="af9c1-228">Teraz możesz toostart gotowe.</span><span class="sxs-lookup"><span data-stu-id="af9c1-228">Now, you're ready toostart.</span></span> <span data-ttu-id="af9c1-229">Począwszy od **ContosoQuorum**, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="af9c1-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="af9c1-230">Połącz za**ContosoQuorum** uruchamiając hello pliki pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="af9c1-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="af9c1-231">Użyj nazwy użytkownika administrator maszyny hello **AzureAdmin** i hasło **Contoso! 000**, określony podczas tworzenia maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="af9c1-232">Sprawdź, czy hello komputery zostały pomyślnie dołączono zbyt**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="af9c1-233">Poczekaj, aż toofinish instalacji programu SQL Server hello uruchomionych zadań inicjowania automatycznego hello przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="af9c1-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="af9c1-234">Otwórz okno programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="af9c1-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="af9c1-235">Zainstaluj funkcję Klaster pracy awaryjnej systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="af9c1-236">Dodaj **CORP\Install** jako administrator lokalny.</span><span class="sxs-lookup"><span data-stu-id="af9c1-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="af9c1-237">Wyloguj ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="af9c1-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="af9c1-238">Gotowe z tym serwerem teraz.</span><span class="sxs-lookup"><span data-stu-id="af9c1-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="af9c1-239">Następnie należy zainicjować **ContosoSQL1** i **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="af9c1-240">Wykonaj hello poniższe czynności, które są identyczne dla obu maszynach wirtualnych serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="af9c1-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="af9c1-241">Połącz toohello dwóch maszyn wirtualnych z serwera SQL, uruchamiając hello pliki pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="af9c1-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="af9c1-242">Użyj nazwy użytkownika administrator maszyny hello **AzureAdmin** i hasło **Contoso! 000**, określony podczas tworzenia maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="af9c1-243">Sprawdź, czy hello komputery zostały pomyślnie dołączono zbyt**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="af9c1-244">Poczekaj, aż toofinish instalacji programu SQL Server hello uruchomionych zadań inicjowania automatycznego hello przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="af9c1-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="af9c1-245">Otwórz okno programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="af9c1-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="af9c1-246">Zainstaluj funkcję Klaster pracy awaryjnej systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="af9c1-247">Dodaj **CORP\Install** jako administrator lokalny.</span><span class="sxs-lookup"><span data-stu-id="af9c1-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="af9c1-248">Importuj hello dostawcy programu PowerShell programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="af9c1-249">Dodaj **CORP\Install** jako hello roli administratora systemu dla hello domyślnego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="af9c1-250">Dodaj **NT AUTHORITY\System** jako logowanie z uprawnieniami hello trzech opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="af9c1-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="af9c1-251">Otwórz zaporę Windows hello dla dostępu zdalnego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="af9c1-252">Wyloguj obie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="af9c1-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="af9c1-253">Na koniec wszystko jest gotowe tooconfigure hello dostępności grupy.</span><span class="sxs-lookup"><span data-stu-id="af9c1-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="af9c1-254">Użyjesz tooperform dostawcy programu PowerShell programu SQL Server hello całe hello pracować w **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="af9c1-255">Skonfiguruj grupy dostępności hello</span><span class="sxs-lookup"><span data-stu-id="af9c1-255">Configure hello availability group</span></span>
1. <span data-ttu-id="af9c1-256">Połącz za**ContosoSQL1** ponownie, uruchamiając hello pliki pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="af9c1-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="af9c1-257">Zamiast logowanie się przy użyciu konta komputera hello, zaloguj się przy użyciu **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="af9c1-258">Otwórz okno programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="af9c1-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="af9c1-259">Zdefiniuj hello następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="af9c1-259">Define hello following variables:</span></span>

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
4. <span data-ttu-id="af9c1-260">Importuj hello dostawcy programu PowerShell programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="af9c1-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="af9c1-261">Zmień hello konta usługi programu SQL Server dla ContosoSQL1 tooCORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="af9c1-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="af9c1-262">Zmień hello konta usługi programu SQL Server dla ContosoSQL2 tooCORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="af9c1-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="af9c1-263">Pobierz **CreateAzureFailoverCluster.ps1** z [Tworzenie klastra trybu Failover dla zawsze włączonych grup dostępności w maszynie Wirtualnej platformy Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello lokalny katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="af9c1-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="af9c1-264">Użyjesz tego toohelp skryptu tworzenia klastra trybu failover funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="af9c1-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="af9c1-265">Ważne informacje na jak klaster pracy awaryjnej systemu Windows współdziała z hello Azure sieciowy, zobacz [wysokiej dostępności i odzyskiwania po awarii dla programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af9c1-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="af9c1-266">Zmień katalog roboczy tooyour i utworzyć klaster trybu failover hello ze skryptem hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="af9c1-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="af9c1-267">Włącz zawsze włączone grupy dostępności dla wystąpień programu SQL Server domyślne hello **ContosoSQL1** i **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="af9c1-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

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
10. <span data-ttu-id="af9c1-268">Utwórz katalog kopii zapasowej i przydziel uprawnienia dla kont usług programu SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="af9c1-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="af9c1-269">Użyjesz bazy danych dostępności tego katalogu tooprepare hello na powitania repliki pomocniczej.</span><span class="sxs-lookup"><span data-stu-id="af9c1-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="af9c1-270">Utwórz bazę danych na **ContosoSQL1** o nazwie **MyDB1**przełączyć pełnej kopii zapasowej i kopii zapasowej dziennika i przywróci je na **ContosoSQL2** z hello **WITH NORECOVERY** opcji.</span><span class="sxs-lookup"><span data-stu-id="af9c1-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="af9c1-271">Utwórz punkty końcowe grupy dostępności hello na powitania maszynach wirtualnych serwera SQL i ustaw hello odpowiednie uprawnienia na powitania punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="af9c1-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

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
13. <span data-ttu-id="af9c1-272">Utwórz hello replik dostępności.</span><span class="sxs-lookup"><span data-stu-id="af9c1-272">Create hello availability replicas.</span></span>

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
14. <span data-ttu-id="af9c1-273">Na koniec Utwórz hello grupy dostępności i grupy dostępności toohello sprzężenia hello repliki pomocniczej.</span><span class="sxs-lookup"><span data-stu-id="af9c1-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="af9c1-274">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af9c1-274">Next steps</span></span>
<span data-ttu-id="af9c1-275">Możesz teraz pomyślnie zaimplementowano program SQL Server AlwaysOn przez utworzenie grupy dostępności na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="af9c1-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="af9c1-276">tooconfigure odbiornika dla tej grupy dostępności, zobacz [skonfigurować odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="af9c1-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="af9c1-277">Aby uzyskać inne informacje o korzystaniu z programu SQL Server na platformie Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af9c1-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
