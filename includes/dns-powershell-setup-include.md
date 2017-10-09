## <a name="set-up-azure-powershell-for-azure-dns"></a>Konfigurowanie programu Azure PowerShell dla usługi Azure DNS

### <a name="before-you-begin"></a>Przed rozpoczęciem

Sprawdź, czy masz hello poniższych elementach przed rozpoczęciem konfiguracji.

* Subskrypcja platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).
* Należy tooinstall hello najnowszą wersję hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Zaloguj się tooyour konto platformy Azure

Otwórz konsolę programu PowerShell i Połącz konto tooyour. Aby uzyskać więcej informacji, zobacz [przy użyciu programu PowerShell z usługą Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Wybierz subskrypcję hello
 
Sprawdź subskrypcje hello hello konta.

```powershell
Get-AzureRmSubscription
```

Wybierz z toouse Twojej subskrypcji platformy Azure.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Jednak ponieważ wszystkie zasoby DNS są globalne, a nie regionalne, wybór hello lokalizacja grupy zasobów nie ma wpływu na usługi Azure DNS.

Ten krok można pominąć, jeśli używasz istniejącej grupy zasobów.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>Rejestrowanie dostawcy zasobów

Usługa Azure DNS Hello jest zarządzana przez dostawcę zasobów Microsoft.Network hello. Twoja subskrypcja platformy Azure musi być zarejestrowany toouse tego dostawcy zasobów przed użyciem usługi Azure DNS. Jest to jednorazowa operacja dla każdej subskrypcji.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```