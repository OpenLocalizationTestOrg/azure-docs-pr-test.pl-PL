---
title: "Tworzenie klastra sieci szkieletowej usług na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć klaster systemu Windows lub Linux Service Fabric na platformie Azure przy użyciu programu PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: f62249417552b9cf840bfac3b94c27f63bd7064e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="399bd-103">Tworzenie bezpiecznej klastra na platformie Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="399bd-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="399bd-104">W tym samouczku przedstawiono sposób tworzenia klastra usługi sieć szkieletowa (Windows lub Linux) działają na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="399bd-104">This tutorial shows you how to create a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="399bd-105">Po zakończeniu, masz działającą w chmurze, które można wdrożyć aplikacji do klastra.</span><span class="sxs-lookup"><span data-stu-id="399bd-105">When you're finished, you have a cluster running in the cloud that you can deploy applications to.</span></span>

<span data-ttu-id="399bd-106">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="399bd-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="399bd-107">Tworzenie bezpiecznej klastra sieci szkieletowej usług na platformie Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="399bd-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="399bd-108">Zabezpieczanie klastra za pomocą certyfikatu X.509</span><span class="sxs-lookup"><span data-stu-id="399bd-108">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="399bd-109">Nawiązywanie połączenia z klastrem przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="399bd-109">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="399bd-110">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="399bd-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="399bd-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="399bd-111">Prerequisites</span></span>
<span data-ttu-id="399bd-112">Przed rozpoczęciem tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="399bd-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="399bd-113">Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="399bd-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="399bd-114">Zainstaluj [modułu zestawu SDK usług sieci szkieletowej i programu PowerShell](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="399bd-114">Install the [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="399bd-115">Zainstaluj [programu Azure Powershell w wersji modułu 4.1 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="399bd-115">Install the [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="399bd-116">Poniższa procedura tworzy Podgląd (jednej maszyny wirtualnej) jednowęzłowy klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="399bd-116">The following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="399bd-117">Klaster jest chroniony przez certyfikatu z podpisem własnym, który pobiera utworzona wraz z klastra, a następnie są umieszczane w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="399bd-117">The cluster is secured by a self-signed certificate that gets created along with the cluster and then placed in a key vault.</span></span> <span data-ttu-id="399bd-118">Nie może zostać przeskalowana jednowęzłowych poza jedną maszynę wirtualną i Podgląd klastrów nie można uaktualnić do nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="399bd-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded to newer versions.</span></span>

<span data-ttu-id="399bd-119">Aby obliczyć kosztów ponoszonych przez uruchomienie klastra sieci szkieletowej usług Azure używana [Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="399bd-119">To calculate cost incurred by running a Service Fabric cluster in Azure use the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="399bd-120">Aby uzyskać więcej informacji na temat tworzenia klastrów sieci szkieletowej usług, zobacz [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="399bd-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-the-cluster-using-azure-powershell"></a><span data-ttu-id="399bd-121">Tworzenie klastra przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="399bd-121">Create the cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="399bd-122">Pobierz kopię lokalną szablonu usługi Azure Resource Manager i pliku parametrów z [szablon Menedżera zasobów Azure dla platformy Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="399bd-122">Download a local copy of the Azure Resource Manager template and the parameter file from the [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="399bd-123">*azuredeploy.JSON* jest szablonu usługi Azure Resource Manager, który definiuje klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="399bd-123">*azuredeploy.json* is the Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="399bd-124">*azuredeploy.parameters.JSON* jest plikiem parametry umożliwiające dostosowywanie wdrożenia klastra.</span><span class="sxs-lookup"><span data-stu-id="399bd-124">*azuredeploy.parameters.json* is a parameters file for you to customize the cluster deployment.</span></span>

2. <span data-ttu-id="399bd-125">Następujące parametry w *azuredeploy.parameters.json* pliku parametrów:</span><span class="sxs-lookup"><span data-stu-id="399bd-125">Customize the following parameters in the *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="399bd-126">Parametr</span><span class="sxs-lookup"><span data-stu-id="399bd-126">Parameter</span></span>       | <span data-ttu-id="399bd-127">Opis</span><span class="sxs-lookup"><span data-stu-id="399bd-127">Description</span></span> | <span data-ttu-id="399bd-128">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="399bd-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="399bd-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="399bd-129">clusterLocation</span></span> | <span data-ttu-id="399bd-130">Region platformy Azure, dla której chcesz wdrożyć w klastrze.</span><span class="sxs-lookup"><span data-stu-id="399bd-130">The Azure region to which to deploy the cluster.</span></span> | <span data-ttu-id="399bd-131">*na przykład westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="399bd-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="399bd-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="399bd-132">clusterName</span></span>     | <span data-ttu-id="399bd-133">Nazwa klastra, który chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="399bd-133">Name of the cluster you want to create.</span></span> | <span data-ttu-id="399bd-134">*na przykład komputer1 sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="399bd-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="399bd-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="399bd-135">adminUserName</span></span>   | <span data-ttu-id="399bd-136">Konto administratora lokalnego na maszynach wirtualnych w klastrze.</span><span class="sxs-lookup"><span data-stu-id="399bd-136">The local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="399bd-137">*Wszelkie prawidłowej nazwy użytkownika systemu Windows Server*</span><span class="sxs-lookup"><span data-stu-id="399bd-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="399bd-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="399bd-138">adminPassword</span></span>   | <span data-ttu-id="399bd-139">Hasło konta administratora lokalnego na maszynach wirtualnych w klastrze.</span><span class="sxs-lookup"><span data-stu-id="399bd-139">Password of the local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="399bd-140">*Wszystkie prawidłowe hasło systemu Windows Server*</span><span class="sxs-lookup"><span data-stu-id="399bd-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="399bd-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="399bd-141">clusterCodeVersion</span></span> | <span data-ttu-id="399bd-142">Wersja usługi sieć szkieletowa usług do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="399bd-142">The Service Fabric version to run.</span></span> <span data-ttu-id="399bd-143">(255.255.X.255 są wersji zapoznawczych).</span><span class="sxs-lookup"><span data-stu-id="399bd-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="399bd-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="399bd-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="399bd-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="399bd-145">vmInstanceCount</span></span> | <span data-ttu-id="399bd-146">Liczba maszyn wirtualnych w klastrze (może być 1 lub 3-99).</span><span class="sxs-lookup"><span data-stu-id="399bd-146">The number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="399bd-147">**1**</span><span class="sxs-lookup"><span data-stu-id="399bd-147">**1**</span></span> | <span data-ttu-id="399bd-148">*W przypadku klastra w wersji zapoznawczej określić tylko jednej maszyny wirtualnej*</span><span class="sxs-lookup"><span data-stu-id="399bd-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="399bd-149">Otwórz konsolę programu PowerShell, logowanie do platformy Azure i wybierz subskrypcję, którą chcesz wdrożyć w klastrze:</span><span class="sxs-lookup"><span data-stu-id="399bd-149">Open a PowerShell console, login to Azure, and select the subscription you want to deploy the cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="399bd-150">Utwórz i szyfrowania hasło dla certyfikatu, który ma być używany przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="399bd-150">Create and encrypt a password for the certificate to be used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="399bd-151">Tworzenie klastra i jego certyfikat, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="399bd-151">Create the cluster and its certificate by running the following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="399bd-152">`-CertificateSubjectName` Parametru powinno odpowiadać parametr clusterName określony w pliku parametrów, a także domeny powiązane region platformy Azure została wybrana opcja, takich jak: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="399bd-152">The `-CertificateSubjectName` parameter should align with the clusterName parameter specified in the parameters file, as well as the domain tied to the Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="399bd-153">Po zakończeniu konfiguracji generuje informacje o klastrze utworzona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="399bd-153">Once the configuration finishes, it outputs information about the cluster created in Azure.</span></span> <span data-ttu-id="399bd-154">Kopiuje również certyfikat klastra katalogu - CertificateOutputFolder na ścieżkę, którą określono dla tego parametru.</span><span class="sxs-lookup"><span data-stu-id="399bd-154">It also copies the cluster certificate to the -CertificateOutputFolder directory on the path you specified for this parameter.</span></span> <span data-ttu-id="399bd-155">Należy na dostęp do Eksploratora usługi sieć szkieletowa i wyświetlić informacje o kondycji klastra tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="399bd-155">You need this certificate to access Service Fabric Explorer and view the health of your cluster.</span></span>

<span data-ttu-id="399bd-156">Zanotuj adres URL dla klastra, które mogą być podobne do następującego adresu URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="399bd-156">Take note of the URL for your cluster, which may be similar to the following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-the-certificate--access-service-fabric-explorer"></a><span data-ttu-id="399bd-157">Dostęp do Eksploratora usługi sieć szkieletowa & zmienić certyfikat</span><span class="sxs-lookup"><span data-stu-id="399bd-157">Modify the certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="399bd-158">Kliknij dwukrotnie certyfikat, aby otworzyć Kreatora importu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="399bd-158">Double-click the certificate to open the Certificate Import Wizard.</span></span>

2. <span data-ttu-id="399bd-159">Użyj ustawień domyślnych, ale pamiętaj sprawdzić **Oznacz ten klucz jako eksportowalny.**</span><span class="sxs-lookup"><span data-stu-id="399bd-159">Use default settings, but make sure to check the **Mark this key as exportable.**</span></span> <span data-ttu-id="399bd-160">należy zaznaczyć pole wyboru, w **ochrony klucza prywatnego** kroku.</span><span class="sxs-lookup"><span data-stu-id="399bd-160">check box, in the **private key protection** step.</span></span> <span data-ttu-id="399bd-161">Program Visual Studio musi wyeksportować certyfikat podczas konfigurowania rejestru kontenera Azure do uwierzytelniania klastra sieci szkieletowej usług w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="399bd-161">Visual Studio needs to export the certificate when configuring Azure Container Registry to Service Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="399bd-162">Teraz możesz otworzyć Eksploratora usługi sieć szkieletowa w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="399bd-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="399bd-163">Aby to zrobić, przejdź do **ManagementEndpoint** adres URL dla klastra przy użyciu przeglądarki sieci web i wybierz certyfikat, który został zapisany na komputerze.</span><span class="sxs-lookup"><span data-stu-id="399bd-163">To do so, navigate to the **ManagementEndpoint** URL for your cluster using a web browser, and select the certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="399bd-164">Podczas otwierania Service Fabric Explorer, zobacz błąd certyfikatu, ponieważ używasz certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="399bd-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="399bd-165">W programie Edge, trzeba kliknąć *szczegóły* , a następnie *przejdź do strony sieci Web* łącza.</span><span class="sxs-lookup"><span data-stu-id="399bd-165">In Edge, you have to click *Details* and then the *Go on to the webpage* link.</span></span> <span data-ttu-id="399bd-166">W przeglądarce Chrome, trzeba kliknąć *zaawansowane* , a następnie *kontynuować* łącza.</span><span class="sxs-lookup"><span data-stu-id="399bd-166">In Chrome, you have to click *Advanced* and then the *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="399bd-167">W przypadku niepowodzenia tworzenia klastra należy zawsze uruchamiaj ponownie polecenie, które aktualizuje zasoby już wdrożone.</span><span class="sxs-lookup"><span data-stu-id="399bd-167">If the cluster creation fails, you can always rerun the command, which updates the resources already deployed.</span></span> <span data-ttu-id="399bd-168">Jeśli certyfikat został utworzony jako część wdrożenia nie powiodło się, zostanie wygenerowany nowy.</span><span class="sxs-lookup"><span data-stu-id="399bd-168">If a certificate was created as part of the failed deployment, a new one is generated.</span></span> <span data-ttu-id="399bd-169">Aby rozwiązać tworzenia klastra, zobacz [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="399bd-169">To troubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-to-the-secure-cluster"></a><span data-ttu-id="399bd-170">Połącz się z klastrem bezpieczne</span><span class="sxs-lookup"><span data-stu-id="399bd-170">Connect to the secure cluster</span></span>
<span data-ttu-id="399bd-171">Połącz z klastrem przy użyciu modułu programu PowerShell usługi Service Fabric zainstalowany przy użyciu zestawu SDK sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="399bd-171">Connect to the cluster using the Service Fabric PowerShell module installed with the Service Fabric SDK.</span></span>  <span data-ttu-id="399bd-172">Najpierw zainstaluj certyfikat do magazynu osobistego (Mój) bieżącego użytkownika na komputerze.</span><span class="sxs-lookup"><span data-stu-id="399bd-172">First, install the certificate into the Personal (My) store of the current user on your computer.</span></span>  <span data-ttu-id="399bd-173">Uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="399bd-173">Run the following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="399bd-174">Teraz możesz przystąpić do nawiązywania połączenia z zabezpieczonym klastrem.</span><span class="sxs-lookup"><span data-stu-id="399bd-174">You are now ready to connect to your secure cluster.</span></span>

<span data-ttu-id="399bd-175">**Sieci szkieletowej usług** modułu programu PowerShell zawiera wiele poleceń cmdlet do zarządzania klastrami, aplikacji i usług sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="399bd-175">The **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="399bd-176">Użyj [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) polecenia cmdlet, aby połączyć się z klastrem bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="399bd-176">Use the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet to connect to the secure cluster.</span></span> <span data-ttu-id="399bd-177">Szczegóły punktu końcowego połączenia i odcisk palca certyfikatu można znaleźć w danych wyjściowych z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="399bd-177">The certificate thumbprint and connection endpoint details are found in the output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="399bd-178">Sprawdź, czy nawiązano połączenie i klastra jest w dobrej kondycji za pomocą [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="399bd-178">Check that you are connected and the cluster is healthy using the [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="399bd-179">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="399bd-179">Clean up resources</span></span>

<span data-ttu-id="399bd-180">Klaster składa się z innych zasobów platformy Azure poza samym zasobem klastra.</span><span class="sxs-lookup"><span data-stu-id="399bd-180">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="399bd-181">Najprostszym sposobem na usunięcie klastra i wszystkich wykorzystywanych przez niego zasobów jest usunięcie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="399bd-181">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span>

<span data-ttu-id="399bd-182">Logowanie do platformy Azure i wybierz identyfikator subskrypcji, z którą chcesz usunąć klaster.</span><span class="sxs-lookup"><span data-stu-id="399bd-182">Log in to Azure and select the subscription ID with which you want to remove the cluster.</span></span>  <span data-ttu-id="399bd-183">Identyfikator subskrypcji można znaleźć po zalogowaniu się do [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="399bd-183">You can find your subscription ID by logging in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="399bd-184">Usuń grupę zasobów i zasobów klastra przy użyciu [polecenia cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="399bd-184">Delete the resource group and all the cluster resources using the [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="399bd-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="399bd-185">Next steps</span></span>
<span data-ttu-id="399bd-186">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="399bd-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="399bd-187">Tworzenie klastra sieci szkieletowej usług na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="399bd-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="399bd-188">Zabezpieczanie klastra za pomocą certyfikatu X.509</span><span class="sxs-lookup"><span data-stu-id="399bd-188">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="399bd-189">Nawiązywanie połączenia z klastrem przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="399bd-189">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="399bd-190">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="399bd-190">Remove a cluster</span></span>

<span data-ttu-id="399bd-191">Następnie przejdź do następujących samouczkiem, aby dowiedzieć się, jak wdrożyć istniejącą aplikację.</span><span class="sxs-lookup"><span data-stu-id="399bd-191">Next, advance to the following tutorial to learn how to deploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="399bd-192">Wdrażanie istniejącą aplikację .NET z rozwiązania Docker Compose</span><span class="sxs-lookup"><span data-stu-id="399bd-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
