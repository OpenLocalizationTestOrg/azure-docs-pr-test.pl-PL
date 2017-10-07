---
title: "Przegląd dostawcy zasobów aaaNetwork | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello nowego dostawcy zasobów sieciowych w systemie Azure Resource Manager"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a>Dostawca zasobów sieciowych
Podstawa w bieżącej sukcesu firmy, jest hello toobuild możliwości zarządzania aplikacjami pamiętać sieci dużą skalę w sposób agile, elastyczne, bezpieczne i repeatable. Usługa Azure Resource Manager umożliwia toocreate można takich aplikacji, jako pojedynczą kolekcję zasobów w grupach zasobów. Takie zasoby są zarządzane przez różnych dostawców zasobów w obszarze usługi Resource Manager.

Usługa Azure Resource Manager zależy od zasobu różnych dostawców tooprovide dostęp do tooyour zasobów. Istnieją trzy dostawców zasobów głównego: sieci, magazynu i zasobów obliczeniowych. W tym dokumencie omówiono hello właściwości i zalet hello dostawcy zasobów sieciowych, w tym:

* **Metadane** — można dodać tooresources informacji przy użyciu tagów. Znaczniki mogą być używane tootrack wykorzystania zasobów między grupami zasobów i subskrypcje.
* **Większą kontrolę nad siecią** — są luźno powiązane z zasobów sieciowych i sterować nimi w sposób bardziej szczegółowego. Oznacza to, że masz większą elastyczność w zarządzaniu hello zasobów sieciowych.
* **Szybsze konfiguracji** — ponieważ są luźno powiązane z zasobów sieciowych, można tworzyć i organizowania zasobów sieciowych równolegle. Ma to znaczne zmniejszoną ilość czasu konfiguracji.
* **Kontroli dostępu opartej na rolach** -RBAC zawiera domyślne role, z określonego zakresu zabezpieczeń, w przypadku tworzenia hello tooallowing dodanie ról niestandardowych do bezpiecznego zarządzania.
* **Łatwiejsze zarządzanie i wdrażanie** — jest łatwiejsze toodeploy i zarządzania aplikacjami, ponieważ można całego stosu aplikacji można utworzyć jako pojedynczą kolekcję zasobów w grupie zasobów. I szybsze toodeploy, ponieważ po prostu zapewniając ładunek JSON szablonu można wdrożyć.
* **Dostosowywanie szybkie** — można użyć szablonów deklaratywne stylu tooenable powtarzalnych i szybkiego dostosowywania wdrożeń.
* **Dostosowywanie powtarzalne** — można użyć szablonów deklaratywne stylu tooenable powtarzalnych i szybkiego dostosowywania wdrożeń.
* **Interfejsy zarządzania** — można użyć dowolnego z następujących interfejsów toomanage hello zasobów:
  * REST API oparty na
  * PowerShell
  * Zestaw SDK .NET
  * Zestaw Node.JS SDK
  * Zestaw SDK Java
  * Interfejs wiersza polecenia platformy Azure
  * Portal w wersji zapoznawczej
  * Język szablonu usługi Resource Manager

## <a name="network-resources"></a>Zasoby sieciowe
Możesz teraz zarządzać zasobów sieciowych niezależnie, zamiast je zarządzanych za pomocą obliczeń jednego zasobu (maszyny wirtualnej). Dzięki temu wyższego poziomu bezpieczeństwa i elastyczność oraz elastyczność w tworzenie infrastruktury złożone i dużej skali, w grupie zasobów.

Widok koncepcyjny Przykładowe wdrożenie obejmujące wielowarstwowych aplikacji znajduje się poniżej. Każdy zasób, który zostanie wyświetlony, takie jak karty sieciowe, publicznych adresów IP i maszyn wirtualnych, można zarządzać niezależnie.

![Model zasobów sieciowych](./media/resource-groups-networking/Figure2.png)

Każdy zasób zawiera zbiór wspólnych właściwości i ich indywidualnych właściwości. wspólne właściwości Hello są:

| Właściwość | Opis | Przykładowe wartości |
| --- | --- | --- |
| **Nazwa** |Nazwa zasobu unikatowy. Każdy typ zasobu ma własną ograniczenia nazewnictwa. |NIC01 PIP01, VM01, |
| **location** |Region platformy Azure, w których hello zasób znajduje się |westus, eastus |
| **Identyfikator** |Unikatowy identyfikator URI na podstawie |/Subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

Możesz sprawdzić hello poszczególnych właściwości zasobów w poniższych sekcjach hello.

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a>Interfejsy zarządzania
Możesz zarządzać zasobami sieci Azure przy użyciu różnych interfejsów. W tym dokumencie firma Microsoft będzie skupić się na tow te interfejsy: interfejs API REST i szablony.

### <a name="rest-api"></a>Interfejs API REST
Jak wspomniano wcześniej, można zarządzać za pośrednictwem różnych interfejsy, w tym interfejsu API REST, zestawu SDK programu .NET, Node.JS SDK, zestaw SDK Java, programu PowerShell, interfejsu wiersza polecenia, portalu Azure i szablony zasobów sieciowych.

