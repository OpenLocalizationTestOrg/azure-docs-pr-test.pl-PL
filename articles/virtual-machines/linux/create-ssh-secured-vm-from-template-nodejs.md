---
title: "aaaCreate maszyny Wirtualnej systemu Linux przy użyciu szablonu platformy Azure z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft"
description: "Utwórz Maszynę wirtualną systemu Linux na platformie Azure przy użyciu hello Azure CLI 1.0 i szablonu usługi Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>Jak toocreate a maszyny Wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 szablonu usługi Azure Resource Manager
W tym artykule opisano sposób tooquickly wdrażania maszyny wirtualnej systemu Linux przy użyciu hello Azure CLI 1.0 i szablonu usługi Azure Resource Manager. wymaga artykułu Hello:

* konta platformy Azure ([skorzystaj z bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/));
* Witaj [Azure CLI 1.0](../../cli-install-nodejs.md) logowania `azure login`.
* Hello Azure CLI *musi znajdować się w* tryb usługi Azure Resource Manager `azure config mode arm`.

Można szybko wdrożyć szablon maszyny Wirtualnej systemu Linux przy użyciu hello [portalu Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#quick-command-summary) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="quick-command-summary"></a>Szybkie polecenia — podsumowanie
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Szczegółowy przewodnik
Szablony umożliwiają toocreate maszyn wirtualnych na platformie Azure przy użyciu ustawień, które mają toocustomize podczas uruchomienia hello, ustawienia, takie jak nazwy użytkowników i nazwy hostów. W tym artykule szablon platformy Azure został użyty do utworzenia maszyny wirtualnej z systemem Ubuntu oraz grupy zabezpieczeń sieci z otwartym portem 22 dla usługi SSH.

Szablony programu Azure Resource Manager są plikami JSON, za pomocą których można wykonywać proste, jednorazowe zadania, takie jak uruchamianie maszyny wirtualnej z systemem Ubuntu przedstawione w tym artykule.  Szablony usługi Azure może być również używane tooconstruct złożonych konfiguracji platformy Azure całego środowisk, takich jak testowych, programistycznych lub produkcyjnych stosu wdrożenia.

## <a name="create-hello-linux-vm"></a>Utwórz hello maszyny Wirtualnej systemu Linux
Witaj po kodu przykładzie pokazano sposób toocall `azure group create` toocreate zasób grupy i wdrażanie zabezpieczone SSH maszyny Wirtualnej systemu Linux hello przy użyciu tego samego czasu [tego szablonu usługi Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Należy pamiętać, że w tym przykładzie należy toouse nazw, które są unikatowe tooyour środowiska. W tym przykładzie użyto *myResourceGroup* jako hello Nazwa grupy zasobów, a *myVM* jako hello nazwę maszyny Wirtualnej.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

dane wyjściowe Hello powinna wyglądać powitania po bloku danych wyjściowych:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Ten przykład wdrożyć Maszynę wirtualną przy użyciu hello `--template-uri` parametru.  Można również pobrać lub utworzyć szablon lokalnie i Przekaż szablon hello przy użyciu hello `--template-file` parametr ścieżki pliku szablonu toohello jako argument. Witaj wiersza polecenia platformy Azure monituje o parametry hello wymagane przez szablon hello.

## <a name="next-steps"></a>Następne kroki
Wyszukiwanie hello [galerię szablonów](https://azure.microsoft.com/documentation/templates/) toodiscover jakie toodeploy struktur aplikacji dalej.

