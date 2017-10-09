Jeśli używasz wartości parametru toopass pliku parametrów podczas wdrażania należy toocreate pliku JSON z formatu toohello podobne, poniższy przykład:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

rozmiar Hello hello pliku parametrów nie może być więcej niż 64 KB.

Jeśli potrzebujesz tooprovide poufną wartość dla parametru (na przykład hasło), Dodaj magazyn kluczy tooa tej wartości. Podczas wdrażania, jak pokazano w poprzednim przykładzie hello, należy pobrać hello magazynu kluczy. Aby uzyskać więcej informacji, zobacz [przekazać wartości bezpieczne podczas wdrażania](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

