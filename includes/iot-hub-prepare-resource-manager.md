## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Przygotowanie tooauthenticate żądań usługi Azure Resource Manager
Musi uwierzytelniać wszystkie operacje hello, które należy wykonać na zasobów przy użyciu hello [usługi Azure Resource Manager] [ lnk-authenticate-arm] z usługi Azure Active Directory (AD). Najprostszym sposobem tooconfigure Hello jest toouse programu PowerShell lub interfejsu wiersza polecenia platformy Azure.

Zainstaluj hello [poleceń cmdlet programu Azure PowerShell] [ lnk-powershell-install] przed kontynuowaniem.

Witaj, jak po Pokaż kroki tooset się uwierzytelniania hasła dla aplikacji usługi AD przy użyciu programu PowerShell. Te polecenia można wykonać w standardowej sesji programu PowerShell.

1. Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello następujące polecenie:

    ```powershell
    Login-AzureRmAccount
    ```

1. Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika. Użyj następującego polecenia toolist hello subskrypcji platformy Azure, dostępne dla Ciebie toouse hello:

    ```powershell
    Get-AzureRMSubscription
    ```

    Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toomanage Centrum IoT hello. Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Zanotuj Twojej **TenantId** i **SubscriptionId**. Należy je później.
3. Utwórz nową aplikację usługi Azure Active Directory przy użyciu hello następujące polecenie, zastępując symbole zastępcze hello:
   
   * **{Nazwa wyświetlana}:** nazwę wyświetlaną dla aplikacji, takich jak **MySampleApp**
   * **{Adres URL strony głównej}:** hello adres URL strony głównej hello aplikacji, takich jak **http://mysampleapp/home**. Ten adres URL nie jest konieczne toopoint tooa rzeczywistej aplikacji.
   * **{Identyfikator aplikacji}:** Unikatowy identyfikator **http://mysampleapp**. Ten adres URL nie jest konieczne toopoint tooa rzeczywistej aplikacji.
   * **{Hasło}:** hasła, użyj tooauthenticate z aplikacją.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Zanotuj hello **ApplicationId** aplikacji hello został utworzony. Należy to później.
5. Utwórz nową główną nazwę usługi przy użyciu hello następujące polecenie, zastępując **{MyApplicationId}** z hello **ApplicationId** hello w poprzednim kroku:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Konfigurowanie przypisania roli przy użyciu hello następujące polecenie, zastępując **{MyApplicationId}** z Twojej **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Tworzenie aplikacji hello Azure AD, która umożliwia tooauthenticate z niestandardowych aplikacji C# zostało zakończone. Potrzebne są następujące wartości w dalszej części tego samouczka hello:

* Dla identyfikatora dzierżawcy
* SubscriptionId
* Identyfikator aplikacji
* Hasło

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
