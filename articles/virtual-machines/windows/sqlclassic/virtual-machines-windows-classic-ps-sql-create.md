---
title: aaaCreate maszyny wirtualnej programu SQL Server w programie Azure PowerShell (klasyczne) | Dokumentacja firmy Microsoft
description: "Zawiera kroki i skryptów programu PowerShell do tworzenia maszyny Wirtualnej platformy Azure z obrazów Galeria maszyny wirtualnej programu SQL Server. W tym temacie używa trybu klasycznego wdrożenia hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="ea3cd-104">Aprowizowanie maszyny wirtualnej programu SQL Server przy użyciu programu Azure PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="ea3cd-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="ea3cd-105">Ten artykuł zawiera kroki opisujące sposób toocreate maszynę wirtualną programu SQL Server na platformie Azure przy użyciu hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ea3cd-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ea3cd-107">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ea3cd-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="ea3cd-109">Wersja usługi Resource Manager hello tego tematu dla [Aprowizowanie maszyny wirtualnej programu SQL Server za pomocą Menedżera zasobów Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="ea3cd-110">Instalowanie i konfigurowanie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ea3cd-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="ea3cd-111">Jeśli nie masz konta platformy Azure, odwiedź stronę [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="ea3cd-112">[Pobierz i zainstaluj najnowsze poleceń programu Azure PowerShell hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="ea3cd-113">Uruchom program Windows PowerShell i podłącz go tooyour subskrypcji platformy Azure z hello **Add-AzureAccount** polecenia.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="ea3cd-114">Określić urządzenie docelowe region platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ea3cd-114">Determine your target Azure region</span></span>

<span data-ttu-id="ea3cd-115">Maszyny wirtualnej programu SQL Server będzie obsługiwana w systemie usługi chmury, która znajduje się w określonym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="ea3cd-116">Hello następujące kroki pomocy możesz toodetermine Twojego regionu, konta magazynu i usługi w chmurze, który będzie używany dla hello pozostałej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="ea3cd-117">Określ hello centrum danych, które mają toouse toohost maszyną Wirtualną programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="ea3cd-118">Hello następującego polecenia programu PowerShell Wyświetla listę nazw dostępnych regionów.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="ea3cd-119">Po wyłaniają preferowanych lokalizacji, ustaw zmienną o nazwie **$dcLocation** toothat regionu.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="ea3cd-120">Na przykład Witaj następujące polecenie ustawia hello region zbyt "Wschodnie stany USA":</span><span class="sxs-lookup"><span data-stu-id="ea3cd-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="ea3cd-121">Ustaw konto subskrypcji i magazynu</span><span class="sxs-lookup"><span data-stu-id="ea3cd-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="ea3cd-122">Określ hello subskrypcji platformy Azure, które będą używane dla nowej maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="ea3cd-123">Przypisywanie sieci docelowej subskrypcji platformy Azure toohello **$subscr** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="ea3cd-124">Następnie ustaw jako Twojej bieżącej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="ea3cd-125">Następnie sprawdź, czy istniejących kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="ea3cd-126">Witaj poniższy skrypt wyświetla wszystkie konta magazynu, które istnieją w wybranym regionie:</span><span class="sxs-lookup"><span data-stu-id="ea3cd-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="ea3cd-127">Jeśli potrzebujesz nowe konto magazynu, należy najpierw utworzyć nazwy konta magazynu liter wszystkich za pomocą polecenia hello AzureStorageAccount nowy jak hello poniższy przykład:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="ea3cd-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="ea3cd-128">Przypisz hello docelowy magazyn konta Nazwa toohello **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="ea3cd-129">Następnie użyj **AzureSubscription zestaw** tooset hello subskrypcji i bieżącego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="ea3cd-130">Wybierz obraz maszyny wirtualnej programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="ea3cd-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="ea3cd-131">Dowiedz się hello listę dostępnych obrazów maszyn wirtualnych serwera SQL z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="ea3cd-132">Tych obrazów, wszystkie mają **ImageFamily** właściwość, która rozpoczyna się od "SQL".</span><span class="sxs-lookup"><span data-stu-id="ea3cd-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="ea3cd-133">Witaj następujące zapytanie Wyświetla hello obrazu rodziny dostępne tooyou mające preinstalowany programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="ea3cd-134">Po znalezieniu rodziny obrazu maszyny wirtualnej hello w tej rodzinie może istnieć wiele obrazów opublikowanych.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="ea3cd-135">Użyj następujących hello skryptu toofind hello najnowszych opublikowanych nazwę maszyny wirtualnej obrazu dla rodziny wybranego obrazu (takich jak **programu SQL Server 2016 RTM przedsiębiorstwa w systemie Windows Server 2012 R2**):</span><span class="sxs-lookup"><span data-stu-id="ea3cd-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="ea3cd-136">Utwórz maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="ea3cd-136">Create hello virtual machine</span></span>

