---
title: "aaaCreate i zarządzanie nimi Java przy użyciu maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Toodeploy Java i usługi Azure Resource Manager za pomocą maszyny wirtualnej i wszystkie dodatkowe zasoby."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="13c4a-103">Tworzenie i zarządzanie maszynami wirtualnymi systemu Windows na platformie Azure przy użyciu języka Java</span><span class="sxs-lookup"><span data-stu-id="13c4a-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="13c4a-104">[Maszyny wirtualnej Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM), wymaga kilku obsługi zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="13c4a-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="13c4a-105">W tym artykule omówiono tworzenia, zarządzania i usuwania zasobów maszyny Wirtualnej przy użyciu języka Java.</span><span class="sxs-lookup"><span data-stu-id="13c4a-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="13c4a-106">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="13c4a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="13c4a-107">Utwórz projekt Maven</span><span class="sxs-lookup"><span data-stu-id="13c4a-107">Create a Maven project</span></span>
> * <span data-ttu-id="13c4a-108">Dodaj zależności</span><span class="sxs-lookup"><span data-stu-id="13c4a-108">Add dependencies</span></span>
> * <span data-ttu-id="13c4a-109">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="13c4a-109">Create credentials</span></span>
> * <span data-ttu-id="13c4a-110">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="13c4a-110">Create resources</span></span>
> * <span data-ttu-id="13c4a-111">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="13c4a-111">Perform management tasks</span></span>
> * <span data-ttu-id="13c4a-112">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="13c4a-112">Delete resources</span></span>
> * <span data-ttu-id="13c4a-113">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="13c4a-113">Run hello application</span></span>

<span data-ttu-id="13c4a-114">Trwa około 20 minut toodo następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="13c4a-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="13c4a-115">Utwórz projekt Maven</span><span class="sxs-lookup"><span data-stu-id="13c4a-115">Create a Maven project</span></span>

