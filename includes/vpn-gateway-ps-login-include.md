Przed rozpoczęciem tej konfiguracji, należy zalogować się tooyour konto platformy Azure. polecenia cmdlet Hello monituje o hello poświadczenia logowania dla konta platformy Azure. Po zalogowaniu pobraniu ustawienia konta tak, aby były dostępne tooAzure środowiska PowerShell. Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

toolog, otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień, a następnie połącz tooyour konta. Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:

```powershell
Login-AzureRmAccount
```

Jeśli masz wiele subskrypcji Azure, sprawdź subskrypcje hello hello konta.

```powershell
Get-AzureRmSubscription
```

Określ, które mają toouse subskrypcji hello.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```