---
title: "aaaSecure certyfikaty serwera sieci web przy użyciu protokołu SSL na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak certyfikaty serwera sieci web NGINX hello toosecure przy użyciu protokołu SSL na maszynie Wirtualnej systemu Linux na platformie Azure"
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="9d5d9-103">Zabezpieczenia serwera sieci web z certyfikatów SSL na maszynie wirtualnej systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9d5d9-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="9d5d9-104">serwery sieci web toosecure, certyfikat później SSL (Secure Sockets) mogą być używane tooencrypt ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="9d5d9-105">Te certyfikaty SSL mogą być przechowywane w usłudze Azure Key Vault i umożliwia bezpieczne wdrażanie certyfikatów tooLinux o maszynach wirtualnych (VM) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="9d5d9-106">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d5d9-107">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9d5d9-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="9d5d9-108">Generowanie lub Przekaż certyfikat toohello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="9d5d9-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="9d5d9-109">Utwórz maszynę Wirtualną i zainstaluj serwer sieci web NGINX hello</span><span class="sxs-lookup"><span data-stu-id="9d5d9-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="9d5d9-110">Wstaw hello certyfikatu do hello maszyny Wirtualnej i skonfigurować NGINX wraz z powiązaniem SSL</span><span class="sxs-lookup"><span data-stu-id="9d5d9-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9d5d9-111">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9d5d9-112">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9d5d9-113">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9d5d9-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="9d5d9-114">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9d5d9-114">Overview</span></span>
<span data-ttu-id="9d5d9-115">Usługa Azure Key Vault zabezpiecza kluczy kryptograficznych i kluczy tajnych takich certyfikatów lub hasła.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="9d5d9-116">Magazyn kluczy pozwala uprościć proces zarządzania hello certyfikatu i umożliwia toomaintain kontrolę nad kluczami, które uzyskują dostęp do tych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="9d5d9-117">Można utworzyć certyfikatu z podpisem własnym wewnątrz usługi Key Vault, lub Przekaż istniejących, zaufanego certyfikatu, który już następującą.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="9d5d9-118">Zamiast przy użyciu niestandardowego obrazu maszyny Wirtualnej, który zawiera certyfikaty rozszerzania w, wstrzyknąć certyfikatów do uruchomionej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="9d5d9-119">Ten proces zapewnia, że certyfikaty aktualną hello są zainstalowane na serwerze sieci web podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="9d5d9-120">Jeśli możesz odnowić lub zastąpić certyfikat, nie masz również toocreate nowego niestandardowego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="9d5d9-121">Hello najnowsze certyfikaty są automatycznie dodane podczas tworzenia dodatkowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="9d5d9-122">W trakcie całego procesu hello certyfikaty hello nigdy nie pozostaw hello platformy Azure lub są widoczne w skrypcie, Historia wiersza polecenia lub szablonu.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="9d5d9-123">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9d5d9-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="9d5d9-124">Przed utworzeniem magazyn kluczy i certyfikatów, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9d5d9-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9d5d9-125">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupSecureWeb* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="9d5d9-126">Następnie należy utworzyć magazyn kluczy o [az keyvault utworzyć](/cli/azure/keyvault#create) i włącz ją do użycia podczas wdrażania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="9d5d9-127">Każdy magazyn kluczy wymaga unikatowej nazwy i powinna być małe litery.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="9d5d9-128">Zastąp  *<mykeyvault>*  w hello poniższy przykład z własną unikatową nazwę usługi Key Vault:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="9d5d9-129">Wygeneruj certyfikat i przechowywania w magazynie kluczy</span><span class="sxs-lookup"><span data-stu-id="9d5d9-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="9d5d9-130">W środowisku produkcyjnym, należy zaimportować prawidłowy certyfikat podpisane przez zaufanego dostawcę z [importu certyfikatów keyvault az](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="9d5d9-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="9d5d9-131">W tym samouczku hello poniższym przykładzie pokazano, jak można wygenerować certyfikatu z podpisem własnym z [utworzenia certyfikatu keyvault az](/cli/azure/certificate#create) używającą hello domyślne zasady certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="9d5d9-132">Przygotowanie certyfikat do użycia z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9d5d9-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="9d5d9-133">certyfikat hello toouse podczas hello maszyny Wirtualnej utworzyć procesu, uzyskać identyfikator hello certyfikatu z [az keyvault wersje klucza tajnego listy-](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="9d5d9-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="9d5d9-134">Konwertuj hello certyfikatu z [az wirtualna format klucz tajny](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="9d5d9-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="9d5d9-135">Poniższy przykład Hello przypisuje hello dane wyjściowe tych poleceń toovariables dla łatwość użycia w hello następne kroki:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="9d5d9-136">Tworzenie chmury init config toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="9d5d9-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="9d5d9-137">[Init chmury](https://cloudinit.readthedocs.io) jest toocustomize podejścia powszechnie używaną Maszynę wirtualną systemu Linux rozruchu dla powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="9d5d9-138">Można użyć pakietów tooinstall init chmury i zapisywać pliki, lub użytkowników tooconfigure i zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="9d5d9-139">Jak init chmury jest uruchamiany podczas hello początkowego procesu rozruchu, nie istnieją żadne dodatkowe czynności lub wymagane tooapply agentów konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="9d5d9-140">Podczas tworzenia maszyny Wirtualnej, certyfikaty i klucze są przechowywane w hello chronione */var/lib/agentawaagent/* katalogu.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="9d5d9-141">Dodawanie tooautomate hello toohello certyfikatów maszyny Wirtualnej i konfigurowanie serwera sieci web hello, użyj init chmury.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="9d5d9-142">W tym przykładzie mamy Instalowanie i konfigurowanie serwera sieci web NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="9d5d9-143">Można użyć hello sam przetwarzania tooinstall i skonfigurować Apache.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="9d5d9-144">Utwórz plik o nazwie *chmurze init-web-server.txt* i Wklej hello następującej konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="9d5d9-145">Tworzenie bezpiecznej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9d5d9-145">Create a secure VM</span></span>
<span data-ttu-id="9d5d9-146">Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9d5d9-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9d5d9-147">dane certyfikatu Hello jest wprowadzona z usługi Key Vault z hello `--secrets` parametru.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="9d5d9-148">Przekaż w konfiguracji chmury init hello z hello `--custom-data` parametru:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="9d5d9-149">Trwa kilka minut, aż hello toobe maszyny Wirtualnej utworzone, tooinstall pakietów hello i toostart aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="9d5d9-150">Po utworzeniu hello maszyny Wirtualnej, zwróć uwagę na powitania `publicIpAddress` wyświetlanych przez hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="9d5d9-151">Ten adres jest używany tooaccess witryny w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="9d5d9-152">tooallow secure tooreach ruchu w sieci web z maszyną Wirtualną, otwórz port 443 z hello Internet z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="9d5d9-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="9d5d9-153">Przetestuj aplikację sieci web bezpiecznego hello</span><span class="sxs-lookup"><span data-stu-id="9d5d9-153">Test hello secure web app</span></span>
<span data-ttu-id="9d5d9-154">Teraz możesz otworzyć przeglądarkę sieci web i wprowadź *https://<publicIpAddress>*  na pasku adresu hello.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="9d5d9-155">Podaj własny publicznego adresu IP z hello maszyny Wirtualnej utworzyć procesu.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="9d5d9-156">Jeśli używasz certyfikatu z podpisem własnym, zaakceptuj ostrzeżenie o zabezpieczeniach hello:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Zaakceptuj ostrzeżenie o zabezpieczeniach przeglądarki sieci web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="9d5d9-158">Następnie wyświetleniem zabezpieczonej witrynie NGINX jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Uruchamianie zabezpieczoną witryną NGINX widoku](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="9d5d9-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d5d9-160">Next steps</span></span>

<span data-ttu-id="9d5d9-161">W tym samouczku NGINX serwera sieci web jest zabezpieczony za pomocą certyfikatu SSL, przechowywane w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="9d5d9-162">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="9d5d9-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d5d9-163">Tworzenie usługi Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9d5d9-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="9d5d9-164">Generowanie lub Przekaż certyfikat toohello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="9d5d9-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="9d5d9-165">Utwórz maszynę Wirtualną i zainstaluj serwer sieci web NGINX hello</span><span class="sxs-lookup"><span data-stu-id="9d5d9-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="9d5d9-166">Wstaw hello certyfikatu do hello maszyny Wirtualnej i skonfigurować NGINX wraz z powiązaniem SSL</span><span class="sxs-lookup"><span data-stu-id="9d5d9-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="9d5d9-167">Postępuj zgodnie z tym toosee łącze wstępnie skompilowany przykłady skryptów maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d5d9-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d5d9-168">Przykłady skryptów maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="9d5d9-168">Windows virtual machine script samples</span></span>](./cli-samples.md)