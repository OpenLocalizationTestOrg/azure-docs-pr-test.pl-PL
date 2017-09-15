
* [<span data-ttu-id="54801-101">Szybkie tworzenie maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="54801-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="54801-102">Wdrażanie maszyny wirtualnej na platformie Azure na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="54801-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="54801-103">Tworzenie maszyny wirtualnej za pomocą obrazu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="54801-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="54801-104">Wdrażanie maszyny wirtualnej korzystającej z sieci wirtualnej i modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="54801-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="54801-105">Usuwanie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="54801-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="54801-106">Wyświetlanie dziennika dla wdrożenia grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="54801-106">Show the log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="54801-107">Wyświetlanie informacji o maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54801-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="54801-108">Łączenie z maszyną wirtualną opartą na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="54801-108">Connect to a Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="54801-109">Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54801-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="54801-110">Uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54801-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="54801-111">Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="54801-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="54801-112">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="54801-112">Getting ready</span></span>
<span data-ttu-id="54801-113">Aby używać interfejsu wiersza polecenia platformy Azure z grupami zasobów Azure, musisz mieć właściwą wersję interfejsu wiersza polecenia platformy Azure i konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54801-113">Before you can use the Azure CLI with Azure resource groups, you need to have the right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="54801-114">Jeśli nie masz interfejsu wiersza polecenia platformy Azure, [zainstaluj go](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="54801-114">If you don't have the Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-to-090-or-later"></a><span data-ttu-id="54801-115">Aktualizowanie interfejsu wiersza polecenia platformy Azure do wersji 0.9.0 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="54801-115">Update your Azure CLI version to 0.9.0 or later</span></span>
<span data-ttu-id="54801-116">Wpisz `azure --version`, aby sprawdzić, czy masz już zainstalowaną wersję 0.9.0 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="54801-116">Type `azure --version` to see whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="54801-117">Jeśli nie masz wersji 0.9.0 ani nowszej, musisz zaktualizować posiadaną wersję przy użyciu jednego z natywnych instalatorów lub za pomocą narzędzia **npm**, wpisując `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="54801-117">If your version is not 0.9.0 or later, you need to update it by using one of the native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="54801-118">Możesz także uruchomić interfejs wiersza polecenia platformy Azure przy użyciu następującego [obrazu platformy Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="54801-118">You can also run Azure CLI as a Docker container by using the following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="54801-119">Z poziomu hosta platformy Docker uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="54801-119">From a Docker host, run the following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="54801-120">Ustawianie konta i subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54801-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="54801-121">Jeśli nie masz jeszcze subskrypcji platformy Azure, ale masz subskrypcję MSDN, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="54801-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="54801-122">lub zarejestrować się w celu skorzystania z [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54801-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="54801-123">Teraz [interaktywnie zaloguj się do konta platformy Azure](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login), wpisując `azure login` i postępując zgodnie z monitami wyświetlanymi w środowisku logowania interakcyjnego do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54801-123">Now [log in to your Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following the prompts for an interactive login experience to your Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="54801-124">Jeśli masz identyfikator służbowy i wiesz, że nie włączono uwierzytelniania dwuskładnikowego, możesz **również** użyć instrukcji `azure login -u` wraz z identyfikatorem służbowym, aby zalogować się do *bez* sesji interakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="54801-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with the work or school ID to log in *without* an interactive session.</span></span> <span data-ttu-id="54801-125">Jeśli nie masz identyfikatora służbowego, możesz [utworzyć identyfikator służbowy z poziomu osobistego konta Microsoft](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), aby logować się w taki sam sposób.</span><span class="sxs-lookup"><span data-stu-id="54801-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to log in the same way.</span></span>
>
>

<span data-ttu-id="54801-126">Twoje konto może mieć więcej niż jedną subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="54801-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="54801-127">Możesz wpisać polecenie `azure account list`, aby wyświetlić listę swoich subskrypcji, która może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="54801-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

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

<span data-ttu-id="54801-128">Aby ustawić bieżącą subskrypcję platformy Azure, wpisz poniższy kod.</span><span class="sxs-lookup"><span data-stu-id="54801-128">You can set the current Azure subscription by typing the following.</span></span> <span data-ttu-id="54801-129">Użyj nazwy subskrypcji lub identyfikatora, który zawiera zasoby przeznaczone do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="54801-129">Use the subscription name or the ID that has the resources you want to manage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-to-the-azure-cli-resource-group-mode"></a><span data-ttu-id="54801-130">Przełączanie do trybu grupy zasobów interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54801-130">Switch to the Azure CLI resource group mode</span></span>
<span data-ttu-id="54801-131">Domyślnie interfejs wiersza polecenia platformy Azure jest uruchamiany w trybie zarządzania usługami (tryb **asm**).</span><span class="sxs-lookup"><span data-stu-id="54801-131">By default, the Azure CLI starts in the service management mode (**asm** mode).</span></span> <span data-ttu-id="54801-132">Wpisz poniższe polecenie, aby przełączyć do trybu grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="54801-132">Type the following to switch to resource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="54801-133">Opis szablonów zasobów i grup zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="54801-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="54801-134">Większość aplikacji jest tworzona z połączenia różnych typów zasobów (na przykład jednej lub kilku maszyn wirtualnych i kont magazynu, bazy danych SQL, sieci wirtualnej lub sieci dostarczania zawartości).</span><span class="sxs-lookup"><span data-stu-id="54801-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="54801-135">W domyślnym interfejsie API zarządzania usługami platformy Azure i klasycznej witrynie Azure Portal te elementy były przedstawiane przy użyciu podejścia „każda usługa oddzielnie”.</span><span class="sxs-lookup"><span data-stu-id="54801-135">The default Azure service management API and the Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="54801-136">Takie podejście wymaga wdrażania poszczególnych usług i zarządzania nimi (lub znalezienia narzędzia, które to robi) indywidualnie, a nie jako pojedynczą jednostką logiczną wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="54801-136">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="54801-137">*Szablony usługi Azure Resource Manager* umożliwiają jednak wdrażanie tych różnych zasobów i zarządzanie nimi jako jedną jednostką logiczną wdrożenia w sposób deklaratywny.</span><span class="sxs-lookup"><span data-stu-id="54801-137">*Azure Resource Manager templates*, however, make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="54801-138">Zamiast instruować platformę Azure odnośnie wdrażanych zasobów w kolejnych poleceniach, możesz opisać całe wdrożenie (wszystkie zasoby oraz skojarzone parametry konfiguracji i wdrożenia) w pliku JSON i poinformować platformę Azure, że te zasoby mają zostać wdrożone jako jedna grupa.</span><span class="sxs-lookup"><span data-stu-id="54801-138">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span></span>

<span data-ttu-id="54801-139">Następnie możesz zarządzać całym cyklem życia zasobów grupy przy użyciu poleceń zarządzania zasobami interfejsu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="54801-139">You can then manage the overall life cycle of the group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="54801-140">zatrzymać, uruchomić lub usunąć wszystkie zasoby w grupie jednocześnie;</span><span class="sxs-lookup"><span data-stu-id="54801-140">Stop, start, or delete all of the resources within the group at once.</span></span>
* <span data-ttu-id="54801-141">zastosować reguły kontroli dostępu opartej na rolach (RBAC) w celu zablokowania dotyczących ich uprawnień zabezpieczeń;</span><span class="sxs-lookup"><span data-stu-id="54801-141">Apply Role-Based Access Control (RBAC) rules to lock down security permissions on them.</span></span>
* <span data-ttu-id="54801-142">przeprowadzać inspekcje operacji;</span><span class="sxs-lookup"><span data-stu-id="54801-142">Audit operations.</span></span>
* <span data-ttu-id="54801-143">oznaczać zasoby za pomocą dodatkowych metadanych w celu ułatwienia śledzenia.</span><span class="sxs-lookup"><span data-stu-id="54801-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="54801-144">Znacznie więcej informacji na temat grup zasobów platformy Azure i oferowanych przez nie funkcji zawiera temat [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54801-144">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="54801-145">Jeśli interesuje Cię tworzenie szablonów, zobacz [Tworzenie szablonów usługi Azure Resource Manager](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="54801-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="54801-146"><a id="quick-create-a-vm-in-azure"></a>Zadanie: Szybkie tworzenie maszyny wirtualnej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="54801-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="54801-147">Czasami wiesz, którego obrazu potrzebujesz, i natychmiast chcesz utworzyć maszynę wirtualną z tego obrazu, niespecjalnie przejmując się infrastrukturą — być może musisz coś przetestować na czystej maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54801-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about the infrastructure -- maybe you have to test something on a clean VM.</span></span> <span data-ttu-id="54801-148">To sytuacja, w której należy użyć polecenia `azure vm quick-create` i przekazać argumenty niezbędne do utworzenia maszyny wirtualnej i jej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="54801-148">That's when you want to use the `azure vm quick-create` command, and pass the arguments necessary to create a VM and its infrastructure.</span></span>

<span data-ttu-id="54801-149">Najpierw utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="54801-149">First, create your resource group.</span></span>

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

<span data-ttu-id="54801-150">Następnie potrzebny będzie obraz.</span><span class="sxs-lookup"><span data-stu-id="54801-150">Second, you'll need an image.</span></span> <span data-ttu-id="54801-151">Aby znaleźć obraz za pomocą interfejsu wiersza polecenia platformy Azure, zobacz [Navigating and selecting Azure virtual machine images with PowerShell and the Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Przechodzenie do obrazów maszyn wirtualnych platformy Azure i wybieranie ich przy użyciu programu PowerShell i interfejsu wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="54801-151">To find an image with the Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and the Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="54801-152">Na potrzeby tego artykułu uwzględniono krótką listę popularnych obrazów.</span><span class="sxs-lookup"><span data-stu-id="54801-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="54801-153">W przypadku tego szybkiego tworzenia używany będzie obraz stabilny systemu CoreOS.</span><span class="sxs-lookup"><span data-stu-id="54801-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="54801-154">Dla opcji ComputeImageVersion można także po prostu podać wartość „latest” (najnowsze) jako parametr w języku szablonu i w interfejsie wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54801-154">For ComputeImageVersion, you can also simply supply 'latest' as the parameter in both the template language and in the Azure CLI.</span></span> <span data-ttu-id="54801-155">Pozwoli to zawsze używać najnowszej wersji obrazu z zastosowanymi wszystkimi poprawkami bez konieczności modyfikowania skryptów i szablonów.</span><span class="sxs-lookup"><span data-stu-id="54801-155">This will allow you to always use the latest and patched version of the image without having to modify your scripts or templates.</span></span> <span data-ttu-id="54801-156">Jest to pokazane poniżej.</span><span class="sxs-lookup"><span data-stu-id="54801-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="54801-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="54801-157">PublisherName</span></span> | <span data-ttu-id="54801-158">Oferta</span><span class="sxs-lookup"><span data-stu-id="54801-158">Offer</span></span> | <span data-ttu-id="54801-159">SKU</span><span class="sxs-lookup"><span data-stu-id="54801-159">Sku</span></span> | <span data-ttu-id="54801-160">Wersja</span><span class="sxs-lookup"><span data-stu-id="54801-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="54801-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="54801-161">OpenLogic</span></span> |<span data-ttu-id="54801-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="54801-162">CentOS</span></span> |<span data-ttu-id="54801-163">7</span><span class="sxs-lookup"><span data-stu-id="54801-163">7</span></span> |<span data-ttu-id="54801-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="54801-164">7.0.201503</span></span> |
| <span data-ttu-id="54801-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="54801-165">OpenLogic</span></span> |<span data-ttu-id="54801-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="54801-166">CentOS</span></span> |<span data-ttu-id="54801-167">7.1</span><span class="sxs-lookup"><span data-stu-id="54801-167">7.1</span></span> |<span data-ttu-id="54801-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="54801-168">7.1.201504</span></span> |
| <span data-ttu-id="54801-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="54801-169">CoreOS</span></span> |<span data-ttu-id="54801-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="54801-170">CoreOS</span></span> |<span data-ttu-id="54801-171">Beta</span><span class="sxs-lookup"><span data-stu-id="54801-171">Beta</span></span> |<span data-ttu-id="54801-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="54801-172">647.0.0</span></span> |
| <span data-ttu-id="54801-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="54801-173">CoreOS</span></span> |<span data-ttu-id="54801-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="54801-174">CoreOS</span></span> |<span data-ttu-id="54801-175">Stable</span><span class="sxs-lookup"><span data-stu-id="54801-175">Stable</span></span> |<span data-ttu-id="54801-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="54801-176">633.1.0</span></span> |
| <span data-ttu-id="54801-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="54801-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="54801-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="54801-178">DynamicsNAV</span></span> |<span data-ttu-id="54801-179">2015</span><span class="sxs-lookup"><span data-stu-id="54801-179">2015</span></span> |<span data-ttu-id="54801-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="54801-180">8.0.40459</span></span> |
| <span data-ttu-id="54801-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="54801-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="54801-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="54801-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="54801-183">2013</span><span class="sxs-lookup"><span data-stu-id="54801-183">2013</span></span> |<span data-ttu-id="54801-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="54801-184">1.0.0</span></span> |
| <span data-ttu-id="54801-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="54801-185">msopentech</span></span> |<span data-ttu-id="54801-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="54801-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="54801-187">Standardowa (Standard)</span><span class="sxs-lookup"><span data-stu-id="54801-187">Standard</span></span> |<span data-ttu-id="54801-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="54801-188">1.0.0</span></span> |
| <span data-ttu-id="54801-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="54801-189">msopentech</span></span> |<span data-ttu-id="54801-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="54801-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="54801-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="54801-191">Enterprise</span></span> |<span data-ttu-id="54801-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="54801-192">1.0.0</span></span> |
| <span data-ttu-id="54801-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="54801-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="54801-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="54801-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="54801-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="54801-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="54801-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="54801-196">12.0.2430</span></span> |
| <span data-ttu-id="54801-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="54801-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="54801-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="54801-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="54801-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="54801-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="54801-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="54801-200">12.0.2430</span></span> |
| <span data-ttu-id="54801-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="54801-201">Canonical</span></span> |<span data-ttu-id="54801-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="54801-202">UbuntuServer</span></span> |<span data-ttu-id="54801-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="54801-203">12.04.5-LTS</span></span> |<span data-ttu-id="54801-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="54801-204">12.04.201504230</span></span> |
| <span data-ttu-id="54801-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="54801-205">Canonical</span></span> |<span data-ttu-id="54801-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="54801-206">UbuntuServer</span></span> |<span data-ttu-id="54801-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="54801-207">14.04.2-LTS</span></span> |<span data-ttu-id="54801-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="54801-208">14.04.201503090</span></span> |
| <span data-ttu-id="54801-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54801-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54801-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54801-210">WindowsServer</span></span> |<span data-ttu-id="54801-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="54801-211">2012-Datacenter</span></span> |<span data-ttu-id="54801-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="54801-212">3.0.201503</span></span> |
| <span data-ttu-id="54801-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54801-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54801-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54801-214">WindowsServer</span></span> |<span data-ttu-id="54801-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="54801-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="54801-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="54801-216">4.0.201503</span></span> |
| <span data-ttu-id="54801-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="54801-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="54801-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="54801-218">WindowsServer</span></span> |<span data-ttu-id="54801-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="54801-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="54801-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="54801-220">5.0.201504</span></span> |
| <span data-ttu-id="54801-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="54801-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="54801-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="54801-222">WindowsServerEssentials</span></span> |<span data-ttu-id="54801-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="54801-223">WindowsServerEssentials</span></span> |<span data-ttu-id="54801-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="54801-224">1.0.141204</span></span> |
| <span data-ttu-id="54801-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="54801-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="54801-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="54801-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="54801-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="54801-227">2012R2</span></span> |<span data-ttu-id="54801-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="54801-228">4.3.4665</span></span> |

<span data-ttu-id="54801-229">Aby utworzyć maszynę wirtualną, wprowadź polecenie `azure vm quick-create` i przygotuj się na monity.</span><span class="sxs-lookup"><span data-stu-id="54801-229">Just create your VM by entering the `azure vm quick-create` command and being ready for the prompts.</span></span> <span data-ttu-id="54801-230">Powinno to wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="54801-230">It should look something like this:</span></span>

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
+ Looking up the VM "coreos"
info:    Using the VM Size "Standard_A1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in the region "westus", trying to create new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up the storage account cli9fd3fce49e9a9b3d14302
+ Looking up the NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
+ Looking up the subnet "coreo-westu-1430261891570-snet" under the virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up the VM "coreos"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
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

<span data-ttu-id="54801-231">I możesz iść dalej z nową maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="54801-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="54801-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Zadanie: Wdrażanie maszyny wirtualnej na platformie Azure na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="54801-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="54801-233">Instrukcje zawarte w tych sekcjach umożliwiają wdrożenie nowej maszyny wirtualnej platformy Azure na podstawie szablonu przy użyciu interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54801-233">Use the instructions in these sections to deploy a new Azure VM by using a template with the Azure CLI.</span></span> <span data-ttu-id="54801-234">Ten szablon umożliwia utworzenie jednej maszyny wirtualnej w nowej sieci wirtualnej z jedną podsiecią i, w odróżnieniu od `azure vm quick-create`, umożliwia dokładne opisanie tego, czego oczekujesz, i powtórzenie go bez błędów.</span><span class="sxs-lookup"><span data-stu-id="54801-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you to describe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="54801-235">Oto, co ten szablon tworzy:</span><span class="sxs-lookup"><span data-stu-id="54801-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-the-json-file-for-the-template-parameters"></a><span data-ttu-id="54801-236">Krok 1. Sprawdzanie pliku JSON dla parametrów szablonu</span><span class="sxs-lookup"><span data-stu-id="54801-236">Step 1: Examine the JSON file for the template parameters</span></span>
<span data-ttu-id="54801-237">Poniżej przedstawiono zawartość pliku JSON dla szablonu.</span><span class="sxs-lookup"><span data-stu-id="54801-237">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="54801-238">(Szablon znajduje się również w witrynie [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json)).</span><span class="sxs-lookup"><span data-stu-id="54801-238">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="54801-239">Szablony są elastyczne, dzięki czemu projektant może udostępnić w szablonie bardzo wiele parametrów lub zaoferować tylko niewielki ich zestaw, tworząc mniej elastyczny szablon.</span><span class="sxs-lookup"><span data-stu-id="54801-239">Templates are flexible, so the designer may have chosen to give you lots of parameters or chosen to offer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="54801-240">Aby zebrać informacje potrzebne do przekazania szablonu w postaci parametrów, otwórz plik szablonu (w tym temacie wymieniono wbudowany szablon, poniżej) i sprawdź wartości **parametrów**.</span><span class="sxs-lookup"><span data-stu-id="54801-240">In order to collect the information you need to pass the template as parameters, open the template file (this topic has a template inline, below) and examine the **parameters** values.</span></span>

<span data-ttu-id="54801-241">W tym przypadku poniższy szablon poprosi o następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="54801-241">In this case, the template below will ask for:</span></span>

* <span data-ttu-id="54801-242">Unikalna nazwa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="54801-242">A unique storage account name.</span></span>
* <span data-ttu-id="54801-243">Nazwa użytkownika administratora maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54801-243">An admin user name for the VM.</span></span>
* <span data-ttu-id="54801-244">Hasło.</span><span class="sxs-lookup"><span data-stu-id="54801-244">A password.</span></span>
* <span data-ttu-id="54801-245">Nazwa domeny do użycia dla świata zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="54801-245">A domain name for the outside world to use.</span></span>
* <span data-ttu-id="54801-246">Numer wersji systemu Ubuntu Server (ale będzie akceptować tylko jeden z listy).</span><span class="sxs-lookup"><span data-stu-id="54801-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="54801-247">Więcej informacji na temat [wymagań dotyczących nazwy użytkownika i hasła](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="54801-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="54801-248">Po podjęciu decyzji dotyczących tych wartości możesz utworzyć grupę i wdrożyć ten szablon w swojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54801-248">Once you decide on these values, you're ready to create a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the storage account where the virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for the virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for the virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the public IP used to access the virtual machine."
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
        "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
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

### <a name="step-2-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="54801-249">Krok 2. Tworzenie maszyny wirtualnej przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="54801-249">Step 2: Create the virtual machine by using the template</span></span>
<span data-ttu-id="54801-250">Kiedy wartości parametrów są gotowe, musisz utworzyć grupę zasobów dla wdrożenia szablonu, a następnie wdrożyć szablon.</span><span class="sxs-lookup"><span data-stu-id="54801-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy the template.</span></span>

<span data-ttu-id="54801-251">Aby utworzyć grupę zasobów, wpisz polecenie `azure group create <group name> <location>` z żądaną nazwą grupy oraz lokalizacją centrum danych, w której chcesz wykonać wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="54801-251">To create the resource group, type `azure group create <group name> <location>` with the name of the group you want and the datacenter location into which you want to deploy.</span></span> <span data-ttu-id="54801-252">To dzieje się szybko:</span><span class="sxs-lookup"><span data-stu-id="54801-252">This happens quickly:</span></span>

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

<span data-ttu-id="54801-253">Teraz aby utworzyć wdrożenie, wywołaj funkcję `azure group deployment create` i przekaż:</span><span class="sxs-lookup"><span data-stu-id="54801-253">Now to create the deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="54801-254">Plik szablonu (jeśli powyższy szablon JSON został zapisany w pliku lokalnym).</span><span class="sxs-lookup"><span data-stu-id="54801-254">The template file (if you saved the above JSON template to a local file).</span></span>
* <span data-ttu-id="54801-255">Identyfikator URI szablonu (jeśli chcesz wskazać plik z witryny GitHub lub innego adresu sieci Web).</span><span class="sxs-lookup"><span data-stu-id="54801-255">A template URI (if you want to point at the file in GitHub or some other web address).</span></span>
* <span data-ttu-id="54801-256">Grupa zasobów, w której chcesz wykonać wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="54801-256">The resource group into which you want to deploy.</span></span>
* <span data-ttu-id="54801-257">Opcjonalna nazwa wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="54801-257">An optional deployment name.</span></span>

<span data-ttu-id="54801-258">Zostanie wyświetlony monit o podanie wartości parametrów w sekcji parametrów pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="54801-258">You will be prompted to supply the values of parameters in the "parameters" section of the JSON file.</span></span> <span data-ttu-id="54801-259">Po określeniu wszystkich wartości parametrów rozpocznie się wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="54801-259">When you have specified all the parameter values, your deployment will begin.</span></span>

<span data-ttu-id="54801-260">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="54801-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="54801-261">Otrzymasz informacje następującego typu:</span><span class="sxs-lookup"><span data-stu-id="54801-261">You will receive the following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
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


## <span data-ttu-id="54801-262"><a id="create-a-custom-vm-image"></a>Zadanie: Tworzenie niestandardowej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54801-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="54801-263">Podstawowe użycia szablonów przedstawiono powyżej, a więc teraz możemy użyć podobnych instrukcji w celu utworzenia niestandardowej maszyny wirtualnej z określonego pliku VHD na platformie Azure przy użyciu szablonu za pośrednictwem interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54801-263">You've seen the basic usage of templates above, so now we can use similar instructions to create a custom VM from a specific .vhd file in Azure by using a template via the Azure CLI.</span></span> <span data-ttu-id="54801-264">Różnica tutaj polega na tym, że ten szablon tworzy jedną maszynę wirtualną z określonego wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="54801-264">The difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="54801-265">Krok 1. Sprawdzanie pliku JSON dla szablonu</span><span class="sxs-lookup"><span data-stu-id="54801-265">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="54801-266">Poniżej przedstawiono zawartość pliku JSON dla szablonu użytego jako przykład w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="54801-266">Here are the contents of the JSON file for the template that this section uses as an example.</span></span> <span data-ttu-id="54801-267">(Szablon znajduje się również w witrynie [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json)).</span><span class="sxs-lookup"><span data-stu-id="54801-267">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="54801-268">Ponownie musisz znaleźć wartości, które chcesz wprowadzić dla parametrów nieposiadających wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="54801-268">Again, you will need to find the values you want to enter for the parameters that do not have default values.</span></span> <span data-ttu-id="54801-269">Po uruchomieniu polecenia `azure group deployment create` interfejs wiersza polecenia platformy Azure wyświetli monit o wprowadzenie tych wartości.</span><span class="sxs-lookup"><span data-stu-id="54801-269">When you run the `azure group deployment create` command, the Azure CLI will prompt you to enter those values.</span></span>

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

### <a name="step-2-obtain-the-vhd"></a><span data-ttu-id="54801-270">Krok 2. Uzyskiwanie dysku VHD</span><span class="sxs-lookup"><span data-stu-id="54801-270">Step 2: Obtain the VHD</span></span>
<span data-ttu-id="54801-271">Oczywiście niezbędny będzie plik VHD.</span><span class="sxs-lookup"><span data-stu-id="54801-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="54801-272">Możesz użyć dysku znajdującego się już na platformie Azure lub przekazać inny.</span><span class="sxs-lookup"><span data-stu-id="54801-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="54801-273">W przypadku maszyny wirtualnej z systemem Windows zobacz [Tworzenie wirtualnego dysku twardego systemu Windows Server i przekazywanie go na platformę Azure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54801-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD to Azure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="54801-274">W przypadku maszyny wirtualnej z systemem Linux zobacz [Tworzenie i przekazywanie wirtualnego dysku twardego zawierającego system operacyjny Linux](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54801-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains the Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="54801-275">Krok 3: Tworzenie maszyny wirtualnej przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="54801-275">Step 3: Create the virtual machine by using the template</span></span>
<span data-ttu-id="54801-276">Teraz możesz przystąpić do tworzenia nowej maszyny wirtualnej na podstawie pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="54801-276">Now you're ready to create a new virtual machine based on the .vhd.</span></span> <span data-ttu-id="54801-277">Utwórz grupę, w której ma zostać wykonane wdrożenie, używając polecenia `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="54801-277">Create a group to deploy into, by using `azure group create <location>`:</span></span>

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

<span data-ttu-id="54801-278">Następnie utwórz wdrożenie za pomocą opcji `--template-uri`, aby wywołać bezpośrednio w szablonie (ewentualnie możesz użyć opcji `--template-file`, aby użyć pliku zapisanego lokalnie).</span><span class="sxs-lookup"><span data-stu-id="54801-278">Then create the deployment by using the `--template-uri` option to call in the template directly (or you can use the `--template-file` option to use a file that you have saved locally).</span></span> <span data-ttu-id="54801-279">Należy zauważyć, że ponieważ szablon ma określone wartości domyślne, użytkownik jest monitowany tylko o kilka elementów.</span><span class="sxs-lookup"><span data-stu-id="54801-279">Note that because the template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="54801-280">W przypadku wdrożenia szablonu w różnych miejscach może się okazać, że występują pewne konflikty nazewnictwa z wartościami domyślnymi (zwłaszcza z tworzoną nazwą DNS).</span><span class="sxs-lookup"><span data-stu-id="54801-280">If you deploy the template in different places, you may find that some naming collisions occur with the default values (particularly the DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="54801-281">Dane wyjściowe wyglądają podobnie do poniższych:</span><span class="sxs-lookup"><span data-stu-id="54801-281">Output looks something like the following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
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

## <span data-ttu-id="54801-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Zadanie: Wdrażanie aplikacji z wieloma maszynami wirtualnymi, korzystającej z sieci wirtualnej i modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="54801-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="54801-283">Ten szablon umożliwia utworzenie dwóch maszyn wirtualnych w ramach modułu równoważenia obciążenia i skonfigurowanie reguły równoważenia obciążenia na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="54801-283">This template allows you to create two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="54801-284">Ten szablon wdraża również konto magazynu, sieć wirtualną, publiczny adres IP, zestaw dostępności i interfejsy sieciowe.</span><span class="sxs-lookup"><span data-stu-id="54801-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="54801-285">Wykonaj poniższe kroki, aby wdrożyć aplikację z wieloma maszynami wirtualnymi, która korzysta z sieci wirtualnej i modułu równoważenia obciążenia, używając szablonu usługi Resource Manager z repozytorium szablonów witryny GitHub za pomocą poleceń programu PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="54801-285">Follow these steps to deploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in the GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="54801-286">Krok 1. Sprawdzanie pliku JSON dla szablonu</span><span class="sxs-lookup"><span data-stu-id="54801-286">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="54801-287">Poniżej przedstawiono zawartość pliku JSON dla szablonu.</span><span class="sxs-lookup"><span data-stu-id="54801-287">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="54801-288">Jeśli chcesz, aby najnowszej wersji go ma się [w repozytorium GitHub dla szablonów](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="54801-288">If you want the most recent version, it's located [at the GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="54801-289">W tym temacie używany jest przełącznik `--template-uri` do wywołania szablonu, ale możesz także użyć przełącznika `--template-file` w celu przekazania lokalnej wersji.</span><span class="sxs-lookup"><span data-stu-id="54801-289">This topic uses the `--template-uri` switch to call in the template, but you can also use the `--template-file` switch to pass a local version.</span></span>

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
                "description": "Prefix to use for VM names"
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
                "description": "Size of the VM"
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

### <a name="step-2-create-the-deployment-by-using-the-template"></a><span data-ttu-id="54801-290">Krok 2. Tworzenie wdrożenia przy użyciu szablonu</span><span class="sxs-lookup"><span data-stu-id="54801-290">Step 2: Create the deployment by using the template</span></span>
<span data-ttu-id="54801-291">Utwórz grupę zasobów szablonu przy użyciu polecenia `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="54801-291">Create a resource group for the template by using `azure group create <location>`.</span></span> <span data-ttu-id="54801-292">Następnie utwórz wdrożenie do tej grupy zasobów za pomocą polecenia `azure group deployment create`, przekazując grupę wdrożenia, nazwę wdrożenia i odpowiadając na monity o parametry w szablonie, które nie mają wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="54801-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing the resource group, passing a deployment name, and answering the prompts for parameters in the template that did not have default values.</span></span>

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

<span data-ttu-id="54801-293">Teraz użyj polecenia `azure group deployment create` i opcji `--template-uri`, aby wdrożyć szablon.</span><span class="sxs-lookup"><span data-stu-id="54801-293">Now use the `azure group deployment create` command and the `--template-uri` option to deploy the template.</span></span> <span data-ttu-id="54801-294">Miej przygotowane wartości parametrów do wprowadzenia po wyświetleniu monitu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="54801-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
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
+ Waiting for deployment to complete
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

<span data-ttu-id="54801-295">Należy zauważyć, że ten szablon wdraża obraz systemu Windows Server, który jednak łatwo może zostać zastąpiony przez dowolny obraz systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="54801-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="54801-296">Czy chcesz utworzyć klaster Docker z wieloma menedżerami Swarm?</span><span class="sxs-lookup"><span data-stu-id="54801-296">Want to create a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="54801-297">[Możesz to zrobić](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="54801-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="54801-298"><a id="remove-a-resource-group"></a>Zadanie: Usuwanie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="54801-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="54801-299">Pamiętaj, że możesz wdrożyć ponownie do grupy zasobów, ale jeśli praca z nią została zakończona, możesz usunąć ją za pomocą polecenia `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="54801-299">Remember that you can redeploy to a resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="54801-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Zadanie: Wyświetlanie dziennika dla wdrożenia grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="54801-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show the log for a resource group deployment</span></span>
<span data-ttu-id="54801-301">To zadanie jest typowe podczas tworzenia lub korzystania z szablonów.</span><span class="sxs-lookup"><span data-stu-id="54801-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="54801-302">Do wywołania wyświetlania dzienników wdrożenia dla grupy służy polecenie `azure group log show <groupname>`, które wyświetla część informacji przydatną dla zrozumienia, dlaczego coś się stało lub się nie stało.</span><span class="sxs-lookup"><span data-stu-id="54801-302">The call to display the deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="54801-303">(Aby uzyskać więcej informacji na temat rozwiązywania problemów dotyczących wdrożeń oraz inne informacje o problemach, zobacz [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md) (Rozwiązywanie typowych problemów dotyczących wdrażania za pomocą usługi Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="54801-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="54801-304">W celu określenia konkretnych błędów możesz korzystać z narzędzi, takich jak na przykład narzędzie **jq**, aby badać problemy bardziej precyzyjnie, na przykład zidentyfikować poszczególne błędy, które wymagają naprawienia.</span><span class="sxs-lookup"><span data-stu-id="54801-304">To target specific failures, for example, you might use tools like **jq** to query things a bit more precisely, such as which individual failures you need to correct.</span></span> <span data-ttu-id="54801-305">W poniższym przykładzie użyto narzędzia **jq** do przeanalizowania dziennika wdrożenia dla **lbgroup** w poszukiwaniu błędów.</span><span class="sxs-lookup"><span data-stu-id="54801-305">The following example uses **jq** to parse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="54801-306">Możesz szybko znaleźć przyczynę problemu, naprawić błąd i ponowić próbę.</span><span class="sxs-lookup"><span data-stu-id="54801-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="54801-307">W poniższym przypadku szablon tworzył dwie maszyny wirtualne jednocześnie, co spowodowało blokadę pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="54801-307">In the following case, the template had been creating two VMs at the same time, which created a lock on the .vhd.</span></span> <span data-ttu-id="54801-308">(Po zmodyfikowaniu szablonu wdrożenie szybko się powiodło).</span><span class="sxs-lookup"><span data-stu-id="54801-308">(After we modified the template, the deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"The resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed to acquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="54801-309"><a id="display-information-about-a-virtual-machine"></a>Zadanie: Wyświetlanie informacji o maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54801-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="54801-310">Informacje o określonych maszynach wirtualnych w grupie zasobów można wyświetlić za pomocą polecenia `azure vm show <groupname> <vmname>`.</span><span class="sxs-lookup"><span data-stu-id="54801-310">You can see information about specific VMs in your resource group by using the `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="54801-311">Jeśli w grupie jest więcej niż jedna maszyna wirtualna, może być konieczne wcześniejsze wyświetlenie listy maszyn wirtualnych w grupie za pomocą polecenia `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="54801-311">If you have more than one VM in your group, you might first need to list the VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="54801-312">Następnie wyszukaj maszynę myVM1:</span><span class="sxs-lookup"><span data-stu-id="54801-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up the VM "myVM1"
+ Looking up the NIC "nic1"
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
> <span data-ttu-id="54801-313">Jeśli chcesz programowo przechowywać dane wyjściowe poleceń konsoli i manipulować nimi, możesz użyć narzędzia analizy JSON, na przykład **[jq](https://github.com/stedolan/jq)** lub **[jsawk](https://github.com/micha/jsawk)**, lub bibliotek języka odpowiednich dla zadania.</span><span class="sxs-lookup"><span data-stu-id="54801-313">If you want to programmatically store and manipulate the output of your console commands, you may want to use a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for the task.</span></span>
>
>

## <span data-ttu-id="54801-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Zadanie: Logowanie na maszynie wirtualnej z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="54801-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on to a Linux-based virtual machine</span></span>
<span data-ttu-id="54801-315">Zazwyczaj maszyny z systemem Linux nawiązują połączenie za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="54801-315">Typically Linux machines are connected to through SSH.</span></span> <span data-ttu-id="54801-316">Aby uzyskać więcej informacji, zobacz temat dotyczący [korzystania z protokołu SSH systemu Linux na platformie Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54801-316">For more information, see [How to use SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="54801-317"><a id="stop-a-virtual-machine"></a>Zadanie: Zatrzymywanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54801-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="54801-318">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="54801-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="54801-319">Użyj tego parametru, aby zachować wirtualny adres IP (VIP) sieci wirtualnej w przypadku, gdy jest to ostatnia maszyna wirtualna w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="54801-319">Use this parameter to keep the virtual IP (VIP) of the vnet in case it's the last VM in that vnet.</span></span> <br><br> <span data-ttu-id="54801-320">Jeśli używasz parametru `StayProvisioned`, opłata nadal będzie naliczana za maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="54801-320">If you use the `StayProvisioned` parameter, you'll still be billed for the VM.</span></span>
>
>

## <span data-ttu-id="54801-321"><a id="start-a-virtual-machine"></a>Zadanie: Uruchamianie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="54801-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="54801-322">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="54801-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="54801-323"><a id="attach-a-data-disk"></a>Zadanie: Dołączanie dysku danych</span><span class="sxs-lookup"><span data-stu-id="54801-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="54801-324">Musisz także zdecydować, czy dołączyć nowy dysk, czy taki, który zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="54801-324">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="54801-325">Dla nowego dysku polecenie tworzy plik VHD i dołącza go w tym samym poleceniu.</span><span class="sxs-lookup"><span data-stu-id="54801-325">For a new disk, the command creates the .vhd file and attaches it in the same command.</span></span>

<span data-ttu-id="54801-326">Aby dołączyć nowy dysk, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="54801-326">To attach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="54801-327">Aby dołączyć istniejący dysk danych, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="54801-327">To attach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="54801-328">Następnie należy zainstalować dysk, tak jak zwykle w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="54801-328">Then you'll need to mount the disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54801-329">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54801-329">Next steps</span></span>
<span data-ttu-id="54801-330">Aby uzyskać znacznie więcej przykładów użycia interfejsu wiersza polecenia platformy Azure z trybem **arm**, zobacz [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md) (Używanie interfejsu wiersza polecenia platformy Azure na komputerach Mac i komputerach z systemem Linux oraz Windows z usługą Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="54801-330">For far more examples of Azure CLI usage with the **arm** mode, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="54801-331">Aby dowiedzieć się więcej na temat zasobów platformy Azure i powiązanych koncepcji, zobacz [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54801-331">To learn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="54801-332">Aby uzyskać dodatkowe szablony, których możesz użyć, zobacz [Szablony szybkiego startu platformy Azure](https://azure.microsoft.com/documentation/templates/) i [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Platformy aplikacji korzystające z szablonów).</span><span class="sxs-lookup"><span data-stu-id="54801-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
