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
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="ae420-103">Publikowanie aplikacji zarządzanych na użytek wewnętrzny</span><span class="sxs-lookup"><span data-stu-id="ae420-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="ae420-104">Możesz utworzyć i opublikować Azure [zarządzane aplikacje](managed-application-overview.md) które są przeznaczone do członków organizacji.</span><span class="sxs-lookup"><span data-stu-id="ae420-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="ae420-105">Na przykład dział INFORMATYCZNY może opublikować zarządzanych aplikacji, które zapewnić zgodność ze standardami w organizacji.</span><span class="sxs-lookup"><span data-stu-id="ae420-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="ae420-106">Te aplikacje zarządzane są dostępne za pośrednictwem hello katalogu usług, hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ae420-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="ae420-107">toopublish zarządzanej aplikacji hello katalogu usług, należy:</span><span class="sxs-lookup"><span data-stu-id="ae420-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="ae420-108">Utwórz pakiet ZIP, który zawiera trzy pliki wymagany szablon hello.</span><span class="sxs-lookup"><span data-stu-id="ae420-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="ae420-109">Zdecyduj, które użytkownika, grupy lub aplikacji wymaga dostępu toohello grupy zasobów w subskrypcji użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="ae420-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="ae420-110">Tworzenie definicji aplikacji hello zarządzane punktów toohello pakiet ZIP, który żąda dostępu do tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="ae420-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="ae420-111">Utwórz pakiet aplikacji zarządzanej</span><span class="sxs-lookup"><span data-stu-id="ae420-111">Create a managed application package</span></span>

<span data-ttu-id="ae420-112">Witaj pierwszym krokiem jest toocreate hello trzy szablonu wymagane pliki.</span><span class="sxs-lookup"><span data-stu-id="ae420-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="ae420-113">Wszystkie trzy pliki pakietu do pliku zip i przekazać go w dostępnej lokalizacji tooan, takie jak konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="ae420-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="ae420-114">Należy przekazać plik zip toothis łączy podczas tworzenia hello zarządzanych definicji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae420-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="ae420-115">**applianceMainTemplate.json**: plik definiuje hello Azure zasoby, które są udostępniane w ramach hello zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae420-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="ae420-116">Szablon Hello jest nie różni się od regularne szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ae420-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="ae420-117">Na przykład toocreate konto magazynu przy użyciu aplikacji zarządzanych applianceMainTemplate.json zawiera:</span><span class="sxs-lookup"><span data-stu-id="ae420-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="ae420-118">**mainTemplate.json**: użytkownicy mogą wdrażać tego szablonu podczas tworzenia hello zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae420-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="ae420-119">Definiuje zasób aplikacji hello zarządzane, który jest typem zasobu Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="ae420-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="ae420-120">Ten plik zawiera wszystkie parametry hello potrzebnych dla zasobów hello w applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="ae420-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="ae420-121">Dwie ważne właściwości można ustawić w tym szablonie.</span><span class="sxs-lookup"><span data-stu-id="ae420-121">You set two important properties in this template.</span></span> <span data-ttu-id="ae420-122">Po pierwsze, hello **applianceDefinitionId** właściwości jest hello identyfikator definicji aplikacji hello zarządzane.</span><span class="sxs-lookup"><span data-stu-id="ae420-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="ae420-123">Możesz utworzyć definicję hello później w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="ae420-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="ae420-124">Ustawienie tej wartości, należy zdecydować, które subskrypcji i zasobu toouse grupy do przechowywania hello definicji zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae420-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="ae420-125">I musi określić nazwę definicji hello.</span><span class="sxs-lookup"><span data-stu-id="ae420-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="ae420-126">Identyfikator Hello jest w formacie hello:</span><span class="sxs-lookup"><span data-stu-id="ae420-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="ae420-127">Po drugie, hello **managedResourceGroupId** właściwości jest identyfikator hello hello grupy zasobów, gdzie hello Azure zasoby są tworzone.</span><span class="sxs-lookup"><span data-stu-id="ae420-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="ae420-128">Można przypisać wartości dla tej nazwy grupy zasobów lub pozwolić Podaj nazwę użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="ae420-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="ae420-129">format Hello identyfikator hello jest:</span><span class="sxs-lookup"><span data-stu-id="ae420-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="ae420-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="ae420-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="ae420-131">Witaj poniższy przykład przedstawia plik mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="ae420-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="ae420-132">Określa grupę zasobów dla zasobów hello wdrożone.</span><span class="sxs-lookup"><span data-stu-id="ae420-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="ae420-133">Witaj identyfikator definicji jest toouse zestaw o nazwie definicji **storageApp** w grupie zasobów o nazwie **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="ae420-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="ae420-134">Można zmienić tych wartości toouse różne nazwy.</span><span class="sxs-lookup"><span data-stu-id="ae420-134">You can change these values toouse different names.</span></span> <span data-ttu-id="ae420-135">Podaj własny identyfikator subskrypcji w identyfikatorze hello definicji.</span><span class="sxs-lookup"><span data-stu-id="ae420-135">Provide your own subscription ID in hello definition ID.</span></span>

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

