## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>Jak toocreate sieć wirtualną przy użyciu konfiguracji sieci plik programu PowerShell
Platforma Azure korzysta toodefine pliku xml wszystkie sieci wirtualne tooa dostępnych subskrypcji. Można pobrać tego pliku, edytować toomodify lub usunąć istniejące sieci wirtualne i utworzyć nowe sieci wirtualnej. Z tego samouczka, dowiesz się, jak toodownload tego pliku, określonej tooas sieci plik konfiguracji (lub netcfg) i go edytować toocreate nowej sieci wirtualnej. toolearn więcej informacji na temat hello pliku konfiguracji sieci, zobacz hello [schemat konfiguracji sieci wirtualnej platformy Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate sieć wirtualną przy użyciu pliku netcfg przy użyciu programu PowerShell, pełną hello następujące kroki:

1. Jeśli nie znasz programu Azure PowerShell, pełną hello etapami hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) artykuł, a następnie zaloguj się tooAzure i wybierz subskrypcję.
2. Za pomocą konsoli programu Azure PowerShell hello, użyj hello **Get-AzureVnetConfig** polecenia cmdlet toodownload hello konfiguracji pliku tooa katalogu sieciowego na komputerze, uruchamiając następujące polecenie hello: 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Oczekiwane dane wyjściowe:
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Otwórz plik hello zapisany w kroku 2, za pomocą dowolnej aplikacji edytora XML lub tekst i poszukaj hello  **<VirtualNetworkSites>**  elementu. Jeśli masz już utworzone sieci każda sieć jest wyświetlana jako własnego  **<VirtualNetworkSite>**  elementu.
4. sieć wirtualna hello toocreate opisane w tym scenariuszu, Dodaj powitania po XML pod hello  **<VirtualNetworkSites>**  elementu:

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. Zapisz plik konfiguracji sieci hello.
6. Za pomocą konsoli programu Azure PowerShell hello, użyj hello **AzureVnetConfig zestaw** polecenia cmdlet tooupload hello pliku konfiguracji sieci, uruchamiając następujące polecenie hello: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Zwrócone dane wyjściowe:
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Jeśli **OperationStatus** nie jest *zakończyło się pomyślnie* w hello zwrócone dane wyjściowe, sprawdź plik xml hello błędów i wykonaj krok 6 ponownie.

7. Za pomocą konsoli programu Azure PowerShell hello, użyj hello **Get-AzureVnetSite** tooverify polecenia cmdlet, które hello nowej sieci został dodany, uruchamiając następujące polecenie hello: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Witaj zwracany (skracania) dane wyjściowe zawierają hello następującego tekstu:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
