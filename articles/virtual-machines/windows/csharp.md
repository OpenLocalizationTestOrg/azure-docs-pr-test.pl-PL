---
title: "aaaCreate i zarządzanie nimi Azure maszyny wirtualnej przy użyciu języka C# | Dokumentacja firmy Microsoft"
description: "Toodeploy C# i usługi Azure Resource Manager za pomocą maszyny wirtualnej i wszystkie dodatkowe zasoby."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="58f98-103">Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows na platformie Azure przy użyciu języka C#</span><span class="sxs-lookup"><span data-stu-id="58f98-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="58f98-104">[Maszyny wirtualnej Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM), wymaga kilku obsługi zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="58f98-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="58f98-105">W tym artykule omówiono tworzenia, zarządzania i usuwania zasobów maszyny Wirtualnej przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="58f98-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="58f98-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="58f98-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="58f98-107">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58f98-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="58f98-108">Zainstaluj pakiet hello</span><span class="sxs-lookup"><span data-stu-id="58f98-108">Install hello package</span></span>
> * <span data-ttu-id="58f98-109">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="58f98-109">Create credentials</span></span>
> * <span data-ttu-id="58f98-110">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="58f98-110">Create resources</span></span>
> * <span data-ttu-id="58f98-111">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="58f98-111">Perform management tasks</span></span>
> * <span data-ttu-id="58f98-112">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="58f98-112">Delete resources</span></span>
> * <span data-ttu-id="58f98-113">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="58f98-113">Run hello application</span></span>

<span data-ttu-id="58f98-114">Trwa około 20 minut toodo następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="58f98-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="58f98-115">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58f98-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="58f98-116">Jeśli nie jest jeszcze zainstalować [programu Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="58f98-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="58f98-117">Wybierz **tworzenia klasycznych aplikacji .NET** na hello obciążeń strony, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="58f98-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="58f98-118">W podsumowaniu hello, można stwierdzić, że **narzędzi programistycznych platformy .NET Framework 4 4.6** jest automatycznie wybrana.</span><span class="sxs-lookup"><span data-stu-id="58f98-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="58f98-119">Jeśli zainstalowano program Visual Studio można dodać hello obciążenia .NET przy użyciu hello uruchamiania usługi Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58f98-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="58f98-120">W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="58f98-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="58f98-121">W **szablony** > **Visual C#**, wybierz pozycję **aplikacji konsoli (.NET Framework)**, wprowadź *myDotnetProject* hello nazwy Witaj projektu, zaznacz hello lokalizację projektu hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="58f98-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="58f98-122">Zainstaluj pakiet hello</span><span class="sxs-lookup"><span data-stu-id="58f98-122">Install hello package</span></span>

<span data-ttu-id="58f98-123">Pakiety NuGet są hello najprostszy sposób tooinstall hello biblioteki muszą toofinish następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="58f98-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="58f98-124">tooget hello bibliotek, które należy w programie Visual Studio, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="58f98-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="58f98-125">Kliknij przycisk **narzędzia** > **Menedżera pakietów Nuget**, a następnie kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="58f98-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="58f98-126">Wpisz następujące polecenie w konsoli hello:</span><span class="sxs-lookup"><span data-stu-id="58f98-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="58f98-127">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="58f98-127">Create credentials</span></span>

