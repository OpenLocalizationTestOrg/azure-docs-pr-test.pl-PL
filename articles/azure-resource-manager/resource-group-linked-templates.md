---
title: "Szablony aaaLink dla wdrożenia usługi Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse połączone szablonów w toocreate szablonu usługi Azure Resource Manager rozwiązania moduły szablonu. Pokazuje, jak toopass wartości parametrów, określ plik parametrów i tworzone dynamicznie adresów URL."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Korzystanie z szablonów połączonych w przypadku wdrażania zasobów platformy Azure
Z jednego szablonu usługi Azure Resource Manager, możesz połączyć tooanother szablonu, który pozwala toodecompose wdrożenia do zestawu docelowego, specyficzne dla celu szablonów. Tak jak w przypadku decomposing aplikację na kilku kod klasy, dekompozycji zapewnia korzyści w zakresie testowania, ponownemu i czytelność.  

Należy przekazać parametry szablonu połączonego tooa szablonu głównego, a te parametry można zamapować bezpośrednio, tooparameters lub zmiennych w hello wywoływania szablonu. Szablon połączonego Hello można również przekazać szablonu źródła zmiennej toohello wstecz dane wyjściowe, włączanie wymiany danych dwukierunkowej między szablonami.

## <a name="linking-tooa-template"></a>Łączenie tooa szablonu
Możesz utworzyć łącza między dwa szablony przez dodanie do zasobu wdrożenia w szablonie głównym hello toohello punktów połączonego szablonu. Ustaw hello **templateLink** toohello właściwość URI hello połączonego szablonu. Można podać wartości parametrów szablonu połączonego hello, bezpośrednio w szablonie lub w pliku parametrów. Witaj poniższym przykładzie użyto hello **parametry** toospecify właściwości bezpośrednio wartości parametru.

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

Podobnie jak inne typy zasobów można ustawić zależności między hello połączonego szablonu i innych zasobów. W związku z tym inne zasoby potrzebują wartość wyjściowa szablonu połączonego hello, można upewnij się, że wdrożeniu szablonu połączonego hello przed ich. Lub, gdy szablon połączonego hello opiera się na inne zasoby, można upewnij się, że inne zasoby są wdrażane przed hello połączonego szablonu. Można pobrać wartości z połączonych szablonu z hello składni:

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Hello usługi Resource Manager musi być możliwe tooaccess hello połączonego szablonu. Nie można określić plik lokalny lub plik, który jest dostępny tylko w sieci lokalnej hello połączonego szablonu. Możesz udostępniać wartość identyfikatora URI, która zawiera jedną **http** lub **https**. Jedną z opcji jest tooplace szablonu połączonego konta magazynu, i użyj hello identyfikatora URI dla tego elementu, takie jak pokazano na powitania poniższy przykład:

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Mimo że hello połączonego szablonu musi być dostępny zewnętrznie, nie musi toobe publicznego toohello ogólnie dostępna. Można dodać konta magazynu prywatnego tooa szablonu, który jest właścicielem konta magazynu hello tooonly dostępny. Następnie można utworzyć dostępu tooenable tokenu sygnatury dostępu Współdzielonego dostępu współdzielonego podczas wdrażania. Możesz dodać tego SAS tokenu toohello URI hello połączonego szablonu. Aby uzyskać instrukcje na temat ustawiania szablonu na koncie magazynu i generowania tokenu sygnatury dostępu Współdzielonego, zobacz [wdrażanie zasobów przy użyciu szablonów usługi Resource Manager i programu Azure PowerShell](resource-group-template-deploy.md) lub [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu wiersza polecenia Azure](resource-group-template-deploy-cli.md). 

Witaj poniższy przykład przedstawia szablonu nadrzędnego szablonu tooanother łącza. Witaj połączony jest uzyskiwany z tokenu sygnatury dostępu Współdzielonego, który jest przekazywana jako parametr.

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

Mimo że hello token jest przekazywany jako bezpieczny ciąg, hello URI szablonu połączonego hello, w tym hello tokenu sygnatury dostępu Współdzielonego, są rejestrowane w hello operacje wdrażania. narażenia toolimit, ustawienia okresu ważności tokenu hello.

Menedżer zasobów obsługuje każdego połączonego szablonu jako osobne wdrożenia. W historii wdrożenia hello hello grupy zasobów można zobaczyć oddzielnych wdrożeń hello nadrzędny i zagnieżdżone szablony.

![historia wdrażania](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Łączenie pliku parametrów tooa
Witaj następnym przykładzie użyto hello **parametersLink** pliku parametrów tooa toolink właściwości.

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

Hello URI wartość hello parametru połączonego pliku nie może być lokalny plik i musi zawierać albo **http** lub **https**. plik parametrów Hello może być również ograniczony tooaccess za pośrednictwem tokenu sygnatury dostępu Współdzielonego.

## <a name="using-variables-toolink-templates"></a>Za pomocą szablonów toolink zmiennych
Witaj poprzednich przykładach pokazano zakodowanych wartości adresu URL dla hello szablon łączy. Takie podejście może działać w przypadku prostego szablonu, ale nie działa w przypadku pracy z dużym zestawem moduły szablonów. Zamiast tego można utworzyć zmienną statyczną, przechowującym bazowy adres URL dla szablonu głównego hello, a następnie dynamicznie utworzyć adresów URL dla szablonów hello połączone z tym podstawowego adresu URL. Możesz z łatwością przenoszenia lub rozwidlenia szablonu hello ponieważ wystarczy zmienna statyczna hello toochange w szablonie głównym hello jest Hello zaletą tej metody. Szablon głównego Hello przekazuje hello prawidłowe identyfikatory URI w całym hello rozłożone szablonu.

Witaj poniższy przykład przedstawia sposób toouse podstawowej toocreate adres URL dwa adresy URL dla połączonych szablonów (**sharedTemplateUrl** i **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

Można również użyć [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello podstawowego adresu URL dla bieżącego szablonu hello i używać tego adresu URL hello tooget innych szablonów w hello tej samej lokalizacji. Ta metoda jest przydatna, jeśli zmieni się lokalizację szablonu (być może z powodu tooversioning) lub ma tooavoid twardych kodowania adresów URL w pliku szablonu hello. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Pełny przykład
następujące szablony przykład Hello Pokaż tooillustrate szablonów połączonych w układzie uproszczony kilka pojęć hello w tym artykule. Zakłada się, że szablony hello dodano toohello tego samego kontenera na koncie magazynu o dostępie jest wyłączona. Szablon połączonego Hello przekazuje szablonie głównym wstecz toohello wartości w hello **generuje** sekcji.

Witaj **parent.json** plik zawiera:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

Witaj **helloworld.json** plik zawiera:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

W programie PowerShell możesz uzyskać token dla kontenera hello i wdrażać hello szablonów:

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

W programie Azure CLI 2.0 uzyskać token dla kontenera hello i wdrażanie szablonów hello z hello następującego kodu:

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a>Następne kroki
* toolearn o hello określające kolejność wdrażania hello zasobów, zobacz [Definiowanie zależności w szablonach usługi Azure Resource Manager](resource-group-define-dependencies.md)
* toolearn toodefine jeden zasób, ale utworzenia wielu wystąpień, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md)

