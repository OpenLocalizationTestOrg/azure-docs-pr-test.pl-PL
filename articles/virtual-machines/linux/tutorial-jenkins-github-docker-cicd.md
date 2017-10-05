---
title: "Tworzenie potoku programowanie na platformie Azure z Wpięć | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć Wpięć maszynę wirtualną na platformie Azure, która pobiera z usługi GitHub na każdym zatwierdzeniu kodu i tworzy nowy kontener Docker do uruchomienia aplikacji sieci"
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
ms.openlocfilehash: d9849b5e061dd7f2ae0744a3522dc2eb1fb37035
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="a5efd-103">Tworzenie infrastruktury programowanie na maszynie Wirtualnej systemu Linux na platformie Azure z Wpięć, GitHub i Docker</span><span class="sxs-lookup"><span data-stu-id="a5efd-103">How to create a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="a5efd-104">Aby zautomatyzować fazy kompilacji i testowania projektowanie aplikacji, można użyć ciągłej integracji i wdrażania (CI/CD) potoku.</span><span class="sxs-lookup"><span data-stu-id="a5efd-104">To automate the build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="a5efd-105">W tym samouczku, możesz utworzyć potok CI/CD na maszynie Wirtualnej platformy Azure w tym jak:</span><span class="sxs-lookup"><span data-stu-id="a5efd-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5efd-106">Tworzenie maszyny Wirtualnej z Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="a5efd-107">Instalowanie i konfigurowanie Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="a5efd-108">Utwórz integrację elementu webhook GitHub i Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="a5efd-109">Tworzenie i zatwierdza wyzwalacza Wpięć Tworzenie zadania z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="a5efd-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="a5efd-110">Tworzenie obrazu Docker dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a5efd-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="a5efd-111">Sprawdź, czy zatwierdzenia GitHub Tworzenie nowego obrazu Docker i aktualizacje uruchamiania aplikacji</span><span class="sxs-lookup"><span data-stu-id="a5efd-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a5efd-112">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a5efd-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a5efd-113">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="a5efd-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="a5efd-114">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a5efd-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="a5efd-115">Utwórz wystąpienie Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-115">Create Jenkins instance</span></span>
<span data-ttu-id="a5efd-116">W poprzednich samouczek dotyczący [sposobu dostosowywania maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md), wiesz, jak można zautomatyzować dostosowania maszyny Wirtualnej z inicjowaniem chmury.</span><span class="sxs-lookup"><span data-stu-id="a5efd-116">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="a5efd-117">W tym samouczku używany jest plik init chmury do zainstalowania Wpięć i Docker na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5efd-117">This tutorial uses a cloud-init file to install Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="a5efd-118">W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i wklej następującą konfigurację.</span><span class="sxs-lookup"><span data-stu-id="a5efd-118">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="a5efd-119">Na przykład utworzyć plik, w powłoce chmury nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="a5efd-119">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="a5efd-120">Wprowadź `sensible-editor cloud-init-jenkins.txt` do tworzenia pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="a5efd-120">Enter `sensible-editor cloud-init-jenkins.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="a5efd-121">Upewnij się, że poprawnie skopiować pliku całego init chmury szczególnie pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="a5efd-121">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="a5efd-122">Przed utworzeniem maszyny Wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a5efd-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a5efd-123">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupJenkins* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="a5efd-123">The following example creates a resource group named *myResourceGroupJenkins* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="a5efd-124">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a5efd-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a5efd-125">Użyj `--custom-data` parametr do przekazania w pliku config init chmury.</span><span class="sxs-lookup"><span data-stu-id="a5efd-125">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="a5efd-126">Podaj pełną ścieżkę do *chmurze init-jenkins.txt* po zapisaniu pliku poza istnieje katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="a5efd-126">Provide the full path to *cloud-init-jenkins.txt* if you saved the file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="a5efd-127">Trwa kilka minut dla maszyny Wirtualnej można tworzyć i konfigurować.</span><span class="sxs-lookup"><span data-stu-id="a5efd-127">It takes a few minutes for the VM to be created and configured.</span></span>