1. <span data-ttu-id="13c4a-116">Jeśli jeszcze tego nie zrobiono, zainstaluj [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="13c4a-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="13c4a-117">Zainstaluj [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="13c4a-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="13c4a-118">Utwórz nowy folder i hello projekt:</span><span class="sxs-lookup"><span data-stu-id="13c4a-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="13c4a-119">Dodaj zależności</span><span class="sxs-lookup"><span data-stu-id="13c4a-119">Add dependencies</span></span>

1. <span data-ttu-id="13c4a-120">W obszarze hello `testAzureApp` folder, otwórz hello `pom.xml` i Dodaj konfigurację kompilacji hello zbyt&lt;projektu&gt; tooenable hello Kompilowanie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="13c4a-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="13c4a-121">Dodaj hello zależności, które są potrzebne tooaccess hello zestawu Java SDK usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="13c4a-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="13c4a-122">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="13c4a-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="13c4a-123">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="13c4a-123">Create credentials</span></span>

<span data-ttu-id="13c4a-124">Przed rozpoczęciem tego kroku upewnij się, że masz dostęp do tooan [nazwy głównej usługi Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="13c4a-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="13c4a-125">Należy również zarejestrować identyfikator aplikacji hello, klucz uwierzytelniania hello i identyfikator dzierżawcy hello, które należy w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="13c4a-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="13c4a-126">Tworzenie pliku autoryzacji hello</span><span class="sxs-lookup"><span data-stu-id="13c4a-126">Create hello authorization file</span></span>

1. <span data-ttu-id="13c4a-127">Utwórz plik o nazwie `azureauth.properties` i dodać tych tooit właściwości:</span><span class="sxs-lookup"><span data-stu-id="13c4a-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

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

    <span data-ttu-id="13c4a-128">Zastąp  **&lt;identyfikator subskrypcji&gt;**  z identyfikatorem subskrypcji  **&lt;identyfikator aplikacji&gt;**  z hello aplikacji usługi Active Directory Identyfikator,  **&lt;klucz uwierzytelniania&gt;**  kluczem aplikacji hello i  **&lt;identyfikator dzierżawcy&gt;**  z dzierżawcą hello Identyfikator.</span><span class="sxs-lookup"><span data-stu-id="13c4a-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="13c4a-129">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="13c4a-129">Save hello file.</span></span>
3. <span data-ttu-id="13c4a-130">Ustaw zmienną środowiskową o nazwie AZURE_AUTH_LOCATION w powłoki hello pełną ścieżkę toohello uwierzytelniania pliku.</span><span class="sxs-lookup"><span data-stu-id="13c4a-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="13c4a-131">Utwórz powitania klienta zarządzania</span><span class="sxs-lookup"><span data-stu-id="13c4a-131">Create hello management client</span></span>

1. <span data-ttu-id="13c4a-132">Otwórz hello `App.java` plików w obszarze `src\main\java\com\fabrikam` i upewnij się, że ta instrukcja pakietu jest u góry hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="13c4a-133">W obszarze hello instrukcji pakietu, dodaj je zaimportować instrukcji:</span><span class="sxs-lookup"><span data-stu-id="13c4a-133">Under hello package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="13c4a-134">poświadczenia usługi Active Directory hello toocreate konieczność toomake żądań, Dodaj ten kod toohello głównego metodę hello klasy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="13c4a-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="13c4a-135">Tworzenie zasobów</span><span class="sxs-lookup"><span data-stu-id="13c4a-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="13c4a-136">Utwórz grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="13c4a-136">Create hello resource group</span></span>

<span data-ttu-id="13c4a-137">Wszystkie zasoby muszą być zawarte w [grupy zasobów](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13c4a-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="13c4a-138">wartości toospecify hello aplikacji i Utwórz grupę zasobów hello, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="13c4a-139">Tworzenie zestawu dostępności hello</span><span class="sxs-lookup"><span data-stu-id="13c4a-139">Create hello availability set</span></span>

<span data-ttu-id="13c4a-140">[Zestawy dostępności](tutorial-availability-sets.md) ułatwić Ci maszyn wirtualnych hello toomaintain używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="13c4a-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="13c4a-141">dostępność hello toocreate ustawić, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="13c4a-142">Utwórz hello publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="13c4a-142">Create hello public IP address</span></span>

<span data-ttu-id="13c4a-143">A [publicznego adresu IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) jest wymagane toocommunicate hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13c4a-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="13c4a-144">toocreate hello publicznego adresu IP dla maszyny wirtualnej hello, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="13c4a-145">Utwórz sieć wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="13c4a-145">Create hello virtual network</span></span>

<span data-ttu-id="13c4a-146">Maszyna wirtualna musi należeć do podsieci [sieci wirtualnej](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13c4a-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="13c4a-147">toocreate a podsieci i sieci wirtualnej, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="13c4a-148">Utwórz hello interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="13c4a-148">Create hello network interface</span></span>

<span data-ttu-id="13c4a-149">Maszyna wirtualna musi toocommunicate interfejsu sieciowego, na powitania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13c4a-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="13c4a-150">toocreate interfejsu sieciowego, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="13c4a-151">Utwórz maszynę wirtualną hello</span><span class="sxs-lookup"><span data-stu-id="13c4a-151">Create hello virtual machine</span></span>

<span data-ttu-id="13c4a-152">Teraz, gdy utworzono hello wszystkie pomocnicze zasoby, można utworzyć maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13c4a-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="13c4a-153">toocreate hello maszyny wirtualnej, należy dodać ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="13c4a-154">W tym samouczku tworzy maszynę wirtualną z wersją systemu operacyjnego Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="13c4a-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="13c4a-155">Zobacz toolearn więcej informacji o wybieraniu inne obrazy [Nawigacja i wybierz obrazów maszyny wirtualnej platformy Azure za pomocą programu Windows PowerShell i hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13c4a-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="13c4a-156">Jeśli chcesz toouse istniejącego dysku zamiast obrazu z witryny marketplace, użyj tego kodu:</span><span class="sxs-lookup"><span data-stu-id="13c4a-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="13c4a-157">Wykonywanie zadań zarządzania</span><span class="sxs-lookup"><span data-stu-id="13c4a-157">Perform management tasks</span></span>

<span data-ttu-id="13c4a-158">Podczas cyklu życia hello maszyny wirtualnej może być toorun zadań zarządzania, takich jak uruchamianie, zatrzymywanie lub usuwanie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13c4a-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="13c4a-159">Ponadto można toocreate kodu tooautomate powtarzających się lub złożonych zadań.</span><span class="sxs-lookup"><span data-stu-id="13c4a-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="13c4a-160">Jeśli potrzebujesz toodo wszystko w usłudze hello maszyny Wirtualnej, należy tooget wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="13c4a-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="13c4a-161">Dodaj ten blok try toohello kodu metody main hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="13c4a-162">Pobierz informacje o hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="13c4a-162">Get information about hello VM</span></span>

<span data-ttu-id="13c4a-163">tooget informacji o maszynie wirtualnej hello, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="13c4a-164">Zatrzymaj hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="13c4a-164">Stop hello VM</span></span>

<span data-ttu-id="13c4a-165">Można zatrzymać maszynę wirtualną i zachować wszystkie jego ustawienia, ale nadal toobe naliczona opłata za go lub można zatrzymać maszyny wirtualnej i jej cofnąć.</span><span class="sxs-lookup"><span data-stu-id="13c4a-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="13c4a-166">Po cofnięciu przydziału maszyny wirtualnej, wszystkie zasoby skojarzone z nim są również zakończenia deallocated i rozliczeń dla niego.</span><span class="sxs-lookup"><span data-stu-id="13c4a-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="13c4a-167">maszyny wirtualnej hello toostop bez dealokowanie, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="13c4a-168">Maszyna wirtualna hello toodeallocate, zmienić kod toothis połączenia PowerOff hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="13c4a-169">Uruchom hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="13c4a-169">Start hello VM</span></span>

<span data-ttu-id="13c4a-170">toostart hello maszyny wirtualnej, należy dodać ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="13c4a-171">Zmień rozmiar hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="13c4a-171">Resize hello VM</span></span>

<span data-ttu-id="13c4a-172">Wiele aspektów wdrożenia należy uwzględnić przy podejmowaniu decyzji o rozmiarze dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13c4a-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="13c4a-173">Aby uzyskać więcej informacji, zobacz [rozmiarów maszyn wirtualnych](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="13c4a-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="13c4a-174">toochange rozmiar maszyny wirtualnej hello, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="13c4a-175">Dodaj toohello dysku danych maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="13c4a-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="13c4a-176">tooadd maszyny wirtualnej toohello dysku danych, który wynosi 2 GB, rozmiar, ma numer LUN 0 i buforowania typu ReadWrite, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="13c4a-177">Usuwanie zasobów</span><span class="sxs-lookup"><span data-stu-id="13c4a-177">Delete resources</span></span>

<span data-ttu-id="13c4a-178">Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="13c4a-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="13c4a-179">Jeśli chcesz maszyn wirtualnych hello toodelete i wszystkich hello obsługi zasobów, wszystkie masz toodo jest grupa zasobów hello delete.</span><span class="sxs-lookup"><span data-stu-id="13c4a-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="13c4a-180">zasób hello toodelete grupy, Dodaj ten blok try toohello kod w metodzie głównego hello:</span><span class="sxs-lookup"><span data-stu-id="13c4a-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="13c4a-181">Zapisz plik App.java hello.</span><span class="sxs-lookup"><span data-stu-id="13c4a-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="13c4a-182">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="13c4a-182">Run hello application</span></span>

<span data-ttu-id="13c4a-183">Należy trwa około pięciu minut, zanim ta toorun aplikacji konsoli całkowicie od początku toofinish.</span><span class="sxs-lookup"><span data-stu-id="13c4a-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="13c4a-184">toorun hello aplikacji, użyj tego polecenia Maven:</span><span class="sxs-lookup"><span data-stu-id="13c4a-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="13c4a-185">Przed naciśnięciem przycisku **Enter** toostart usuwanie zasobów, można wykonać kilka minut tooverify hello tworzenia zasobów hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="13c4a-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="13c4a-186">Kliknij przycisk hello wdrożenia toosee informacje o stanie wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="13c4a-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="13c4a-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13c4a-187">Next steps</span></span>
* <span data-ttu-id="13c4a-188">Dowiedz się więcej o korzystaniu z hello [bibliotek platformy Azure dla języka Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="13c4a-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

