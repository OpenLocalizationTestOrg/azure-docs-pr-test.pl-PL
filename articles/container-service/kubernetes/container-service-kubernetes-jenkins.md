---
title: "aaaJenkins CI/CD z Kubernetes usługi kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Sposobu tooautomate CI/CD procesu z Wpięć toodeploy i uaktualniania konteneryzowanych aplikacji na Kubernetes usługi kontenera platformy Azure"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: "Rozwiązanie docker kontenerów, Kubernetes, Azure, Wpięć"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="dff8f-104">Wpięć integracji z usługą kontenera Azure i Kubernetes</span><span class="sxs-lookup"><span data-stu-id="dff8f-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="dff8f-105">W tym samouczku będziemy przeprowadzenie tooset procesu hello zapasowej ciągłej integracji aplikacji kontenera wielu do Kubernetes usługi kontenera platformy Azure przy użyciu platformy Wpięć hello.</span><span class="sxs-lookup"><span data-stu-id="dff8f-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="dff8f-106">przepływ pracy Hello aktualizacji hello kontener obrazu w Centrum Docker i uaktualnień stanowiskami Kubernetes hello przy użyciu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="dff8f-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="dff8f-107">Wysokiego poziomu ładowania</span><span class="sxs-lookup"><span data-stu-id="dff8f-107">High level process</span></span>
<span data-ttu-id="dff8f-108">podstawowe kroki Hello szczegółowo opisane w tym artykule przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="dff8f-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="dff8f-109">Zainstaluj Kubernetes klaster usługi kontenera</span><span class="sxs-lookup"><span data-stu-id="dff8f-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="dff8f-110">Konfigurowanie Wpięć i konfigurowanie tooContainer dostępu usługi</span><span class="sxs-lookup"><span data-stu-id="dff8f-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="dff8f-111">Tworzenie przepływów pracy Wpięć</span><span class="sxs-lookup"><span data-stu-id="dff8f-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="dff8f-112">Testowanie tooend zakończenia procesu CI/CD hello</span><span class="sxs-lookup"><span data-stu-id="dff8f-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="dff8f-113">Zainstaluj klaster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="dff8f-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="dff8f-114">Wdrażanie hello Kubernetes klastra usługi kontenera platformy Azure przy użyciu hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="dff8f-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="dff8f-115">Pełną dokumentację znajduje się [tutaj](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="dff8f-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="dff8f-116">Krok 1: Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="dff8f-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="dff8f-117">Krok 2: Wdrażanie klastra hello</span><span class="sxs-lookup"><span data-stu-id="dff8f-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="dff8f-118">Witaj poniższe czynności wymagają lokalnych klucz publiczny SSH, przechowywane w folderze ~/.ssh hello.</span><span class="sxs-lookup"><span data-stu-id="dff8f-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="dff8f-119">Konfigurowanie Wpięć i konfigurowanie tooContainer dostępu usługi</span><span class="sxs-lookup"><span data-stu-id="dff8f-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="dff8f-120">Krok 1: Instalowanie Wpięć</span><span class="sxs-lookup"><span data-stu-id="dff8f-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="dff8f-121">Tworzenie maszyny Wirtualnej platformy Azure z Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="dff8f-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="dff8f-122">Ponieważ w dalszej części hello kroków będzie konieczne tooconnect toothis maszynę Wirtualną przy użyciu bash na komputerze lokalnym, a klucz publiczny zestawu hello "Typ uwierzytelniania" too'SSH "i Wklej hello klucz publiczny SSH jest przechowywany lokalnie w folderze ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="dff8f-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="dff8f-123">Ponadto pod uwagę hello 'Nazwa użytkownika', że możesz określić, ponieważ ta nazwa użytkownika będzie pulpitu nawigacyjnego Wpięć hello tooview potrzebne i łączenia toohello Wpięć maszyny Wirtualnej w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="dff8f-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="dff8f-124">Zainstaluj Wpięć za pośrednictwem tych [instrukcje](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="dff8f-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="dff8f-125">Bardziej szczegółowy samouczek jest przeznaczony na [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="dff8f-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="dff8f-126">tooview hello pulpitu nawigacyjnego Wpięć na komputerze lokalnym, zaktualizuj hello sieć platformy Azure zabezpieczeń grupy tooallow portu 8080, dodając regułę ruchu przychodzącego, który umożliwia dostęp tooport 8080.</span><span class="sxs-lookup"><span data-stu-id="dff8f-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="dff8f-127">Alternatywnie mogą instalacji przekierowania portów, uruchamiając poniższe polecenie:`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="dff8f-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="dff8f-128">Połącz przy użyciu przeglądarki hello przechodząc toohello publiczny adres IP serwera Wpięć tooyour (http:// < your_jenkins_public_ip >: 8080) i odblokować hello Wpięć, odwiedź pulpit nawigacyjny hello o hasło administratora początkowej powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="dff8f-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="dff8f-129">hasło administratora Hello są przechowywane w /var/lib/jenkins/secrets/initialAdminPassword na powitania Wpięć maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dff8f-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="dff8f-130">Tooget łatwo to hasło jest tooSSH do hello wirtualna Wpięć: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="dff8f-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="dff8f-131">Następnie uruchom: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="dff8f-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="dff8f-132">Zainstaluj Docker na maszynie Wpięć hello za pośrednictwem tych [instrukcje](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="dff8f-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="dff8f-133">Umożliwia to uruchamianie zadań Wpięć toobe polecenia Docker.</span><span class="sxs-lookup"><span data-stu-id="dff8f-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="dff8f-134">Skonfiguruj Docker uprawnienia tooallow Wpięć tooaccess hello Docker punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="dff8f-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="dff8f-135">Zainstaluj `kubectl` CLI na Wpięć.</span><span class="sxs-lookup"><span data-stu-id="dff8f-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="dff8f-136">Szczegółowe informacje są w [Instalowanie i konfigurowanie kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="dff8f-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="dff8f-137">Zadania Wpięć będzie używać toomanage "kubectl" i wdróż toohello Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="dff8f-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="dff8f-138">Krok 2: Konfigurowanie klastra Kubernetes toohello dostępu</span><span class="sxs-lookup"><span data-stu-id="dff8f-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="dff8f-139">Istnieje wiele metod tooaccomplishing hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="dff8f-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="dff8f-140">Podejście hello Użyj najłatwiej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="dff8f-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="dff8f-141">Kopiuj hello `kubectl` Wpięć komputera tak, aby zadania Wpięć mają dostęp toohello Kubernetes klastra toohello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dff8f-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="dff8f-142">W poniższych instrukcjach przyjęto, że używasz bash z innego komputera niż hello Wpięć maszyny Wirtualnej i że lokalny klucz publiczny SSH jest przechowywany w folderze ~/.ssh hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="dff8f-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="dff8f-143">Sprawdzanie poprawności z Wpięć tego hello Kubernetes klastra jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="dff8f-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="dff8f-144">toodo tego SSH do hello wirtualna Wpięć: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="dff8f-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="dff8f-145">Następnie sprawdź połączenia klastra tooyour Wpięć: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="dff8f-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="dff8f-146">Tworzenie przepływów pracy Wpięć</span><span class="sxs-lookup"><span data-stu-id="dff8f-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dff8f-147">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dff8f-147">Prerequisites</span></span>

