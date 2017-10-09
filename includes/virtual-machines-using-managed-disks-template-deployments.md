# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="b2cbe-101">Za pomocą Managed dysków w szablonach usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b2cbe-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="b2cbe-102">Ten dokument przeprowadzi Cię przez hello różnice między dyskami zarządzane i niezarządzane, korzystając z maszyn wirtualnych tooprovision szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-102">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="b2cbe-103">Pomoże to tooupdate istniejących szablonów, które korzystają z niezarządzanego dysków toomanaged dysków.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-103">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="b2cbe-104">Odwołania, jest używany hello [101 maszyny wirtualnej — prosty — windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) szablonu jako przewodnika.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-104">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="b2cbe-105">Widać hello szablonu przy użyciu zarówno [dyskach zarządzanych](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) i przy użyciu poprzedniej wersji [niezarządzanych dysków](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) Jeśli chcesz toodirectly porównania.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-105">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="b2cbe-106">Niezarządzane formatowania szablonu dysków</span><span class="sxs-lookup"><span data-stu-id="b2cbe-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="b2cbe-107">toobegin, możemy też zwrócić uwagę na sposób niezarządzany dyski są wdrażane.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-107">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="b2cbe-108">Podczas tworzenia dysków niezarządzane, należy się pliki VHD hello toohold konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-108">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="b2cbe-109">Możesz utworzyć nowe konto magazynu lub użyć już istniejącego.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="b2cbe-110">W tym artykule opisano, jak toocreate nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-110">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="b2cbe-111">tooaccomplish, to należy zasób konta magazynu w bloku zasobów hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-111">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

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

<span data-ttu-id="b2cbe-112">W ramach hello obiektu maszyny wirtualnej potrzebujemy zależności hello tooensure konta magazynu, utworzony przed hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-112">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="b2cbe-113">W ramach hello `storageProfile` sekcji, a następnie określ hello pełny identyfikator URI hello lokalizacja wirtualnego dysku twardego, który odwołuje się do konta magazynu hello i jest wymagany dla dysku hello systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-113">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="b2cbe-114">Zarządzane formatowania szablonu dysków</span><span class="sxs-lookup"><span data-stu-id="b2cbe-114">Managed disks template formatting</span></span>

<span data-ttu-id="b2cbe-115">Zarządzane dysków Azure hello dysku staje się zasobem najwyższego poziomu i nie wymaga już utworzone przez użytkownika hello toobe konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-115">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="b2cbe-116">Dyski zarządzanych najpierw były widoczne w hello `2016-04-30-preview` wersja interfejsu API są dostępne w wszystkie kolejne wersje interfejsu API i są teraz hello domyślny typ dysku.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-116">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="b2cbe-117">Witaj sekcje przeprowadzenie hello domyślne ustawienia i szczegółów jak toofurther dostosować dysków.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-117">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="b2cbe-118">Zalecane jest toouse interfejsu API w wersji nowszej niż `2016-04-30-preview` jako wystąpiły zmiany podziału między `2016-04-30-preview` i `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-118">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="b2cbe-119">Domyślne ustawienia dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="b2cbe-119">Default managed disk settings</span></span>

