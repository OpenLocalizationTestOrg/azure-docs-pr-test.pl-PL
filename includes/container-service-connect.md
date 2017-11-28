# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="3f1c9-101">Nawiązywanie zdalnego połączenia z klastrem Kubernetes, DC/OS lub Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="3f1c9-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="3f1c9-102">Po utworzeniu klastra usługi Azure Container Service należy połączyć się z klastrem, aby wdrożyć obciążenia i zarządzać nimi.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="3f1c9-103">W tym artykule opisano sposób nawiązywania połączenia z główną maszyną wirtualną klastra z komputera zdalnego.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="3f1c9-104">Klastry Kubernetes, DC/OS i Docker Swarm udostępniają punkty końcowe HTTP lokalnie.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="3f1c9-105">W przypadku klastrów Kubernetes ten punkt końcowy jest bezpiecznie uwidaczniany w Internecie i można do niego uzyskać dostęp, uruchamiając narzędzie wiersza polecenia `kubectl` z dowolnej maszyny podłączonej do Internetu.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="3f1c9-106">W przypadku rozwiązań DC/OS i Docker Swarm zalecamy utworzenie tunelu Secure Shell (SSH) między komputerem lokalnym a systemem zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="3f1c9-107">Po utworzeniu tunelu możesz uruchamiać polecenia korzystające z punktów końcowych HTTP i wyświetlać interfejs sieci Web koordynatora (jeśli jest dostępny) z systemu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3f1c9-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3f1c9-108">Prerequisites</span></span>

