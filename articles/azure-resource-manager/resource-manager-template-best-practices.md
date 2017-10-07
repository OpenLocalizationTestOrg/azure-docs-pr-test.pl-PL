---
title: "aaaBest wskazówki dotyczące tworzenia szablonów usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Wytyczne dotyczące uproszczenia szablonów usługi Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Najlepsze rozwiązania dotyczące tworzenia szablonów usługi Azure Resource Manager
Niniejsze wytyczne ułatwia tworzenie szablonów usługi Azure Resource Manager, które są toouse niezawodnych i prostych. wskazówki Hello są tylko sugestie. Nie są one wymagania, oprócz wskazanych wyjątków. Scenariusz może wymagać zmiany jednego hello podejścia lub przykłady.

## <a name="resource-names"></a>Nazwy zasobów
Ogólnie rzecz biorąc pracować z trzech rodzajów nazw zasobów w Menedżerze zasobów:

* Nazwy zasobów, które muszą być unikatowe.
* Nazwy zasobów, które nie są wymagane toobe unikatowy, ale możesz wybrać tooprovide nazwę, która może pomóc w identyfikacji zasobu na podstawie kontekstu.
* Nazwy zasobów, które mogą być ogólne.

 Aby uzyskać informacje o ograniczeniach nazw zasobów, zobacz [konwencje nazewnictwa dla zasobów platformy Azure zalecane](../guidance/guidance-naming-conventions.md).

### <a name="unique-resource-names"></a>Nazwy zasobów unikatowy
Musisz podać nazwę zasobu unikatowy dla dowolnego typu zasobu, która zawiera punkt końcowy dostępu do danych. Niektóre typowe typy zasobów, które wymagają unikatową nazwę obejmują:

* Usługa Azure Storage<sup>1</sup> 
* Funkcje aplikacji internetowych w usłudze Azure App Service
* Oprogramowanie SQL Server
* W usłudze Azure Key Vault
* Azure Redis Cache
* Azure Batch
* Azure Traffic Manager
* Azure Search
* Usługa Azure HDInsight

<sup>1</sup> nazwy konta magazynu musi być także małe litery, 24 znaków lub mniej, a nie ma żadnych łączników.

Jeśli podasz nazwę zasobu parametr, Podaj unikatową nazwę podczas wdrażania zasobu hello. Opcjonalnie można utworzyć zmiennej, która używa hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate nazwę funkcji. 

Możesz również mają tooadd prefiks lub sufiks toohello **uniqueString** wynik. Modyfikowanie hello unikatową nazwę może pomóc więcej łatwo zidentyfikować hello typu zasobu na podstawie nazwy hello. Na przykład można wygenerować unikatowej nazwy dla konta magazynu przy użyciu następującej zmiennej hello:

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Nazwy zasobów do identyfikacji
Niektóre typy zasobów może być tooname, ale ich nazwy nie mają toobe unikatowy. W przypadku tych typów zasobów można Podaj nazwę, która identyfikuje zarówno hello zasobów kontekst, jak i hello typu zasobu. Wprowadź opisową nazwę, która pomaga w identyfikacji zasobów hello na liście zasobów. Jeśli potrzebujesz toouse inną nazwę zasobu dla różnych wdrożeń można użyć parametru hello nazwy:

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

Jeśli nie potrzebują toopass w nazwie podczas wdrażania, można użyć zmiennej: 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

Można także użyć wartości stałe:

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>Nazwy zasobów ogólnych
Dla typów zasobów, które przede wszystkim uzyskują dostęp za pomocą innego zasobu można użyć nazwy ogólnej, który jest ustalony w szablonie hello. Na przykład można ustawić nazwę standardowego, ogólne reguły zapory na serwerze SQL server:

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>Parametry
Witaj następujące informacje mogą być pomocne podczas pracy z parametrów:

