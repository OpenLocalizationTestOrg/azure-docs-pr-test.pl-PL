# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="0fa93-101">Skalowanie węzłów agenta w klastrze usługi Container Service</span><span class="sxs-lookup"><span data-stu-id="0fa93-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="0fa93-102">Po [wdrożeniu klastra usługi Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md) być może trzeba będzie zmienić liczbę węzłów agenta.</span><span class="sxs-lookup"><span data-stu-id="0fa93-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need to change the number of agent nodes.</span></span> <span data-ttu-id="0fa93-103">Możesz na przykład potrzebować więcej agentów, aby uruchamiać więcej wystąpień lub aplikacji kontenera.</span><span class="sxs-lookup"><span data-stu-id="0fa93-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="0fa93-104">Możesz zmienić liczbę węzłów agenta w klastrze DC/OS, Docker Swarm lub Kubernetes za pomocą witryny Azure Portal lub interfejsu wiersza polecenia platformy Azure w wersji 2.0.</span><span class="sxs-lookup"><span data-stu-id="0fa93-104">You can change the number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using the Azure portal or the Azure CLI 2.0.</span></span> 

## <a name="scale-with-the-azure-portal"></a><span data-ttu-id="0fa93-105">Skalowanie w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0fa93-105">Scale with the Azure portal</span></span>

