# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="cc4f4-101">Za pomocą Managed dysków w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cc4f4-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="cc4f4-102">Ten dokument przeprowadzi Cię przez różnice między zarządzanymi i niezarządzanymi dysków przy użyciu szablonów usługi Azure Resource Manager na umieszczanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-102">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="cc4f4-103">Umożliwi to aktualizowanie istniejących szablonów, które korzystają z dysków niezarządzanych do zarządzanych dysków.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-103">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="cc4f4-104">Odwołania, jest używany [101 maszyny wirtualnej — prosty — windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) szablonu jako przewodnika.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-104">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="cc4f4-105">Widać szablon przy użyciu zarówno [dyskach zarządzanych](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) i przy użyciu poprzedniej wersji [niezarządzanych dysków](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) Jeśli chcesz bezpośrednio porównywać.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-105">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="cc4f4-106">Niezarządzane formatowania szablonu dysków</span><span class="sxs-lookup"><span data-stu-id="cc4f4-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="cc4f4-107">Aby rozpocząć, firma Microsoft zapoznaj się z informacjami w sposób niezarządzany dyski są wdrażane.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-107">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="cc4f4-108">Podczas tworzenia dysków niezarządzane, potrzebujesz konta magazynu do przechowywania plików wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-108">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="cc4f4-109">Możesz utworzyć nowe konto magazynu lub użyć już istniejącego.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="cc4f4-110">W tym artykule opisano sposób tworzenia nowego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-110">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="cc4f4-111">W tym celu należy zasób konta magazynu w bloku zasobów, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-111">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="cc4f4-112">W obiekcie maszyny wirtualnej potrzebujemy zależności na koncie magazynu, aby upewnić się, że został utworzony przed maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-112">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="cc4f4-113">W ramach `storageProfile` sekcji możemy następnie określ pełny identyfikator URI lokalizacji wirtualnego dysku twardego, który odwołuje się do konta magazynu i jest wymagany dla dysku systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-113">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="cc4f4-114">Zarządzane formatowania szablonu dysków</span><span class="sxs-lookup"><span data-stu-id="cc4f4-114">Managed disks template formatting</span></span>

<span data-ttu-id="cc4f4-115">W przypadku dysków zarządzanych Azure dysk staje się zasobem najwyższego poziomu i nie wymaga już konto magazynu ma zostać utworzony przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-115">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="cc4f4-116">Dysków zarządzanych zostały najpierw udostępnione w `2016-04-30-preview` wersja interfejsu API są dostępne w wszystkie kolejne wersje interfejsu API i są teraz domyślny typ dysku.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-116">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="cc4f4-117">Poniższe sekcje przeprowadzenie ustawienia domyślne i szczegółów jak dostosować dysków.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-117">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="cc4f4-118">Zalecane jest użycie wersji interfejsu API później niż `2016-04-30-preview` jako wystąpiły zmiany podziału między `2016-04-30-preview` i `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-118">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="cc4f4-119">Domyślne ustawienia dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="cc4f4-119">Default managed disk settings</span></span>

