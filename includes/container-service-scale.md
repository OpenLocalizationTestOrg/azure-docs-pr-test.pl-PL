# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="26718-101">Skalowanie węzłów agenta w klastrze usługi Container Service</span><span class="sxs-lookup"><span data-stu-id="26718-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="26718-102">Po [wdrażanie klastra usługi kontenera platformy Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), może być konieczne toochange hello liczba węzłów agenta.</span><span class="sxs-lookup"><span data-stu-id="26718-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="26718-103">Możesz na przykład potrzebować więcej agentów, aby uruchamiać więcej wystąpień lub aplikacji kontenera.</span><span class="sxs-lookup"><span data-stu-id="26718-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="26718-104">Można zmienić liczbę hello agenta węzłów w klastrze DC/OS, Docker Swarm lub Kubernetes przy użyciu portalu Azure hello lub hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="26718-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="26718-105">Skalować hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="26718-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="26718-106">W hello [portalu Azure](https://portal.azure.com), wyszukaj **usługi kontenerów**, a następnie kliknij przycisk hello kontenera usługi, które mają toomodify.</span><span class="sxs-lookup"><span data-stu-id="26718-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="26718-107">W hello **usługi kontenera** bloku, kliknij przycisk **agentów**.</span><span class="sxs-lookup"><span data-stu-id="26718-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="26718-108">W **liczba maszyn wirtualnych**, wprowadź hello żądaną liczbę węzłów agentów.</span><span class="sxs-lookup"><span data-stu-id="26718-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Skalowanie puli w portalu hello](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="26718-110">Konfiguracja hello toosave, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="26718-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="26718-111">Skalować hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="26718-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="26718-112">Upewnij się, że możesz [zainstalowane](/cli/azure/install-az-cli2) hello najnowsze Azure CLI 2.0 i rejestrowane w tooan konto platformy azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="26718-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="26718-113">Zobacz hello bieżąca liczba agentów</span><span class="sxs-lookup"><span data-stu-id="26718-113">See hello current agent count</span></span>
<span data-ttu-id="26718-114">toosee hello liczby agentów obecnie w klastrze hello Uruchom hello `az acs show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="26718-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="26718-115">Oznacza to hello konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="26718-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="26718-116">Na przykład Witaj następujące polecenia pokazuje hello konfiguracji hello usługi kontenera o nazwie `containerservice-myACSName` w grupie zasobów hello `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="26718-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="26718-117">polecenie Hello zwraca hello liczba agentów w hello `Count` wartości w obszarze `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="26718-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="26718-118">Użyj hello az polecenia Skaluj acs</span><span class="sxs-lookup"><span data-stu-id="26718-118">Use hello az acs scale command</span></span>
<span data-ttu-id="26718-119">toochange hello liczba węzłów agenta, uruchom hello `az acs scale` polecenia i dostawy hello **grupy zasobów**, **nazwa kontenera usługi**i hello potrzeby **nowego licznika agenta**.</span><span class="sxs-lookup"><span data-stu-id="26718-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="26718-120">Używając mniejszej lub większej liczby, możesz odpowiednio skalować w dół lub w górę.</span><span class="sxs-lookup"><span data-stu-id="26718-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="26718-121">Na przykład toochange hello liczba agentów w poprzednim hello klastra too10, hello wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="26718-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="26718-122">Hello Azure CLI 2.0 zwraca ciąg JSON reprezentujący hello nową konfigurację usługi kontenera hello, w tym hello nowego licznika agenta.</span><span class="sxs-lookup"><span data-stu-id="26718-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="26718-123">Aby uzyskać więcej opcji poleceń, uruchom polecenie `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="26718-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="26718-124">Zagadnienia dotyczące skalowania</span><span class="sxs-lookup"><span data-stu-id="26718-124">Scaling considerations</span></span>

* <span data-ttu-id="26718-125">Hello liczba węzłów agent musi być od 1 do 100 włącznie.</span><span class="sxs-lookup"><span data-stu-id="26718-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="26718-126">Limitu przydziału rdzeni można ograniczyć liczbę hello agenta węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="26718-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="26718-127">Operacje skalowania węzła agenta są zastosowane tooan zestaw skali maszyny wirtualnej platformy Azure, zawierający hello puli agenta.</span><span class="sxs-lookup"><span data-stu-id="26718-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="26718-128">W klastrze DC/OS tylko węzły agenta w puli prywatnej hello są skalowane przez operacje hello wyświetlane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="26718-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="26718-129">W zależności od hello programu orchestrator, które można wdrożyć w klastrze można oddzielnie skalować hello liczbę wystąpień kontenera uruchomiona w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="26718-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="26718-130">Na przykład w klastrze DC/OS, należy użyć hello [interfejs użytkownika platformy Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello liczbę wystąpień kontenera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="26718-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="26718-131">Obecnie automatyczne skalowanie węzłów agenta w klastrze usługi kontenera nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="26718-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26718-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="26718-132">Next steps</span></span>
* <span data-ttu-id="26718-133">Zobacz [więcej przykładów](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) używania poleceń interfejsu wiersza polecenia platformy Azure 2.0 z usługą Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="26718-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="26718-134">Dowiedz się więcej o [pulach agentów platformy DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) w usłudze Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="26718-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