1. <span data-ttu-id="0fa93-106">W witrynie [Azure Portal](https://portal.azure.com) przejdź do pozycji **Usługi kontenerów**, a następnie kliknij usługę kontenera, którą chcesz zmodyfikować.</span><span class="sxs-lookup"><span data-stu-id="0fa93-106">In the [Azure portal](https://portal.azure.com), browse for **Container services**, and then click the container service that you want to modify.</span></span>
2. <span data-ttu-id="0fa93-107">W bloku **Usługi kontenerów** kliknij przycisk **Agenci**.</span><span class="sxs-lookup"><span data-stu-id="0fa93-107">In the **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="0fa93-108">W polu **Liczba maszyn wirtualnych** wpisz odpowiednią liczbę węzłów agentów.</span><span class="sxs-lookup"><span data-stu-id="0fa93-108">In **VM Count**, enter the desired number of agents nodes.</span></span>

    ![Skalowanie puli w portalu](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="0fa93-110">Aby zapisać konfigurację, kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0fa93-110">To save the configuration, click **Save**.</span></span>

## <a name="scale-with-the-azure-cli-20"></a><span data-ttu-id="0fa93-111">Skalowanie przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="0fa93-111">Scale with the Azure CLI 2.0</span></span>

<span data-ttu-id="0fa93-112">Upewnij się, że [zainstalowano](/cli/azure/install-az-cli2) najnowszy interfejs wiersza polecenia platformy Azure 2.0 i zalogowano się na koncie platformy Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="0fa93-112">Make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an azure account (`az login`).</span></span>

### <a name="see-the-current-agent-count"></a><span data-ttu-id="0fa93-113">Sprawdzanie bieżącej liczby agentów</span><span class="sxs-lookup"><span data-stu-id="0fa93-113">See the current agent count</span></span>
<span data-ttu-id="0fa93-114">Aby wyświetlić bieżącą liczbę agentów w klastrze, uruchom polecenie `az acs show`.</span><span class="sxs-lookup"><span data-stu-id="0fa93-114">To see the number of agents currently in the cluster, run the `az acs show` command.</span></span> <span data-ttu-id="0fa93-115">Przedstawia ono konfigurację klastra.</span><span class="sxs-lookup"><span data-stu-id="0fa93-115">This shows the cluster configuration.</span></span> <span data-ttu-id="0fa93-116">Na przykład następujące polecenie przedstawia konfigurację usługi kontenera o nazwie `containerservice-myACSName` w grupie zasobów `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="0fa93-116">For example, the following command shows the configuration of the container service named `containerservice-myACSName` in the resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="0fa93-117">Polecenie zwraca liczbę agentów w wartości `Count` w obszarze `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="0fa93-117">The command returns the number of agents in the `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-the-az-acs-scale-command"></a><span data-ttu-id="0fa93-118">Użycie polecenia az acs scale</span><span class="sxs-lookup"><span data-stu-id="0fa93-118">Use the az acs scale command</span></span>
<span data-ttu-id="0fa93-119">Aby zmienić liczbę węzłów agenta, uruchom polecenie `az acs scale` i określ **grupę zasobów**, **nazwę usługi kontenera** i żądaną **nową liczbę agentów**.</span><span class="sxs-lookup"><span data-stu-id="0fa93-119">To change the number of agent nodes, run the `az acs scale` command and supply the **resource group**, **container service name**, and the desired **new agent count**.</span></span> <span data-ttu-id="0fa93-120">Używając mniejszej lub większej liczby, możesz odpowiednio skalować w dół lub w górę.</span><span class="sxs-lookup"><span data-stu-id="0fa93-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="0fa93-121">Aby na przykład zmienić liczbę agentów w poprzednim klastrze na 10, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="0fa93-121">For example, to change the number of agents in the previous cluster to 10, type the following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="0fa93-122">Interfejs wiersza polecenia platformy Azure 2.0 zwraca ciąg JSON reprezentujący nową konfigurację usługi kontenera, w tym nową liczbę agentów.</span><span class="sxs-lookup"><span data-stu-id="0fa93-122">The Azure CLI 2.0 returns a JSON string representing the new configuration of the container service, including the new agent count.</span></span>

<span data-ttu-id="0fa93-123">Aby uzyskać więcej opcji poleceń, uruchom polecenie `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="0fa93-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="0fa93-124">Zagadnienia dotyczące skalowania</span><span class="sxs-lookup"><span data-stu-id="0fa93-124">Scaling considerations</span></span>

* <span data-ttu-id="0fa93-125">Liczba węzłów agenta musi należeć do przedziału od 1 do 100 włącznie.</span><span class="sxs-lookup"><span data-stu-id="0fa93-125">The number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="0fa93-126">Limit przydziału rdzeni może ograniczyć liczbę węzłów agenta w klastrze.</span><span class="sxs-lookup"><span data-stu-id="0fa93-126">Your cores quota can limit the number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="0fa93-127">Operacje skalowania węzła agenta są stosowane do zestawu skalowania maszyn wirtualnych platformy Azure, który zawiera pulę agentów.</span><span class="sxs-lookup"><span data-stu-id="0fa93-127">Agent node scaling operations are applied to an Azure virtual machine scale set that contains the agent pool.</span></span> <span data-ttu-id="0fa93-128">W klastrze DC/OS tylko węzły agenta w puli prywatnej są skalowane przy użyciu operacji przedstawionych w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="0fa93-128">In a DC/OS cluster, only agent nodes in the private pool are scaled by the operations shown in this article.</span></span>

* <span data-ttu-id="0fa93-129">W zależności od wdrażanego w klastrze koordynatora można oddzielnie skalować liczbę wystąpień kontenera uruchomionego w klastrze.</span><span class="sxs-lookup"><span data-stu-id="0fa93-129">Depending on the orchestrator you deploy in your cluster, you can separately scale the number of instances of a container running on the cluster.</span></span> <span data-ttu-id="0fa93-130">Na przykład w klastrze DC/OS należy użyć [interfejsu użytkownika platformy Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md), aby zmienić liczbę wystąpień aplikacji kontenera.</span><span class="sxs-lookup"><span data-stu-id="0fa93-130">For example, in a DC/OS cluster, use the [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) to change the number of instances of a container application.</span></span>

* <span data-ttu-id="0fa93-131">Obecnie automatyczne skalowanie węzłów agenta w klastrze usługi kontenera nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0fa93-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fa93-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0fa93-132">Next steps</span></span>
* <span data-ttu-id="0fa93-133">Zobacz [więcej przykładów](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) używania poleceń interfejsu wiersza polecenia platformy Azure 2.0 z usługą Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="0fa93-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="0fa93-134">Dowiedz się więcej o [pulach agentów platformy DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) w usłudze Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="0fa93-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

