---
title: "kolejność wdrożenia aaaSet zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób wdrożenia tooset jednego zasobu jako zależny od innego zasobu podczas wdrażania tooensure zasobów w odpowiedniej kolejności hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Zdefiniuj kolejność hello wdrażania zasobów w szablonach usługi Azure Resource Manager
Dla danego zasobu może być inne zasoby, które muszą istnieć przed wdrożeniem hello zasobów. Na przykład serwer SQL musi istnieć przed podjęciem próby wykonania toodeploy bazy danych SQL. Należy zdefiniować tę relację oznaczając jednego zasobu jako zależne hello innego zasobu. Definiowanie zależności z hello **dependsOn** elementu, lub za pomocą hello **odwołania** funkcji. 

Menedżer zasobów ocenia hello zależności między zasobami i wdraża je w porządku zależnych. Jeśli zasoby nie są zależne od siebie, Menedżer zasobów wdraża je równolegle. Wystarczy toodefine zależności zasobów, które są wdrażane w hello tego samego szablonu. 

## <a name="dependson"></a>dependsOn
W szablonie hello dependsOn element umożliwia toodefine jeden zasób, w zależności od jednego lub więcej zasobów. Wartość może być rozdzielana przecinkami lista nazw zasobów. 

Witaj poniższy przykład przedstawia zestaw skali maszyny wirtualnej, która zależy od usługi równoważenia obciążenia, sieć wirtualną i pętli, które tworzy wiele kont magazynu. Poniższy przykład hello te inne zasoby nie są wyświetlane, ale powinny tooexist w innym miejscu w szablonie hello.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

Zawiera zależność hello poprzedzających przykład, hello zasobów, które są tworzone przez pętlę kopiowania o nazwie **storageLoop**. Na przykład zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).

Podczas definiowania zależności, mogą obejmować hello zasobów dostawcy przestrzeń nazw i zasobów typu tooavoid niejednoznaczności. Na przykład tooclarify, które usługa równoważenia obciążenia i sieć wirtualna, która może być hello nazwy takie same jak inne zasoby, hello Użyj następującego formatu:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

