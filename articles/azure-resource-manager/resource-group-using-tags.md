---
title: "aaaTag Azure do zasobów organizacji logicznego | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak tooapply znaczniki tooorganize Azure zasoby dotyczące rozliczeń i zarządzania nimi."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a>Użyj tagów tooorganize zasobów platformy Azure
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> Można stosować tylko tooresources tagi, która obsługuje operacje usługi Azure Resource Manager. Jeśli utworzono maszyny wirtualnej, sieci wirtualnej lub konta magazynu za pośrednictwem hello klasycznego modelu wdrażania (takie jak za pomocą hello klasyczny portal Azure), nie można zastosować zasobów toothat tagu. toosupport znakowanie, należy ponownie wdrożyć tych zasobów za pomocą Menedżera zasobów. Inne zasoby obsługują znakowanie.
> 
> 

## <a name="policies-for-tag-consistency"></a>Zasady spójności tag

Standardowe reguły toocreate zasad zasobów można użyć dla Twojej organizacji. Można utworzyć zasad, które upewnij się, że zasoby są oznaczane hello odpowiednie wartości. Aby uzyskać więcej informacji, zobacz [stosowania zasad zasobów dla tagów](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

toosee hello znaczników dla *grupy zasobów*, użyj:

```azurecli
az group show -n examplegroup --query tags
```

Czy skrypt zwraca hello następującego formatu:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee hello znaczników dla *zasób, który ma identyfikator określonego zasobu*, użyj:

```azurecli
az resource show --id {resource-id} --query tags
```

Lub toosee hello znaczników dla *zasób, który ma nazwę, typ i zasobów do określonej grupy*, użyj:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

Użyj tooget grupy zasobów, które mają konkretnego znacznika `az group list`:

```azurecli
az group list --tag Dept=IT
```

tooget wszystkie zasoby hello, które mają określony tag i wartości, używają `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Zawsze należy zastosować tagi tooa zasób lub grupa zasobów, należy zastąpić znaczników hello na tym zasób lub grupa zasobów. W związku z tym należy użyć innego podejścia opartego na czy hello zasób lub grupa zasobów ma znaczników. 

tooadd znaczniki tooa *grupy zasobów bez znaczników*, użyj:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd znaczniki tooa *zasobu bez znaczników*, użyj:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

tooadd tagi tooa zasób, który ma już tagów, pobrać znaczników hello, sformatuj ponownie tę wartość i zastosuj je ponownie hello istniejących i nowych znaczników: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply wszystkie znaczniki z tooits zasobów grupy zasobów i *nie zachować istniejące znaczniki zasobów hello*, użyj następującego skryptu hello:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

tooapply wszystkie znaczniki z tooits zasobów grupy zasobów i *zachować istniejące znaczniki zasobów*, użyj następującego skryptu hello:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a>Szablony

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>Interfejs API REST
Witaj portalu Azure i programu PowerShell Użyj hello [interfejsu REST API usługi Resource Manager](https://docs.microsoft.com/rest/api/resources/) tle hello. Toointegrate znakowanie do innego środowiska, należy tagów można uzyskać za pomocą **UZYSKAĆ** na hello identyfikator i aktualizacji hello zestawu zasobów tagów za pomocą **poprawka** wywołania.

## <a name="tags-and-billing"></a>Znaczniki i rozliczeń
Toogroup tagów można użyć danych rozliczeń. Na przykład jeśli używasz wielu maszyn wirtualnych w różnych organizacjach użycie hello tagi toogroup przez Centrum kosztów. Umożliwia także koszty toocategorize tagi przez środowisko uruchomieniowe, takich jak hello rozliczeń użycia dla maszyn wirtualnych w środowisku produkcyjnym hello.


Można pobrać informacji na temat tagów za pośrednictwem hello [użycia zasobów platformy Azure i interfejsów API RateCard](../billing/billing-usage-rate-card-overview.md) lub pliku wartości rozdzielanych przecinkami (CSV) użycia hello. Pobieranie pliku użycia hello z hello [portalu konta usługi Azure](https://account.windowsazure.com/) lub [EA portal](https://ea.azure.com). Aby uzyskać więcej informacji o dostęp programistyczny toobilling informacji, zobacz [uzyskać wgląd w Microsoft Azure użycia zasobów](../billing/billing-usage-rate-card-overview.md). Dla operacji interfejsu API REST, zobacz [dokumentacja interfejsu API REST rozliczenia Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Po pobraniu hello użycia woluminów CSV dla usług, które obsługują tagów z rozliczeniami hello znaczniki są wyświetlane w hello **tagi** kolumny. Aby uzyskać więcej informacji, zobacz [zrozumieć rachunku platformy Microsoft Azure](../billing/billing-understand-your-bill.md).

![Zobacz tagów w rozliczeń](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Następne kroki
* Za pomocą niestandardowych zasad można stosować ograniczenia i konwencje w Twojej subskrypcji. Zasady, które należy zdefiniować może wymagać, że wszystkie zasoby mają wartość określony tag. Aby uzyskać więcej informacji, zobacz [używają zasad toomanage zasobów i kontroli dostępu](resource-manager-policy.md).
* Aby toousing wprowadzenie programu Azure PowerShell podczas wdrażania zasobów, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](powershell-azure-resource-manager.md).
* Do wprowadzenia toousing hello Azure CLI podczas wdrażania zasobów, zobacz [hello Using Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](xplat-cli-azure-resource-manager.md).
* Wprowadzenie toousing hello portalu, zobacz [Using hello Azure toomanage portalu zasobów platformy Azure](resource-group-portal.md).  
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

