
* [Szybkie tworzenie maszyny wirtualnej na platformie Azure](#quick-create-a-vm-in-azure)
* [Wdrażanie maszyny wirtualnej na platformie Azure na podstawie szablonu](#deploy-a-vm-in-azure-from-a-template)
* [Tworzenie maszyny wirtualnej za pomocą obrazu niestandardowego](#create-a-custom-vm-image)
* [Wdrażanie maszyny wirtualnej korzystającej z sieci wirtualnej i modułu równoważenia obciążenia](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [Usuwanie grupy zasobów](#remove-a-resource-group)
* [Pokaż dziennik hello wdrożenia grupy zasobów](#show-the-log-for-a-resource-group-deployment)
* [Wyświetlanie informacji o maszynie wirtualnej](#display-information-about-a-virtual-machine)
* [Łączenie maszyny wirtualnej opartych na systemie Linux tooa](#log-on-to-a-linux-based-virtual-machine)
* [Zatrzymywanie maszyny wirtualnej](#stop-a-virtual-machine)
* [Uruchamianie maszyny wirtualnej](#start-a-virtual-machine)
* [Dołączanie dysku danych](#attach-a-data-disk)

## <a name="getting-ready"></a>Przygotowanie
Zanim użyjesz hello wiersza polecenia platformy Azure z grup zasobów platformy Azure, należy toohave hello właściwej wersji interfejsu wiersza polecenia Azure oraz konta platformy Azure. Jeśli nie masz hello Azure CLI [go zainstalować](../articles/cli-install-nodejs.md).

### <a name="update-your-azure-cli-version-too090-or-later"></a>Aktualizacja z wiersza polecenia platformy Azure w wersji too0.9.0 lub nowszej
Typ `azure --version` toosee, czy masz już zainstalowany w wersji 0.9.0 lub nowszej.

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

Jeśli używana wersja nie jest 0.9.0 lub później, należy tooupdate hello go za pomocą jednej z natywnego instalatorów lub za pomocą **npm** , wpisując `npm update -g azure-cli`.

Można również uruchomić wiersza polecenia platformy Azure jako kontener Docker, za pomocą następujących hello [obrazu Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/). Z hosta Docker i uruchom hello następujące polecenie:

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a>Ustawianie konta i subskrypcji platformy Azure
Jeśli nie masz jeszcze subskrypcji platformy Azure, ale masz subskrypcję MSDN, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). lub zarejestrować się w celu skorzystania z [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

Teraz [interakcyjnego logowania tooyour konta Azure](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) , wpisując `azure login` i wykonując hello monity o tooyour środowisko logowania interakcyjnego konto platformy Azure. 

> [!NOTE]
> Jeśli masz służbowego lub szkolnego identyfikator i wiesz, nie ma włączone uwierzytelnianie dwuskładnikowe, możesz **również** użyj `azure login -u` wraz z hello służbowe toolog identyfikator w *bez* sesji interaktywnej. Jeśli nie ma służbowego lub szkolnego identyfikator, możesz [Utwórz identyfikator firmy lub szkoły z osobistego konta Microsoft](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog w hello tak samo.
>
>

Twoje konto może mieć więcej niż jedną subskrypcję. Możesz wpisać polecenie `azure account list`, aby wyświetlić listę swoich subskrypcji, która może wyglądać następująco:

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

Można ustawić hello bieżącej subskrypcji Azure, wpisując następujące hello. Użyj hello nazwy lub hello identyfikator subskrypcji zawierającego zasoby hello ma toomanage.

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a>Przełącz tryb grupy zasobów Azure CLI toohello
Domyślnie program hello Azure CLI jest uruchamiany w trybie zarządzania usługi hello (**asm** tryb). Wpisz powitania po tooswitch tooresource grupy tryb.

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a>Opis szablonów zasobów i grup zasobów platformy Azure
Większość aplikacji jest tworzona z połączenia różnych typów zasobów (na przykład jednej lub kilku maszyn wirtualnych i kont magazynu, bazy danych SQL, sieci wirtualnej lub sieci dostarczania zawartości). Witaj interfejsu API zarządzania usługami Azure domyślne i hello klasycznego portalu Azure reprezentowana tych elementów przy użyciu podejścia przez usługi. To rozwiązanie wymaga toodeploy i indywidualnie zarządzania hello poszczególnych usług (lub znaleźć innych narzędzi, które to zrobić), a nie jako pojedyncza jednostka logiczna wdrożenia.

*Szablony usługi Azure Resource Manager*, jednak umożliwiają możesz toodeploy zasobów i zarządzanie nimi tych różnych jako jedną jednostkę logiczną wdrożenia w sposób deklaratywnego. Zamiast imperatively informuje Azure jakie toodeploy jednego polecenia po kolei, opisu całego wdrożenia w pliku JSON, — wszystkie zasoby hello i skojarzone konfiguracji i parametrów wdrożenia — i poinformuj Azure toodeploy tych zasobów jako jeden Grupa.

Następnie można zarządzać hello ogólną cyklu życia hello grupy zasobów za pomocą interfejsu wiersza polecenia Azure zasobów zarządzania poleceń do:

* Zatrzymać, uruchomić lub usunąć wszystkie zasoby hello w obrębie grupy hello naraz.
* Zastosuj toolock zasady kontroli dostępu opartej na rolach (RBAC) uprawnień zabezpieczeń w dół na nich.
* przeprowadzać inspekcje operacji;
* oznaczać zasoby za pomocą dodatkowych metadanych w celu ułatwienia śledzenia.

Dowiedz się więcej na temat grup zasobów platformy Azure i sposób ich działania dla Ciebie w hello partii [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md). Jeśli interesuje Cię tworzenie szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager](../articles/resource-group-authoring-templates.md).

## <a id="quick-create-a-vm-in-azure"></a>Zadanie: Szybkie tworzenie maszyny wirtualnej na platformie Azure
Czasami wiesz, jakie obrazu należy i maszyny Wirtualnej z obrazu należy od razu i nie zależy Ci zbyt dużo o infrastruktury hello — może być po zdefiniowaniu tootest czystą maszyny wirtualnej. Gdy to ma toouse hello `azure vm quick-create` polecenia i przekaż toocreate niezbędne argumenty hello maszyny Wirtualnej i jej infrastruktury.

Najpierw utwórz grupę zasobów.

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Następnie potrzebny będzie obraz. toofind jako obraz z hello wiersza polecenia platformy Azure, zobacz [Navigating i wybieranie obrazów maszyny wirtualnej platformy Azure za pomocą programu PowerShell i hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Na potrzeby tego artykułu uwzględniono krótką listę popularnych obrazów. W przypadku tego szybkiego tworzenia używany będzie obraz stabilny systemu CoreOS.

> [!NOTE]
> Dla ComputeImageVersion możesz także po prostu podać "najnowsze" jako parametru w obu język szablonu hello i hello Azure CLI hello. Pozwoli to wykonywanych tooalways hello najnowsze i poprawioną wersja obrazu hello bez konieczności toomodify skryptu lub szablonów. Jest to pokazane poniżej.
>
>

| PublisherName | Oferta | SKU | Wersja |
|:--- |:--- |:--- |:--- |
| OpenLogic |CentOS |7 |7.0.201503 |
| OpenLogic |CentOS |7.1 |7.1.201504 |
| CoreOS |CoreOS |Beta |647.0.0 |
| CoreOS |CoreOS |Stable |633.1.0 |
| MicrosoftDynamicsNAV |DynamicsNAV |2015 |8.0.40459 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2013 |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Standardowa (Standard) |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Enterprise |1.0.0 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-DW |12.0.2430 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-OLTP |12.0.2430 |
| Canonical |UbuntuServer |12.04.5-LTS |12.04.201504230 |
| Canonical |UbuntuServer |14.04.2-LTS |14.04.201503090 |
| MicrosoftWindowsServer |WindowsServer |2012-Datacenter |3.0.201503 |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |4.0.201503 |
| MicrosoftWindowsServer |WindowsServer |Windows-Server-Technical-Preview |5.0.201504 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |1.0.141204 |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |4.3.4665 |

Po prostu utworzyć maszyny Wirtualnej, wprowadzając hello `azure vm quick-create` polecenia i gotowe do hello monitów. Powinno to wyglądać następująco:

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

I możesz iść dalej z nową maszyną wirtualną.

## <a id="deploy-a-vm-in-azure-from-a-template"></a>Zadanie: Wdrażanie maszyny wirtualnej na platformie Azure na podstawie szablonu
Użyj instrukcji hello w tych sekcjach toodeploy nowej maszyny Wirtualnej platformy Azure przy użyciu szablonu z hello wiersza polecenia platformy Azure. Ten szablon tworzy jednej maszyny wirtualnej w nowej sieci wirtualnej z pojedynczą podsiecią w przeciwieństwie do `azure vm quick-create`, umożliwia toodescribe należy dokładnie mają i powtarzaj go bez błędów. Oto, co ten szablon tworzy:

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a>Krok 1: Sprawdź plik JSON hello hello parametrów szablonu
Poniżej przedstawiono hello zawartość pliku JSON hello hello szablonu. (szablon hello znajduje się również w [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)

Szablony są elastyczne i co projektanta hello może wybrany toogive wiele parametrów albo wybrany toooffer tylko kilka, tworząc szablon, który jest bardziej stała. Wymagany jest szablon hello toopass jako parametry informacje hello toocollect kolejności, otwórz plik szablonu hello (w tym temacie ma wbudowany szablonu, poniżej) i sprawdź, czy hello **parametry** wartości.

W takim przypadku poniższy szablon hello poprosi o:

* Unikalna nazwa konta magazynu.
* Nazwa użytkownika administratora dla hello maszyny Wirtualnej.
* Hasło.
* Nazwa domeny hello poza world toouse.
* Numer wersji systemu Ubuntu Server (ale będzie akceptować tylko jeden z listy).

Więcej informacji na temat [wymagań dotyczących nazwy użytkownika i hasła](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).

Po podjęciu decyzji o tych wartości, wszystko gotowe toocreate grupę i wdrożenia tego szablonu do Twojej subskrypcji platformy Azure.

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a>Krok 2: Tworzenie maszyny wirtualnej hello przy użyciu szablonu hello
Po utworzeniu wartości parametru gotowe, możesz utworzyć grupę zasobów do wdrożenia szablonu, a następnie wdrożyć hello szablonu.

Grupa zasobów hello toocreate, typ `azure group create <group name> <location>` o nazwie hello grupy hello ma i hello centrum danych lokalizacji, do której ma zostać toodeploy. To dzieje się szybko:

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Teraz toocreate hello wdrożenia, wywołanie `azure group deployment create` i przekaż:

* Plik szablonu Hello (jeśli został zapisany hello powyżej pliku lokalnego tooa szablonu JSON).
* Szablon identyfikatora URI (jeśli ma toopoint hello plik w witrynie GitHub lub inny adres sieci web).
* grupy zasobów Hello, do której ma zostać toodeploy.
* Opcjonalna nazwa wdrożenia.

Będzie toosupply zostanie wyświetlony monit o hello wartości parametrów w sekcji "Parametry" hello hello pliku JSON. Po określeniu wszystkich wartości parametru hello rozpocznie się wdrożenia.

Oto przykład:

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

Zostanie wyświetlony hello następujące rodzaje informacji:

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <a id="create-a-custom-vm-image"></a>Zadanie: Tworzenie niestandardowej maszyny wirtualnej
W tym samouczku hello podstawowe sposoby użycia szablonów powyżej, więc teraz możemy użyć podobne toocreate instrukcje niestandardowe maszyny Wirtualnej z pliku VHD określonych na platformie Azure przy użyciu szablonu za pomocą hello wiersza polecenia platformy Azure. Witaj różnicą jest to, że ten szablon tworzy jednej maszyny wirtualnej na podstawie określony wirtualny dysk twardy (VHD).

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Krok 1: Sprawdź plik JSON hello hello szablonu
Poniżej przedstawiono hello zawartość pliku JSON hello hello szablonu, który używa tej sekcji to przykład. (szablon hello znajduje się również w [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)

Ponownie konieczne będzie toofind hello wartości, które mają tooenter hello parametrów, które nie mają wartości domyślne. Po uruchomieniu hello `azure group deployment create` polecenia hello Azure CLI wyświetli monit o tooenter możesz tych wartości.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a>Krok 2: Uzyskaj hello wirtualnego dysku twardego
Oczywiście niezbędny będzie plik VHD. Możesz użyć dysku znajdującego się już na platformie Azure lub przekazać inny.

Dla maszyny wirtualnej z systemem Windows, temacie [tworzenie i przekazywanie wirtualnego dysku twardego z systemem Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Dla maszyny wirtualnej opartych na systemie Linux, zobacz [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a>Krok 3: Tworzenie maszyny wirtualnej hello przy użyciu szablonu hello
Teraz wszystko jest gotowe toocreate VHD hello — na podstawie nowej maszyny wirtualnej. Tworzenie toodeploy grupy, do, przy użyciu `azure group create <location>`:

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Następnie utwórz hello wdrożenia przy użyciu hello `--template-uri` toocall opcji w szablonie hello bezpośrednio (lub użyć hello `--template-file` toouse opcja pliku zapisanych lokalnie). Należy pamiętać, że szablonu hello się domyślnych ustawień, zostanie wyświetlony monit o tylko kilka rzeczy. Jeśli wdrożono szablon hello w różnych miejscach, może się okazać, że niektóre kolizji nazw wystąpić z wartościami domyślnymi hello (szczególnie hello nazwa DNS utworzone).

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Dane wyjściowe podobne hello następujące czynności:

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Zadanie: Wdrażanie aplikacji z wieloma maszynami wirtualnymi, korzystającej z sieci wirtualnej i modułu równoważenia obciążenia
Ten szablon umożliwia toocreate dwóch maszyn wirtualnych należących do modułu równoważenia obciążenia i skonfigurować regułę równoważenia obciążenia na porcie 80. Ten szablon wdraża również konto magazynu, sieć wirtualną, publiczny adres IP, zestaw dostępności i interfejsy sieciowe.

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

Wykonaj te kroki toodeploy aplikacji wielu maszyn wirtualnych, która korzysta z sieci wirtualnej i modułu równoważenia obciążenia przy użyciu szablonu usługi Resource Manager w repozytorium hello GitHub szablonu, za pomocą poleceń programu PowerShell systemu Azure.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Krok 1: Sprawdź plik JSON hello hello szablonu
Poniżej przedstawiono hello zawartość pliku JSON hello hello szablonu. Jeśli chcesz, aby hello najnowszej wersji, jej ma znajduje się [w repozytorium GitHub hello szablonów](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json). W tym temacie używa hello `--template-uri` toocall przełącznika hello szablonu, ale można również użyć hello `--template-file` przełącznika toopass lokalnej wersji.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a>Krok 2: Tworzenie hello wdrożenia przy użyciu szablonu hello
Utwórz grupę zasobów dla szablonu hello przy użyciu `azure group create <location>`. Następnie utwórz wdrożenie w tej grupie zasobów przy użyciu `azure group deployment create` i przekazywanie hello grupy zasobów, przekazywanie Nazwa wdrożenia i udzielenie odpowiedzi na powitania monity dla parametrów w szablonie hello, która nie ma wartości domyślnej.

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Teraz używać hello `azure group deployment create` polecenia i hello `--template-uri` szablon hello toodeploy opcji. Miej przygotowane wartości parametrów do wprowadzenia po wyświetleniu monitu, jak pokazano poniżej.

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

Należy zauważyć, że ten szablon wdraża obraz systemu Windows Server, który jednak łatwo może zostać zastąpiony przez dowolny obraz systemu Linux. Chcesz toocreate klastrze Docker z wielu menedżerów swarm? [Możesz to zrobić](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).

## <a id="remove-a-resource-group"></a>Zadanie: Usuwanie grupy zasobów
Należy pamiętać, że można wdrożyć ponownie tooa grupy zasobów, ale po zakończeniu jednego, można usunąć go za pomocą `azure group delete <group name>`.

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <a id="show-the-log-for-a-resource-group-deployment"></a>Zadanie: Pokaż dziennik hello wdrożenia grupy zasobów
To zadanie jest typowe podczas tworzenia lub korzystania z szablonów. Witaj wywołania toodisplay hello wdrożenia dzienniki dla grupy jest `azure group log show <groupname>`, które powoduje wyświetlenie dość nieco informacje, które ułatwia zrozumienie, dlaczego coś się stało--lub nie. (Aby uzyskać więcej informacji na temat rozwiązywania problemów dotyczących wdrożeń oraz inne informacje o problemach, zobacz [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md) (Rozwiązywanie typowych problemów dotyczących wdrażania za pomocą usługi Azure Resource Manager).

tootarget określonych niepowodzeń, na przykład można na przykład takich narzędzi jak **jq** tooquery rzeczy bardziej precyzyjnie, takich jak które poszczególnych błędów należy toocorrect. Witaj poniższym przykładzie użyto **jq** tooparse, poszukaj w dzienniku wdrożenia **lbgroup**poszukujący błędów.

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
Możesz szybko znaleźć przyczynę problemu, naprawić błąd i ponowić próbę. W następujących przypadków hello, hello szablonu ma były tworzone dwie maszyny wirtualne na powitania tym samym czasie, który utworzony blokady na powitania VHD. (Po zmodyfikowaniu szablonu hello firma Microsoft hello Zakończono pomyślnie wdrażanie szybko.)

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <a id="display-information-about-a-virtual-machine"></a>Zadanie: Wyświetlanie informacji o maszynie wirtualnej
Umożliwia wyświetlenie informacji o określonych maszynach wirtualnych w grupie zasobów, przy użyciu hello `azure vm show <groupname> <vmname>` polecenia. Jeśli masz więcej niż jedną maszynę Wirtualną w grupie, być może konieczne toolist hello maszyn wirtualnych w grupie za pomocą `azure vm list <groupname>`.

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

Następnie wyszukaj maszynę myVM1:

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> Magazyn tooprogrammatically i manipulowania hello dane wyjściowe z konsoli poleceń, może być toouse JSON podczas analizowania narzędzi takich jak  **[jq](https://github.com/stedolan/jq)**  lub  **[jsawk](https://github.com/micha/jsawk)** , lub bibliotek języka, które są odpowiednie dla hello zadania.
>
>

## <a id="log-on-to-a-linux-based-virtual-machine"></a>Zadań: Zaloguj się maszyny wirtualnej opartych na systemie Linux tooa
Zazwyczaj maszyny z systemem Linux są toothrough połączenia SSH. Aby uzyskać więcej informacji, zobacz [jak toouse SSH z systemem Linux na platformie Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a id="stop-a-virtual-machine"></a>Zadanie: Zatrzymywanie maszyny wirtualnej
Uruchom następujące polecenie:

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> Użyj tego parametru tookeep hello wirtualnego adresu IP (VIP) hello sieci wirtualnej, w razie hello ostatnia maszyna wirtualna w tej sieci wirtualnej. <br><br> Jeśli używasz hello `StayProvisioned` parametru nadal zostaną naliczone opłaty dla hello maszyny Wirtualnej.
>
>

## <a id="start-a-virtual-machine"></a>Zadanie: Uruchamianie maszyny wirtualnej
Uruchom następujące polecenie:

```azurecli
azure vm start <group name> <virtual machine name>
```

## <a id="attach-a-data-disk"></a>Zadanie: Dołączanie dysku danych
Należy również toodecide czy tooattach nowy dysk lub jeden zawierający dane. Dla nowego dysku hello polecenie tworzy plik VHD hello i dołącza go w hello tego samego polecenia.

tooattach nowego dysku, uruchom następujące polecenie:

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

tooattach istniejący dysk danych, uruchom następujące polecenie:

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

Następnie należy toomount hello dysku, jak zwykle w systemie Linux.

## <a name="next-steps"></a>Następne kroki
Znacznie więcej przykładów dotyczących użycia interfejsu wiersza polecenia Azure za pomocą hello **arm** tryb, zobacz [hello Using Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](../articles/xplat-cli-azure-resource-manager.md). Zobacz toolearn więcej informacji na temat zasobów platformy Azure i ich pojęcia [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).

Aby uzyskać dodatkowe szablony, których możesz użyć, zobacz [Szablony szybkiego startu platformy Azure](https://azure.microsoft.com/documentation/templates/) i [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Platformy aplikacji korzystające z szablonów).