* <span data-ttu-id="ae420-136">**applianceCreateUiDefinition.json**: hello portalu Azure korzysta z tego pliku toogenerate hello interfejsu użytkownika dla użytkowników, którzy tworzą hello zarządzanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae420-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="ae420-137">Zdefiniuj, jak użytkownicy podawanie danych wejściowych dla każdego parametru.</span><span class="sxs-lookup"><span data-stu-id="ae420-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="ae420-138">Można użyć opcji, takie jak listy rozwijanej, pole tekstowe, pole hasła i inne dane wejściowe narzędzia.</span><span class="sxs-lookup"><span data-stu-id="ae420-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="ae420-139">toolearn toocreate plik definicji interfejsu użytkownika dla aplikacji zarządzanych, zobacz temat [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae420-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="ae420-140">Witaj poniższy przykład przedstawia plik applianceCreateUiDefinition.json, który umożliwia użytkownikom toospecify hello magazynu konta prefiks nazwy za pomocą pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ae420-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

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

<span data-ttu-id="ae420-141">Po wszystkich plików hello potrzebne są gotowe, pakiet je jako plik .zip.</span><span class="sxs-lookup"><span data-stu-id="ae420-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="ae420-142">Hello trzy pliki muszą być na poziomie głównym hello hello pliku zip.</span><span class="sxs-lookup"><span data-stu-id="ae420-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="ae420-143">Jeśli je umieścić w folderze, zostanie wyświetlony błąd podczas tworzenia hello zarządzanych definicji aplikacji, stwierdzający, że hello wymaganych plików nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="ae420-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="ae420-144">Przekaż hello pakietu tooan dostępnej lokalizacji, z którym mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="ae420-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="ae420-145">Witaj dalszej części tego artykułu przyjęto założenie, że plik zip hello istnieje w kontenerze obiektu blob magazynu publicznie.</span><span class="sxs-lookup"><span data-stu-id="ae420-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="ae420-146">Tworzenie grupy użytkowników usługi Azure Active Directory lub aplikacji</span><span class="sxs-lookup"><span data-stu-id="ae420-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="ae420-147">drugim krokiem Hello jest tooselect grupy użytkowników lub aplikacji do zarządzania zasobami hello w imieniu powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="ae420-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="ae420-148">Tej grupy użytkowników lub aplikacji ma uprawnienia do hello zasobów zarządzanych grupy zgodnie z toohello rola przypisana.</span><span class="sxs-lookup"><span data-stu-id="ae420-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="ae420-149">Witaj roli może być żadnych wbudowanych ról kontroli dostępu opartej na rolach (RBAC) jak właściciela lub współautora.</span><span class="sxs-lookup"><span data-stu-id="ae420-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="ae420-150">Również można nadać użytkownikowi uprawnień toomanage hello zasobów, ale zazwyczaj przypisać tej grupy uprawnienie tooa użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ae420-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="ae420-151">toocreate nowej grupy użytkowników usługi Active Directory, zobacz [Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ae420-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="ae420-152">Identyfikator obiektu hello toouse grupy użytkownika hello potrzebę zarządzania zasobami hello.</span><span class="sxs-lookup"><span data-stu-id="ae420-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="ae420-153">Witaj poniższy przykład pokazuje, jak tooget hello Identyfikatora obiektu z nazwę wyświetlaną grupy hello:</span><span class="sxs-lookup"><span data-stu-id="ae420-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="ae420-154">Hello przykładowe polecenie powoduje zwrócenie hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ae420-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="ae420-155">Identyfikator obiektu tylko hello tooretrieve, użyj:</span><span class="sxs-lookup"><span data-stu-id="ae420-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="ae420-156">Pobierz identyfikator definicji roli hello</span><span class="sxs-lookup"><span data-stu-id="ae420-156">Get hello role definition ID</span></span>

<span data-ttu-id="ae420-157">Następnie należy identyfikator definicji roli hello hello RBAC wbudowana rola toogrant dostępu toohello użytkownika, grupy użytkowników lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae420-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="ae420-158">Należy zwykle użyć hello właściciela lub współautora lub czytelnika roli.</span><span class="sxs-lookup"><span data-stu-id="ae420-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="ae420-159">Witaj następujące polecenia pokazuje, jak tooget hello identyfikator definicji roli dla roli właściciela hello:</span><span class="sxs-lookup"><span data-stu-id="ae420-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="ae420-160">To polecenie zwraca hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ae420-160">That command returns hello following output:</span></span>

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

<span data-ttu-id="ae420-161">Należy hello wartość właściwości "name" hello z hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="ae420-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="ae420-162">Można pobrać właśnie tej właściwości z:</span><span class="sxs-lookup"><span data-stu-id="ae420-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="ae420-163">Tworzenie definicji aplikacji hello zarządzane</span><span class="sxs-lookup"><span data-stu-id="ae420-163">Create hello managed application definition</span></span>

<span data-ttu-id="ae420-164">Jeśli grupy zasobów nie jest już ma do przechowywania definicji aplikacji zarządzanych, utwórz ją teraz:</span><span class="sxs-lookup"><span data-stu-id="ae420-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="ae420-165">Teraz utworzymy hello zarządzanych aplikacji definicji zasobu.</span><span class="sxs-lookup"><span data-stu-id="ae420-165">Now, create hello managed application definition resource.</span></span>

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

<span data-ttu-id="ae420-166">są używane w hello poprzedzających przykład parametry Hello:</span><span class="sxs-lookup"><span data-stu-id="ae420-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="ae420-167">**Grupa zasobów**: Nazwa hello hello grupy zasobów, której hello zarządzane definicji aplikacji jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="ae420-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="ae420-168">**poziomu blokady**: hello typ blokady umieszczona w grupie zasobów zarządzanych hello.</span><span class="sxs-lookup"><span data-stu-id="ae420-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="ae420-169">Powitania klienta uniemożliwia niepożądanych operacji w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="ae420-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="ae420-170">Obecnie tylko do odczytu jest hello obsługiwane tylko poziomu blokady.</span><span class="sxs-lookup"><span data-stu-id="ae420-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="ae420-171">Jeśli określono tylko do odczytu, powitania klienta mogą odczytywać tylko hello zasoby w grupie zasobów zarządzanych hello.</span><span class="sxs-lookup"><span data-stu-id="ae420-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="ae420-172">**autoryzacje**: Opisuje hello identyfikator podmiotu zabezpieczeń i identyfikator definicji roli hello są używane toogrant uprawnienia toohello zasobów zarządzanych grupy.</span><span class="sxs-lookup"><span data-stu-id="ae420-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="ae420-173">Jest on określony w formacie hello `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="ae420-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="ae420-174">Wiele wartości można również określić dla tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="ae420-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="ae420-175">Jeśli potrzebna jest wiele wartości, należy je określić w postaci hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="ae420-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="ae420-176">Wiele wartości są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="ae420-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="ae420-177">**Identyfikator uri pliku pakietu**: hello lokalizacji pakietu zarządzanej aplikacji hello, który zawiera pliki szablonów hello, co może mieć obiektu blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="ae420-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae420-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ae420-178">Next steps</span></span>

* <span data-ttu-id="ae420-179">Wprowadzenie toomanaged aplikacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae420-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ae420-180">Przykłady hello plików można znaleźć [zarządzanych aplikacji przykłady](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="ae420-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="ae420-181">Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="ae420-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="ae420-182">Aby informacji na temat publikowania aplikacji zarządzanych toohello portalu Azure Marketplace, zobacz [Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="ae420-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="ae420-183">Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanej z hello Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="ae420-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="ae420-184">toolearn toocreate plik definicji interfejsu użytkownika dla aplikacji zarządzanych, zobacz temat [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae420-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
