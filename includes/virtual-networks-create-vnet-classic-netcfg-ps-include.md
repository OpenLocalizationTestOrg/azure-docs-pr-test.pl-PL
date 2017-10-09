## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="31dc0-101">Jak toocreate sieć wirtualną przy użyciu konfiguracji sieci plik programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="31dc0-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="31dc0-102">Platforma Azure korzysta toodefine pliku xml wszystkie sieci wirtualne tooa dostępnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="31dc0-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="31dc0-103">Można pobrać tego pliku, edytować toomodify lub usunąć istniejące sieci wirtualne i utworzyć nowe sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="31dc0-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="31dc0-104">Z tego samouczka, dowiesz się, jak toodownload tego pliku, określonej tooas sieci plik konfiguracji (lub netcfg) i go edytować toocreate nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="31dc0-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="31dc0-105">toolearn więcej informacji na temat hello pliku konfiguracji sieci, zobacz hello [schemat konfiguracji sieci wirtualnej platformy Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="31dc0-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="31dc0-106">toocreate sieć wirtualną przy użyciu pliku netcfg przy użyciu programu PowerShell, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="31dc0-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="31dc0-107">Jeśli nie znasz programu Azure PowerShell, pełną hello etapami hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) artykuł, a następnie zaloguj się tooAzure i wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="31dc0-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="31dc0-108">Za pomocą konsoli programu Azure PowerShell hello, użyj hello **Get-AzureVnetConfig** polecenia cmdlet toodownload hello konfiguracji pliku tooa katalogu sieciowego na komputerze, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="31dc0-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="31dc0-109">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="31dc0-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="31dc0-110">Otwórz plik hello zapisany w kroku 2, za pomocą dowolnej aplikacji edytora XML lub tekst i poszukaj hello  **<VirtualNetworkSites>**  elementu.</span><span class="sxs-lookup"><span data-stu-id="31dc0-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="31dc0-111">Jeśli masz już utworzone sieci każda sieć jest wyświetlana jako własnego  **<VirtualNetworkSite>**  elementu.</span><span class="sxs-lookup"><span data-stu-id="31dc0-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="31dc0-112">sieć wirtualna hello toocreate opisane w tym scenariuszu, Dodaj powitania po XML pod hello  **<VirtualNetworkSites>**  elementu:</span><span class="sxs-lookup"><span data-stu-id="31dc0-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

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
   
5. <span data-ttu-id="31dc0-113">Zapisz plik konfiguracji sieci hello.</span><span class="sxs-lookup"><span data-stu-id="31dc0-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="31dc0-114">Za pomocą konsoli programu Azure PowerShell hello, użyj hello **AzureVnetConfig zestaw** polecenia cmdlet tooupload hello pliku konfiguracji sieci, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="31dc0-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="31dc0-115">Zwrócone dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="31dc0-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="31dc0-116">Jeśli **OperationStatus** nie jest *zakończyło się pomyślnie* w hello zwrócone dane wyjściowe, sprawdź plik xml hello błędów i wykonaj krok 6 ponownie.</span><span class="sxs-lookup"><span data-stu-id="31dc0-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="31dc0-117">Za pomocą konsoli programu Azure PowerShell hello, użyj hello **Get-AzureVnetSite** tooverify polecenia cmdlet, które hello nowej sieci został dodany, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="31dc0-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="31dc0-118">Witaj zwracany (skracania) dane wyjściowe zawierają hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="31dc0-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
