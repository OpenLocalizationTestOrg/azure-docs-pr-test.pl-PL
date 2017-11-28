---
title: "udział aaaFile dla klastra Azure DC/OS | Dokumentacja firmy Microsoft"
description: "Utworzy i zainstaluje klastra DC/OS tooa udziału plików w usłudze kontenera platformy Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenerów, Micro-services, Mesos, Azure, udziału plików, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a><span data-ttu-id="c3b7f-104">Utworzy i zainstaluje klaster DC/OS tooa udziału plików</span><span class="sxs-lookup"><span data-stu-id="c3b7f-104">Create and mount a file share tooa DC/OS cluster</span></span>
<span data-ttu-id="c3b7f-105">Ten samouczek zawiera szczegóły dotyczące sposobu toocreate pliku udostępnionej w programie Azure i zainstalować go na każdy agent i główny hello klastra DC/OS.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-105">This tutorial details how toocreate a file share in Azure and mount it on each agent and master of hello DC/OS cluster.</span></span> <span data-ttu-id="c3b7f-106">Konfigurowanie udziału plików umożliwia łatwiejsze tooshare plików w klastrze, takich jak konfiguracja, access, dzienników i.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-106">Setting up a file share makes it easier tooshare files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="c3b7f-107">Witaj następujące zadania są wykonywane w ramach tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="c3b7f-107">hello following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c3b7f-108">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c3b7f-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="c3b7f-109">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="c3b7f-109">Create a file share</span></span>
> * <span data-ttu-id="c3b7f-110">Instalowanie udziału hello w klastrze DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="c3b7f-110">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="c3b7f-111">Należy ACS DC/OS hello toocomplete klastra kroków w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-111">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="c3b7f-112">W razie potrzeby [w tym przykładzie skrypt](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="c3b7f-113">Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-113">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c3b7f-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c3b7f-115">Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c3b7f-115">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="c3b7f-116">Tworzenie udziału plików w systemie Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c3b7f-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="c3b7f-117">Przed rozpoczęciem korzystania z udziału plików na platformę Azure z klastrem ACS DC/OS, można utworzyć hello magazynu konta i udział plików.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-117">Before using an Azure file share with an ACS DC/OS cluster, hello storage account and file share must be created.</span></span> <span data-ttu-id="c3b7f-118">Uruchom hello następującego skryptu toocreate hello magazynu i udział plików.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-118">Run hello following script toocreate hello storage and file share.</span></span> <span data-ttu-id="c3b7f-119">Aktualizowanie parametrów hello z thoes ze środowiska.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-119">Update hello parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a><span data-ttu-id="c3b7f-120">Instalowanie udziału hello w klastrze</span><span class="sxs-lookup"><span data-stu-id="c3b7f-120">Mount hello share in your cluster</span></span>

<span data-ttu-id="c3b7f-121">Następnie hello toobe potrzeb udziału plików zainstalowanych na każdej maszynie wirtualnej w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-121">Next, hello file share needs toobe mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="c3b7f-122">To zadanie zostało wykonane przy użyciu narzędzia cifs hello/protokołu.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-122">This task is completed using hello cifs tool/protocol.</span></span> <span data-ttu-id="c3b7f-123">Operacja instalacji Hello można wykonać ręcznie na każdym węźle klastra hello lub uruchamiając skrypt względem każdego węzła w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-123">hello mount operation can be completed manually on each node of hello cluster, or by running a script against each node in hello cluster.</span></span>

<span data-ttu-id="c3b7f-124">W tym przykładzie dwa skrypty są uruchamiane, co toomount hello Azure plików udziału, a drugi toorun ten skrypt w każdym węźle klastra DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-124">In this example, two scripts are run, one toomount hello Azure file share, and a second toorun this script on each node of hello DC/OS cluster.</span></span>

