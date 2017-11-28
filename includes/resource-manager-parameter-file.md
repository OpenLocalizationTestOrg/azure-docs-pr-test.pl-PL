<span data-ttu-id="6ae25-101">Użycie pliku parametrów można podać wartości parametrów podczas wdrażania, należy utworzyć plik JSON w formacie podobny do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="6ae25-101">If you use a parameter file to pass parameter values during deployment, you need to create a JSON file with a format similar to the following example:</span></span>

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

<span data-ttu-id="6ae25-102">Rozmiar pliku parametrów nie może być więcej niż 64 KB.</span><span class="sxs-lookup"><span data-stu-id="6ae25-102">The size of the parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="6ae25-103">Jeśli trzeba podać poufne wartość dla parametru (na przykład hasło), należy dodać tę wartość do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="6ae25-103">If you need to provide a sensitive value for a parameter (such as a password), add that value to a key vault.</span></span> <span data-ttu-id="6ae25-104">Podczas wdrażania należy pobrać magazynu kluczy, jak pokazano w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="6ae25-104">Retrieve the key vault during deployment as shown in the previous example.</span></span> <span data-ttu-id="6ae25-105">Aby uzyskać więcej informacji, zobacz [przekazać wartości bezpieczne podczas wdrażania](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="6ae25-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

