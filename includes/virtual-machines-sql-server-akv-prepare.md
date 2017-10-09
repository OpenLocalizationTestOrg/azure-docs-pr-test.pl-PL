## <a name="prepare-for-akv-integration"></a>Przygotowanie do Integracja
toouse tooconfigure integracji magazynu kluczy Azure maszyny Wirtualnej programu SQL Server, istnieje kilka wymagań wstępnych: 

1. [Instalowanie programu Azure Powershell](#install-azure-powershell)
2. [Tworzenie usługi Azure Active Directory](#create-an-azure-active-directory)
3. [Tworzenie magazynu kluczy](#create-a-key-vault)

Witaj poniższych sekcjach opisano te warunki wstępne i hello informacje potrzebne toocollect toolater Uruchom hello — poleceń cmdlet programu PowerShell.

### <a name="install-azure-powershell"></a>Instalowanie programu Azure PowerShell
Upewnij się, że zainstalowano najnowszy zestaw Azure PowerShell SDK hello. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Tworzenie usługi Azure Active Directory
Najpierw należy toohave [usługi Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) w ramach subskrypcji. Między wiele korzyści umożliwia magazynu kluczy tooyour uprawnienia toogrant dla niektórych użytkowników i aplikacji.

Następnie należy zarejestrować aplikację przy użyciu usługi AAD. Zapewni to konto nazwy głównej usługi, które ma dostęp tooyour magazynu kluczy, które będą potrzebne maszyny Wirtualnej. W artykule usługi Azure Key Vault hello, te kroki można znaleźć w hello [zarejestrować aplikację w usłudze Azure Active Directory](../articles/key-vault/key-vault-get-started.md#register) sekcji, lub można czynności hello z zrzuty ekranu w hello **uzyskać tożsamości dla aplikacji hello sekcja** z [ten wpis w blogu](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Przed wykonaniem tych kroków, należy zauważyć, że możesz hello toocollect następujących informacji podczas tej rejestracji, który będzie później potrzebny po włączeniu integracji magazynu kluczy Azure na maszynie Wirtualnej SQL.

* Po dodaniu aplikacji hello Znajdź hello **identyfikator klienta** na powitania **Konfiguruj** kartę.   ![Identyfikator klienta usługi Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    Identyfikator klienta Hello jest przypisany nowsze toohello **$spName** parametr (nazwę główną usługi) w tooenable skrypt programu PowerShell hello integracji magazynu kluczy Azure. 
* Ponadto podczas tych czynności podczas tworzenia klucza, skopiować hello klucza tajnego klucza pokazane na powitania po zrzut ekranu. Ten klucza klucz tajny jest przypisany nowsze toohello **$spSecret** parametr (klucz tajny nazwy głównej usługi) w hello skrypt programu PowerShell.  
    ![Klucz tajny usługi Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* Musisz zezwolić tej nowej powitania toohave Identyfikatora klienta, na następujących uprawnień dostępu: **szyfrowania**, **odszyfrować**, **wrapKey**, **unwrapKey**, **znak**, i **Sprawdź**. Jest to zrobić za pomocą hello [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) polecenia cmdlet. Aby uzyskać więcej informacji, zobacz [autoryzacji hello aplikacji toouse hello klucza lub klucza tajnego](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Tworzenie magazynu kluczy
W kolejności toouse usługi Azure Key Vault toostore hello kluczy, który będzie używany do szyfrowania maszyny Wirtualnej należy magazynu kluczy tooa dostępu. Jeśli magazynu kluczy nie zostały już skonfigurowane, utwórz ją wykonać kroki hello w hello [wprowadzenie do korzystania z usługi Azure Key Vault](../articles/key-vault/key-vault-get-started.md) tematu. Przed wykonaniem tych kroków, należy pamiętać, że jest niektóre informacje potrzebne toocollect podczas tego zestawu zapasową, która będzie później potrzebny po włączeniu integracji magazynu kluczy Azure na maszynie Wirtualnej SQL.

Po wyświetleniu okna toohello Utwórz krok magazynu kluczy, zwrócił hello Uwaga **vaultUri** właściwość, która jest hello adres URL magazynu kluczy. W przykładzie hello podane w tym kroku przedstawiony poniżej nazwa magazynu kluczy hello jest ContosoKeyVault, w związku z tym adresem URL magazynu kluczy hello byłoby https://contosokeyvault.vault.azure.net/.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

adres URL magazynu kluczy Hello jest przypisany nowsze toohello **$akvURL** parametru w tooenable skrypt programu PowerShell hello integracji magazynu kluczy Azure.

