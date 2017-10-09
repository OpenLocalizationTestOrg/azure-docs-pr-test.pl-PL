
## <a name="start-your-powershell-session"></a>Uruchamianie sesji programu PowerShell
Najpierw należy toohave hello najnowszych [programu Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) zainstalowana i uruchomiona. Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Witaj przykłady w tym temacie [modelu wdrażania usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), dlatego w przykładach użyto hello [poleceń cmdlet usługi Azure Resource Manager](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Uruchom hello [ **Add-AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet zostanie wyświetlone z logowaniem tooenter ekranu swoje poświadczenia. Użyj hello same poświadczenia Użyj toosign w toohello portalu Azure.

    Add-AzureRmAccount

Jeśli masz wiele subskrypcji, użyj hello [ **Set-AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) tooselect polecenia cmdlet, które subskrypcji należy używać w sesji programu PowerShell. toosee jaka subskrypcja hello bieżącego środowiska PowerShell korzysta z sesji, uruchom [ **Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). Uruchom wszystkie subskrypcje, toosee [ **Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

