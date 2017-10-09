1. <span data-ttu-id="58ab6-101">Skopiuj hello Instalator tooa folder lokalny (na przykład /tmp) na powitania serwera, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="58ab6-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="58ab6-102">W terminalu uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="58ab6-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="58ab6-103">tooinstall usługi mobilności, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="58ab6-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="58ab6-104">Po zakończeniu instalacji hello usługi mobilności musi tooget zarejestrowanych toohello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="58ab6-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="58ab6-105">Hello uruchom następujące polecenie tooregister hello usługi mobilności z serwerem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="58ab6-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="58ab6-106">Instalator usługi mobilności wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="58ab6-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="58ab6-107">Parametr</span><span class="sxs-lookup"><span data-stu-id="58ab6-107">Parameter</span></span>|<span data-ttu-id="58ab6-108">Typ</span><span class="sxs-lookup"><span data-stu-id="58ab6-108">Type</span></span>|<span data-ttu-id="58ab6-109">Opis</span><span class="sxs-lookup"><span data-stu-id="58ab6-109">Description</span></span>|<span data-ttu-id="58ab6-110">Możliwe wartości</span><span class="sxs-lookup"><span data-stu-id="58ab6-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="58ab6-111">-r</span><span class="sxs-lookup"><span data-stu-id="58ab6-111">-r</span></span> |<span data-ttu-id="58ab6-112">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="58ab6-112">Mandatory</span></span>|<span data-ttu-id="58ab6-113">Określa, czy należy zainstalować usługi mobilności (MS) lub MasterTarget(MT) powinna zostać zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="58ab6-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="58ab6-114">MS</span><span class="sxs-lookup"><span data-stu-id="58ab6-114">MS</span></span> </br> <span data-ttu-id="58ab6-115">MT</span><span class="sxs-lookup"><span data-stu-id="58ab6-115">MT</span></span>|
|<span data-ttu-id="58ab6-116">-d</span><span class="sxs-lookup"><span data-stu-id="58ab6-116">-d</span></span> |<span data-ttu-id="58ab6-117">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="58ab6-117">Optional</span></span>|<span data-ttu-id="58ab6-118">Lokalizacja, w którym zostanie zainstalowana usługa mobilności</span><span class="sxs-lookup"><span data-stu-id="58ab6-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="58ab6-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="58ab6-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="58ab6-120">-v</span><span class="sxs-lookup"><span data-stu-id="58ab6-120">-v</span></span>|<span data-ttu-id="58ab6-121">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="58ab6-121">Mandatory</span></span>|<span data-ttu-id="58ab6-122">Określa platformę hello, na które hello usługa mobilności jest wprowadzenie zainstalowana</span><span class="sxs-lookup"><span data-stu-id="58ab6-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="58ab6-123">- **VMware** : Użyj tej wartości, jeśli instalujesz usługi mobilności na maszynie Wirtualnej uruchomionych na *VMware vSphere hostach ESXi*, *hosty funkcji Hyper-V* i *Phsyical serwerów*</span><span class="sxs-lookup"><span data-stu-id="58ab6-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="58ab6-124">- **Azure** : Użyj tej wartości, jeśli instalujesz agenta na maszynie Wirtualnej Azure IaaS</span><span class="sxs-lookup"><span data-stu-id="58ab6-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="58ab6-125">VMware</span><span class="sxs-lookup"><span data-stu-id="58ab6-125">VMware</span></span> </br> <span data-ttu-id="58ab6-126">Azure</span><span class="sxs-lookup"><span data-stu-id="58ab6-126">Azure</span></span>|
|<span data-ttu-id="58ab6-127">-q</span><span class="sxs-lookup"><span data-stu-id="58ab6-127">-q</span></span>|<span data-ttu-id="58ab6-128">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="58ab6-128">Optional</span></span>|<span data-ttu-id="58ab6-129">Określa toorun Instalatora w trybie dyskretnym</span><span class="sxs-lookup"><span data-stu-id="58ab6-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="58ab6-130">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="58ab6-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="58ab6-131">Konfiguracja usługi mobilności wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="58ab6-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="58ab6-132">Parametr</span><span class="sxs-lookup"><span data-stu-id="58ab6-132">Parameter</span></span>|<span data-ttu-id="58ab6-133">Typ</span><span class="sxs-lookup"><span data-stu-id="58ab6-133">Type</span></span>|<span data-ttu-id="58ab6-134">Opis</span><span class="sxs-lookup"><span data-stu-id="58ab6-134">Description</span></span>|<span data-ttu-id="58ab6-135">Możliwe wartości</span><span class="sxs-lookup"><span data-stu-id="58ab6-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="58ab6-136">-i</span><span class="sxs-lookup"><span data-stu-id="58ab6-136">-i</span></span> |<span data-ttu-id="58ab6-137">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="58ab6-137">Mandatory</span></span>|<span data-ttu-id="58ab6-138">Adres IP serwera konfiguracji hello</span><span class="sxs-lookup"><span data-stu-id="58ab6-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="58ab6-139">Dowolny prawidłowy adres IP</span><span class="sxs-lookup"><span data-stu-id="58ab6-139">Any valid IP Address</span></span>|
|<span data-ttu-id="58ab6-140">-P</span><span class="sxs-lookup"><span data-stu-id="58ab6-140">-P</span></span> |<span data-ttu-id="58ab6-141">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="58ab6-141">Mandatory</span></span>|<span data-ttu-id="58ab6-142">Pełna ścieżka hello pliku której jest zapisywany hello hasło połączenia</span><span class="sxs-lookup"><span data-stu-id="58ab6-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="58ab6-143">Nieprawidłowa folderu</span><span class="sxs-lookup"><span data-stu-id="58ab6-143">Any valid folder</span></span>|
