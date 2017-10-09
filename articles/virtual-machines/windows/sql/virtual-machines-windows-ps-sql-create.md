---
title: aaaCreate maszyny wirtualnej programu SQL Server w programie Azure PowerShell (Resource Manager) | Dokumentacja firmy Microsoft
description: "Zawiera kroki i skryptów programu PowerShell do tworzenia maszyny Wirtualnej platformy Azure z obrazów Galeria maszyny wirtualnej programu SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="8ba17-103">Aprowizowanie maszyny wirtualnej programu SQL Server przy użyciu programu Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="8ba17-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ba17-104">Portal</span><span class="sxs-lookup"><span data-stu-id="8ba17-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="8ba17-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ba17-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="8ba17-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8ba17-106">Overview</span></span>
<span data-ttu-id="8ba17-107">Ten samouczek pokazuje, jak hello toocreate jednej maszyny wirtualnej platformy Azure przy użyciu **usługi Azure Resource Manager** modelu wdrażania przy użyciu poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ba17-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8ba17-108">W tym samouczku utworzymy jednej maszyny wirtualnej za pomocą pojedynczego dysku z obrazu w hello galerii SQL.</span><span class="sxs-lookup"><span data-stu-id="8ba17-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="8ba17-109">Zostanie utworzony nowy dostawców dla hello magazynu, sieci i zasoby obliczeniowe, które będą używane przez maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="8ba17-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="8ba17-110">Jeśli masz istniejące dostawców dla każdego z tych zasobów, można użyć tych dostawców.</span><span class="sxs-lookup"><span data-stu-id="8ba17-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="8ba17-111">Należy hello klasycznej wersji w tym temacie, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server przy użyciu usługi Azure PowerShell klasycznego](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="8ba17-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ba17-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ba17-112">Prerequisites</span></span>
<span data-ttu-id="8ba17-113">W tym samouczku potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="8ba17-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="8ba17-114">Konto platformy Azure i subskrypcji przed jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="8ba17-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="8ba17-115">Jeśli nie masz, zaloguj się do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ba17-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8ba17-116">[Program Azure PowerShell)](/powershell/azure/overview), minimalna wersja 1.4.0 lub nowszy (w tym samouczku napisane przy użyciu wersji 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="8ba17-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="8ba17-117">tooretrieve Twojej wersji, typ **flagą Azure Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="8ba17-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="8ba17-118">Skonfiguruj subskrypcję</span><span class="sxs-lookup"><span data-stu-id="8ba17-118">Configure your subscription</span></span>
<span data-ttu-id="8ba17-119">Otwórz program Windows PowerShell i ustanowienia tooyour dostępu do konta platformy Azure, uruchamiając następujące polecenie cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="8ba17-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="8ba17-120">Zostaną wyświetlone z logowaniem tooenter ekranu swoje poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="8ba17-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="8ba17-121">Użyj hello sam adres e-mail i hasło, użyj toosign w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba17-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="8ba17-122">Po pomyślnym zalogowaniu zobaczysz niektóre informacje na ekranie, zawierającą SubscriptionId hello, z którym użytkownik zalogowany.</span><span class="sxs-lookup"><span data-stu-id="8ba17-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="8ba17-123">Jest to hello subskrypcji, w którym zostaną utworzone zasoby hello w tym samouczku, chyba że zostanie zmienione tooa innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8ba17-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="8ba17-124">Jeśli masz wiele SubscriptionIds, uruchom następujące polecenie cmdlet tooreturn hello listę wszystkich SubscriptionIds Twojego:</span><span class="sxs-lookup"><span data-stu-id="8ba17-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="8ba17-125">Uruchom następujące polecenie cmdlet z Twojej żądany identyfikator subskrypcji hello tooanother toochange SubscriptionID.</span><span class="sxs-lookup"><span data-stu-id="8ba17-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="8ba17-126">Zdefiniuj zmienne obrazu</span><span class="sxs-lookup"><span data-stu-id="8ba17-126">Define image variables</span></span>
<span data-ttu-id="8ba17-127">toosimplify użyteczność i zrozumienia ukończyć powitalnych skryptu z tego samouczka Rozpoczniemy, definiując liczba zmiennych.</span><span class="sxs-lookup"><span data-stu-id="8ba17-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="8ba17-128">Zmień wartości parametrów hello, ale należy wziąć pod nazewnictwa długości pokrewne tooname ograniczenia i znaków specjalnych podczas modyfikowania hello wartości.</span><span class="sxs-lookup"><span data-stu-id="8ba17-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="8ba17-129">Lokalizacji i grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="8ba17-129">Location and Resource Group</span></span>
<span data-ttu-id="8ba17-130">Użyj dwóch zmiennych toodefine hello danych regionu i hello grupy zasobów w której zostanie utworzona hello inne zasoby dotyczące hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="8ba17-131">Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="8ba17-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="8ba17-132">Magazyn właściwości</span><span class="sxs-lookup"><span data-stu-id="8ba17-132">Storage properties</span></span>
<span data-ttu-id="8ba17-133">Użyj hello następujące zmienne toodefine hello konta i hello typ magazynu używanych przez maszynę wirtualną hello toobe magazynu.</span><span class="sxs-lookup"><span data-stu-id="8ba17-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="8ba17-134">Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="8ba17-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="8ba17-135">Należy pamiętać, że w tym przykładzie używamy [magazyn w warstwie Premium](../../../storage/common/storage-premium-storage.md), który jest zalecane w przypadku obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="8ba17-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="8ba17-136">Aby uzyskać więcej informacji na ten wskazówki i inne zalecenia, zobacz [wydajności najlepsze rozwiązania dotyczące programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="8ba17-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="8ba17-137">Właściwości sieci</span><span class="sxs-lookup"><span data-stu-id="8ba17-137">Network properties</span></span>
<span data-ttu-id="8ba17-138">Użyj powitania po interfejsu sieciowego hello toodefine zmienne, Metoda alokacji TCP/IP hello, hello wirtualnej nazwy sieciowej, Nazwa podsieci wirtualnej hello, hello zakres adresów IP dla sieci wirtualnej hello, hello zakres adresów IP podsieci hello i hello używanej przez sieć hello w maszynie wirtualnej hello toobe etykieta nazwy domeny publicznej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="8ba17-139">Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="8ba17-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="8ba17-140">Właściwości maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8ba17-140">Virtual machine properties</span></span>
<span data-ttu-id="8ba17-141">Użyj następującego nazwę maszyny wirtualnej hello toodefine zmienne, nazwę komputera hello hello rozmiar maszyny wirtualnej i hello nazwa dysku systemu operacyjnego dla maszyny wirtualnej hello hello.</span><span class="sxs-lookup"><span data-stu-id="8ba17-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="8ba17-142">Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="8ba17-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="8ba17-143">Właściwości obrazu</span><span class="sxs-lookup"><span data-stu-id="8ba17-143">Image properties</span></span>
<span data-ttu-id="8ba17-144">Użyj hello następujące zmienne toodefine hello obrazu toouse hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="8ba17-145">W tym przykładzie obraz programu SQL Server 2016 Enterprise hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="8ba17-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="8ba17-146">Zmodyfikować zgodnie z potrzebami, a następnie wykonaj następujące polecenia cmdlet tooinitialize hello tych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="8ba17-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="8ba17-147">Należy pamiętać, że można uzyskać pełną listę ofert obrazu programu SQL Server za pomocą polecenia Get-AzureRmVMImageOffer hello:</span><span class="sxs-lookup"><span data-stu-id="8ba17-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="8ba17-148">Aby zobaczyć hello dostępne oferty, za pomocą polecenia Get-AzureRmVMImageSku hello jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="8ba17-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="8ba17-149">Witaj następujące polecenie zawiera wszystkie jednostki SKU, które są dostępne dla hello **SQL2014SP1 WS2012R2** oferty.</span><span class="sxs-lookup"><span data-stu-id="8ba17-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="8ba17-150">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="8ba17-150">Create a resource group</span></span>
<span data-ttu-id="8ba17-151">Z modelu wdrażania usługi Resource Manager hello pierwszy obiekt hello, tworzona jest hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="8ba17-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="8ba17-152">Używamy hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate polecenia cmdlet, grupy zasobów platformy Azure i jej zasobach z zasobem hello grupy nazwy i lokalizacji zdefiniowane przez hello zmiennych, które zostały wcześniej zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="8ba17-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="8ba17-153">Wykonaj następujące polecenie cmdlet toocreate hello nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="8ba17-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="8ba17-154">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="8ba17-154">Create a storage account</span></span>
<span data-ttu-id="8ba17-155">maszyny wirtualnej Hello wymaga zasobów magazynu hello dysku systemu operacyjnego oraz hello danych programu SQL Server i plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="8ba17-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="8ba17-156">Dla uproszczenia utworzymy jednego dysku dla obu.</span><span class="sxs-lookup"><span data-stu-id="8ba17-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="8ba17-157">Możesz dołączyć dodatkowe dyski później za pomocą hello [dysku Azure Dodaj](/powershell/module/azure/add-azuredisk) polecenia cmdlet w kolejności tooplace danych programu SQL Server i pliki dziennika w dedykowanych dysków.</span><span class="sxs-lookup"><span data-stu-id="8ba17-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="8ba17-158">Używamy hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) toocreate polecenia cmdlet magazynu w warstwie standardowa konta w nowej grupy zasobów oraz nazwy konta magazynu hello, nazwa jednostki Sku magazynu i lokalizacja zdefiniowane przy użyciu zmiennych hello wcześniej zainicjowana.</span><span class="sxs-lookup"><span data-stu-id="8ba17-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="8ba17-159">Wykonaj następujące polecenie cmdlet toocreate hello nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8ba17-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="8ba17-160">Utwórz zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="8ba17-160">Create network resources</span></span>
<span data-ttu-id="8ba17-161">Maszyna wirtualna Hello wymaga liczba zasobów sieciowych do obsługi łączności sieciowej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="8ba17-162">Każda maszyna wirtualna wymaga sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="8ba17-163">Sieć wirtualna musi mieć co najmniej jedną podsieć zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="8ba17-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="8ba17-164">Interfejs sieciowy musi być zdefiniowany publiczny lub prywatny adres IP.</span><span class="sxs-lookup"><span data-stu-id="8ba17-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="8ba17-165">Tworzenie konfiguracji podsieci sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8ba17-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="8ba17-166">Firma Microsoft będzie Rozpocznij od utworzenia konfiguracji podsieci dla naszych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="8ba17-167">W naszym samouczku utworzymy podsieci domyślnej przy użyciu hello [AzureRmVirtualNetworkSubnetConfig nowy](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8ba17-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="8ba17-168">Utworzymy naszych konfiguracji podsieci sieci wirtualnej z hello nazwy i adresu prefiks podsieci zdefiniowane przy użyciu hello zmiennych, które zostały wcześniej zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="8ba17-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="8ba17-169">Można zdefiniować dodatkowe właściwości konfiguracji podsieci sieci wirtualnej hello za pomocą tego polecenia cmdlet, ale która wykracza poza zakres tego samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="8ba17-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="8ba17-170">Wykonaj następujące polecenia cmdlet toocreate hello konfiguracji podsieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="8ba17-171">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8ba17-171">Create a virtual network</span></span>
<span data-ttu-id="8ba17-172">Następnie utworzymy naszych sieci wirtualnej przy użyciu hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8ba17-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="8ba17-173">W tej nowej grupy zasobów o nazwie hello, lokalizacji i prefiksu adresu zdefiniowane przy użyciu hello zmiennych, które zostały wcześniej zainicjowane i konfiguracji podsieci hello zdefiniowaną w poprzednim kroku hello utworzymy naszych sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="8ba17-174">Wykonaj następujące polecenia cmdlet toocreate hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="8ba17-175">Utwórz hello publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="8ba17-175">Create hello public IP address</span></span>
<span data-ttu-id="8ba17-176">Teraz, gdy mamy naszych sieci wirtualnej zdefiniowane potrzebujemy tooconfigure adresu IP dla maszyny wirtualnej toohello łączności.</span><span class="sxs-lookup"><span data-stu-id="8ba17-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="8ba17-177">W tym samouczku utworzymy publiczny adres IP za pomocą dynamicznego adresu IP, adresy toosupport łączności z Internetem.</span><span class="sxs-lookup"><span data-stu-id="8ba17-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="8ba17-178">Używamy hello [AzureRmPublicIpAddress nowy](/powershell/module/azurerm.network/new-azurermpublicipaddress) polecenia cmdlet toocreate hello publicznego adresu IP w prevously utworzoną grupę zasobów hello oraz hello nazwy, lokalizacji, Metoda alokacji i etykieta nazwy domeny DNS zdefiniowane przy użyciu hello zmienne, które zostały wcześniej zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="8ba17-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="8ba17-179">Można zdefiniować dodatkowe właściwości hello publicznego adresu IP za pomocą tego polecenia cmdlet, ale która wykracza poza zakres hello tego samouczka początkowej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="8ba17-180">Można również utworzyć za pomocą statycznego adresu prywatny adres lub adres, ale jest to poza zakresem hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="8ba17-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="8ba17-181">Wykonaj następujące polecenie cmdlet toocreate hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="8ba17-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="8ba17-182">Utwórz hello interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="8ba17-182">Create hello network interface</span></span>
<span data-ttu-id="8ba17-183">Teraz możemy toocreate gotowy interfejs sieciowy hello, używanego przez naszych maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="8ba17-184">Używamy hello [AzureRmNetworkInterface nowy](/powershell/module/azurerm.network/new-azurermnetworkinterface) toocreate polecenia cmdlet naszych interfejsu sieciowego w grupie zasobów hello utworzonego wcześniej i o nazwie hello, lokalizacji, podsieci i publicznego adresu IP wcześniej zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="8ba17-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="8ba17-185">Wykonaj następujące polecenia cmdlet toocreate hello interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="8ba17-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="8ba17-186">Konfigurowanie obiektu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8ba17-186">Configure a VM object</span></span>
<span data-ttu-id="8ba17-187">Teraz, gdy mamy magazynu i zasobów sieciowych zdefiniowanych możemy gotowe toodefine zasoby obliczeniowe dla maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="8ba17-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="8ba17-188">W naszym samouczku firma Microsoft będzie określić różne właściwości systemu operacyjnego i hello rozmiar maszyny wirtualnej, określ hello interfejsu sieciowego, który wcześniej utworzony, zdefiniuj magazynu obiektów blob, a następnie określ hello dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ba17-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="8ba17-189">Utwórz hello obiektu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8ba17-189">Create hello VM object</span></span>
<span data-ttu-id="8ba17-190">Firma Microsoft zostanie uruchomiony, określając hello rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="8ba17-191">W tym samouczku będziemy określania DS13.</span><span class="sxs-lookup"><span data-stu-id="8ba17-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="8ba17-192">Używamy hello [AzureRmVMConfig nowy](/powershell/module/azurerm.compute/new-azurermvmconfig) toocreate polecenia cmdlet obiektu można skonfigurować maszyny wirtualnej o nazwie hello i rozmiar zdefiniowane przy użyciu hello zmiennych, które zostały wcześniej zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="8ba17-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="8ba17-193">Wykonaj następujące polecenia cmdlet toocreate hello maszyny wirtualnej obiekt hello.</span><span class="sxs-lookup"><span data-stu-id="8ba17-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="8ba17-194">Utwórz poświadczenia obiektu toohold hello nazwę i hasło dla hello poświadczenia administratora lokalnego</span><span class="sxs-lookup"><span data-stu-id="8ba17-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="8ba17-195">Zanim firma Microsoft można ustawić właściwości systemu operacyjnego hello hello maszyny wirtualnej, potrzebujemy toosupply hello poświadczenia dla konta administratora lokalnego hello jako bezpieczny ciąg.</span><span class="sxs-lookup"><span data-stu-id="8ba17-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="8ba17-196">tooaccomplish, użyjemy hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8ba17-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="8ba17-197">Wykonaj następujące polecenie cmdlet hello i w hello okno żądanie poświadczeń programu Windows PowerShell, wpisz hello toouse nazwę i hasło dla konta administratora lokalnego hello w maszynie wirtualnej Windows hello.</span><span class="sxs-lookup"><span data-stu-id="8ba17-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="8ba17-198">Ustaw właściwości systemu operacyjnego hello hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8ba17-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="8ba17-199">Teraz możemy gotowe tooset hello właściwości maszyny wirtualnej w system operacyjny.</span><span class="sxs-lookup"><span data-stu-id="8ba17-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="8ba17-200">Używamy hello [AzureRmVMOperatingSystem zestaw](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) polecenia cmdlet tooset hello typu systemu operacyjnego Windows, wymagają hello [agenta maszyny wirtualnej](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe zainstalowane, określ to polecenie cmdlet hello umożliwia automatyczne Zaktualizuj i ustawić hello nazwę maszyny wirtualnej, hello nazwy komputera i poświadczeń hello przy użyciu hello zmiennych, które zostały wcześniej zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="8ba17-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="8ba17-201">Wykonanie hello następujące polecenia cmdlet tooset hello systemu operacyjnego właściwości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="8ba17-202">Dodaj maszynę wirtualną toohello hello sieciowych — Interfejs</span><span class="sxs-lookup"><span data-stu-id="8ba17-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="8ba17-203">Następnie dodamy hello interfejsu sieciowego, że utworzono wcześniej toohello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="8ba17-204">Używamy hello [AzureRmVMNetworkInterface Dodaj](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) polecenia cmdlet tooadd hello interfejsu sieciowego przy użyciu zmiennej hello interfejsu sieci, wcześniej zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="8ba17-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="8ba17-205">Wykonanie hello następującego polecenia cmdlet tooset hello sieciowej dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="8ba17-206">Ustaw lokalizację magazynu obiektów blob hello hello toobe dysku używane przez maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="8ba17-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="8ba17-207">Następnie możemy ustawi lokalizację magazynu obiektów blob hello hello toobe dysku używane przez maszynę wirtualną hello za pomocą zmiennych hello, wcześniej zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="8ba17-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="8ba17-208">Wykonanie powitania od lokalizacji magazynu obiektów blob hello tooset polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8ba17-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="8ba17-209">Ustaw właściwości dysku dla maszyny wirtualnej hello hello systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="8ba17-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="8ba17-210">Następnie możemy ustawi systemu operacyjnego hello właściwości dysku dla maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="8ba17-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="8ba17-211">Używamy hello [AzureRmVMOSDisk zestaw](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify polecenia cmdlet, który system operacyjny dla maszyny wirtualnej hello hello będą pobierane z obrazu tooset buforowanie tylko tooread (ponieważ program SQL Server jest instalowany na powitania tego samego dysku) i definiowanie Nazwa maszyny wirtualnej Hello i dysku systemu operacyjnego hello zdefiniowane przy użyciu zmiennych hello zdefiniowanego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="8ba17-212">Wykonanie hello następującego polecenia cmdlet tooset hello właściwości dysku systemu operacyjnego dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="8ba17-213">Określ obraz platformy hello hello maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8ba17-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="8ba17-214">Nasze ostatnim krokiem konfiguracji jest obrazu platformy hello toospecify naszych maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="8ba17-215">W naszym samouczku używamy hello najnowsze obrazu programu SQL Server 2016 CTP.</span><span class="sxs-lookup"><span data-stu-id="8ba17-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="8ba17-216">Używamy hello [AzureRmVMSourceImage zestaw](/powershell/module/azurerm.compute/set-azurermvmsourceimage) toouse polecenia cmdlet tego obrazu zgodnie z definicją w zmiennych hello, wcześniej zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="8ba17-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="8ba17-217">Wykonanie hello następującego polecenia cmdlet toospecify hello platformy obrazu dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="8ba17-218">Utwórz hello maszyny Wirtualnej SQL</span><span class="sxs-lookup"><span data-stu-id="8ba17-218">Create hello SQL VM</span></span>
<span data-ttu-id="8ba17-219">Zakończono hello czynności konfiguracyjne, użytkownik jest maszyny wirtualnej hello toocreate gotowe.</span><span class="sxs-lookup"><span data-stu-id="8ba17-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="8ba17-220">Używamy hello [AzureRmVM nowy](/powershell/module/azurerm.compute/new-azurermvm) polecenia cmdlet toocreate hello maszyny wirtualnej za pomocą zmiennych hello zdefiniowaniu.</span><span class="sxs-lookup"><span data-stu-id="8ba17-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="8ba17-221">Wykonaj następujące polecenia cmdlet toocreate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8ba17-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="8ba17-222">Maszyna wirtualna Hello jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="8ba17-222">hello virtual machine is created.</span></span> <span data-ttu-id="8ba17-223">Powiadomienie, że dla diagnostyki rozruchu utworzeniu konta magazynu w warstwie standardowa ponieważ hello określono konto magazynu dla maszyny wirtualnej hello dysku to konto magazynu premium.</span><span class="sxs-lookup"><span data-stu-id="8ba17-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="8ba17-224">Możesz teraz przeglądać tej maszyny w hello Azure Portal toosee [publicznego adresu IP i nazwy FQDN](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="8ba17-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="8ba17-225">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="8ba17-225">Example script</span></span>
<span data-ttu-id="8ba17-226">Witaj poniższy skrypt zawiera hello wykonania skryptu programu PowerShell na potrzeby tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="8ba17-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="8ba17-227">Przyjęto założenie, że masz już toouse subskrypcji platformy Azure hello Instalatora z hello **Add-AzureRmAccount** i **Select-AzureRmSubscription** poleceń.</span><span class="sxs-lookup"><span data-stu-id="8ba17-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="8ba17-228">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ba17-228">Next steps</span></span>
<span data-ttu-id="8ba17-229">Po utworzeniu maszyny wirtualnej hello jesteś maszyny wirtualnej toohello tooconnect gotowe za pomocą protokołu RDP i ustawienia łączności.</span><span class="sxs-lookup"><span data-stu-id="8ba17-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="8ba17-230">Aby uzyskać więcej informacji, zobacz [połączyć tooa maszyny wirtualnej programu SQL Server na platformie Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8ba17-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

