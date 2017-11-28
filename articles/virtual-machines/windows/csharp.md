---
title: "Tworzenie i zarządzanie nimi maszyny wirtualnej platformy Azure przy użyciu języka C# | Dokumentacja firmy Microsoft"
description: "Używanie języka C# i Menedżera zasobów Azure, aby wdrożyć maszynę wirtualną i wszystkie dodatkowe zasoby."
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
ms.openlocfilehash: 5d9021c2f65b70e36d5ea82992c9fb9d2d6d394a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="74a5c-103">Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows na platformie Azure przy użyciu języka C#</span><span class="sxs-lookup"><span data-stu-id="74a5c-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="74a5c-104">[Maszyny wirtualnej Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM), wymaga kilku obsługi zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="74a5c-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="74a5c-105">W tym artykule omówiono tworzenia, zarządzania i usuwania zasobów maszyny Wirtualnej przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="74a5c-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="74a5c-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="74a5c-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74a5c-107">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74a5c-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="74a5c-108">Zainstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="74a5c-108">Install the package</span></span>
> * <span data-ttu-id="74a5c-109">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="74a5c-109">Create credentials</span></span>
> * <span data-ttu-id="74a5c-110">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="74a5c-110">Create resources</span></span>
> * <span data-ttu-id="74a5c-111">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="74a5c-111">Perform management tasks</span></span>
> * <span data-ttu-id="74a5c-112">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="74a5c-112">Delete resources</span></span>
> * <span data-ttu-id="74a5c-113">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="74a5c-113">Run the application</span></span>

<span data-ttu-id="74a5c-114">Wykonaj te kroki trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="74a5c-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="74a5c-115">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74a5c-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="74a5c-116">Jeśli nie jest jeszcze zainstalować [programu Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="74a5c-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="74a5c-117">Wybierz **tworzenia klasycznych aplikacji .NET** na stronie obciążeń, a następnie kliknij **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="74a5c-117">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="74a5c-118">Podsumowując, można stwierdzić, że **narzędzi programistycznych platformy .NET Framework 4 4.6** jest automatycznie wybrana.</span><span class="sxs-lookup"><span data-stu-id="74a5c-118">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="74a5c-119">Jeśli zainstalowano program Visual Studio można dodać obciążenia .NET przy użyciu Uruchom okno programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74a5c-119">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="74a5c-120">W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="74a5c-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="74a5c-121">W **szablony** > **Visual C#**, wybierz pozycję **aplikacji konsoli (.NET Framework)**, wprowadź *myDotnetProject* dla nazwy Projekt, wybierz lokalizację projektu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="74a5c-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-package"></a><span data-ttu-id="74a5c-122">Zainstaluj pakiet</span><span class="sxs-lookup"><span data-stu-id="74a5c-122">Install the package</span></span>

<span data-ttu-id="74a5c-123">Najprostszym sposobem zainstalowania bibliotek, które muszą zakończyć te kroki są pakiety NuGet.</span><span class="sxs-lookup"><span data-stu-id="74a5c-123">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="74a5c-124">Aby uzyskać bibliotek, które należy w programie Visual Studio, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="74a5c-124">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="74a5c-125">Kliknij przycisk **narzędzia** > **Menedżera pakietów Nuget**, a następnie kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="74a5c-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="74a5c-126">W konsoli wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="74a5c-126">Type this command in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="74a5c-127">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="74a5c-127">Create credentials</span></span>