<span data-ttu-id="c3b7f-125">Po pierwsze nazwę konta magazynu Azure hello i klucz dostępu są wymagane.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-125">First, hello Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="c3b7f-126">Uruchom następujące polecenia tooget hello te informacje.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-126">Run hello following commands tooget this information.</span></span> <span data-ttu-id="c3b7f-127">Zwróć uwagę, te wartości są używane w kolejnym kroku.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="c3b7f-128">Nazwa konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="c3b7f-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="c3b7f-129">Klucz dostępu do konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="c3b7f-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="c3b7f-130">Następnie Pobierz hello FQDN hello DC/OS wzorca i zapisze go w zmiennej.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-130">Next, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="c3b7f-131">Skopiuj węzeł główny toohello klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-131">Copy your private key toohello master node.</span></span> <span data-ttu-id="c3b7f-132">Ten klucz jest wymagane toocreate ssh połączenia z wszystkie węzły w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-132">This key is needed toocreate an ssh connection with all nodes in hello cluster.</span></span> <span data-ttu-id="c3b7f-133">Zaktualizuj hello nazwy użytkownika, jeśli podczas tworzenia klastra hello użyto wartości innych niż domyślne.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-133">Update hello user name if a non-default value was used when creating hello cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="c3b7f-134">Utwórz połączenie SSH z głównego hello (lub hello pierwszego serwera głównego) klastra systemu DC/OS.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-134">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="c3b7f-135">Zaktualizuj hello nazwy użytkownika, jeśli podczas tworzenia klastra hello użyto wartości innych niż domyślne.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-135">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="c3b7f-136">Utwórz plik o nazwie **cifsMount.sh**, i hello kopiowania zawartości do niego.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-136">Create a file named **cifsMount.sh**, and copy hello following contents into it.</span></span> 

<span data-ttu-id="c3b7f-137">Ten skrypt jest udział plików na platformę Azure hello toomount używane.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-137">This script is used toomount hello Azure file share.</span></span> <span data-ttu-id="c3b7f-138">Aktualizacja hello `STORAGE_ACCT_NAME` i `ACCESS_KEY` zmienne hello informacji zebranych wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-138">Update hello `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with hello information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="c3b7f-139">Utworzyć drugi plik o nazwie **getNodesRunScript.sh** i hello Kopiuj zawartość do pliku hello.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-139">Create a second file named **getNodesRunScript.sh** and copy hello following contents into hello file.</span></span> 

<span data-ttu-id="c3b7f-140">Ten skrypt umożliwia odnalezienie wszystkich węzłów klastra, a następnie wykonuje hello **cifsMount.sh** udział pliku skryptu toomount hello na każdym.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-140">This script discovers all cluster nodes, and then runs hello **cifsMount.sh** script toomount hello file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="c3b7f-141">Witaj wykonywania skryptu toomount hello Azure udziału plików na wszystkich węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-141">Run hello script toomount hello Azure file share on all nodes of hello cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="c3b7f-142">Witaj udziału plików jest teraz dostępny w `/mnt/share/dcosshare` w każdym węźle klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-142">hello file share is now accessible at `/mnt/share/dcosshare` on each node of hello cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3b7f-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3b7f-143">Next steps</span></span>

<span data-ttu-id="c3b7f-144">W tym samouczku platformy Azure udział plików został dokonano tooa dostępne klastra DC/OS, wykonując kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c3b7f-144">In this tutorial an Azure file share was made available tooa DC/OS cluster using hello steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c3b7f-145">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c3b7f-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="c3b7f-146">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="c3b7f-146">Create a file share</span></span>
> * <span data-ttu-id="c3b7f-147">Instalowanie udziału hello w klastrze DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="c3b7f-147">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="c3b7f-148">Przejdź dalej toolearn samouczka toohello temat integracji Azure kontenera rejestru z DC/OS na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c3b7f-148">Advance toohello next tutorial toolearn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3b7f-149">Równoważenie obciążenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="c3b7f-149">Load balance applications</span></span>](container-service-dcos-acr.md)