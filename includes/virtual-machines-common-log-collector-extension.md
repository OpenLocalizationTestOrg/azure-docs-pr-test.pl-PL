
<span data-ttu-id="83147-101">Diagnozowanie problemów z usługą w chmurze Microsoft Azure wymaga zbieranie plików dziennika usługi hello na maszynach wirtualnych, ponieważ występują problemy z hello.</span><span class="sxs-lookup"><span data-stu-id="83147-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="83147-102">Można użyć hello AzureLogCollector rozszerzenia na żądanie tooperfom jednorazowe kolekcję dzienników z maszyn wirtualnych usługi w chmurze (od ról sieć web i roli proces roboczy) i transfer hello zebrane pliki tooan kontem magazynu platformy Azure — wszystko to bez zdalne logowanie tooany hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="83147-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="83147-103">Opisy dla większości hello rejestrowane informacje znajdują się w http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="83147-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="83147-104">Zależne od typów hello toobe pliki pobierane są dwa tryby kolekcji.</span><span class="sxs-lookup"><span data-stu-id="83147-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="83147-105">Gość Azure dzienniki agentów tylko (GA).</span><span class="sxs-lookup"><span data-stu-id="83147-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="83147-106">Ten tryb kolekcji zawiera wszystkich agentów gości pokrewne tooAzure hello dzienniki i inne składniki platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="83147-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="83147-107">Wszystkie dzienniki (pełną).</span><span class="sxs-lookup"><span data-stu-id="83147-107">All Logs (Full).</span></span> <span data-ttu-id="83147-108">Ten tryb kolekcji będzie zbierać wszystkie pliki w trybie GA plus:</span><span class="sxs-lookup"><span data-stu-id="83147-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="83147-109">dzienniki zdarzeń systemu i aplikacji</span><span class="sxs-lookup"><span data-stu-id="83147-109">system and application event logs</span></span>
  * <span data-ttu-id="83147-110">Dzienniki błędów HTTP</span><span class="sxs-lookup"><span data-stu-id="83147-110">HTTP error logs</span></span>
  * <span data-ttu-id="83147-111">Dzienniki programu IIS</span><span class="sxs-lookup"><span data-stu-id="83147-111">IIS Logs</span></span>
  * <span data-ttu-id="83147-112">Dzienniki instalacji</span><span class="sxs-lookup"><span data-stu-id="83147-112">Setup logs</span></span>
  * <span data-ttu-id="83147-113">inne dzienniki systemu</span><span class="sxs-lookup"><span data-stu-id="83147-113">other system logs</span></span>

