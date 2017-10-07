---
title: "za pomocą usługi Azure API REST - Azure klastrów Hadoop aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate HDInsight clusters poprzez przesłanie toohello szablonów usługi Azure Resource Manager interfejsu API REST Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a>Tworzenie klastrów Hadoop przy użyciu interfejsu API REST Azure hello

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Dowiedz się, jak toocreate HDInsight klastra przy użyciu szablonu usługi Azure Resource Manager i hello interfejsu API REST Azure.

Witaj interfejsu API REST Azure umożliwia tooperform operacji zarządzania na usług hostowanych w hello platformy Azure, w tym hello tworzenia nowych zasobów, takich jak klastry usługi HDInsight.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

> [!NOTE]
> Hello czynnościach w ramach tego dokumentu Użyj hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate narzędzie z hello interfejsu API REST Azure.

## <a name="create-a-template"></a>Tworzenie szablonu

Szablony usługi Azure Resource Manager są dokumentów JSON, które opisują **grupy zasobów** i wszystkie zasoby w niej (np. usługi HDInsight). To rozwiązanie oparte na szablonach umożliwia toodefine hello zasoby, które należy dla usługi HDInsight w jednym szablonie.

Hello następującego dokumentu JSON jest połączenie hello plików szablonu i parametry [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), co powoduje opartych na systemie Linux klaster przy użyciu hello toosecure hasło konta użytkownika SSH.

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used tooremotely access hello cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
                               "name": "headnode",
                               "targetInstanceCount": "2",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           },
                           {
                               "name": "workernode",
                               "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

Ten przykład jest używany w procedurze hello w tym dokumencie. Przykład Witaj Zastąp *wartości* w hello **parametry** sekcji hello wartościami dla klastra.

> [!IMPORTANT]
> Szablon Hello używa hello domyślna liczba węzłów procesu roboczego (4) dla klastra usługi HDInsight. Jeśli planujesz na więcej niż 32 węzłami procesów roboczych, musi wybierz rozmiar węzła głównego z co najmniej 8 rdzeni i 14 GB pamięci ram.
>
> Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="log-in-tooyour-azure-subscription"></a>Zaloguj się za tooyour subskrypcji platformy Azure

Wykonaj kroki hello udokumentowane w [wprowadzenie Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) i nawiąż połączenie przy użyciu hello subskrypcji tooyour `az login` polecenia.

## <a name="create-a-service-principal"></a>Tworzenie nazwy głównej usługi

> [!NOTE]
> Te kroki są skróconej wersji hello *Tworzenie nazwy głównej usługi z hasłem* sekcji hello [toocreate wiersza polecenia platformy Azure Użyj nazwy głównej usługi zasobów tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) dokumentu. Te kroki tworzenia nazwy głównej usługi, która jest używana tooauthenticate toohello interfejsu API REST usługi Azure.

1. Z wiersza polecenia użyj hello następujące polecenia toolist subskrypcji platformy Azure.

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    Na liście hello, wybierz subskrypcję hello, że mają toouse i zanotuj hello **IDENTYFIKATOR_SUBSKRYPCJI** i __Tenant_ID__ kolumn. Zapisz te wartości.

2. Użyj hello następujące polecenia toocreate aplikacji w usłudze Azure Active Directory.

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    Zastąp wartości hello hello `--display-name`, `--homepage`, i `--identifier-uris` z własne wartości. Podaj hasło dla hello nowy wpis usługi Active Directory.

   > [!NOTE]
   > Witaj `--home-page` i `--identifier-uris` wartości nie ma potrzeby tooreference rzeczywistej stronie sieci web hostowanej na powitania internet. Klienci muszą mieć unikatowe identyfikatory URI.

   Witaj wartość zwracana z tego polecenia jest hello __identyfikator aplikacji__ dla nowej aplikacji hello. Zapisz tę wartość.

3. Użyj hello następujące polecenie toocreate nazwy głównej usługi przy użyciu hello **identyfikator aplikacji**.

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     Witaj wartość zwracana z tego polecenia jest hello __obiektu o identyfikatorze__. Zapisz tę wartość.

4. Przypisz hello **właściciela** roli: toohello nazwy głównej usługi przy użyciu hello **obiektu o identyfikatorze** wartość. Użyj hello **identyfikator subskrypcji** uzyskanymi wcześniej.

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a>Uzyskiwanie tokenu uwierzytelniania

Użyj hello następujące polecenia tooretrieve tokenu uwierzytelniania:

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

Ustaw `$TENANTID`, `$APPID`, i `$PASSWORD` wartości toohello uzyskany lub użyte wcześniej.

Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i hello treść odpowiedzi zawiera dokument JSON.

Witaj dokumentu JSON zwróconych przez to żądanie zawiera element o nazwie **' access_token '**. Witaj wartość **' access_token '** jest używane tooauthentication toohello żądania interfejsu API REST.

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Użyj powitania po toocreate grupę zasobów.

* Ustaw `$SUBSCRIPTIONID` toohello identyfikator subskrypcji otrzymanych podczas tworzenia hello nazwy głównej usługi.
* Ustaw `$ACCESSTOKEN` token dostępu toohello Odebrano hello poprzedniego kroku.
* Zastąp `DATACENTERLOCATION` z centrum danych hello ma grupy zasobów hello toocreate i zasobów, w. Na przykład "południowo-środkowe Stany".
* Ustaw `$RESOURCEGROUPNAME` nazwę toohello, mają toouse dla tej grupy:

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i hello treść odpowiedzi zawiera dokument JSON zawierający informacje o grupie hello. Witaj `"provisioningState"` element zawiera wartość `"Succeeded"`.

## <a name="create-a-deployment"></a>Tworzenie wdrożenia

Użyj hello następujące polecenie grupy zasobów toohello toodeploy hello szablonu.

* Ustaw `$DEPLOYMENTNAME` nazwę toohello, mają toouse dla tego wdrożenia.

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> Zapisanie pliku tooa szablonu hello, można użyć hello następujące polecenie, a nie `-d "{ template and parameters}"`:
>
> `--data-binary "@/path/to/file.json"`

Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i hello treść odpowiedzi zawiera dokument JSON zawierający informacje o operacji wdrażania hello.

> [!IMPORTANT]
> wdrożenie Hello zostało przesłane, ale nie zostało ukończone. Może upłynąć kilka minut, zazwyczaj około 15 hello toocomplete wdrożenia.

## <a name="check-hello-status-of-a-deployment"></a>Sprawdź stan hello wdrożenia

Stan hello toocheck hello wdrożenia, hello Użyj następującego polecenia:

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

To polecenie zwraca zawierający informacje o operacji wdrażania hello dokumentu JSON. Witaj `"provisioningState"` element zawiera stan hello hello wdrożenia. Jeśli ten element zawiera wartość `"Succeeded"`, następnie hello wdrożenia została pomyślnie ukończona.

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki

Po pomyślnym utworzeniu klastra usługi HDInsight, za pomocą powitania po toolearn jak toowork z klastrem.

### <a name="hadoop-clusters"></a>Klastry Hadoop

* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystać z usługi MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Klastrów HBase

* [Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Klastry STORM

* [Tworzenie topologii Java dla Storm w usłudze HDInsight](hdinsight-storm-develop-java-topology.md)
* [Użyj składników języka Python w Storm w usłudze HDInsight](hdinsight-storm-develop-python-topology.md)
* [Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)
