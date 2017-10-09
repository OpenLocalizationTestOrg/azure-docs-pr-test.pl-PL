---
title: "typowe błędy wdrożenia usługi Azure aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooresolve typowe błędy podczas wdrażania tooAzure zasobów przy użyciu usługi Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Błąd wdrażania, wdrożenia usługi azure wdrażanie tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager
W tym temacie opisano, jak może rozwiązać niektóre typowe mogą wystąpić błędy wdrożenia usługi Azure.

w tym temacie opisano następujące kody błędów Hello:

* [AccountNameInvalid](#accountnameinvalid)
* [Nie powiodło się](#authorization-failed)
* [Element BadRequest](#badrequest)
* [Niepowodzenia wdrożenia](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>Niepowodzenia wdrożenia

Ten kod błędu wskazuje błąd ogólnego wdrożenia, ale nie jest to kod błędu hello należy toostart rozwiązywania problemów. Kod błędu Hello, która faktycznie pomaga rozwiązać problem hello jest zwykle jeden poziom w dół tego błędu. Na przykład hello poniższy obraz przedstawia hello **RequestDisallowedByPolicy** kodu błędu, który podlega hello Błąd wdrażania.

![Pokaż kod błędu:](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

W przypadku wdrażania zasobów (zazwyczaj maszyny wirtualnej), może zostać wyświetlony powitania po błąd kodu i komunikatu o błędzie:

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

Ten błąd jest wyświetlany, gdy zasób hello SKU wybrano (takich jak rozmiar maszyny Wirtualnej) nie jest dostępny dla lokalizacji hello, wybrana przez Ciebie. tooresolve ten problem, należy toodetermine jednostki SKU dostępnych w danym regionie. Możesz użyć programu PowerShell, hello portal lub toofind operacji REST dostępne jednostki SKU.

- Dla programu PowerShell, użyj [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) i Filtruj według lokalizacji. Musi mieć hello najnowszej wersji programu PowerShell dla tego polecenia.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  Witaj wyniki obejmują listę jednostek SKU dla lokalizacji hello i zastosowanie jakiekolwiek ograniczenia dotyczące tej wersji produktu.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- Witaj toouse [portal](https://portal.azure.com), zaloguj się w portalu toohello i Dodaj zasób za pośrednictwem interfejsu hello. Podczas określania wartości hello, zobacz hello dostępne jednostki SKU dla tego zasobu. Nie trzeba toocomplete hello wdrożenia.

    ![dostępne jednostki SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- Witaj toouse interfejsu API REST dla maszyn wirtualnych, Wyślij hello następujące żądania:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Zwraca dostępne jednostki SKU i regiony w hello następującego formatu:

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

Jeśli toofind odpowiedniej jednostki SKU w tym regionie lub alternatywne region, który spełnia potrzeby biznesowe, przesłać [żądania SKU](https://aka.ms/skurestriction) tooAzure pomocy technicznej.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

Jeśli ten błąd jest wyświetlany, używasz subskrypcji, która nie jest dozwolone tooaccess dowolnych usług Azure innego niż Azure Active Directory. Ten typ subskrypcji mogą wystąpić podczas musi tooaccess hello klasycznego portalu, ale nie są dozwolone toodeploy zasobów. tooresolve ten problem, należy użyć subskrypcji, które ma uprawnienie toodeploy zasobów.  

tooview dostępnych subskrypcji przy użyciu programu PowerShell, należy użyć:

```powershell
Get-AzureRmSubscription
```

I tooset hello bieżącej subskrypcji, użyj:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview dostępnych subskrypcji Azure CLI 2.0, należy użyć:

```azurecli
az account list
```

I tooset hello bieżącej subskrypcji, użyj:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Ten błąd może wynikać z kilku różnych typów błędów.

- Błąd składni

   Jeśli zostanie wyświetlony komunikat o błędzie wskazuje hello szablonu nie powiodła się weryfikacja, mogą mieć problem składni w szablonie.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Ten błąd jest łatwe toomake, ponieważ wyrażenia szablonu mogą być skomplikowanych. Na przykład hello następującego przypisania nazwy dla konta magazynu zawiera jeden zestaw nawiasów, trzy funkcje trzy zestawy nawiasów, jeden zestaw apostrofy i jedną właściwość:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Jeśli nie zostanie określona hello Składnia dopasowania, hello szablon tworzy wartość, która różni się od masz zamiar.

   Po otrzymaniu tego typu błędu, należy dokładnie przejrzeć hello składni wyrażeń. Należy wziąć pod uwagę przy użyciu edytora JSON, takich jak [programu Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) lub [Visual Studio Code](resource-manager-vs-code.md), który może zostać wyświetlone ostrzeżenie dotyczące błędy składniowe.

- Niepoprawne segmentu długości

   Inny błąd nieprawidłowego szablonu występuje, gdy hello Nazwa zasobu nie jest w poprawnym formacie hello.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Zasób poziomu głównego musi mieć jeden mniej segment nazwy hello niż hello typu zasobu. Każdy z segmentów odróżnia się kreską ułamkową. W hello poniższy przykład, typ hello ma dwa segmenty i nazwa hello ma jeden segment, tak aby zawierała **prawidłową nazwę**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Ale hello w następnym przykładzie **Nieprawidłowa nazwa** ponieważ ma ona hello samą liczbę segmentów jak hello typu.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Zasoby podrzędne hello typem i nazwą mieć hello samą liczbę segmentów. Liczba segmentów ma sens, ponieważ hello pełną nazwę i typ podrzędny hello obejmuje hello nadrzędnego nazwę i typ. W związku z tym hello Pełna nazwa nadal ma jeden segment mniej niż pełny typ hello.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   Pobieranie segmentów hello prawo może być trudnych z typami Menedżera zasobów, które są stosowane przez dostawców zasobów. Na przykład stosowania witryny sieci web zasobu blokady tooa wymaga typu z czterech segmentów. W związku z tym nazwa hello jest trzy segmenty:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- Indeks kopiowania nie jest oczekiwany.

   To wystąpią **InvalidTemplate** Błąd stosowania hello **kopiowania** elementu tooa część hello szablon, który nie obsługuje tego elementu. Można stosować tylko typ zasobu tooa hello kopiowania elementu. Nie można zastosować właściwości tooa kopiowania w ramach typu zasobu. Na przykład zastosować maszyny wirtualnej tooa kopiowania, ale nie można zastosować dysków toohello systemu operacyjnego dla maszyny wirtualnej. W niektórych przypadkach można przekonwertować podrzędnych zasobów tooa nadrzędnej zasobów toocreate pętlę kopiowania. Aby uzyskać więcej informacji o używaniu kopiowania, zobacz [utworzyć wiele wystąpień zasobów usługi Azure Resource Manager](resource-group-create-multiple.md).

- Parametr jest nieprawidłowy

   Jeśli szablon hello Określa dozwolone wartości parametru, a następnie podaj wartość, która nie jest jednym z tych wartości, zostanie wyświetlony komunikat toohello podobne, następujący błąd:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   Sprawdź hello dozwolone wartości w szablonie hello i podaj jeden podczas wdrażania.

- Wykryto zależność cykliczną

   Ten błąd jest wyświetlany, gdy zasoby są zależne od siebie nawzajem w sposób uniemożliwiający wdrożenia hello uruchamianiu. Kombinacja zależnościami sprawia, że dwa lub więcej zasobów, poczekaj, aż inne zasoby, które są również oczekiwania. Na przykład zasób1 zależy od resource3 zasób2 zależy od zasób1 i resource3 zależy od zasób2. Zazwyczaj można rozwiązać ten problem, usuwając zbędne zależności. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound i ResourceNotFound
Jeśli szablon zawiera nazwę hello zasobu, którego nie można rozwiązać, komunikat o błędzie podobny do:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Jeśli próbujesz hello toodeploy Brak zasobów w szablonie hello, sprawdź, czy potrzebujesz tooadd zależności. Menedżer zasobów optymalizuje wdrożenia przez utworzenie zasobów równoległe, gdy jest to możliwe. Jeśli jeden zasób należy wdrożyć po inny zasób, należy toouse hello **dependsOn** element toocreate Twojego szablonu w zależności od hello innego zasobu. Na przykład w przypadku wdrażania aplikacji sieci web, musi istnieć hello planu usługi aplikacji. Jeśli nie określono tej aplikacji sieci web hello jest zależna od hello planu usługi aplikacji, usługi Resource Manager tworzy oba zasoby w hello tym samym czasie. Pojawi się komunikat o błędzie informujący tego hello, którego nie można odnaleźć zasobu planu usługi aplikacji, ponieważ nie istnieje jeszcze podczas próby tooset właściwość hello aplikacji sieci web. Ustawiając hello zależności w aplikacji sieci web hello zapobiec wystąpieniu tego błędu.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

Aby sugestie dotyczące rozwiązywania problemów z błędami zależności, zobacz [Sprawdź wdrożenia sekwencji](#check-deployment-sequence).

Gdy hello zasób istnieje w innej grupie zasobów niż hello jedną wdrażane na również wyświetlenie tego błędu. W takim przypadku należy użyć hello [funkcja resourceId](resource-group-template-functions-resource.md#resourceid) tooget hello pełni kwalifikowana nazwa zasobu hello.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Jeśli próba toouse hello [odwołania](resource-group-template-functions-resource.md#reference) lub [listKeys](resource-group-template-functions-resource.md#listkeys) funkcje z zasobów, których nie można rozpoznać, zostanie wyświetlony następujący błąd hello:

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Wyszukaj wyrażenie, które zawiera hello **odwołania** funkcji. Sprawdź, czy wartości parametrów hello są poprawne.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Gdy jeden zasób jest zasobem nadrzędnej tooanother, zasobu nadrzędnego hello musi istnieć przed utworzeniem hello zasobu podrzędnego. Jeśli go jeszcze nie istnieje, zostanie wyświetlony hello następujący błąd:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

Nazwa Hello hello podrzędnych zasobu zawiera nazwę nadrzędnego hello. Na przykład można zdefiniować jako bazy danych SQL:

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Jednak jeśli nie określisz zależność od zasobu nadrzędnego hello, zasobu podrzędnego hello może wdrożony przed hello nadrzędną. tooresolve ten błąd, obejmują zależności.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists i StorageAccountAlreadyTaken
W przypadku kont magazynu należy podać nazwę zasobu hello, która jest unikatowa w obrębie platformy Azure. Jeśli nie zapewnia unikatową nazwę, komunikat o błędzie takich jak:

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

Można utworzyć unikatowej nazwy przez łączenie z wynikiem hello hello Konwencja nazewnictwa [uniqueString](resource-group-template-functions-string.md#uniquestring) funkcji.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

W przypadku wdrożenia konto magazynu z hello sam nazwę istniejącego konta magazynu w ramach subskrypcji, ale Podaj inną lokalizację, komunikat o błędzie wskazuje konta magazynu hello istnieje już w innej lokalizacji. Usuń istniejące konto magazynu hello, lub podaj hello tej samej lokalizacji, ponieważ hello istniejącego konta magazynu.

## <a name="accountnameinvalid"></a>AccountNameInvalid
Zobacz hello **AccountNameInvalid** wystąpił błąd podczas próby toogive nazwę, która zawiera konta magazynu zabronione znaki. Nazwy konta magazynu musi należeć do zakresu od 3 do 24 znaków i korzystać tylko cyfry i małe litery. Witaj [uniqueString](resource-group-template-functions-string.md#uniquestring) funkcja zwraca 13 znaków. Jeśli łączenie toohello prefiks **uniqueString** wyniku, podaj prefiks, który jest 11 znaków lub mniej.

## <a name="badrequest"></a>Element BadRequest

Stan element BadRequest mogą wystąpić, gdy zawierają nieprawidłową wartość dla właściwości. Na przykład, jeśli podasz niepoprawną wartość jednostki SKU dla konta magazynu hello wdrożenie zakończy się niepowodzeniem. toodetermine prawidłowe wartości dla właściwości, obejrzyj hello [interfejsu API REST](/rest/api) dla typu zasobu hello jest wdrażany.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound i MissingSubscriptionRegistration
Podczas wdrażania zasobu, mogą otrzymywać hello następującego kodu błędu i komunikatów:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Lub może zostać wyświetlony komunikat podobny:

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

Te błędy dla jednego z trzech powodów:

1. Dostawca zasobów Hello nie została zarejestrowana dla Twojej subskrypcji
2. Wersja interfejsu API nie jest obsługiwana dla typu zasobu hello
3. Lokalizacja nie jest obsługiwana dla typu zasobu hello

komunikat o błędzie Hello powinien zapewnić sugestie dotyczące hello obsługiwane lokalizacje i wersje interfejsu API. Możesz zmienić tooone Twojego szablonu z hello sugerowane wartości. Większość dostawców są rejestrowane automatycznie przez hello Azure portalu lub hello interfejsu wiersza polecenia, którego używasz, ale nie wszystkich. Jeśli nie używasz dostawcy określonego zasobu przed, może być konieczne tooregister tego dostawcę. Użytkownik może dowiedzieć się więcej o dostawców zasobów za pomocą programu PowerShell lub interfejsu wiersza polecenia platformy Azure.

**Portal**

Możesz wyświetlić hello stanu rejestracji i zarejestrować przestrzeń nazw dostawcy zasobów za pośrednictwem portalu hello.

1. Dla Twojej subskrypcji, wybierz **dostawców zasobów**.

   ![Wybierz dostawców zasobów](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Spójrz na powitania listę dostawców zasobów i w razie potrzeby wybierz hello **zarejestrować** dostawcy zasobów hello tooregister łącza typu hello próbujesz toodeploy.

   ![Lista dostawców zasobów](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee stan rejestracji, użyj **Get-AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

Użyj tooregister dostawcy, **AzureRmResourceProvider rejestru** i podaj nazwę hello dostawcy zasobów hello mają tooregister.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

tooget hello obsługiwane lokalizacje dla określonego typu zasobu, należy użyć:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Witaj tooget obsługiwane wersje interfejsu API dla określonego typu zasobu, użyj:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Interfejs wiersza polecenia platformy Azure**

toosee, czy dostawca hello jest zarejestrowany, użyj hello `azure provider list` polecenia.

```azurecli
az provider list
```

tooregister dostawcy zasobów, użyj hello `azure provider register` polecenia, a następnie określ hello *przestrzeni nazw* tooregister.

```azurecli
az provider register --namespace Microsoft.Cdn
```

Użyj toosee hello obsługiwane lokalizacje i wersje interfejsu API dla typu zasobu:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded i OperationNotAllowed
Problemy mogą wystąpić podczas wdrażania przekracza limit przydziału, który może być według grupy zasobów, subskrypcje, konta i innych zakresów. Na przykład dana subskrypcja może być skonfigurowany toolimit hello liczba rdzeni dla regionu. Jeśli toodeploy maszynę wirtualną o większej liczby rdzeni niż dozwolona kwota hello, wystąpi błąd, który określania hello została przekroczona.
Przydział pełne informacje, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).

tooexamine przydziały swoją subskrypcję dla rdzeni, możesz użyć hello `azure vm list-usage` w hello wiersza polecenia platformy Azure. Witaj poniższy przykład przedstawia ten limit przydziału rdzeni hello bezpłatne konto próbne jest 4:

```azurecli
az vm list-usage --location "South Central US"
```

Polecenie to zwraca:

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

Jeśli wdrożono szablon, który tworzy więcej niż cztery rdzenie hello regionu zachodnie stany USA, można uzyskać Błąd wdrażania, która wygląda jak:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

W programie PowerShell, możesz użyć hello **Get-AzureRmVMUsage** polecenia cmdlet.

```powershell
Get-AzureRmVMUsage
```

Polecenie to zwraca:

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

W takich przypadkach możesz Przejdź toohello portalu i pliku limitu przydziału dla regionu hello, do którego będzie toodeploy tooraise problem pomocy technicznej.

> [!NOTE]
> Należy pamiętać, grup zasobów, limitu przydziału hello jest dla poszczególnych regionów, nie dla całej subskrypcji hello. Jeśli potrzebujesz toodeploy 30 rdzeni zachodnie stany USA, masz tooask dla 30 rdzeni Resource Manager zachodnie stany USA. Jeśli potrzebujesz toodeploy 30 rdzeni w jednym z toowhich regionów hello masz dostęp, należy poprosić dla 30 rdzeni Resource Manager we wszystkich regionach.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Gdy pojawi się komunikat o błędzie hello:

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

Prawdopodobnie podjęto toolink tooa zagnieżdżonych szablon, który nie jest dostępna. Sprawdź hello przewidzianych hello zagnieżdżony szablon identyfikatora URI. Jeśli szablon hello istnieje na koncie magazynu, upewnij się, że hello identyfikatora URI jest dostępny. Może być konieczne toopass tokenu sygnatury dostępu Współdzielonego. Aby uzyskać więcej informacji, zobacz [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md) (Używanie szablonów połączonych w usłudze Azure Resource Manager).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
Ten błąd jest wyświetlany, gdy Twoja subskrypcja obejmuje uniemożliwiający akcji próbujesz tooperform podczas wdrażania zasad zasobów. W komunikacie o błędzie hello Wyszukaj identyfikator zasad hello.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

W **PowerShell**, podaj identyfikator zasad jako hello **identyfikator** parametru tooretrieve szczegóły hello zasad zablokowane wdrożenia.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

W **interfejsu wiersza polecenia Azure**, podaj nazwę hello hello definicji zasad:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Aby uzyskać więcej informacji zobacz następujące artykuły hello:

- [RequestDisallowedByPolicy error (Błąd RequestDisallowedByPolicy)](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Korzystanie z zasobów toomanage zasad i kontrola dostępu](resource-manager-policy.md).

## <a name="authorization-failed"></a>Nie powiodło się
Ponieważ hello konta lub głównej próby toodeploy hello zasobów usługi nie ma dostępu tooperform tych czynności może zostać wyświetlony błąd podczas wdrażania. Usługa Azure Active Directory umożliwia toocontrol Twojego administratora, tożsamości, które mają dostęp do zasobów, jakie precyzyjną precyzji. Na przykład jeśli konto jest przypisaną rolę czytelnika toohello, nie jesteś toocreate stanie zasobów. W takim przypadku zostanie wyświetlony komunikat o błędzie wskazujący, że autoryzacja nie powiodła się.

Aby uzyskać więcej informacji na temat kontroli dostępu opartej na rolach, zobacz [kontroli dostępu](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Następne kroki
* toolearn o inspekcji akcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).
* toolearn o błędach hello toodetermine akcje podczas wdrażania, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).
