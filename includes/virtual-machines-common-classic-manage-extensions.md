


## <a name="using-vm-extensions"></a>Przy użyciu rozszerzeń maszyny Wirtualnej
Implementowanie rozszerzeń maszyny Wirtualnej Azure zachowania lub funkcje, które ułatwiają albo inne programy, które działają na maszynach wirtualnych Azure (na przykład Witaj **WebDeployForVSDevTest** rozszerzenia umożliwia tooWeb Visual Studio wdrażania rozwiązań na maszynie Wirtualnej platformy Azure) lub podaj Witaj możliwość toointeract z hello wirtualna toosupport niektóre inne zachowanie (na przykład można użyć rozszerzenia dostępu do maszyny Wirtualnej hello z programu PowerShell, hello wiersza polecenia platformy Azure i tooreset klienci pozostałe lub zmodyfikuj wartości dostępu zdalnego na maszynie Wirtualnej platformy Azure).

> [!IMPORTANT]
> Pełną listę rozszerzeń przez funkcje hello obsługują zobacz [rozszerzeń maszyny Wirtualnej platformy Azure i funkcje](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Ponieważ każde rozszerzenie maszyny Wirtualnej obsługuje określonych funkcji, dokładnie co można, a nie z rozszerzeniem jest zależna od hello rozszerzenia. W związku z tym przed zmodyfikowaniem maszyny Wirtualnej, upewnij się, że znasz hello dokumentacji hello rozszerzenia maszyny Wirtualnej ma toouse polecenie. Usunięcie niektórych rozszerzeń maszyny Wirtualnej nie jest obsługiwany; inne mają właściwości, które można ustawić które znacząco zmieniają zachowanie maszyny Wirtualnej.
> 
> 

najbardziej typowych zadań Hello są:

1. Znajdowanie dostępnych rozszerzeń
2. Aktualizacja rozszerzeń załadowany
3. Dodawanie rozszerzeń
4. Usuwanie rozszerzeń

## <a name="find-available-extensions"></a>Znajdowanie dostępnych rozszerzeń
Można znaleźć rozszerzenia i używanie rozszerzonych informacji:

* PowerShell
* Interfejs wiersza polecenia i Platform Azure (Azure CLI)
* Interfejs API protokołu REST zarządzania usługami

### <a name="azure-powershell"></a>Azure PowerShell
Niektóre rozszerzenia zostały poleceń cmdlet programu PowerShell, które są określone toothem, które mogą ułatwić ich konfiguracji z programu PowerShell; ale hello następujących poleceń cmdlet dla wszystkich rozszerzeń maszyny Wirtualnej.

Można użyć następujących poleceń cmdlet tooobtain informacji o dostępnych rozszerzeń hello:

* Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) polecenia cmdlet.
* Dla wystąpień maszyn wirtualnych, można użyć hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) polecenia cmdlet.
  
   Na przykład Witaj po kodu przykładzie pokazano sposób toolist informacje dotyczące hello **IaaSDiagnostics** rozszerzenia przy użyciu programu PowerShell.
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a>Interfejs wiersza polecenia platformy Azure (Azure CLI)
Niektóre rozszerzenia zostały poleceń interfejsu wiersza polecenia Azure, które są określone toothem (hello Docker rozszerzenia maszyny Wirtualnej jest jednym z przykładów), która może ułatwić ich konfiguracji; ale hello następujące polecenia pracy dla wszystkich rozszerzeń maszyny Wirtualnej.

Można użyć hello **listy rozszerzeń maszyny wirtualnej azure** polecenia tooobtain informacji o dostępnych rozszerzeń, a następnie użyj hello **—-json** opcję toodisplay wszystkie dostępne informacje o jedno lub więcej rozszerzeń. Jeśli nie używasz rozszerzenie nazwy, hello polecenie zwraca opisu JSON wszystkie dostępne rozszerzenia.