* Zminimalizować korzystanie z parametrów. Jeśli to możliwe, należy użyć zmiennej lub wartość literału. Parametry tylko dla tych scenariuszy:
   
   * Ustawienia, które mają toouse zmian zgodnie z tooenvironment (jednostka SKU, rozmiar, pojemności).
   * Nazwy zasobów ma toospecify ułatwiający identyfikację.
   * Wartości użycie często toocomplete inne zadania (takie jak nazwa użytkownika administratora).
   * Klucze tajne (takie jak hasła).
   * numer Hello lub tablicy toouse wartości podczas tworzenia wielu wystąpień typu zasobu.
* Użyj formatu camelcase dla nazw parametrów.
* Podaj opis każdego parametru w metadanych hello:

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* Zdefiniuj wartości domyślne parametrów (z wyjątkiem hasła i klucze SSH):
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* Użyj **SecureString** dla wszystkich hasła i klucze tajne: 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* Jeśli to możliwe, nie używaj lokalizacji toospecify parametru. Zamiast tego należy użyć hello **lokalizacji** właściwości hello grupy zasobów. Za pomocą hello **resourceGroup () .location** wyrażenie dla wszystkich zasobów, zasobów w szablonie hello są wdrażane w tej samej lokalizacji co grupa zasobów hello hello:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   Jeśli typ zasobu jest obsługiwana w ograniczonej liczby miejsc, można toospecify bezpośrednio w szablonie hello prawidłową lokalizację. Jeśli musisz użyć **lokalizacji** parametru udostępniać tę wartość parametru możliwie zasoby, które są prawdopodobnie toobe w hello tej samej lokalizacji. Pozwala to zmniejszyć hello liczba użytkownicy są proszeni tooprovide informacji o lokalizacji.
* Unikaj używania parametr lub zmienna hello wersji interfejsu API dla typu zasobu. Właściwości zasobów i wartości może się różnić przez numer wersji. Gdy wersja interfejsu API hello ustawiono tooa parametr lub zmienna IntelliSense w edytorze kodu nie może określić hello poprawny schemat. Zamiast tego należy trwale kodować hello wersja interfejsu API w szablonie hello.

## <a name="variables"></a>Zmienne
Witaj następujące informacje mogą być pomocne podczas pracy ze zmiennymi:

