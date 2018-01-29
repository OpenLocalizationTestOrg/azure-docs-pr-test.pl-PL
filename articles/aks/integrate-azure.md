---
title: "Integracja z usługami zarządzanymi przez platformę Azure przy użyciu usługi Open Service Broker for Azure (OSBA)"
description: "Integracja z usługami zarządzanymi przez platformę Azure przy użyciu usługi Open Service Broker for Azure (OSBA)"
services: container-service
author: sozercan
manager: timlt
ms.service: container-service
ms.topic: overview
ms.date: 12/05/2017
ms.author: seozerca
ms.openlocfilehash: 339e600f18613e8cf4e5529c759ad33076d48654
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="integrate-with-azure-managed-services-using-open-service-broker-for-azure-osba"></a>Integracja z usługami zarządzanymi przez platformę Azure przy użyciu usługi Open Service Broker for Azure (OSBA)

Razem z [wykazem usług Kubernetes][kubernetes-service-catalog] usługa Open Service Broker for Azure (OSBA) umożliwia deweloperom korzystanie z usług zarządzanych przez platformę Azure w usłudze Kubernetes. Ten przewodnik dotyczy wdrażania wykazu usług Kubernetes, usługi Open Service Broker for Azure (OSBA) oraz aplikacji korzystających z usług zarządzanych przez platformę Azure przy użyciu usługi Kubernetes.

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure

* Interfejs wiersza polecenia platformy Azure 2.0: można [lokalnie zainstalować tę funkcję][azure-cli-install] lub korzystać z niej w usłudze [Azure Cloud Shell][azure-cloud-shell].

* Interfejs wiersza polecenia narzędzia Helm 2.7+: można [lokalnie zainstalować tę usługę][helm-cli-install] lub korzystać z niej w usłudze [Azure Cloud Shell][azure-cloud-shell].

* Uprawnienia do tworzenia jednostki usługi z rolą współautora w subskrypcji platformy Azure

* Istniejący klaster usługi Azure Container Service (AKS). Jeśli potrzebujesz klastra AKS, wykonaj instrukcje podane w przewodniku Szybki start [Tworzenie klastra AKS][create-aks-cluster].

## <a name="install-service-catalog"></a>Instalowanie wykazu usług

Pierwszym krokiem jest zainstalowanie wykazu usług w klastrze usługi Kubernetes przy użyciu planu narzędzia Helm. Uaktualnij instalację programu Tiller (serwera narzędzia Helm) w klastrze:

```azurecli-interactive
helm init --upgrade
```

Teraz dodaj plan wykazu usług do repozytorium narzędzia Helm:

```azurecli-interactive
helm repo add svc-cat https://svc-catalog-charts.storage.googleapis.com
```

Na koniec zainstaluj wykaz usług przy użyciu planu narzędzia Helm:

```azurecli-interactive
helm install svc-cat/catalog --name catalog --namespace catalog --set rbacEnable=false
```

Po uruchomieniu planu narzędzia Helm upewnij się, że pozycja `servicecatalog` jest wyświetlana w danych wyjściowych następującego polecenia:

```azurecli-interactive
kubectl get apiservice
```

Na przykład powinny pojawić się dane wyjściowe podobne do następujących (tutaj zostały obcięte):

```
NAME                                 AGE
v1.                                  10m
v1.authentication.k8s.io             10m
...
v1beta1.servicecatalog.k8s.io        34s
v1beta1.storage.k8s.io               10
```

## <a name="install-open-service-broker-for-azure"></a>Instalowanie usługi Open Service Broker for Azure

Następnym krokiem jest zainstalowanie usługi [Open Service Broker for Azure][open-service-broker-azure], która obejmuje wykaz dla usług zarządzanych przez platformę Azure. Przykłady dostępnych usług platformy Azure to Azure Database for PostgreSQL, Azure Redis Cache, Azure Database for MySQL, Azure Cosmos DB, Azure SQL Database i inne.

Najpierw dodajmy repozytorium narzędzia Helm dla usługi Open Service Broker for Azure:

```azurecli-interactive
helm repo add azure https://kubernetescharts.blob.core.windows.net/azure
```

Utwórz [jednostkę usługi][create-service-principal] za pomocą następującego polecenia interfejsu wiersza polecenia platformy Azure:

```azurecli-interactive
az ad sp create-for-rbac
```

Dane wyjściowe powinny być podobne do następujących. Zanotuj wartości `appId`, `password` i `tenant`, których użyjesz w następnym kroku.

```JSON
{
  "appId": "7248f250-0000-0000-0000-dbdeb8400d85",
  "displayName": "azure-cli-2017-10-15-02-20-15",
  "name": "http://azure-cli-2017-10-15-02-20-15",
  "password": "77851d2c-0000-0000-0000-cb3ebc97975a",
  "tenant": "72f988bf-0000-0000-0000-2d7cd011db47"
}
```

Ustaw następujące zmienne środowiskowe z podanymi wcześniej wartościami:

```azurecli-interactive
AZURE_CLIENT_ID=<appId>
AZURE_CLIENT_SECRET=<password>
AZURE_TENANT_ID=<tenant>
```