<span data-ttu-id="58f98-128">Przed rozpoczęciem tego kroku upewnij się, że masz dostęp do tooan [nazwy głównej usługi Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="58f98-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="58f98-129">Należy również zarejestrować identyfikator aplikacji hello, klucz uwierzytelniania hello i identyfikator dzierżawcy hello, które należy w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="58f98-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="58f98-130">Tworzenie pliku autoryzacji hello</span><span class="sxs-lookup"><span data-stu-id="58f98-130">Create hello authorization file</span></span>

1. <span data-ttu-id="58f98-131">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="58f98-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="58f98-132">Nazwa pliku hello *azureauth.properties*, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="58f98-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="58f98-133">Dodaj te właściwości autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="58f98-133">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="58f98-134">Zastąp  **&lt;identyfikator subskrypcji&gt;**  z identyfikatorem subskrypcji  **&lt;identyfikator aplikacji&gt;**  z hello aplikacji usługi Active Directory Identyfikator,  **&lt;klucz uwierzytelniania&gt;**  kluczem aplikacji hello i  **&lt;identyfikator dzierżawcy&gt;**  z dzierżawcą hello Identyfikator.</span><span class="sxs-lookup"><span data-stu-id="58f98-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="58f98-135">Zapisz plik azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="58f98-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="58f98-136">Ustaw zmienną środowiskową systemu Windows o nazwie AZURE_AUTH_LOCATION z hello Pełna ścieżka tooauthorization pliku, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="58f98-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="58f98-137">Na przykład można użyć następującego polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="58f98-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="58f98-138">Utwórz powitania klienta zarządzania</span><span class="sxs-lookup"><span data-stu-id="58f98-138">Create hello management client</span></span>

1. <span data-ttu-id="58f98-139">Otwórz plik Program.cs hello hello projektu, który został utworzony, a następnie dodaj te instrukcje toohello istniejące instrukcje using u góry pliku hello:</span><span class="sxs-lookup"><span data-stu-id="58f98-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="58f98-140">Klient zarządzania hello toocreate, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="58f98-141">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="58f98-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="58f98-142">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="58f98-142">Create hello resource group</span></span>

<span data-ttu-id="58f98-143">Wszystkie zasoby muszą być zawarte w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58f98-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="58f98-144">wartości toospecify hello aplikacji i Utwórz grupę zasobów hello, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="58f98-145">Tworzenie zestawu dostępności hello</span><span class="sxs-lookup"><span data-stu-id="58f98-145">Create hello availability set</span></span>

<span data-ttu-id="58f98-146">[Zestawy dostępności](tutorial-availability-sets.md) ułatwić Ci maszyn wirtualnych hello toomaintain używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="58f98-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="58f98-147">dostępność hello toocreate ustawić, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="58f98-148">Utwórz hello publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="58f98-148">Create hello public IP address</span></span>

<span data-ttu-id="58f98-149">A [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) jest wymagane toocommunicate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="58f98-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="58f98-150">toocreate hello publicznego adresu IP dla maszyny wirtualnej hello, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="58f98-151">Utwórz sieć wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="58f98-151">Create hello virtual network</span></span>

<span data-ttu-id="58f98-152">Maszyna wirtualna musi należeć do podsieci [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="58f98-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="58f98-153">toocreate a podsieci i sieci wirtualnej, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="58f98-154">Utwórz hello interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="58f98-154">Create hello network interface</span></span>

<span data-ttu-id="58f98-155">Maszyna wirtualna musi toocommunicate interfejsu sieciowego, na powitania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="58f98-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="58f98-156">toocreate interfejsu sieciowego, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-156">toocreate a network interface, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="58f98-157">Utwórz maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="58f98-157">Create hello virtual machine</span></span>

<span data-ttu-id="58f98-158">Teraz, gdy utworzono hello wszystkie pomocnicze zasoby, można utworzyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="58f98-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="58f98-159">toocreate hello maszyny wirtualnej, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> <span data-ttu-id="58f98-160">W tym samouczku tworzy maszynę wirtualną z wersją systemu operacyjnego Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="58f98-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="58f98-161">Zobacz toolearn więcej informacji o wybieraniu inne obrazy [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą programu Windows PowerShell i hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58f98-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="58f98-162">Jeśli chcesz toouse istniejącego dysku zamiast obrazu z witryny marketplace, użyj tego kodu:</span><span class="sxs-lookup"><span data-stu-id="58f98-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a><span data-ttu-id="58f98-163">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="58f98-163">Perform management tasks</span></span>

<span data-ttu-id="58f98-164">Podczas cyklu życia hello maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="58f98-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="58f98-165">Ponadto można toocreate kodu tooautomate powtarzających się lub złożonych zadań.</span><span class="sxs-lookup"><span data-stu-id="58f98-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="58f98-166">Jeśli potrzebujesz toodo wszystko w usłudze hello maszyny Wirtualnej, należy tooget wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="58f98-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="58f98-167">Pobierz informacje o hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="58f98-167">Get information about hello VM</span></span>

<span data-ttu-id="58f98-168">tooget informacji o maszynie wirtualnej hello, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a><span data-ttu-id="58f98-169">Zatrzymaj hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="58f98-169">Stop hello VM</span></span>

<span data-ttu-id="58f98-170">Można zatrzymać maszynę wirtualną i zachować wszystkie jego ustawienia, ale nadal toobe naliczona opłata za go lub można zatrzymać maszyny wirtualnej i jej cofnąć.</span><span class="sxs-lookup"><span data-stu-id="58f98-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="58f98-171">Po cofnięciu przydziału maszyny wirtualnej, wszystkie zasoby skojarzone z nim są również zakończenia deallocated i rozliczeń dla niego.</span><span class="sxs-lookup"><span data-stu-id="58f98-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="58f98-172">maszyny wirtualnej hello toostop bez dealokowanie, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="58f98-173">Maszyna wirtualna hello toodeallocate, zmienić kod toothis połączenia PowerOff hello:</span><span class="sxs-lookup"><span data-stu-id="58f98-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="58f98-174">Uruchom hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="58f98-174">Start hello VM</span></span>

<span data-ttu-id="58f98-175">toostart hello maszyny wirtualnej, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="58f98-176">Zmień rozmiar hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="58f98-176">Resize hello VM</span></span>

<span data-ttu-id="58f98-177">Wiele aspektów wdrożenia należy uwzględnić przy podejmowaniu decyzji o rozmiarze dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="58f98-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="58f98-178">Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="58f98-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="58f98-179">rozmiar toochange hello maszyny wirtualnej, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="58f98-180">Dodaj toohello dysku danych maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="58f98-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="58f98-181">tooadd maszyny wirtualnej toohello dysku danych, Dodaj ten kod toohello Main metody tooadd dysku danych o rozmiarze, han jednostki LUN 0 i buforowania rodzaj ReadWrite 2 GB:</span><span class="sxs-lookup"><span data-stu-id="58f98-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="58f98-182">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="58f98-182">Delete resources</span></span>

<span data-ttu-id="58f98-183">Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="58f98-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="58f98-184">Jeśli chcesz maszyn wirtualnych hello toodelete i wszystkich hello obsługi zasobów, wszystkie masz toodo jest grupa zasobów hello delete.</span><span class="sxs-lookup"><span data-stu-id="58f98-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="58f98-185">zasób hello toodelete grupy, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="58f98-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="58f98-186">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="58f98-186">Run hello application</span></span>

<span data-ttu-id="58f98-187">Należy trwa około pięciu minut, zanim ta toorun aplikacji konsoli całkowicie od początku toofinish.</span><span class="sxs-lookup"><span data-stu-id="58f98-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="58f98-188">toorun hello aplikacji konsoli, kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="58f98-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="58f98-189">Przed naciśnięciem przycisku **Enter** toostart usuwanie zasobów, można wykonać kilka minut tooverify hello tworzenia zasobów hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="58f98-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="58f98-190">Kliknij przycisk hello wdrożenia toosee informacje o stanie wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="58f98-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58f98-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="58f98-191">Next steps</span></span>
* <span data-ttu-id="58f98-192">Zalety przy użyciu toocreate szablonu maszyny wirtualnej przy użyciu informacji hello w [wdrożyć maszynę wirtualną platformy Azure przy użyciu języka C# i szablonu usługi Resource Manager](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58f98-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="58f98-193">Dowiedz się więcej o korzystaniu z hello [bibliotek platformy Azure dla platformy .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="58f98-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

