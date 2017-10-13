---
title: "Nazwa główna usługi klastra Azure Kubernetes | Dokumentacja firmy Microsoft"
description: "Tworzenie jednostki usługi Azure Active Directory dla klastra Kubernetes w usłudze Azure Container Service i zarządzanie nią"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 14975454cbc0afcfbdbd3aa6b52983be4d4b1785
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Konfigurowanie jednostki usługi Azure AD dla klastra Kubernetes w usłudze Azure Container Service


W usłudze Azure Container Service klaster Kubernetes wymaga [jednostki usługi Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) do współpracy z interfejsami API platformy Azure. Nazwa główna usługi jest potrzebna do dynamicznego zarządzania zasobami, takimi jak [trasy zdefiniowane przez użytkownika](../../virtual-network/virtual-networks-udr-overview.md) i narzędzie [Azure Load Balancer dla warstwy 4](../../load-balancer/load-balancer-overview.md).


W tym artykule przedstawiono różne sposoby konfigurowania jednostki usługi dla klastra Kubernetes. Na przykład jeśli zainstalowano i skonfigurowano [interfejs wiersza polecenia platformy Azure w wersji 2.0](/cli/azure/install-az-cli2), można uruchomić polecenie [`az acs create`](/cli/azure/acs#create), aby jednocześnie utworzyć klaster Kubernetes i nazwę główną usługi.


## <a name="requirements-for-the-service-principal"></a>Wymagania dotyczące nazwy głównej usługi

Możesz użyć istniejącej jednostki usługi Azure AD, która spełnia następujące wymagania, albo utworzyć nową.

* **Zakres**: subskrypcja używana do wdrożenia klastra.

* **Rola**: **Współautor**

* **Wpis tajny klienta**: musi to być hasło. Obecnie nie można używać nazwy głównej usługi do uwierzytelniania certyfikatu.

> [!IMPORTANT]
> Aby utworzyć jednostkę usługi, musisz mieć uprawnienia do zarejestrowania aplikacji w swojej dzierżawie usługi Azure AD i przypisania aplikacji do roli w swojej subskrypcji. Aby sprawdzić, czy masz wymagane uprawnienia, [zajrzyj do portalu](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>Opcja 1. Tworzenie jednostki usługi w usłudze Azure AD

Jeśli chcesz utworzyć jednostkę usługi Azure AD przed wdrożeniem klastra Kubernetes, platforma Azure udostępnia kilka metod.

Następujące przykładowe polecenia pokazują, jak wykonać to za pomocą interfejsu [wiersza polecenia platformy Azure w wersji 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). Można też utworzyć jednostkę usługi za pomocą programu [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), [portalu](../../azure-resource-manager/resource-group-create-service-principal-portal.md) lub innej metody.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create --name "myResourceGroup" --location "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID"
```

Dane wyjściowe są zbliżone do następujących (pokazane tutaj zostały zredagowane):

![Tworzenie nazwy głównej usługi](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Wyróżniono **identyfikator klienta** (`appId`) i **klucz tajny klienta** (`password`), używane jako parametry nazwy głównej usługi przy wdrażaniu klastra.


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a>Określanie jednostki usługi podczas tworzenia klastra Kubernetes

Podaj **identyfikator klienta** (nazywany również `appId`, identyfikator aplikacji) i **wpis tajny klienta** (`password`) istniejącej nazwy głównej usługi jako parametry podczas tworzenia klastra Kubernetes. Upewnij się, że jednostka usługi spełnia wymagania przedstawione na początku tego artykułu.

Te parametry można określić podczas wdrażania klastra Kubernetes za pomocą [interfejsu wiersza polecenia platformy Azure w wersji 2.0](container-service-kubernetes-walkthrough.md), witryny [Azure Portal](../dcos-swarm/container-service-deployment.md) lub innymi metodami.

>[!TIP]
>Podczas określania **identyfikatora klienta** należy użyć identyfikatora `appId`, a nie `ObjectId` nazwy głównej usługi.
>

Poniższy przykład przedstawia sposób przekazania parametrów poprzez interfejs wiersza polecenia Azure w wersji 2.0. W tym przykładzie użyto [szablonu Kubernetes quickstart](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Pobierz](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) plik parametrów szablonu `azuredeploy.parameters.json` z usługi GitHub.

2. Aby określić nazwę główną usługi, wprowadź wartości dla `servicePrincipalClientId` i `servicePrincipalClientSecret` w pliku. (Należy również podać własne wartości dla `dnsNamePrefix` i `sshRSAPublicKey`. Ta ostatnia jest kluczem publicznym SSH umożliwiającym dostęp do klastra). Zapisz plik.

    ![Przekazywanie parametrów nazwy głównej usługi](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Przy użyciu opcji `--parameters` uruchom następujące polecenie, aby ustawić ścieżkę do pliku azuredeploy.parameters.json. To polecenie wdraża klaster w utworzonej grupie zasobów o nazwie `myResourceGroup` w regionie Zachodnie stany USA.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus"

    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a>Opcja 2. Wygenerowanie jednostki usługi podczas tworzenia klastra przy użyciu polecenia `az acs create`

Jeśli uruchamiasz polecenie [`az acs create`](/cli/azure/acs#create) w celu utworzenia klastra Kubernetes, masz możliwość automatycznego wygenerowania jednostki usługi.

Tak jak w przypadku innych opcji tworzenia klastra Kubernetes, parametry istniejącej nazwy głównej usługi można określić po uruchomieniu polecenia `az acs create`. Jednak w przypadku pominięcia tych parametrów interfejs wiersza polecenia platformy Azure automatycznie tworzy jednostkę usługi do użycia z usługą Container Service. Podczas wdrażania dzieje się to w sposób niewidoczny dla użytkownika.

Następujące polecenie tworzy klaster Kubernetes i generuje zarówno klucze SSH, jak i poświadczenia nazwy głównej usługi:

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Jeśli konto nie ma uprawnień usługi Azure AD i subskrypcji do utworzenia jednostki usługi, polecenie generuje błąd podobny do: `Insufficient privileges to complete the operation.`
>

## <a name="additional-considerations"></a>Dodatkowe zagadnienia

* Jeśli nie masz uprawnień do utworzenia jednostki usługi w swojej subskrypcji, konieczne może być poproszenie administratora usługi Azure AD lub subskrypcji o przypisanie niezbędnych uprawnień albo o jednostkę usługi do użycia z usługą Azure Container Service.

* Jednostka usługi dla rozwiązania Kubernetes jest częścią konfiguracji klastra. Nie należy jednak używać tożsamości do wdrażania klastra.

* Każda jednostka usługi jest skojarzona z aplikacją usługi Azure AD. Jednostka usługi dla klastra Kubernetes może zostać skojarzona z dowolną prawidłową nazwą aplikacji usługi Azure AD (np. `https://www.contoso.org/example`). Adres URL dla aplikacji nie musi być rzeczywistym punktem końcowym.

* Podczas określania **identyfikatora klienta** jednostki usługi można użyć wartości `appId` (jak pokazano w tym artykule) lub odpowiedniej jednostki usługi `name` (na przykład `https://www.contoso.org/example`).

* Na głównej maszynie wirtualnej i maszynach wirtualnych agentów w klastrze Kubernetes poświadczenia jednostki usługi są przechowywane w pliku /etc/kubernetes/azure.json.

* Gdy używasz polecenia `az acs create`, aby automatycznie wygenerować jednostkę usługi, poświadczenia jednostki usługi są zapisywane w pliku ~/.azure/acsServicePrincipal.json na maszynie użytej do uruchomienia polecenia.

* Kiedy używasz polecenia `az acs create` do automatycznego wygenerowania jednostki usługi, jednostka usługi może także uwierzytelnić się za pomocą [rejestru kontenera platformy Azure](../../container-registry/container-registry-intro.md) utworzonego w tej samej subskrypcji.

## <a name="next-steps"></a>Następne kroki

* [Rozpocznij pracę z klastrem Kubernetes](container-service-kubernetes-walkthrough.md) w klastrze usług kontenera.

* Aby rozwiązać problemy z jednostką usługi dla rozwiązania Kubernetes, zobacz [dokumentację aparatu ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).