Pobierz identyfikator subskrypcji platformy Azure:

```azurecli-interactive
az account show --query id --output tsv
```

Ustaw następującą zmienną środowiskową z podaną wcześniej wartością:

```azurecli-interactive
AZURE_SUBSCRIPTION_ID=[your Azure subscription ID from above]
```

Po wypełnieniu tych zmiennych środowiskowych uruchom następujące polecenie, aby zainstalować usługę Open Service Broker for Azure przy użyciu planu narzędzia Helm:

```azurecli-interactive
helm install azure/open-service-broker-azure --name osba --namespace osba \
    --set azure.subscriptionId=$AZURE_SUBSCRIPTION_ID \
    --set azure.tenantId=$AZURE_TENANT_ID \
    --set azure.clientId=$AZURE_CLIENT_ID \
    --set azure.clientSecret=$AZURE_CLIENT_SECRET
```

Po zakończeniu wdrażania usługi OSBA zainstaluj [interfejs wiersza polecenia wykazu usług][service-catalog-cli] — łatwy w użyciu interfejs wiersza polecenia umożliwiający wysyłanie zapytań dotyczących brokerów usług, klas usług, planów usług i nie tylko.

Uruchom następujące polecenia, aby zainstalować dane binarne interfejsu wiersza polecenia wykazu usług:

```azurecli-interactive
curl -sLO https://servicecatalogcli.blob.core.windows.net/cli/latest/$(uname -s)/$(uname -m)/svcat
chmod +x ./svcat
```

Wyświetl listę zainstalowanych brokerów usług:

```azurecli-interactive
./svcat get brokers
```

Powinny zostać wyświetlone dane wyjściowe podobne do następujących:

```
  NAME                               URL                                STATUS
+------+--------------------------------------------------------------+--------+
  osba   http://osba-open-service-broker-azure.osba.svc.cluster.local   Ready
```

Następnie wyświetl listę dostępnych klas usług. Wyświetlane klasy usług to dostępne usługi zarządzane przez platformę Azure, które można aprowizować za pośrednictwem usługi Open Service Broker for Azure.

```azurecli-interactive
./svcat get classes
```

Na koniec wyświetl listę wszystkich dostępnych planów usług. Plany usług to warstwy usług dotyczące usług zarządzanych przez platformę Azure. Na przykład w przypadku usługi Azure Database for MySQL są dostępne plany od `basic50` dla warstwy Podstawowa z 50 jednostkami DTU do `standard800` dla warstwy Standardowa z 800 jednostkami DTU.

```azurecli-interactive
./svcat get plans
```

## <a name="install-wordpress-from-helm-chart-using-azure-database-for-mysql"></a>Instalowanie środowiska WordPress z planu narzędzia Helm przy użyciu usługi Azure Database for MySQL

W tym kroku użyjesz narzędzia Helm do zainstalowania zaktualizowanego planu narzędzia Helm dla środowiska WordPress. Plan umożliwia aprowizację zewnętrznego wystąpienia usługi Azure Database for MySQL, z którego może korzystać środowisko WordPress. Ten proces może potrwać kilka minut.

```azurecli-interactive
helm install azure/wordpress --name wordpress --namespace wordpress --set resources.requests.cpu=0
```

Aby sprawdzić, czy instalacja spowodowała aprowizację odpowiednich zasobów, wyświetl zainstalowane wystąpienia usług i powiązania:

```azurecli-interactive
./svcat get instances -n wordpress
./svcat get bindings -n wordpress
```

Wyświetl zainstalowane klucze tajne:

```azurecli-interactive
kubectl get secrets -n wordpress -o yaml
```

## <a name="next-steps"></a>Następne kroki

Wykonanie instrukcji podanych w tym artykule spowodowało wdrożenie wykazu usług w klastrze usługi Azure Container Service (AKS). Została użyta usługa Open Service Broker for Azure w celu wdrożenia instalacji środowiska WordPress korzystającego z usług zarządzanych przez platformę Azure, w tym przypadku — Azure Database for MySQL.

Zapoznaj się z repozytorium [Azure/helm-charts][helm-charts], aby uzyskać dostęp do innych zaktualizowanych planów narzędzia Helm opartych na usłudze OSBA. Jeśli chcesz utworzyć własne plany współpracujące z usługą OSBA, zobacz [Tworzenie nowego planu][helm-create-new-chart].

<!-- LINKS - external -->
[helm-charts]: https://github.com/Azure/helm-charts
[helm-cli-install]: kubernetes-helm.md#install-helm-cli
[helm-create-new-chart]: https://github.com/Azure/helm-charts#creating-a-new-chart
[kubernetes-service-catalog]: https://github.com/kubernetes-incubator/service-catalog
[open-service-broker-azure]: https://github.com/Azure/open-service-broker-azure
[service-catalog-cli]: https://github.com/Azure/service-catalog-cli

<!-- LINKS - internal -->
[azure-cli-install]: /cli/azure/install-azure-cli
[azure-cloud-shell]: ../cloud-shell/overview.md
[create-aks-cluster]: ./kubernetes-walkthrough.md
[create-service-principal]: ./kubernetes-service-principal.md
