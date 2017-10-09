# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="43a6c-101">Wprowadź klastra połączenia zdalnego tooa Kubernetes, DC/OS lub Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="43a6c-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="43a6c-102">Po utworzeniu klastra usługi kontenera platformy Azure, należy tooconnect toohello klastra toodeploy i zarządzanie zadaniami.</span><span class="sxs-lookup"><span data-stu-id="43a6c-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="43a6c-103">W tym artykule opisano, jak tooconnect toohello wzorca wirtualna hello klastra ze zdalnego komputera.</span><span class="sxs-lookup"><span data-stu-id="43a6c-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="43a6c-104">klastry Kubernetes DC/OS i Docker Swarm Hello Podaj lokalnie punktów końcowych HTTP.</span><span class="sxs-lookup"><span data-stu-id="43a6c-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="43a6c-105">Dla Kubernetes, ten punkt końcowy jest bezpiecznie narażony na hello internet i można do niego dostęp, uruchamiając hello `kubectl` narzędzia wiersza polecenia z dowolnego komputera podłączonego do Internetu.</span><span class="sxs-lookup"><span data-stu-id="43a6c-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="43a6c-106">DC/OS i Docker Swarm zaleca się tworzenia tunelu bezpiecznej powłoki (SSH) z systemu zarządzania klastrem toohello komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="43a6c-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="43a6c-107">Po ustanowieniu tunelu hello, możesz uruchamiać polecenia korzystające z punktów końcowych HTTP hello i widoku hello orchestrator interfejs sieci web (jeśli jest dostępna) z systemu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="43a6c-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="43a6c-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="43a6c-108">Prerequisites</span></span>

