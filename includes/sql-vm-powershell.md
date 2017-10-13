
## <a name="start-your-powershell-session"></a>Uruchamianie sesji programu PowerShell
Najpierw musisz mieć najnowszej [programu Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) zainstalowana i uruchomiona. Aby uzyskać szczegółowe informacje, zobacz artykuł [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (Instalowanie i konfigurowanie programu Azure PowerShell).

> [!NOTE]
> Przykłady w tym temacie [modelu wdrażania usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), dlatego w przykładach użyto [poleceń cmdlet usługi Azure Resource Manager](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Uruchom [ **Add-AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet zostanie wyświetlone logowania na ekranie, aby wprowadzić swoje poświadczenia. Użyj tych samych poświadczeń, których używasz do logowania w witrynie Azure Portal.

    Add-AzureRmAccount

Jeśli masz wiele subskrypcji, użyj [ **Set-AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) Wybierz subskrypcję, która sesji programu PowerShell należy użyć polecenia cmdlet. Aby sprawdzić, która subskrypcja jest używana w bieżącej sesji programu PowerShell, uruchom polecenie [**Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). Aby wyświetlić wszystkie subskrypcje, uruchom polecenie [**Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

