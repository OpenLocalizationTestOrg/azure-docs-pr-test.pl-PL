---
title: aaaCustomize maszyny Wirtualnej systemu Linux, po pierwszym uruchomieniu komputera na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak inicjowaniem chmury toouse i Key Vault toocustomze maszyn wirtualnych systemu Linux powitania po raz pierwszy one rozruchu w systemie Azure"
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
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="f5ef5-103">Jak toocustomize maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera</span><span class="sxs-lookup"><span data-stu-id="f5ef5-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="f5ef5-104">W poprzednich instrukcji możesz przedstawiono sposób maszyny wirtualnej tooa tooSSH (VM) i ręcznie zainstalować NGINX.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="f5ef5-105">wymagane jest zwykle toocreate maszyn wirtualnych w szybki i spójny sposób jakiegoś automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="f5ef5-106">Typowe toocustomize podejście maszyny Wirtualnej po pierwszym uruchomieniu komputera jest toouse [init chmury](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="f5ef5-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5ef5-108">Utwórz plik konfiguracji init chmury</span><span class="sxs-lookup"><span data-stu-id="f5ef5-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="f5ef5-109">Utwórz maszynę Wirtualną, która używa pliku init chmury</span><span class="sxs-lookup"><span data-stu-id="f5ef5-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="f5ef5-110">Wyświetlanie działającej aplikacji Node.js po powitalne zostanie utworzona maszyna wirtualna</span><span class="sxs-lookup"><span data-stu-id="f5ef5-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="f5ef5-111">Użyj usługi Key Vault toosecurely magazyn certyfikatów</span><span class="sxs-lookup"><span data-stu-id="f5ef5-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="f5ef5-112">Automatyzacja bezpiecznego wdrażania z NGINX z inicjowaniem chmury</span><span class="sxs-lookup"><span data-stu-id="f5ef5-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f5ef5-113">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f5ef5-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f5ef5-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="f5ef5-116">Init chmury — omówienie</span><span class="sxs-lookup"><span data-stu-id="f5ef5-116">Cloud-init overview</span></span>
<span data-ttu-id="f5ef5-117">[Init chmury](https://cloudinit.readthedocs.io) jest toocustomize podejścia powszechnie używaną Maszynę wirtualną systemu Linux rozruchu dla powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="f5ef5-118">Można użyć pakietów tooinstall init chmury i zapisywać pliki, lub użytkowników tooconfigure i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="f5ef5-119">Jak init chmury jest uruchamiany podczas hello początkowego procesu rozruchu, nie istnieją żadne dodatkowe czynności lub wymagane tooapply agentów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="f5ef5-120">Init chmury działa także w dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="f5ef5-121">Na przykład nie używaj **instalacji stanie get** lub **yum zainstalować** tooinstall pakietu.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="f5ef5-122">Zamiast tego można zdefiniować listę tooinstall pakietów.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="f5ef5-123">Init chmury automatycznie używa narzędzia do zarządzania natywnego pakietu hello distro hello, którą wybierzesz.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="f5ef5-124">Możemy pracy z naszych partnerów tooget chmury inicjowania uwzględnione i Praca w obrazach hello udostępniają one tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="f5ef5-125">Witaj w poniższej tabeli przedstawiono hello bieżącej dostępności init chmury na obrazy platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="f5ef5-126">Alias</span><span class="sxs-lookup"><span data-stu-id="f5ef5-126">Alias</span></span> | <span data-ttu-id="f5ef5-127">Wydawca</span><span class="sxs-lookup"><span data-stu-id="f5ef5-127">Publisher</span></span> | <span data-ttu-id="f5ef5-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="f5ef5-128">Offer</span></span> | <span data-ttu-id="f5ef5-129">SKU</span><span class="sxs-lookup"><span data-stu-id="f5ef5-129">SKU</span></span> | <span data-ttu-id="f5ef5-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="f5ef5-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="f5ef5-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="f5ef5-131">UbuntuLTS</span></span> |<span data-ttu-id="f5ef5-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="f5ef5-132">Canonical</span></span> |<span data-ttu-id="f5ef5-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f5ef5-133">UbuntuServer</span></span> |<span data-ttu-id="f5ef5-134">16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="f5ef5-134">16.04-LTS</span></span> |<span data-ttu-id="f5ef5-135">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f5ef5-135">latest</span></span> |
| <span data-ttu-id="f5ef5-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="f5ef5-136">UbuntuLTS</span></span> |<span data-ttu-id="f5ef5-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="f5ef5-137">Canonical</span></span> |<span data-ttu-id="f5ef5-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f5ef5-138">UbuntuServer</span></span> |<span data-ttu-id="f5ef5-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="f5ef5-139">14.04.5-LTS</span></span> |<span data-ttu-id="f5ef5-140">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f5ef5-140">latest</span></span> |
| <span data-ttu-id="f5ef5-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f5ef5-141">CoreOS</span></span> |<span data-ttu-id="f5ef5-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f5ef5-142">CoreOS</span></span> |<span data-ttu-id="f5ef5-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f5ef5-143">CoreOS</span></span> |<span data-ttu-id="f5ef5-144">Stable</span><span class="sxs-lookup"><span data-stu-id="f5ef5-144">Stable</span></span> |<span data-ttu-id="f5ef5-145">najnowsza</span><span class="sxs-lookup"><span data-stu-id="f5ef5-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="f5ef5-146">Utwórz plik konfiguracji init chmury</span><span class="sxs-lookup"><span data-stu-id="f5ef5-146">Create cloud-init config file</span></span>
<span data-ttu-id="f5ef5-147">inicjowaniem chmury toosee akcji, utwórz maszynę Wirtualną, która instaluje NGINX i uruchamia prostej aplikacji Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="f5ef5-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="f5ef5-148">powitania po konfiguracji chmury init instaluje hello wymagane pakiety, utworzenie aplikacji Node.js, a następnie zainicjować i uruchomienie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="f5ef5-149">W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i Wklej powitania po konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="f5ef5-150">Na przykład utworzyć plik hello w hello powłoki chmury nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="f5ef5-151">Można użyć dowolnego edytora, którego chcesz.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-151">You can use any editor you wish.</span></span> <span data-ttu-id="f5ef5-152">Wprowadź `sensible-editor cloud-init.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="f5ef5-153">Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="f5ef5-154">Aby uzyskać więcej informacji o opcjach konfiguracji chmury init, zobacz [przykłady konfiguracji chmury init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="f5ef5-155">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f5ef5-155">Create virtual machine</span></span>
<span data-ttu-id="f5ef5-156">Przed utworzeniem maszyny Wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f5ef5-157">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAutomate* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="f5ef5-158">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f5ef5-159">Użyj hello `--custom-data` toopass parametru w pliku config init chmury.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="f5ef5-160">Podaj hello pełną ścieżkę toohello *init.txt chmury* konfiguracji w przypadku zapisania pliku hello poza istnieje katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="f5ef5-161">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="f5ef5-162">Trwa kilka minut, aż hello toobe maszyny Wirtualnej utworzone, tooinstall pakietów hello i toostart aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="f5ef5-163">Istnieją zadania w tle, które nadal toorun po hello Azure CLI zwraca toohello wiersza.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="f5ef5-164">Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="f5ef5-165">Po utworzeniu hello maszyny Wirtualnej, zwróć uwagę na powitania `publicIpAddress` wyświetlanych przez hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="f5ef5-166">Ten adres jest aplikacja Node.js hello tooaccess używane za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="f5ef5-167">tooallow web tooreach ruch maszyny Wirtualnej, otwórz port 80 z hello Internet z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="f5ef5-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="f5ef5-168">Przetestuj aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="f5ef5-168">Test web app</span></span>
<span data-ttu-id="f5ef5-169">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź *http://<publicIpAddress>*  na pasku adresu hello.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="f5ef5-170">Podaj własny publicznego adresu IP z hello maszyny Wirtualnej utworzyć procesu.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="f5ef5-171">Aplikacja Node.js jest wyświetlana tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-171">Your Node.js app is displayed as in hello following example:</span></span>

![Wyświetl uruchomione NGINX lokacji](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="f5ef5-173">Wstaw certyfikaty z magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="f5ef5-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="f5ef5-174">W tej sekcji opcjonalne przedstawiono, jak można bezpiecznie certyfikaty są przechowywane w usłudze Azure Key Vault i wstrzyknąć podczas hello wdrożenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="f5ef5-175">Zamiast przy użyciu niestandardowego obrazu, który zawiera certyfikaty hello rozszerzania programu, ten proces zapewnia, że hello najbardziej aktualne certyfikaty są wstrzykiwane tooa maszyny Wirtualnej po pierwszym uruchomieniu komputera.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="f5ef5-176">W trakcie hello certyfikatu hello nigdy nie opuszcza hello platformy Azure lub jest widoczna w skryptu, Historia wiersza polecenia lub szablonu.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="f5ef5-177">Usługa Azure Key Vault zabezpiecza kluczy kryptograficznych i kluczy tajnych, takich jak certyfikaty lub hasła.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="f5ef5-178">Key Vault ułatwia usprawnić proces zarządzania kluczami hello i umożliwia toomaintain kontrolę nad kluczami, które dostępu i szyfrowania danych.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="f5ef5-179">W tym scenariuszu przedstawiono niektóre toocreate pojęcia magazyn kluczy i użycia certyfikatu, jednak nie jest wyczerpujący Przegląd na temat toouse magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="f5ef5-180">Hello następujące kroki pokazują, jak można:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="f5ef5-181">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f5ef5-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="f5ef5-182">Generowanie lub Przekaż certyfikat toohello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="f5ef5-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="f5ef5-183">Utwórz klucz tajny z tooinject certyfikatu hello w tooa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f5ef5-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="f5ef5-184">Utwórz maszynę Wirtualną i wstrzyknąć hello certyfikatu</span><span class="sxs-lookup"><span data-stu-id="f5ef5-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="f5ef5-185">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f5ef5-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="f5ef5-186">Najpierw utwórz magazyn kluczy o [az keyvault utworzyć](/cli/azure/keyvault#create) i włącz ją do użycia podczas wdrażania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="f5ef5-187">Każdy magazyn kluczy wymaga unikatowej nazwy i powinna być małe litery.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="f5ef5-188">Zastąp *mykeyvault* w hello poniższy przykład z własną unikatową nazwę usługi Key Vault:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="f5ef5-189">Generowanie certyfikatu i przechowywania w magazynie kluczy</span><span class="sxs-lookup"><span data-stu-id="f5ef5-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="f5ef5-190">W środowisku produkcyjnym, należy zaimportować prawidłowy certyfikat podpisane przez zaufanego dostawcę z [importu certyfikatów keyvault az](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="f5ef5-191">W tym samouczku hello poniższym przykładzie pokazano, jak można wygenerować certyfikatu z podpisem własnym z [utworzenia certyfikatu keyvault az](/cli/azure/keyvault/certificate#create) używającą hello domyślne zasady certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="f5ef5-192">Przygotowywanie certyfikatów do użytku z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="f5ef5-193">certyfikat hello toouse podczas hello maszyny Wirtualnej utworzyć procesu, uzyskać identyfikator hello certyfikatu z [az keyvault wersje klucza tajnego listy-](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="f5ef5-194">Hello maszyna wirtualna wymaga certyfikatu hello tooinject format go podczas rozruchu, więc przekonwertować hello certyfikatu z [az wirtualna format klucz tajny](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="f5ef5-195">Poniższy przykład Hello przypisuje hello dane wyjściowe tych poleceń toovariables dla łatwość użycia w hello następne kroki:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="f5ef5-196">Tworzenie chmury init config toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="f5ef5-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="f5ef5-197">Podczas tworzenia maszyny Wirtualnej, certyfikaty i klucze są przechowywane w hello chronione */var/lib/agentawaagent/* katalogu.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="f5ef5-198">tooautomate Dodawanie hello certyfikatu toohello maszyny Wirtualnej i skonfigurowaniu NGINX, można użyć konfiguracji zaktualizowane init chmury z poprzedniego przykładu hello.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="f5ef5-199">Utwórz plik o nazwie *chmurze init-secured.txt* i Wklej powitania po konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="f5ef5-200">Ponownie Jeśli używasz hello powłoki chmury, Utwórz plik konfiguracji init chmury hello, występują, a nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="f5ef5-201">Użyj `sensible-editor cloud-init-secured.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="f5ef5-202">Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="f5ef5-203">Tworzenie bezpiecznej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f5ef5-203">Create secure VM</span></span>
<span data-ttu-id="f5ef5-204">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f5ef5-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f5ef5-205">dane certyfikatu Hello jest wprowadzona z usługi Key Vault z hello `--secrets` parametru.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="f5ef5-206">Jak w poprzednim przykładzie hello, należy także podać w konfiguracji chmury init hello z hello `--custom-data` parametru:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="f5ef5-207">Trwa kilka minut, aż hello toobe maszyny Wirtualnej utworzone, tooinstall pakietów hello i toostart aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="f5ef5-208">Istnieją zadania w tle, które nadal toorun po hello Azure CLI zwraca toohello wiersza.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="f5ef5-209">Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="f5ef5-210">Po utworzeniu hello maszyny Wirtualnej, zwróć uwagę na powitania `publicIpAddress` wyświetlanych przez hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="f5ef5-211">Ten adres jest aplikacja Node.js hello tooaccess używane za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="f5ef5-212">tooallow secure tooreach ruchu w sieci web z maszyną Wirtualną, otwórz port 443 z hello Internet z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="f5ef5-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="f5ef5-213">Przetestuj aplikację sieci web bezpiecznego</span><span class="sxs-lookup"><span data-stu-id="f5ef5-213">Test secure web app</span></span>
<span data-ttu-id="f5ef5-214">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź *https://<publicIpAddress>*  na pasku adresu hello.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="f5ef5-215">Podaj własny publicznego adresu IP z hello maszyny Wirtualnej utworzyć procesu.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="f5ef5-216">Jeśli używasz certyfikatu z podpisem własnym, zaakceptuj ostrzeżenie o zabezpieczeniach hello:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![Zaakceptuj ostrzeżenie o zabezpieczeniach przeglądarki sieci web](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="f5ef5-218">Zabezpieczonej witrynie NGINX i Node.js jak hello poniższy przykład następnie jest wyświetlana aplikacja:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![Uruchamianie zabezpieczoną witryną NGINX widoku](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="f5ef5-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5ef5-220">Next steps</span></span>
<span data-ttu-id="f5ef5-221">W tym samouczku należy skonfigurować po pierwszym uruchomieniu komputera z inicjowaniem chmury maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="f5ef5-222">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="f5ef5-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5ef5-223">Utwórz plik konfiguracji init chmury</span><span class="sxs-lookup"><span data-stu-id="f5ef5-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="f5ef5-224">Utwórz maszynę Wirtualną, która używa pliku init chmury</span><span class="sxs-lookup"><span data-stu-id="f5ef5-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="f5ef5-225">Wyświetlanie działającej aplikacji Node.js po powitalne zostanie utworzona maszyna wirtualna</span><span class="sxs-lookup"><span data-stu-id="f5ef5-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="f5ef5-226">Użyj usługi Key Vault toosecurely magazyn certyfikatów</span><span class="sxs-lookup"><span data-stu-id="f5ef5-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="f5ef5-227">Automatyzacja bezpiecznego wdrażania z NGINX z inicjowaniem chmury</span><span class="sxs-lookup"><span data-stu-id="f5ef5-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="f5ef5-228">Jak przejść dalej toolearn samouczka toohello toocreate niestandardowych obrazów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f5ef5-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f5ef5-229">Tworzenie niestandardowych obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f5ef5-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
