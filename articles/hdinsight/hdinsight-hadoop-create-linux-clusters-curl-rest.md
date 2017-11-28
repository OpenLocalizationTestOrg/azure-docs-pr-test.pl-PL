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
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="901c2-103">Tworzenie klastrów Hadoop przy użyciu interfejsu API REST Azure hello</span><span class="sxs-lookup"><span data-stu-id="901c2-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="901c2-104">Dowiedz się, jak toocreate HDInsight klastra przy użyciu szablonu usługi Azure Resource Manager i hello interfejsu API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="901c2-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="901c2-105">Witaj interfejsu API REST Azure umożliwia tooperform operacji zarządzania na usług hostowanych w hello platformy Azure, w tym hello tworzenia nowych zasobów, takich jak klastry usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="901c2-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="901c2-106">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="901c2-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="901c2-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="901c2-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="901c2-108">Hello czynnościach w ramach tego dokumentu Użyj hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate narzędzie z hello interfejsu API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="901c2-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="901c2-109">Tworzenie szablonu</span><span class="sxs-lookup"><span data-stu-id="901c2-109">Create a template</span></span>

<span data-ttu-id="901c2-110">Szablony usługi Azure Resource Manager są dokumentów JSON, które opisują **grupy zasobów** i wszystkie zasoby w niej (np. usługi HDInsight). To rozwiązanie oparte na szablonach umożliwia toodefine hello zasoby, które należy dla usługi HDInsight w jednym szablonie.</span><span class="sxs-lookup"><span data-stu-id="901c2-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="901c2-111">Hello następującego dokumentu JSON jest połączenie hello plików szablonu i parametry [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), co powoduje opartych na systemie Linux klaster przy użyciu hello toosecure hasło konta użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="901c2-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

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

<span data-ttu-id="901c2-112">Ten przykład jest używany w procedurze hello w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="901c2-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="901c2-113">Przykład Witaj Zastąp *wartości* w hello **parametry** sekcji hello wartościami dla klastra.</span><span class="sxs-lookup"><span data-stu-id="901c2-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="901c2-114">Szablon Hello używa hello domyślna liczba węzłów procesu roboczego (4) dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="901c2-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="901c2-115">Jeśli planujesz na więcej niż 32 węzłami procesów roboczych, musi wybierz rozmiar węzła głównego z co najmniej 8 rdzeni i 14 GB pamięci ram.</span><span class="sxs-lookup"><span data-stu-id="901c2-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="901c2-116">Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="901c2-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="901c2-117">Zaloguj się za tooyour subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="901c2-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="901c2-118">Wykonaj kroki hello udokumentowane w [wprowadzenie Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) i nawiąż połączenie przy użyciu hello subskrypcji tooyour `az login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="901c2-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="901c2-119">Tworzenie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="901c2-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="901c2-120">Te kroki są skróconej wersji hello *Tworzenie nazwy głównej usługi z hasłem* sekcji hello [toocreate wiersza polecenia platformy Azure Użyj nazwy głównej usługi zasobów tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="901c2-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="901c2-121">Te kroki tworzenia nazwy głównej usługi, która jest używana tooauthenticate toohello interfejsu API REST usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="901c2-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="901c2-122">Z wiersza polecenia użyj hello następujące polecenia toolist subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="901c2-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="901c2-123">Na liście hello, wybierz subskrypcję hello, że mają toouse i zanotuj hello **IDENTYFIKATOR_SUBSKRYPCJI** i __Tenant_ID__ kolumn.</span><span class="sxs-lookup"><span data-stu-id="901c2-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="901c2-124">Zapisz te wartości.</span><span class="sxs-lookup"><span data-stu-id="901c2-124">Save these values.</span></span>

2. <span data-ttu-id="901c2-125">Użyj hello następujące polecenia toocreate aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="901c2-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="901c2-126">Zastąp wartości hello hello `--display-name`, `--homepage`, i `--identifier-uris` z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="901c2-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="901c2-127">Podaj hasło dla hello nowy wpis usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="901c2-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="901c2-128">Witaj `--home-page` i `--identifier-uris` wartości nie ma potrzeby tooreference rzeczywistej stronie sieci web hostowanej na powitania internet.</span><span class="sxs-lookup"><span data-stu-id="901c2-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="901c2-129">Klienci muszą mieć unikatowe identyfikatory URI.</span><span class="sxs-lookup"><span data-stu-id="901c2-129">They must be unique URIs.</span></span>

   <span data-ttu-id="901c2-130">Witaj wartość zwracana z tego polecenia jest hello __identyfikator aplikacji__ dla nowej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="901c2-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="901c2-131">Zapisz tę wartość.</span><span class="sxs-lookup"><span data-stu-id="901c2-131">Save this value.</span></span>

3. <span data-ttu-id="901c2-132">Użyj hello następujące polecenie toocreate nazwy głównej usługi przy użyciu hello **identyfikator aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="901c2-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="901c2-133">Witaj wartość zwracana z tego polecenia jest hello __obiektu o identyfikatorze__.</span><span class="sxs-lookup"><span data-stu-id="901c2-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="901c2-134">Zapisz tę wartość.</span><span class="sxs-lookup"><span data-stu-id="901c2-134">Save this value.</span></span>

4. <span data-ttu-id="901c2-135">Przypisz hello **właściciela** roli: toohello nazwy głównej usługi przy użyciu hello **obiektu o identyfikatorze** wartość.</span><span class="sxs-lookup"><span data-stu-id="901c2-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="901c2-136">Użyj hello **identyfikator subskrypcji** uzyskanymi wcześniej.</span><span class="sxs-lookup"><span data-stu-id="901c2-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="901c2-137">Uzyskiwanie tokenu uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="901c2-137">Get an authentication token</span></span>

<span data-ttu-id="901c2-138">Użyj hello następujące polecenia tooretrieve tokenu uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="901c2-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="901c2-139">Ustaw `$TENANTID`, `$APPID`, i `$PASSWORD` wartości toohello uzyskany lub użyte wcześniej.</span><span class="sxs-lookup"><span data-stu-id="901c2-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="901c2-140">Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i hello treść odpowiedzi zawiera dokument JSON.</span><span class="sxs-lookup"><span data-stu-id="901c2-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="901c2-141">Witaj dokumentu JSON zwróconych przez to żądanie zawiera element o nazwie **' access_token '**.</span><span class="sxs-lookup"><span data-stu-id="901c2-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="901c2-142">Witaj wartość **' access_token '** jest używane tooauthentication toohello żądania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="901c2-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="901c2-143">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="901c2-143">Create a resource group</span></span>

<span data-ttu-id="901c2-144">Użyj powitania po toocreate grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="901c2-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="901c2-145">Ustaw `$SUBSCRIPTIONID` toohello identyfikator subskrypcji otrzymanych podczas tworzenia hello nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="901c2-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="901c2-146">Ustaw `$ACCESSTOKEN` token dostępu toohello Odebrano hello poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="901c2-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="901c2-147">Zastąp `DATACENTERLOCATION` z centrum danych hello ma grupy zasobów hello toocreate i zasobów, w.</span><span class="sxs-lookup"><span data-stu-id="901c2-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="901c2-148">Na przykład "południowo-środkowe Stany".</span><span class="sxs-lookup"><span data-stu-id="901c2-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="901c2-149">Ustaw `$RESOURCEGROUPNAME` nazwę toohello, mają toouse dla tej grupy:</span><span class="sxs-lookup"><span data-stu-id="901c2-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="901c2-150">Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i hello treść odpowiedzi zawiera dokument JSON zawierający informacje o grupie hello.</span><span class="sxs-lookup"><span data-stu-id="901c2-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="901c2-151">Witaj `"provisioningState"` element zawiera wartość `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="901c2-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="901c2-152">Tworzenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="901c2-152">Create a deployment</span></span>

