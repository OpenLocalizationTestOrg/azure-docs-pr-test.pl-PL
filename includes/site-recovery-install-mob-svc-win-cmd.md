1. <span data-ttu-id="3c65c-101">Skopiuj hello Instalator tooa folder lokalny (na przykład C:\Temp) na powitania serwera, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="3c65c-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="3c65c-102">Uruchom następujące polecenia z uprawnieniami administracyjnymi w wierszu polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3c65c-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="3c65c-103">tooinstall usługi mobilności, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="3c65c-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="3c65c-104">Hello agent musi teraz toobe zarejestrowane na powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3c65c-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="3c65c-105">Argumenty wiersza polecenia Instalatora usługi mobilności</span><span class="sxs-lookup"><span data-stu-id="3c65c-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="3c65c-106">Parametr</span><span class="sxs-lookup"><span data-stu-id="3c65c-106">Parameter</span></span>|<span data-ttu-id="3c65c-107">Typ</span><span class="sxs-lookup"><span data-stu-id="3c65c-107">Type</span></span>|<span data-ttu-id="3c65c-108">Opis</span><span class="sxs-lookup"><span data-stu-id="3c65c-108">Description</span></span>|<span data-ttu-id="3c65c-109">Możliwe wartości</span><span class="sxs-lookup"><span data-stu-id="3c65c-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="3c65c-110">/ Roli</span><span class="sxs-lookup"><span data-stu-id="3c65c-110">/Role</span></span>|<span data-ttu-id="3c65c-111">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="3c65c-111">Mandatory</span></span>|<span data-ttu-id="3c65c-112">Określa, czy należy zainstalować usługi mobilności (MS) lub MasterTarget(MT) powinna zostać zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="3c65c-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="3c65c-113">MS</span><span class="sxs-lookup"><span data-stu-id="3c65c-113">MS</span></span> </br> <span data-ttu-id="3c65c-114">MT</span><span class="sxs-lookup"><span data-stu-id="3c65c-114">MT</span></span>|
|<span data-ttu-id="3c65c-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="3c65c-115">/InstallLocation</span></span>|<span data-ttu-id="3c65c-116">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="3c65c-116">Optional</span></span>|<span data-ttu-id="3c65c-117">Lokalizacja, w którym jest zainstalowana usługa mobilności</span><span class="sxs-lookup"><span data-stu-id="3c65c-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="3c65c-118">Dowolnego folderu na komputerze hello</span><span class="sxs-lookup"><span data-stu-id="3c65c-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="3c65c-119">/ Platform</span><span class="sxs-lookup"><span data-stu-id="3c65c-119">/Platform</span></span>|<span data-ttu-id="3c65c-120">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="3c65c-120">Mandatory</span></span>|<span data-ttu-id="3c65c-121">Określa platformę hello, na które hello usługa mobilności jest wprowadzenie zainstalowana</span><span class="sxs-lookup"><span data-stu-id="3c65c-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="3c65c-122">- **VMware** : Użyj tej wartości, jeśli instalujesz usługi mobilności na maszynie Wirtualnej uruchomionych na *VMware vSphere hostach ESXi*, *hosty funkcji Hyper-V* i *Phsyical serwerów*</span><span class="sxs-lookup"><span data-stu-id="3c65c-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="3c65c-123">- **Azure** : Użyj tej wartości, jeśli instalujesz agenta na maszynie Wirtualnej Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="3c65c-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="3c65c-124">VMware</span><span class="sxs-lookup"><span data-stu-id="3c65c-124">VMware</span></span> </br> <span data-ttu-id="3c65c-125">Azure</span><span class="sxs-lookup"><span data-stu-id="3c65c-125">Azure</span></span>|
|<span data-ttu-id="3c65c-126">/ Dyskretnej</span><span class="sxs-lookup"><span data-stu-id="3c65c-126">/Silent</span></span>|<span data-ttu-id="3c65c-127">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="3c65c-127">Optional</span></span>|<span data-ttu-id="3c65c-128">Określa toorun hello Instalatora w trybie dyskretnym</span><span class="sxs-lookup"><span data-stu-id="3c65c-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="3c65c-129">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="3c65c-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="3c65c-130">dzienniki instalacji Hello znajduje się w obszarze %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="3c65c-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="3c65c-131">Argumenty wiersza polecenia rejestracji usługi mobilności</span><span class="sxs-lookup"><span data-stu-id="3c65c-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="3c65c-132">Parametr</span><span class="sxs-lookup"><span data-stu-id="3c65c-132">Parameter</span></span>|<span data-ttu-id="3c65c-133">Typ</span><span class="sxs-lookup"><span data-stu-id="3c65c-133">Type</span></span>|<span data-ttu-id="3c65c-134">Opis</span><span class="sxs-lookup"><span data-stu-id="3c65c-134">Description</span></span>|<span data-ttu-id="3c65c-135">Możliwe wartości</span><span class="sxs-lookup"><span data-stu-id="3c65c-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="3c65c-136">/ CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="3c65c-136">/CSEndPoint</span></span> |<span data-ttu-id="3c65c-137">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="3c65c-137">Mandatory</span></span>|<span data-ttu-id="3c65c-138">Adres IP serwera konfiguracji hello</span><span class="sxs-lookup"><span data-stu-id="3c65c-138">IP address of hello configuration server</span></span>| <span data-ttu-id="3c65c-139">Dowolny prawidłowy adres IP</span><span class="sxs-lookup"><span data-stu-id="3c65c-139">Any valid IP address</span></span>|
  |<span data-ttu-id="3c65c-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="3c65c-140">/PassphraseFilePath</span></span>|<span data-ttu-id="3c65c-141">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="3c65c-141">Mandatory</span></span>|<span data-ttu-id="3c65c-142">Lokalizacja hello hasło</span><span class="sxs-lookup"><span data-stu-id="3c65c-142">Location of hello passphrase</span></span> |<span data-ttu-id="3c65c-143">Wszelkie prawidłową ścieżką UNC lub ścieżkę do pliku lokalnego</span><span class="sxs-lookup"><span data-stu-id="3c65c-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="3c65c-144">Hello AgentConfiguration Dzienniki znajdują się w obszarze %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="3c65c-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