* <span data-ttu-id="3f1c9-109">Klaster Kubernetes, DC/OS lub Docker Swarm [wdrożony w usłudze Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="3f1c9-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="3f1c9-110">Plik klucza prywatnego SSH RSA odpowiadający kluczowi publicznemu dodanemu do klastra podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="3f1c9-111">Te polecenia zakładają, że prywatny klucz SSH znajduje się w folderu `$HOME/.ssh/id_rsa` na komputerze.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="3f1c9-112">Zobacz te instrukcje dla systemów [macOS i Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) lub [Windows](../articles/virtual-machines/linux/ssh-from-windows.md), aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="3f1c9-113">Jeśli połączenie SSH nie działa, konieczne może być [zresetowanie kluczy SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3f1c9-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="3f1c9-114">Nawiązywanie połączenia z klastrem Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3f1c9-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="3f1c9-115">Wykonaj następujące kroki, aby zainstalować i skonfigurować narzędzie `kubectl` na komputerze.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="3f1c9-116">W systemie Linux lub macOS może być konieczne uruchomienie poleceń w tej sekcji przy użyciu elementu `sudo`.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="3f1c9-117">Instalowanie narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="3f1c9-117">Install kubectl</span></span>
<span data-ttu-id="3f1c9-118">Jednym ze sposobów instalacji tego narzędzia jest użycie polecenia `az acs kubernetes install-cli` interfejsu wiersza polecenia platformy Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="3f1c9-119">Aby uruchomić to polecenie, upewnij się, że [zainstalowano](/cli/azure/install-az-cli2) najnowszy interfejs wiersza polecenia platformy Azure 2.0 i zalogowano się na koncie platformy Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="3f1c9-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="3f1c9-120">Możesz też pobrać najnowszego klienta `kubectl` bezpośrednio ze [strony z wersjami usługi Kubernetes](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="3f1c9-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="3f1c9-121">Aby uzyskać więcej informacji, zobacz [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Instalowanie i konfigurowanie narzędzia kubectl).</span><span class="sxs-lookup"><span data-stu-id="3f1c9-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="3f1c9-122">Pobieranie poświadczeń klastra</span><span class="sxs-lookup"><span data-stu-id="3f1c9-122">Download cluster credentials</span></span>
<span data-ttu-id="3f1c9-123">Po zainstalowaniu narzędzia `kubectl` musisz skopiować poświadczenia klastra do swojej maszyny.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="3f1c9-124">Jednym ze sposobów uzyskania poświadczeń jest użycie polecenia `az acs kubernetes get-credentials`.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="3f1c9-125">Przekaż nazwę grupy zasobów i nazwę zasobu usługi Container Service:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="3f1c9-126">To polecenie pobiera poświadczenia klastra do folderu `$HOME/.kube/config` zgodnie z oczekiwaniami narzędzia `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="3f1c9-127">Możesz też użyć narzędzia `scp`, aby bezpiecznie skopiować plik z folderu `$HOME/.kube/config` na głównej maszynie wirtualnej do maszyny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="3f1c9-128">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="3f1c9-129">Jeśli pracujesz w systemie Windows, możesz użyć narzędzia Bash on Ubuntu on Windows, klienta bezpiecznego kopiowania plików programu PuTTy lub podobnego narzędzia.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="3f1c9-130">Używanie narzędzia kubectl</span><span class="sxs-lookup"><span data-stu-id="3f1c9-130">Use kubectl</span></span>

<span data-ttu-id="3f1c9-131">Po skonfigurowaniu narzędzia `kubectl` przetestuj połączenie, wyświetlając listę węzłów w klastrze:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="3f1c9-132">Możesz wypróbować inne polecenia narzędzia `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="3f1c9-133">Możesz na przykład wyświetlić pulpit nawigacyjny platformy Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="3f1c9-134">Najpierw uruchom serwer proxy do serwera interfejsu API Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="3f1c9-135">Interfejs użytkownika platformy Kubernetes jest obecnie dostępny pod adresem: `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="3f1c9-136">Aby uzyskać więcej informacji, zobacz [Kubernetes — szybki start](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="3f1c9-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="3f1c9-137">Nawiązywanie połączenia z klastrem DC/OS lub Swarm</span><span class="sxs-lookup"><span data-stu-id="3f1c9-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="3f1c9-138">Aby korzystać z klastrów DC/OS i Docker Swarm wdrożonych przez usługę Azure Container Service, postępuj zgodnie z tymi instrukcjami w celu utworzenia tunelu SSH z lokalnego systemu Linux, macOS lub Windows.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="3f1c9-139">Te instrukcje koncentrują się na tunelowaniu ruchu TCP przez protokół SSH.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="3f1c9-140">Możesz też uruchomić interaktywną sesję SSH z jednym z wewnętrznych systemów zarządzania klastrami, ale nie zalecamy tego.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="3f1c9-141">Praca bezpośrednio na systemie wewnętrznym niesie za sobą ryzyko wprowadzenia niezamierzonych zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="3f1c9-142">Tworzenie tunelu SSH w systemie Linux lub macOS</span><span class="sxs-lookup"><span data-stu-id="3f1c9-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="3f1c9-143">Pierwszym krokiem tworzenia tunelu SSH w systemie Linux lub macOS jest zlokalizowanie publicznej nazwy DNS serwerów głównych ze zrównoważonym obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="3f1c9-144">Wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-144">Follow these steps:</span></span>


1. <span data-ttu-id="3f1c9-145">W witrynie [Azure Portal](https://portal.azure.com) przejdź do grupy zasobów zawierającej klaster usługi Containter Service.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="3f1c9-146">Rozwiń grupę zasobów, aby wyświetlić poszczególne zasoby.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="3f1c9-147">Kliknij zasób **Usługa kontenera**, a następnie kliknij pozycję **Przegląd**.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="3f1c9-148">W obszarze **Podstawy** zostanie wyświetlona **główna nazwa FQDN** klastra.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="3f1c9-149">Zapisz tę nazwę do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-149">Save this name for later use.</span></span> 

    ![Publiczna nazwa DNS](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="3f1c9-151">Możesz też uruchomić polecenie `az acs show` względem usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="3f1c9-152">Następnie poszukaj właściwości **Master Profile:fqdn** w danych wyjściowych polecenia.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="3f1c9-153">Otwórz powłokę i uruchom polecenie `ssh`, określając następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="3f1c9-154">**LOCAL_PORT** to port TCP tunelu po stronie usługi, z którym należy się połączyć.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="3f1c9-155">W przypadku klastra Swarm ustaw tę wartość na 2375.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="3f1c9-156">W przypadku klastra DC/OS ustaw tę wartość na 80.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="3f1c9-157">**REMOTE_PORT** to port punktu końcowego, który ma zostać udostępniony.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="3f1c9-158">W przypadku klastra Swarm jest to port 2375.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="3f1c9-159">W przypadku klastra DC/OS jest to port 80.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="3f1c9-160">**USERNAME** (nazwa_użytkownika) to nazwa użytkownika podana podczas wdrażania klastra.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="3f1c9-161">**DNSPREFIX** (prefiks_DNS) to prefiks DNS podany podczas wdrażania klastra.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="3f1c9-162">**REGION** to region, w którym znajduje się grupa zasobów.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="3f1c9-163">**PATH_TO_PRIVATE_KEY** [OPCJONALNIE] to ścieżka do klucza prywatnego odpowiadającego kluczowi publicznemu podanemu podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="3f1c9-164">Użyj tej opcji z flagą `-i`.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="3f1c9-165">Port połączenia SSH to 2200, a nie standardowy port 22.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="3f1c9-166">W klastrze z więcej niż jedną główną maszyną wirtualną jest to port połączenia z pierwszą główną maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="3f1c9-167">Polecenie jest zwracane bez danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-167">The command returns without output.</span></span>

<span data-ttu-id="3f1c9-168">Zobacz przykłady dla klastrów DC/OS i Swarm w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="3f1c9-169">Tunel DC/OS</span><span class="sxs-lookup"><span data-stu-id="3f1c9-169">DC/OS tunnel</span></span>
<span data-ttu-id="3f1c9-170">Aby otworzyć tunel dla punktów końcowych DC/OS, uruchom polecenie podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="3f1c9-171">Upewnij się, że nie ma innego procesu lokalnego powiązanego z portem 80.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="3f1c9-172">Jeśli to konieczne, możesz określić port lokalny inny niż 80, na przykład 8080.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="3f1c9-173">Jednak gdy ten port jest używany, niektóre linki w interfejsie użytkownika sieci Web mogą nie działać.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="3f1c9-174">Możesz teraz uzyskiwać dostęp do punktów końcowych DC/OS z systemu lokalnego, używając następujących adresów URL (zakładając, że port lokalny to 80):</span><span class="sxs-lookup"><span data-stu-id="3f1c9-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="3f1c9-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="3f1c9-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="3f1c9-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="3f1c9-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="3f1c9-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="3f1c9-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="3f1c9-178">Podobnie za pomocą tego tunelu możesz uzyskiwać dostęp do interfejsów API REST dla poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="3f1c9-179">Tunel Swarm</span><span class="sxs-lookup"><span data-stu-id="3f1c9-179">Swarm tunnel</span></span>
<span data-ttu-id="3f1c9-180">Aby otworzyć tunel do punktu końcowego Swarm, uruchom polecenie podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="3f1c9-181">Upewnij się, że nie ma innego procesu lokalnego powiązanego z portem 2375.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="3f1c9-182">Jeśli na przykład demon platformy Docker jest uruchomiony lokalnie, domyślnie jest używany port 2375.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="3f1c9-183">Jeśli to konieczne, możesz określić port lokalny inny niż 2375.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="3f1c9-184">Teraz możesz uzyskać dostęp do klastra Docker Swarm za pomocą interfejsu wiersza polecenia platformy Docker w systemie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="3f1c9-185">Aby uzyskać instrukcje dotyczące instalacji, zobacz [Instalowanie platformy Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="3f1c9-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="3f1c9-186">Ustaw dla zmiennej środowiskowej DOCKER_HOST port lokalny skonfigurowany dla tunelu.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="3f1c9-187">Uruchom polecenia platformy Docker tunelowane do klastra Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="3f1c9-188">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="3f1c9-189">Tworzenie tunelu SSH w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="3f1c9-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="3f1c9-190">Istnieje wiele opcji tworzenia tuneli SSH w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="3f1c9-191">Jeśli używasz narzędzia Bash on Ubuntu on Windows lub podobnego narzędzia, możesz wykonać instrukcje dotyczące tunelowania SSH przedstawione wcześniej w tym artykule dla systemów macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="3f1c9-192">W tej sekcji opisano sposób tworzenia tunelu przy użyciu programu PuTTY w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="3f1c9-193">[Pobierz program PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) do systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="3f1c9-194">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-194">Run the application.</span></span>

3. <span data-ttu-id="3f1c9-195">Wprowadź nazwę hosta złożoną z nazwy użytkownika administratora klastra i publicznej nazwy DNS pierwszego serwera głównego w klastrze.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="3f1c9-196">**Nazwa hosta** wygląda podobnie do `azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="3f1c9-197">W polu **Port** wprowadź wartość 2200.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-197">Enter 2200 for the **Port**.</span></span>

    ![Konfiguracja programu PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="3f1c9-199">Wybierz pozycje **SSH > Uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-199">Select **SSH > Auth**.</span></span> <span data-ttu-id="3f1c9-200">Dodaj ścieżkę do pliku klucza prywatnego (format ppk) na potrzeby uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-200">Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="3f1c9-201">Możesz użyć narzędzia takiego jak [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html), aby wygenerować ten plik z klucza SSH użytego do utworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-201">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![Konfiguracja programu PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="3f1c9-203">Wybierz pozycje **SSH > Tunele** i skonfiguruj następujące przekazane porty:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-203">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="3f1c9-204">**Port źródłowy:** — użyj portu 80 w przypadku opcji DC/OS lub portu 2375 w przypadku opcji Swarm.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-204">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="3f1c9-205">**Miejsce docelowe:** — użyj wartości localhost:80 w przypadku opcji DC/OS lub wartości localhost:2375 w przypadku opcji Swarm.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-205">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="3f1c9-206">Poniższy przykład został skonfigurowany na potrzeby opcji DC/OS, ale będzie wyglądać podobnie w przypadku rozwiązania Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-206">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3f1c9-207">W przypadku tworzenia tego tunelu nie można używać portu 80.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-207">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Konfiguracja programu PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="3f1c9-209">Po zakończeniu kliknij pozycje **Sesja > Zapisz**, aby zapisać konfigurację połączenia.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-209">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="3f1c9-210">Aby nawiązać połączenie z sesją programu PuTTY, kliknij pozycję **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-210">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="3f1c9-211">Po nawiązaniu połączenia konfiguracja portów będzie dostępna w dzienniku zdarzeń programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-211">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![Dziennik zdarzeń programu PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="3f1c9-213">Po skonfigurowaniu tunelu dla koordynatora DC/OS można uzyskiwać dostęp do powiązanych punktów końcowych w następujących lokalizacjach:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-213">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="3f1c9-214">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="3f1c9-214">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="3f1c9-215">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="3f1c9-215">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="3f1c9-216">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="3f1c9-216">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="3f1c9-217">Po skonfigurowaniu tunelu dla koordynatora Docker Swarm otwórz ustawienia systemu Windows, aby skonfigurować systemową zmienną środowiskową o nazwie `DOCKER_HOST` przy użyciu wartości `:2375`.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-217">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="3f1c9-218">Następnie możesz uzyskać dostęp do klastra Swarm za pośrednictwem interfejsu wiersza polecenia platformy Docker.</span><span class="sxs-lookup"><span data-stu-id="3f1c9-218">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f1c9-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f1c9-219">Next steps</span></span>
<span data-ttu-id="3f1c9-220">Wdrażanie kontenerów i zarządzanie nimi w klastrze:</span><span class="sxs-lookup"><span data-stu-id="3f1c9-220">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="3f1c9-221">Współpraca z usługą Azure Container Service i rozwiązaniem Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3f1c9-221">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="3f1c9-222">Współpraca z usługą Azure Container Service i rozwiązaniem DC/OS</span><span class="sxs-lookup"><span data-stu-id="3f1c9-222">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="3f1c9-223">Współpraca z usługą Azure Container Service i rozwiązaniem Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="3f1c9-223">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

