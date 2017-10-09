## <a name="setting-up-powershell-for-resource-manager-templates"></a>Konfigurowanie środowiska PowerShell dla Menedżera zasobów szablonów
Przed użyciem programu Azure PowerShell z usługą Resource Manager, należy toohave hello właściwych środowiska Windows PowerShell i programu Azure PowerShell wersji.

### <a name="verify-powershell-versions"></a>Sprawdź wersje programu PowerShell
Sprawdź, czy masz środowiska Windows PowerShell w wersji 3.0 lub 4.0. toofind hello wersja programu Windows PowerShell, wpisz następujące polecenie w wierszu polecenia programu Windows PowerShell.

    $PSVersionTable

Zostanie wyświetlony hello następujące rodzaje informacji:

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


Sprawdź, czy hello z **PSVersion** 3.0 lub 4.0. Jeśli nie, zobacz [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) lub [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

### <a name="set-your-azure-account-and-subscription"></a>Ustawianie konta i subskrypcji platformy Azure
Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

Otwórz wiersz polecenia programu PowerShell systemu Azure i zaloguj się na tooAzure za pomocą tego polecenia.

    Login-AzureRmAccount

Jeśli masz wiele subskrypcji Azure, można wyświetlić listę subskrypcji platformy Azure za pomocą tego polecenia.

    Get-AzureRmSubscription

Zostanie wyświetlony hello następujące rodzaje informacji:

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

Możesz ustawić hello bieżącej subskrypcji Azure, uruchamiając następujące polecenia w wierszu polecenia programu Azure PowerShell hello. Zamień wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, hello poprawną nazwę.

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Aby uzyskać więcej informacji na temat subskrypcji platformy Azure i kont, zobacz [porady: łączenie subskrypcji tooyour](/powershell/azureps-cmdlets-docs#step-3-connect).

