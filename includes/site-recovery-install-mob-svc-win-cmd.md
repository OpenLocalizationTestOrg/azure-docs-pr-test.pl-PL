1. <span data-ttu-id="36a87-101">Skopiuj Instalatora na folder lokalny (na przykład C:\Temp) na serwerze, który chcesz chronić.</span><span class="sxs-lookup"><span data-stu-id="36a87-101">Copy the installer to a local folder (for example, C:\Temp) on the server that you want to protect.</span></span> <span data-ttu-id="36a87-102">Uruchom następujące polecenia z uprawnieniami administracyjnymi w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="36a87-102">Run the following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="36a87-103">Aby zainstalować usługi mobilności, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="36a87-103">To install Mobility Service, run the following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="36a87-104">Teraz agent musi być zarejestrowany na serwerze konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="36a87-104">Now the agent needs to be registered with the Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="36a87-105">Argumenty wiersza polecenia Instalatora usługi mobilności</span><span class="sxs-lookup"><span data-stu-id="36a87-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="36a87-106">Parametr</span><span class="sxs-lookup"><span data-stu-id="36a87-106">Parameter</span></span>|<span data-ttu-id="36a87-107">Typ</span><span class="sxs-lookup"><span data-stu-id="36a87-107">Type</span></span>|<span data-ttu-id="36a87-108">Opis</span><span class="sxs-lookup"><span data-stu-id="36a87-108">Description</span></span>|<span data-ttu-id="36a87-109">Możliwe wartości</span><span class="sxs-lookup"><span data-stu-id="36a87-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="36a87-110">/ Roli</span><span class="sxs-lookup"><span data-stu-id="36a87-110">/Role</span></span>|<span data-ttu-id="36a87-111">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="36a87-111">Mandatory</span></span>|<span data-ttu-id="36a87-112">Określa, czy należy zainstalować usługi mobilności (MS) lub MasterTarget(MT) powinna zostać zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="36a87-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="36a87-113">MS</span><span class="sxs-lookup"><span data-stu-id="36a87-113">MS</span></span> </br> <span data-ttu-id="36a87-114">MT</span><span class="sxs-lookup"><span data-stu-id="36a87-114">MT</span></span>|
|<span data-ttu-id="36a87-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="36a87-115">/InstallLocation</span></span>|<span data-ttu-id="36a87-116">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="36a87-116">Optional</span></span>|<span data-ttu-id="36a87-117">Lokalizacja, w którym jest zainstalowana usługa mobilności</span><span class="sxs-lookup"><span data-stu-id="36a87-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="36a87-118">Dowolny folder na komputerze</span><span class="sxs-lookup"><span data-stu-id="36a87-118">Any folder on the computer</span></span>|
|<span data-ttu-id="36a87-119">/ Platform</span><span class="sxs-lookup"><span data-stu-id="36a87-119">/Platform</span></span>|<span data-ttu-id="36a87-120">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="36a87-120">Mandatory</span></span>|<span data-ttu-id="36a87-121">Określa platformę, na którym zainstalowano pobierania usługi mobilności</span><span class="sxs-lookup"><span data-stu-id="36a87-121">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="36a87-122">- **VMware** : Użyj tej wartości, jeśli instalujesz usługi mobilności na maszynie Wirtualnej uruchomionych na *VMware vSphere hostach ESXi*, *hosty funkcji Hyper-V* i *Phsyical serwerów*</span><span class="sxs-lookup"><span data-stu-id="36a87-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="36a87-123">- **Azure** : Użyj tej wartości, jeśli instalujesz agenta na maszynie Wirtualnej Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="36a87-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="36a87-124">VMware</span><span class="sxs-lookup"><span data-stu-id="36a87-124">VMware</span></span> </br> <span data-ttu-id="36a87-125">Azure</span><span class="sxs-lookup"><span data-stu-id="36a87-125">Azure</span></span>|
|<span data-ttu-id="36a87-126">/ Dyskretnej</span><span class="sxs-lookup"><span data-stu-id="36a87-126">/Silent</span></span>|<span data-ttu-id="36a87-127">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="36a87-127">Optional</span></span>|<span data-ttu-id="36a87-128">Określa, aby uruchomić Instalatora w trybie dyskretnym</span><span class="sxs-lookup"><span data-stu-id="36a87-128">Specifies to run the installer in silent mode</span></span>| <span data-ttu-id="36a87-129">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="36a87-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="36a87-130">Dzienniki instalacji można znaleźć w %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="36a87-130">The setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="36a87-131">Argumenty wiersza polecenia rejestracji usługi mobilności</span><span class="sxs-lookup"><span data-stu-id="36a87-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="36a87-132">Parametr</span><span class="sxs-lookup"><span data-stu-id="36a87-132">Parameter</span></span>|<span data-ttu-id="36a87-133">Typ</span><span class="sxs-lookup"><span data-stu-id="36a87-133">Type</span></span>|<span data-ttu-id="36a87-134">Opis</span><span class="sxs-lookup"><span data-stu-id="36a87-134">Description</span></span>|<span data-ttu-id="36a87-135">Możliwe wartości</span><span class="sxs-lookup"><span data-stu-id="36a87-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="36a87-136">/ CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="36a87-136">/CSEndPoint</span></span> |<span data-ttu-id="36a87-137">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="36a87-137">Mandatory</span></span>|<span data-ttu-id="36a87-138">Adres IP serwera konfiguracji</span><span class="sxs-lookup"><span data-stu-id="36a87-138">IP address of the configuration server</span></span>| <span data-ttu-id="36a87-139">Dowolny prawidłowy adres IP</span><span class="sxs-lookup"><span data-stu-id="36a87-139">Any valid IP address</span></span>|
  |<span data-ttu-id="36a87-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="36a87-140">/PassphraseFilePath</span></span>|<span data-ttu-id="36a87-141">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="36a87-141">Mandatory</span></span>|<span data-ttu-id="36a87-142">Lokalizacja hasło</span><span class="sxs-lookup"><span data-stu-id="36a87-142">Location of the passphrase</span></span> |<span data-ttu-id="36a87-143">Wszelkie prawidłową ścieżką UNC lub ścieżkę do pliku lokalnego</span><span class="sxs-lookup"><span data-stu-id="36a87-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="36a87-144">Dzienniki AgentConfiguration znajduje się w obszarze %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="36a87-144">The AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