Może być odchylona toouse dependsOn toomap relacje między zasobami, jest ważne toounderstand Dlaczego podczas jej wykonywania. Na przykład toodocument jak zasoby są połączone ze sobą, dependsOn nie jest hello podejście. Nie można wykonać zapytania, które zasoby zostały zdefiniowane w elemencie dependsOn powitania po wdrożeniu. Za pomocą dependsOn, możesz potencjalnie wpływ czas wdrażania, ponieważ Menedżer zasobów nie wdraża równoległych dwa zasoby, które mają zależności. Zamiast tego użyj toodocument relacje między zasobami, [łączenia zasobów](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Zasoby podrzędne
Właściwość zasobów Hello pozwala toospecify podrzędne zasoby, które są powiązane toohello zasobów definiowanego. Zasoby podrzędne może być tylko zdefiniowanych głębokości pięciu poziomów. Należy utworzyć toonote niejawne zależności nie będący między zasobu podrzędnego i zasobu nadrzędnego hello. Jeśli konieczne hello wdrożyć po zasobu nadrzędnego hello toobe zasobów podrzędnych, musi jawnie określać tej zależności z hello dependsOn właściwości. 

Każdy zasób nadrzędnego akceptuje tylko niektóre typy zasobów jako zasoby podrzędne. zaakceptowane Hello typów zasobów są określone w hello [schematu szablonu](https://github.com/Azure/azure-resource-manager-schemas) hello zasobu nadrzędnego. Witaj Nazwa typu zasobu podrzędnego obejmuje hello Nazwa typu zasobu nadrzędnego hello, takich jak **Microsoft.Web/sites/config** i **Microsoft.Web/sites/extensions** są zasobami podrzędnymi zarówno hello  **Microsoft.Web/sites**.

Witaj poniższy przykład przedstawia programu SQL server i bazy danych SQL. Zwróć uwagę, zdefiniowania jawne zależności między hello SQL database i programu SQL server, nawet jeśli hello bazy danych jest elementem podrzędnym powitania serwera.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>Odwołanie do funkcji
Witaj [odwołania funkcji](resource-group-template-functions-resource.md#reference) umożliwia tooderive wyrażenie jego wartość z innych pary nazw i wartości JSON lub zasobów środowiska uruchomieniowego. Wyrażenia odwołania niejawnie deklaruje, że jeden zasób jest zależny od innego. format Ogólne Hello jest:

```json
reference('resourceName').propertyPath
```

W hello poniższy przykład punktu końcowego usługi CDN jawnie zależy od hello profilu CDN i niejawnie zależy od aplikacji sieci web.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

Można używać tego elementu albo hello zależności toospecify element dependsOn, ale nie ma potrzeby toouse zarówno dla hello tego samego zasobu zależnego. Jeśli to możliwe, należy użyć tooavoid niejawne odwołanie Dodawanie niepotrzebnych zależności.

toolearn więcej, zobacz [odwołania funkcja](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Zalecenia dotyczące ustawiania zależności

Podczas podejmowania decyzji o jakie tooset zależności, użyj hello następujące wytyczne:

* Jak to możliwe, należy ustawić jako kilka zależności.
* Ustaw zasobu podrzędnego jako zależy od jego zasobu nadrzędnego.
* Użyj hello **odwołania** funkcji tooset niejawne zależności między zasobami, które wymagają tooshare właściwości. Nie dodawaj jawne zależności (**dependsOn**) podczas niejawnego zależności został już zdefiniowany. Takie podejście zmniejsza ryzyko hello niepotrzebnych zależności. 
* Ustaw zależność zasobu nie może być **utworzony** bez funkcji z innego zasobu. Nie należy ustawiać zależność, jeśli zasoby hello komunikować się tylko po wdrożeniu.
* Let zależności cascade bez jawnie ich ustawienia. Na przykład maszyny wirtualnej zależy od interfejsu sieci wirtualnej, a interfejs sieci wirtualnej hello jest zależna od sieci wirtualnej i publiczne adresy IP. W związku z tym hello maszyny wirtualnej jest wdrożone po wszystkich trzech zasoby, ale nie ustawiaj jawnie hello maszyny wirtualnej jako zależne od wszystkich trzech zasobów. Takie podejście wyjaśnia, kolejność zależności hello i umożliwia łatwiejsze szablonu hello toochange później.
* Jeśli wartość można określić przed wdrożeniem, spróbuj wdrażanie zasobów hello bez zależności. Na przykład jeśli wartość konfiguracji musi hello nazwę innego zasobu, może być konieczne nie zależności. W tych wskazówkach nie zawsze działa, ponieważ niektóre zasoby Sprawdź istnienie hello hello innego zasobu. Jeśli wystąpi błąd, należy dodać zależności. 

Menedżer zasobów identyfikuje zależności cykliczne podczas walidacji szablonu. Jeśli zostanie wyświetlony komunikat o błędzie informujący, że istnieje zależność cykliczną, ocenić toosee Twojego szablonu, czy wszystkie zależności nie są wymagane i może zostać usunięta. Jeśli usuwanie zależności nie działa, można uniknąć zależności cykliczne przez przeniesienie niektórych operacji wdrażania do zasobów podrzędne, które są wdrażane po hello zasoby, które mają hello zależność cykliczną. Załóżmy na przykład wdrażasz dwóch maszyn wirtualnych, ale należy ustawić na każdej z nich, która odwołuje się toohello innych właściwości. Można je wdrożyć w hello w następującej kolejności:

1. vm1
2. maszyny vm2
3. Rozszerzenie na vm1 zależy od vm1 i maszyny vm2. rozszerzenie Hello ustawia wartości vm1, który otrzymuje od maszyny vm2.
4. Rozszerzenie maszyny vm2 zależy od vm1 i maszyny vm2. rozszerzenie Hello ustawia wartości maszyny vm2, który otrzymuje od vm1.

Uzyskać informacje o ocenie hello kolejność wdrażania i rozwiązywaniu problemów z błędami zależności, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Następne kroki
* toolearn dotyczące rozwiązywania problemów z zależności podczas wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn o tworzeniu szablonów usługi Azure Resource Manager, zobacz [tworzenia szablonów](resource-group-authoring-templates.md). 
* Aby uzyskać listę dostępnych funkcji hello w szablonie, zobacz [szablonu funkcji](resource-group-template-functions.md).

