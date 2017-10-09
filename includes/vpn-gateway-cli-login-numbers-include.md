1. <span data-ttu-id="31ac9-101">Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="31ac9-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="31ac9-102">Aby uzyskać więcej informacji na temat logowania się, zobacz artykuł [Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="31ac9-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="31ac9-103">Jeśli masz więcej niż jedną subskrypcją platformy Azure, Lista subskrypcji hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="31ac9-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="31ac9-104">Określ, które mają toouse subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="31ac9-104">Specify hello subscription that you want toouse.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```