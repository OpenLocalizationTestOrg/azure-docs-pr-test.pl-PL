---
title: "Konfigurowanie zawsze włączonej grupy dostępności na maszynie Wirtualnej platformy Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym samouczku korzysta z zasobów, które zostały utworzone z klasycznym modelu wdrażania. Tworzenie zawsze włączonej grupy dostępności na platformie Azure za pomocą programu PowerShell."
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
ms.openlocfilehash: b99cf767fb931d3f7fe14fcbe7990126244613ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="4ffeb-104">Konfigurowanie zawsze włączonej grupy dostępności na maszynie Wirtualnej platformy Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ffeb-104">Configure the Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ffeb-105">Klasycznym: interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="4ffeb-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="4ffeb-106">[Klasycznym: środowiska PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="4ffeb-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="4ffeb-107">Przed rozpoczęciem należy wziąć pod uwagę może teraz ukończyć tego zadania w modelu Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="4ffeb-108">Firma Microsoft zaleca model Menedżera zasobów Azure dla nowych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="4ffeb-109">Zobacz [programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ffeb-110">Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-110">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="4ffeb-111">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4ffeb-112">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-112">This article covers using the classic deployment model.</span></span>

<span data-ttu-id="4ffeb-113">Azure maszynach wirtualnych (VM) może pomóc administratorom bazy danych na niższy koszt systemu wysokiej dostępności programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-113">Azure virtual machines (VMs) can help database administrators to lower the cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="4ffeb-114">W tym samouczku przedstawiono sposób wdrażania grupy dostępności za pomocą programu SQL Server AlwaysOn end-to-end wewnątrz środowiska platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-114">This tutorial shows you how to implement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="4ffeb-115">Na koniec samouczka rozwiązania programu SQL Server zawsze na platformie Azure będzie składać się z następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-115">At the end of the tutorial, your SQL Server Always On solution in Azure will consist of the following elements:</span></span>

* <span data-ttu-id="4ffeb-116">Sieć wirtualna zawiera wiele podsieci, w tym frontonu i zaplecza podsieci.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="4ffeb-117">Kontroler domeny z domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="4ffeb-118">Dwa programu SQL Server maszyny wirtualne, które są wdrażane do podsieci wewnętrznej i przyłączone do domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-118">Two SQL Server VMs that are deployed to the back-end subnet and joined to the Active Directory domain.</span></span>
* <span data-ttu-id="4ffeb-119">Trzy węzeł klastra pracy awaryjnej systemu Windows z modelu kworum Większość węzłów.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-119">A three-node Windows failover cluster with the Node Majority quorum model.</span></span>
* <span data-ttu-id="4ffeb-120">Grupa dostępności o dwóch replik z zatwierdzaniem synchronicznym bazy danych dostępności.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="4ffeb-121">Ten scenariusz jest dobrym rozwiązaniem dla uproszczenia jej na platformie Azure, a nie dla jego efektywność kosztowa lub innych czynników.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="4ffeb-122">Na przykład można zminimalizować liczbę maszyn wirtualnych dla dwóch repliki dostępności grupy do zapisywania godziny obliczeń na platformie Azure przy użyciu kontrolera domeny jako monitor udziału plików kworum w klastrze trybu failover z dwoma węzłami.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-122">For example, you can minimize the number of VMs for a two-replica availability group to save on compute hours in Azure by using the domain controller as the quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="4ffeb-123">Ta metoda zmniejsza liczbę maszyn wirtualnych przez jedną z powyższych konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-123">This method reduces the VM count by one from the above configuration.</span></span>

<span data-ttu-id="4ffeb-124">Ten samouczek jest przeznaczony do opisano kroki, które są wymagane, aby skonfigurować rozwiązanie opisane powyżej, bez opracowanie szczegóły każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-124">This tutorial is intended to show you the steps that are required to set up the described solution above, without elaborating on the details of each step.</span></span> <span data-ttu-id="4ffeb-125">W związku z tym etapy konfiguracji graficznego interfejsu użytkownika, a nie używa programu PowerShell skrypty umożliwiające szybkie przejście przez kolejne kroki.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-125">Therefore, instead of providing the GUI configuration steps, it uses PowerShell scripting to take you quickly through each step.</span></span> <span data-ttu-id="4ffeb-126">Ten samouczek zakłada następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-126">This tutorial assumes the following:</span></span>

* <span data-ttu-id="4ffeb-127">Masz już konto platformy Azure z subskrypcją maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-127">You already have an Azure account with the virtual machine subscription.</span></span>
* <span data-ttu-id="4ffeb-128">Po zainstalowaniu [poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-128">You've installed the [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="4ffeb-129">Masz już pełny opis zawsze włączonych grup dostępności dla rozwiązań lokalnych.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="4ffeb-130">Aby uzyskać więcej informacji, zobacz [zawsze włączonych grup dostępności (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-to-your-azure-subscription-and-create-the-virtual-network"></a><span data-ttu-id="4ffeb-131">Łączenie z subskrypcją platformy Azure i tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4ffeb-131">Connect to your Azure subscription and create the virtual network</span></span>
1. <span data-ttu-id="4ffeb-132">W oknie programu PowerShell na komputerze lokalnym Zaimportuj moduł Azure, pobieranie pliku ustawień publikowania do maszyny i sesji programu PowerShell połączyć się z subskrypcją platformy Azure przez zaimportowanie pobrany ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-132">In a PowerShell window on your local computer, import the Azure module, download the publishing settings file to your machine, and connect your PowerShell session to your Azure subscription by importing the downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="4ffeb-133">**Get AzurePublishSettingsFile** polecenie automatycznie generuje certyfikat zarządzania platformy Azure i pliki do pobrania na komputerze.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-133">The **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it to your machine.</span></span> <span data-ttu-id="4ffeb-134">Przeglądarką jest automatycznie otwierane i zostanie wyświetlony monit o podanie poświadczeń konta Microsoft dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-134">A browser is automatically opened, and you're prompted to enter the Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="4ffeb-135">Pobrany **.publishsettings** plik zawiera wszystkich informacji potrzebnych do zarządzania subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-135">The downloaded **.publishsettings** file contains all the information that you need to manage your Azure subscription.</span></span> <span data-ttu-id="4ffeb-136">Po zapisaniu tego pliku do katalogu lokalnego, zaimportuj go za pomocą **AzurePublishSettingsFile importu** polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-136">After saving this file to a local directory, import it by using the **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ffeb-137">Plik .publishsettings zawiera swoje poświadczenia (Niezakodowane), które są używane do administrowania subskrypcji platformy Azure i usługi.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-137">The .publishsettings file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="4ffeb-138">Najlepszym rozwiązaniem bezpieczeństwa dla tego pliku jest tymczasowo przechowywane poza katalogów źródła (na przykład w folderze Libraries\Documents), a następnie usuń ją po zakończeniu importowania.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-138">The security best practice for this file is to store it temporarily outside your source directories (for example, in the Libraries\Documents folder), and then delete it after the import has finished.</span></span> <span data-ttu-id="4ffeb-139">Złośliwy użytkownik, który uzyskuje dostęp do pliku .publishsettings można edytować, tworzenia i usuwania usług Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-139">A malicious user who gains access to the .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="4ffeb-140">Zdefiniuj szereg zmiennych, które będą używane do tworzenia infrastruktury chmury.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-140">Define a series of variables that you'll use to create your cloud IT infrastructure.</span></span>

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

    <span data-ttu-id="4ffeb-141">Należy zwrócić uwagę na następujące, aby upewnić się, że poleceniach powiedzie się później:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-141">Pay attention to the following to ensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="4ffeb-142">Zmienne **$storageAccountName** i **$dcServiceName** musi być unikatowa, ponieważ są używane do identyfikowania chmury konta i w chmurze serwer magazynu, odpowiednio w Internecie.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used to identify your cloud storage account and cloud server, respectively, on the Internet.</span></span>
   * <span data-ttu-id="4ffeb-143">Nazwy, które określisz zmiennych **$affinityGroupName** i **$virtualNetworkName** są skonfigurowane w dokumencie konfiguracji sieci wirtualnej, który będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-143">The names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in the virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="4ffeb-144">**$sqlImageName** Określa zaktualizowaną nazwę obrazu maszyny Wirtualnej, która zawiera SQL Server 2012 Service Pack 1 Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-144">**$sqlImageName** specifies the updated name of the VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="4ffeb-145">Dla uproszczenia **Contoso! 000** to samo hasło, które jest używane w całej samouczka.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-145">For simplicity, **Contoso!000** is the same password that's used throughout the entire tutorial.</span></span>

3. <span data-ttu-id="4ffeb-146">Utwórz grupę koligacji.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="4ffeb-147">Tworzenie sieci wirtualnej przez zaimportowanie pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="4ffeb-148">Plik konfiguracji zawiera następujący dokument XML.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-148">The configuration file contains the following XML document.</span></span> <span data-ttu-id="4ffeb-149">Krótko mówiąc, określa sieć wirtualną o nazwie **ContosoNET** w grupie koligacji o nazwie **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-149">In brief, it specifies a virtual network called **ContosoNET** in the affinity group called **ContosoAG**.</span></span> <span data-ttu-id="4ffeb-150">Przestrzeń adresowa ma **10.10.0.0/16** i ma dwie podsieci **10.10.1.0/24** i **10.10.2.0/24**, będące odpowiednio podsieci frontonu i Wstecz podsieci.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-150">It has the address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are the front subnet and back subnet, respectively.</span></span> <span data-ttu-id="4ffeb-151">Front podsieci jest umieszczane aplikacji klienckich, takich jak Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-151">The front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="4ffeb-152">Wstecz podsieci będą umieszczane są maszynach wirtualnych serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-152">The back subnet is where you'll place the SQL Server VMs.</span></span> <span data-ttu-id="4ffeb-153">Jeśli zmienisz **$affinityGroupName** i **$virtualNetworkName** zmienne wcześniej, należy również zmienić nazwy poniżej.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-153">If you change the **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change the corresponding names below.</span></span>

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

5. <span data-ttu-id="4ffeb-154">Utwórz konto magazynu, który został skojarzony z grupą koligacji utworzyć i ustawić go jako bieżącego konta magazynu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-154">Create a storage account that's associated with the affinity group that you created, and set it as the current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="4ffeb-155">Utwórz serwer kontrolera domeny w nowym zestawie dostępności i usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-155">Create the domain controller server in the new cloud service and availability set.</span></span>

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

    <span data-ttu-id="4ffeb-156">Te polecenia gazociągami wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-156">These piped commands do the following things:</span></span>

   * <span data-ttu-id="4ffeb-157">**Nowy AzureVMConfig** tworzy konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="4ffeb-158">**Dodaj AzureProvisioningConfig** daje parametry konfiguracji autonomicznym serwerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-158">**Add-AzureProvisioningConfig** gives the configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="4ffeb-159">**Dodaj AzureDataDisk** dodaje dysk danych, które będzie używane do przechowywania danych usługi Active Directory przy użyciu opcji buforowania, wartość None.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-159">**Add-AzureDataDisk** adds the data disk that you'll use for storing Active Directory data, with the caching option set to None.</span></span>
   * <span data-ttu-id="4ffeb-160">**Nowy AzureVM** tworzy nową usługę w chmurze i utworzenie nowej maszyny Wirtualnej platformy Azure w nowej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-160">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span>

7. <span data-ttu-id="4ffeb-161">Poczekaj, aż nowej maszyny Wirtualnej być w pełni obsługiwany i pobranie pliku pulpitu zdalnego do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-161">Wait for the new VM to be fully provisioned, and download the remote desktop file to your working directory.</span></span> <span data-ttu-id="4ffeb-162">Ponieważ nowej maszyny Wirtualnej Azure zajmuje dużo czasu, aby udostępnić, `while` pętli kontynuuje sondowanie nowej maszyny Wirtualnej, dopóki nie jest gotowa do użycia.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-162">Because the new Azure VM takes a long time to provision, the `while` loop continues to poll the new VM until it's ready for use.</span></span>

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

<span data-ttu-id="4ffeb-163">Teraz pomyślnie obsługiwanej przez serwer kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-163">The domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="4ffeb-164">Następnie należy skonfigurować domeny usługi Active Directory na tym serwerze kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-164">Next, you'll configure the Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="4ffeb-165">Pozostaw otwarte okno programu PowerShell na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-165">Leave the PowerShell window open on your local computer.</span></span> <span data-ttu-id="4ffeb-166">Użyjesz go ponownie później można utworzyć dwóch maszyn wirtualnych serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-166">You'll use it again later to create the two SQL Server VMs.</span></span>

## <a name="configure-the-domain-controller"></a><span data-ttu-id="4ffeb-167">Konfiguracja kontrolera domeny</span><span class="sxs-lookup"><span data-stu-id="4ffeb-167">Configure the domain controller</span></span>
1. <span data-ttu-id="4ffeb-168">Połączyć się z serwerem kontrolera domeny przez uruchomienie pliku pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-168">Connect to the domain controller server by launching the remote desktop file.</span></span> <span data-ttu-id="4ffeb-169">Użyj AzureAdmin nazwy użytkownika i hasło administratora maszyny **Contoso! 000**, która została określona podczas tworzenia nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-169">Use the machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created the new VM.</span></span>
2. <span data-ttu-id="4ffeb-170">Otwórz okno programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="4ffeb-171">Uruchom następujące polecenie **DCPROMO. EXE** polecenie, aby skonfigurować **corp.contoso.com** domeny z katalogami danych na dysku M.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-171">Run the following **DCPROMO.EXE** command to set up the **corp.contoso.com** domain, with the data directories on drive M.</span></span>

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

    <span data-ttu-id="4ffeb-172">Po zakończeniu działania polecenia do automatycznego uruchomienia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-172">After the command finishes, the VM restarts automatically.</span></span>

4. <span data-ttu-id="4ffeb-173">Ponownie nawiąż połączenie z serwerem kontrolera domeny przez uruchomienie pliku pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-173">Connect to the domain controller server again by launching the remote desktop file.</span></span> <span data-ttu-id="4ffeb-174">Teraz, zaloguj się jako **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="4ffeb-175">Otwórz okno programu PowerShell w trybie administratora, a następnie zaimportować moduł środowiska PowerShell usługi Active Directory przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-175">Open a PowerShell window in administrator mode, and import the Active Directory PowerShell module by using the following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="4ffeb-176">Uruchom następujące polecenia, aby dodać trzech użytkowników do domeny.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-176">Run the following commands to add three users to the domain.</span></span>

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

    <span data-ttu-id="4ffeb-177">**CORP\Install** służy do konfigurowania wszystkich związanych z wystąpień usługi programu SQL Server i klastra trybu failover oraz grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-177">**CORP\Install** is used to configure everything related to the SQL Server service instances, the failover cluster, and the availability group.</span></span> <span data-ttu-id="4ffeb-178">**CORP\SQLSvc1** i **CORP\SQLSvc2** są używane jako konto usługi programu SQL Server dla dwóch maszyn wirtualnych serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as the SQL Server service accounts for the two SQL Server VMs.</span></span>
7. <span data-ttu-id="4ffeb-179">Następnie uruchom następujące polecenia, aby zapewnić **CORP\Install** uprawnienia do tworzenia obiektów komputerów w domenie.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-179">Next, run the following commands to give **CORP\Install** the permissions to create computer objects in the domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="4ffeb-180">Wymienione powyżej identyfikator GUID jest identyfikatorem GUID dla typu obiektu komputera.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-180">The GUID specified above is the GUID for the computer object type.</span></span> <span data-ttu-id="4ffeb-181">**CORP\Install** konta potrzeb **Odczyt wszystkich właściwości** i **tworzenia obiektów komputerów** uprawnienia do tworzenia obiektów Active bezpośrednie dla klastra trybu failover.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-181">The **CORP\Install** account needs the **Read All Properties** and **Create Computer Objects** permission to create the Active Direct objects for the failover cluster.</span></span> <span data-ttu-id="4ffeb-182">**Odczyt wszystkich właściwości** uprawnienie jest już używana CORP\Install domyślnie, dzięki czemu nie trzeba go jawnie udzielić.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-182">The **Read All Properties** permission is already given to CORP\Install by default, so you don't need to grant it explicitly.</span></span> <span data-ttu-id="4ffeb-183">Aby uzyskać więcej informacji dotyczących uprawnień, które są niezbędne do utworzenia klastra trybu failover, zobacz [przewodnik krok po kroku klastra pracy awaryjnej: Konfigurowanie kont w usłudze Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-183">For more information on permissions that are needed to create the failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="4ffeb-184">Teraz, po zakończeniu konfigurowania usługi Active Directory i obiektów użytkowników, będzie dwóch maszyn wirtualnych programu SQL Server Utwórz i dołącz je do tej domeny.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-184">Now that you've finished configuring Active Directory and the user objects, you'll create two SQL Server VMs and join them to this domain.</span></span>

## <a name="create-the-sql-server-vms"></a><span data-ttu-id="4ffeb-185">Tworzenie maszyn wirtualnych serwera SQL</span><span class="sxs-lookup"><span data-stu-id="4ffeb-185">Create the SQL Server VMs</span></span>
1. <span data-ttu-id="4ffeb-186">Nadal używać okno programu PowerShell, który jest otwarty na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-186">Continue to use the PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="4ffeb-187">Zdefiniuj następujące zmienne dodatkowe:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-187">Define the following additional variables:</span></span>

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

    <span data-ttu-id="4ffeb-188">Adres IP **10.10.0.4** zwykle jest przypisany do pierwszej maszyny Wirtualnej utworzone w **10.10.0.0/16** podsieci sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-188">The IP address **10.10.0.4** is typically assigned to the first VM that you create in the **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="4ffeb-189">Należy sprawdzić, czy jest to adres serwera kontrolera domeny, uruchamiając **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-189">You should verify that this is the address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="4ffeb-190">Uruchom następujące przetwarzana potokowo poleceń, aby utworzyć pierwszy maszyny Wirtualnej w klastrze trybu failover o nazwie **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-190">Run the following piped commands to create the first VM in the failover cluster, named **ContosoQuorum**:</span></span>

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

    <span data-ttu-id="4ffeb-191">Należy pamiętać, że dotyczących powyższego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-191">Note the following regarding the command above:</span></span>

   * <span data-ttu-id="4ffeb-192">**Nowy AzureVMConfig** tworzy konfiguracji maszyny Wirtualnej o nazwie zestaw żądaną dostępności.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-192">**New-AzureVMConfig** creates a VM configuration with the desired availability set name.</span></span> <span data-ttu-id="4ffeb-193">Kolejnych maszyn wirtualnych o takiej samej nazwie zestawu dostępności zostanie utworzony, dzięki czemu są one przyłączone do tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-193">The subsequent VMs will be created with the same availability set name so that they're joined to the same availability set.</span></span>
   * <span data-ttu-id="4ffeb-194">**Dodaj AzureProvisioningConfig** dołącza maszynę Wirtualną do domeny usługi Active Directory, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-194">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="4ffeb-195">**Zestaw AzureSubnet** umieszcza maszynę Wirtualną do tyłu podsieci.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-195">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="4ffeb-196">**Nowy AzureVM** tworzy nową usługę w chmurze i utworzenie nowej maszyny Wirtualnej platformy Azure w nowej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-196">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span> <span data-ttu-id="4ffeb-197">**DnsSettings** parametr określa, że serwer DNS dla serwerów w nowej usługi w chmurze ma adres IP **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-197">The **DnsSettings** parameter specifies that the DNS server for the servers in the new cloud service has the IP address **10.10.0.4**.</span></span> <span data-ttu-id="4ffeb-198">Jest to adres IP serwera kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-198">This is the IP address of the domain controller server.</span></span> <span data-ttu-id="4ffeb-199">Ten parametr jest wymagane do włączenia nowych maszyn wirtualnych w usłudze w chmurze do przyłączania do domeny usługi Active Directory pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-199">This parameter is needed to enable the new VMs in the cloud service to join to the Active Directory domain successfully.</span></span> <span data-ttu-id="4ffeb-200">Bez tego parametru musi ręcznie skonfigurować ustawienia protokołu IPv4 maszynie wirtualnej, aby użyć serwera kontrolera domeny jako podstawowy serwer DNS po udostępnieniu maszyny Wirtualnej, a następnie dołącz maszynę Wirtualną do domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-200">Without this parameter, you must manually set the IPv4 settings in your VM to use the domain controller server as the primary DNS server after the VM is provisioned, and then join the VM to the Active Directory domain.</span></span>
3. <span data-ttu-id="4ffeb-201">Uruchom następujące przetwarzana potokowo poleceń, aby utworzyć maszynach wirtualnych serwera SQL, o nazwie **ContosoSQL1** i **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-201">Run the following piped commands to create the SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

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

    <span data-ttu-id="4ffeb-202">Należy pamiętać, że dotyczących powyższego polecenia:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-202">Note the following regarding the commands above:</span></span>

   * <span data-ttu-id="4ffeb-203">**Nowy AzureVMConfig** korzysta taką samą nazwę zestawu dostępności jako serwer kontrolera domeny, a SQL Server 2012 Service Pack 1 Enterprise Edition obraz w galerii maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-203">**New-AzureVMConfig** uses the same availability set name as the domain controller server, and uses the SQL Server 2012 Service Pack 1 Enterprise Edition image in the virtual machine gallery.</span></span> <span data-ttu-id="4ffeb-204">Ustawia również dysku systemu operacyjnego do odczytu buforowania tylko (nie buforowania zapisu).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-204">It also sets the operating system disk to read-caching only (no write caching).</span></span> <span data-ttu-id="4ffeb-205">Firma Microsoft zaleca migracji pliki bazy danych na dysku odrębne dołączonej do maszyny Wirtualnej i skonfiguruj ją bez odczytu lub zapisu w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-205">We recommend that you migrate the database files to a separate data disk that you attach to the VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="4ffeb-206">Jednakże następnym krokiem jest usunięcie buforowanie zapisu na dysku systemu operacyjnego, ponieważ nie można usunąć buforowania odczytu na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-206">However, the next best thing is to remove write caching on the operating system disk because you can't remove read caching on the operating system disk.</span></span>
   * <span data-ttu-id="4ffeb-207">**Dodaj AzureProvisioningConfig** dołącza maszynę Wirtualną do domeny usługi Active Directory, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-207">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="4ffeb-208">**Zestaw AzureSubnet** umieszcza maszynę Wirtualną do tyłu podsieci.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-208">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="4ffeb-209">**Dodaj AzureEndpoint** dodaje punkty końcowe dostępu, dzięki czemu aplikacje klienckie mogą uzyskiwać dostęp do tych wystąpień usługi programu SQL Server w Internecie.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on the Internet.</span></span> <span data-ttu-id="4ffeb-210">Inne porty są podane ContosoSQL1 i ContosoSQL2.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-210">Different ports are given to ContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="4ffeb-211">**Nowy AzureVM** tworzy nową maszynę Wirtualną programu SQL Server w tej samej usłudze w chmurze jako ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-211">**New-AzureVM** creates the new SQL Server VM in the same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="4ffeb-212">Maszyny wirtualne należy umieścić w tej samej usłudze w chmurze, jeśli użytkownicy powinni być w tym samym zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-212">You must place the VMs in the same cloud service if you want them to be in the same availability set.</span></span>
4. <span data-ttu-id="4ffeb-213">Poczekaj na każdej maszynie Wirtualnej, aby być w pełni obsługiwany i dla każdej maszyny Wirtualnej pobrać jego pliku pulpitu zdalnego do katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-213">Wait for each VM to be fully provisioned and for each VM to download its remote desktop file to your working directory.</span></span> <span data-ttu-id="4ffeb-214">`for` Pętli przełączanie po kolei trzech nowych maszyn wirtualnych i wykonuje polecenia wewnątrz najwyższego poziomu nawiasów klamrowych dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-214">The `for` loop cycles through the three new VMs and executes the commands inside the top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until the VM status is "ReadyRole"
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

    <span data-ttu-id="4ffeb-215">Teraz obsługi administracyjnej maszyn wirtualnych serwera SQL i uruchomiona, ale są zainstalowane z programem SQL Server z opcji domyślnych.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-215">The SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-the-failover-cluster-vms"></a><span data-ttu-id="4ffeb-216">Inicjowanie klastra trybu failover maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="4ffeb-216">Initialize the failover cluster VMs</span></span>
<span data-ttu-id="4ffeb-217">W tej sekcji należy zmodyfikować trzy serwery, które będą używane w klastrze trybu failover i instalacji programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-217">In this section, you need to modify the three servers that you'll use in the failover cluster and the SQL Server installation.</span></span> <span data-ttu-id="4ffeb-218">W szczególności:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-218">Specifically:</span></span>

* <span data-ttu-id="4ffeb-219">Wszystkie serwery: należy zainstalować **klaster pracy awaryjnej** funkcji.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-219">All servers: You need to install the **Failover Clustering** feature.</span></span>
* <span data-ttu-id="4ffeb-220">Wszystkie serwery: należy dodać **CORP\Install** jako maszynę **administratora**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-220">All servers: You need to add **CORP\Install** as the machine **administrator**.</span></span>
* <span data-ttu-id="4ffeb-221">ContosoSQL1 i ContosoSQL2 tylko: należy dodać **CORP\Install** jako **sysadmin** roli w domyślnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-221">ContosoSQL1 and ContosoSQL2 only: You need to add **CORP\Install** as a **sysadmin** role in the default database.</span></span>
* <span data-ttu-id="4ffeb-222">ContosoSQL1 i ContosoSQL2 tylko: należy dodać **NT AUTHORITY\System** jako logowanie z następującymi uprawnieniami:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-222">ContosoSQL1 and ContosoSQL2 only: You need to add **NT AUTHORITY\System** as a sign-in with the following permissions:</span></span>

  * <span data-ttu-id="4ffeb-223">Instrukcja ALTER żadnej grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="4ffeb-223">Alter any availability group</span></span>
  * <span data-ttu-id="4ffeb-224">Połączenia SQL</span><span class="sxs-lookup"><span data-stu-id="4ffeb-224">Connect SQL</span></span>
  * <span data-ttu-id="4ffeb-225">Widok stanu serwera</span><span class="sxs-lookup"><span data-stu-id="4ffeb-225">View server state</span></span>
* <span data-ttu-id="4ffeb-226">ContosoSQL1 i ContosoSQL2 tylko: **TCP** na maszynie Wirtualnej serwera SQL jest już włączony protokół.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-226">ContosoSQL1 and ContosoSQL2 only: The **TCP** protocol is already enabled on the SQL Server VM.</span></span> <span data-ttu-id="4ffeb-227">Jednakże nadal konieczne otwarcie zapory dla dostępu zdalnego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-227">However, you still need to open the firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="4ffeb-228">Teraz możesz przystąpić do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-228">Now, you're ready to start.</span></span> <span data-ttu-id="4ffeb-229">Począwszy od **ContosoQuorum**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-229">Beginning with **ContosoQuorum**, follow the steps below:</span></span>

1. <span data-ttu-id="4ffeb-230">Połączyć się z **ContosoQuorum** uruchamiając pliki pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-230">Connect to **ContosoQuorum** by launching the remote desktop files.</span></span> <span data-ttu-id="4ffeb-231">Użyj nazwy użytkownika administratora maszyny **AzureAdmin** i hasło **Contoso! 000**, która została określona podczas tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-231">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="4ffeb-232">Sprawdź, czy komputery zostały pomyślnie przyłączone do **corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-232">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="4ffeb-233">Poczekaj na zakończenie uruchomionych zadań inicjowania automatycznego przed kontynuowaniem instalacji programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-233">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="4ffeb-234">Otwórz okno programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="4ffeb-235">Zainstaluj funkcję Klaster pracy awaryjnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-235">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="4ffeb-236">Dodaj **CORP\Install** jako administrator lokalny.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="4ffeb-237">Wyloguj ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="4ffeb-238">Gotowe z tym serwerem teraz.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="4ffeb-239">Następnie należy zainicjować **ContosoSQL1** i **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="4ffeb-240">Wykonaj poniższe kroki, które są takie same dla obu maszynach wirtualnych serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-240">Follow the steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="4ffeb-241">Nawiązać dwóch maszyn wirtualnych serwera SQL, uruchamiając pliki pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-241">Connect to the two SQL Server VMs by launching the remote desktop files.</span></span> <span data-ttu-id="4ffeb-242">Użyj nazwy użytkownika administratora maszyny **AzureAdmin** i hasło **Contoso! 000**, która została określona podczas tworzenia maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-242">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="4ffeb-243">Sprawdź, czy komputery zostały pomyślnie przyłączone do **corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-243">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="4ffeb-244">Poczekaj na zakończenie uruchomionych zadań inicjowania automatycznego przed kontynuowaniem instalacji programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-244">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="4ffeb-245">Otwórz okno programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="4ffeb-246">Zainstaluj funkcję Klaster pracy awaryjnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-246">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="4ffeb-247">Dodaj **CORP\Install** jako administrator lokalny.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="4ffeb-248">Importuj dostawcy programu PowerShell programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-248">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="4ffeb-249">Dodaj **CORP\Install** jako rola administratora systemu dla domyślnego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-249">Add **CORP\Install** as the sysadmin role for the default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="4ffeb-250">Dodaj **NT AUTHORITY\System** jako logowanie przy użyciu uprawnień trzech opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-250">Add **NT AUTHORITY\System** as a sign-in with the three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="4ffeb-251">Otwórz Zaporę dostępu zdalnego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-251">Open the firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="4ffeb-252">Wyloguj obie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="4ffeb-253">Ponadto możesz przystąpić do konfigurowania grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-253">Finally, you're ready to configure the availability group.</span></span> <span data-ttu-id="4ffeb-254">Dostawcy programu PowerShell programu SQL Server używanego do wykonywania pracy na **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-254">You'll use the SQL Server PowerShell Provider to perform all of the work on **ContosoSQL1**.</span></span>

## <a name="configure-the-availability-group"></a><span data-ttu-id="4ffeb-255">Skonfiguruj grupy dostępności</span><span class="sxs-lookup"><span data-stu-id="4ffeb-255">Configure the availability group</span></span>
1. <span data-ttu-id="4ffeb-256">Połączyć się z **ContosoSQL1** ponownie, uruchamiając pliki pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-256">Connect to **ContosoSQL1** again by launching the remote desktop files.</span></span> <span data-ttu-id="4ffeb-257">Zamiast logowanie się przy użyciu konta komputera, zaloguj się przy użyciu **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-257">Instead of signing in by using the machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="4ffeb-258">Otwórz okno programu PowerShell w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="4ffeb-259">Zdefiniuj następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="4ffeb-259">Define the following variables:</span></span>

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
4. <span data-ttu-id="4ffeb-260">Importuj dostawcy programu PowerShell programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-260">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="4ffeb-261">Zmień konto usługi programu SQL Server dla ContosoSQL1 na CORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-261">Change the SQL Server service account for ContosoSQL1 to CORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="4ffeb-262">Zmień konto usługi programu SQL Server dla ContosoSQL2 na CORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-262">Change the SQL Server service account for ContosoSQL2 to CORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="4ffeb-263">Pobierz **CreateAzureFailoverCluster.ps1** z [Tworzenie klastra trybu Failover dla zawsze włączonych grup dostępności w maszynie Wirtualnej platformy Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) do lokalny katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) to the local working directory.</span></span> <span data-ttu-id="4ffeb-264">Tworzenie klastra trybu failover funkcjonalności użyjesz tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-264">You'll use this script to help you create a functional failover cluster.</span></span> <span data-ttu-id="4ffeb-265">Ważne informacje dotyczące jak klaster pracy awaryjnej systemu Windows współdziała z sieci platformy Azure znajdują się w temacie [wysokiej dostępności i odzyskiwania po awarii dla programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-265">For important information on how Windows Failover Clustering interacts with the Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="4ffeb-266">Zmień katalog roboczy i utworzyć klaster trybu failover z pobranego skryptu.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-266">Change to your working directory and create the failover cluster with the downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="4ffeb-267">Włącz zawsze włączone grupy dostępności dla domyślnego wystąpienia programu SQL Server na **ContosoSQL1** i **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-267">Enable Always On availability groups for the default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

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
10. <span data-ttu-id="4ffeb-268">Utwórz katalog kopii zapasowej i przydziel uprawnienia dla kont usług programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-268">Create a backup directory and grant permissions for the SQL Server service accounts.</span></span> <span data-ttu-id="4ffeb-269">Ten katalog będzie umożliwia przygotowanie bazy danych dostępności w replice pomocniczej.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-269">You'll use this directory to prepare the availability database on the secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="4ffeb-270">Utwórz bazę danych na **ContosoSQL1** o nazwie **MyDB1**przełączyć pełnej kopii zapasowej i kopii zapasowej dziennika i przywróci je na **ContosoSQL2** z **WITH NORECOVERY**  opcji.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with the **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="4ffeb-271">Tworzenie punktów końcowych grupy dostępności na maszynach wirtualnych serwera SQL i ustaw odpowiednie uprawnienia w punktach końcowych.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-271">Create the availability group endpoints on the SQL Server VMs and set the proper permissions on the endpoints.</span></span>

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
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct1]" -ServerInstance $server2
13. <span data-ttu-id="4ffeb-272">Tworzenie replik dostępności.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-272">Create the availability replicas.</span></span>

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
14. <span data-ttu-id="4ffeb-273">Na koniec należy utworzyć grupy dostępności i przyłączania repliki pomocniczej do grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-273">Finally, create the availability group and join the secondary replica to the availability group.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4ffeb-274">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ffeb-274">Next steps</span></span>
<span data-ttu-id="4ffeb-275">Możesz teraz pomyślnie zaimplementowano program SQL Server AlwaysOn przez utworzenie grupy dostępności na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4ffeb-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="4ffeb-276">Aby skonfigurować odbiornik grupy dostępności, zobacz [skonfigurować odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-276">To configure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="4ffeb-277">Aby uzyskać inne informacje o korzystaniu z programu SQL Server na platformie Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ffeb-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
