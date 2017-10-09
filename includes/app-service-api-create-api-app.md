
Utwórz [aplikacji interfejsu API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) w hello `myAppServicePlan` planu usługi aplikacji z hello [tworzenie aplikacji sieci Web az](/cli/azure/appservice/web#create) polecenia. 

aplikacji sieci web Hello hostingu miejsce do interfejsu API i zapewnia to aplikacja hello wdrożone tooview adresu URL.

Zastąp następujące polecenie, w hello  *\<nazwa_aplikacji >* o unikatowej nazwie. Jeśli `<app_name>` jest nie jest unikatowy, otrzymasz komunikat o błędzie hello "Witryny sieci Web o podanej nazwie < nazwa_aplikacji > już istnieje." Witaj domyślny adres URL aplikacji sieci web hello jest `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Podczas tworzenia aplikacji sieci web hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

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