* Użyj zmienne dla wartości, należy toouse więcej niż raz w szablonie. Jeśli wartość jest używana tylko raz, wartość ustalony sprawia, że Twoje tooread łatwiejsze szablonu.
* Nie można użyć hello [odwołania](resource-group-template-functions-resource.md#reference) funkcji w hello **zmienne** sekcji hello szablonu. Witaj **odwołania** funkcja pochodzi wartość stanu środowiska uruchomieniowego hello zasobu. Jednak zmienne są rozpoznawane podczas początkowej analizy szablonu hello hello. Tworzenia wartości, które wymagają hello **odwołania** funkcji bezpośrednio w hello **zasobów** lub **generuje** sekcji hello szablonu.
* Obejmują zmienne dla nazw zasobów, które muszą być unikatowe, zgodnie z opisem w [nazw zasobów](#resource-names).
* Zmienne można grupować w obiektów złożonych. Użyj hello **variable.subentry** format tooreference wartości z obiektu złożonego. Grupowania zmiennych może ułatwić śledzenie powiązanych zmiennych. Zwiększa czytelność hello szablonu. Oto przykład:
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > Obiekt złożony nie może zawierać wyrażenia, który odwołuje się do wartości z obiektu złożonego. W tym celu zdefiniowane osobnej zmiennej.
   > 
   > 
   
     Przykłady zaawansowanych za pomocą obiektu złożonego jako zmiennych, zobacz [udostępniania stanu w szablonach usługi Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="resources"></a>Zasoby
Hello następujące informacje mogą być przydatne podczas pracy z zasobami:

* toohelp innych uczestników zrozumienie przeznaczenia hello hello zasobu, należy określić **komentarze** dla każdego zasobu w szablonie hello:
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* Można użyć znaczników tooadd metadanych tooresources. Użyj metadanych tooadd informacji o zasobach. Na przykład można dodać szczegółów rozliczeń toorecord metadanych dla zasobu. Aby uzyskać więcej informacji, zobacz [używanie tagów tooorganize zasobów platformy Azure](resource-group-using-tags.md).
* Jeśli używasz *publiczny punkt końcowy* w szablonie (np. Azure Blob magazynu publiczny punkt końcowy), *czy nie kodowane* hello przestrzeni nazw. Użyj hello **odwołania** toodynamically funkcja pobrać hello przestrzeni nazw. Można użyć tego podejścia toodeploy hello szablonu toodifferent publicznej przestrzeni nazw środowiskach bez ręcznej zmiany punktu końcowego hello w szablonie hello. Ustaw toohello wersji interfejsu API hello tej samej wersji, używanego dla konta magazynu hello w szablonie:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Jeśli konto magazynu hello jest wdrażana w hello tego samego szablonu, który tworzysz, nie trzeba przestrzeń nazw dostawcy hello toospecify odwołanie hello zasobów. Jest to hello uproszczony składni:
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Jeśli masz inne wartości w szablonie, które są skonfigurowane toouse publicznej przestrzeni nazw, zmień wartości tych tooreflect hello sam **odwołania** funkcji. Na przykład można ustawić hello **storageUri** właściwości profilu diagnostyki maszyny wirtualnej hello:
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   Możesz także odwoływać się do istniejącego konta magazynu, który znajduje się w innej grupie zasobów:

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Przypisz publicznego maszyny wirtualnej tooa adresy IP tylko wtedy, gdy aplikacja wymaga on. tooconnect tooa maszyny wirtualnej (VM) do debugowania lub zarządzania lub celów administracyjnych, użyj reguły NAT ruchu przychodzącego, Brama sieci wirtualnej lub jumpbox.
   
     Aby uzyskać więcej informacji o podłączaniu toovirtual maszyny zobacz:
   
   * [Uruchamianie maszyn wirtualnych dla architektury N-warstwowa na platformie Azure](../guidance/guidance-compute-n-tier-vm.md)
   * [Konfigurowanie dostępu do usługi WinRM dla maszyn wirtualnych w usłudze Azure Resource Manager](../virtual-machines/windows/winrm.md)
   * [Zezwalaj na tooyour dostępu zewnętrznego maszyny Wirtualnej za pomocą hello portalu Azure](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [Zezwalaj na tooyour dostępu zewnętrznego maszyny Wirtualnej za pomocą programu PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Zezwalaj na tooyour dostępu zewnętrznego maszyny Wirtualnej systemu Linux przy użyciu wiersza polecenia platformy Azure](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Witaj **domainNameLabel** właściwości dla publicznych adresów IP muszą być unikatowe. Witaj **domainNameLabel** wartość musi mieć długość od 3 do 63 znaków i reguły hello określonego przez tego wyrażenia regularnego: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Ponieważ hello **uniqueString** funkcja generuje ciąg, który jest 13 znaków hello **dnsPrefixString** parametr jest ograniczona too50 znaków:

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* Po dodaniu hasła tooa niestandardowe rozszerzenie skryptu Użyj hello **commandToExecute** właściwości w hello **protectedSettings** właściwości:
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > tooensure, że hasła są szyfrowane, gdy są one przekazywane jako parametry tooVMs i rozszerzenia, użyj hello **protectedSettings** właściwości hello odpowiednich rozszerzeń.
   > 
   > 

## <a name="outputs"></a>dane wyjściowe
Jeśli używasz publiczne adresy IP szablonu toocreate obejmują **generuje** sekcja, która zwraca szczegóły hello adresu IP i hello pełną nazwę domeny (FQDN). Po wdrożeniu można użyć danych wyjściowych wartości tooeasily pobranie szczegółów dotyczących publicznych adresów IP i nazwy FQDN. Podając odniesienie hello zasobów, użyj wersji hello interfejsu API użytą toocreate go: 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>Jednego szablonu, a zagnieżdżone szablony
toodeploy rozwiązania, można użyć jednego szablonu lub szablonu głównego z wielu szablonów zagnieżdżonych. Zagnieżdżone szablony są wspólne dla bardziej zaawansowanych scenariuszy. Przy użyciu zapewnia szablon zagnieżdżony, tekst hello następujące korzyści:

* Można podzielić rozwiązania do elementów docelowych.
* Zagnieżdżone szablony z różnych szablonów głównego można użyć ponownie.

Jeśli wybierzesz toouse zagnieżdżone szablony hello następujące wytyczne może pomóc normalizacji projektu szablonu. Niniejsze wytyczne dotyczą [wzorce projektowania szablonów usługi Azure Resource Manager](best-practices-resource-manager-design-templates.md). Zaleca się projekt, który ma hello następujące szablony:

* **Główny szablon** (azuredeploy.json). Na użytek hello parametrów wejściowych.
* **Udostępnione zasoby szablonu**. Użyj toodeploy udostępnionych zasobów korzystających z innych zasobów (na przykład wirtualnych sieci i dostępność zestawy). Użyj hello **dependsOn** tooensure wyrażenia, że ten szablon jest wdrażany przed innych szablonów.
* **Opcjonalne zasoby szablonu**. Użyj tooconditionally wdrażanie zasobów na podstawie parametru (na przykład jumpbox).
* **Szablon elementu członkowskiego zasobów**. Każdy typ wystąpienie w warstwie aplikacji ma własny konfiguracji. W ramach warstwy można zdefiniować typy innego wystąpienia. (Na przykład hello pierwsze wystąpienie jest tworzony klaster, i dodatkowe wystąpienia są dodawane toohello istniejącego klastra) Każdy typ wystąpienia ma własny szablon wdrożenia.
* **Skrypty**. Powszechnie wielokrotnego użytku skrypty są stosowane do każdego wystąpienia typu (na przykład, inicjowanie i formatowanie dodatkowe dyski). Niestandardowych skryptów utworzonych w celu dostosowania określonych są różne, na podstawie hello wystąpienia typu.

![Szablon zagnieżdżony](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

Aby uzyskać więcej informacji, zobacz [używać szablonów połączonych z usługą Azure Resource Manager](resource-group-linked-templates.md).

## <a name="conditionally-link-toonested-templates"></a>Warunkowo link toonested szablonów
Można użyć parametru tooconditionally łącze toonested szablonów. Parametr Hello staje się częścią hello identyfikatora URI dla szablonu hello:

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>Format szablonu
Toopass dobrym rozwiązaniem jest szablonu przez moduł weryfikacji JSON. Moduł weryfikacji ułatwia Usuń nadmiarowe przecinkami, nawiasy i nawiasy, które może spowodować wystąpienie błędu podczas wdrażania. Spróbuj [JSONLint](http://jsonlint.com/) lub pakiet linter dla Ulubione edycji środowiska (Sublime tekstu Visual Studio Code, Atom, Visual Studio).

Istnieje również tooformat dobrze czy kod JSON w celu zwiększenia czytelności. Pakiet programu formatującego JSON można użyć dla Edytora lokalnych. W programie Visual Studio, tooformat hello dokumentu, naciśnij klawisz **Ctrl + K, Ctrl + D**. W programie Visual Studio Code, naciśnij klawisz **Alt + Shift + F**. Edytor lokalnych nie formatuje hello dokumentu, można użyć [online program formatujący](https://www.bing.com/search?q=json+formatter).

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać wskazówki dotyczące projektowania rozwiązania dla maszyn wirtualnych, zobacz [Uruchom Maszynę wirtualną systemu Windows na platformie Azure](../guidance/guidance-compute-single-vm.md) i [Uruchom Maszynę wirtualną systemu Linux na platformie Azure](../guidance/guidance-compute-single-vm-linux.md).
* Aby uzyskać instrukcje na temat konfigurowania konta magazynu, zobacz [Lista kontrolna wydajności i skalowalności magazynu Azure](../storage/common/storage-performance-checklist.md).
* toolearn dotyczące wykorzystania tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise: ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

