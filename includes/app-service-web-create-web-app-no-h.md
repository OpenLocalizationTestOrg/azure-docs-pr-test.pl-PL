<span data-ttu-id="14ebf-101">Utwórz [aplikacji sieci web](../articles/app-service-web/app-service-web-overview.md) w hello `myAppServicePlan` planu usługi aplikacji z hello [tworzenie aplikacji sieci Web az](/cli/azure/webapp#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="14ebf-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="14ebf-102">aplikacji sieci web Hello hostingu miejsce dla kodu i zapewnia to aplikacja hello wdrożone tooview adresu URL.</span><span class="sxs-lookup"><span data-stu-id="14ebf-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="14ebf-103">Zastąp następujące polecenie, w hello  *\<nazwa_aplikacji >* o unikatowej nazwie (prawidłowe znaki to `a-z`, `0-9`, i `-`).</span><span class="sxs-lookup"><span data-stu-id="14ebf-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="14ebf-104">Jeśli `<app_name>` jest nie jest unikatowy, otrzymasz komunikat o błędzie hello "Witryny sieci Web o podanej nazwie < nazwa_aplikacji > już istnieje."</span><span class="sxs-lookup"><span data-stu-id="14ebf-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="14ebf-105">Witaj domyślny adres URL aplikacji sieci web hello jest `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="14ebf-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="14ebf-106">Podczas tworzenia aplikacji sieci web hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="14ebf-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="14ebf-107">Przeglądaj toosee lokacji toohello Twojego nowo utworzonej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="14ebf-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
