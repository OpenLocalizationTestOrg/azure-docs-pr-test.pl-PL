<span data-ttu-id="a1fa3-101">Tworzenie planu usługi aplikacji z hello [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="a1fa3-101">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="a1fa3-102">Witaj poniższy przykład tworzy plan usługi aplikacji o nazwie `myAppServicePlan` w hello **wolne** warstwa cenowa:</span><span class="sxs-lookup"><span data-stu-id="a1fa3-102">hello following example creates an App Service plan named `myAppServicePlan` in hello **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="a1fa3-103">Po utworzeniu planu usługi aplikacji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="a1fa3-103">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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