<span data-ttu-id="22dc6-101">Jeśli używasz wartości parametru toopass pliku parametrów podczas wdrażania należy toocreate pliku JSON z formatu toohello podobne, poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="22dc6-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="22dc6-102">rozmiar Hello hello pliku parametrów nie może być więcej niż 64 KB.</span><span class="sxs-lookup"><span data-stu-id="22dc6-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="22dc6-103">Jeśli potrzebujesz tooprovide poufną wartość dla parametru (na przykład hasło), Dodaj magazyn kluczy tooa tej wartości.</span><span class="sxs-lookup"><span data-stu-id="22dc6-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="22dc6-104">Podczas wdrażania, jak pokazano w poprzednim przykładzie hello, należy pobrać hello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="22dc6-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="22dc6-105">Aby uzyskać więcej informacji, zobacz [przekazać wartości bezpieczne podczas wdrażania](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="22dc6-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