* <span data-ttu-id="43a6c-109">Klaster Kubernetes, DC/OS lub Docker Swarm [wdrożony w usłudze Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="43a6c-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="43a6c-110">SSH RSA pliku klucza prywatnego odpowiadającego toohello publicznego klucza toohello dodano klastra podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="43a6c-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="43a6c-111">Tych poleceniach założono, jest klucz prywatny SSH hello `$HOME/.ssh/id_rsa` na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="43a6c-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="43a6c-112">Zobacz te instrukcje dla systemów [macOS i Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) lub [Windows](../articles/virtual-machines/linux/ssh-from-windows.md), aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="43a6c-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="43a6c-113">Jeśli hello połączenia SSH nie działa, może być konieczne zbyt [zresetować Twoje klucze SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="43a6c-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="43a6c-114">Połącz tooa Kubernetes klastra</span><span class="sxs-lookup"><span data-stu-id="43a6c-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="43a6c-115">Wykonaj te kroki tooinstall i skonfigurować `kubectl` na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="43a6c-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="43a6c-116">W systemie Linux lub macOS, może być konieczne toorun hello polecenia w tej sekcji przy użyciu `sudo`.</span><span class="sxs-lookup"><span data-stu-id="43a6c-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="43a6c-117">Instalowanie narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="43a6c-117">Install kubectl</span></span>
<span data-ttu-id="43a6c-118">Jednym ze sposobów tooinstall to narzędzie jest toouse hello `az acs kubernetes install-cli` polecenia 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="43a6c-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="43a6c-119">toorun to polecenie, upewnij się, że możesz [zainstalowane](/cli/azure/install-az-cli2) hello najnowsze Azure CLI 2.0 i rejestrowane w tooan konto platformy Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="43a6c-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="43a6c-120">Alternatywnie można pobrać hello najnowszych `kubectl` klienta bezpośrednio z hello [Kubernetes zwalnia strony](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="43a6c-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="43a6c-121">Aby uzyskać więcej informacji, zobacz [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Instalowanie i konfigurowanie narzędzia kubectl).</span><span class="sxs-lookup"><span data-stu-id="43a6c-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="43a6c-122">Pobieranie poświadczeń klastra</span><span class="sxs-lookup"><span data-stu-id="43a6c-122">Download cluster credentials</span></span>
<span data-ttu-id="43a6c-123">Po utworzeniu `kubectl` zainstalowany, należy toocopy hello klastra poświadczenia tooyour maszyny.</span><span class="sxs-lookup"><span data-stu-id="43a6c-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="43a6c-124">Jednym ze sposobów toodo get hello poświadczeń jest z hello `az acs kubernetes get-credentials` polecenia.</span><span class="sxs-lookup"><span data-stu-id="43a6c-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="43a6c-125">Przekaż hello nazwę grupy zasobów hello i hello Nazwa zasobu usługi kontenera hello:</span><span class="sxs-lookup"><span data-stu-id="43a6c-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="43a6c-126">To polecenie pobiera poświadczenia klastra hello zbyt`$HOME/.kube/config`, gdzie `kubectl` oczekuje toobe znajduje się.</span><span class="sxs-lookup"><span data-stu-id="43a6c-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="43a6c-127">Alternatywnie można użyć `scp` toosecurely kopiowania hello pliku z `$HOME/.kube/config` na komputerze lokalnym hello głównej maszyny Wirtualnej tooyour.</span><span class="sxs-lookup"><span data-stu-id="43a6c-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="43a6c-128">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="43a6c-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="43a6c-129">Jeśli w systemie Windows, można użyć Bash na Ubuntu systemu Windows, klient kopiowania PuTTy bezpiecznych plików hello lub podobnego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="43a6c-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="43a6c-130">Używanie narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="43a6c-130">Use kubectl</span></span>

<span data-ttu-id="43a6c-131">Po utworzeniu `kubectl` skonfigurowane, Testuj połączenie hello poprzez wyszczególnienie hello węzłów w klastrze:</span><span class="sxs-lookup"><span data-stu-id="43a6c-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="43a6c-132">Możesz wypróbować inne polecenia narzędzia `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="43a6c-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="43a6c-133">Na przykład można wyświetlić hello Kubernetes pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="43a6c-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="43a6c-134">Najpierw uruchom serwer proxy serwera interfejsu API Kubernetes toohello:</span><span class="sxs-lookup"><span data-stu-id="43a6c-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="43a6c-135">Hello Kubernetes interfejsu użytkownika jest teraz dostępne pod adresem: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="43a6c-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="43a6c-136">Aby uzyskać więcej informacji, zobacz hello [Kubernetes szybki start](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="43a6c-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="43a6c-137">Połącz z klastrem DC/OS lub Swarm tooa</span><span class="sxs-lookup"><span data-stu-id="43a6c-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="43a6c-138">hello toouse DC/OS i Docker Swarm klastrów wdrożone przez usługi kontenera platformy Azure, wykonaj te instrukcje toocreate tunelu SSH z lokalnego systemu Linux, macOS lub systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="43a6c-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="43a6c-139">Te instrukcje koncentrują się na tunelowaniu ruchu TCP przez protokół SSH.</span><span class="sxs-lookup"><span data-stu-id="43a6c-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="43a6c-140">Można też uruchomić sesji interaktywnej SSH z jednego z systemów zarządzania hello wewnątrz klastra, ale nie jest to zalecane.</span><span class="sxs-lookup"><span data-stu-id="43a6c-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="43a6c-141">Praca bezpośrednio na systemie wewnętrznym niesie za sobą ryzyko wprowadzenia niezamierzonych zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="43a6c-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="43a6c-142">Tworzenie tunelu SSH w systemie Linux lub macOS</span><span class="sxs-lookup"><span data-stu-id="43a6c-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="43a6c-143">Hello pierwszym krokiem tworzenia tunelu SSH w systemie Linux lub macOS jest toolocate hello publicznej nazwy DNS hello zrównoważonym obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="43a6c-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="43a6c-144">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="43a6c-144">Follow these steps:</span></span>


1. <span data-ttu-id="43a6c-145">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello grupę zasobów, zawierającą klaster usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="43a6c-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="43a6c-146">Rozwiń grupę zasobów hello tak, aby każdy z zasobów jest wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="43a6c-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="43a6c-147">Kliknij przycisk hello **usługi kontenera** zasobów, a następnie kliknij przycisk **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="43a6c-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="43a6c-148">Witaj **wzorca nazwy FQDN** z hello klastra jest wyświetlana w obszarze **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="43a6c-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="43a6c-149">Zapisz tę nazwę do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="43a6c-149">Save this name for later use.</span></span> 

    ![Publiczna nazwa DNS](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="43a6c-151">Można również uruchomić hello `az acs show` polecenia w usłudze kontenera.</span><span class="sxs-lookup"><span data-stu-id="43a6c-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="43a6c-152">Wyszukaj hello **wzorca profilu: fqdn** właściwości w danych wyjściowych polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="43a6c-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="43a6c-153">Teraz Otwórz powłokę i uruchom hello `ssh` polecenie, określając hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="43a6c-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="43a6c-154">**LOCAL_PORT** jest port TCP powitania po stronie usługi hello tooconnect tunelu hello do.</span><span class="sxs-lookup"><span data-stu-id="43a6c-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="43a6c-155">W przypadku klastra Swarm Ustaw ten too2375.</span><span class="sxs-lookup"><span data-stu-id="43a6c-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="43a6c-156">W przypadku DC/OS wartość ta too80.</span><span class="sxs-lookup"><span data-stu-id="43a6c-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="43a6c-157">**REMOTE_PORT** jest port hello hello punktu końcowego, które mają tooexpose.</span><span class="sxs-lookup"><span data-stu-id="43a6c-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="43a6c-158">W przypadku klastra Swarm jest to port 2375.</span><span class="sxs-lookup"><span data-stu-id="43a6c-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="43a6c-159">W przypadku klastra DC/OS jest to port 80.</span><span class="sxs-lookup"><span data-stu-id="43a6c-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="43a6c-160">**Nazwa użytkownika** jest nazwą użytkownika hello dostarczony po wdrożeniu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="43a6c-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="43a6c-161">**DNSPREFIX** jest hello prefiks DNS podany podczas wdrażania klastra hello.</span><span class="sxs-lookup"><span data-stu-id="43a6c-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="43a6c-162">**REGION** jest hello regionu, w którym znajduje się w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="43a6c-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="43a6c-163">**PATH_TO_PRIVATE_KEY** [OPCJONALNIE] to hello ścieżki toohello klucza prywatnego, który odpowiada toohello klucza publicznego podane podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="43a6c-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="43a6c-164">Użyj tej opcji z hello `-i` flagi.</span><span class="sxs-lookup"><span data-stu-id="43a6c-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="43a6c-165">Hello port połączenia SSH to 2200, a nie hello standardowy port 22.</span><span class="sxs-lookup"><span data-stu-id="43a6c-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="43a6c-166">W klastrze z więcej niż jedną maszyną Wirtualną głównego jest hello połączenia portu toohello pierwszego serwera głównego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43a6c-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="43a6c-167">polecenie Hello zwraca bez danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="43a6c-167">hello command returns without output.</span></span>

<span data-ttu-id="43a6c-168">Przykłady hello DC/OS i Swarm w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="43a6c-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="43a6c-169">Tunel DC/OS</span><span class="sxs-lookup"><span data-stu-id="43a6c-169">DC/OS tunnel</span></span>
<span data-ttu-id="43a6c-170">tooopen tunelu dla punktów końcowych DC/OS, uruchom polecenie, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="43a6c-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="43a6c-171">Upewnij się, że nie ma innego procesu lokalnego powiązanego z portem 80.</span><span class="sxs-lookup"><span data-stu-id="43a6c-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="43a6c-172">Jeśli to konieczne, możesz określić port lokalny inny niż 80, na przykład 8080.</span><span class="sxs-lookup"><span data-stu-id="43a6c-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="43a6c-173">Jednak gdy ten port jest używany, niektóre linki w interfejsie użytkownika sieci Web mogą nie działać.</span><span class="sxs-lookup"><span data-stu-id="43a6c-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="43a6c-174">Punkty końcowe DC/OS hello można uzyskać dostęp z systemu lokalnego za pośrednictwem hello następujące adresy URL (przy założeniu lokalnych port 80):</span><span class="sxs-lookup"><span data-stu-id="43a6c-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="43a6c-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="43a6c-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="43a6c-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="43a6c-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="43a6c-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="43a6c-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="43a6c-178">Podobnie można osiągnąć hello interfejsów API rest dla każdej aplikacji przez ten tunel.</span><span class="sxs-lookup"><span data-stu-id="43a6c-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="43a6c-179">Tunel Swarm</span><span class="sxs-lookup"><span data-stu-id="43a6c-179">Swarm tunnel</span></span>
<span data-ttu-id="43a6c-180">tooopen punktu końcowego Swarm toohello tunelu, uruchom polecenie, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="43a6c-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="43a6c-181">Upewnij się, że nie ma innego procesu lokalnego powiązanego z portem 2375.</span><span class="sxs-lookup"><span data-stu-id="43a6c-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="43a6c-182">Na przykład jeśli jest uruchomiony demon Docker hello lokalnie, jest ustawiona przez domyślny toouse port 2375.</span><span class="sxs-lookup"><span data-stu-id="43a6c-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="43a6c-183">Jeśli to konieczne, możesz określić port lokalny inny niż 2375.</span><span class="sxs-lookup"><span data-stu-id="43a6c-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="43a6c-184">Można teraz uzyskać dostępu do hello klaster Docker Swarm przy użyciu interfejsu wiersza polecenia Docker hello (Docker CLI) w systemie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="43a6c-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="43a6c-185">Aby uzyskać instrukcje dotyczące instalacji, zobacz [Instalowanie platformy Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="43a6c-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="43a6c-186">Ustaw zmienną DOCKER_HOST toohello w środowisku portów lokalnych skonfigurowane dla hello tunelu.</span><span class="sxs-lookup"><span data-stu-id="43a6c-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="43a6c-187">Uruchom polecenia Docker klastrze Docker Swarm toohello tunelu.</span><span class="sxs-lookup"><span data-stu-id="43a6c-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="43a6c-188">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="43a6c-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="43a6c-189">Tworzenie tunelu SSH w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="43a6c-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="43a6c-190">Istnieje wiele opcji tworzenia tuneli SSH w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="43a6c-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="43a6c-191">Jeżeli Bash na Ubuntu działają w systemie Windows lub podobnego narzędzia, należy wykonać instrukcje tunelowania SSH hello przedstawionej w tym artykule, aby system macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="43a6c-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="43a6c-192">Alternatywnie w systemie Windows, w tej sekcji opisano sposób toouse PuTTY toocreate hello tunelu.</span><span class="sxs-lookup"><span data-stu-id="43a6c-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="43a6c-193">[Pobierz program PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="43a6c-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="43a6c-194">Uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="43a6c-194">Run hello application.</span></span>

3. <span data-ttu-id="43a6c-195">Wprowadź nazwę hosta, który składa się z nazwy użytkownika administratora klastra hello i hello publicznej nazwy DNS pierwszego serwera głównego hello w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="43a6c-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="43a6c-196">Witaj **nazwy hosta** wygląda podobnie zbyt`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="43a6c-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="43a6c-197">Wprowadź wartość 2200 dla hello **portu**.</span><span class="sxs-lookup"><span data-stu-id="43a6c-197">Enter 2200 for hello **Port**.</span></span>

    ![Konfiguracja programu PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="43a6c-199">Wybierz pozycje **SSH > Uwierzytelnianie**. Dodaj ścieżkę tooyour plik klucza prywatnego (format ppk) do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="43a6c-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="43a6c-200">Można użyć narzędzia, takie jak [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate to plik z hello klastra hello toocreate używane klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="43a6c-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![Konfiguracja programu PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="43a6c-202">Wybierz **SSH > tuneli** i skonfigurować hello następujące przekazane porty:</span><span class="sxs-lookup"><span data-stu-id="43a6c-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="43a6c-203">**Port źródłowy:** — użyj portu 80 w przypadku opcji DC/OS lub portu 2375 w przypadku opcji Swarm.</span><span class="sxs-lookup"><span data-stu-id="43a6c-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="43a6c-204">**Miejsce docelowe:** — użyj wartości localhost:80 w przypadku opcji DC/OS lub wartości localhost:2375 w przypadku opcji Swarm.</span><span class="sxs-lookup"><span data-stu-id="43a6c-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="43a6c-205">Poniższy przykład Hello jest skonfigurowany dla DC/OS, ale będzie wyglądać podobnie w przypadku rozwiązania Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="43a6c-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43a6c-206">W przypadku tworzenia tego tunelu nie można używać portu 80.</span><span class="sxs-lookup"><span data-stu-id="43a6c-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Konfiguracja programu PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="43a6c-208">Po zakończeniu kliknij przycisk **sesji > Zapisz** toosave hello połączenie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="43a6c-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="43a6c-209">tooconnect toohello programu PuTTY sesji, kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="43a6c-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="43a6c-210">Po ustanowieniu połączenia widać hello konfiguracji portów w dzienniku zdarzeń programu PuTTY hello.</span><span class="sxs-lookup"><span data-stu-id="43a6c-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![Dziennik zdarzeń programu PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="43a6c-212">Po skonfigurowaniu tunelu hello w przypadku opcji DC/OS, możesz uzyskać dostęp hello powiązane punkty końcowe na:</span><span class="sxs-lookup"><span data-stu-id="43a6c-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="43a6c-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="43a6c-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="43a6c-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="43a6c-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="43a6c-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="43a6c-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="43a6c-216">Po skonfigurowaniu hello tunelu dla rozwiązania Docker Swarm, otwórz tooconfigure ustawień z systemu Windows w systemie zmienną środowiskową o nazwie `DOCKER_HOST` o wartości `:2375`.</span><span class="sxs-lookup"><span data-stu-id="43a6c-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="43a6c-217">Następnie mają dostęp do klastra Swarm hello przez hello interfejsu wiersza polecenia Docker.</span><span class="sxs-lookup"><span data-stu-id="43a6c-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43a6c-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43a6c-218">Next steps</span></span>
<span data-ttu-id="43a6c-219">Wdrażanie kontenerów i zarządzanie nimi w klastrze:</span><span class="sxs-lookup"><span data-stu-id="43a6c-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="43a6c-220">Współpraca z usługą Azure Container Service i rozwiązaniem Kubernetes</span><span class="sxs-lookup"><span data-stu-id="43a6c-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="43a6c-221">Współpraca z usługą Azure Container Service i rozwiązaniem DC/OS</span><span class="sxs-lookup"><span data-stu-id="43a6c-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="43a6c-222">Praca z hello usługi kontenera platformy Azure i klastrem Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="43a6c-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

