---
title: "Tworzenie klastrów platformy Hadoop za pomocą usługi Azure API REST - Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia klastrów usługi HDInsight poprzez przesłanie szablonów usługi Azure Resource Manager w interfejsie API REST Azure."
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
ms.openlocfilehash: a36a41c231472ceeeb46d02ddb65549b1c79728a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="92b59-103">Tworzenie klastrów Hadoop przy użyciu interfejsu API REST Azure</span><span class="sxs-lookup"><span data-stu-id="92b59-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="92b59-104">Informacje o sposobie tworzenia klastra usługi HDInsight przy użyciu szablonu usługi Azure Resource Manager i interfejsu API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="92b59-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="92b59-105">Interfejs API REST Azure umożliwia wykonywanie operacji zarządzania na usługi hostowanej na platformie Azure, w tym tworzenie nowych zasobów, takich jak klastry usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="92b59-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92b59-106">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="92b59-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="92b59-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="92b59-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="92b59-108">Użyj dokumentów z krokami w tym [curl (https://curl.haxx.se/)](https://curl.haxx.se/) narzędzie do komunikowania się z interfejsu API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="92b59-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="92b59-109">Tworzenie szablonu</span><span class="sxs-lookup"><span data-stu-id="92b59-109">Create a template</span></span>

<span data-ttu-id="92b59-110">Szablony usługi Azure Resource Manager są dokumentów JSON, które opisują **grupy zasobów** i wszystkie zasoby w niej (np. usługi HDInsight). Takie podejście oparty na szablonie można zdefiniować zasoby potrzebne dla usługi HDInsight w jednym szablonie.</span><span class="sxs-lookup"><span data-stu-id="92b59-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="92b59-111">Następujący dokument JSON jest połączenie z plików szablonu i parametry [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), który jest tworzony klaster opartych na systemie Linux przy użyciu hasła, aby zabezpieczyć konto użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="92b59-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

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
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to remotely access the cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
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

<span data-ttu-id="92b59-112">W tym przykładzie jest używany w procedurze w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="92b59-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="92b59-113">Zastąp przykładzie *wartości* w **parametry** sekcji z wartościami dla klastra.</span><span class="sxs-lookup"><span data-stu-id="92b59-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92b59-114">Szablon używa domyślna liczba węzłów procesu roboczego (4) do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="92b59-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="92b59-115">Jeśli planujesz na więcej niż 32 węzłami procesów roboczych, musi wybierz rozmiar węzła głównego z co najmniej 8 rdzeni i 14 GB pamięci ram.</span><span class="sxs-lookup"><span data-stu-id="92b59-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="92b59-116">Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="92b59-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="92b59-117">Logowanie się do subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="92b59-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="92b59-118">Wykonaj kroki opisane w temacie [wprowadzenie Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) i nawiązać połączenia z subskrypcją za pomocą `az login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="92b59-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="92b59-119">Tworzenie nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="92b59-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="92b59-120">Te kroki są skróconej wersji *Tworzenie nazwy głównej usługi z hasłem* sekcji [Użyj wiersza polecenia platformy Azure można utworzyć nazwy głównej usługi dostępu do zasobów](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="92b59-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="92b59-121">Te kroki tworzenia nazwy głównej usługi, który jest używany do uwierzytelniania interfejsu API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="92b59-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="92b59-122">Z wiersza polecenia użyj następującego polecenia, aby wyświetlić listę subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="92b59-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="92b59-123">Na liście, wybierz subskrypcję, którą chcesz używać i zanotuj **IDENTYFIKATOR_SUBSKRYPCJI** i __Tenant_ID__ kolumn.</span><span class="sxs-lookup"><span data-stu-id="92b59-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="92b59-124">Zapisz te wartości.</span><span class="sxs-lookup"><span data-stu-id="92b59-124">Save these values.</span></span>

2. <span data-ttu-id="92b59-125">Użyj następującego polecenia, aby utworzyć aplikację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92b59-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="92b59-126">Zastąp wartości `--display-name`, `--homepage`, i `--identifier-uris` z własne wartości.</span><span class="sxs-lookup"><span data-stu-id="92b59-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="92b59-127">Podaj hasło dla nowego wpisu usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="92b59-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="92b59-128">`--home-page` i `--identifier-uris` wartości nie ma potrzeby odwołać rzeczywistej stronie sieci web hostowanych w Internecie.</span><span class="sxs-lookup"><span data-stu-id="92b59-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="92b59-129">Klienci muszą mieć unikatowe identyfikatory URI.</span><span class="sxs-lookup"><span data-stu-id="92b59-129">They must be unique URIs.</span></span>

   <span data-ttu-id="92b59-130">Wartość zwracana z tego polecenia jest __identyfikator aplikacji__ nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92b59-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="92b59-131">Zapisz tę wartość.</span><span class="sxs-lookup"><span data-stu-id="92b59-131">Save this value.</span></span>

3. <span data-ttu-id="92b59-132">Użyj następującego polecenia, aby utworzyć przy użyciu nazwy głównej usługi **identyfikator aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="92b59-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="92b59-133">Wartość zwracana z tego polecenia jest __obiektu o identyfikatorze__.</span><span class="sxs-lookup"><span data-stu-id="92b59-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="92b59-134">Zapisz tę wartość.</span><span class="sxs-lookup"><span data-stu-id="92b59-134">Save this value.</span></span>

