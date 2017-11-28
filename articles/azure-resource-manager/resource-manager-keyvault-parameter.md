---
title: "klucz tajny magazynu aaaKey z szablonu usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak toopass klucz tajny z klucza magazynu jako parametr podczas wdrażania."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="558dc-103">Użyj wartości parametru secure toopass Key Vault podczas wdrażania</span><span class="sxs-lookup"><span data-stu-id="558dc-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="558dc-104">Jeśli potrzebujesz toopass bezpiecznego wartość (na przykład hasło) jako parametr podczas wdrażania można pobrać wartość hello z [usługi Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="558dc-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="558dc-105">Możesz pobrać wartość hello odwołując hello magazynu kluczy oraz klucz tajny w pliku parametrów.</span><span class="sxs-lookup"><span data-stu-id="558dc-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="558dc-106">wartość Hello nigdy nie jest uwidaczniana, ponieważ można odwoływać się tylko jego identyfikator magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="558dc-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="558dc-107">Nie trzeba toomanually wprowadź hello wartość klucza tajnego hello każdym wdrożeniu hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="558dc-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="558dc-108">magazyn kluczy Hello może istnieć w innej subskrypcji niż hello grupy zasobów, które wdrażasz.</span><span class="sxs-lookup"><span data-stu-id="558dc-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="558dc-109">Podczas odwoływania się do magazynu kluczy hello, obejmują identyfikatora hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="558dc-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="558dc-110">Podczas tworzenia magazynu kluczy hello należy skonfigurować hello *enabledForTemplateDeployment* właściwości zbyt*true*.</span><span class="sxs-lookup"><span data-stu-id="558dc-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="558dc-111">Ustawienie tej wartości tootrue, można zezwolić na dostęp z szablonów usługi Resource Manager podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="558dc-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="558dc-112">Wdrażanie magazynu kluczy oraz klucz tajny</span><span class="sxs-lookup"><span data-stu-id="558dc-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="558dc-113">toocreate magazyn kluczy i klucz tajny, za pomocą wiersza polecenia platformy Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="558dc-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="558dc-114">Należy zauważyć, że tego magazynu kluczy hello jest włączony do wdrożenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="558dc-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="558dc-115">W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="558dc-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="558dc-116">W przypadku programu PowerShell użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="558dc-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="558dc-117">Włącz klucz tajny toohello dostępu</span><span class="sxs-lookup"><span data-stu-id="558dc-117">Enable access toohello secret</span></span>

<span data-ttu-id="558dc-118">Czy używasz nowego magazynu kluczy lub istniejący, upewnij się, że użytkownik hello wdrażanie szablonu hello mogą uzyskiwać dostęp do klucza tajnego hello.</span><span class="sxs-lookup"><span data-stu-id="558dc-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="558dc-119">Użytkownik Hello wdrażania szablonu, który odwołuje się klucz tajny musi mieć hello `Microsoft.KeyVault/vaults/deploy/action` uprawnienie hello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="558dc-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="558dc-120">Witaj [właściciela](../active-directory/role-based-access-built-in-roles.md#owner) i [współautora](../active-directory/role-based-access-built-in-roles.md#contributor) ról zarówno udzielić dostępu.</span><span class="sxs-lookup"><span data-stu-id="558dc-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="558dc-121">Można również utworzyć [niestandardowej roli zabezpieczeń](../active-directory/role-based-access-control-custom-roles.md) daje to uprawnienie i dodać rolę toothat użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="558dc-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="558dc-122">Uzyskać informacji o dodawaniu tooa roli użytkownika, zobacz [przypisać role tooadministrator w usłudze Azure Active Directory użytkownika](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="558dc-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="558dc-123">Odwołanie klucza tajnego o identyfikatorze statyczne</span><span class="sxs-lookup"><span data-stu-id="558dc-123">Reference a secret with static ID</span></span>

<span data-ttu-id="558dc-124">Szablon Hello odbiera klucz tajny magazynu kluczy jest podobnie jak każdy inny szablon.</span><span class="sxs-lookup"><span data-stu-id="558dc-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="558dc-125">Jest to spowodowane tym **odwołania hello magazynu kluczy w pliku parametrów hello, nie hello szablonu.**</span><span class="sxs-lookup"><span data-stu-id="558dc-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="558dc-126">Na przykład hello następującego szablonu wdraża bazy danych SQL, która zawiera hasła administratora.</span><span class="sxs-lookup"><span data-stu-id="558dc-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="558dc-127">Parametr hasła Hello ustawiono tooa bezpieczny ciąg.</span><span class="sxs-lookup"><span data-stu-id="558dc-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="558dc-128">Jednak hello szablonu nie określa, z której pochodzi ta wartość.</span><span class="sxs-lookup"><span data-stu-id="558dc-128">But, hello template does not specify where that value comes from.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

<span data-ttu-id="558dc-129">Teraz Utwórz plik parametrów dla hello poprzedzających szablonu.</span><span class="sxs-lookup"><span data-stu-id="558dc-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="558dc-130">W pliku parametrów hello należy określić parametr, który odpowiada nazwie hello parametru hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="558dc-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="558dc-131">Wartość parametru hello odwoływać się w magazynie kluczy hello hello.</span><span class="sxs-lookup"><span data-stu-id="558dc-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="558dc-132">Klucz tajny hello odwoływać się przez przekazanie hello identyfikator zasobu magazynu kluczy hello i nazwę hello hello klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="558dc-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="558dc-133">W hello poniższy przykład klucz tajny magazynu kluczy hello musi już istnieć, podaj wartość statyczną dla jego identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="558dc-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="558dc-134">Odwołanie klucza tajnego o identyfikatorze dynamiczne</span><span class="sxs-lookup"><span data-stu-id="558dc-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="558dc-135">Witaj w poprzedniej sekcji pokazano, jak toopass identyfikator zasobu statycznych hello klucza magazynu klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="558dc-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="558dc-136">Jednak w niektórych scenariuszach należy tooreference magazynu kluczy klucz tajny, który jest różny oparte na powitania bieżącego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="558dc-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="558dc-137">W takim przypadku można identyfikator zasobu hello kodowane w pliku parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="558dc-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="558dc-138">Niestety, nie można dynamicznie wygenerować identyfikator zasobu hello w pliku parametrów hello ponieważ wyrażenia nie są dozwolone w pliku parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="558dc-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="558dc-139">toodynamically generować hello identyfikator zasobu dla klucza tajnego w magazynie kluczy, należy przenieść hello zasobem, który wymaga klucza tajnego hello szablon zagnieżdżony.</span><span class="sxs-lookup"><span data-stu-id="558dc-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="558dc-140">W szablonie głównym dodać hello zagnieżdżony szablon i podaj parametr, który zawiera identyfikator zasobu hello generowane dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="558dc-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a><span data-ttu-id="558dc-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="558dc-141">Next steps</span></span>
* <span data-ttu-id="558dc-142">Aby uzyskać ogólne informacje o magazynów kluczy, zobacz [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="558dc-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="558dc-143">Przykłady pełną odwołujące się do kluczy tajnych kluczy, zobacz [przykłady Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="558dc-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

