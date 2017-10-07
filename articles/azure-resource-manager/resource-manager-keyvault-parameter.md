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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Użyj wartości parametru secure toopass Key Vault podczas wdrażania

Jeśli potrzebujesz toopass bezpiecznego wartość (na przykład hasło) jako parametr podczas wdrażania można pobrać wartość hello z [usługi Azure Key Vault](../key-vault/key-vault-whatis.md). Możesz pobrać wartość hello odwołując hello magazynu kluczy oraz klucz tajny w pliku parametrów. wartość Hello nigdy nie jest uwidaczniana, ponieważ można odwoływać się tylko jego identyfikator magazynu kluczy. Nie trzeba toomanually wprowadź hello wartość klucza tajnego hello każdym wdrożeniu hello zasobów. magazyn kluczy Hello może istnieć w innej subskrypcji niż hello grupy zasobów, które wdrażasz. Podczas odwoływania się do magazynu kluczy hello, obejmują identyfikatora hello subskrypcji.

Podczas tworzenia magazynu kluczy hello należy skonfigurować hello *enabledForTemplateDeployment* właściwości zbyt*true*. Ustawienie tej wartości tootrue, można zezwolić na dostęp z szablonów usługi Resource Manager podczas wdrażania.  

## <a name="deploy-a-key-vault-and-secret"></a>Wdrażanie magazynu kluczy oraz klucz tajny

toocreate magazyn kluczy i klucz tajny, za pomocą wiersza polecenia platformy Azure lub programu PowerShell. Należy zauważyć, że tego magazynu kluczy hello jest włączony do wdrożenia szablonu. 

W przypadku interfejsu wiersza polecenia platformy Azure użyj polecenia:

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

W przypadku programu PowerShell użyj polecenia:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Włącz klucz tajny toohello dostępu

Czy używasz nowego magazynu kluczy lub istniejący, upewnij się, że użytkownik hello wdrażanie szablonu hello mogą uzyskiwać dostęp do klucza tajnego hello. Użytkownik Hello wdrażania szablonu, który odwołuje się klucz tajny musi mieć hello `Microsoft.KeyVault/vaults/deploy/action` uprawnienie hello magazynu kluczy. Witaj [właściciela](../active-directory/role-based-access-built-in-roles.md#owner) i [współautora](../active-directory/role-based-access-built-in-roles.md#contributor) ról zarówno udzielić dostępu. Można również utworzyć [niestandardowej roli zabezpieczeń](../active-directory/role-based-access-control-custom-roles.md) daje to uprawnienie i dodać rolę toothat użytkownika hello. Uzyskać informacji o dodawaniu tooa roli użytkownika, zobacz [przypisać role tooadministrator w usłudze Azure Active Directory użytkownika](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Odwołanie klucza tajnego o identyfikatorze statyczne

Szablon Hello odbiera klucz tajny magazynu kluczy jest podobnie jak każdy inny szablon. Jest to spowodowane tym **odwołania hello magazynu kluczy w pliku parametrów hello, nie hello szablonu.** Na przykład hello następującego szablonu wdraża bazy danych SQL, która zawiera hasła administratora. Parametr hasła Hello ustawiono tooa bezpieczny ciąg. Jednak hello szablonu nie określa, z której pochodzi ta wartość.

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

Teraz Utwórz plik parametrów dla hello poprzedzających szablonu. W pliku parametrów hello należy określić parametr, który odpowiada nazwie hello parametru hello hello szablonu. Wartość parametru hello odwoływać się w magazynie kluczy hello hello. Klucz tajny hello odwoływać się przez przekazanie hello identyfikator zasobu magazynu kluczy hello i nazwę hello hello klucz tajny. W hello poniższy przykład klucz tajny magazynu kluczy hello musi już istnieć, podaj wartość statyczną dla jego identyfikator zasobu.

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

## <a name="reference-a-secret-with-dynamic-id"></a>Odwołanie klucza tajnego o identyfikatorze dynamiczne

Witaj w poprzedniej sekcji pokazano, jak toopass identyfikator zasobu statycznych hello klucza magazynu klucz tajny. Jednak w niektórych scenariuszach należy tooreference magazynu kluczy klucz tajny, który jest różny oparte na powitania bieżącego wdrożenia. W takim przypadku można identyfikator zasobu hello kodowane w pliku parametrów hello. Niestety, nie można dynamicznie wygenerować identyfikator zasobu hello w pliku parametrów hello ponieważ wyrażenia nie są dozwolone w pliku parametrów hello.

toodynamically generować hello identyfikator zasobu dla klucza tajnego w magazynie kluczy, należy przenieść hello zasobem, który wymaga klucza tajnego hello szablon zagnieżdżony. W szablonie głównym dodać hello zagnieżdżony szablon i podaj parametr, który zawiera identyfikator zasobu hello generowane dynamicznie.

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

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać ogólne informacje o magazynów kluczy, zobacz [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md).
* Przykłady pełną odwołujące się do kluczy tajnych kluczy, zobacz [przykłady Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

