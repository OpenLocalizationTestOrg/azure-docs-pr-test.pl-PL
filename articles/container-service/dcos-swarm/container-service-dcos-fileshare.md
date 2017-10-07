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
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>Utworzy i zainstaluje klaster DC/OS tooa udziału plików
Ten samouczek zawiera szczegóły dotyczące sposobu toocreate pliku udostępnionej w programie Azure i zainstalować go na każdy agent i główny hello klastra DC/OS. Konfigurowanie udziału plików umożliwia łatwiejsze tooshare plików w klastrze, takich jak konfiguracja, access, dzienników i. Witaj następujące zadania są wykonywane w ramach tego samouczka:

> [!div class="checklist"]
> * Tworzenie konta usługi Azure Storage
> * Tworzenie udziału plików
> * Instalowanie udziału hello w klastrze DC/OS hello

Należy ACS DC/OS hello toocomplete klastra kroków w tym samouczku. W razie potrzeby [w tym przykładzie skrypt](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) można utworzyć.

Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Tworzenie udziału plików w systemie Microsoft Azure

Przed rozpoczęciem korzystania z udziału plików na platformę Azure z klastrem ACS DC/OS, można utworzyć hello magazynu konta i udział plików. Uruchom hello następującego skryptu toocreate hello magazynu i udział plików. Aktualizowanie parametrów hello z thoes ze środowiska.

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

## <a name="mount-hello-share-in-your-cluster"></a>Instalowanie udziału hello w klastrze

Następnie hello toobe potrzeb udziału plików zainstalowanych na każdej maszynie wirtualnej w klastrze. To zadanie zostało wykonane przy użyciu narzędzia cifs hello/protokołu. Operacja instalacji Hello można wykonać ręcznie na każdym węźle klastra hello lub uruchamiając skrypt względem każdego węzła w klastrze hello.

W tym przykładzie dwa skrypty są uruchamiane, co toomount hello Azure plików udziału, a drugi toorun ten skrypt w każdym węźle klastra DC/OS hello.

Po pierwsze nazwę konta magazynu Azure hello i klucz dostępu są wymagane. Uruchom następujące polecenia tooget hello te informacje. Zwróć uwagę, te wartości są używane w kolejnym kroku.

Nazwa konta magazynu:

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

Klucz dostępu do konta magazynu:

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

Następnie Pobierz hello FQDN hello DC/OS wzorca i zapisze go w zmiennej.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Skopiuj węzeł główny toohello klucza prywatnego. Ten klucz jest wymagane toocreate ssh połączenia z wszystkie węzły w klastrze hello. Zaktualizuj hello nazwy użytkownika, jeśli podczas tworzenia klastra hello użyto wartości innych niż domyślne. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

Utwórz połączenie SSH z głównego hello (lub hello pierwszego serwera głównego) klastra systemu DC/OS. Zaktualizuj hello nazwy użytkownika, jeśli podczas tworzenia klastra hello użyto wartości innych niż domyślne.

```azurecli-interactive
ssh azureuser@$FQDN
```

Utwórz plik o nazwie **cifsMount.sh**, i hello kopiowania zawartości do niego. 

Ten skrypt jest udział plików na platformę Azure hello toomount używane. Aktualizacja hello `STORAGE_ACCT_NAME` i `ACCESS_KEY` zmienne hello informacji zebranych wcześniej.

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
Utworzyć drugi plik o nazwie **getNodesRunScript.sh** i hello Kopiuj zawartość do pliku hello. 

Ten skrypt umożliwia odnalezienie wszystkich węzłów klastra, a następnie wykonuje hello **cifsMount.sh** udział pliku skryptu toomount hello na każdym.

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

Witaj wykonywania skryptu toomount hello Azure udziału plików na wszystkich węzłach klastra hello.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

Witaj udziału plików jest teraz dostępny w `/mnt/share/dcosshare` w każdym węźle klastra hello.

## <a name="next-steps"></a>Następne kroki

W tym samouczku platformy Azure udział plików został dokonano tooa dostępne klastra DC/OS, wykonując kroki hello:

> [!div class="checklist"]
> * Tworzenie konta usługi Azure Storage
> * Tworzenie udziału plików
> * Instalowanie udziału hello w klastrze DC/OS hello

Przejdź dalej toolearn samouczka toohello temat integracji Azure kontenera rejestru z DC/OS na platformie Azure.  

> [!div class="nextstepaction"]
> [Równoważenie obciążenia aplikacji](container-service-dcos-acr.md)