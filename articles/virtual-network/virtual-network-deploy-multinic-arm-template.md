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
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>Utwórz maszynę Wirtualną z wieloma kartami sieciowymi przy użyciu szablonu
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](virtual-network-deploy-multinic-classic-ps.md).
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Witaj następujące kroki Użyj grupy zasobów o nazwie *IaaSStory* hello serwerów sieci WEB oraz grupę zasobów o nazwie *IaaSStory zaplecza* dla serwerów hello bazy danych.

## <a name="prerequisites"></a>Wymagania wstępne
Przed utworzeniem hello serwerów bazy danych, należy toocreate hello *IaaSStory* grupy zasobów z wszystkie niezbędne zasoby hello w tym scenariuszu. ukończenie tych zasobów, toocreate hello następujące kroki:

1. Przejdź za[strony szablonu hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Na stronie szablon hello toohello po prawej **nadrzędnej grupy zasobów**, kliknij przycisk **wdrażanie tooAzure**.
3. W razie potrzeby zmień wartości parametrów hello, a następnie wykonaj kroki hello w grupie zasobów hello toodeploy portalu Azure w wersji zapoznawczej hello.

> [!IMPORTANT]
> Upewnij się, że nazwy konta magazynu są unikatowe. Nie może mieć nazwy konta magazynu zduplikowanych na platformie Azure.
> 

## <a name="understand-hello-deployment-template"></a>Zrozumienie hello Szablon wdrożenia
Przed przystąpieniem do wdrażania szablonu hello wyposażone w tej dokumentacji, upewnij się, że rozumiesz, jakie operacje. Witaj, wykonaj czynności zawierają omówienie hello szablonu:

1. Przejdź za[strony szablonu hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Kliknij przycisk **azuredeploy.json** tooopen hello szablon pliku.
3. Powiadomienie hello *osType* parametrów wymienionych poniżej. Ten parametr jest używany tooselect ustawienia powiązane z jakiego toouse obrazu maszyny Wirtualnej na powitania serwera bazy danych, wraz z wielu systemów operacyjnych.

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

4. Przewiń w dół listę zmiennych toohello i sprawdź definicję hello hello **dbVMSetting** zmienne wymienione poniżej. Jeden z elementów tablicy hello zawarte w hello odbierze **dbVMSettings** zmiennej. Jeśli znasz terminologii rozwoju oprogramowania, możesz wyświetlić hello **dbVMSettings** zmiennej jako tablicy skrótów lub w słowniku.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. Załóżmy, że zdecydujesz maszyn wirtualnych systemu Windows toodeploy programem SQL w wewnętrznej hello. Następnie hello wartość **osType** będzie *Windows*i hello **dbVMSetting** zmiennej może zawierać element hello wymienione poniżej, który reprezentuje hello pierwsza wartość hello **dbVMSettings** zmiennej.

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

6. Powiadomienie hello **vmSize** zawiera wartość hello *Standard_DS3*. Niektórych rozmiarów maszyn wirtualnych umożliwiają hello korzystanie z wielu kart sieciowych. Możesz sprawdzić rozmiarów maszyn wirtualnych, które obsługują wiele kart sieciowych, odczytując hello [rozmiarów maszyn wirtualnych systemu Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [rozmiarów maszyn wirtualnych systemu Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artykułów.

7. Przewiń w dół za**zasobów** i powiadomienia hello pierwszego elementu. Opisuje konta magazynu. To konto magazynu będzie używane przez każdą bazę danych maszyny Wirtualnej dysków z danymi hello toomaintain używane. W tym scenariuszu każda baza danych maszyny Wirtualnej ma dysku systemu operacyjnego przechowywanego w regularnych magazynu oraz dwóch dysków danych przechowywanych w magazynie SSD (premium).

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

8. Przewiń w dół toohello następnego zasobu wymienione poniżej. Ten zasób reprezentuje hello używane dla dostępu do bazy danych w każdej bazie danych maszyny Wirtualnej karty Sieciowej. Użycie hello powiadomienia hello **kopiowania** funkcji w przypadku tego zasobu. Szablon Hello pozwala toodeploy jako wiele maszyn wirtualnych można dowolnie na podstawie hello **dbCount** parametru. W związku z tym należy toocreate hello samo kart sieciowych dla dostępu do bazy danych, po jednej dla każdej maszyny Wirtualnej.

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

9. Przewiń w dół toohello następnego zasobu wymienione poniżej. Ten zasób reprezentuje hello używanego przez kartę Sieciową do zarządzania w każdej bazie danych maszyny Wirtualnej. Ponownie potrzebujesz jednego z tych kart sieciowych dla każdej maszyny Wirtualnej bazy danych. Powiadomienie hello **grupy networkSecurityGroup** element łączenie umożliwiająca dostęp toothis tooRDP/SSH kart interfejsu Sieciowego tylko grupy NSG.

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

10. Przewiń w dół toohello następnego zasobu wymienione poniżej. Ten zasób reprezentuje toobe zestaw dostępności współużytkowane przez wszystkie bazy danych maszyn wirtualnych. W ten sposób można zagwarantować, że zawsze będzie jedna maszyna wirtualna w hello ustawić uruchamianie w trakcie konserwacji.

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

11. Przewiń w dół toohello następnego zasobu. Ten zasób reprezentuje hello bazy danych maszyn wirtualnych, jak pokazano w hello pierwszych kilku wierszy wymienionych poniżej. Użycie hello powiadomienia hello **kopiowania** ponownie działać, zapewniając, że wiele maszyn wirtualnych są tworzone w oparciu hello **dbCount** parametru. Ponadto hello **dependsOn** kolekcji. Wyświetlane są dwie karty sieciowe są niezbędne toobe utworzone przed powitalne maszyna wirtualna jest wdrożona, wraz z zestawu dostępności hello i hello konta magazynu.

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

12. Przewiń w dół w toohello zasobów maszyny Wirtualnej hello **networkProfile** elementu wymienione poniżej. Zwróć uwagę, że istnieją dwie karty sieciowe są odwołania dla każdej maszyny Wirtualnej. Podczas tworzenia wielu kart sieciowych maszyny wirtualnej, należy ustawić hello **głównej** właściwość hello karty sieciowe za*true*, i hello rest zbyt*false*.

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

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Wdrażanie szablonu ARM hello przy użyciu kliknij toodeploy

> [!IMPORTANT]
> Upewnij się, że wykonaj hello [wstępne](#Pre-requisites) kroki przed wykonaniem instrukcji hello poniżej.
> 

Hello przykładowy szablon dostępne w publicznych repozytorium hello używa parametru plik zawierający hello domyślne wartości używane toogenerate hello scenariusz opisany powyżej. toodeploy przy użyciu tego szablonu kliknij toodeploy, postępuj zgodnie z [to łącze](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello po prawej **grupy zasobów w wewnętrznej bazie danych (zobacz dokumentację)** kliknij **wdrażanie tooAzure**, Zastąp Witaj domyślne wartości parametrów, jeśli to konieczne i wykonaj instrukcje hello w portalu hello.

na poniższej ilustracji Hello przedstawiona zawartość hello hello nową grupę zasobów, po wdrożeniu.

![Wewnętrzna grupa zasobów](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>Wdrażanie szablonu hello przy użyciu programu PowerShell
toodeploy hello szablon został pobrany przy użyciu programu PowerShell, instalowanie i konfigurowanie programu PowerShell, wykonując kroki hello hello [Instalowanie i konfigurowanie programu PowerShell](/powershell/azure/overview) artykuł, a następnie ukończ hello następujące kroki:

Uruchom hello  **`New-AzureRmResourceGroup`**  toocreate polecenia cmdlet, grupy zasobów przy użyciu hello szablonu.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

Oczekiwane dane wyjściowe:

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

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Wdrażanie szablonu hello przy użyciu hello wiersza polecenia platformy Azure
Szablon hello toodeploy za pomocą hello wiersza polecenia platformy Azure, wykonaj kroki hello poniżej.

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello  **`azure config mode`**  tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.

    ```azurecli
    azure config mode arm
    ```

    Witaj oczekiwane dane wyjściowe w następujący sposób:

        info:    New mode is arm

3. Otwórz hello [pliku parametrów](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), zaznacz zawartością i zapisz go tooa plik na swoim komputerze. Na przykład zapisaliśmy hello pliku parametrów, za*parameters.JSON następującym kodem*.
4. Uruchom hello  **`azure group deployment create`**  hello toodeploy polecenia cmdlet nowej sieci wirtualnej przy użyciu szablonu hello i parametr pliki uprzednio pobranego i zmodyfikowanego. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    Oczekiwane dane wyjściowe:
   
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

