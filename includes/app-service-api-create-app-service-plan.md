<span data-ttu-id="0b12e-101">Utwórz plan usługi App Service za pomocą polecenia [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="0b12e-101">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="0b12e-102">W poniższym przykładzie jest tworzony plan usługi App Service o nazwie `myAppServicePlan` przy użyciu warstwy cenowej **Bezpłatna**:</span><span class="sxs-lookup"><span data-stu-id="0b12e-102">The following example creates an App Service plan named `myAppServicePlan` in the **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="0b12e-103">Po utworzeniu planu usługi App Service interfejs wiersza polecenia platformy Azure wyświetli informacje podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="0b12e-103">When the App Service plan has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```