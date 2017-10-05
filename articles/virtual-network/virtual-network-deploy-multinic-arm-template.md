---
title: "Utwórz maszynę Wirtualną z wieloma kartami sieciowymi — szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu szablonu usługi Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85bfa264c6cf2b0586816a47b3ab72f3aee8ec96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="92970-103">Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="92970-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="92970-104">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="92970-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="92970-105">Ten artykuł dotyczy używania modelu wdrażania usługi Resource Manager zalecanego przez firmę Microsoft w przypadku większości nowych wdrożeń zamiast [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="92970-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="92970-106">Poniższe kroki Użyj grupy zasobów o nazwie *IaaSStory* dla serwerów sieci WEB i grupy zasobów o nazwie *IaaSStory zaplecza* dla serwerów baz danych.</span><span class="sxs-lookup"><span data-stu-id="92970-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92970-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="92970-107">Prerequisites</span></span>
<span data-ttu-id="92970-108">Przed utworzeniem serwerów bazy danych, należy utworzyć *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby dotyczące tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="92970-108">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="92970-109">Aby utworzyć tych zasobów, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="92970-109">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="92970-110">Przejdź do [strony szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="92970-110">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="92970-111">Na stronie szablonu z prawej strony **grupy zasobów nadrzędnej**, kliknij przycisk **wdrażanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="92970-111">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="92970-112">W razie potrzeby zmień wartości parametrów, a następnie wykonaj kroki w portalu Azure w wersji zapoznawczej, aby wdrożyć grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="92970-112">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92970-113">Upewnij się, że nazwy konta magazynu są unikatowe.</span><span class="sxs-lookup"><span data-stu-id="92970-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="92970-114">Nie może mieć nazwy konta magazynu zduplikowanych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="92970-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-the-deployment-template"></a><span data-ttu-id="92970-115">Zrozumienie szablonu wdrożenia</span><span class="sxs-lookup"><span data-stu-id="92970-115">Understand the deployment template</span></span>
<span data-ttu-id="92970-116">Przed przystąpieniem do wdrażania szablonu dostarczanego z tej dokumentacji, upewnij się, że rozumiesz, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="92970-116">Before you deploy the template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="92970-117">W poniższych krokach przedstawiono omówienie szablonu:</span><span class="sxs-lookup"><span data-stu-id="92970-117">The following steps provide a good overview of the template:</span></span>

1. <span data-ttu-id="92970-118">Przejdź do [strony szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="92970-118">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="92970-119">Kliknij przycisk **azuredeploy.json** można otworzyć pliku szablonu.</span><span class="sxs-lookup"><span data-stu-id="92970-119">Click **azuredeploy.json** to open the template file.</span></span>
3. <span data-ttu-id="92970-120">Powiadomienie *osType* parametrów wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="92970-120">Notice the *osType* parameter listed below.</span></span> <span data-ttu-id="92970-121">Ten parametr jest używany do wybierania obrazów maszyny Wirtualnej serwera bazy danych, wraz z wielu systemów operacyjnych powiązane ustawienia.</span><span class="sxs-lookup"><span data-stu-id="92970-121">This parameter is used to select what VM image to use for the database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS to use for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="92970-122">Przewiń w dół listę zmiennych i sprawdź definicję **dbVMSetting** zmienne wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="92970-122">Scroll down to the list of variables, and check the definition for the **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="92970-123">Odbiera jeden z elementów tablicy zawarte w **dbVMSettings** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="92970-123">It receives one of the array elements contained in the **dbVMSettings** variable.</span></span> <span data-ttu-id="92970-124">Jeśli znasz terminologii rozwoju oprogramowania, możesz wyświetlić **dbVMSettings** zmiennej jako tablicy skrótów lub w słowniku.</span><span class="sxs-lookup"><span data-stu-id="92970-124">If you are familiar with software development terminology, you can view the **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="92970-125">Załóżmy, że użytkownik chce wdrożyć maszyn wirtualnych systemu Windows, programem SQL w wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="92970-125">Suppose you decide to deploy Windows VMs running SQL in the back-end.</span></span> <span data-ttu-id="92970-126">Następnie wartość **osType** będzie *Windows*i **dbVMSetting** zmiennej może zawierać elementu wymienione poniżej, co stanowi pierwszą wartość **dbVMSettings** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="92970-126">Then the value for **osType** would be *Windows*, and the **dbVMSetting** variable would contain the element listed below, which represents the first value in the **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="92970-127">Powiadomienie **vmSize** zawiera wartość *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="92970-127">Notice the **vmSize** contains the value *Standard_DS3*.</span></span> <span data-ttu-id="92970-128">Niektórych rozmiarów maszyn wirtualnych umożliwiają korzystanie z wielu kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="92970-128">Only certain VM sizes allow for the use of multiple NICs.</span></span> <span data-ttu-id="92970-129">Możesz sprawdzić rozmiarów maszyn wirtualnych, które obsługują wiele kart sieciowych, odczytując [rozmiarów maszyn wirtualnych systemu Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [rozmiarów maszyn wirtualnych systemu Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykułów.</span><span class="sxs-lookup"><span data-stu-id="92970-129">You can verify which VM sizes support multiple NICs by reading the [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="92970-130">Przewiń w dół do **zasobów** i zwróć uwagę, pierwszego elementu.</span><span class="sxs-lookup"><span data-stu-id="92970-130">Scroll down to **resources** and notice the first element.</span></span> <span data-ttu-id="92970-131">Opisuje konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="92970-131">It describes a storage account.</span></span> <span data-ttu-id="92970-132">To konto magazynu będzie używane do obsługi dysków danych używany przez każdą bazę danych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="92970-132">This storage account will be used to maintain the data disks used by each database VM.</span></span> <span data-ttu-id="92970-133">W tym scenariuszu każda baza danych maszyny Wirtualnej ma dysku systemu operacyjnego przechowywanego w regularnych magazynu oraz dwóch dysków danych przechowywanych w magazynie SSD (premium).</span><span class="sxs-lookup"><span data-stu-id="92970-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="92970-134">Przewiń w dół do następnego zasobu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="92970-134">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="92970-135">Ten zasób reprezentuje używane do dostępu do bazy danych w każdej bazie danych maszyny Wirtualnej karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="92970-135">This resource represents the NIC used for database access in each database VM.</span></span> <span data-ttu-id="92970-136">Zwróć uwagę na **kopiowania** funkcji w przypadku tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="92970-136">Notice the use of the **copy** function in this resource.</span></span> <span data-ttu-id="92970-137">Ten szablon umożliwia wdrażanie jako wiele maszyn wirtualnych można dowolnie na podstawie **dbCount** parametru.</span><span class="sxs-lookup"><span data-stu-id="92970-137">The template allows you to deploy as many VMs as you want, based on the **dbCount** parameter.</span></span> <span data-ttu-id="92970-138">Dlatego należy utworzyć tę samą wartość, kart sieciowych dla dostępu do bazy danych, po jednej dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="92970-138">Therefore you need to create the same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="92970-139">Przewiń w dół do następnego zasobu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="92970-139">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="92970-140">Ten zasób reprezentuje używany do zarządzania w każdej bazie danych maszyny Wirtualnej karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="92970-140">This resource represents the NIC used for management in each database VM.</span></span> <span data-ttu-id="92970-141">Ponownie potrzebujesz jednego z tych kart sieciowych dla każdej maszyny Wirtualnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92970-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="92970-142">Powiadomienie **grupy networkSecurityGroup** element NSG, która zezwala na dostęp do protokołu RDP/SSH do tej karty Sieciowej tylko połączeń.</span><span class="sxs-lookup"><span data-stu-id="92970-142">Notice the **networkSecurityGroup** element, linking an NSG that allows access to RDP/SSH to this NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="92970-143">Przewiń w dół do następnego zasobu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="92970-143">Scroll down to the next resource, as listed below.</span></span> <span data-ttu-id="92970-144">Ten zasób reprezentuje zbiór być współużytkowane przez wszystkie maszyny wirtualne z bazy danych dostępności.</span><span class="sxs-lookup"><span data-stu-id="92970-144">This resource represents an availability set to be shared by all database VMs.</span></span> <span data-ttu-id="92970-145">W ten sposób można zagwarantować, że zawsze będzie jedna maszyna wirtualna w zestawie uruchomiony podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="92970-145">That way, you guarantee that there will always be one VM in the set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="92970-146">Przewiń w dół do następnego zasobu.</span><span class="sxs-lookup"><span data-stu-id="92970-146">Scroll down to the next resource.</span></span> <span data-ttu-id="92970-147">Ten zasób reprezentuje bazy danych maszyn wirtualnych, jak pokazano w pierwszym kilka wierszy wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="92970-147">This resource represents the database VMs, as seen in the first few lines listed below.</span></span> <span data-ttu-id="92970-148">Zwróć uwagę na **kopiowania** funkcji ponownie, zapewniając, że wiele maszyn wirtualnych są tworzone na podstawie **dbCount** parametru.</span><span class="sxs-lookup"><span data-stu-id="92970-148">Notice the use of the **copy** function again, ensuring that multiple VMs are created based on the **dbCount** parameter.</span></span> <span data-ttu-id="92970-149">Ponadto **dependsOn** kolekcji.</span><span class="sxs-lookup"><span data-stu-id="92970-149">Also notice the **dependsOn** collection.</span></span> <span data-ttu-id="92970-150">Wyświetlane są dwie karty sieciowe są niezbędne do utworzenia przed wdrożeniem maszyny Wirtualnej, wraz z zestawu dostępności i konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="92970-150">It lists two NICs being necessary to be created before the VM is deployed, along with the availability set, and the storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="92970-151">Przewiń w dół w zasobu maszyny Wirtualnej do **networkProfile** elementu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="92970-151">Scroll down in the VM resource to the **networkProfile** element, as listed below.</span></span> <span data-ttu-id="92970-152">Zwróć uwagę, że istnieją dwie karty sieciowe są odwołania dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="92970-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="92970-153">Podczas tworzenia wielu kart sieciowych maszyny wirtualnej, należy ustawić **głównej** właściwości jednej z kart sieciowych do *true*, a reszta do *false*.</span><span class="sxs-lookup"><span data-stu-id="92970-153">When you create multiple NICs for a VM, you must set the **primary** property of one of the NICs to *true*, and the rest to *false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="92970-154">Wdrażanie szablonu ARM przy użyciu metody „kliknij, aby wdrożyć”</span><span class="sxs-lookup"><span data-stu-id="92970-154">Deploy the ARM template by using click to deploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92970-155">Wykonaj [wstępne](#Pre-requisites) kroki przed zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="92970-155">Make sure you follow the [pre-requisites](#Pre-requisites) steps before following the instructions below.</span></span>
> 

<span data-ttu-id="92970-156">Przykładowy szablon dostępny w repozytorium publicznym korzysta z pliku parametrów zawierającego wartości domyślne używane do generowania scenariusza opisanego powyżej.</span><span class="sxs-lookup"><span data-stu-id="92970-156">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="92970-157">Aby wdrożyć tego szablonu można wdrożyć przy użyciu kliknij przycisk, wykonaj [to łącze](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), z prawej strony **grupy zasobów w wewnętrznej bazie danych (zobacz dokumentację)** kliknij **wdrażanie na platformie Azure**, Zastąp domyślne wartości parametrów, jeśli to konieczne i postępuj zgodnie z instrukcjami w portalu.</span><span class="sxs-lookup"><span data-stu-id="92970-157">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), to the right of **Backend resource group (see documentation)** click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

<span data-ttu-id="92970-158">Na poniższym rysunku przedstawiono zawartość nową grupę zasobów, po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="92970-158">The figure below shows the contents of the new resource group, after deployment.</span></span>

![Wewnętrzna grupa zasobów](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="92970-160">Wdrażanie szablonu przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="92970-160">Deploy the template by using PowerShell</span></span>
<span data-ttu-id="92970-161">Aby wdrożyć szablon został pobrany przy użyciu programu PowerShell, instalowanie i konfigurowanie programu PowerShell, wykonując kroki opisane w [Instalowanie i konfigurowanie programu PowerShell](/powershell/azure/overview) artykuł, a następnie wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="92970-161">To deploy the template you downloaded by using PowerShell, install and configure PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article and then complete the following steps:</span></span>

<span data-ttu-id="92970-162">Uruchom  **`New-AzureRmResourceGroup`**  polecenia cmdlet, aby utworzyć grupę zasobów, przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="92970-162">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="92970-163">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="92970-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="92970-164">Wdrażanie szablonu przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="92970-164">Deploy the template by using the Azure CLI</span></span>
<span data-ttu-id="92970-165">Aby wdrożyć szablon przy użyciu interfejsu wiersza polecenia platformy Azure, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="92970-165">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="92970-166">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz artykuł [Instalowanie i konfigurowania interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) i postępuj zgodnie z instrukcjami aż do punktu, w którym należy wybrać konto platformy Azure i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="92970-166">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="92970-167">Uruchom polecenie **`azure config mode`**, aby włączyć tryb Resource Manager, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="92970-167">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="92970-168">Oczekiwane dane wyjściowe są następujące:</span><span class="sxs-lookup"><span data-stu-id="92970-168">The expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="92970-169">Otwórz [pliku parametrów](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), zaznacz zawartością i zapisać go w pliku na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="92970-169">Open the [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="92970-170">W tym przykładzie zapisaliśmy plik parametrów w pliku *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="92970-170">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="92970-171">Uruchom polecenie cmdlet **`azure group deployment create`**, aby wdrożyć nową sieć wirtualną przy użyciu uprzednio pobranego i zmodyfikowanego pliku szablonu i pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="92970-171">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="92970-172">Lista wyświetlana po danych wyjściowych zawiera opis używanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="92970-172">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="92970-173">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="92970-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

