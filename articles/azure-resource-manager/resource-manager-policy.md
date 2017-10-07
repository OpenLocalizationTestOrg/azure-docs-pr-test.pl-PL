---
title: "zasady zasobów aaaAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse usługi Azure Resource Manager zasady tooensure spójne zasobów właściwości są ustawione podczas wdrażania. Zasady można stosować na powitania grupy zasobów lub subskrypcji."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>Przegląd zasad zasobów
Zasady zasobów Włącz konwencje tooestablish dla zasobów w organizacji. Definiowanie Konwencji, można kontrolować koszty i zarządzania zasobami. Na przykład można określić, czy dozwolone są tylko niektóre typy maszyn wirtualnych. Alternatywnie można wymagać, że wszystkie zasoby mają określony tag. Zasady są dziedziczone przez wszystkie zasoby podrzędne. Jeśli zasady są stosowane tooa grupy zasobów, jest odpowiednie tooall hello zasobów w danej grupie zasobów.

Istnieją dwa toounderstand pojęcia dotyczące zasad:

* Definicja zasad - opisano wymuszenie zasad hello i jakie tootake akcji
* przypisania zasad - Zastosuj hello definicji tooa zakres zasad (subskrypcji lub grupy zasobów)

Ten temat koncentruje się na definicji zasad. Informacje o przypisywaniu zasad, zobacz [tooassign portalu Azure Użyj zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md) lub [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).

Zasady są oceniane podczas tworzenia i aktualizowania zasobów (PUT i poprawka operacji).

> [!NOTE]
> Obecnie zasad nie może oszacować typów zasobów, które nie obsługują tagi, typu i lokalizacji, takiej jak typ zasobu Microsoft.Resources/deployments hello. Ta obsługa zostanie dodana w przyszłości. problemy ze zgodnością z poprzednimi wersjami tooavoid, należy jawnie określić typ podczas tworzenia zasady. Na przykład zasady tag, która nie określa typy jest stosowana dla wszystkich typów. W takim przypadku wdrażania szablonu może zakończyć się niepowodzeniem, jeśli istnieje zagnieżdżonych zasobów, która nie obsługuje tagi, a typ zasobu wdrożenia hello dodano toopolicy oceny. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Czym się różni od RBAC?
Istnieje kilka podstawowych różnic między zasadami i kontroli dostępu opartej na rolach (RBAC). RBAC koncentruje się na **użytkownika** działań w innych zakresach. Na przykład dzięki czemu można zmieniać grupy zasobów toothat zmiany są dodawane toohello roli współautora dla grupy zasobów w zakresie hello potrzebne. Zasady koncentruje się na **zasobów** właściwości podczas wdrażania. Na przykład za pomocą zasad, można kontrolować hello typów zasobów, które mogą być udostępniane. Alternatywnie można ograniczyć lokalizacje hello, w których można udostępnić zasoby hello. W odróżnieniu od RBAC, zasady są domyślnie Zezwól jawne i odmawianie systemu. 

zasady toouse, użytkownik musi zostać uwierzytelniony za pośrednictwem RBAC. W szczególności, Twoje konto musi:

* `Microsoft.Authorization/policydefinitions/write`uprawnienie toodefine zasady
* `Microsoft.Authorization/policyassignments/write`uprawnienie tooassign zasady 

Te uprawnienia nie są uwzględnione w hello **współautora** roli.

## <a name="built-in-policies"></a>Wbudowane zasady

Platforma Azure udostępnia definicje zasad wbudowanych, których może zmniejszyć liczbę hello zasad masz toodefine. Przed kontynuowaniem definicje zasad, należy rozważyć, czy wbudowanych zasad już zawiera definicję hello, które są potrzebne. Definicje zasad wbudowany Hello są:

* Dozwolonych lokalizacji
* Typy zasobów dozwolonych
* Dozwolone konto magazynu jednostki SKU
* Dozwolone jednostki SKU maszyny wirtualnej
* Zastosowanie tagu i domyślne wartości
* Wymuszanie tagu i wartości
* Niedozwolone typy zasobów
* Wymaga programu SQL Server w wersji 12.0
* Wymagaj szyfrowania konta magazynu

