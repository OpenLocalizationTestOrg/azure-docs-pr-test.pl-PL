---
title: aaaUse hello rozszerzenia CustomScript na maszynie Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello CustomScript rozszerzenia toodeploy aplikacji na maszynach wirtualnych systemu Linux na platformie Azure utworzone przy użyciu hello klasycznego modelu wdrażania."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="187a2-103">Wdrażanie aplikacji światła przy użyciu hello rozszerzenia CustomScript Azure dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="187a2-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="187a2-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="187a2-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="187a2-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="187a2-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="187a2-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="187a2-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="187a2-107">Informacje o wdrażaniu przy użyciu modelu Resource Manager hello stosu światło, zobacz [tutaj](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="187a2-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="187a2-108">Witaj rozszerzenia CustomScript Azure firmy Microsoft dla systemu Linux udostępnia toocustomize sposób maszyn wirtualnych (VM), uruchamiając dowolny kod napisany w dowolnym języku skryptowym obsługiwane przez hello maszyny Wirtualnej (na przykład, Python i Bash).</span><span class="sxs-lookup"><span data-stu-id="187a2-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="187a2-109">Zapewnia to tooautomate bardzo elastyczny sposób maszyny toomultiple wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="187a2-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="187a2-110">Witaj rozszerzenia CustomScript można wdrożyć przy użyciu hello portalu Azure, programu Windows PowerShell lub hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="187a2-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="187a2-111">W tym artykule, które będą używane hello Azure CLI toodeploy proste tooan aplikacji światła maszyny Wirtualnej systemu Ubuntu utworzone przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="187a2-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="187a2-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="187a2-112">Prerequisites</span></span>
<span data-ttu-id="187a2-113">W tym przykładzie należy najpierw utworzyć dwie maszyny wirtualne Azure systemem Ubuntu 14.04 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="187a2-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="187a2-114">Witaj maszyny wirtualne są nazywane *maszyny wirtualnej skryptu* i *światło vm*.</span><span class="sxs-lookup"><span data-stu-id="187a2-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="187a2-115">Użyj unikatowej nazwy podczas tworzenia maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="187a2-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="187a2-116">Jeden z nich jest używana toorun hello polecenia interfejsu wiersza polecenia i jednym jest używana toodeploy hello światła aplikacji.</span><span class="sxs-lookup"><span data-stu-id="187a2-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="187a2-117">Należy również konta usługi Azure Storage i klucza tooaccess it (można uzyskać to hello portalu Azure).</span><span class="sxs-lookup"><span data-stu-id="187a2-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="187a2-118">Jeśli potrzebujesz, aby uzyskać pomoc przy tworzeniu maszyn wirtualnych systemu Linux na platformie Azure można znaleźć zbyt[tworzenia maszyny wirtualnej systemem Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="187a2-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="187a2-119">Witaj instalacji poleceniach założono, Ubuntu, ale hello instalacji można dostosować dowolne obsługiwane distro systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="187a2-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="187a2-120">Witaj maszyny Wirtualnej vm skryptu musi toohave instalowania interfejsu wiersza polecenia Azure, z tooAzure połączenia pracy.</span><span class="sxs-lookup"><span data-stu-id="187a2-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="187a2-121">Aby uzyskać pomoc na ten temat, zobacz zbyt[Instalowanie i Konfigurowanie interfejsu wiersza polecenia platformy Azure hello](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="187a2-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="187a2-122">Przekaż skryptu</span><span class="sxs-lookup"><span data-stu-id="187a2-122">Upload a script</span></span>
<span data-ttu-id="187a2-123">Firma Microsoft będzie hello rozszerzenia CustomScript toorun skrypt w systemie zdalnym stos światła hello tooinstall maszyny Wirtualnej i Utwórz stronę PHP.</span><span class="sxs-lookup"><span data-stu-id="187a2-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="187a2-124">W skrypcie hello tooaccess zamówień z dowolnego miejsca będzie przekazać jako obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="187a2-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="187a2-125">Przegląd skryptu</span><span class="sxs-lookup"><span data-stu-id="187a2-125">Script overview</span></span>
<span data-ttu-id="187a2-126">Przykładowy skrypt Hello instaluje tooUbuntu stosu światło, (w tym konfigurowania instalacji dyskretnej programu MySQL), zapisuje prostego pliku PHP i uruchamia Apache.</span><span class="sxs-lookup"><span data-stu-id="187a2-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="187a2-127">Przekaż skryptu</span><span class="sxs-lookup"><span data-stu-id="187a2-127">Upload script</span></span>
<span data-ttu-id="187a2-128">Zapisz skrypt hello jako pliku tekstowego, na przykład *install_lamp.sh*, a następnie przekaż tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="187a2-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="187a2-129">Można to zrobić łatwo z wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="187a2-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="187a2-130">Witaj poniższy przykład przekazuje hello pliku tooa kontenera magazynu o nazwie "skrypty".</span><span class="sxs-lookup"><span data-stu-id="187a2-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="187a2-131">Jeśli nie istnieje w kontenerze hello potrzebujesz toocreate go pierwszy.</span><span class="sxs-lookup"><span data-stu-id="187a2-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="187a2-132">Utwórz również pliku JSON, który opisuje, jak toodownload hello skryptu z usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="187a2-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="187a2-133">Zapisz jako *public_config.json* (zastępując "mystorage" hello nazwą konta magazynu):</span><span class="sxs-lookup"><span data-stu-id="187a2-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="187a2-134">Wdrażanie rozszerzenia hello</span><span class="sxs-lookup"><span data-stu-id="187a2-134">Deploy hello extension</span></span>
<span data-ttu-id="187a2-135">Teraz można używać hello następnego polecenia toodeploy hello rozszerzenia CustomScript Linux toohello zdalnego maszynę Wirtualną przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="187a2-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="187a2-136">Witaj poprzednie polecenie pobiera i uruchamia hello *install_lamp.sh* skrypt na powitania maszyny Wirtualnej o nazwie *maszyny wirtualnej światła*.</span><span class="sxs-lookup"><span data-stu-id="187a2-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="187a2-137">Ponieważ aplikacja hello obejmuje serwer sieci web, pamiętaj tooopen HTTP port nasłuchiwania na powitania zdalnego maszyny Wirtualnej z hello następnego polecenia.</span><span class="sxs-lookup"><span data-stu-id="187a2-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="187a2-138">Monitorowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="187a2-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="187a2-139">Możesz sprawdzić na jak hello niestandardowy skrypt będzie uruchamiany sprawdzając plik dziennika hello hello zdalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="187a2-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="187a2-140">SSH za*maszyny wirtualnej światła* i pliku dziennika hello tail z hello następnego polecenia.</span><span class="sxs-lookup"><span data-stu-id="187a2-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="187a2-141">Po uruchomieniu hello rozszerzenia CustomScript można przeglądać strony PHP toohello, utworzone informacji.</span><span class="sxs-lookup"><span data-stu-id="187a2-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="187a2-142">Strona Hello PHP, na przykład hello w tym artykule jest *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="187a2-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="187a2-143">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="187a2-143">Additional resources</span></span>
<span data-ttu-id="187a2-144">Można użyć hello toodeploy podstawowe kroki tej samej bardziej złożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="187a2-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="187a2-145">W tym przykładzie skrypt instalacji hello został zapisany jako publiczny obiektów blob w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="187a2-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="187a2-146">Opcja bardziej bezpieczna byłoby skrypt instalacji hello toostore jako bezpieczne obiektów blob z [bezpiecznego dostępu podpisu](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="187a2-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="187a2-147">Dodatkowe zasoby dla wiersza polecenia platformy Azure, Linux i hello rozszerzenia CustomScript są wyświetlane obok.</span><span class="sxs-lookup"><span data-stu-id="187a2-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="187a2-148">Automatyzowanie zadań dostosowania maszyny Wirtualnej systemu Linux za pomocą rozszerzenia CustomScript</span><span class="sxs-lookup"><span data-stu-id="187a2-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="187a2-149">Rozszerzenia Azure Linux (GitHub)</span><span class="sxs-lookup"><span data-stu-id="187a2-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)