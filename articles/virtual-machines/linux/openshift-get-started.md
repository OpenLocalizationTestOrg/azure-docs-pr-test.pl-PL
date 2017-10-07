---
title: aaaDeploy tooAzure pochodzenia OpenShift | Dokumentacja firmy Microsoft
description: "Dowiedz się maszyny wirtualne tooAzure pochodzenia OpenShift toodeploy."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>Wdrażanie tooAzure pochodzenia OpenShift maszyny wirtualne 

[Pochodzenie OpenShift](https://www.openshift.org/) to platforma kontenera typu open source oparty na [Kubernetes](https://kubernetes.io/). Takie rozwiązanie upraszcza hello procesu wdrażania, skalowanie i działania aplikacji wielodostępnej. 

W tym przewodniku opisano, jak toodeploy pochodzenia OpenShift na maszynach wirtualnych platformy Azure przy użyciu hello wiersza polecenia platformy Azure i szablony Menedżera zasobów Azure. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie kluczy SSH dla klastra OpenShift hello KeyVault toomanage.
> * Wdrażanie klastra OpenShift na maszynach wirtualnych Azure. 
> * Instalowanie i konfigurowanie hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello klastra.
> * Dostosowywanie hello OpenShift wdrożenia.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

To szybki start wymaga hello Azure CLI w wersji 2.0.8 lub nowszej. Wersja hello toofind, uruchom `az --version`. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure 
Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) polecenia i wykonaj hello na ekranie instrukcjami lub kliknij przycisk **wypróbuj** toouse powłoki chmury.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>Tworzenie magazynu kluczy
Tworzenie kluczy SSH dla klastra hello KeyVault toostore hello z hello [az keyvault utworzyć](/cli/azure/keyvault#create) polecenia.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>Tworzenie klucza SSH 
Klucz SSH jest wymagane toosecure dostępu toohello pochodzenia OpenShift klastra. Utwórz parę kluczy SSH za pomocą hello `ssh-keygen` polecenia. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> Witaj pary kluczy SSH, którą utworzysz nie może zawierać hasło.

Aby uzyskać więcej informacji na temat kluczy SSH w systemie Windows [jak klucze toocreate SSH w systemie Windows](/azure/virtual-machines/linux/ssh-from-windows).

## <a name="store-ssh-private-key-in-key-vault"></a>Przechowywanie klucza prywatnego SSH w magazynie kluczy
Hello wdrożenia OpenShift używa klucza SSH hello utworzone dostępu toosecure toohello OpenShift wzorca. tooenable hello wdrożenia toosecurely pobrać hello klucz SSH, przechowywać klucz hello w Key Vault za pomocą następującego polecenia hello.

# <a name="enabled-for-template-deployment"></a>Włączony do wdrożenia szablonu
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>Tworzenie nazwy głównej usługi 
OpenShift komunikuje się z platformy Azure przy użyciu nazwy użytkownika i hasła lub nazwy głównej usługi. Podmiot zabezpieczeń usługi Azure jest tożsamość zabezpieczeń korzystających z aplikacji, usługami i automatyzacja takich narzędzi jak OpenShift. Kontrolowanie i definiowanie uprawnień hello toowhat operacji hello service principal można wykonywać na platformie Azure. tooimprove zabezpieczeń za pośrednictwem tylko podanie nazwy użytkownika i hasła, w tym przykładzie tworzy podstawowe usługę podmiotu zabezpieczeń.

Utwórz usługę podmiotu zabezpieczeń z [az ad sp utworzyć do rbac](/cli/azure/ad/sp#create-for-rbac) i dane wyjściowe hello poświadczenia, które wymaga OpenShift:

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Zwróć uwagę na powitania appId właściwości zwróconej z hello polecenia.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > Nie twórz niezabezpieczonego hasła.  Postępuj zgodnie ze wskazówkami zawartymi w [ograniczeniach i regułach dotyczących hasła usługi Azure AD](/azure/active-directory/active-directory-passwords-policy).

Aby uzyskać więcej informacji dotyczących nazwy główne usług, zobacz [Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="deploy-hello-openshift-origin-template"></a>Wdrażanie hello pochodzenia OpenShift szablonu
Następnie wdrożyć pochodzenia OpenShift przy użyciu szablonu usługi Azure Resource Manager. 

> [!NOTE] 
> Witaj następujące polecenie wymaga az CLI 2.0.8 lub nowszym. Możesz sprawdzić hello az CLI wersji z hello `az --version` polecenia. tooupdate hello wersji interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).

Użyj hello `appId` wartości z nazwy głównej usługi hello utworzony wcześniej dla hello `aadClientId` parametru.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
Witaj wdrażania może potrwać too20 toocomplete minut. Witaj adres URL konsoli OpenShift hello i nazwa DNS hello OpenShift wzorzec jest drukowane toohello terminal po zakończeniu wdrażania hello.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Połącz toohello OpenShift klastra
Po zakończeniu wdrażania hello, Połącz konsolę OpenShift toohello za pomocą przeglądarki hello przy użyciu hello `OpenShift Console Uri`. Alternatywnie możesz połączyć za pomocą następującego polecenia hello wzorca OpenShift toohello.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, OpenShift klastra i wszystkich powiązanych zasobów.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W przypadku tego samouczka, zapamiętanych jak:
> [!div class="checklist"]
> * Tworzenie kluczy SSH dla klastra OpenShift hello KeyVault toomanage.
> * Wdrażanie klastra OpenShift na maszynach wirtualnych Azure. 
> * Instalowanie i konfigurowanie hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello klastra.

Po wdrożeniu klastra OpenShift pochodzenia. Jak wykonać toolearn samouczki OpenShift toodeploy pierwszą aplikację i użyj narzędzia OpenShift hello. Zobacz [wprowadzenie pochodzenia OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget uruchomiona. 