- <span data-ttu-id="dff8f-148">Konto usługi GitHub repozytorium kodu.</span><span class="sxs-lookup"><span data-stu-id="dff8f-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="dff8f-149">Centrum konta toostore i aktualizacji obrazy usługi docker.</span><span class="sxs-lookup"><span data-stu-id="dff8f-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="dff8f-150">Konteneryzowanych aplikacja, która może być ponownie skompilowany i zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="dff8f-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="dff8f-151">Można użyć tej przykładowej aplikacji kontenera napisana Golang: https://github.com/chzbrgr71/go-web</span><span class="sxs-lookup"><span data-stu-id="dff8f-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="dff8f-152">Witaj poniższe kroki należy wykonać na koncie usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="dff8f-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="dff8f-153">Hello wolnego tooclone powyżej repozytorium, możesz, ale należy użyć własnych elementów webhook hello tooconfigure konta i Wpięć dostępu.</span><span class="sxs-lookup"><span data-stu-id="dff8f-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="dff8f-154">Krok 1: Wdrażanie początkowej v1 aplikacji</span><span class="sxs-lookup"><span data-stu-id="dff8f-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="dff8f-155">Tworzenie aplikacji hello z hello developer maszyny z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="dff8f-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="dff8f-156">Zastąp `myrepo` własnymi.</span><span class="sxs-lookup"><span data-stu-id="dff8f-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="dff8f-157">Wypchnij tooDocker obrazu koncentratora.</span><span class="sxs-lookup"><span data-stu-id="dff8f-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="dff8f-158">Wdrażanie klastra Kubernetes toohello.</span><span class="sxs-lookup"><span data-stu-id="dff8f-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="dff8f-159">Edytuj hello `go-web.yaml` pliku tooupdate Twojego obraz kontenera i repozytorium.</span><span class="sxs-lookup"><span data-stu-id="dff8f-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="dff8f-160">Krok 2: Konfigurowanie Wpięć systemu</span><span class="sxs-lookup"><span data-stu-id="dff8f-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="dff8f-161">Kliknij przycisk **Zarządzanie Wpięć** > **skonfigurować System**.</span><span class="sxs-lookup"><span data-stu-id="dff8f-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="dff8f-162">W obszarze **GitHub**, wybierz pozycję **Dodaj serwer GitHub**.</span><span class="sxs-lookup"><span data-stu-id="dff8f-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="dff8f-163">Pozostaw **adres URL interfejsu API** jako domyślny.</span><span class="sxs-lookup"><span data-stu-id="dff8f-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="dff8f-164">W obszarze **poświadczenia**, Dodaj poświadczenie Wpięć przy użyciu **tajny tekstu**.</span><span class="sxs-lookup"><span data-stu-id="dff8f-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="dff8f-165">Firma Microsoft zaleca używanie GitHub osobiste tokeny dostępu, które są konfigurowane w ustawieniach konta użytkownika usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="dff8f-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="dff8f-166">Więcej informacji na ten [tutaj.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="dff8f-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="dff8f-167">Kliknij przycisk **połączenie testowe** tooensure to jest poprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="dff8f-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="dff8f-168">W obszarze **globalnych właściwości**, dodać zmienną środowiskową `DOCKER_HUB` i podaj hasło do Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="dff8f-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="dff8f-169">(Jest to przydatne w przypadku tego pokazu, ale scenariuszu produkcyjnym wymagają bardziej bezpieczną metodą).</span><span class="sxs-lookup"><span data-stu-id="dff8f-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="dff8f-170">Zapisz.</span><span class="sxs-lookup"><span data-stu-id="dff8f-170">Save.</span></span>

![GitHub Wpięć dostępu](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="dff8f-172">Krok 3: Tworzenie przepływu pracy Wpięć hello</span><span class="sxs-lookup"><span data-stu-id="dff8f-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="dff8f-173">Utwórz element Wpięć.</span><span class="sxs-lookup"><span data-stu-id="dff8f-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="dff8f-174">Podaj nazwę (na przykład "Przejdź sieci web") i wybierz **projektu dowolne**.</span><span class="sxs-lookup"><span data-stu-id="dff8f-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="dff8f-175">Sprawdź **projektu GitHub** i podaj repozytorium GitHub tooyour adres URL hello.</span><span class="sxs-lookup"><span data-stu-id="dff8f-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="dff8f-176">W **zarządzania kodem źródłowym**, podaj adres URL repozytorium GitHub hello i poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="dff8f-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="dff8f-177">Dodaj **krok kompilacji** typu **wykonywania powłoki** i hello Użyj następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="dff8f-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="dff8f-178">Dodaj inny **krok kompilacji** typu **wykonywania powłoki** i hello Użyj następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="dff8f-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Kroki procesu kompilacji Wpięć](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="dff8f-180">Zapisz element Wpięć hello i testowania **kompilacji teraz**.</span><span class="sxs-lookup"><span data-stu-id="dff8f-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="dff8f-181">Krok 4: Łączenie element webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="dff8f-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="dff8f-182">W elemencie Wpięć hello został utworzony, kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="dff8f-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="dff8f-183">W obszarze **kompilacji wyzwalaczy**, wybierz pozycję **wyzwalacza haku GitHub dla sondowania GITScm** i **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="dff8f-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="dff8f-184">Spowoduje to automatyczne skonfigurowanie hello element webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="dff8f-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="dff8f-185">W Twojej repozytorium GitHub dla go w sieci web, kliknij przycisk **Ustawienia > elementów Webhook**.</span><span class="sxs-lookup"><span data-stu-id="dff8f-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="dff8f-186">Upewnij się, że hello webhook Wpięć, który został pomyślnie dodany adres URL.</span><span class="sxs-lookup"><span data-stu-id="dff8f-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="dff8f-187">adres URL Hello powinien kończyć się "element webhook github".</span><span class="sxs-lookup"><span data-stu-id="dff8f-187">hello URL should end in "github-webhook".</span></span>

![Konfiguracja elementu webhook Wpięć](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="dff8f-189">Testowanie tooend zakończenia procesu CI/CD hello</span><span class="sxs-lookup"><span data-stu-id="dff8f-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="dff8f-190">Zaktualizuj kod dla repozytorium hello i wypychania/synchronizacji z repozytorium GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="dff8f-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="dff8f-191">Za pomocą konsoli Wpięć hello, sprawdź hello **kompilacji historii** i zweryfikować tego hello zadanie zostało uruchomione.</span><span class="sxs-lookup"><span data-stu-id="dff8f-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="dff8f-192">Wyświetl szczegóły toosee danych wyjściowych konsoli.</span><span class="sxs-lookup"><span data-stu-id="dff8f-192">View console output toosee details.</span></span>
3. <span data-ttu-id="dff8f-193">Z Kubernetes Wyświetl szczegóły hello uaktualnić wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="dff8f-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="dff8f-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dff8f-194">Next steps</span></span>

- <span data-ttu-id="dff8f-195">Wdróż rejestru kontenera Azure i przechowywania w bezpiecznym repozytorium obrazów.</span><span class="sxs-lookup"><span data-stu-id="dff8f-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="dff8f-196">Zobacz [docs rejestru kontenera Azure](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="dff8f-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="dff8f-197">Tworzyć bardziej złożone przepływu pracy, który obejmuje side-by-side wdrożenia oraz testów automatycznych w Wpięć.</span><span class="sxs-lookup"><span data-stu-id="dff8f-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="dff8f-198">Aby uzyskać więcej informacji na temat CI/CD z Wpięć i Kubernetes, zobacz hello [blog Wpięć](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="dff8f-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
