
<span data-ttu-id="12dd9-101">Utwórz [aplikacji interfejsu API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) w hello `myAppServicePlan` planu usługi aplikacji z hello [tworzenie aplikacji sieci Web az](/cli/azure/appservice/web#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="12dd9-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="12dd9-102">aplikacji sieci web Hello hostingu miejsce do interfejsu API i zapewnia to aplikacja hello wdrożone tooview adresu URL.</span><span class="sxs-lookup"><span data-stu-id="12dd9-102">hello web app provides a hosting space for your API and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="12dd9-103">Zastąp następujące polecenie, w hello  *\<nazwa_aplikacji >* o unikatowej nazwie.</span><span class="sxs-lookup"><span data-stu-id="12dd9-103">In hello following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="12dd9-104">Jeśli `<app_name>` jest nie jest unikatowy, otrzymasz komunikat o błędzie hello "Witryny sieci Web o podanej nazwie < nazwa_aplikacji > już istnieje."</span><span class="sxs-lookup"><span data-stu-id="12dd9-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="12dd9-105">Witaj domyślny adres URL aplikacji sieci web hello jest `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="12dd9-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="12dd9-106">Podczas tworzenia aplikacji sieci web hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="12dd9-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```