Można przypisać dowolną z tych zasad za pomocą hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), lub [interfejsu wiersza polecenia Azure](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Struktura definicji zasad
Możesz użyć toocreate JSON definicji zasad. Definicja zasad Hello zawiera elementy dla:

* parameters
* Nazwa wyświetlana
* description
* Reguła zasad
  * Ocena logiczne
  * Efekt

Witaj poniższy przykład przedstawia zasadę, która ogranicza wdrożonym zasobów:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>Parametry
Przy użyciu parametrów upraszcza zarządzanie zasadami dzięki zmniejszeniu liczby hello definicje zasad. Zdefiniuj zasady dla właściwości zasobów (na przykład ograniczenie lokalizacji hello wdrożonym zasobów) i obejmują parametry w definicji hello. Następnie ponowne użycie tej definicji zasad dla różnych scenariuszy przez przekazywanie różne wartości (na przykład określenie jeden zestaw lokalizacji dla subskrypcji) podczas przypisywania hello zasady.

Deklarowanie parametrów, podczas tworzenia definicji zasad.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

Typ parametru Hello może być ciągiem lub tablicą. Właściwość metadanych Hello jest używana dla narzędzia, takie jak informacje przyjazną dla użytkownika toodisplay portalu Azure. 

W regule zasad hello możesz odwołania do parametrów z hello następującej składni: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Nazwę wyświetlaną i opis

Użyj hello **displayName** i **opis** tooidentify hello definicji zasad i podanie gdy jest używana w kontekście.

## <a name="policy-rule"></a>Reguła zasad

Reguła zasad Hello składa się z **Jeśli** i **następnie** bloków. W hello **Jeśli** bloku, należy zdefiniować co najmniej jeden warunek, które określają, kiedy hello zasady są wymuszane. Operatory logiczne toothese warunki można stosować tooprecisely zdefiniuj hello scenariusz dla zasad. W hello **następnie** bloku, zdefiniuj efekt hello spowodowany hello **Jeśli** warunki są spełnione.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Operatory logiczne
Operatory logiczne Hello obsługiwane są:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Witaj **nie** składni odwraca wynik hello hello warunku. Hello **wszystkie** składni (podobne toohello logicznej **i** operacji) wymaga wszystkie warunki toobe o wartości PRAWDA. Witaj **anyOf** składni (podobne toohello logicznej **lub** operacji) wymaga co najmniej jeden true toobe warunki.

Operatory logiczne można zagnieżdżać. powitania po przykładzie **nie** operacja, która jest zagnieżdżona w **wszystkie** operacji. 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>Warunki
warunek Hello czy **pola** spełnia określone kryteria. warunki Hello obsługiwane są:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Korzystając z hello **jak** warunku, możesz podać symbol wieloznaczny (*) w hello wartości.

Korzystając z hello **odpowiada** warunku, podaj `#` toorepresent cyfrę, `?` dla list i innych znaków toorepresent rzeczywiste znaku. Aby uzyskać przykłady, zobacz [stosowania zasad zasobów dla nazwy i tekst](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Pola
Warunki są utworzone za pomocą pola. Pole reprezentuje właściwości w ładunku żądania zasobów hello czyli używane toodescribe hello stanu typu zasobu hello.  

obsługiwane są następujące pola Hello:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* Aliasy właściwości — Aby uzyskać listę, zobacz [aliasy](#aliases).

### <a name="effect"></a>Efekt
Zasady obsługuje trzy rodzaje efekt — `deny`, `audit`, i `append`. 

* **Odmów** generuje zdarzenie w dzienniku inspekcji hello i kończy się niepowodzeniem hello żądania
* **Inspekcja** generuje to zdarzenie ostrzegawcze w dzienniku inspekcji, ale nie wystąpi niepowodzenie żądania hello
* **Dołącz** dodaje hello zdefiniowany zestaw pól toohello żądania 

Aby uzyskać **Dołącz**, musisz podać hello poniższe informacje:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

wartość Hello może być ciągiem lub obiekt do formatu JSON. 

## <a name="aliases"></a>Aliasy

Korzystając z właściwości aliasów tooaccess określonych właściwości dla typu zasobu. Aliasy Włącz toorestrict warunki lub wartości, jakie są dozwolone dla właściwości w zasobie. Każdy alias mapuje toopaths w różnych wersjach interfejsu API dla typu zasobu. Podczas oceny zasad aparat zasad hello pobiera hello właściwość ścieżki dla danej wersji interfejsu API.

**Microsoft.Cache/Redis**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Wartość określa, czy serwer Redis bez użycia protokołu ssl hello portu (6379) jest włączona. |
| Microsoft.Cache/Redis/shardCount | Ustaw liczbę hello toobe odłamków utworzone w pamięci podręcznej klastra Premium.  |
| Microsoft.Cache/Redis/sku.capacity | Określ rozmiar hello toodeploy pamięci podręcznej Redis hello.  |
| Microsoft.Cache/Redis/sku.family | Ustaw toouse rodziny SKU hello. |
| Microsoft.Cache/Redis/sku.name | Ustaw typ hello toodeploy pamięci podręcznej Redis. |

**Microsoft.Cdn/profiles**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Ustaw nazwę hello hello warstwy cenowej. |

**Microsoft.Compute/disks**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Ustaw oferta hello hello platformy obrazu lub marketplace obraz używany toocreate hello maszyny wirtualnej. |
| Microsoft.Compute/imagePublisher | Zestaw hello wydawcy obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate. |
| Microsoft.Compute/imageSku | Zestaw hello jednostka SKU obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate. |
| Microsoft.Compute/imageVersion | Maszyna wirtualna hello toocreate używana wersja hello zestaw obrazu platformy hello lub obrazu z witryny marketplace. |


**Microsoft.Compute/virtualMachines**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Compute/imageId | Identyfikator hello maszyny wirtualnej hello toocreate obraz używany hello zestawu. |
| Microsoft.Compute/imageOffer | Ustaw oferta hello hello platformy obrazu lub marketplace obraz używany toocreate hello maszyny wirtualnej. |
| Microsoft.Compute/imagePublisher | Zestaw hello wydawcy obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate. |
| Microsoft.Compute/imageSku | Zestaw hello jednostka SKU obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate. |
| Microsoft.Compute/imageVersion | Maszyna wirtualna hello toocreate używana wersja hello zestaw obrazu platformy hello lub obrazu z witryny marketplace. |
| Microsoft.Compute/licenseType | Ustaw ten obraz powitania lub dysk jest licencjonowane lokalnymi. Ta wartość jest używana tylko dla obrazów, które zawierają system operacyjny serwera Windows hello.  |
| Microsoft.Compute/virtualMachines/imageOffer | Ustaw oferta hello hello platformy obrazu lub marketplace obraz używany toocreate hello maszyny wirtualnej. |
| Microsoft.Compute/virtualMachines/imagePublisher | Zestaw hello wydawcy obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate. |
| Microsoft.Compute/virtualMachines/imageSku | Zestaw hello jednostka SKU obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate. |
| Microsoft.Compute/virtualMachines/imageVersion | Maszyna wirtualna hello toocreate używana wersja hello zestaw obrazu platformy hello lub obrazu z witryny marketplace. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Ustaw hello wirtualnego dysku twardego identyfikatora URI. |
| Microsoft.Compute/virtualMachines/sku.name | Ustaw rozmiar hello hello maszyny wirtualnej. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Ustaw nazwę hello rozszerzenia hello wydawcy. |
| Microsoft.Compute/virtualMachines/extensions/type | Ustaw typ hello rozszerzenia. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Ustaw wersję hello hello rozszerzenia. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Compute/imageId | Identyfikator hello maszyny wirtualnej hello toocreate obraz używany hello zestawu. |
| Microsoft.Compute/imageOffer | Ustaw oferta hello hello platformy obrazu lub marketplace obraz używany toocreate hello maszyny wirtualnej. |
| Microsoft.Compute/imagePublisher | Zestaw hello wydawcy obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate. |
| Microsoft.Compute/imageSku | Zestaw hello jednostka SKU obrazu platformy hello lub obrazu z witryny marketplace używane maszyny wirtualnej hello toocreate. |
| Microsoft.Compute/imageVersion | Maszyna wirtualna hello toocreate używana wersja hello zestaw obrazu platformy hello lub obrazu z witryny marketplace. |
| Microsoft.Compute/licenseType | Ustaw ten obraz powitania lub dysk jest licencjonowane lokalnymi. Ta wartość jest używana tylko dla obrazów, które zawierają system operacyjny serwera Windows hello. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Ustaw hello prefiks nazwy komputera dla wszystkich maszyn wirtualnych hello w zestawie skalowania hello. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Ustaw hello identyfikator URI obiektu blob obrazu użytkownika. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Ustawianie adresów URL kontenera hello, które są używane toostore dysków systemu operacyjnego dla zestawu skalowania hello. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Ustaw rozmiar hello maszyn wirtualnych w zestawie skalowania. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Ustawienie warstwy hello maszyn wirtualnych w zestawie skalowania. |
  
**Microsoft.Network/applicationGateways**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Ustaw rozmiar hello hello bramy. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Ustaw typ hello tej bramy sieci wirtualnej. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Ustaw nazwę jednostki SKU bramy hello. |

**Microsoft.Sql/servers**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Ustaw wersję hello powitania serwera. |

**Microsoft.Sql/databases**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Wartość hello hello bazy danych. |
| Microsoft.Sql/servers/databases/elasticPoolName | Zestaw hello Nazwa bazy danych hello puli elastycznej hello jest. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Ustaw hello skonfigurowana usługa celu identyfikator poziomu hello bazy danych. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Ustaw nazwę hello cel poziomu usługi hello skonfigurowane hello bazy danych.  |

**Microsoft.Sql/elasticpools**

| Alias | Opis |
| ----- | ----------- |
| serwery/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Suma hello zestaw udostępnionego jednostek dtu w warstwie dla elastycznej puli baz danych hello. |
| serwery/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Wartość hello hello puli elastycznej. |

**Microsoft.Storage/storageAccounts**

| Alias | Opis |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Warstwa dostępu hello zestaw używany na potrzeby rozliczeń. |
| Microsoft.Storage/storageAccounts/accountType | Nazwa jednostki SKU hello zestawu. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Określ, czy usługa hello szyfruje dane hello, jak są przechowywane w usłudze magazyn obiektów blob hello. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Określ, czy usługa hello szyfruje dane hello zapisanymi w usłudze magazyn plików hello. |
| Microsoft.Storage/storageAccounts/sku.name | Nazwa jednostki SKU hello zestawu. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Ustaw toostorage ruchu tooallow tylko protokołu https. |


## <a name="policy-examples"></a>Przykłady zasad

Witaj następujące tematy zawierają przykłady zasad:

* Aby uzyskać przykłady tagu zasad, zobacz [stosowania zasad zasobów dla tagów](resource-manager-policy-tags.md).
* Przykłady wzorców nazewnictwa i tekst, zobacz [stosowania zasad zasobów dla nazwy i tekst](resource-manager-policy-naming-convention.md).
* Przykłady zasad przechowywania można znaleźć [zastosować kont toostorage zasad zasobów](resource-manager-policy-storage.md).
* Przykłady zasad maszyny wirtualnej, zobacz [zastosować tooLinux zasad zasobów maszyn wirtualnych](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) i [zastosować tooWindows zasad zasobów maszyn wirtualnych](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Następne kroki
* Po zdefiniowaniu reguły zasad, przypisz tooa zakresu. Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](resource-manager-policy-portal.md). zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](resource-manager-policy-create-assign.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).
* Schemat zasad Hello jest opublikowana w [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