4. <span data-ttu-id="92b59-135">Przypisz **właściciela** roli do głównej usługi przy użyciu **obiektu o identyfikatorze** wartość.</span><span class="sxs-lookup"><span data-stu-id="92b59-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="92b59-136">Użyj **identyfikator subskrypcji** uzyskanymi wcześniej.</span><span class="sxs-lookup"><span data-stu-id="92b59-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="92b59-137">Uzyskiwanie tokenu uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="92b59-137">Get an authentication token</span></span>

<span data-ttu-id="92b59-138">Użyj następującego polecenia, aby pobrać tokenu uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="92b59-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="92b59-139">Ustaw `$TENANTID`, `$APPID`, i `$PASSWORD` wartości uzyskane lub użyte wcześniej.</span><span class="sxs-lookup"><span data-stu-id="92b59-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="92b59-140">Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i treść odpowiedzi zawiera dokument JSON.</span><span class="sxs-lookup"><span data-stu-id="92b59-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="92b59-141">Dokument JSON zwróconych przez to żądanie zawiera element o nazwie **' access_token '**.</span><span class="sxs-lookup"><span data-stu-id="92b59-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="92b59-142">Wartość **' access_token '** jest używany do uwierzytelniania żądań interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="92b59-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="92b59-143">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="92b59-143">Create a resource group</span></span>

<span data-ttu-id="92b59-144">Aby utworzyć grupę zasobów, należy użyć następującego.</span><span class="sxs-lookup"><span data-stu-id="92b59-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="92b59-145">Ustaw `$SUBSCRIPTIONID` subskrypcji identyfikator otrzymane podczas tworzenia nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="92b59-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="92b59-146">Ustaw `$ACCESSTOKEN` do tokena dostępu została odebrana w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="92b59-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="92b59-147">Zastąp `DATACENTERLOCATION` przy użyciu chcesz utworzyć grupę zasobów i zasobów, w centrum danych.</span><span class="sxs-lookup"><span data-stu-id="92b59-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="92b59-148">Na przykład "południowo-środkowe Stany".</span><span class="sxs-lookup"><span data-stu-id="92b59-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="92b59-149">Ustaw `$RESOURCEGROUPNAME` na nazwę chcesz użyć dla tej grupy:</span><span class="sxs-lookup"><span data-stu-id="92b59-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="92b59-150">Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i treść odpowiedzi zawiera dokument JSON zawierający informacje o grupie.</span><span class="sxs-lookup"><span data-stu-id="92b59-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="92b59-151">`"provisioningState"` Element zawiera wartość `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="92b59-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="92b59-152">Tworzenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="92b59-152">Create a deployment</span></span>

<span data-ttu-id="92b59-153">Użyj następującego polecenia, aby wdrożyć szablon do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="92b59-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="92b59-154">Ustaw `$DEPLOYMENTNAME` nazwa ma zostać użyty dla tego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="92b59-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="92b59-155">Jeśli szablon został zapisany do pliku, można użyć następującego polecenia zamiast `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="92b59-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="92b59-156">Jeśli to żądanie zakończy się pomyślnie, otrzymasz odpowiedź 200 serii i treść odpowiedzi zawiera dokument JSON zawierający informacje o operacji wdrażania.</span><span class="sxs-lookup"><span data-stu-id="92b59-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92b59-157">Wdrożenie zostało przesłane, ale nie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="92b59-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="92b59-158">Może upłynąć kilka minut, zazwyczaj około 15 dla wdrożenia, aby zakończyć.</span><span class="sxs-lookup"><span data-stu-id="92b59-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="92b59-159">Sprawdź stan wdrożenia</span><span class="sxs-lookup"><span data-stu-id="92b59-159">Check the status of a deployment</span></span>

<span data-ttu-id="92b59-160">Aby sprawdzić stan wdrożenia, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="92b59-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="92b59-161">To polecenie zwraca dokument JSON zawierający informacje o operacji wdrażania.</span><span class="sxs-lookup"><span data-stu-id="92b59-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="92b59-162">`"provisioningState"` Element zawiera stan wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="92b59-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="92b59-163">Jeśli ten element zawiera wartość `"Succeeded"`, a następnie wdrożenie zostało ukończone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="92b59-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="92b59-164">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="92b59-164">Troubleshoot</span></span>

<span data-ttu-id="92b59-165">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="92b59-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="92b59-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="92b59-166">Next steps</span></span>

<span data-ttu-id="92b59-167">Teraz, że pomyślnie utworzono klaster usługi HDInsight, użyj następującego polecenia, aby dowiedzieć się, jak pracować z klastra.</span><span class="sxs-lookup"><span data-stu-id="92b59-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="92b59-168">Klastry Hadoop</span><span class="sxs-lookup"><span data-stu-id="92b59-168">Hadoop clusters</span></span>

* [<span data-ttu-id="92b59-169">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="92b59-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="92b59-170">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="92b59-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="92b59-171">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="92b59-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="92b59-172">Klastrów HBase</span><span class="sxs-lookup"><span data-stu-id="92b59-172">HBase clusters</span></span>

* [<span data-ttu-id="92b59-173">Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="92b59-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="92b59-174">Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="92b59-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="92b59-175">Klastry STORM</span><span class="sxs-lookup"><span data-stu-id="92b59-175">Storm clusters</span></span>

* [<span data-ttu-id="92b59-176">Tworzenie topologii Java dla Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="92b59-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="92b59-177">Użyj składników języka Python w Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="92b59-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="92b59-178">Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="92b59-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
