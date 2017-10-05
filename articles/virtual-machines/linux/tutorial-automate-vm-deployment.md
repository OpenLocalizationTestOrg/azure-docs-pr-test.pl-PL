---
title: Dostosowywanie maszyny Wirtualnej systemu Linux, po pierwszym uruchomieniu komputera na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak na potrzeby chmury init i Key Vault customze maszyn wirtualnych systemu Linux rozruchu Azure po raz pierwszy"
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
ms.openlocfilehash: 6adf4e43aa80c28c6f5f8d8a071966323ba85723
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="ecd9e-103">Dostosowywanie maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera</span><span class="sxs-lookup"><span data-stu-id="ecd9e-103">How to customize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="ecd9e-104">W poprzednich samouczka przedstawiono sposób, aby SSH z maszyną wirtualną (VM) oraz ręcznie zainstalować NGINX.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-104">In a previous tutorial, you learned how to SSH to a virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="ecd9e-105">Do tworzenia maszyn wirtualnych w sposób szybki i spójny, wymagane jest zwykle jakiegoś automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-105">To create VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="ecd9e-106">Typowym podejściem dostosować Maszynę wirtualną po pierwszym uruchomieniu komputera jest użycie [init chmury](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-106">A common approach to customize a VM on first boot is to use [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="ecd9e-107">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ecd9e-108">Utwórz plik konfiguracji init chmury</span><span class="sxs-lookup"><span data-stu-id="ecd9e-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="ecd9e-109">Utwórz maszynę Wirtualną, która używa pliku init chmury</span><span class="sxs-lookup"><span data-stu-id="ecd9e-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="ecd9e-110">Wyświetlanie działającej aplikacji Node.js po utworzeniu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ecd9e-110">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="ecd9e-111">Użyj magazynu kluczy bezpiecznie przechowywać certyfikatów</span><span class="sxs-lookup"><span data-stu-id="ecd9e-111">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="ecd9e-112">Automatyzacja bezpiecznego wdrażania z NGINX z inicjowaniem chmury</span><span class="sxs-lookup"><span data-stu-id="ecd9e-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ecd9e-113">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ecd9e-114">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="ecd9e-115">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="ecd9e-116">Init chmury — omówienie</span><span class="sxs-lookup"><span data-stu-id="ecd9e-116">Cloud-init overview</span></span>
<span data-ttu-id="ecd9e-117">[Init chmury](https://cloudinit.readthedocs.io) jest powszechnie używaną podejście, aby dostosować Maszynę wirtualną systemu Linux, ponieważ jest on uruchamiany po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="ecd9e-118">Init chmury można użyć, aby zainstalować pakiety i zapisywać pliki, lub aby skonfigurować użytkowników i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-118">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="ecd9e-119">Podczas inicjowania chmury działania podczas początkowego procesu rozruchu, nie ma, nie dodatkowe kroki lub agentów wymaganych do zastosowania konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-119">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="ecd9e-120">Init chmury działa także w dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="ecd9e-121">Na przykład nie używaj **instalacji stanie get** lub **yum zainstalować** do zainstalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-121">For example, you don't use **apt-get install** or **yum install** to install a package.</span></span> <span data-ttu-id="ecd9e-122">Zamiast tego można zdefiniować listę pakietów do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-122">Instead you can define a list of packages to install.</span></span> <span data-ttu-id="ecd9e-123">Init chmury automatycznie używa narzędzia do zarządzania natywnego pakietu dla distro, którą wybierzesz.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-123">Cloud-init automatically uses the native package management tool for the distro you select.</span></span>

<span data-ttu-id="ecd9e-124">Pracujemy nad z naszych partnerów uzyskanie init chmury uwzględnione i Praca w obrazach, zapewniające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-124">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span> <span data-ttu-id="ecd9e-125">W poniższej tabeli przedstawiono bieżącej dostępności init chmury na obrazy platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-125">The following table outlines the current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="ecd9e-126">Alias</span><span class="sxs-lookup"><span data-stu-id="ecd9e-126">Alias</span></span> | <span data-ttu-id="ecd9e-127">Wydawca</span><span class="sxs-lookup"><span data-stu-id="ecd9e-127">Publisher</span></span> | <span data-ttu-id="ecd9e-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="ecd9e-128">Offer</span></span> | <span data-ttu-id="ecd9e-129">SKU</span><span class="sxs-lookup"><span data-stu-id="ecd9e-129">SKU</span></span> | <span data-ttu-id="ecd9e-130">Wersja</span><span class="sxs-lookup"><span data-stu-id="ecd9e-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="ecd9e-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="ecd9e-131">UbuntuLTS</span></span> |<span data-ttu-id="ecd9e-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="ecd9e-132">Canonical</span></span> |<span data-ttu-id="ecd9e-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="ecd9e-133">UbuntuServer</span></span> |<span data-ttu-id="ecd9e-134">16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="ecd9e-134">16.04-LTS</span></span> |<span data-ttu-id="ecd9e-135">najnowsza</span><span class="sxs-lookup"><span data-stu-id="ecd9e-135">latest</span></span> |
| <span data-ttu-id="ecd9e-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="ecd9e-136">UbuntuLTS</span></span> |<span data-ttu-id="ecd9e-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="ecd9e-137">Canonical</span></span> |<span data-ttu-id="ecd9e-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="ecd9e-138">UbuntuServer</span></span> |<span data-ttu-id="ecd9e-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="ecd9e-139">14.04.5-LTS</span></span> |<span data-ttu-id="ecd9e-140">najnowsza</span><span class="sxs-lookup"><span data-stu-id="ecd9e-140">latest</span></span> |
| <span data-ttu-id="ecd9e-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ecd9e-141">CoreOS</span></span> |<span data-ttu-id="ecd9e-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ecd9e-142">CoreOS</span></span> |<span data-ttu-id="ecd9e-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ecd9e-143">CoreOS</span></span> |<span data-ttu-id="ecd9e-144">Stable</span><span class="sxs-lookup"><span data-stu-id="ecd9e-144">Stable</span></span> |<span data-ttu-id="ecd9e-145">najnowsza</span><span class="sxs-lookup"><span data-stu-id="ecd9e-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="ecd9e-146">Utwórz plik konfiguracji init chmury</span><span class="sxs-lookup"><span data-stu-id="ecd9e-146">Create cloud-init config file</span></span>
<span data-ttu-id="ecd9e-147">Aby wyświetlić inicjowania chmury w akcji, utwórz maszynę Wirtualną, która instaluje NGINX i uruchamia prosty "Hello World" aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-147">To see cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="ecd9e-148">Następującą konfigurację chmury init instaluje wymagane pakiety, tworzy aplikacji Node.js, a następnie zainicjować i uruchamia aplikację.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-148">The following cloud-init configuration installs the required packages, creates a Node.js app, then initialize and starts the app.</span></span>

<span data-ttu-id="ecd9e-149">W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i wklej następującą konfigurację.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-149">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="ecd9e-150">Na przykład utworzyć plik, w powłoce chmury nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-150">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="ecd9e-151">Można użyć dowolnego edytora, którego chcesz.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-151">You can use any editor you wish.</span></span> <span data-ttu-id="ecd9e-152">Wprowadź `sensible-editor cloud-init.txt` do tworzenia pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-152">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="ecd9e-153">Upewnij się, że poprawnie skopiować pliku całego init chmury szczególnie pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-153">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

<span data-ttu-id="ecd9e-154">Aby uzyskać więcej informacji o opcjach konfiguracji chmury init, zobacz [przykłady konfiguracji chmury init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="ecd9e-155">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ecd9e-155">Create virtual machine</span></span>
<span data-ttu-id="ecd9e-156">Przed utworzeniem maszyny Wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ecd9e-157">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAutomate* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-157">The following example creates a resource group named *myResourceGroupAutomate* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="ecd9e-158">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ecd9e-159">Użyj `--custom-data` parametr do przekazania w pliku config init chmury.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-159">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="ecd9e-160">Podaj pełną ścieżkę do *init.txt chmury* konfiguracji, jeśli plik został zapisany poza istnieje katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-160">Provide the full path to the *cloud-init.txt* config if you saved the file outside of your present working directory.</span></span> <span data-ttu-id="ecd9e-161">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-161">The following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="ecd9e-162">Trwa kilka minut, aż do utworzenia maszyny Wirtualnej, pakietów do zainstalowania i aplikacji, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-162">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="ecd9e-163">Istnieją zadania w tle, które nadal działać po interfejsu wiersza polecenia Azure powrót do wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-163">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="ecd9e-164">Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-164">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="ecd9e-165">Po utworzeniu maszyny Wirtualnej, zanotuj `publicIpAddress` wyświetlanych przez wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-165">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="ecd9e-166">Ten adres jest używany na dostęp do aplikacji Node.js za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-166">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="ecd9e-167">Aby zezwolić na ruch w sieci web do maszyny Wirtualnej, należy otworzyć port 80 z Internetu z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="ecd9e-167">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="ecd9e-168">Przetestuj aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="ecd9e-168">Test web app</span></span>
<span data-ttu-id="ecd9e-169">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź *http://<publicIpAddress>*  na pasku adresu.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-169">Now you can open a web browser and enter *http://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="ecd9e-170">Podaj własny publicznego adresu IP z maszyny Wirtualnej utworzyć procesu.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-170">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="ecd9e-171">Aplikacja Node.js jest wyświetlana, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-171">Your Node.js app is displayed as in the following example:</span></span>

![Wyświetl uruchomione NGINX lokacji](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="ecd9e-173">Wstaw certyfikaty z magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="ecd9e-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="ecd9e-174">W tej sekcji opcjonalne przedstawiono, jak można bezpiecznie certyfikaty są przechowywane w usłudze Azure Key Vault i wstrzyknąć podczas wdrażania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during the VM deployment.</span></span> <span data-ttu-id="ecd9e-175">Zamiast przy użyciu niestandardowego obrazu, który zawiera certyfikaty rozszerzania programu, ten proces zapewnia, że najbardziej aktualne certyfikaty są wstrzykiwane do maszyny Wirtualnej po pierwszym uruchomieniu komputera.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-175">Rather than using a custom image that includes the certificates baked-in, this process ensures that the most up-to-date certificates are injected to a VM on first boot.</span></span> <span data-ttu-id="ecd9e-176">W trakcie nigdy nie opuszcza platformy Azure lub certyfikatu jest widoczna w skryptu, Historia wiersza polecenia lub szablonu.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-176">During the process, the certificate never leaves the Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="ecd9e-177">Usługa Azure Key Vault zabezpiecza kluczy kryptograficznych i kluczy tajnych, takich jak certyfikaty lub hasła.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="ecd9e-178">Key Vault ułatwia uprościć proces zarządzania kluczami i pozwala zachować kontrolę nad kluczami, które dostępu i szyfrowania danych.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-178">Key Vault helps streamline the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="ecd9e-179">W tym scenariuszu niektóre pojęcia Key Vault do utworzenia i użycia certyfikatu, jednak nie jest wyczerpujący Przegląd sposobu użycia usługi Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-179">This scenario introduces some Key Vault concepts to create and use a certificate, though is not an exhaustive overview on how to use Key Vault.</span></span>

<span data-ttu-id="ecd9e-180">W poniższej procedurze pokazano, jak można:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-180">The following steps show how you can:</span></span>

- <span data-ttu-id="ecd9e-181">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ecd9e-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="ecd9e-182">Generowanie lub Przekaż certyfikat do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="ecd9e-182">Generate or upload a certificate to the Key Vault</span></span>
- <span data-ttu-id="ecd9e-183">Utwórz klucz tajny z certyfikatów do dodania w z maszyną wirtualną</span><span class="sxs-lookup"><span data-stu-id="ecd9e-183">Create a secret from the certificate to inject in to a VM</span></span>
- <span data-ttu-id="ecd9e-184">Utwórz maszynę Wirtualną i wprowadzić certyfikat</span><span class="sxs-lookup"><span data-stu-id="ecd9e-184">Create a VM and inject the certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="ecd9e-185">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ecd9e-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="ecd9e-186">Najpierw utwórz magazyn kluczy o [az keyvault utworzyć](/cli/azure/keyvault#create) i włącz ją do użycia podczas wdrażania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="ecd9e-187">Każdy magazyn kluczy wymaga unikatowej nazwy i powinna być małe litery.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="ecd9e-188">Zastąp *mykeyvault* w poniższym przykładzie z własną unikatową nazwę usługi Key Vault:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-188">Replace *mykeyvault* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="ecd9e-189">Generowanie certyfikatu i przechowywania w magazynie kluczy</span><span class="sxs-lookup"><span data-stu-id="ecd9e-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="ecd9e-190">W środowisku produkcyjnym, należy zaimportować prawidłowy certyfikat podpisane przez zaufanego dostawcę z [importu certyfikatów keyvault az](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="ecd9e-191">W tym samouczku, w poniższym przykładzie pokazano, jak można wygenerować certyfikatu z podpisem własnym z [utworzenia certyfikatu keyvault az](/cli/azure/keyvault/certificate#create) używającą domyślne zasady certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-191">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="ecd9e-192">Przygotowywanie certyfikatów do użytku z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="ecd9e-193">Do używania certyfikatu podczas maszyny Wirtualnej utworzyć procesu, Uzyskaj identyfikator certyfikatu z [az keyvault wersje klucza tajnego listy-](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-193">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="ecd9e-194">Maszyna wirtualna wymaga certyfikatu w określonym formacie do wprowadzenia jej podczas rozruchu, więc konwertowanie certyfikatu z [az wirtualna format klucz tajny](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-194">The VM needs the certificate in a certain format to inject it on boot, so convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="ecd9e-195">Poniższy przykład przypisuje dane wyjściowe tych poleceń zmienne łatwość użycia w następnych krokach:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-195">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="ecd9e-196">Tworzenie konfiguracji chmury init do zabezpieczania NGINX</span><span class="sxs-lookup"><span data-stu-id="ecd9e-196">Create cloud-init config to secure NGINX</span></span>
<span data-ttu-id="ecd9e-197">Podczas tworzenia maszyny Wirtualnej, certyfikaty i klucze są przechowywane w chronionej */var/lib/agentawaagent/* katalogu.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-197">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="ecd9e-198">Aby zautomatyzować Dodawanie certyfikatu do maszyny Wirtualnej i konfigurowanie NGINX, można użyć konfiguracji zaktualizowane init chmury z poprzedniego przykładu.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-198">To automate adding the certificate to the VM and configuring NGINX, you can use an updated cloud-init config from the previous example.</span></span>

<span data-ttu-id="ecd9e-199">Utwórz plik o nazwie *chmurze init-secured.txt* i wklej następującą konfigurację.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-199">Create a file named *cloud-init-secured.txt* and paste the following configuration.</span></span> <span data-ttu-id="ecd9e-200">Ponownie korzystając z powłoki chmury, Utwórz plik konfiguracji init chmury, występują, a nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-200">Again, if you use the Cloud Shell, create the cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="ecd9e-201">Użyj `sensible-editor cloud-init-secured.txt` do tworzenia pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-201">Use `sensible-editor cloud-init-secured.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="ecd9e-202">Upewnij się, że poprawnie skopiować pliku całego init chmury szczególnie pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-202">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-secure-vm"></a><span data-ttu-id="ecd9e-203">Tworzenie bezpiecznej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ecd9e-203">Create secure VM</span></span>
<span data-ttu-id="ecd9e-204">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ecd9e-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ecd9e-205">Dane certyfikatu jest wprowadzonym z magazynu kluczy o `--secrets` parametru.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-205">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="ecd9e-206">Co w poprzednim przykładzie, możesz również przekazać w konfiguracji chmury init z `--custom-data` parametru:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-206">As in the previous example, you also pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="ecd9e-207">Trwa kilka minut, aż do utworzenia maszyny Wirtualnej, pakietów do zainstalowania i aplikacji, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-207">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="ecd9e-208">Istnieją zadania w tle, które nadal działać po interfejsu wiersza polecenia Azure powrót do wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-208">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="ecd9e-209">Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-209">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="ecd9e-210">Po utworzeniu maszyny Wirtualnej, zanotuj `publicIpAddress` wyświetlanych przez wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-210">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="ecd9e-211">Ten adres jest używany na dostęp do aplikacji Node.js za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-211">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="ecd9e-212">Aby zezwolić na ruch bezpieczną internetową nawiązać połączenie z maszyną Wirtualną, otwórz port 443 z Internetu z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="ecd9e-212">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="ecd9e-213">Przetestuj aplikację sieci web bezpiecznego</span><span class="sxs-lookup"><span data-stu-id="ecd9e-213">Test secure web app</span></span>
<span data-ttu-id="ecd9e-214">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź *https://<publicIpAddress>*  na pasku adresu.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-214">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="ecd9e-215">Podaj własny publicznego adresu IP z maszyny Wirtualnej utworzyć procesu.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-215">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="ecd9e-216">Jeśli używasz certyfikatu z podpisem własnym, zaakceptuj ostrzeżenie o zabezpieczeniach:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-216">Accept the security warning if you used a self-signed certificate:</span></span>

![Zaakceptuj ostrzeżenie o zabezpieczeniach przeglądarki sieci web](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="ecd9e-218">Zabezpieczonej witrynie NGINX i Node.js aplikacji zostaną wyświetlone jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-218">Your secured NGINX site and Node.js app is then displayed as in the following example:</span></span>

![Uruchamianie zabezpieczoną witryną NGINX widoku](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="ecd9e-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ecd9e-220">Next steps</span></span>
<span data-ttu-id="ecd9e-221">W tym samouczku należy skonfigurować po pierwszym uruchomieniu komputera z inicjowaniem chmury maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="ecd9e-222">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="ecd9e-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ecd9e-223">Utwórz plik konfiguracji init chmury</span><span class="sxs-lookup"><span data-stu-id="ecd9e-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="ecd9e-224">Utwórz maszynę Wirtualną, która używa pliku init chmury</span><span class="sxs-lookup"><span data-stu-id="ecd9e-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="ecd9e-225">Wyświetlanie działającej aplikacji Node.js po utworzeniu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ecd9e-225">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="ecd9e-226">Użyj magazynu kluczy bezpiecznie przechowywać certyfikatów</span><span class="sxs-lookup"><span data-stu-id="ecd9e-226">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="ecd9e-227">Automatyzacja bezpiecznego wdrażania z NGINX z inicjowaniem chmury</span><span class="sxs-lookup"><span data-stu-id="ecd9e-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="ecd9e-228">Przejdź do samouczka dalej informacje na temat tworzenia niestandardowych obrazów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ecd9e-228">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ecd9e-229">Tworzenie niestandardowych obrazów maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="ecd9e-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
