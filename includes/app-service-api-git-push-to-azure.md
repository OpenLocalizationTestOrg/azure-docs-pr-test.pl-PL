<span data-ttu-id="9bec1-101">Użyj interfejsu wiersza polecenia platformy Azure, aby uzyskać adres URL zdalnego wdrożenia dla swojej aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9bec1-101">Use the Azure CLI to get the remote deployment URL for your API App.</span></span> <span data-ttu-id="9bec1-102">W poniższym poleceniu zastąp ciąg *\<nazwa_aplikacji>* nazwą swojej aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="9bec1-102">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="9bec1-103">Skonfiguruj swoje lokalne wdrożenie Git, aby było możliwe wypychanie do lokalizacji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="9bec1-103">Configure your local Git deployment to be able to push to the remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="9bec1-104">Wypchnij na zdalną platformę Azure w celu wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9bec1-104">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="9bec1-105">Zostanie wyświetlony monit o podanie hasła utworzonego wcześniej podczas tworzenia użytkownika wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9bec1-105">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="9bec1-106">Upewnij się, że zostało wprowadzone hasło utworzone wcześniej podczas postępowania zgodnie z przewodnikiem szybkiego startu, a nie hasło, którego używasz do logowania się w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9bec1-106">Make sure that you enter the password you created in earlier in the quickstart, and not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```
