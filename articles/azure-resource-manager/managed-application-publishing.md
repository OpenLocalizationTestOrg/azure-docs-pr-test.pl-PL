---
title: "aaaCreate i publikowanie aplikacji zarządzanych katalogu usługi Azure | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak toocreate platformy Azure zarządzanych aplikacji, która jest przeznaczony dla członków organizacji."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a>Publikowanie aplikacji zarządzanych na użytek wewnętrzny

Możesz utworzyć i opublikować Azure [zarządzane aplikacje](managed-application-overview.md) które są przeznaczone do członków organizacji. Na przykład dział INFORMATYCZNY może opublikować zarządzanych aplikacji, które zapewnić zgodność ze standardami w organizacji. Te aplikacje zarządzane są dostępne za pośrednictwem hello katalogu usług, hello Azure Marketplace.

toopublish zarządzanej aplikacji hello katalogu usług, należy:

* Utwórz pakiet ZIP, który zawiera trzy pliki wymagany szablon hello.
* Zdecyduj, które użytkownika, grupy lub aplikacji wymaga dostępu toohello grupy zasobów w subskrypcji użytkownika hello.
* Tworzenie definicji aplikacji hello zarządzane punktów toohello pakiet ZIP, który żąda dostępu do tożsamości hello.

## <a name="create-a-managed-application-package"></a>Utwórz pakiet aplikacji zarządzanej

Witaj pierwszym krokiem jest toocreate hello trzy szablonu wymagane pliki. Wszystkie trzy pliki pakietu do pliku zip i przekazać go w dostępnej lokalizacji tooan, takie jak konto magazynu. Należy przekazać plik zip toothis łączy podczas tworzenia hello zarządzanych definicji aplikacji.

* **applianceMainTemplate.json**: plik definiuje hello Azure zasoby, które są udostępniane w ramach hello zarządzanych aplikacji. Szablon Hello jest nie różni się od regularne szablonu usługi Resource Manager. Na przykład toocreate konto magazynu przy użyciu aplikacji zarządzanych applianceMainTemplate.json zawiera:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* **mainTemplate.json**: użytkownicy mogą wdrażać tego szablonu podczas tworzenia hello zarządzanych aplikacji. Definiuje zasób aplikacji hello zarządzane, który jest typem zasobu Microsoft.Solutions/appliances. Ten plik zawiera wszystkie parametry hello potrzebnych dla zasobów hello w applianceMainTemplate.json.

  Dwie ważne właściwości można ustawić w tym szablonie. Po pierwsze, hello **applianceDefinitionId** właściwości jest hello identyfikator definicji aplikacji hello zarządzane. Możesz utworzyć definicję hello później w tym temacie. Ustawienie tej wartości, należy zdecydować, które subskrypcji i zasobu toouse grupy do przechowywania hello definicji zarządzanych aplikacji. I musi określić nazwę definicji hello. Identyfikator Hello jest w formacie hello:

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  Po drugie, hello **managedResourceGroupId** właściwości jest identyfikator hello hello grupy zasobów, gdzie hello Azure zasoby są tworzone. Można przypisać wartości dla tej nazwy grupy zasobów lub pozwolić Podaj nazwę użytkownika hello. format Hello identyfikator hello jest:

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  Witaj poniższy przykład przedstawia plik mainTemplate.json. Określa grupę zasobów dla zasobów hello wdrożone. Witaj identyfikator definicji jest toouse zestaw o nazwie definicji **storageApp** w grupie zasobów o nazwie **managedApplicationGroup**. Można zmienić tych wartości toouse różne nazwy. Podaj własny identyfikator subskrypcji w identyfikatorze hello definicji.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* **applianceCreateUiDefinition.json**: hello portalu Azure korzysta z tego pliku toogenerate hello interfejsu użytkownika dla użytkowników, którzy tworzą hello zarządzanej aplikacji. Zdefiniuj, jak użytkownicy podawanie danych wejściowych dla każdego parametru. Można użyć opcji, takie jak listy rozwijanej, pole tekstowe, pole hasła i inne dane wejściowe narzędzia. toolearn toocreate plik definicji interfejsu użytkownika dla aplikacji zarządzanych, zobacz temat [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).

  Witaj poniższy przykład przedstawia plik applianceCreateUiDefinition.json, który umożliwia użytkownikom toospecify hello magazynu konta prefiks nazwy za pomocą pola tekstowego.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

