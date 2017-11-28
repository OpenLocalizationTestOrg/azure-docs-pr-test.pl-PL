


## <a name="using-vm-extensions"></a><span data-ttu-id="c8e0e-101">Przy użyciu rozszerzeń maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c8e0e-101">Using VM Extensions</span></span>
<span data-ttu-id="c8e0e-102">Implementowanie rozszerzeń maszyny Wirtualnej Azure zachowania lub funkcje, które ułatwiają albo inne programy, które działają na maszynach wirtualnych Azure (na przykład **WebDeployForVSDevTest** rozszerzenia umożliwia programowi Visual Studio Web Deploy rozwiązań na maszynie Wirtualnej platformy Azure) lub podaj zdolność umożliwia interakcję z maszyną Wirtualną do obsługi niektóre inne zachowanie (na przykład umożliwia rozszerzenia dostępu do maszyny Wirtualnej z klientów programu PowerShell, interfejsu wiersza polecenia Azure i REST resetowania lub zmodyfikuj wartości dostępu zdalnego na maszynie Wirtualnej platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="c8e0e-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8e0e-103">Pełną listę rozszerzeń przez funkcje obsługują zobacz [rozszerzeń maszyny Wirtualnej platformy Azure i funkcje](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c8e0e-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="c8e0e-104">Ponieważ każde rozszerzenie maszyny Wirtualnej obsługuje określonych funkcji, dokładnie co można, a nie z rozszerzeniem jest zależna od rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span></span> <span data-ttu-id="c8e0e-105">W związku z tym przed zmodyfikowaniem maszyny Wirtualnej, sprawdź, czy znasz dokumentacji dla rozszerzenia maszyny Wirtualnej, którego chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span></span> <span data-ttu-id="c8e0e-106">Usunięcie niektórych rozszerzeń maszyny Wirtualnej nie jest obsługiwany; inne mają właściwości, które można ustawić które znacząco zmieniają zachowanie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="c8e0e-107">Typowe zadania są:</span><span class="sxs-lookup"><span data-stu-id="c8e0e-107">The most common tasks are:</span></span>

1. <span data-ttu-id="c8e0e-108">Znajdowanie dostępnych rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="c8e0e-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="c8e0e-109">Aktualizacja rozszerzeń załadowany</span><span class="sxs-lookup"><span data-stu-id="c8e0e-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="c8e0e-110">Dodawanie rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="c8e0e-110">Adding Extensions</span></span>
4. <span data-ttu-id="c8e0e-111">Usuwanie rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="c8e0e-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="c8e0e-112">Znajdowanie dostępnych rozszerzeń</span><span class="sxs-lookup"><span data-stu-id="c8e0e-112">Find Available Extensions</span></span>
<span data-ttu-id="c8e0e-113">Można znaleźć rozszerzenia i używanie rozszerzonych informacji:</span><span class="sxs-lookup"><span data-stu-id="c8e0e-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="c8e0e-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8e0e-114">PowerShell</span></span>
* <span data-ttu-id="c8e0e-115">Interfejs wiersza polecenia i Platform Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="c8e0e-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="c8e0e-116">Interfejs API protokołu REST zarządzania usługami</span><span class="sxs-lookup"><span data-stu-id="c8e0e-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="c8e0e-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8e0e-117">Azure PowerShell</span></span>
<span data-ttu-id="c8e0e-118">Niektóre rozszerzenia zostały poleceń cmdlet programu PowerShell, które są specyficzne dla nich, które mogą ułatwić ich konfiguracji z programu PowerShell; jednak następujące polecenia cmdlet działać dla wszystkich rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="c8e0e-119">Aby uzyskać informacje o dostępnych rozszerzeń służy następujące polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c8e0e-119">You can use the following cmdlets to obtain information about available extensions:</span></span>

* <span data-ttu-id="c8e0e-120">Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="c8e0e-121">Dla wystąpień maszyn wirtualnych, można użyć [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="c8e0e-122">Na przykład następujący przykładowy kod przedstawia sposób wyświetlania informacji dotyczących **IaaSDiagnostics** rozszerzenia przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="c8e0e-123">Interfejs wiersza polecenia platformy Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="c8e0e-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="c8e0e-124">Niektóre rozszerzenia zostały polecenia interfejsu wiersza polecenia Azure, które są specyficzne dla ich (Docker rozszerzenia maszyny Wirtualnej jest jednym z przykładów), która może ułatwić ich konfiguracji; Jednak poniższe polecenia działać dla wszystkich rozszerzeń maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span></span>

<span data-ttu-id="c8e0e-125">Można użyć **listy rozszerzeń maszyny wirtualnej azure** polecenie, aby uzyskać informacje o dostępnych rozszerzeń, a następnie użyj **—-json** opcję, aby wyświetlić wszystkie dostępne informacje o jedno lub więcej rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span></span> <span data-ttu-id="c8e0e-126">Jeśli nie używasz rozszerzenie nazwy, polecenie zwraca opisu JSON wszystkie dostępne rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="c8e0e-127">Na przykład następujący przykładowy kod przedstawia sposób wyświetlania informacji dotyczących **IaaSDiagnostics** rozszerzenia przy użyciu interfejsu wiersza polecenia Azure **listy rozszerzeń maszyny wirtualnej azure** polecenia i używa **—-json**  opcję, aby zwracać pełne informacje.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="c8e0e-128">Interfejsy API REST zarządzania usługami</span><span class="sxs-lookup"><span data-stu-id="c8e0e-128">Service Management REST APIs</span></span>
<span data-ttu-id="c8e0e-129">Aby uzyskać informacje o dostępnych rozszerzeń służy następujących interfejsów API REST:</span><span class="sxs-lookup"><span data-stu-id="c8e0e-129">You can use the following REST APIs to obtain information about available extensions:</span></span>

* <span data-ttu-id="c8e0e-130">Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć [listę dostępnych rozszerzeń](https://msdn.microsoft.com/library/dn169559.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="c8e0e-131">Aby wyświetlić listę wersji dostępne rozszerzenia, można użyć [wersji rozszerzenia listy](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8e0e-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="c8e0e-132">Dla wystąpień maszyn wirtualnych, można użyć [listy rozszerzeń zasobu](https://msdn.microsoft.com/library/dn495441.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="c8e0e-133">Aby wyświetlić listę wersji dostępne rozszerzenia, można użyć [wersji rozszerzenia zasobu listy](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8e0e-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="c8e0e-134">Dodawanie, aktualizowanie lub wyłączyć rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="c8e0e-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="c8e0e-135">Podczas tworzenia wystąpienia lub mogą być dodawane uruchomione wystąpienie można dodać rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-135">Extensions can be added when an instance is created or they can be added to a running instance.</span></span> <span data-ttu-id="c8e0e-136">Rozszerzenia może zostać zaktualizowany, wyłączone lub usunięte.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="c8e0e-137">Można wykonywać te akcje za pomocą poleceń cmdlet programu Azure PowerShell lub przy użyciu operacji interfejsu API REST zarządzania usługi.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span></span> <span data-ttu-id="c8e0e-138">Aby zainstalować i skonfigurować niektóre rozszerzenia są wymagane parametry.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-138">Parameters are required to install and set up some extensions.</span></span> <span data-ttu-id="c8e0e-139">Parametry publiczne i prywatne są obsługiwane dla rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="c8e0e-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8e0e-140">Azure PowerShell</span></span>
<span data-ttu-id="c8e0e-141">Za pomocą poleceń cmdlet programu Azure PowerShell jest najprostszym sposobem na dodawanie i aktualizowanie rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span></span> <span data-ttu-id="c8e0e-142">Korzystając z polecenia cmdlet rozszerzenia, większość ustawień konfiguracji rozszerzenia odbywa się automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span></span> <span data-ttu-id="c8e0e-143">W czasie konieczne może być programowane Dodawanie rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-143">At times, you may need to programmatically add an extension.</span></span> <span data-ttu-id="c8e0e-144">Należy to zrobić, należy podać konfiguracji rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-144">When you need to do this, you must provide the configuration of the extension.</span></span>

<span data-ttu-id="c8e0e-145">Następujące polecenia cmdlet umożliwia wiedzieć, czy rozszerzenie wymaga konfiguracji publiczne i prywatne parametrów:</span><span class="sxs-lookup"><span data-stu-id="c8e0e-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="c8e0e-146">Dla wystąpienia ról sieci web lub roli proces roboczy, można użyć **Get-AzureServiceAvailableExtension** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="c8e0e-147">Dla wystąpień maszyn wirtualnych, można użyć **Get-AzureVMAvailableExtension** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="c8e0e-148">Interfejsy API REST zarządzania usługami</span><span class="sxs-lookup"><span data-stu-id="c8e0e-148">Service Management REST APIs</span></span>
<span data-ttu-id="c8e0e-149">Podczas pobierania listy dostępnych rozszerzeń przy użyciu interfejsów API REST, pojawi się informacji na temat sposobu rozszerzenia ma zostać skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span></span> <span data-ttu-id="c8e0e-150">Zwracane informacje mogą być wyświetlane informacje o parametrach reprezentowany przez schemat publicznej i prywatnej schematu.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-150">The information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="c8e0e-151">Wartości parametrów publicznego są zwracane w zapytaniach dotyczących wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-151">Public parameter values are returned in queries about the instances.</span></span> <span data-ttu-id="c8e0e-152">Wartości parametrów prywatne nie są zwracane.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="c8e0e-153">Następujące interfejsy API REST umożliwia wiedzieć, czy rozszerzenie wymaga konfiguracji publiczne i prywatne parametrów:</span><span class="sxs-lookup"><span data-stu-id="c8e0e-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="c8e0e-154">Dla wystąpienia ról sieci web lub roli proces roboczy **PublicConfigurationSchema** i **PrivateConfigurationSchema** elementy zawierają informacje w odpowiedzi z [dostępne listy Rozszerzenia](https://msdn.microsoft.com/library/dn169559.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="c8e0e-155">Dla wystąpień maszyn wirtualnych, **PublicConfigurationSchema** i **PrivateConfigurationSchema** elementy zawierają informacje w odpowiedzi z [listy zasobów Rozszerzenia](https://msdn.microsoft.com/library/dn495441.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="c8e0e-156">Rozszerzenia za pomocą konfiguracji, które są zdefiniowane JSON.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="c8e0e-157">Gdy te typy rozszerzeń są używane, tylko **SampleConfig** element jest używany.</span><span class="sxs-lookup"><span data-stu-id="c8e0e-157">When these types of extensions are used, only the **SampleConfig** element is used.</span></span>
> 
> 