<span data-ttu-id="83147-114">W obu trybach kolekcji można określić przy użyciu kolekcji hello następujące struktury folderów kolekcji dodatkowe dane:</span><span class="sxs-lookup"><span data-stu-id="83147-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="83147-115">**Nazwa**: Nazwa hello hello kolekcji, która będzie używana jako nazwa podfolderu wewnątrz toobe pliku zip hello hello zbierane.</span><span class="sxs-lookup"><span data-stu-id="83147-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="83147-116">**Lokalizacja**: hello toohello folder ścieżki na maszynie wirtualnej hello gdzie będą zbierane pliku.</span><span class="sxs-lookup"><span data-stu-id="83147-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="83147-117">**SearchPattern**: hello wzorzec nazw hello toobe pliki pobierane.</span><span class="sxs-lookup"><span data-stu-id="83147-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="83147-118">Domyślna to "*"</span><span class="sxs-lookup"><span data-stu-id="83147-118">Default is “*”</span></span>
* <span data-ttu-id="83147-119">**Cykliczne**: Jeśli hello pliki będą zbierane rekursywnie w folderze hello.</span><span class="sxs-lookup"><span data-stu-id="83147-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83147-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="83147-120">Prerequisites</span></span>
* <span data-ttu-id="83147-121">Należy toohave konta magazynu dla plików zip toosave wygenerowany rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="83147-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="83147-122">Należy upewnić się, że używasz V0.8.0 poleceń cmdlet programu PowerShell Azure lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="83147-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="83147-123">Aby uzyskać więcej informacji, zobacz [Azure pobiera](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="83147-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="83147-124">Dodaj rozszerzenie hello</span><span class="sxs-lookup"><span data-stu-id="83147-124">Add hello extension</span></span>
<span data-ttu-id="83147-125">Można użyć [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) poleceń cmdlet lub [API REST zarządzania usługami](https://msdn.microsoft.com/library/ee460799.aspx) hello tooadd AzureLogCollector rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="83147-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="83147-126">Dla usług w chmurze, hello istniejącego polecenia cmdlet Azure Powershell, **AzureServiceExtension zestaw**, mogą być używane tooenable hello rozszerzenia dla wystąpień roli usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="83147-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="83147-127">Za każdym razem, gdy to rozszerzenie jest włączona za pomocą tego polecenia cmdlet, zbieranie danych dziennika zostanie wywołany dla wystąpień roli hello wybrane wybranych ról.</span><span class="sxs-lookup"><span data-stu-id="83147-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="83147-128">W przypadku maszyn wirtualnych hello istniejącego polecenia cmdlet Azure Powershell, **AzureVMExtension zestaw**, mogą być używane tooenable hello rozszerzenia na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="83147-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="83147-129">Za każdym razem, gdy to rozszerzenie jest włączona za pomocą poleceń cmdlet hello, zbierania dzienników jest wyzwalane w każdym wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="83147-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="83147-130">Wewnętrznie to rozszerzenie używa hello PublicConfiguration opartych na formacie JSON i PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="83147-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="83147-131">następujące Hello jest układ hello próbki JSON konfiguracji publiczne i prywatne.</span><span class="sxs-lookup"><span data-stu-id="83147-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="83147-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="83147-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="83147-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="83147-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="83147-134">To rozszerzenie nie wymaga **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="83147-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="83147-135">Podobnie można zapewnić pustą strukturą hello **— PrivateConfiguration** argumentu.</span><span class="sxs-lookup"><span data-stu-id="83147-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="83147-136">Możesz wykonać jedną z dwóch hello następujące kroki tooadd hello AzureLogCollector tooone lub więcej wystąpień usługi w chmurze lub maszynę wirtualną wybranych ról, które wyzwalaczy hello kolekcje w każdej toorun maszyny Wirtualnej i wysyłać hello zebrane pliki tooAzure konta określona.</span><span class="sxs-lookup"><span data-stu-id="83147-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="83147-137">Dodawanie jako rozszerzenie usługi</span><span class="sxs-lookup"><span data-stu-id="83147-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="83147-138">Wykonaj hello instrukcje tooconnect programu Azure PowerShell tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="83147-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="83147-139">Określ nazwę usługi hello, miejsca, ról i toowhich wystąpień roli mają tooadd i włączyć rozszerzenie AzureLogCollector hello.</span><span class="sxs-lookup"><span data-stu-id="83147-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="83147-140">Określ folder dodatkowe dane hello, dla której będą zbierane pliki (ten krok jest opcjonalny).</span><span class="sxs-lookup"><span data-stu-id="83147-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="83147-141">Można użyć tokenu `%roleroot%` toospecify hello roli katalog główny dysku, ponieważ nie używa dysk stały.</span><span class="sxs-lookup"><span data-stu-id="83147-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="83147-142">Podaj nazwę konta magazynu Azure hello i klucza toowhich zebrane pliki zostaną przekazane.</span><span class="sxs-lookup"><span data-stu-id="83147-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="83147-143">Wywołania hello SetAzureServiceLogCollector.ps1 (dołączony na końcu artykułu hello hello) jako sposób tooenable hello AzureLogCollector rozszerzenia dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="83147-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="83147-144">Po zakończeniu wykonywania hello można znaleźć pliku hello przekazany w`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="83147-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="83147-145">Witaj poniżej znajduje się definicja hello hello parametry przekazywane toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="83147-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="83147-146">(To jest kopiowana poniżej również.)</span><span class="sxs-lookup"><span data-stu-id="83147-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="83147-147">*ServiceName*: Nazwa usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="83147-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="83147-148">*Role*: lista ról, takich jak "WebRole1" lub "WorkerRole1".</span><span class="sxs-lookup"><span data-stu-id="83147-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="83147-149">*Wystąpienia*: Lista nazw hello wystąpień roli oddzielonych przecinkami — Użyj hello ciąg symbolu wieloznacznego ("*") dla wszystkich wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="83147-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="83147-150">*Gniazdo*: nazwa miejsca.</span><span class="sxs-lookup"><span data-stu-id="83147-150">*Slot*: Slot name.</span></span> <span data-ttu-id="83147-151">"Production" lub "Tymczasowości".</span><span class="sxs-lookup"><span data-stu-id="83147-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="83147-152">*Tryb*: tryb kolekcji.</span><span class="sxs-lookup"><span data-stu-id="83147-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="83147-153">"Pełnej" lub "GA".</span><span class="sxs-lookup"><span data-stu-id="83147-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="83147-154">*StorageAccountName*: Nazwa Azure konta magazynu do przechowywania zbieranych danych.</span><span class="sxs-lookup"><span data-stu-id="83147-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="83147-155">*StorageAccountKey*: klucz konta magazynu Name Azure.</span><span class="sxs-lookup"><span data-stu-id="83147-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="83147-156">*AdditionalDataLocationList*: Lista hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="83147-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="83147-157">Dodawanie jako rozszerzenie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="83147-157">Adding as a VM Extension</span></span>
<span data-ttu-id="83147-158">Wykonaj hello instrukcje tooconnect programu Azure PowerShell tooyour subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="83147-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="83147-159">Określ nazwę usługi hello, maszyny Wirtualnej i tryb kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="83147-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="83147-160">Podaj nazwę konta magazynu Azure hello i klucza toowhich zebrane pliki zostaną przekazane.</span><span class="sxs-lookup"><span data-stu-id="83147-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="83147-161">Wywołania hello SetAzureVMLogCollector.ps1 (dołączony na końcu artykułu hello hello) jako sposób tooenable hello AzureLogCollector rozszerzenia dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="83147-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="83147-162">Po zakończeniu wykonywania hello można znaleźć pliku hello przekazany w https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span><span class="sxs-lookup"><span data-stu-id="83147-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="83147-163">Witaj poniżej znajduje się definicja hello hello parametry przekazywane toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="83147-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="83147-164">(To jest kopiowana poniżej również.)</span><span class="sxs-lookup"><span data-stu-id="83147-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="83147-165">ServiceName: Twoje nazwa usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="83147-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="83147-166">Nazwa hello VMName hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="83147-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="83147-167">Tryb: Tryb kolekcji.</span><span class="sxs-lookup"><span data-stu-id="83147-167">Mode: Collection mode.</span></span> <span data-ttu-id="83147-168">"Pełnej" lub "GA".</span><span class="sxs-lookup"><span data-stu-id="83147-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="83147-169">StorageAccountName: Nazwa konta magazynu Azure do przechowywania zebranych danych.</span><span class="sxs-lookup"><span data-stu-id="83147-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="83147-170">StorageAccountKey: Nazwa klucz konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="83147-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="83147-171">AdditionalDataLocationList: Lista hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="83147-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="83147-172">Rozszerzenie plików skryptów środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="83147-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="83147-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="83147-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="83147-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="83147-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="83147-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83147-175">Next Steps</span></span>
<span data-ttu-id="83147-176">Teraz możesz zbadać lub skopiuj dzienniki z jednej lokalizacji bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="83147-176">Now you can examine or copy your logs from one very simple location.</span></span>

