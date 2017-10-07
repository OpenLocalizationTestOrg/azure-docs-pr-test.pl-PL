---
title: "rozwój potoku na platformie Azure z Wpięć aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak maszyny toocreate Wpięć wirtualnego w platformie Azure, że ściąga z serwisu GitHub dla każdego kodu zatwierdzić i tworzy nowy Docker toorun kontenera aplikacji"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="d779a-103">Jak toocreate infrastrukturze programowanie na maszynie Wirtualnej systemu Linux na platformie Azure z Wpięć, GitHub i Docker</span><span class="sxs-lookup"><span data-stu-id="d779a-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="d779a-104">tooautomate hello kompilacji i przetestowania etap tworzenia aplikacji, można użyć ciągłej integracji i wdrażania (CI/CD) potoku.</span><span class="sxs-lookup"><span data-stu-id="d779a-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="d779a-105">W tym samouczku, możesz utworzyć potok CI/CD na maszynie Wirtualnej platformy Azure w tym jak:</span><span class="sxs-lookup"><span data-stu-id="d779a-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d779a-106">Tworzenie maszyny Wirtualnej z Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="d779a-107">Instalowanie i konfigurowanie Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="d779a-108">Utwórz integrację elementu webhook GitHub i Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="d779a-109">Tworzenie i zatwierdza wyzwalacza Wpięć Tworzenie zadania z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="d779a-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="d779a-110">Tworzenie obrazu Docker dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="d779a-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="d779a-111">Sprawdź, czy zatwierdzenia GitHub Tworzenie nowego obrazu Docker i aktualizacje uruchamiania aplikacji</span><span class="sxs-lookup"><span data-stu-id="d779a-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d779a-112">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d779a-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d779a-113">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="d779a-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d779a-114">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d779a-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="d779a-115">Utwórz wystąpienie Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-115">Create Jenkins instance</span></span>
<span data-ttu-id="d779a-116">W poprzednim samouczek dotyczący [jak toocustomize maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md), możesz przedstawiono sposób dostosowywania maszyny Wirtualnej tooautomate z inicjowaniem chmury.</span><span class="sxs-lookup"><span data-stu-id="d779a-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="d779a-117">Ten samouczek używa init chmury pliku tooinstall Wpięć i Docker na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d779a-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="d779a-118">W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i Wklej powitania po konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d779a-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="d779a-119">Na przykład utworzyć plik hello w hello powłoki chmury nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="d779a-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="d779a-120">Wprowadź `sensible-editor cloud-init-jenkins.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="d779a-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="d779a-121">Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="d779a-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

<span data-ttu-id="d779a-122">Przed utworzeniem maszyny Wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d779a-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="d779a-123">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupJenkins* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="d779a-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="d779a-124">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="d779a-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="d779a-125">Użyj hello `--custom-data` toopass parametru w pliku config init chmury.</span><span class="sxs-lookup"><span data-stu-id="d779a-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="d779a-126">Podaj pełną ścieżkę hello zbyt*chmurze init-jenkins.txt* po zapisaniu pliku hello poza istnieje katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="d779a-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="d779a-127">Trwa kilka minut, aż hello wirtualna toobe utworzone i skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="d779a-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="d779a-128">tooallow web tooreach ruch maszyny Wirtualnej, użyj [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) portu tooopen *8080* Wpięć ruchu i portu *1337* hello aplikacji Node.js, który jest używany toorun przykładową aplikację:</span><span class="sxs-lookup"><span data-stu-id="d779a-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="d779a-129">Skonfiguruj Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-129">Configure Jenkins</span></span>
<span data-ttu-id="d779a-130">tooaccess Twojego Wpięć wystąpienia, Uzyskaj hello publicznego adresu IP maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="d779a-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="d779a-131">Ze względów bezpieczeństwa należy tooenter hello początkowej administratora hasła, które są przechowywane w pliku tekstowym na Wpięć zainstalować powitalne toostart Twojej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d779a-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="d779a-132">Użyj hello uzyskane w hello poprzedniego kroku tooSSH tooyour maszyny Wirtualnej publiczny adres IP:</span><span class="sxs-lookup"><span data-stu-id="d779a-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="d779a-133">Widok hello `initialAdminPassword` Twojego Wpięć zainstalować i skopiuj go:</span><span class="sxs-lookup"><span data-stu-id="d779a-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="d779a-134">Jeśli plik hello nie jest jeszcze dostępny, zaczekaj kilka minut dla chmury init toocomplete hello Wpięć i zainstaluj Docker.</span><span class="sxs-lookup"><span data-stu-id="d779a-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="d779a-135">Teraz Otwórz przeglądarkę sieci web i przejdź zbyt`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="d779a-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="d779a-136">Ukończenie początkowej konfiguracji Wpięć hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d779a-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="d779a-137">Wprowadź hello *initialAdminPassword* uzyskane z hello maszyny Wirtualnej w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="d779a-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="d779a-138">Kliknij przycisk **wybierz tooinstall wtyczek**</span><span class="sxs-lookup"><span data-stu-id="d779a-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="d779a-139">Wyszukaj *GitHub* w polu tekstowym hello hello górze wybierz hello *wtyczki GitHub*, następnie kliknij przycisk **instalacji**</span><span class="sxs-lookup"><span data-stu-id="d779a-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="d779a-140">toocreate Wpięć konta użytkownika, wypełnij formularz hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="d779a-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="d779a-141">Z punktu widzenia zabezpieczeń należy utworzyć ten pierwszy użytkownik Wpięć zamiast kontynuowanie jako hello domyślnego konta administratora.</span><span class="sxs-lookup"><span data-stu-id="d779a-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="d779a-142">Gdy skończysz, kliknij przycisk **Rozpoczynanie korzystania z Wpięć**</span><span class="sxs-lookup"><span data-stu-id="d779a-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="d779a-143">Utwórz element webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="d779a-143">Create GitHub webhook</span></span>
<span data-ttu-id="d779a-144">tooconfigure hello Integracja z usługą GitHub, otwórz hello [Node.js Hello World Przykładowa aplikacja](https://github.com/Azure-Samples/nodejs-docs-hello-world) z hello repozytorium przykładów dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d779a-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="d779a-145">toofork hello repozytorium tooyour własne konto GitHub, kliknij przycisk hello **rozwidlenia** przycisk w prawym górnym rogu hello.</span><span class="sxs-lookup"><span data-stu-id="d779a-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="d779a-146">Tworzenie elementu webhook wewnątrz rozwidlenia hello, utworzone:</span><span class="sxs-lookup"><span data-stu-id="d779a-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="d779a-147">Kliknij przycisk **ustawienia**, a następnie wybierz pozycję **integracji i usługi** na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d779a-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="d779a-148">Kliknij przycisk **dodawania usługi**, wprowadź *Wpięć* w polu filtru.</span><span class="sxs-lookup"><span data-stu-id="d779a-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="d779a-149">Wybierz *Wpięć (GitHub wtyczki)*</span><span class="sxs-lookup"><span data-stu-id="d779a-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="d779a-150">Dla hello **Wpięć utworzenie punktu zaczepienia adresu URL**, wprowadź `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="d779a-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="d779a-151">Upewnij się, że możesz uwzględnić końcowe hello /</span><span class="sxs-lookup"><span data-stu-id="d779a-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="d779a-152">Kliknij przycisk **dodawania usługi**</span><span class="sxs-lookup"><span data-stu-id="d779a-152">Click **Add service**</span></span>

![Dodaj repozytorium tooyour rozwidlone elementu webhook GitHub](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="d779a-154">Utwórz zadanie Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-154">Create Jenkins job</span></span>
<span data-ttu-id="d779a-155">toohave Wpięć odpowiedź tooan zdarzeń w usłudze GitHub takich jak zatwierdzania kodu, Utwórz zadanie Wpięć.</span><span class="sxs-lookup"><span data-stu-id="d779a-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="d779a-156">W witrynie sieci Web Wpięć kliknij **tworzenie nowych zadań** ze strony głównej hello:</span><span class="sxs-lookup"><span data-stu-id="d779a-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="d779a-157">Wprowadź *HelloWorld* jako nazwa zadania.</span><span class="sxs-lookup"><span data-stu-id="d779a-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="d779a-158">Wybierz **stylu projektu**, a następnie wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="d779a-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="d779a-159">W obszarze hello **ogólne** zaznacz **GitHub** projektu i wprowadź adres URL repozytorium rozwidlonych, takich jak *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="d779a-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="d779a-160">W obszarze hello **źródła zarządzania kodem** zaznacz **Git**, wprowadź Twojego repozytorium rozwidlonych *.git* adres URL, takie jak *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="d779a-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="d779a-161">W obszarze hello **kompilacji wyzwalaczy** zaznacz **wyzwalacza haku GitHub dla sondowania GITscm**.</span><span class="sxs-lookup"><span data-stu-id="d779a-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="d779a-162">W obszarze hello **kompilacji** wybierz **kroku kompilacji Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d779a-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="d779a-163">Wybierz **wykonywania powłoki**, wprowadź `echo "Testing"` w oknie toocommand.</span><span class="sxs-lookup"><span data-stu-id="d779a-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="d779a-164">Kliknij przycisk **zapisać** u dołu okna zadań hello hello.</span><span class="sxs-lookup"><span data-stu-id="d779a-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="d779a-165">Testowanie integracji usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="d779a-165">Test GitHub integration</span></span>
<span data-ttu-id="d779a-166">Witaj tootest GitHub integracji z Wpięć, zatwierdzić zmiany w rozwidlenia.</span><span class="sxs-lookup"><span data-stu-id="d779a-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="d779a-167">W witrynie GitHub interfejs użytkownika sieci web, wybierz użytkownika rozwidlonych repozytorium, a następnie kliknij hello **index.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="d779a-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="d779a-168">Kliknij ten plik tooedit ikonę ołówka hello tak odczytuje wiersz 6:</span><span class="sxs-lookup"><span data-stu-id="d779a-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="d779a-169">toocommit zmiany, kliknij przycisk hello **Zatwierdź zmiany** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d779a-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="d779a-170">W Wpięć, nowej kompilacji zaczyna się w obszarze hello **kompilacji historii** sekcji hello lewym dolnym rogu strony zadania.</span><span class="sxs-lookup"><span data-stu-id="d779a-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="d779a-171">Kliknij łącze numer kompilacji hello i wybierz **dane wyjściowe konsoli** hello rozmiaru po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d779a-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="d779a-172">Można wyświetlić kroki hello Wpięć przyjmuje jako kodu są pobierane z usługi GitHub i hello kompilacji akcji dane wyjściowe wiadomości powitania `Testing` toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="d779a-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="d779a-173">Zawsze, gdy zatwierdzenie jest przeprowadzane w witrynie GitHub, hello webhook przez nią miejsce osiągnie limit tooJenkins i wyzwalają nowej kompilacji w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="d779a-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="d779a-174">Zdefiniuj obraz kompilacji Docker</span><span class="sxs-lookup"><span data-stu-id="d779a-174">Define Docker build image</span></span>
<span data-ttu-id="d779a-175">Aplikacja Node.js hello toosee oparte na systemie zatwierdzenia GitHub, umożliwia tworzenie aplikacji hello toorun obrazu Docker.</span><span class="sxs-lookup"><span data-stu-id="d779a-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="d779a-176">Obraz powitania składa się z plik Dockerfile, który definiuje sposób tooconfigure hello kontenera, w którym działa aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="d779a-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="d779a-177">Z tooyour połączenia SSH hello maszyny Wirtualnej należy zmienić katalogu roboczego Wpięć toohello o nazwie po zadaniu hello, utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="d779a-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="d779a-178">W naszym przykładzie, który miał nazwę *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="d779a-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="d779a-179">Utwórz plik o w bieżącym katalogu roboczym z `sudo sensible-editor Dockerfile` i Wklej powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="d779a-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="d779a-180">Upewnij się, że w tym hello jest cały plik Dockerfile skopiowane poprawnie, szczególnie hello pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="d779a-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="d779a-181">Ten plik Dockerfile używa hello podstawowy obraz Node.js przy użyciu Alpine Linux, port ujawnia 1337 aplikacji Hello World hello jest uruchamiany na, a następnie kopiuje pliki aplikacji hello i inicjuje go.</span><span class="sxs-lookup"><span data-stu-id="d779a-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="d779a-182">Tworzenie reguł kompilacji Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-182">Create Jenkins build rules</span></span>
<span data-ttu-id="d779a-183">W poprzednim kroku możesz utworzyć podstawowe reguły kompilacji Wpięć, że dane wyjściowe konsoli toohello wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d779a-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="d779a-184">Umożliwia tworzenie toouse kroku kompilacji hello naszych plik Dockerfile i uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d779a-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="d779a-185">Ponownie w wystąpieniu Wpięć wybierz zadanie hello, utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="d779a-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="d779a-186">Kliknij przycisk **Konfiguruj** na powitania po lewej stronie i przewiń w dół toohello **kompilacji** sekcji:</span><span class="sxs-lookup"><span data-stu-id="d779a-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="d779a-187">Usuń istniejącą `echo "Test"` kroku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d779a-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="d779a-188">Kliknij przycisk hello red cross na powitania prawym górnym rogu hello istniejącego pola kroku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d779a-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="d779a-189">Kliknij przycisk **kroku kompilacji Dodaj**, a następnie wybierz pozycję **wykonania powłoki**</span><span class="sxs-lookup"><span data-stu-id="d779a-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="d779a-190">W hello **polecenia** polu, wprowadź następujące polecenia Docker hello, a następnie wybierz **zapisać**:</span><span class="sxs-lookup"><span data-stu-id="d779a-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="d779a-191">kroki procesu kompilacji Docker Hello Tworzenie obrazu i tagu za pomocą hello Wpięć numer kompilacji, więc można zachowują historię obrazów.</span><span class="sxs-lookup"><span data-stu-id="d779a-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="d779a-192">Kontenerach istniejących uruchamiania aplikacji hello są zatrzymane i następnie usuwane.</span><span class="sxs-lookup"><span data-stu-id="d779a-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="d779a-193">Nowy kontener jest uruchomiony przy użyciu obrazu hello i uruchamia aplikację Node.js oparte na najnowszej zatwierdzeń hello w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d779a-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="d779a-194">Testowanie potoku sieci</span><span class="sxs-lookup"><span data-stu-id="d779a-194">Test your pipeline</span></span>
<span data-ttu-id="d779a-195">toosee hello całego procesu akcji, Edytuj hello *index.js* ponownie plik w Twojej rozwidlonych repozytorium GitHub i kliknij przycisk **zatwierdzić zmiany**.</span><span class="sxs-lookup"><span data-stu-id="d779a-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="d779a-196">Nowe zadanie uruchamia w Wpięć oparta na powitania webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="d779a-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="d779a-197">On zajmuje kilka sekund toocreate hello Docker obrazu i uruchomić aplikację w nowym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="d779a-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="d779a-198">W razie potrzeby ponownie uzyskać hello publicznego adresu IP maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="d779a-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="d779a-199">Otwórz przeglądarkę sieci web, a następnie wprowadź `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="d779a-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="d779a-200">Aplikacji Node.js jest wyświetlany i odzwierciedla hello najnowsze zatwierdzenia w rozwidlenia GitHub w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d779a-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Uruchomionej aplikacji Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="d779a-202">Teraz należy innego toohello edycji *index.js* plików w przypadku zmiany hello GitHub i zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="d779a-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="d779a-203">Zaczekaj kilka sekund na powitania toocomplete zadania w Wpięć, a następnie Odśwież wersji hello zaktualizowane toosee przeglądarki sieci web programu aplikacji uruchomionej w nowym kontenerze w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d779a-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Uruchomienie aplikacji Node.js po innym zatwierdzenia GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="d779a-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d779a-205">Next steps</span></span>
<span data-ttu-id="d779a-206">W tym samouczku skonfigurowane toorun GitHub zadania kompilacji Wpięć na każdym zatwierdzeniu kodu, a następnie wdrożyć tootest kontenera Docker aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d779a-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="d779a-207">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="d779a-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d779a-208">Tworzenie maszyny Wirtualnej z Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="d779a-209">Instalowanie i konfigurowanie Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="d779a-210">Utwórz integrację elementu webhook GitHub i Wpięć</span><span class="sxs-lookup"><span data-stu-id="d779a-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="d779a-211">Tworzenie i zatwierdza wyzwalacza Wpięć Tworzenie zadania z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="d779a-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="d779a-212">Tworzenie obrazu Docker dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="d779a-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="d779a-213">Sprawdź, czy zatwierdzenia GitHub Tworzenie nowego obrazu Docker i aktualizacje uruchamiania aplikacji</span><span class="sxs-lookup"><span data-stu-id="d779a-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="d779a-214">Więcej informacji na temat przejść dalej toolearn samouczka toohello toointegrate Wpięć z Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="d779a-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d779a-215">Wdrażanie aplikacji przy użyciu Wpięć i usługi Team Services</span><span class="sxs-lookup"><span data-stu-id="d779a-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)