<span data-ttu-id="b2cbe-120">toocreate maszynę Wirtualną za pomocą dysków zarządzanych, użytkownik nie jest już konieczne zasobów konta magazynu hello toocreate i można zaktualizować zasobu maszyny wirtualnej w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-120">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="b2cbe-121">W szczególności należy pamiętać, że hello `apiVersion` odzwierciedla `2017-03-30` i hello `osDisk` i `dataDisks` nie można znaleźć tooa określonego identyfikatora URI dla hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-121">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="b2cbe-122">Wdrażając bez określenia dodatkowych właściwości użyje dysku hello [magazynu Standard-LRS](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="b2cbe-122">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="b2cbe-123">Jeśli nazwa nie zostanie określona, zajmuje hello format `<VMName>_OsDisk_1_<randomstring>` dla dysku systemu operacyjnego hello i `<VMName>_disk<#>_<randomstring>` dla każdego dysku danych.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-123">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="b2cbe-124">Domyślnie szyfrowania dysków Azure jest wyłączony; buforowanie jest odczytu/zapisu dla dysku systemu operacyjnego hello i brak w przypadku dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-124">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="b2cbe-125">W poniższym przykładzie hello mogą pojawić się, że istnieje zależność konta magazynu, mimo że to jest tylko do przechowywania diagnostyki i nie jest wymagany dla magazynu danych na dysku.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-125">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="b2cbe-126">Przy użyciu zasobów dysków zarządzanych w najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="b2cbe-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="b2cbe-127">Jako alternatywne toospecifying hello konfigurację dysku w hello obiektu maszyny wirtualnej można tworzyć zasób dysku najwyższego poziomu i dołącz je jako część hello tworzenie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-127">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="b2cbe-128">Na przykład możemy utworzyć zasób dysku następujący toouse jako dysk danych.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-128">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

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

<span data-ttu-id="b2cbe-129">W ramach hello obiektu maszyny Wirtualnej możemy odwołania tego dysku toobe obiektu, który jest dołączony.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-129">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="b2cbe-130">Określ identyfikator ID zasobu hello z hello zarządzane dysku utworzone hello `managedDisk` właściwość umożliwia dołączanie hello hello dysku jako hello zostanie utworzona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-130">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="b2cbe-131">Należy pamiętać, że hello `apiVersion` dla hello zasobu maszyny Wirtualnej jest ustawiony za`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-131">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="b2cbe-132">Należy również zauważyć, że utworzyliśmy zależności na powitania tooensure zasobu dysku, którym pomyślnie zostały utworzone przed utworzeniem maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-132">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="b2cbe-133">Tworzenie zestawów dostępności zarządzanych maszyn wirtualnych za pomocą dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="b2cbe-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="b2cbe-134">toocreate zarządzane dostępności zestawów z maszyn wirtualnych za pomocą dysków zarządzanych, Dodaj hello `sku` obiektu toohello dostępności ustawić zasobów i ustawić hello `name` właściwości zbyt`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-134">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="b2cbe-135">To zapewnia, że dyski powitania dla każdej maszyny Wirtualnej są wystarczająco odizolowane od siebie nawzajem tooavoid pojedynczych punktów awarii.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-135">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="b2cbe-136">Należy również zauważyć, że hello `apiVersion` dla zestawu dostępności hello zasobów ustawiono zbyt`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-136">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="b2cbe-137">Dodatkowe scenariusze i dostosowania</span><span class="sxs-lookup"><span data-stu-id="b2cbe-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="b2cbe-138">toofind pełne informacje dotyczące hello specyfikacji interfejsu API REST, zapoznaj się z tematem hello [tworzenie dysków zarządzanych w dokumentacji interfejsu API REST](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="b2cbe-138">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="b2cbe-139">Dostępne są dodatkowe scenariusze, a także domyślne i dopuszczalne wartości, które mogą być przesłane toohello API za pomocą szablonu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-139">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b2cbe-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2cbe-140">Next steps</span></span>

* <span data-ttu-id="b2cbe-141">Pełna szablonów, które zarządzanych dysków można znaleźć hello następującego łącza repozytorium Szybki Start Azure.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-141">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="b2cbe-142">Maszyny Wirtualnej systemu Windows z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="b2cbe-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="b2cbe-143">Maszyny Wirtualnej systemu Linux z dyskiem zarządzanym</span><span class="sxs-lookup"><span data-stu-id="b2cbe-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="b2cbe-144">Pełną listę szablonów zarządzanych dysku</span><span class="sxs-lookup"><span data-stu-id="b2cbe-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="b2cbe-145">Odwiedź hello [omówienie dysków zarządzanych Azure](../articles/virtual-machines/windows/managed-disks-overview.md) dokumentu toolearn więcej informacji o dyskach zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-145">Visit hello [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="b2cbe-146">Przejrzyj dokumentację referencyjną szablonu hello zasobów maszyny wirtualnej, przechodząc na stronę hello [odwołania do szablonu Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-146">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="b2cbe-147">Przejrzyj dokumentację referencyjną szablonu hello zasoby dyskowe, przechodząc na stronę hello [odwołania do szablonu Microsoft.Compute/disks](/templates/microsoft.compute/disks) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="b2cbe-147">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
