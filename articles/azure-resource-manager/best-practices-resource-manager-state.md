---
title: "złożone wartości aaaPass między szablonami platformy Azure | Dokumentacja firmy Microsoft"
description: "Przedstawia zalecane podejścia do korzystania z usługi Azure Resource Manager szablony i połączone przy użyciu danych o stanie tooshare obiektów złożonych."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>Udostępnianie tooand stanu z szablonów usługi Azure Resource Manager
W tym temacie przedstawiono najlepsze rozwiązania dotyczące zarządzania i udostępniania stanu w szablonach. Witaj parametry i zmienne, które przedstawiono w tym temacie przedstawiono przykłady typu hello obiektów można zdefiniować tooconveniently organizowanie wymagań dotyczących wdrożenia. W tych przykładach można zaimplementować obiekty z wartości właściwości odpowiednich dla danego środowiska.

Ten temat jest częścią większej oficjalny dokument. Pobierz hello tooread pełnej papier [światowej klasy zasobu menedżera szablony zagadnienia i sprawdzonych rozwiązań](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

## <a name="provide-standard-configuration-settings"></a>Określ ustawienia konfiguracji standardowej
Zamiast oferują szablon, który zapewnia elastyczność całkowitej i niezliczonych zmian, wspólnego wzorca jest tooprovide wybór znanych konfiguracji. W efekcie, użytkownicy mogą wybrać standardowe rozmiary obrazów na koszulki, takich jak piaskownicy, małych, średnich i dużych. Inne przykłady rozmiary obrazów na koszulki są ofert produktów, takich jak community edition lub enterprise edition. W innych przypadkach może być konfiguracje specyficznego dla obciążenia technologii — takie jak ograniczyć mapy lub nie sql.

Złożone obiekty możesz tworzyć zmiennych, które zawierają zbiory danych, czasami znana jako "zbiory właściwości" i użyj deklaracja zasobów hello toodrive danych w szablonie. Takie podejście zapewnia dobre, znanej konfiguracji o różnych rozmiarach, które są wstępnie skonfigurowane dla klientów. Bez znanych konfiguracji użytkowników hello szablonu musi określić rozmiaru klastra na ich własnych, współczynnik w powiązanych zasobów platformy i czy matematyczne tooidentify hello wynikowa partycjonowanie konta magazynu i innych zasobów (ze względu na rozmiar toocluster i ograniczenia zasobów). Ponadto toomaking lepsze środowisko dla powitania klienta kilka znanych konfiguracji są łatwiejsze toosupport i ułatwiają dostarczanie wyższego poziomu gęstości.

powitania po przykładzie pokazano, jak toodefine zmiennych, które zawierają złożone obiekty odpowiadające kolekcji danych. kolekcje Hello zdefiniuj wartości, które są używane dla rozmiaru maszyny wirtualnej, ustawienia sieciowe, ustawień systemu operacyjnego i ustawienia dostępności.

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

Zwróć uwagę, że hello **tshirtSize** zmiennej łączy Rozmiar koszulki hello udostępnianej parametr (**małych**, **średni**, **duży**) tekst toohello **tshirtSize**. Ten rozmiar koszulki używany tej zmiennej tooretrieve hello skojarzony obiekt złożony zmiennej.

Następnie można odwoływać się tych zmiennych w dalszej części hello szablonu. Witaj możliwości tooreference o nazwie — zmienne i ich właściwości upraszcza składni szablonu hello i umożliwia łatwe toounderstand kontekstu. Poniższy przykład Hello definiuje toodeploy zasobów za pomocą obiektów hello przedstawione wcześniej tooset wartości. Na przykład hello rozmiar maszyny Wirtualnej jest ustawiana przez pobierania wartości hello `variables('tshirtSize').vmSize` podczas hello wartość na rozmiar dysku hello są pobierane z `variables('tshirtSize').diskSize`. Ponadto hello identyfikatora URI dla połączonych szablonu jest ustawiony z wartością hello `variables('tshirtSize').vmTemplate`.

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a>Przekaż szablon tooa stanu
Możesz udostępniać stanu do szablonu za pomocą parametrów, które zapewniają bezpośrednio podczas wdrażania.

Witaj następujące parametry tabeli listy najczęściej używanych w szablonach.

| Nazwa | Wartość | Opis |
| --- | --- | --- |
| location |Ciąg z listy ograniczone regiony platformy Azure |Lokalizacja Hello wdrożonym hello zasobów. |
| storageAccountNamePrefix |Ciąg |Unikatową nazwę DNS hello rozmieszczenia dysków hello wirtualna konta magazynu |
| domainName |Ciąg |Nazwa domeny hello publicznie jumpbox maszyny Wirtualnej w formacie hello: **{domainName}. { Lokalizacja}.cloudapp.com** na przykład: **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |Ciąg |Nazwa użytkownika dla hello maszyny wirtualne |
| adminPassword |Ciąg |Hasło dla hello maszyny wirtualne |
| tshirtSize |Rozmiary obrazów na koszulki oferowane ciąg z listy ograniczone |Witaj o nazwie tooprovision rozmiar jednostki skalowania. Na przykład "Małe", "Medium", "Duże" |
| virtualNetworkName |Ciąg |Nazwa hello sieci wirtualnej hello konsumenta chce toouse. |
| enableJumpbox |Ciąg z listą ograniczone (włączone/wyłączone) |Parametr, który identyfikuje czy tooenable jumpbox hello środowiska. Wartości: "enabled", "wyłączone" |

Witaj **tshirtSize** parametru użytego w poprzedniej sekcji hello jest zdefiniowany jako:

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a>Przekaż szablony toolinked stanu
Podczas łączenia z toolinked szablony, można często używać różnych statyczne i wygenerować zmienne.

### <a name="static-variables"></a>Zmienne statyczne
Zmienne statyczne są często wartości podstawowe tooprovide używane, takie jak adresy URL, które są używane w szablonie.

W hello następującego fragmentu szablonu `templateBaseUrl` Określa lokalizację głównego hello hello szablonu w witrynie GitHub. Witaj w następnym wierszu tworzy nową zmienną `sharedTemplateUrl` który łączy hello podstawowego adresu URL hello znanej nazwy szablonu zasobów udostępnionych hello. Poniżej tego wiersza, zmienną obiekt złożony jest używane toostore Rozmiar koszulki, który hello podstawowego adresu URL toohello połączonych znane lokalizacji szablonu konfiguracji i przechowywane w hello `vmTemplate` właściwości.

Witaj zaletą tej metody jest zmiana lokalizacji szablonu hello tylko potrzeby toochange hello statyczna zmienna w jednym miejscu, która przechodzi on w całym szablony hello połączone.

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a>Wygenerowany zmiennych
Dodanie toostatic zmienne kilku zmiennych są generowane dynamicznie. W tej sekcji wymieniono niektóre typy typowe hello wygenerowanego zmiennych.

#### <a name="tshirtsize"></a>tshirtSize
Znasz tej zmiennej wygenerowanych w powyższych przykładach hello.

#### <a name="networksettings"></a>networkSettings
W hello wydajność, możliwości lub szablon rozwiązania zakresami end-to-end, połączone szablony zwykle Utwórz zasoby, które istnieją w sieci. Jednym z podejść prostego jest toouse ustawień sieciowych toostore obiekt złożony i przekazać je toolinked szablonów.

Przykład komunikacji ustawienia sieciowe są widoczne poniżej.

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a>availabilitySettings
Zasoby utworzone w szablonach połączonego często są umieszczane w zestawie dostępności. W hello poniższy przykład nazwa zbioru dostępności hello określono również hello domeny błędów i toouse liczby domen aktualizacji.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

Jeśli potrzebujesz wiele zestawów dostępności (na przykład, jeden dla węzłów głównych) i drugi dla węzłów danych, można użyć jako prefiksu nazwy, określ wiele zestawów dostępności lub wykonaj modelu hello przedstawiona wcześniej do utworzenia zmiennej w określonym Rozmiar koszulki.

#### <a name="storagesettings"></a>storageSettings
Szczegóły magazynu często są współużytkowane z szablonami połączony. W poniższym przykładzie hello *storageSettings* obiektu zawiera szczegółowe informacje o hello nazwy konta i kontener magazynu.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
Z szablonami połączonego toopass systemu operacyjnego ustawienia toovarious węzłów typów może być konieczne w innej konfiguracji znanych typów. Obiekt złożony jest łatwy sposób toostore i udziału informacje dotyczące systemu operacyjnego i umożliwia łatwiejsze toosupport wiele wyborów systemu operacyjnego dla wdrożenia.

Witaj poniższy przykład przedstawia dla obiekt *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
Generowana zmienna, *machineSettings* jest obiekt złożony, zawierające kombinację zmiennych core dla tworzenia maszyny Wirtualnej. zmienne Hello obejmują nazwa użytkownika administratora i hasła, prefiks dla nazw maszyn wirtualnych hello i odwołanie do obrazu systemu operacyjnego.

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

Należy pamiętać, że *osImageReference* pobiera hello wartości z hello *osSettings* zmiennej zdefiniowanej w szablonie głównym hello. Oznacza to, że można łatwo zmienić hello systemu operacyjnego dla maszyny Wirtualnej — całkowicie lub, w zależności od preferencji powitania klienta szablonu.

#### <a name="vmscripts"></a>vmScripts
Witaj *vmScripts* obiektu zawiera szczegółowe informacje o hello toodownload skrypty i wykonywanie w wystąpieniu maszyny Wirtualnej, w tym odniesienia i wewnętrznego. Poza odwołaniami obejmują hello infrastruktury.
Wewnątrz odwołania zawierać hello zainstalowane oprogramowanie i konfiguracji.

Użyj hello *scriptsToDownload* właściwości toolist hello skrypty toohello toodownload maszyny Wirtualnej. Ten obiekt zawiera również argumenty wiersza toocommand odwołania dla różnego rodzaju akcje. Dostępne są akcje wykonywane hello domyślnej instalacji dla każdego indywidualnego węzła, instalacja wykonywana po wdrożeniu wszystkich węzłów i dodatkowych skryptów, które mogą być określone tooa danego szablonu.

W tym przykładzie jest używany szablon toodeploy bazy danych MongoDB, co wymaga kryterium toodeliver wysokiej dostępności. Witaj *arbiterNodeInstallCommand* został dodany za*vmScripts* tooinstall hello kryterium.

sekcja zmienne Hello jest, gdzie znaleźć zmiennych hello, definiujące hello określony tekst tooexecute hello skryptu hello odpowiednie wartości.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>Zwraca stan z szablonu
Nie tylko można przekazywania danych do szablonu, możesz również udostępnianie danych wstecz toohello wywoływania szablonu. W hello **generuje** sekcji połączonych szablonu, możesz podać pary klucz wartość, które mogą być używane w szablonie źródłowym hello.

Witaj poniższy przykład przedstawia sposób toopass hello generowane w szablonie połączonego prywatnego adresu IP.

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

W szablonie głównym hello można użyć danych z hello następującej składni:

    "[reference('master-node').outputs.masterip.value]"

Można użyć tego wyrażenia w sekcji danych wyjściowych hello lub sekcja zasobów hello hello głównym szablonu. Nie można użyć wyrażenia hello w sekcji zmiennych hello, ponieważ zależy od hello stan czasu wykonywania. tooreturn wartość tego parametru szablonu głównego hello, użyj:

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

Na przykład za pomocą hello generuje części szablonu połączonego tooreturn dysków z danymi dla maszyny wirtualnej, zobacz [tworzenie wielu dysków danych maszyny wirtualnej](resource-group-create-multiple.md).

## <a name="define-authentication-settings-for-virtual-machine"></a>Zdefiniuj ustawienia uwierzytelniania dla maszyny wirtualnej
Witaj można użyć tego samego wzorca wcześniej ustawień uwierzytelniania hello toospecify ustawienia konfiguracji dla maszyny wirtualnej. Parametr do przekazania do tworzenia hello typu uwierzytelniania.

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

Należy dodać zmienne dla hello różnymi typami uwierzytelniania i zmiennej toostore, jaki typ jest używany dla tego wdrożenia na podstawie wartości hello hello parametru.

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

Podczas definiowania hello maszyny wirtualnej, ustaw hello **osProfile** toohello zmiennej został utworzony.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn o hello części szablonu hello [Authoring Azure Resource Manager szablonów](resource-group-authoring-templates.md)
* toosee hello funkcje, które są dostępne w ramach szablonu, zobacz [funkcje szablonów usługi Azure Resource Manager](resource-group-template-functions.md)