<span data-ttu-id="cc4f4-120">Aby utworzyć Maszynę wirtualną z dyskami zarządzanych, już nie musisz utworzyć magazyn kont zasobów i można zaktualizować zasobu maszyny wirtualnej w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-120">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="cc4f4-121">W szczególności należy pamiętać, że `apiVersion` odzwierciedla `2017-03-30` i `osDisk` i `dataDisks` nie odnoszą się do określonego identyfikatora URI dysku VHD.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-121">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="cc4f4-122">W przypadku wdrażania bez określenia dodatkowych właściwości, dysk będzie używać [magazynu Standard-LRS](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="cc4f4-122">When deploying without specifying additional properties, the disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="cc4f4-123">Jeśli nazwa nie zostanie określona, zajmuje format `<VMName>_OsDisk_1_<randomstring>` dla dysku systemu operacyjnego i `<VMName>_disk<#>_<randomstring>` dla każdego dysku danych.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-123">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="cc4f4-124">Domyślnie szyfrowania dysków Azure jest wyłączony; buforowanie jest odczytu/zapisu dla dysku systemu operacyjnego i brak w przypadku dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-124">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="cc4f4-125">W poniższym przykładzie mogą pojawić się, że istnieje zależność konta magazynu, mimo że to jest tylko do przechowywania diagnostyki i nie jest wymagany dla magazynu danych na dysku.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-125">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="cc4f4-126">Przy użyciu zasobów dysków zarządzanych w najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="cc4f4-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="cc4f4-127">Zamiast określać konfigurację dysków w obiekcie maszyny wirtualnej można tworzenia zasobu dysku najwyższego poziomu i dołącz je jako część tworzenie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-127">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="cc4f4-128">Na przykład możemy utworzyć zasób dysku w następujący sposób, aby użyć jako dysku danych.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-128">For example, we can create a disk resource as follows to use as a data disk.</span></span>

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

<span data-ttu-id="cc4f4-129">W ramach obiektu maszyny Wirtualnej możemy odwoływać ten obiekt jest dołączony.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-129">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="cc4f4-130">Określ identyfikator ID zasobu dysku zarządzanego utworzone `managedDisk` właściwość umożliwia dołączanie dysku tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-130">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="cc4f4-131">Należy pamiętać, że `apiVersion` dla maszyny Wirtualnej zasobów ma ustawioną wartość `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-131">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="cc4f4-132">Należy również zauważyć, że utworzyliśmy zależność od zasobu dyskowego, aby upewnić się, że pomyślnie utworzono przed utworzeniem maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-132">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="cc4f4-133">Tworzenie zestawów dostępności zarządzanych maszyn wirtualnych za pomocą dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="cc4f4-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="cc4f4-134">Do tworzenia zarządzanego zestawy dostępności z maszynami wirtualnymi przy użyciu dysków zarządzanych, Dodaj `sku` obiektu dostępności ustawić zasobów i ustawić `name` właściwości `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-134">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="cc4f4-135">To zapewnia, że dyski dla każdej maszyny Wirtualnej są wystarczająco odizolowane od siebie, aby uniknąć pojedynczych punktów awarii.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-135">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="cc4f4-136">Należy również zauważyć, że `apiVersion` dla zestawu dostępności zasobów ma ustawioną wartość `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-136">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="cc4f4-137">Dodatkowe scenariusze i dostosowania</span><span class="sxs-lookup"><span data-stu-id="cc4f4-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="cc4f4-138">Aby uzyskać pełne informacje dotyczące specyfikacji interfejsu API REST, zapoznaj się z tematem [tworzenie dysków zarządzanych w dokumentacji interfejsu API REST](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="cc4f4-138">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="cc4f4-139">Dostępne są dodatkowe scenariusze, a także domyślne i dopuszczalne wartości, które można przesłać do interfejsu API za pomocą szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-139">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cc4f4-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc4f4-140">Next steps</span></span>

* <span data-ttu-id="cc4f4-141">Pełna szablonów, które zarządzanych dysków można znaleźć w następujących łączy repozytorium Szybki Start Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-141">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="cc4f4-142">Maszyny Wirtualnej systemu Windows z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="cc4f4-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="cc4f4-143">Maszyny Wirtualnej systemu Linux z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="cc4f4-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="cc4f4-144">Pełną listę szablonów zarządzanych dysku</span><span class="sxs-lookup"><span data-stu-id="cc4f4-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="cc4f4-145">Odwiedź stronę [omówienie dysków zarządzanych Azure](../articles/virtual-machines/windows/managed-disks-overview.md) dokumentu, aby dowiedzieć się więcej o dyskach zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-145">Visit the [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="cc4f4-146">Zapoznaj się z dokumentacją odwołanie szablonu, zasobów maszyny wirtualnej po przejściu na stronę [odwołania do szablonu Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-146">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="cc4f4-147">Zapoznaj się z dokumentacją odwołanie szablonu, zasoby dyskowe odwiedzając [odwołania do szablonu Microsoft.Compute/disks](/templates/microsoft.compute/disks) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="cc4f4-147">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
