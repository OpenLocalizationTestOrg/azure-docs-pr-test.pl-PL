
* [<span data-ttu-id="2c81f-101">Szybkie tworzenie maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="2c81f-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="2c81f-102">Wdrażanie maszyny wirtualnej na platformie Azure na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="2c81f-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="2c81f-103">Tworzenie maszyny wirtualnej za pomocą obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="2c81f-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="2c81f-104">Wdrażanie maszyny wirtualnej korzystającej z sieci wirtualnej i modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="2c81f-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="2c81f-105">Usuwanie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="2c81f-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="2c81f-106">Pokaż dziennik hello wdrożenia grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="2c81f-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="2c81f-107">Wyświetlanie informacji o maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c81f-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="2c81f-108">Łączenie maszyny wirtualnej opartych na systemie Linux tooa</span><span class="sxs-lookup"><span data-stu-id="2c81f-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="2c81f-109">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c81f-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="2c81f-110">Uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c81f-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="2c81f-111">Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="2c81f-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="2c81f-112">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="2c81f-112">Getting ready</span></span>
<span data-ttu-id="2c81f-113">Zanim użyjesz hello wiersza polecenia platformy Azure z grup zasobów platformy Azure, należy toohave hello właściwej wersji interfejsu wiersza polecenia Azure oraz konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c81f-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="2c81f-114">Jeśli nie masz hello Azure CLI [go zainstalować](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2c81f-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="2c81f-115">Aktualizacja z wiersza polecenia platformy Azure w wersji too0.9.0 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="2c81f-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="2c81f-116">Typ `azure --version` toosee, czy masz już zainstalowany w wersji 0.9.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="2c81f-117">Jeśli używana wersja nie jest 0.9.0 lub później, należy tooupdate hello go za pomocą jednej z natywnego instalatorów lub za pomocą **npm** , wpisując `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="2c81f-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="2c81f-118">Można również uruchomić wiersza polecenia platformy Azure jako kontener Docker, za pomocą następujących hello [obrazu Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="2c81f-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="2c81f-119">Z hosta Docker i uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2c81f-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="2c81f-120">Ustawianie konta i subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2c81f-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="2c81f-121">Jeśli nie masz jeszcze subskrypcji platformy Azure, ale masz subskrypcję MSDN, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="2c81f-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="2c81f-122">lub zarejestrować się w celu skorzystania z [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2c81f-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="2c81f-123">Teraz [interakcyjnego logowania tooyour konta Azure](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) , wpisując `azure login` i wykonując hello monity o tooyour środowisko logowania interakcyjnego konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c81f-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="2c81f-124">Jeśli masz służbowego lub szkolnego identyfikator i wiesz, nie ma włączone uwierzytelnianie dwuskładnikowe, możesz **również** użyj `azure login -u` wraz z hello służbowe toolog identyfikator w *bez* sesji interaktywnej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="2c81f-125">Jeśli nie ma służbowego lub szkolnego identyfikator, możesz [Utwórz identyfikator firmy lub szkoły z osobistego konta Microsoft](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog w hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="2c81f-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="2c81f-126">Twoje konto może mieć więcej niż jedną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="2c81f-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="2c81f-127">Możesz wpisać polecenie `azure account list`, aby wyświetlić listę swoich subskrypcji, która może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="2c81f-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="2c81f-128">Można ustawić hello bieżącej subskrypcji Azure, wpisując następujące hello.</span><span class="sxs-lookup"><span data-stu-id="2c81f-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="2c81f-129">Użyj hello nazwy lub hello identyfikator subskrypcji zawierającego zasoby hello ma toomanage.</span><span class="sxs-lookup"><span data-stu-id="2c81f-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="2c81f-130">Przełącz tryb grupy zasobów Azure CLI toohello</span><span class="sxs-lookup"><span data-stu-id="2c81f-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="2c81f-131">Domyślnie program hello Azure CLI jest uruchamiany w trybie zarządzania usługi hello (**asm** tryb).</span><span class="sxs-lookup"><span data-stu-id="2c81f-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="2c81f-132">Wpisz powitania po tooswitch tooresource grupy tryb.</span><span class="sxs-lookup"><span data-stu-id="2c81f-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="2c81f-133">Opis szablonów zasobów i grup zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2c81f-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="2c81f-134">Większość aplikacji jest tworzona z połączenia różnych typów zasobów (na przykład jednej lub kilku maszyn wirtualnych i kont magazynu, bazy danych SQL, sieci wirtualnej lub sieci dostarczania zawartości).</span><span class="sxs-lookup"><span data-stu-id="2c81f-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="2c81f-135">Witaj interfejsu API zarządzania usługami Azure domyślne i hello klasycznego portalu Azure reprezentowana tych elementów przy użyciu podejścia przez usługi.</span><span class="sxs-lookup"><span data-stu-id="2c81f-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="2c81f-136">To rozwiązanie wymaga toodeploy i indywidualnie zarządzania hello poszczególnych usług (lub znaleźć innych narzędzi, które to zrobić), a nie jako pojedyncza jednostka logiczna wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2c81f-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="2c81f-137">*Szablony usługi Azure Resource Manager*, jednak umożliwiają możesz toodeploy zasobów i zarządzanie nimi tych różnych jako jedną jednostkę logiczną wdrożenia w sposób deklaratywnego.</span><span class="sxs-lookup"><span data-stu-id="2c81f-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="2c81f-138">Zamiast imperatively informuje Azure jakie toodeploy jednego polecenia po kolei, opisu całego wdrożenia w pliku JSON, — wszystkie zasoby hello i skojarzone konfiguracji i parametrów wdrożenia — i poinformuj Azure toodeploy tych zasobów jako jeden Grupa.</span><span class="sxs-lookup"><span data-stu-id="2c81f-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="2c81f-139">Następnie można zarządzać hello ogólną cyklu życia hello grupy zasobów za pomocą interfejsu wiersza polecenia Azure zasobów zarządzania poleceń do:</span><span class="sxs-lookup"><span data-stu-id="2c81f-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="2c81f-140">Zatrzymać, uruchomić lub usunąć wszystkie zasoby hello w obrębie grupy hello naraz.</span><span class="sxs-lookup"><span data-stu-id="2c81f-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="2c81f-141">Zastosuj toolock zasady kontroli dostępu opartej na rolach (RBAC) uprawnień zabezpieczeń w dół na nich.</span><span class="sxs-lookup"><span data-stu-id="2c81f-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="2c81f-142">przeprowadzać inspekcje operacji;</span><span class="sxs-lookup"><span data-stu-id="2c81f-142">Audit operations.</span></span>
* <span data-ttu-id="2c81f-143">oznaczać zasoby za pomocą dodatkowych metadanych w celu ułatwienia śledzenia.</span><span class="sxs-lookup"><span data-stu-id="2c81f-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="2c81f-144">Dowiedz się więcej na temat grup zasobów platformy Azure i sposób ich działania dla Ciebie w hello partii [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c81f-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="2c81f-145">Jeśli interesuje Cię tworzenie szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2c81f-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="2c81f-146"><a id="quick-create-a-vm-in-azure"></a>Zadanie: Szybkie tworzenie maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="2c81f-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="2c81f-147">Czasami wiesz, jakie obrazu należy i maszyny Wirtualnej z obrazu należy od razu i nie zależy Ci zbyt dużo o infrastruktury hello — może być po zdefiniowaniu tootest czystą maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="2c81f-148">Gdy to ma toouse hello `azure vm quick-create` polecenia i przekaż toocreate niezbędne argumenty hello maszyny Wirtualnej i jej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="2c81f-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="2c81f-149">Najpierw utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="2c81f-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="2c81f-150">Następnie potrzebny będzie obraz.</span><span class="sxs-lookup"><span data-stu-id="2c81f-150">Second, you'll need an image.</span></span> <span data-ttu-id="2c81f-151">toofind jako obraz z hello wiersza polecenia platformy Azure, zobacz [Navigating i wybieranie obrazów maszyny wirtualnej platformy Azure za pomocą programu PowerShell i hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c81f-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2c81f-152">Na potrzeby tego artykułu uwzględniono krótką listę popularnych obrazów.</span><span class="sxs-lookup"><span data-stu-id="2c81f-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="2c81f-153">W przypadku tego szybkiego tworzenia używany będzie obraz stabilny systemu CoreOS.</span><span class="sxs-lookup"><span data-stu-id="2c81f-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="2c81f-154">Dla ComputeImageVersion możesz także po prostu podać "najnowsze" jako parametru w obu język szablonu hello i hello Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="2c81f-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="2c81f-155">Pozwoli to wykonywanych tooalways hello najnowsze i poprawioną wersja obrazu hello bez konieczności toomodify skryptu lub szablonów.</span><span class="sxs-lookup"><span data-stu-id="2c81f-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="2c81f-156">Jest to pokazane poniżej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="2c81f-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="2c81f-157">PublisherName</span></span> | <span data-ttu-id="2c81f-158">Oferta</span><span class="sxs-lookup"><span data-stu-id="2c81f-158">Offer</span></span> | <span data-ttu-id="2c81f-159">SKU</span><span class="sxs-lookup"><span data-stu-id="2c81f-159">Sku</span></span> | <span data-ttu-id="2c81f-160">Wersja</span><span class="sxs-lookup"><span data-stu-id="2c81f-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2c81f-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="2c81f-161">OpenLogic</span></span> |<span data-ttu-id="2c81f-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="2c81f-162">CentOS</span></span> |<span data-ttu-id="2c81f-163">7</span><span class="sxs-lookup"><span data-stu-id="2c81f-163">7</span></span> |<span data-ttu-id="2c81f-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="2c81f-164">7.0.201503</span></span> |
| <span data-ttu-id="2c81f-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="2c81f-165">OpenLogic</span></span> |<span data-ttu-id="2c81f-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="2c81f-166">CentOS</span></span> |<span data-ttu-id="2c81f-167">7.1</span><span class="sxs-lookup"><span data-stu-id="2c81f-167">7.1</span></span> |<span data-ttu-id="2c81f-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="2c81f-168">7.1.201504</span></span> |
| <span data-ttu-id="2c81f-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2c81f-169">CoreOS</span></span> |<span data-ttu-id="2c81f-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2c81f-170">CoreOS</span></span> |<span data-ttu-id="2c81f-171">Beta</span><span class="sxs-lookup"><span data-stu-id="2c81f-171">Beta</span></span> |<span data-ttu-id="2c81f-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="2c81f-172">647.0.0</span></span> |
| <span data-ttu-id="2c81f-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2c81f-173">CoreOS</span></span> |<span data-ttu-id="2c81f-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2c81f-174">CoreOS</span></span> |<span data-ttu-id="2c81f-175">Stable</span><span class="sxs-lookup"><span data-stu-id="2c81f-175">Stable</span></span> |<span data-ttu-id="2c81f-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="2c81f-176">633.1.0</span></span> |
| <span data-ttu-id="2c81f-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="2c81f-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="2c81f-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="2c81f-178">DynamicsNAV</span></span> |<span data-ttu-id="2c81f-179">2015</span><span class="sxs-lookup"><span data-stu-id="2c81f-179">2015</span></span> |<span data-ttu-id="2c81f-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="2c81f-180">8.0.40459</span></span> |
| <span data-ttu-id="2c81f-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="2c81f-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="2c81f-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="2c81f-183">2013</span><span class="sxs-lookup"><span data-stu-id="2c81f-183">2013</span></span> |<span data-ttu-id="2c81f-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="2c81f-184">1.0.0</span></span> |
| <span data-ttu-id="2c81f-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="2c81f-185">msopentech</span></span> |<span data-ttu-id="2c81f-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="2c81f-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="2c81f-187">Standardowa (Standard)</span><span class="sxs-lookup"><span data-stu-id="2c81f-187">Standard</span></span> |<span data-ttu-id="2c81f-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="2c81f-188">1.0.0</span></span> |
| <span data-ttu-id="2c81f-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="2c81f-189">msopentech</span></span> |<span data-ttu-id="2c81f-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="2c81f-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="2c81f-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="2c81f-191">Enterprise</span></span> |<span data-ttu-id="2c81f-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="2c81f-192">1.0.0</span></span> |
| <span data-ttu-id="2c81f-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="2c81f-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="2c81f-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="2c81f-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="2c81f-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="2c81f-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="2c81f-196">12.0.2430</span></span> |
| <span data-ttu-id="2c81f-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="2c81f-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="2c81f-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="2c81f-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="2c81f-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="2c81f-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="2c81f-200">12.0.2430</span></span> |
| <span data-ttu-id="2c81f-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="2c81f-201">Canonical</span></span> |<span data-ttu-id="2c81f-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-202">UbuntuServer</span></span> |<span data-ttu-id="2c81f-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="2c81f-203">12.04.5-LTS</span></span> |<span data-ttu-id="2c81f-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="2c81f-204">12.04.201504230</span></span> |
| <span data-ttu-id="2c81f-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="2c81f-205">Canonical</span></span> |<span data-ttu-id="2c81f-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-206">UbuntuServer</span></span> |<span data-ttu-id="2c81f-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="2c81f-207">14.04.2-LTS</span></span> |<span data-ttu-id="2c81f-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="2c81f-208">14.04.201503090</span></span> |
| <span data-ttu-id="2c81f-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="2c81f-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-210">WindowsServer</span></span> |<span data-ttu-id="2c81f-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="2c81f-211">2012-Datacenter</span></span> |<span data-ttu-id="2c81f-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="2c81f-212">3.0.201503</span></span> |
| <span data-ttu-id="2c81f-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="2c81f-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-214">WindowsServer</span></span> |<span data-ttu-id="2c81f-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="2c81f-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="2c81f-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="2c81f-216">4.0.201503</span></span> |
| <span data-ttu-id="2c81f-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="2c81f-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="2c81f-218">WindowsServer</span></span> |<span data-ttu-id="2c81f-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="2c81f-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="2c81f-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="2c81f-220">5.0.201504</span></span> |
| <span data-ttu-id="2c81f-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="2c81f-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="2c81f-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="2c81f-222">WindowsServerEssentials</span></span> |<span data-ttu-id="2c81f-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="2c81f-223">WindowsServerEssentials</span></span> |<span data-ttu-id="2c81f-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="2c81f-224">1.0.141204</span></span> |
| <span data-ttu-id="2c81f-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="2c81f-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="2c81f-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="2c81f-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="2c81f-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="2c81f-227">2012R2</span></span> |<span data-ttu-id="2c81f-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="2c81f-228">4.3.4665</span></span> |

<span data-ttu-id="2c81f-229">Po prostu utworzyć maszyny Wirtualnej, wprowadzając hello `azure vm quick-create` polecenia i gotowe do hello monitów.</span><span class="sxs-lookup"><span data-stu-id="2c81f-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="2c81f-230">Powinno to wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="2c81f-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="2c81f-231">I możesz iść dalej z nową maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="2c81f-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="2c81f-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Zadanie: Wdrażanie maszyny wirtualnej na platformie Azure na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="2c81f-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="2c81f-233">Użyj instrukcji hello w tych sekcjach toodeploy nowej maszyny Wirtualnej platformy Azure przy użyciu szablonu z hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c81f-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="2c81f-234">Ten szablon tworzy jednej maszyny wirtualnej w nowej sieci wirtualnej z pojedynczą podsiecią w przeciwieństwie do `azure vm quick-create`, umożliwia toodescribe należy dokładnie mają i powtarzaj go bez błędów.</span><span class="sxs-lookup"><span data-stu-id="2c81f-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="2c81f-235">Oto, co ten szablon tworzy:</span><span class="sxs-lookup"><span data-stu-id="2c81f-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="2c81f-236">Krok 1: Sprawdź plik JSON hello hello parametrów szablonu</span><span class="sxs-lookup"><span data-stu-id="2c81f-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="2c81f-237">Poniżej przedstawiono hello zawartość pliku JSON hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="2c81f-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="2c81f-238">(szablon hello znajduje się również w [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="2c81f-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="2c81f-239">Szablony są elastyczne i co projektanta hello może wybrany toogive wiele parametrów albo wybrany toooffer tylko kilka, tworząc szablon, który jest bardziej stała.</span><span class="sxs-lookup"><span data-stu-id="2c81f-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="2c81f-240">Wymagany jest szablon hello toopass jako parametry informacje hello toocollect kolejności, otwórz plik szablonu hello (w tym temacie ma wbudowany szablonu, poniżej) i sprawdź, czy hello **parametry** wartości.</span><span class="sxs-lookup"><span data-stu-id="2c81f-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="2c81f-241">W takim przypadku poniższy szablon hello poprosi o:</span><span class="sxs-lookup"><span data-stu-id="2c81f-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="2c81f-242">Unikalna nazwa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="2c81f-242">A unique storage account name.</span></span>
* <span data-ttu-id="2c81f-243">Nazwa użytkownika administratora dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="2c81f-244">Hasło.</span><span class="sxs-lookup"><span data-stu-id="2c81f-244">A password.</span></span>
* <span data-ttu-id="2c81f-245">Nazwa domeny hello poza world toouse.</span><span class="sxs-lookup"><span data-stu-id="2c81f-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="2c81f-246">Numer wersji systemu Ubuntu Server (ale będzie akceptować tylko jeden z listy).</span><span class="sxs-lookup"><span data-stu-id="2c81f-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="2c81f-247">Więcej informacji na temat [wymagań dotyczących nazwy użytkownika i hasła](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="2c81f-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="2c81f-248">Po podjęciu decyzji o tych wartości, wszystko gotowe toocreate grupę i wdrożenia tego szablonu do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c81f-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="2c81f-249">Krok 2: Tworzenie maszyny wirtualnej hello przy użyciu szablonu hello</span><span class="sxs-lookup"><span data-stu-id="2c81f-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="2c81f-250">Po utworzeniu wartości parametru gotowe, możesz utworzyć grupę zasobów do wdrożenia szablonu, a następnie wdrożyć hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="2c81f-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="2c81f-251">Grupa zasobów hello toocreate, typ `azure group create <group name> <location>` o nazwie hello grupy hello ma i hello centrum danych lokalizacji, do której ma zostać toodeploy.</span><span class="sxs-lookup"><span data-stu-id="2c81f-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="2c81f-252">To dzieje się szybko:</span><span class="sxs-lookup"><span data-stu-id="2c81f-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="2c81f-253">Teraz toocreate hello wdrożenia, wywołanie `azure group deployment create` i przekaż:</span><span class="sxs-lookup"><span data-stu-id="2c81f-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="2c81f-254">Plik szablonu Hello (jeśli został zapisany hello powyżej pliku lokalnego tooa szablonu JSON).</span><span class="sxs-lookup"><span data-stu-id="2c81f-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="2c81f-255">Szablon identyfikatora URI (jeśli ma toopoint hello plik w witrynie GitHub lub inny adres sieci web).</span><span class="sxs-lookup"><span data-stu-id="2c81f-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="2c81f-256">grupy zasobów Hello, do której ma zostać toodeploy.</span><span class="sxs-lookup"><span data-stu-id="2c81f-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="2c81f-257">Opcjonalna nazwa wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2c81f-257">An optional deployment name.</span></span>

<span data-ttu-id="2c81f-258">Będzie toosupply zostanie wyświetlony monit o hello wartości parametrów w sekcji "Parametry" hello hello pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="2c81f-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="2c81f-259">Po określeniu wszystkich wartości parametru hello rozpocznie się wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2c81f-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="2c81f-260">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="2c81f-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="2c81f-261">Zostanie wyświetlony hello następujące rodzaje informacji:</span><span class="sxs-lookup"><span data-stu-id="2c81f-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="2c81f-262"><a id="create-a-custom-vm-image"></a>Zadanie: Tworzenie niestandardowej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c81f-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="2c81f-263">W tym samouczku hello podstawowe sposoby użycia szablonów powyżej, więc teraz możemy użyć podobne toocreate instrukcje niestandardowe maszyny Wirtualnej z pliku VHD określonych na platformie Azure przy użyciu szablonu za pomocą hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c81f-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="2c81f-264">Witaj różnicą jest to, że ten szablon tworzy jednej maszyny wirtualnej na podstawie określony wirtualny dysk twardy (VHD).</span><span class="sxs-lookup"><span data-stu-id="2c81f-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="2c81f-265">Krok 1: Sprawdź plik JSON hello hello szablonu</span><span class="sxs-lookup"><span data-stu-id="2c81f-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="2c81f-266">Poniżej przedstawiono hello zawartość pliku JSON hello hello szablonu, który używa tej sekcji to przykład.</span><span class="sxs-lookup"><span data-stu-id="2c81f-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="2c81f-267">(szablon hello znajduje się również w [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="2c81f-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="2c81f-268">Ponownie konieczne będzie toofind hello wartości, które mają tooenter hello parametrów, które nie mają wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="2c81f-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="2c81f-269">Po uruchomieniu hello `azure group deployment create` polecenia hello Azure CLI wyświetli monit o tooenter możesz tych wartości.</span><span class="sxs-lookup"><span data-stu-id="2c81f-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="2c81f-270">Krok 2: Uzyskaj hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="2c81f-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="2c81f-271">Oczywiście niezbędny będzie plik VHD.</span><span class="sxs-lookup"><span data-stu-id="2c81f-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="2c81f-272">Możesz użyć dysku znajdującego się już na platformie Azure lub przekazać inny.</span><span class="sxs-lookup"><span data-stu-id="2c81f-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="2c81f-273">Dla maszyny wirtualnej z systemem Windows, temacie [tworzenie i przekazywanie wirtualnego dysku twardego z systemem Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c81f-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="2c81f-274">Dla maszyny wirtualnej opartych na systemie Linux, zobacz [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c81f-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="2c81f-275">Krok 3: Tworzenie maszyny wirtualnej hello przy użyciu szablonu hello</span><span class="sxs-lookup"><span data-stu-id="2c81f-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="2c81f-276">Teraz wszystko jest gotowe toocreate VHD hello — na podstawie nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="2c81f-277">Tworzenie toodeploy grupy, do, przy użyciu `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="2c81f-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="2c81f-278">Następnie utwórz hello wdrożenia przy użyciu hello `--template-uri` toocall opcji w szablonie hello bezpośrednio (lub użyć hello `--template-file` toouse opcja pliku zapisanych lokalnie).</span><span class="sxs-lookup"><span data-stu-id="2c81f-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="2c81f-279">Należy pamiętać, że szablonu hello się domyślnych ustawień, zostanie wyświetlony monit o tylko kilka rzeczy.</span><span class="sxs-lookup"><span data-stu-id="2c81f-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="2c81f-280">Jeśli wdrożono szablon hello w różnych miejscach, może się okazać, że niektóre kolizji nazw wystąpić z wartościami domyślnymi hello (szczególnie hello nazwa DNS utworzone).</span><span class="sxs-lookup"><span data-stu-id="2c81f-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="2c81f-281">Dane wyjściowe podobne hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2c81f-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="2c81f-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Zadanie: Wdrażanie aplikacji z wieloma maszynami wirtualnymi, korzystającej z sieci wirtualnej i modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="2c81f-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="2c81f-283">Ten szablon umożliwia toocreate dwóch maszyn wirtualnych należących do modułu równoważenia obciążenia i skonfigurować regułę równoważenia obciążenia na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="2c81f-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="2c81f-284">Ten szablon wdraża również konto magazynu, sieć wirtualną, publiczny adres IP, zestaw dostępności i interfejsy sieciowe.</span><span class="sxs-lookup"><span data-stu-id="2c81f-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="2c81f-285">Wykonaj te kroki toodeploy aplikacji wielu maszyn wirtualnych, która korzysta z sieci wirtualnej i modułu równoważenia obciążenia przy użyciu szablonu usługi Resource Manager w repozytorium hello GitHub szablonu, za pomocą poleceń programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="2c81f-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="2c81f-286">Krok 1: Sprawdź plik JSON hello hello szablonu</span><span class="sxs-lookup"><span data-stu-id="2c81f-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="2c81f-287">Poniżej przedstawiono hello zawartość pliku JSON hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="2c81f-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="2c81f-288">Jeśli chcesz, aby hello najnowszej wersji, jej ma znajduje się [w repozytorium GitHub hello szablonów](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="2c81f-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="2c81f-289">W tym temacie używa hello `--template-uri` toocall przełącznika hello szablonu, ale można również użyć hello `--template-file` przełącznika toopass lokalnej wersji.</span><span class="sxs-lookup"><span data-stu-id="2c81f-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="2c81f-290">Krok 2: Tworzenie hello wdrożenia przy użyciu szablonu hello</span><span class="sxs-lookup"><span data-stu-id="2c81f-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="2c81f-291">Utwórz grupę zasobów dla szablonu hello przy użyciu `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="2c81f-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="2c81f-292">Następnie utwórz wdrożenie w tej grupie zasobów przy użyciu `azure group deployment create` i przekazywanie hello grupy zasobów, przekazywanie Nazwa wdrożenia i udzielenie odpowiedzi na powitania monity dla parametrów w szablonie hello, która nie ma wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="2c81f-293">Teraz używać hello `azure group deployment create` polecenia i hello `--template-uri` szablon hello toodeploy opcji.</span><span class="sxs-lookup"><span data-stu-id="2c81f-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="2c81f-294">Miej przygotowane wartości parametrów do wprowadzenia po wyświetleniu monitu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="2c81f-295">Należy zauważyć, że ten szablon wdraża obraz systemu Windows Server, który jednak łatwo może zostać zastąpiony przez dowolny obraz systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="2c81f-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="2c81f-296">Chcesz toocreate klastrze Docker z wielu menedżerów swarm?</span><span class="sxs-lookup"><span data-stu-id="2c81f-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="2c81f-297">[Możesz to zrobić](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="2c81f-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="2c81f-298"><a id="remove-a-resource-group"></a>Zadanie: Usuwanie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="2c81f-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="2c81f-299">Należy pamiętać, że można wdrożyć ponownie tooa grupy zasobów, ale po zakończeniu jednego, można usunąć go za pomocą `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="2c81f-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="2c81f-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Zadanie: Pokaż dziennik hello wdrożenia grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="2c81f-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="2c81f-301">To zadanie jest typowe podczas tworzenia lub korzystania z szablonów.</span><span class="sxs-lookup"><span data-stu-id="2c81f-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="2c81f-302">Witaj wywołania toodisplay hello wdrożenia dzienniki dla grupy jest `azure group log show <groupname>`, które powoduje wyświetlenie dość nieco informacje, które ułatwia zrozumienie, dlaczego coś się stało--lub nie.</span><span class="sxs-lookup"><span data-stu-id="2c81f-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="2c81f-303">(Aby uzyskać więcej informacji na temat rozwiązywania problemów dotyczących wdrożeń oraz inne informacje o problemach, zobacz [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md) (Rozwiązywanie typowych problemów dotyczących wdrażania za pomocą usługi Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="2c81f-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="2c81f-304">tootarget określonych niepowodzeń, na przykład można na przykład takich narzędzi jak **jq** tooquery rzeczy bardziej precyzyjnie, takich jak które poszczególnych błędów należy toocorrect.</span><span class="sxs-lookup"><span data-stu-id="2c81f-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="2c81f-305">Witaj poniższym przykładzie użyto **jq** tooparse, poszukaj w dzienniku wdrożenia **lbgroup**poszukujący błędów.</span><span class="sxs-lookup"><span data-stu-id="2c81f-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="2c81f-306">Możesz szybko znaleźć przyczynę problemu, naprawić błąd i ponowić próbę.</span><span class="sxs-lookup"><span data-stu-id="2c81f-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="2c81f-307">W następujących przypadków hello, hello szablonu ma były tworzone dwie maszyny wirtualne na powitania tym samym czasie, który utworzony blokady na powitania VHD.</span><span class="sxs-lookup"><span data-stu-id="2c81f-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="2c81f-308">(Po zmodyfikowaniu szablonu hello firma Microsoft hello Zakończono pomyślnie wdrażanie szybko.)</span><span class="sxs-lookup"><span data-stu-id="2c81f-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="2c81f-309"><a id="display-information-about-a-virtual-machine"></a>Zadanie: Wyświetlanie informacji o maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c81f-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="2c81f-310">Umożliwia wyświetlenie informacji o określonych maszynach wirtualnych w grupie zasobów, przy użyciu hello `azure vm show <groupname> <vmname>` polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c81f-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="2c81f-311">Jeśli masz więcej niż jedną maszynę Wirtualną w grupie, być może konieczne toolist hello maszyn wirtualnych w grupie za pomocą `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="2c81f-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="2c81f-312">Następnie wyszukaj maszynę myVM1:</span><span class="sxs-lookup"><span data-stu-id="2c81f-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="2c81f-313">Magazyn tooprogrammatically i manipulowania hello dane wyjściowe z konsoli poleceń, może być toouse JSON podczas analizowania narzędzi takich jak  **[jq](https://github.com/stedolan/jq)**  lub  **[jsawk](https://github.com/micha/jsawk)** , lub bibliotek języka, które są odpowiednie dla hello zadania.</span><span class="sxs-lookup"><span data-stu-id="2c81f-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="2c81f-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Zadań: Zaloguj się maszyny wirtualnej opartych na systemie Linux tooa</span><span class="sxs-lookup"><span data-stu-id="2c81f-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="2c81f-315">Zazwyczaj maszyny z systemem Linux są toothrough połączenia SSH.</span><span class="sxs-lookup"><span data-stu-id="2c81f-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="2c81f-316">Aby uzyskać więcej informacji, zobacz [jak toouse SSH z systemem Linux na platformie Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c81f-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="2c81f-317"><a id="stop-a-virtual-machine"></a>Zadanie: Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c81f-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="2c81f-318">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2c81f-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="2c81f-319">Użyj tego parametru tookeep hello wirtualnego adresu IP (VIP) hello sieci wirtualnej, w razie hello ostatnia maszyna wirtualna w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="2c81f-320">Jeśli używasz hello `StayProvisioned` parametru nadal zostaną naliczone opłaty dla hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c81f-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="2c81f-321"><a id="start-a-virtual-machine"></a>Zadanie: Uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c81f-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="2c81f-322">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2c81f-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="2c81f-323"><a id="attach-a-data-disk"></a>Zadanie: Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="2c81f-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="2c81f-324">Należy również toodecide czy tooattach nowy dysk lub jeden zawierający dane.</span><span class="sxs-lookup"><span data-stu-id="2c81f-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="2c81f-325">Dla nowego dysku hello polecenie tworzy plik VHD hello i dołącza go w hello tego samego polecenia.</span><span class="sxs-lookup"><span data-stu-id="2c81f-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="2c81f-326">tooattach nowego dysku, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2c81f-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="2c81f-327">tooattach istniejący dysk danych, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2c81f-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="2c81f-328">Następnie należy toomount hello dysku, jak zwykle w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="2c81f-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c81f-329">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c81f-329">Next steps</span></span>
<span data-ttu-id="2c81f-330">Znacznie więcej przykładów dotyczących użycia interfejsu wiersza polecenia Azure za pomocą hello **arm** tryb, zobacz [hello Using Azure CLI for Mac, Linux i Windows za pomocą Menedżera zasobów Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2c81f-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="2c81f-331">Zobacz toolearn więcej informacji na temat zasobów platformy Azure i ich pojęcia [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c81f-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="2c81f-332">Aby uzyskać dodatkowe szablony, których możesz użyć, zobacz [Szablony szybkiego startu platformy Azure](https://azure.microsoft.com/documentation/templates/) i [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Platformy aplikacji korzystające z szablonów).</span><span class="sxs-lookup"><span data-stu-id="2c81f-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
