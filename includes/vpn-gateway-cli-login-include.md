<span data-ttu-id="311a4-101">Zaloguj się do subskrypcji platformy Azure za pomocą polecenia [az login](/cli/azure/#login) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.</span><span class="sxs-lookup"><span data-stu-id="311a4-101">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="311a4-102">Aby uzyskać więcej informacji na temat logowania się, zobacz artykuł [Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="311a4-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="311a4-103">Jeśli masz więcej niż jedną subskrypcję platformy Azure, wyświetl subskrypcje dla konta.</span><span class="sxs-lookup"><span data-stu-id="311a4-103">If you have more than one Azure subscription, list the subscriptions for the account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="311a4-104">Wskaż subskrypcję, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="311a4-104">Specify the subscription that you want to use.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```