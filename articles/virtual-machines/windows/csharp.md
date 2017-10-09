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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows na platformie Azure przy użyciu języka C# #

[Maszyny wirtualnej Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM), wymaga kilku obsługi zasobów platformy Azure. W tym artykule omówiono tworzenia, zarządzania i usuwania zasobów maszyny Wirtualnej przy użyciu języka C#. Omawiane kwestie:

> [!div class="checklist"]
> * Tworzenie projektu programu Visual Studio
> * Zainstaluj pakiet hello
> * Utwórz poświadczenia
> * Tworzenie zasobów
> * Wykonywanie zadań zarządzania
> * Usuwanie zasobów
> * Uruchamianie aplikacji hello

Trwa około 20 minut toodo następujące kroki.

## <a name="create-a-visual-studio-project"></a>Tworzenie projektu programu Visual Studio

1. Jeśli nie jest jeszcze zainstalować [programu Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Wybierz **tworzenia klasycznych aplikacji .NET** na hello obciążeń strony, a następnie kliknij przycisk **zainstalować**. W podsumowaniu hello, można stwierdzić, że **narzędzi programistycznych platformy .NET Framework 4 4.6** jest automatycznie wybrana. Jeśli zainstalowano program Visual Studio można dodać hello obciążenia .NET przy użyciu hello uruchamiania usługi Visual Studio.
2. W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.
3. W **szablony** > **Visual C#**, wybierz pozycję **aplikacji konsoli (.NET Framework)**, wprowadź *myDotnetProject* hello nazwy Witaj projektu, zaznacz hello lokalizację projektu hello, a następnie kliknij przycisk **OK**.

## <a name="install-hello-package"></a>Zainstaluj pakiet hello

Pakiety NuGet są hello najprostszy sposób tooinstall hello biblioteki muszą toofinish następujące kroki. tooget hello bibliotek, które należy w programie Visual Studio, wykonaj następujące kroki:

1. Kliknij przycisk **narzędzia** > **Menedżera pakietów Nuget**, a następnie kliknij przycisk **Konsola Menedżera pakietów**.
2. Wpisz następujące polecenie w konsoli hello:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Utwórz poświadczenia

Przed rozpoczęciem tego kroku upewnij się, że masz dostęp do tooan [nazwy głównej usługi Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Należy również zarejestrować identyfikator aplikacji hello, klucz uwierzytelniania hello i identyfikator dzierżawcy hello, które należy w kolejnym kroku.

### <a name="create-hello-authorization-file"></a>Tworzenie pliku autoryzacji hello

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*. Nazwa pliku hello *azureauth.properties*, a następnie kliknij przycisk **Dodaj**.
2. Dodaj te właściwości autoryzacji:

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

    Zastąp  **&lt;identyfikator subskrypcji&gt;**  z identyfikatorem subskrypcji  **&lt;identyfikator aplikacji&gt;**  z hello aplikacji usługi Active Directory Identyfikator,  **&lt;klucz uwierzytelniania&gt;**  kluczem aplikacji hello i  **&lt;identyfikator dzierżawcy&gt;**  z dzierżawcą hello Identyfikator.

3. Zapisz plik azureauth.properties hello. 
4. Ustaw zmienną środowiskową systemu Windows o nazwie AZURE_AUTH_LOCATION z hello Pełna ścieżka tooauthorization pliku, który został utworzony. Na przykład można użyć następującego polecenia programu PowerShell hello:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Utwórz powitania klienta zarządzania

1. Otwórz plik Program.cs hello hello projektu, który został utworzony, a następnie dodaj te instrukcje toohello istniejące instrukcje using u góry pliku hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. Klient zarządzania hello toocreate, Dodaj ten kod toohello metody Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>Tworzenie zasobów

### <a name="create-hello-resource-group"></a>Utwórz grupę zasobów hello

Wszystkie zasoby muszą być zawarte w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).

wartości toospecify hello aplikacji i Utwórz grupę zasobów hello, Dodaj ten kod toohello metody Main:

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Tworzenie zestawu dostępności hello

[Zestawy dostępności](tutorial-availability-sets.md) ułatwić Ci maszyn wirtualnych hello toomaintain używanych przez aplikację.

dostępność hello toocreate ustawić, Dodaj ten kod toohello metody Main:

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Utwórz hello publicznego adresu IP

A [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) jest wymagane toocommunicate hello maszyny wirtualnej.

toocreate hello publicznego adresu IP dla maszyny wirtualnej hello, Dodaj ten kod toohello metody Main:
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Utwórz sieć wirtualną hello

Maszyna wirtualna musi należeć do podsieci [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).

toocreate a podsieci i sieci wirtualnej, Dodaj ten kod toohello metody Main:

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Utwórz hello interfejsu sieciowego

Maszyna wirtualna musi toocommunicate interfejsu sieciowego, na powitania sieci wirtualnej.

toocreate interfejsu sieciowego, Dodaj ten kod toohello metody Main:

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

### <a name="create-hello-virtual-machine"></a>Utwórz maszynę wirtualną hello

Teraz, gdy utworzono hello wszystkie pomocnicze zasoby, można utworzyć maszyny wirtualnej.

toocreate hello maszyny wirtualnej, Dodaj ten kod toohello metody Main:

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
> W tym samouczku tworzy maszynę wirtualną z wersją systemu operacyjnego Windows Server hello. Zobacz toolearn więcej informacji o wybieraniu inne obrazy [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą programu Windows PowerShell i hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Jeśli chcesz toouse istniejącego dysku zamiast obrazu z witryny marketplace, użyj tego kodu:

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

## <a name="perform-management-tasks"></a>Wykonywanie zadań zarządzania

Podczas cyklu życia hello maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej. Ponadto można toocreate kodu tooautomate powtarzających się lub złożonych zadań.

Jeśli potrzebujesz toodo wszystko w usłudze hello maszyny Wirtualnej, należy tooget wystąpienie:

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Pobierz informacje o hello maszyny Wirtualnej

tooget informacji o maszynie wirtualnej hello, Dodaj ten kod toohello metody Main:

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

### <a name="stop-hello-vm"></a>Zatrzymaj hello maszyny Wirtualnej

Można zatrzymać maszynę wirtualną i zachować wszystkie jego ustawienia, ale nadal toobe naliczona opłata za go lub można zatrzymać maszyny wirtualnej i jej cofnąć. Po cofnięciu przydziału maszyny wirtualnej, wszystkie zasoby skojarzone z nim są również zakończenia deallocated i rozliczeń dla niego.

maszyny wirtualnej hello toostop bez dealokowanie, Dodaj ten kod toohello metody Main:

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Maszyna wirtualna hello toodeallocate, zmienić kod toothis połączenia PowerOff hello:

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Uruchom hello maszyny Wirtualnej

toostart hello maszyny wirtualnej, Dodaj ten kod toohello metody Main:

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Zmień rozmiar hello maszyny Wirtualnej

Wiele aspektów wdrożenia należy uwzględnić przy podejmowaniu decyzji o rozmiarze dla maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych](sizes.md).  

rozmiar toochange hello maszyny wirtualnej, Dodaj ten kod toohello metody Main:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Dodaj toohello dysku danych maszyny Wirtualnej

tooadd maszyny wirtualnej toohello dysku danych, Dodaj ten kod toohello Main metody tooadd dysku danych o rozmiarze, han jednostki LUN 0 i buforowania rodzaj ReadWrite 2 GB:

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Usuwanie zasobów

Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne. Jeśli chcesz maszyn wirtualnych hello toodelete i wszystkich hello obsługi zasobów, wszystkie masz toodo jest grupa zasobów hello delete.

zasób hello toodelete grupy, Dodaj ten kod toohello metody Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Należy trwa około pięciu minut, zanim ta toorun aplikacji konsoli całkowicie od początku toofinish. 

1. toorun hello aplikacji konsoli, kliknij przycisk **Start**.

2. Przed naciśnięciem przycisku **Enter** toostart usuwanie zasobów, można wykonać kilka minut tooverify hello tworzenia zasobów hello w hello portalu Azure. Kliknij przycisk hello wdrożenia toosee informacje o stanie wdrożenia hello.

## <a name="next-steps"></a>Następne kroki
* Zalety przy użyciu toocreate szablonu maszyny wirtualnej przy użyciu informacji hello w [wdrożyć maszynę wirtualną platformy Azure przy użyciu języka C# i szablonu usługi Resource Manager](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Dowiedz się więcej o korzystaniu z hello [bibliotek platformy Azure dla platformy .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

