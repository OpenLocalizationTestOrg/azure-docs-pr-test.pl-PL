<span data-ttu-id="324a3-101">Użyj adresu URL hello Azure CLI tooget hello zdalnego wdrażania dla aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="324a3-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="324a3-102">Zastąp następujące polecenie, w hello  *\<nazwa_aplikacji >* o nazwie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="324a3-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="324a3-103">Konfigurowanie sieci lokalnej Git wdrożenia toobe stanie toopush toohello zdalnego.</span><span class="sxs-lookup"><span data-stu-id="324a3-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="324a3-104">Wypchnij toohello Azure zdalnego toodeploy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="324a3-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="324a3-105">Zostanie wyświetlony monit o hello hasło utworzone wcześniej podczas tworzenia hello wdrożenia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="324a3-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="324a3-106">Upewnij się, możesz wprowadzić hasło hello, utworzony we wcześniejszej części szybkiego startu hello i nie hasło hello używasz toolog toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="324a3-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
