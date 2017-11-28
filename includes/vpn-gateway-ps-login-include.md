<span data-ttu-id="3108e-101">Przed rozpoczęciem tej konfiguracji musisz zalogować się na koncie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3108e-101">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="3108e-102">Polecenie cmdlet wyświetla monit o podanie poświadczeń logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3108e-102">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="3108e-103">Po zalogowaniu pobiera ono ustawienia konta, aby były dostępne dla programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3108e-103">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span> <span data-ttu-id="3108e-104">Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3108e-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="3108e-105">Aby się zalogować, otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i połącz się ze swoim kontem.</span><span class="sxs-lookup"><span data-stu-id="3108e-105">To log in, open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="3108e-106">Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:</span><span class="sxs-lookup"><span data-stu-id="3108e-106">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3108e-107">Jeśli masz wiele subskrypcji platformy Azure, wyświetl subskrypcje dla konta.</span><span class="sxs-lookup"><span data-stu-id="3108e-107">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="3108e-108">Wskaż subskrypcję, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="3108e-108">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```