Po wszystkich plików hello potrzebne są gotowe, pakiet je jako plik .zip. Hello trzy pliki muszą być na poziomie głównym hello hello pliku zip. Jeśli je umieścić w folderze, zostanie wyświetlony błąd podczas tworzenia hello zarządzanych definicji aplikacji, stwierdzający, że hello wymaganych plików nie są dostępne. Przekaż hello pakietu tooan dostępnej lokalizacji, z którym mogą być używane. Witaj dalszej części tego artykułu przyjęto założenie, że plik zip hello istnieje w kontenerze obiektu blob magazynu publicznie.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Tworzenie grupy użytkowników usługi Azure Active Directory lub aplikacji

drugim krokiem Hello jest tooselect grupy użytkowników lub aplikacji do zarządzania zasobami hello w imieniu powitania klienta. Tej grupy użytkowników lub aplikacji ma uprawnienia do hello zasobów zarządzanych grupy zgodnie z toohello rola przypisana. Witaj roli może być żadnych wbudowanych ról kontroli dostępu opartej na rolach (RBAC) jak właściciela lub współautora. Również można nadać użytkownikowi uprawnień toomanage hello zasobów, ale zazwyczaj przypisać tej grupy uprawnienie tooa użytkownika. toocreate nowej grupy użytkowników usługi Active Directory, zobacz [Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).

Identyfikator obiektu hello toouse grupy użytkownika hello potrzebę zarządzania zasobami hello. Witaj poniższy przykład pokazuje, jak tooget hello Identyfikatora obiektu z nazwę wyświetlaną grupy hello:

```azurecli-interactive
az ad group show --group exampleGroupName
```

Hello przykładowe polecenie powoduje zwrócenie hello następujące dane wyjściowe:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

Identyfikator obiektu tylko hello tooretrieve, użyj:

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Pobierz identyfikator definicji roli hello

Następnie należy identyfikator definicji roli hello hello RBAC wbudowana rola toogrant dostępu toohello użytkownika, grupy użytkowników lub aplikacji. Należy zwykle użyć hello właściciela lub współautora lub czytelnika roli. Witaj następujące polecenia pokazuje, jak tooget hello identyfikator definicji roli dla roli właściciela hello:


```azurecli-interactive
az role definition list --name owner
```

To polecenie zwraca hello następujące dane wyjściowe:

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

Należy hello wartość właściwości "name" hello z hello poprzedzających przykład. Można pobrać właśnie tej właściwości z:

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Tworzenie definicji aplikacji hello zarządzane

Jeśli grupy zasobów nie jest już ma do przechowywania definicji aplikacji zarządzanych, utwórz ją teraz:

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

Teraz utworzymy hello zarządzanych aplikacji definicji zasobu.

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

są używane w hello poprzedzających przykład parametry Hello:

* **Grupa zasobów**: Nazwa hello hello grupy zasobów, której hello zarządzane definicji aplikacji jest tworzona.
* **poziomu blokady**: hello typ blokady umieszczona w grupie zasobów zarządzanych hello. Powitania klienta uniemożliwia niepożądanych operacji w tej grupie zasobów. Obecnie tylko do odczytu jest hello obsługiwane tylko poziomu blokady. Jeśli określono tylko do odczytu, powitania klienta mogą odczytywać tylko hello zasoby w grupie zasobów zarządzanych hello.
* **autoryzacje**: Opisuje hello identyfikator podmiotu zabezpieczeń i identyfikator definicji roli hello są używane toogrant uprawnienia toohello zasobów zarządzanych grupy. Jest on określony w formacie hello `<principalId>:<roleDefinitionId>`. Wiele wartości można również określić dla tej właściwości. Jeśli potrzebna jest wiele wartości, należy je określić w postaci hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. Wiele wartości są oddzielone spacją.
* **Identyfikator uri pliku pakietu**: hello lokalizacji pakietu zarządzanej aplikacji hello, który zawiera pliki szablonów hello, co może mieć obiektu blob magazynu Azure.

## <a name="next-steps"></a>Następne kroki

* Wprowadzenie toomanaged aplikacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).
* Przykłady hello plików można znaleźć [zarządzanych aplikacji przykłady](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).
* Aby informacji na temat publikowania aplikacji zarządzanych toohello portalu Azure Marketplace, zobacz [Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-author-marketplace.md).
* Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanej z hello Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-consume-marketplace.md).
* toolearn toocreate plik definicji interfejsu użytkownika dla aplikacji zarządzanych, zobacz temat [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