Na przykład hello poniższy przykład kodu pokazuje, jak toolist hello informacje dotyczące hello **IaaSDiagnostics** przy użyciu rozszerzenia hello Azure CLI **listy rozszerzeń maszyny wirtualnej azure** polecenia i używa hello **—-json** opcję tooreturn pełne informacje.

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a>Interfejsy API REST zarządzania usługami
Program hello następujących interfejsów API REST tooobtain informacji o dostępnych rozszerzeń:

* Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć hello [listę dostępnych rozszerzeń](https://msdn.microsoft.com/library/dn169559.aspx) operacji. wersje hello toolist dostępne rozszerzenia, można użyć [wersji rozszerzenia listy](https://msdn.microsoft.com/library/dn495437.aspx).
* Dla wystąpień maszyn wirtualnych, można użyć hello [listy rozszerzeń zasobu](https://msdn.microsoft.com/library/dn495441.aspx) operacji. wersje hello toolist dostępne rozszerzenia, można użyć [wersji rozszerzenia zasobu listy](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Dodawanie, aktualizowanie lub wyłączyć rozszerzenia
Podczas tworzenia wystąpienia lub mogą być dodawane tooa uruchomione wystąpienie można dodać rozszerzenia. Rozszerzenia może zostać zaktualizowany, wyłączone lub usunięte. Za pomocą poleceń cmdlet programu Azure PowerShell lub przy użyciu operacji interfejsu API REST zarządzania usługi hello można wykonywać te akcje. Parametry są wymagane tooinstall i skonfigurować niektóre rozszerzenia. Parametry publiczne i prywatne są obsługiwane dla rozszerzeń.

### <a name="azure-powershell"></a>Azure PowerShell
Za pomocą poleceń cmdlet programu Azure PowerShell jest hello Najprostszym sposobem tooadd i aktualizacji rozszerzenia. Korzystając z polecenia cmdlet rozszerzenia hello, większość konfiguracji hello rozszerzenia hello odbywa się automatycznie. Czasami może być konieczne tooprogrammatically dodać rozszerzenie. Gdy toodo to konieczne, należy podać konfiguracji hello hello rozszerzenia.

Program hello po tooknow poleceń cmdlet, czy rozszerzenie wymaga konfiguracji parametrów publicznych i prywatnych:

* Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć hello **Get-AzureServiceAvailableExtension** polecenia cmdlet.
* Dla wystąpień maszyn wirtualnych, można użyć hello **Get-AzureVMAvailableExtension** polecenia cmdlet.

### <a name="service-management-rest-apis"></a>Interfejsy API REST zarządzania usługami
Podczas pobierania listy dostępnych rozszerzeń przy użyciu hello interfejsów API REST, pojawi się informacji na temat sposobu rozszerzenia hello jest toobe skonfigurowany. zwracane informacje Hello mogą być wyświetlane informacje o parametrach reprezentowany przez schemat publicznej i prywatnej schematu. Wartości parametrów publicznego są zwracane w zapytaniach o wystąpieniach hello. Wartości parametrów prywatne nie są zwracane.

Program hello po tooknow interfejsów API REST, czy rozszerzenie wymaga konfiguracji parametrów publicznych i prywatnych:

* Dla wystąpienia ról sieci web lub roli proces roboczy hello **PublicConfigurationSchema** i **PrivateConfigurationSchema** elementy zawierają informacje hello hello odpowiedzi z hello [listy Dostępne rozszerzenia](https://msdn.microsoft.com/library/dn169559.aspx) operacji.
* Dla wystąpień maszyn wirtualnych hello **PublicConfigurationSchema** i **PrivateConfigurationSchema** elementy zawierają informacje hello hello odpowiedzi z hello [listy Rozszerzeń zasobu](https://msdn.microsoft.com/library/dn495441.aspx) operacji.

> [!NOTE]
> Rozszerzenia za pomocą konfiguracji, które są zdefiniowane JSON. W przypadku tych typów rozszerzeń tylko hello **SampleConfig** element jest używany.
> 
> 