Witaj interfejsu API Rest jest zgodna z toohello Specyfikacja protokołu HTTP 1.1. Hello ogólną strukturę URI hello interfejsu API jest przedstawiony poniżej:

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

I reprezentują parametry hello w nawiasach klamrowych hello następujące elementy:

* **Identyfikator subskrypcji** — identyfikator subskrypcji platformy Azure.
* **przestrzeń nazw dostawcy zasobów** — przestrzeń nazw dla dostawca hello jest używany. wartość Hello dostawcy zasobów sieciowych hello jest *Microsoft.Network*.
* **Nazwa regionu** — nazwa regionu Azure hello

Witaj następujących metod HTTP obsługiwanych podczas wprowadzania toohello wywołania interfejsu API REST:

* **Umieść** — używane toocreate zasobów danego typu, modyfikować właściwości zasobu lub zmień skojarzenia między zasobami.
* **Pobierz** — używane informacje tooretrieve elastycznie zasobu.
* **Usuń** — używane toodelete istniejącego zasobu.

Zarówno hello żądania i odpowiedzi jest zgodna z format ładunku JSON tooa. Aby uzyskać więcej informacji, zobacz [interfejsów API usługi Azure Resource Management](https://msdn.microsoft.com/library/azure/dn948464.aspx).

### <a name="resource-manager-template-language"></a>Język szablonu usługi Resource Manager
Dodanie toomanaging zasobów imperatively (za pośrednictwem interfejsów API lub zestawu SDK) można również użyć deklaratywne programowania toobuild styl i zarządzania zasobami sieci przy użyciu hello język szablonu usługi Resource Manager.

Poniższe przykładowe reprezentację szablonu —

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

Szablon Hello jest głównie opisu JSON zasobów hello i wartości wystąpienia hello wprowadzonym za pomocą parametrów. w poniższym przykładzie Hello mogą być używane toocreate sieć wirtualną przy użyciu podsieci 2.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

Masz hello opcja podania wartości parametrów hello ręcznie, przy użyciu szablonu, lub można użyć pliku parametrów. Witaj w poniższym przykładzie przedstawiono możliwe zestaw używany z szablonem hello powyżej toobe wartości parametru:

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


główne zalety Hello za pomocą szablonów są następujące:

* Można tworzyć złożone infrastruktury w grupie zasobów w stylu deklaratywne. Witaj aranżacji tworzenia zasobów hello, w tym zarządzania zależności jest obsługiwany przez Menedżera zasobów.
* Witaj infrastruktury można tworzyć w sposób powtarzalny w różnych regionach i w obrębie regionu, zmieniając po prostu parametrów.
* Styl deklaratywne Hello prowadzi tooshorter czas realizacji w tworzeniu szablonów hello i wdrażania infrastruktury hello.

Przykładowe szablonów, zobacz [szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates).

Aby uzyskać więcej informacji na powitania język szablonu usługi Resource Manager, zobacz [język szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Przykładowy szablon Hello powyżej używa hello sieci wirtualnej i zasoby podsieci. Brak innych zasobów sieciowych, których można używać wymienione poniżej:

### <a name="using-a-template"></a>Przy użyciu szablonu
TooAzure usługi z szablonu można wdrożyć przy użyciu programu PowerShell, AzureCLI, lub wykonując toodeploy kliknij pozycję z witryny GitHub. toodeploy usługi z szablonu w witrynie GitHub, wykonaj hello następujące kroki:

1. Otwórz plik template3 hello z usługi GitHub. Na przykład otwórz [sieci wirtualnej z dwoma podsieciami](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).
2. Polecenie **wdrażanie tooAzure**, a następnie zaloguj się na toohello portalu Azure przy użyciu poświadczeń.
3. Sprawdź hello szablonu, a następnie kliknij przycisk **zapisać**.
4. Kliknij przycisk **Edytuj parametry** i wybierz lokalizację, takich jak *zachodnie stany USA*, hello sieci wirtualnej i podsieci.
5. W razie potrzeby zmień hello **prefiks adresu** i **SUBNETPREFIX** parametry, a następnie kliknij przycisk **OK**.
6. Kliknij przycisk **wybierz grupę zasobów** a następnie kliknij polecenie hello grupa zasobów ma tooadd hello w sieci wirtualnej i podsieci z. Alternatywnie można utworzyć nową grupę zasobów, klikając **lub utworzyć nowy**.
7. Kliknij przycisk **Utwórz**. Zwróć uwagę, hello wyświetlanie kafelka **wdrażania szablonu inicjowania obsługi administracyjnej**. Po ukończeniu wdrażania hello, zobaczysz ekran podobny tooone poniżej.

![Przykładowe wdrożenie szablonu](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>Następne kroki
[Język szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)

[Sieć platformy Azure — często używane szablony](https://github.com/Azure/azure-quickstart-templates)

[Usługa Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md)

[Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