<span data-ttu-id="901c2-153">Użyj hello następujące polecenie grupy zasobów toohello toodeploy hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="901c2-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="901c2-154">Ustaw `$DEPLOYMENTNAME` nazwę toohello, mają toouse dla tego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="901c2-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="901c2-155">Zapisanie pliku tooa szablonu hello, można użyć hello następujące polecenie, a nie `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="901c2-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="901c2-156">Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i hello treść odpowiedzi zawiera dokument JSON zawierający informacje o operacji wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="901c2-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="901c2-157">wdrożenie Hello zostało przesłane, ale nie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="901c2-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="901c2-158">Może upłynąć kilka minut, zazwyczaj około 15 hello toocomplete wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="901c2-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="901c2-159">Sprawdź stan hello wdrożenia</span><span class="sxs-lookup"><span data-stu-id="901c2-159">Check hello status of a deployment</span></span>

<span data-ttu-id="901c2-160">Stan hello toocheck hello wdrożenia, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="901c2-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="901c2-161">To polecenie zwraca zawierający informacje o operacji wdrażania hello dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="901c2-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="901c2-162">Witaj `"provisioningState"` element zawiera stan hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="901c2-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="901c2-163">Jeśli ten element zawiera wartość `"Succeeded"`, następnie hello wdrożenia została pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="901c2-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="901c2-164">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="901c2-164">Troubleshoot</span></span>

<span data-ttu-id="901c2-165">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="901c2-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="901c2-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="901c2-166">Next steps</span></span>

<span data-ttu-id="901c2-167">Po pomyślnym utworzeniu klastra usługi HDInsight, za pomocą powitania po toolearn jak toowork z klastrem.</span><span class="sxs-lookup"><span data-stu-id="901c2-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="901c2-168">Klastry Hadoop</span><span class="sxs-lookup"><span data-stu-id="901c2-168">Hadoop clusters</span></span>

* [<span data-ttu-id="901c2-169">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="901c2-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="901c2-170">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="901c2-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="901c2-171">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="901c2-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="901c2-172">Klastrów HBase</span><span class="sxs-lookup"><span data-stu-id="901c2-172">HBase clusters</span></span>

* [<span data-ttu-id="901c2-173">Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="901c2-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="901c2-174">Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="901c2-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="901c2-175">Klastry STORM</span><span class="sxs-lookup"><span data-stu-id="901c2-175">Storm clusters</span></span>

* [<span data-ttu-id="901c2-176">Tworzenie topologii Java dla Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="901c2-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="901c2-177">Użyj składników języka Python w Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="901c2-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="901c2-178">Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="901c2-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