<span data-ttu-id="ea3cd-137">Na koniec Utwórz hello maszyny wirtualnej przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ea3cd-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="ea3cd-138">Tworzenie chmury usługi toohost hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="ea3cd-139">Należy pamiętać, że również możliwe toouse istniejącą usługę w chmurze zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="ea3cd-140">Utwórz nową zmienną **$svcname** z krótką nazwą hello hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="ea3cd-141">Określ nazwę maszyny wirtualnej hello i rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="ea3cd-142">Aby uzyskać więcej informacji na temat rozmiarów maszyn wirtualnych, zobacz [rozmiarów maszyn wirtualnych na platformie Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="ea3cd-143">Określ hello konta administratora lokalnego i hasło.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="ea3cd-144">Uruchom hello następującej maszyny wirtualnej hello toocreate skryptu.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="ea3cd-145">Dla opcji konfiguracji i dodatkowe informacje, zobacz hello **Utwórz zestaw poleceń** sekcji [toocreate Użyj programu PowerShell Azure i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="ea3cd-146">Przykładowy skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea3cd-146">Example PowerShell script</span></span>

<span data-ttu-id="ea3cd-147">Witaj następującego skryptu przykładowego pełną skryptu, który tworzy **programu SQL Server 2016 RTM przedsiębiorstwa w systemie Windows Server 2012 R2** maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="ea3cd-148">Jeśli używasz tego skryptu, należy dostosować hello początkowej zmiennych hello poprzednie kroki w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="ea3cd-149">Uzyskuj dostęp do usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="ea3cd-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="ea3cd-150">Tworzenie plików RDP hello toolaunch folderu dokumentu hello bieżącego użytkownika instalacji toocomplete tych maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="ea3cd-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="ea3cd-151">W katalogu dokumenty hello Uruchom plik RDP hello.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="ea3cd-152">Łączenie się z nazwą użytkownika administratora hello i hasło podane wcześniej (na przykład, jeśli nazwa użytkownika została VMAdmin, określ "\VMAdmin" jako użytkownik hello i podaj hasło hello).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="ea3cd-153">Konfiguracja pełną hello hello komputera serwera SQL dla dostępu zdalnego</span><span class="sxs-lookup"><span data-stu-id="ea3cd-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="ea3cd-154">Po zalogowaniu się na komputerze toohello przy użyciu pulpitu zdalnego, skonfigurować program SQL Server na powitania instrukcje w podstawie [kroki związane z konfigurowaniem łączności z serwerem SQL w maszynie Wirtualnej platformy Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea3cd-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ea3cd-155">Next steps</span></span>

<span data-ttu-id="ea3cd-156">Można znaleźć dodatkowe instrukcje dotyczące inicjowania obsługi administracyjnej maszyn wirtualnych przy użyciu programu PowerShell w hello [dokumentacji maszyn wirtualnych](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="ea3cd-157">W wielu przypadkach hello następnym krokiem jest toomigrate Twojego toothis baz danych nową maszynę Wirtualną programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="ea3cd-158">Aby uzyskać wskazówki dotyczące migracji bazy danych, zobacz [Migrowanie tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="ea3cd-159">Jeśli interesuje Cię również przy użyciu hello toocreate portalu Azure maszyny wirtualnej SQL, zobacz [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="ea3cd-160">Należy pamiętać, że samouczek hello zalecanym modelu Resource Manager, a nie hello modelu klasycznego, używane w tym temacie PowerShell tekst hello przeszukiwań przez hello portal tworzy maszyny wirtualne za pomocą.</span><span class="sxs-lookup"><span data-stu-id="ea3cd-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="ea3cd-161">Ponadto toothese zasobów, firma Microsoft zaleca przejrzenie [innych tematach dotyczących programu SQL Server w usłudze Azure Virtual Machines toorunning](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea3cd-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