<span data-ttu-id="a5efd-128">Aby zezwolić na ruch sieci web do maszyny Wirtualnej, użyj [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) otwierania portu *8080* Wpięć ruchu i portu *1337* aplikacji Node.js, który służy do uruchamiania przykładową aplikację:</span><span class="sxs-lookup"><span data-stu-id="a5efd-128">To allow web traffic to reach your VM, use [az vm open-port](/cli/azure/vm#open-port) to open port *8080* for Jenkins traffic and port *1337* for the Node.js app that is used to run a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="a5efd-129">Skonfiguruj Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-129">Configure Jenkins</span></span>
<span data-ttu-id="a5efd-130">Aby uzyskać dostęp do Twojego wystąpienia Wpięć, uzyskać publicznego adresu IP maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="a5efd-130">To access your Jenkins instance, obtain the public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="a5efd-131">Ze względów bezpieczeństwa musisz wprowadzić hasło administratora początkowej, która jest przechowywana w pliku tekstowego na maszynie Wirtualnej, aby rozpocząć instalację Wpięć.</span><span class="sxs-lookup"><span data-stu-id="a5efd-131">For security purposes, you need to enter the initial admin password that is stored in a text file on your VM to start the Jenkins install.</span></span> <span data-ttu-id="a5efd-132">Użyj publicznego adresu IP uzyskanych w poprzednim kroku, aby SSH do maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="a5efd-132">Use the public IP address obtained in the previous step to SSH to your VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="a5efd-133">Widok `initialAdminPassword` Twojego Wpięć zainstalować i skopiuj go:</span><span class="sxs-lookup"><span data-stu-id="a5efd-133">View the `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="a5efd-134">Jeśli plik nie jest jeszcze dostępna, poczekaj jeszcze kilka minut init chmury do ukończenia instalacji Wpięć i Docker.</span><span class="sxs-lookup"><span data-stu-id="a5efd-134">If the file isn't available yet, wait a couple more minutes for cloud-init to complete the Jenkins and Docker install.</span></span>

<span data-ttu-id="a5efd-135">Teraz Otwórz przeglądarkę sieci web i przejdź do `http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="a5efd-135">Now open a web browser and go to `http://<publicIps>:8080`.</span></span> <span data-ttu-id="a5efd-136">Ukończenie początkowej konfiguracji Wpięć w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a5efd-136">Complete the initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="a5efd-137">Wprowadź *initialAdminPassword* uzyskany z maszyny Wirtualnej w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a5efd-137">Enter the *initialAdminPassword* obtained from the VM in the previous step.</span></span>
- <span data-ttu-id="a5efd-138">Kliknij przycisk **Wybierz wtyczki do zainstalowania**</span><span class="sxs-lookup"><span data-stu-id="a5efd-138">Click **Select plugins to install**</span></span>
- <span data-ttu-id="a5efd-139">Wyszukaj *GitHub* w polu tekstowym u góry wybierz *wtyczki GitHub*, następnie kliknij przycisk **instalacji**</span><span class="sxs-lookup"><span data-stu-id="a5efd-139">Search for *GitHub* in the text box across the top, select the *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="a5efd-140">Aby utworzyć konto użytkownika Wpięć, wypełnij formularz zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="a5efd-140">To create a Jenkins user account, fill out the form as desired.</span></span> <span data-ttu-id="a5efd-141">Z punktu widzenia zabezpieczeń należy utworzyć ten pierwszy użytkownik Wpięć zamiast kontynuowanie jako domyślnego konta administratora.</span><span class="sxs-lookup"><span data-stu-id="a5efd-141">From a security perspective, you should create this first Jenkins user rather than continuing as the default admin account.</span></span>
- <span data-ttu-id="a5efd-142">Gdy skończysz, kliknij przycisk **Rozpoczynanie korzystania z Wpięć**</span><span class="sxs-lookup"><span data-stu-id="a5efd-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="a5efd-143">Utwórz element webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="a5efd-143">Create GitHub webhook</span></span>
<span data-ttu-id="a5efd-144">Aby skonfigurować integrację z usługi GitHub, otwórz [Node.js Hello World Przykładowa aplikacja](https://github.com/Azure-Samples/nodejs-docs-hello-world) z repozytorium przykładów dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a5efd-144">To configure the integration with GitHub, open the [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from the Azure samples repo.</span></span> <span data-ttu-id="a5efd-145">Aby rozwidlania repozytorium na koncie usługi GitHub, kliknij przycisk **rozwidlenia** przycisk w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="a5efd-145">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

<span data-ttu-id="a5efd-146">Tworzenie elementu webhook wewnątrz rozwidlenia, utworzone:</span><span class="sxs-lookup"><span data-stu-id="a5efd-146">Create a webhook inside the fork you created:</span></span>

- <span data-ttu-id="a5efd-147">Kliknij przycisk **ustawienia**, a następnie wybierz pozycję **integracji i usługi** po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a5efd-147">Click **Settings**, then select **Integrations & services** on the left-hand side.</span></span>
- <span data-ttu-id="a5efd-148">Kliknij przycisk **dodawania usługi**, wprowadź *Wpięć* w polu filtru.</span><span class="sxs-lookup"><span data-stu-id="a5efd-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="a5efd-149">Wybierz *Wpięć (GitHub wtyczki)*</span><span class="sxs-lookup"><span data-stu-id="a5efd-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="a5efd-150">Aby uzyskać **Wpięć utworzenie punktu zaczepienia adresu URL**, wprowadź `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="a5efd-150">For the **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="a5efd-151">Upewnij się, że możesz wpisać kreskę końcową /</span><span class="sxs-lookup"><span data-stu-id="a5efd-151">Make sure you include the trailing /</span></span>
- <span data-ttu-id="a5efd-152">Kliknij przycisk **dodawania usługi**</span><span class="sxs-lookup"><span data-stu-id="a5efd-152">Click **Add service**</span></span>

![Dodaj element webhook GitHub do Twojego repozytorium rozwidlonych](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="a5efd-154">Utwórz zadanie Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-154">Create Jenkins job</span></span>
<span data-ttu-id="a5efd-155">Aby Wpięć odpowiadanie na zdarzenia w usłudze GitHub takich jak zatwierdzania kodu, Utwórz zadanie Wpięć.</span><span class="sxs-lookup"><span data-stu-id="a5efd-155">To have Jenkins respond to an event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="a5efd-156">W witrynie sieci Web Wpięć kliknij **tworzenie nowych zadań** na stronie głównej:</span><span class="sxs-lookup"><span data-stu-id="a5efd-156">In your Jenkins website, click **Create new jobs** from the home page:</span></span>

- <span data-ttu-id="a5efd-157">Wprowadź *HelloWorld* jako nazwa zadania.</span><span class="sxs-lookup"><span data-stu-id="a5efd-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="a5efd-158">Wybierz **stylu projektu**, a następnie wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5efd-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="a5efd-159">W obszarze **ogólne** zaznacz **GitHub** projektu i wprowadź adres URL repozytorium rozwidlonych, takich jak *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="a5efd-159">Under the **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="a5efd-160">W obszarze **źródła zarządzania kodem** zaznacz **Git**, wprowadź Twojego repozytorium rozwidlonych *.git* adres URL, takie jak *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="a5efd-160">Under the **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="a5efd-161">W obszarze **kompilacji wyzwalaczy** zaznacz **wyzwalacza haku GitHub dla sondowania GITscm**.</span><span class="sxs-lookup"><span data-stu-id="a5efd-161">Under the **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="a5efd-162">W obszarze **kompilacji** wybierz **kroku kompilacji Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a5efd-162">Under the **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="a5efd-163">Wybierz **wykonywania powłoki**, wprowadź `echo "Testing"` w oknie polecenia.</span><span class="sxs-lookup"><span data-stu-id="a5efd-163">Select **Execute shell**, then enter `echo "Testing"` in to command window.</span></span>
- <span data-ttu-id="a5efd-164">Kliknij przycisk **zapisać** w dolnej części okna zadań.</span><span class="sxs-lookup"><span data-stu-id="a5efd-164">Click **Save** at the bottom of the jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="a5efd-165">Testowanie integracji usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="a5efd-165">Test GitHub integration</span></span>
<span data-ttu-id="a5efd-166">Aby przetestować integracji GitHub z Wpięć, Zatwierdź zmiany w rozwidlenia.</span><span class="sxs-lookup"><span data-stu-id="a5efd-166">To test the GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="a5efd-167">W witrynie GitHub interfejs użytkownika sieci web, wybierz użytkownika rozwidlonych repozytorium, a następnie kliknij **index.js** pliku.</span><span class="sxs-lookup"><span data-stu-id="a5efd-167">Back in GitHub web UI, select your forked repo, and then click the **index.js** file.</span></span> <span data-ttu-id="a5efd-168">Kliknij ikonę ołówka, aby edytować ten plik, więc odczytuje wiersz 6:</span><span class="sxs-lookup"><span data-stu-id="a5efd-168">Click the pencil icon to edit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="a5efd-169">Aby zatwierdzić zmiany, kliknij przycisk **Zatwierdź zmiany** znajdujący się u dołu.</span><span class="sxs-lookup"><span data-stu-id="a5efd-169">To commit your changes, click the **Commit changes** button at the bottom.</span></span>

<span data-ttu-id="a5efd-170">W Wpięć, nowej kompilacji zaczyna się w obszarze **kompilacji historii** sekcji lewym dolnym rogu strony zadania.</span><span class="sxs-lookup"><span data-stu-id="a5efd-170">In Jenkins, a new build starts under the **Build history** section of the bottom left-hand corner of your job page.</span></span> <span data-ttu-id="a5efd-171">Kliknij łącze numerów kompilacji i wybierz **dane wyjściowe konsoli** rozmiaru po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a5efd-171">Click the build number link and select **Console output** on the left-hand size.</span></span> <span data-ttu-id="a5efd-172">Można wyświetlić kroki Wpięć przyjmuje jako kodu są pobierane z usługi GitHub i Akcja kompilacji generuje komunikat `Testing` do konsoli.</span><span class="sxs-lookup"><span data-stu-id="a5efd-172">You can view the steps Jenkins takes as your code is pulled from GitHub and the build action outputs the message `Testing` to the console.</span></span> <span data-ttu-id="a5efd-173">Zawsze, gdy zatwierdzenie jest przeprowadzane w witrynie GitHub, elementu webhook osiągnie do Wpięć i wyzwalają nowej kompilacji w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="a5efd-173">Each time a commit is made in GitHub, the webhook reaches out to Jenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="a5efd-174">Zdefiniuj obraz kompilacji Docker</span><span class="sxs-lookup"><span data-stu-id="a5efd-174">Define Docker build image</span></span>
<span data-ttu-id="a5efd-175">Aby wyświetlić aplikację Node.js oparte na systemie zatwierdzenia GitHub, umożliwia tworzenie obrazów Docker, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="a5efd-175">To see the Node.js app running based on your GitHub commits, lets build a Docker image to run the app.</span></span> <span data-ttu-id="a5efd-176">Obraz jest tworzony z plik Dockerfile, który definiuje sposób konfigurowania kontenera, który uruchamia aplikację.</span><span class="sxs-lookup"><span data-stu-id="a5efd-176">The image is built from a Dockerfile that defines how to configure the container that runs the app.</span></span> 

<span data-ttu-id="a5efd-177">Połączenie SSH maszyny Wirtualnej przejdź do katalogu roboczego Wpięć o nazwie po zadania, który został utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a5efd-177">From the SSH connection to your VM, change to the Jenkins workspace directory named after the job you created in a previous step.</span></span> <span data-ttu-id="a5efd-178">W naszym przykładzie, który miał nazwę *HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="a5efd-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="a5efd-179">Utwórz plik o w bieżącym katalogu roboczym z `sudo sensible-editor Dockerfile` i Wklej poniższą zawartość.</span><span class="sxs-lookup"><span data-stu-id="a5efd-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste the following contents.</span></span> <span data-ttu-id="a5efd-180">Upewnij się, że cały plik Dockerfile zostały skopiowane poprawnie, szczególnie pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="a5efd-180">Make sure that the whole Dockerfile is copied correctly, especially the first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="a5efd-181">Ten plik Dockerfile używa obrazu podstawowego środowiska Node.js przy użyciu Alpine Linux, port ujawnia 1337 działa aplikacja Hello World na, następnie kopiuje pliki aplikacji i inicjuje go.</span><span class="sxs-lookup"><span data-stu-id="a5efd-181">This Dockerfile uses the base Node.js image using Alpine Linux, exposes port 1337 that the Hello World app runs on, then copies the app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="a5efd-182">Tworzenie reguł kompilacji Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-182">Create Jenkins build rules</span></span>
<span data-ttu-id="a5efd-183">W poprzednim kroku możesz utworzyć podstawowe reguły kompilacji Wpięć, że dane wyjściowe komunikat do konsoli.</span><span class="sxs-lookup"><span data-stu-id="a5efd-183">In a previous step, you created a basic Jenkins build rule that output a message to the console.</span></span> <span data-ttu-id="a5efd-184">Umożliwia tworzenie kroku kompilacji, aby użyć naszych plik Dockerfile i uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="a5efd-184">Lets create the build step to use our Dockerfile and run the app.</span></span>

<span data-ttu-id="a5efd-185">Ponownie w wystąpieniu Wpięć wybierz zadanie utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="a5efd-185">Back in your Jenkins instance, select the job you created in a previous step.</span></span> <span data-ttu-id="a5efd-186">Kliknij przycisk **Konfiguruj** po lewej stronie i przewiń w dół do **kompilacji** sekcji:</span><span class="sxs-lookup"><span data-stu-id="a5efd-186">Click **Configure** on the left-hand side and scroll down to the **Build** section:</span></span>

- <span data-ttu-id="a5efd-187">Usuń istniejącą `echo "Test"` kroku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a5efd-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="a5efd-188">Kliknij czerwony krzyżyk w prawym górnym rogu istniejącego pola kroku kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a5efd-188">Click the red cross on the top right-hand corner of the existing build step box.</span></span>
- <span data-ttu-id="a5efd-189">Kliknij przycisk **kroku kompilacji Dodaj**, a następnie wybierz pozycję **wykonania powłoki**</span><span class="sxs-lookup"><span data-stu-id="a5efd-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="a5efd-190">W **polecenia** polu, wprowadź następujące polecenia Docker, a następnie wybierz **zapisać**:</span><span class="sxs-lookup"><span data-stu-id="a5efd-190">In the **Command** box, enter the following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="a5efd-191">Kroki procesu kompilacji Docker Utwórz obraz i tagu go z Wpięć numer kompilacji, dzięki czemu można utrzymać historii obrazów.</span><span class="sxs-lookup"><span data-stu-id="a5efd-191">The Docker build steps create an image and tag it with the Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="a5efd-192">Kontenerach istniejącą aplikację zatrzymana, a następnie usuwane.</span><span class="sxs-lookup"><span data-stu-id="a5efd-192">Any existing containers running the app are stopped and then removed.</span></span> <span data-ttu-id="a5efd-193">Nowy kontener jest następnie uruchamiany przy użyciu obrazu i uruchamia aplikację Node.js oparte na najnowszych zatwierdzenia w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="a5efd-193">A new container is then started using the image and runs your Node.js app based on the latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="a5efd-194">Testowanie potoku sieci</span><span class="sxs-lookup"><span data-stu-id="a5efd-194">Test your pipeline</span></span>
<span data-ttu-id="a5efd-195">Aby wyświetlić całą potoku w akcji, należy edytować *index.js* ponownie plik w Twojej rozwidlonych repozytorium GitHub i kliknij przycisk **zatwierdzić zmiany**.</span><span class="sxs-lookup"><span data-stu-id="a5efd-195">To see the whole pipeline in action, edit the *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="a5efd-196">Nowe zadanie uruchamia w Wpięć oparta na elementu webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="a5efd-196">A new job starts in Jenkins based on the webhook for GitHub.</span></span> <span data-ttu-id="a5efd-197">Trwa kilka sekund, aby utworzyć obraz Docker i uruchomić aplikację w nowym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="a5efd-197">It takes a few seconds to create the Docker image and start your app in a new container.</span></span>

<span data-ttu-id="a5efd-198">W razie potrzeby ponownie uzyskać publicznego adresu IP maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="a5efd-198">If needed, obtain the public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="a5efd-199">Otwórz przeglądarkę sieci web, a następnie wprowadź `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="a5efd-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="a5efd-200">Aplikacji Node.js jest wyświetlany i odzwierciedla najnowszej zatwierdzenia w rozwidlenia GitHub w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a5efd-200">Your Node.js app is displayed and reflects the latest commits in your GitHub fork as follows:</span></span>

![Uruchomionej aplikacji Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="a5efd-202">Teraz należy edytować innej *index.js* pliku w usłudze GitHub i zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="a5efd-202">Now make another edit to the *index.js* file in GitHub and commit the change.</span></span> <span data-ttu-id="a5efd-203">Poczekaj kilka sekund dla zadania do wykonania w Wpięć, a następnie odśwież przeglądarkę sieci web, aby wyświetlić zaktualizowaną wersję aplikacji uruchomionej w nowym kontenerze w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a5efd-203">Wait a few seconds for the job to complete in Jenkins, then refresh your web browser to see the updated version of your app running in a new container as follows:</span></span>

![Uruchomienie aplikacji Node.js po innym zatwierdzenia GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="a5efd-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5efd-205">Next steps</span></span>
<span data-ttu-id="a5efd-206">W tym samouczku należy skonfigurować GitHub do uruchomienia zadania kompilacji Wpięć na każdym zatwierdzeniu kodu, a następnie wdrożyć kontener Docker do testowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a5efd-206">In this tutorial, you configured GitHub to run a Jenkins build job on each code commit and then deploy a Docker container to test your app.</span></span> <span data-ttu-id="a5efd-207">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="a5efd-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a5efd-208">Tworzenie maszyny Wirtualnej z Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="a5efd-209">Instalowanie i konfigurowanie Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="a5efd-210">Utwórz integrację elementu webhook GitHub i Wpięć</span><span class="sxs-lookup"><span data-stu-id="a5efd-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="a5efd-211">Tworzenie i zatwierdza wyzwalacza Wpięć Tworzenie zadania z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="a5efd-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="a5efd-212">Tworzenie obrazu Docker dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a5efd-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="a5efd-213">Sprawdź, czy zatwierdzenia GitHub Tworzenie nowego obrazu Docker i aktualizacje uruchamiania aplikacji</span><span class="sxs-lookup"><span data-stu-id="a5efd-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="a5efd-214">Przejdź do następnego samouczkiem, aby dowiedzieć się więcej na temat sposobu integracji Wpięć z Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a5efd-214">Advance to the next tutorial to learn more about how to integrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a5efd-215">Wdrażanie aplikacji przy użyciu Wpięć i usługi Team Services</span><span class="sxs-lookup"><span data-stu-id="a5efd-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)