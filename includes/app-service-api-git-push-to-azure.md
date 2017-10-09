Użyj adresu URL hello Azure CLI tooget hello zdalnego wdrażania dla aplikacji interfejsu API. Zastąp następujące polecenie, w hello  *\<nazwa_aplikacji >* o nazwie aplikacji sieci web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Konfigurowanie sieci lokalnej Git wdrożenia toobe stanie toopush toohello zdalnego.

```bash
git remote add azure <URI from previous step>
```

Wypchnij toohello Azure zdalnego toodeploy aplikacji. Zostanie wyświetlony monit o hello hasło utworzone wcześniej podczas tworzenia hello wdrożenia użytkownika. Upewnij się, możesz wprowadzić hasło hello, utworzony we wcześniejszej części szybkiego startu hello i nie hasło hello używasz toolog toohello portalu Azure.

```bash
git push azure master
```
