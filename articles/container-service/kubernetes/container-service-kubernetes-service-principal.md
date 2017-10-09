---
title: "podmiot zabezpieczeń aaaService klastra Azure Kubernetes | Dokumentacja firmy Microsoft"
description: "Tworzenie jednostki usługi Azure Active Directory dla klastra Kubernetes w usłudze Azure Container Service i zarządzanie nią"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Konfigurowanie jednostki usługi Azure AD dla klastra Kubernetes w usłudze Azure Container Service


W usłudze kontenera platformy Azure, wymaga klastra Kubernetes [nazwy głównej usługi Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract z interfejsami API Azure. Witaj nazwy głównej usługi jest wymagane toodynamically zarządzanie zasobami, takich jak [trasy zdefiniowane przez użytkownika](../../virtual-network/virtual-networks-udr-overview.md) i hello [równoważenia obciążenia Azure 4 warstwy](../../load-balancer/load-balancer-overview.md). 


W tym artykule przedstawiono różne opcje tooset usługi głównej dla klastra Kubernetes. Na przykład, jeśli zostanie zainstalowany i skonfigurowany hello [Azure CLI 2.0](/cli/azure/install-az-cli2), możesz uruchomić hello [ `az acs create` ](/cli/azure/acs#create) polecenia toocreate hello Kubernetes głównej na powitania usługi klastrowania i hello tym samym czasie.


## <a name="requirements-for-hello-service-principal"></a>Wymagania dotyczące hello nazwy głównej usługi

Można użyć istniejącej usługi Azure AD nazwy głównej usługi spełnia hello wymogów lub Utwórz nową.

* **Zakres**: hello grupy zasobów w subskrypcji hello używane toodeploy hello Kubernetes klastra lub (mniej twierdzi) hello subskrypcji używane toodeploy hello klastra.

* **Rola**: **Współautor**

* **Wpis tajny klienta**: musi to być hasło. Obecnie nie można używać nazwy głównej usługi do uwierzytelniania certyfikatu.

> [!IMPORTANT] 
> toocreate nazwy głównej usługi musisz mieć uprawnienia tooregister aplikację z dzierżawą usługi Azure AD i rolę tooa aplikacji hello tooassign w ramach subskrypcji. toosee, jeśli masz uprawnienia wymagane hello [zaewidencjonować hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions). 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>Opcja 1. Tworzenie jednostki usługi w usłudze Azure AD

Jeśli chcesz toocreate nazwy głównej usługi Azure AD, przed wdrożeniem klastra Kubernetes, platforma Azure udostępnia kilka metod. 

następujące przykładowe polecenia Hello przedstawia sposób toodo pomocą hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). Można też utworzyć główną usługi za pomocą [programu Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), lub innych metod.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

Dane wyjściowe są podobne następujące toohello (w tym miejscu pokazano zredagowanym):

![Tworzenie nazwy głównej usługi](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Wyróżnione są hello **identyfikator klienta** (`appId`) i hello **klucz tajny klienta** (`password`) używanej jako parametry główną usługi dla wdrożenia klastra.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Podczas tworzenia klastra Kubernetes hello należy podać nazwę główną usługi

Podaj hello **identyfikator klienta** (nazywane również hello `appId`, dla Identyfikatora aplikacji) i **klucz tajny klienta** (`password`) z istniejącą usługę podmiotu zabezpieczeń jako parametry podczas tworzenia hello Kubernetes klastra. Upewnij się, że nazwy głównej usługi hello spełnia wymagania hello na powitania rozpoczynający się w tym artykule.

Te parametry można określić podczas wdrażania klastra Kubernetes hello przy użyciu hello [Azure interfejsu wiersza polecenia (CLI) 2.0](container-service-kubernetes-walkthrough.md), [portalu Azure](../dcos-swarm/container-service-deployment.md), lub innych metod.

>[!TIP] 
>Podczas określania hello **identyfikator klienta**, należy się hello toouse `appId`, nie hello `ObjectId`, hello głównej usługi.
>

Witaj poniższy przykład przedstawia toopass jednokierunkowej hello parametrów z hello Azure CLI 2.0. W tym przykładzie użyto hello [szablon szybkiego startu Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Pobierz](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) pliku parametrów szablonu hello `azuredeploy.parameters.json` z usługi GitHub.

2. Usługa hello toospecify główna, wprowadź wartości w polach `servicePrincipalClientId` i `servicePrincipalClientSecret` w pliku hello. (Należy też tooprovide własne wartości `dnsNamePrefix` i `sshRSAPublicKey`. ostatnie Hello jest klastra hello tooaccess klucza publicznego SSH hello). Zapisz plik hello.

    ![Przekazywanie parametrów nazwy głównej usługi](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Witaj uruchom następujące polecenie, używając `--parameters` tooset hello ścieżki toohello azuredeploy.parameters.json pliku. To polecenie wdraża hello klastra w grupie zasobów o nazwie tworzenia `myResourceGroup` hello regionu zachodnie stany USA.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>Opcja 2: Generowanie nazwy głównej usługi podczas tworzenia klastra hello z`az acs create`

Po uruchomieniu hello [ `az acs create` ](/cli/azure/acs#create) toocreate polecenia hello Kubernetes klastra, masz toogenerate opcji hello nazwy głównej usługi automatycznie.

Tak jak w przypadku innych opcji tworzenia klastra Kubernetes, parametry istniejącej nazwy głównej usługi można określić po uruchomieniu polecenia `az acs create`. Jednak jeśli pominięto tych parametrów, hello Azure CLI tworzy jeden automatycznie do użycia z usługą kontenera. Podczas wdrażania hello to ma miejsce przezroczysty. 

Witaj następujące polecenie tworzy klaster Kubernetes i generuje zarówno kluczy SSH i poświadczenia główne usługi:

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Jeśli konto nie ma hello Azure AD i toocreate uprawnienia subskrypcji nazwy głównej usługi, polecenie hello zbyt generuje błąd podobny`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>Dodatkowe zagadnienia

* Jeśli nie masz uprawnień toocreate nazwy głównej usługi w ramach subskrypcji, może być konieczne tooask usługi Azure AD lub tooassign administratora subskrypcji hello niezbędne uprawnienia lub uzyskać toouse głównej usługi, z usługi kontenera platformy Azure. 

* nazwy głównej usługi powitania dla Kubernetes jest częścią hello konfiguracji klastra. Jednak nie należy używać hello tożsamości toodeploy hello klastra.

* Każda jednostka usługi jest skojarzona z aplikacją usługi Azure AD. Hello nazwy głównej usługi dla klastra Kubernetes może być skojarzony z żadnych Azure prawidłową nazwę aplikacji usługi AD (na przykład: `https://www.contoso.org/example`). adres URL aplikacji hello Hello nie ma toobe rzeczywistych punktu końcowego.

* Podczas określania nazwy głównej usługi hello **identyfikator klienta**, można użyć wartości hello hello `appId` (jak pokazano w tym artykule) lub nazwy głównej usługi odpowiedniego hello `name` (na przykład`https://www.contoso.org/example`).

* Na wzorcu hello i agenta maszyny wirtualne w klastrze Kubernetes hello hello poświadczenia główne są przechowywane w hello /etc/kubernetes/azure.json pliku.

* Jeśli używasz hello `az acs create` polecenia nazwy głównej usługi hello toogenerate automatycznie, hello poświadczenia główne są zapisywane toohello ~/.azure/acsServicePrincipal.json pliku na maszynie hello używane toorun hello polecenia. 

* Jeśli używasz hello `az acs create` polecenia nazwy głównej usługi hello toogenerate automatycznie, nazwy głównej usługi hello mogą również uwierzytelniać za pomocą [rejestru kontenera platformy Azure](../../container-registry/container-registry-intro.md) utworzone w hello sam subskrypcji.




## <a name="next-steps"></a>Następne kroki

* [Rozpocznij pracę z klastrem Kubernetes](container-service-kubernetes-walkthrough.md) w klastrze usług kontenera.

* tootroubleshoot hello nazwy głównej usługi dla Kubernetes, zobacz hello [dokumentacji aparatu ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).


