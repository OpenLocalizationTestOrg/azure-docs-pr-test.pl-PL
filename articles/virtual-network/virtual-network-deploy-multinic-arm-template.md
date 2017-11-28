---
title: "aaaCreate Maszynę wirtualną z wieloma kartami sieciowymi — szablonu usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="c758e-103">Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="c758e-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c758e-104">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c758e-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c758e-105">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c758e-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="c758e-106">Witaj następujące kroki Użyj grupy zasobów o nazwie *IaaSStory* hello serwerów sieci WEB oraz grupę zasobów o nazwie *IaaSStory zaplecza* dla serwerów hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c758e-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c758e-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c758e-107">Prerequisites</span></span>
<span data-ttu-id="c758e-108">Przed utworzeniem hello serwerów bazy danych, należy toocreate hello *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby hello w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="c758e-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="c758e-109">ukończenie tych zasobów, toocreate hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c758e-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="c758e-110">Przejdź za[strony szablonu hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="c758e-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="c758e-111">Na stronie szablon hello toohello po prawej **nadrzędnej grupy zasobów**, kliknij przycisk **wdrażanie tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="c758e-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="c758e-112">W razie potrzeby zmień wartości parametrów hello, a następnie wykonaj kroki hello w grupie zasobów hello toodeploy portalu Azure w wersji zapoznawczej hello.</span><span class="sxs-lookup"><span data-stu-id="c758e-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c758e-113">Upewnij się, że nazwy konta magazynu są unikatowe.</span><span class="sxs-lookup"><span data-stu-id="c758e-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="c758e-114">Nie może mieć nazwy konta magazynu zduplikowanych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c758e-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="c758e-115">Zrozumienie hello Szablon wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c758e-115">Understand hello deployment template</span></span>
<span data-ttu-id="c758e-116">Przed przystąpieniem do wdrażania szablonu hello wyposażone w tej dokumentacji, upewnij się, że rozumiesz, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="c758e-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="c758e-117">Witaj, wykonaj czynności zawierają omówienie hello szablonu:</span><span class="sxs-lookup"><span data-stu-id="c758e-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="c758e-118">Przejdź za[strony szablonu hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="c758e-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="c758e-119">Kliknij przycisk **azuredeploy.json** tooopen hello szablon pliku.</span><span class="sxs-lookup"><span data-stu-id="c758e-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="c758e-120">Powiadomienie hello *osType* parametrów wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="c758e-121">Ten parametr jest używany tooselect ustawienia powiązane z jakiego toouse obrazu maszyny Wirtualnej na powitania serwera bazy danych, wraz z wielu systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c758e-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="c758e-122">Przewiń w dół listę zmiennych toohello i sprawdź definicję hello hello **dbVMSetting** zmienne wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="c758e-123">Jeden z elementów tablicy hello zawarte w hello odbierze **dbVMSettings** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="c758e-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="c758e-124">Jeśli znasz terminologii rozwoju oprogramowania, możesz wyświetlić hello **dbVMSettings** zmiennej jako tablicy skrótów lub w słowniku.</span><span class="sxs-lookup"><span data-stu-id="c758e-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="c758e-125">Załóżmy, że zdecydujesz maszyn wirtualnych systemu Windows toodeploy programem SQL w wewnętrznej hello.</span><span class="sxs-lookup"><span data-stu-id="c758e-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="c758e-126">Następnie hello wartość **osType** będzie *Windows*i hello **dbVMSetting** zmiennej może zawierać element hello wymienione poniżej, który reprezentuje hello pierwsza wartość hello **dbVMSettings** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="c758e-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

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

6. <span data-ttu-id="c758e-127">Powiadomienie hello **vmSize** zawiera wartość hello *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="c758e-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="c758e-128">Niektórych rozmiarów maszyn wirtualnych umożliwiają hello korzystanie z wielu kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="c758e-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="c758e-129">Możesz sprawdzić rozmiarów maszyn wirtualnych, które obsługują wiele kart sieciowych, odczytując hello [rozmiarów maszyn wirtualnych systemu Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [rozmiarów maszyn wirtualnych systemu Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykułów.</span><span class="sxs-lookup"><span data-stu-id="c758e-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="c758e-130">Przewiń w dół za**zasobów** i powiadomienia hello pierwszego elementu.</span><span class="sxs-lookup"><span data-stu-id="c758e-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="c758e-131">Opisuje konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c758e-131">It describes a storage account.</span></span> <span data-ttu-id="c758e-132">To konto magazynu będzie używane przez każdą bazę danych maszyny Wirtualnej dysków z danymi hello toomaintain używane.</span><span class="sxs-lookup"><span data-stu-id="c758e-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="c758e-133">W tym scenariuszu każda baza danych maszyny Wirtualnej ma dysku systemu operacyjnego przechowywanego w regularnych magazynu oraz dwóch dysków danych przechowywanych w magazynie SSD (premium).</span><span class="sxs-lookup"><span data-stu-id="c758e-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

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

8. <span data-ttu-id="c758e-134">Przewiń w dół toohello następnego zasobu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="c758e-135">Ten zasób reprezentuje hello używane dla dostępu do bazy danych w każdej bazie danych maszyny Wirtualnej karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="c758e-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="c758e-136">Użycie hello powiadomienia hello **kopiowania** funkcji w przypadku tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c758e-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="c758e-137">Szablon Hello pozwala toodeploy jako wiele maszyn wirtualnych można dowolnie na podstawie hello **dbCount** parametru.</span><span class="sxs-lookup"><span data-stu-id="c758e-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="c758e-138">W związku z tym należy toocreate hello samo kart sieciowych dla dostępu do bazy danych, po jednej dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c758e-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

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

9. <span data-ttu-id="c758e-139">Przewiń w dół toohello następnego zasobu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="c758e-140">Ten zasób reprezentuje hello używanego przez kartę Sieciową do zarządzania w każdej bazie danych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c758e-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="c758e-141">Ponownie potrzebujesz jednego z tych kart sieciowych dla każdej maszyny Wirtualnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c758e-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="c758e-142">Powiadomienie hello **grupy networkSecurityGroup** element łączenie umożliwiająca dostęp toothis tooRDP/SSH kart interfejsu Sieciowego tylko grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="c758e-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

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

10. <span data-ttu-id="c758e-143">Przewiń w dół toohello następnego zasobu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="c758e-144">Ten zasób reprezentuje toobe zestaw dostępności współużytkowane przez wszystkie bazy danych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c758e-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="c758e-145">W ten sposób można zagwarantować, że zawsze będzie jedna maszyna wirtualna w hello ustawić uruchamianie w trakcie konserwacji.</span><span class="sxs-lookup"><span data-stu-id="c758e-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

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

11. <span data-ttu-id="c758e-146">Przewiń w dół toohello następnego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c758e-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="c758e-147">Ten zasób reprezentuje hello bazy danych maszyn wirtualnych, jak pokazano w hello pierwszych kilku wierszy wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="c758e-148">Użycie hello powiadomienia hello **kopiowania** ponownie działać, zapewniając, że wiele maszyn wirtualnych są tworzone w oparciu hello **dbCount** parametru.</span><span class="sxs-lookup"><span data-stu-id="c758e-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="c758e-149">Ponadto hello **dependsOn** kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c758e-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="c758e-150">Wyświetlane są dwie karty sieciowe są niezbędne toobe utworzone przed powitalne maszyna wirtualna jest wdrożona, wraz z zestawu dostępności hello i hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c758e-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

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

12. <span data-ttu-id="c758e-151">Przewiń w dół w toohello zasobów maszyny Wirtualnej hello **networkProfile** elementu wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="c758e-152">Zwróć uwagę, że istnieją dwie karty sieciowe są odwołania dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c758e-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="c758e-153">Podczas tworzenia wielu kart sieciowych maszyny wirtualnej, należy ustawić hello **głównej** właściwość hello karty sieciowe za*true*, i hello rest zbyt*false*.</span><span class="sxs-lookup"><span data-stu-id="c758e-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

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

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="c758e-154">Wdrażanie szablonu ARM hello przy użyciu kliknij toodeploy</span><span class="sxs-lookup"><span data-stu-id="c758e-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c758e-155">Upewnij się, że wykonaj hello [wstępne](#Pre-requisites) kroki przed wykonaniem instrukcji hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="c758e-156">Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="c758e-157">toodeploy przy użyciu tego szablonu kliknij toodeploy, postępuj zgodnie z [to łącze](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello po prawej **grupy zasobów w wewnętrznej bazie danych (zobacz dokumentację)** kliknij **wdrażanie tooAzure**, Zastąp Witaj domyślne wartości parametrów, jeśli to konieczne i wykonaj instrukcje hello w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="c758e-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="c758e-158">na poniższej ilustracji Hello przedstawiona zawartość hello hello nową grupę zasobów, po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="c758e-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![Wewnętrzna grupa zasobów](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="c758e-160">Wdrażanie szablonu hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c758e-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="c758e-161">toodeploy hello szablon został pobrany przy użyciu programu PowerShell, instalowanie i konfigurowanie programu PowerShell, wykonując kroki hello hello [Instalowanie i konfigurowanie programu PowerShell](/powershell/azure/overview) artykuł, a następnie ukończ hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c758e-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="c758e-162">Uruchom hello  **`New-AzureRmResourceGroup`**  toocreate polecenia cmdlet, grupy zasobów przy użyciu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="c758e-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="c758e-163">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c758e-163">Expected output:</span></span>

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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="c758e-164">Wdrażanie szablonu hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c758e-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="c758e-165">Szablon hello toodeploy za pomocą hello wiersza polecenia platformy Azure, wykonaj kroki hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="c758e-166">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c758e-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c758e-167">Uruchom hello  **`azure config mode`**  tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c758e-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="c758e-168">Witaj oczekiwane dane wyjściowe w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c758e-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="c758e-169">Otwórz hello [pliku parametrów](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), zaznacz zawartością i zapisz go tooa plik na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="c758e-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="c758e-170">Na przykład zapisaliśmy hello pliku parametrów, za*parameters.JSON następującym kodem*.</span><span class="sxs-lookup"><span data-stu-id="c758e-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="c758e-171">Uruchom hello  **`azure group deployment create`**  hello toodeploy polecenia cmdlet nowej sieci wirtualnej przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego.</span><span class="sxs-lookup"><span data-stu-id="c758e-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="c758e-172">Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.</span><span class="sxs-lookup"><span data-stu-id="c758e-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="c758e-173">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c758e-173">Expected output:</span></span>
   
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