<span data-ttu-id="74a5c-128">Przed rozpoczęciem tego kroku upewnij się, że masz dostęp do [nazwy głównej usługi Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="74a5c-128">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="74a5c-129">Należy również zarejestrować identyfikator aplikacji, klucz uwierzytelniania i Identyfikatora dzierżawy, które są potrzebne w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="74a5c-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="74a5c-130">Tworzenie pliku autoryzacji</span><span class="sxs-lookup"><span data-stu-id="74a5c-130">Create the authorization file</span></span>

1. <span data-ttu-id="74a5c-131">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="74a5c-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="74a5c-132">Nadaj nazwę plikowi *azureauth.properties*, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="74a5c-132">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="74a5c-133">Dodaj te właściwości autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="74a5c-133">Add these authorization properties:</span></span>

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

    <span data-ttu-id="74a5c-134">Zastąp  **&lt;identyfikator subskrypcji&gt;**  z identyfikatorem subskrypcji  **&lt;identyfikator aplikacji&gt;**  z identyfikatorem aplikacji usługi Active Directory  **&lt;klucz uwierzytelniania&gt;**  z klucz aplikacji i  **&lt;identyfikator dzierżawcy&gt;**  przy użyciu identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="74a5c-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="74a5c-135">Zapisz plik azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="74a5c-135">Save the azureauth.properties file.</span></span> 
4. <span data-ttu-id="74a5c-136">Ustaw zmienną środowiskową systemu Windows o nazwie AZURE_AUTH_LOCATION z pełną ścieżkę do pliku autoryzacji, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="74a5c-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created.</span></span> <span data-ttu-id="74a5c-137">Na przykład można użyć następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="74a5c-137">For example, the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-the-management-client"></a><span data-ttu-id="74a5c-138">Tworzenie klienta zarządzania</span><span class="sxs-lookup"><span data-stu-id="74a5c-138">Create the management client</span></span>

1. <span data-ttu-id="74a5c-139">Otwórz plik Program.cs w projekcie, który został utworzony, a następnie dodaj te instrukcje do istniejącej deklaracji using u góry pliku:</span><span class="sxs-lookup"><span data-stu-id="74a5c-139">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="74a5c-140">Aby utworzyć klient zarządzania, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-140">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="74a5c-141">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="74a5c-141">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="74a5c-142">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="74a5c-142">Create the resource group</span></span>

<span data-ttu-id="74a5c-143">Wszystkie zasoby muszą być zawarte w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74a5c-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="74a5c-144">Określ wartości dla aplikacji i utworzyć grupę zasobów, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-144">To specify values for the application and create the resource group, add this code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="74a5c-145">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="74a5c-145">Create the availability set</span></span>

<span data-ttu-id="74a5c-146">[Zestawy dostępności](tutorial-availability-sets.md) ułatwienia obsługi maszyn wirtualnych używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="74a5c-146">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="74a5c-147">Aby utworzyć zbiór dostępności, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-147">To create the availability set, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-the-public-ip-address"></a><span data-ttu-id="74a5c-148">Utwórz publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="74a5c-148">Create the public IP address</span></span>

<span data-ttu-id="74a5c-149">A [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) jest potrzebne do komunikowania się z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="74a5c-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="74a5c-150">Aby utworzyć publiczny adres IP dla maszyny wirtualnej, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-150">To create the public IP address for the virtual machine, add this code to the Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="74a5c-151">Utwórz sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="74a5c-151">Create the virtual network</span></span>

<span data-ttu-id="74a5c-152">Maszyna wirtualna musi należeć do podsieci [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74a5c-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="74a5c-153">Aby utworzyć podsieć i sieć wirtualną, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-153">To create a subnet and a virtual network, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="74a5c-154">Tworzenie interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="74a5c-154">Create the network interface</span></span>

<span data-ttu-id="74a5c-155">Maszyna wirtualna musi komunikować się w sieci wirtualnej do interfejsu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="74a5c-155">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="74a5c-156">Aby utworzyć interfejsu sieciowego, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-156">To create a network interface, add this code to the Main method:</span></span>

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

### <a name="create-the-virtual-machine"></a><span data-ttu-id="74a5c-157">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="74a5c-157">Create the virtual machine</span></span>

<span data-ttu-id="74a5c-158">Teraz, gdy utworzono pomocnicze zasoby, można utworzyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="74a5c-158">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="74a5c-159">Aby utworzyć maszynę wirtualną, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-159">To create the virtual machine, add this code to the Main method:</span></span>

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
> <span data-ttu-id="74a5c-160">W tym samouczku tworzy maszynę wirtualną z wersją systemu operacyjnego Windows Server.</span><span class="sxs-lookup"><span data-stu-id="74a5c-160">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="74a5c-161">Aby dowiedzieć się więcej o wybieraniu innych obrazów, zobacz [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą programu Windows PowerShell i interfejsu wiersza polecenia Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="74a5c-161">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="74a5c-162">Jeśli chcesz użyć istniejącego dysku zamiast obrazu z witryny marketplace, użyj tego kodu:</span><span class="sxs-lookup"><span data-stu-id="74a5c-162">If you want to use an existing disk instead of a marketplace image, use this code:</span></span>

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

## <a name="perform-management-tasks"></a><span data-ttu-id="74a5c-163">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="74a5c-163">Perform management tasks</span></span>

<span data-ttu-id="74a5c-164">Podczas cyklu maszyny wirtualnej można uruchomić zadania zarządzania, takie jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="74a5c-164">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="74a5c-165">Ponadto można utworzyć kod do automatyzowania zadań powtarzających się lub złożonych.</span><span class="sxs-lookup"><span data-stu-id="74a5c-165">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="74a5c-166">Gdy trzeba wykonywać żadnych czynności z maszyną Wirtualną, należy uzyskać wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="74a5c-166">When you need to do anything with the VM, you need to get an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="74a5c-167">Uzyskiwanie informacji o Maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="74a5c-167">Get information about the VM</span></span>

<span data-ttu-id="74a5c-168">Aby uzyskać informacje o maszynie wirtualnej, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-168">To get information about the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Getting information about the virtual machine...");
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
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="stop-the-vm"></a><span data-ttu-id="74a5c-169">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="74a5c-169">Stop the VM</span></span>

<span data-ttu-id="74a5c-170">Należy zatrzymać maszynę wirtualną i zachować wszystkie jego ustawienia, ale nadal naliczane za jej lub można zatrzymać maszyny wirtualnej i jej cofnąć.</span><span class="sxs-lookup"><span data-stu-id="74a5c-170">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="74a5c-171">Po cofnięciu przydziału maszyny wirtualnej, wszystkie zasoby skojarzone z nim są również zakończenia deallocated i rozliczeń dla niego.</span><span class="sxs-lookup"><span data-stu-id="74a5c-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="74a5c-172">Aby zatrzymać maszynę wirtualną bez dealokowanie go, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-172">To stop the virtual machine without deallocating it, add this code to the Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

<span data-ttu-id="74a5c-173">Jeśli chcesz Cofnij Przydział maszyny wirtualnej, należy zmienić wywołanie PowerOff ten kod:</span><span class="sxs-lookup"><span data-stu-id="74a5c-173">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```
vm.Deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="74a5c-174">Uruchom maszynę Wirtualną</span><span class="sxs-lookup"><span data-stu-id="74a5c-174">Start the VM</span></span>

<span data-ttu-id="74a5c-175">Aby uruchomić maszynę wirtualną, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-175">To start the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="74a5c-176">Zmień rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="74a5c-176">Resize the VM</span></span>

<span data-ttu-id="74a5c-177">Wiele aspektów wdrożenia należy uwzględnić przy podejmowaniu decyzji o rozmiarze dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="74a5c-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="74a5c-178">Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="74a5c-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="74a5c-179">Aby zmienić rozmiar maszyny wirtualnej, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-179">To change size of the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="74a5c-180">Dodaj dysk danych do maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="74a5c-180">Add a data disk to the VM</span></span>

<span data-ttu-id="74a5c-181">Aby dodać dysk z danymi do maszyny wirtualnej, Dodaj ten kod do metody Main, aby dodać dysk danych o rozmiarze, han jednostki LUN 0 i buforowania rodzaj ReadWrite 2 GB:</span><span class="sxs-lookup"><span data-stu-id="74a5c-181">To add a data disk to the virtual machine, add this code to the Main method to add a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk to vm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter to delete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="74a5c-182">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="74a5c-182">Delete resources</span></span>

<span data-ttu-id="74a5c-183">Ponieważ naliczane są opłaty za zasoby używane na platformie Azure, zawsze jest dobrym rozwiązaniem, aby usunąć zasoby, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="74a5c-183">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="74a5c-184">Jeśli chcesz usunąć maszyn wirtualnych i pomocnicze zasoby, musisz wykonać będzie usunąć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="74a5c-184">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

<span data-ttu-id="74a5c-185">Aby usunąć grupę zasobów, Dodaj ten kod do metody Main:</span><span class="sxs-lookup"><span data-stu-id="74a5c-185">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="74a5c-186">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="74a5c-186">Run the application</span></span>

<span data-ttu-id="74a5c-187">Zakończ powinno zająć około pięciu minut dla tej aplikacji konsoli uruchomić zupełnie od początku.</span><span class="sxs-lookup"><span data-stu-id="74a5c-187">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="74a5c-188">Aby uruchomić aplikację konsoli, kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="74a5c-188">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="74a5c-189">Przed naciśnięciem przycisku **Enter** zacząć usuwanie zasobów może potrwać kilka minut, aby zweryfikować utworzenie zasobów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="74a5c-189">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="74a5c-190">Kliknij stan wdrożenia, aby wyświetlić informacje o wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="74a5c-190">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74a5c-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="74a5c-191">Next steps</span></span>
* <span data-ttu-id="74a5c-192">Zalety przy użyciu szablonu, aby utworzyć maszynę wirtualną, korzystając z informacji w [wdrożyć maszynę wirtualną platformy Azure przy użyciu języka C# i szablonu usługi Resource Manager](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="74a5c-192">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="74a5c-193">Dowiedz się więcej o korzystaniu z [bibliotek platformy Azure dla platformy .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="74a5c-193">Learn more about using the [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

