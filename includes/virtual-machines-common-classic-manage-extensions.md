


## <a name="using-vm-extensions"></a><span data-ttu-id="a77b6-101">Przy użyciu rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="a77b6-101">Using VM Extensions</span></span>
<span data-ttu-id="a77b6-102">Implementowanie rozszerzeń maszyny Wirtualnej Azure zachowania lub funkcje, które ułatwiają albo inne programy, które działają na maszynach wirtualnych Azure (na przykład Witaj **WebDeployForVSDevTest** rozszerzenia umożliwia tooWeb Visual Studio wdrażania rozwiązań na maszynie Wirtualnej platformy Azure) lub podaj Witaj możliwość toointeract z hello wirtualna toosupport niektóre inne zachowanie (na przykład można użyć rozszerzenia dostępu do maszyny Wirtualnej hello z programu PowerShell, hello wiersza polecenia platformy Azure i tooreset klienci pozostałe lub zmodyfikuj wartości dostępu zdalnego na maszynie Wirtualnej platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="a77b6-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a77b6-103">Pełną listę rozszerzeń przez funkcje hello obsługują zobacz [rozszerzeń maszyny Wirtualnej platformy Azure i funkcje](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a77b6-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a77b6-104">Ponieważ każde rozszerzenie maszyny Wirtualnej obsługuje określonych funkcji, dokładnie co można, a nie z rozszerzeniem jest zależna od hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a77b6-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="a77b6-105">W związku z tym przed zmodyfikowaniem maszyny Wirtualnej, upewnij się, że znasz hello dokumentacji hello rozszerzenia maszyny Wirtualnej ma toouse polecenie.</span><span class="sxs-lookup"><span data-stu-id="a77b6-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="a77b6-106">Usunięcie niektórych rozszerzeń maszyny Wirtualnej nie jest obsługiwany; inne mają właściwości, które można ustawić które znacząco zmieniają zachowanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a77b6-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="a77b6-107">najbardziej typowych zadań Hello są:</span><span class="sxs-lookup"><span data-stu-id="a77b6-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="a77b6-108">Znajdowanie dostępnych rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="a77b6-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="a77b6-109">Aktualizacja rozszerzeń załadowany</span><span class="sxs-lookup"><span data-stu-id="a77b6-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="a77b6-110">Dodawanie rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="a77b6-110">Adding Extensions</span></span>
4. <span data-ttu-id="a77b6-111">Usuwanie rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="a77b6-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="a77b6-112">Znajdowanie dostępnych rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="a77b6-112">Find Available Extensions</span></span>
<span data-ttu-id="a77b6-113">Można znaleźć rozszerzenia i używanie rozszerzonych informacji:</span><span class="sxs-lookup"><span data-stu-id="a77b6-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="a77b6-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a77b6-114">PowerShell</span></span>
* <span data-ttu-id="a77b6-115">Interfejs wiersza polecenia i Platform Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="a77b6-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="a77b6-116">Interfejs API protokołu REST zarządzania usługami</span><span class="sxs-lookup"><span data-stu-id="a77b6-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="a77b6-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a77b6-117">Azure PowerShell</span></span>
<span data-ttu-id="a77b6-118">Niektóre rozszerzenia zostały poleceń cmdlet programu PowerShell, które są określone toothem, które mogą ułatwić ich konfiguracji z programu PowerShell; ale hello następujących poleceń cmdlet dla wszystkich rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a77b6-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="a77b6-119">Można użyć następujących poleceń cmdlet tooobtain informacji o dostępnych rozszerzeń hello:</span><span class="sxs-lookup"><span data-stu-id="a77b6-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="a77b6-120">Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a77b6-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="a77b6-121">Dla wystąpień maszyn wirtualnych, można użyć hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a77b6-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="a77b6-122">Na przykład Witaj po kodu przykładzie pokazano sposób toolist informacje dotyczące hello **IaaSDiagnostics** rozszerzenia przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a77b6-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="a77b6-123">Interfejs wiersza polecenia platformy Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="a77b6-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="a77b6-124">Niektóre rozszerzenia zostały poleceń interfejsu wiersza polecenia Azure, które są określone toothem (hello Docker rozszerzenia maszyny Wirtualnej jest jednym z przykładów), która może ułatwić ich konfiguracji; ale hello następujące polecenia pracy dla wszystkich rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a77b6-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="a77b6-125">Można użyć hello **listy rozszerzeń maszyny wirtualnej azure** polecenia tooobtain informacji o dostępnych rozszerzeń, a następnie użyj hello **—-json** opcję toodisplay wszystkie dostępne informacje o jedno lub więcej rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="a77b6-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="a77b6-126">Jeśli nie używasz rozszerzenie nazwy, hello polecenie zwraca opisu JSON wszystkie dostępne rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a77b6-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="a77b6-127">Na przykład hello poniższy przykład kodu pokazuje, jak toolist hello informacje dotyczące hello **IaaSDiagnostics** przy użyciu rozszerzenia hello Azure CLI **listy rozszerzeń maszyny wirtualnej azure** polecenia i używa hello **—-json** opcję tooreturn pełne informacje.</span><span class="sxs-lookup"><span data-stu-id="a77b6-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="a77b6-128">Interfejsy API REST zarządzania usługami</span><span class="sxs-lookup"><span data-stu-id="a77b6-128">Service Management REST APIs</span></span>
<span data-ttu-id="a77b6-129">Program hello następujących interfejsów API REST tooobtain informacji o dostępnych rozszerzeń:</span><span class="sxs-lookup"><span data-stu-id="a77b6-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="a77b6-130">Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć hello [listę dostępnych rozszerzeń](https://msdn.microsoft.com/library/dn169559.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="a77b6-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="a77b6-131">wersje hello toolist dostępne rozszerzenia, można użyć [wersji rozszerzenia listy](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="a77b6-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="a77b6-132">Dla wystąpień maszyn wirtualnych, można użyć hello [listy rozszerzeń zasobu](https://msdn.microsoft.com/library/dn495441.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="a77b6-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="a77b6-133">wersje hello toolist dostępne rozszerzenia, można użyć [wersji rozszerzenia zasobu listy](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="a77b6-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="a77b6-134">Dodawanie, aktualizowanie lub wyłączyć rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="a77b6-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="a77b6-135">Podczas tworzenia wystąpienia lub mogą być dodawane tooa uruchomione wystąpienie można dodać rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a77b6-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="a77b6-136">Rozszerzenia może zostać zaktualizowany, wyłączone lub usunięte.</span><span class="sxs-lookup"><span data-stu-id="a77b6-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="a77b6-137">Za pomocą poleceń cmdlet programu Azure PowerShell lub przy użyciu operacji interfejsu API REST zarządzania usługi hello można wykonywać te akcje.</span><span class="sxs-lookup"><span data-stu-id="a77b6-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="a77b6-138">Parametry są wymagane tooinstall i skonfigurować niektóre rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a77b6-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="a77b6-139">Parametry publiczne i prywatne są obsługiwane dla rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="a77b6-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="a77b6-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a77b6-140">Azure PowerShell</span></span>
<span data-ttu-id="a77b6-141">Za pomocą poleceń cmdlet programu Azure PowerShell jest hello Najprostszym sposobem tooadd i aktualizacji rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a77b6-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="a77b6-142">Korzystając z polecenia cmdlet rozszerzenia hello, większość konfiguracji hello rozszerzenia hello odbywa się automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a77b6-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="a77b6-143">Czasami może być konieczne tooprogrammatically dodać rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="a77b6-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="a77b6-144">Gdy toodo to konieczne, należy podać konfiguracji hello hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="a77b6-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="a77b6-145">Program hello po tooknow poleceń cmdlet, czy rozszerzenie wymaga konfiguracji parametrów publicznych i prywatnych:</span><span class="sxs-lookup"><span data-stu-id="a77b6-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="a77b6-146">Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć hello **Get-AzureServiceAvailableExtension** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a77b6-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="a77b6-147">Dla wystąpień maszyn wirtualnych, można użyć hello **Get-AzureVMAvailableExtension** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a77b6-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="a77b6-148">Interfejsy API REST zarządzania usługami</span><span class="sxs-lookup"><span data-stu-id="a77b6-148">Service Management REST APIs</span></span>
<span data-ttu-id="a77b6-149">Podczas pobierania listy dostępnych rozszerzeń przy użyciu hello interfejsów API REST, pojawi się informacji na temat sposobu rozszerzenia hello jest toobe skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="a77b6-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="a77b6-150">zwracane informacje Hello mogą być wyświetlane informacje o parametrach reprezentowany przez schemat publicznej i prywatnej schematu.</span><span class="sxs-lookup"><span data-stu-id="a77b6-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="a77b6-151">Wartości parametrów publicznego są zwracane w zapytaniach o wystąpieniach hello.</span><span class="sxs-lookup"><span data-stu-id="a77b6-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="a77b6-152">Wartości parametrów prywatne nie są zwracane.</span><span class="sxs-lookup"><span data-stu-id="a77b6-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="a77b6-153">Program hello po tooknow interfejsów API REST, czy rozszerzenie wymaga konfiguracji parametrów publicznych i prywatnych:</span><span class="sxs-lookup"><span data-stu-id="a77b6-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="a77b6-154">Dla wystąpienia ról sieci web lub roli proces roboczy hello **PublicConfigurationSchema** i **PrivateConfigurationSchema** elementy zawierają informacje hello hello odpowiedzi z hello [listy Dostępne rozszerzenia](https://msdn.microsoft.com/library/dn169559.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="a77b6-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="a77b6-155">Dla wystąpień maszyn wirtualnych hello **PublicConfigurationSchema** i **PrivateConfigurationSchema** elementy zawierają informacje hello hello odpowiedzi z hello [listy Rozszerzeń zasobu](https://msdn.microsoft.com/library/dn495441.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="a77b6-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="a77b6-156">Rozszerzenia za pomocą konfiguracji, które są zdefiniowane JSON.</span><span class="sxs-lookup"><span data-stu-id="a77b6-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="a77b6-157">W przypadku tych typów rozszerzeń tylko hello **SampleConfig** element jest używany.</span><span class="sxs-lookup"><span data-stu-id="a77b6-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

