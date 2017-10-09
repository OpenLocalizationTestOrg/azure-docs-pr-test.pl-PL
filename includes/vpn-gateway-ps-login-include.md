<span data-ttu-id="36bb9-101">Przed rozpoczęciem tej konfiguracji, należy zalogować się tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36bb9-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="36bb9-102">polecenia cmdlet Hello monituje o hello poświadczenia logowania dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36bb9-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="36bb9-103">Po zalogowaniu pobraniu ustawienia konta tak, aby były dostępne tooAzure środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36bb9-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="36bb9-104">Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="36bb9-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="36bb9-105">toolog, otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień, a następnie połącz tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="36bb9-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="36bb9-106">Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="36bb9-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="36bb9-107">Jeśli masz wiele subskrypcji Azure, sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="36bb9-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="36bb9-108">Określ, które mają toouse subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="36bb9-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```