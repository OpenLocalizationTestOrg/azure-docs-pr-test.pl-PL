
## <a name="start-your-powershell-session"></a>Uruchamianie sesji programu PowerShell
Najpierw można powinny mieć hello programu Azure PowerShell najnowsze zainstalowany i uruchomiony. Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Wiele nowych funkcji bazy danych SQL są obsługiwane tylko, gdy używasz hello [modelu wdrażania usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), dlatego w przykładach użyto hello [poleceń cmdlet programu PowerShell bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) dla Menedżera zasobów . model wdrażania zarządzania (klasyczne) usługi Hello [poleceń cmdlet do zarządzania usługi bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) są obsługiwane w celu zapewnienia zgodności z poprzednimi wersjami, ale zalecane jest użycie hello poleceń cmdlet Menedżera zasobów.
> 
> 

Uruchom hello [ **Add-AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) polecenia cmdlet, a użytkownik zobaczy tooenter ekranu logowania swoje poświadczenia. Użyj hello same poświadczenia Użyj toosign w toohello portalu Azure.

```PowerShell
Add-AzureRmAccount
```

Jeśli masz wiele subskrypcji, użyj hello [ **Set-AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) tooselect polecenia cmdlet, które subskrypcji należy używać w sesji programu PowerShell. toosee jaka subskrypcja hello bieżącego środowiska PowerShell korzysta z sesji, uruchom [ **Get-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). Uruchom wszystkie subskrypcje, toosee [ **Get-AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
