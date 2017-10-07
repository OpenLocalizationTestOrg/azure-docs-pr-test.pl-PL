---
title: "aaaCreate usługi sieć szkieletowa klastra na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate systemu Windows lub Linux Service Fabric klastra na platformie Azure przy użyciu programu PowerShell."
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
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="ef098-103">Tworzenie bezpiecznej klastra na platformie Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef098-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="ef098-104">Ten samouczek pokazuje, jak toocreate usługi sieć szkieletowa klastra (z systemem Windows lub Linux) w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="ef098-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="ef098-105">Po zakończeniu, masz klastra z systemem w chmurze hello, którą można wdrożyć aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ef098-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="ef098-106">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ef098-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ef098-107">Tworzenie bezpiecznej klastra sieci szkieletowej usług na platformie Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef098-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="ef098-108">Zabezpieczanie klastra hello za pomocą certyfikatu X.509</span><span class="sxs-lookup"><span data-stu-id="ef098-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="ef098-109">Połącz toohello klastra przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef098-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="ef098-110">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="ef098-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef098-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ef098-111">Prerequisites</span></span>
<span data-ttu-id="ef098-112">Przed rozpoczęciem tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="ef098-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="ef098-113">Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="ef098-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="ef098-114">Zainstaluj hello [modułu zestawu SDK usług sieci szkieletowej i programu PowerShell](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="ef098-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="ef098-115">Zainstaluj hello [programu Azure Powershell w wersji modułu 4.1 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="ef098-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="ef098-116">Witaj procedury tworzy Podgląd (jednej maszyny wirtualnej) jednowęzłowy klaster sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="ef098-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="ef098-117">klaster Hello jest zabezpieczony przez certyfikatu z podpisem własnym, który pobiera utworzony wraz hello klastra, a następnie są umieszczane w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="ef098-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="ef098-118">Nie może zostać przeskalowana jednowęzłowych poza jedną maszynę wirtualną i klastrów w wersji zapoznawczej nie może być toonewer uaktualnionej wersji.</span><span class="sxs-lookup"><span data-stu-id="ef098-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="ef098-119">toocalculate kosztów ponoszonych przez uruchomienie klastra sieci szkieletowej usług w hello Azure użyj [Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="ef098-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="ef098-120">Aby uzyskać więcej informacji na temat tworzenia klastrów sieci szkieletowej usług, zobacz [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ef098-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="ef098-121">Tworzenie klastra hello przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef098-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="ef098-122">Pobierz kopię lokalną hello szablonu usługi Azure Resource Manager i pliku parametrów hello z hello [szablon Menedżera zasobów Azure dla platformy Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="ef098-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="ef098-123">*azuredeploy.JSON* jest hello szablonu usługi Azure Resource Manager, który definiuje klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="ef098-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="ef098-124">*azuredeploy.parameters.JSON* pliku parametrów dla użytkowników jest wdrożenie klastra hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="ef098-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="ef098-125">Dostosowywanie hello następujące parametry w hello *azuredeploy.parameters.json* pliku parametrów:</span><span class="sxs-lookup"><span data-stu-id="ef098-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="ef098-126">Parametr</span><span class="sxs-lookup"><span data-stu-id="ef098-126">Parameter</span></span>       | <span data-ttu-id="ef098-127">Opis</span><span class="sxs-lookup"><span data-stu-id="ef098-127">Description</span></span> | <span data-ttu-id="ef098-128">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="ef098-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="ef098-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="ef098-129">clusterLocation</span></span> | <span data-ttu-id="ef098-130">Witaj regionu Azure toowhich toodeploy hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ef098-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="ef098-131">*na przykład westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="ef098-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="ef098-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="ef098-132">clusterName</span></span>     | <span data-ttu-id="ef098-133">Nazwa klastra hello ma toocreate.</span><span class="sxs-lookup"><span data-stu-id="ef098-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="ef098-134">*na przykład komputer1 sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="ef098-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="ef098-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="ef098-135">adminUserName</span></span>   | <span data-ttu-id="ef098-136">Hello konto administratora lokalnego na maszynach wirtualnych hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ef098-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="ef098-137">*Wszelkie prawidłowej nazwy użytkownika systemu Windows Server*</span><span class="sxs-lookup"><span data-stu-id="ef098-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="ef098-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="ef098-138">adminPassword</span></span>   | <span data-ttu-id="ef098-139">Hasło konta administratora lokalnego hello na powitania klastrowanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ef098-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="ef098-140">*Wszystkie prawidłowe hasło systemu Windows Server*</span><span class="sxs-lookup"><span data-stu-id="ef098-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="ef098-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="ef098-141">clusterCodeVersion</span></span> | <span data-ttu-id="ef098-142">Witaj toorun wersji platformy Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ef098-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="ef098-143">(255.255.X.255 są wersji zapoznawczych).</span><span class="sxs-lookup"><span data-stu-id="ef098-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="ef098-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="ef098-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="ef098-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="ef098-145">vmInstanceCount</span></span> | <span data-ttu-id="ef098-146">Witaj liczbę maszyn wirtualnych w klastrze (może być 1 lub 3-99).</span><span class="sxs-lookup"><span data-stu-id="ef098-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="ef098-147">**1**</span><span class="sxs-lookup"><span data-stu-id="ef098-147">**1**</span></span> | <span data-ttu-id="ef098-148">*W przypadku klastra w wersji zapoznawczej określić tylko jednej maszyny wirtualnej*</span><span class="sxs-lookup"><span data-stu-id="ef098-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="ef098-149">Otwórz konsolę programu PowerShell, tooAzure logowania, a następnie wybierz subskrypcję hello, który ma toodeploy hello klastra w:</span><span class="sxs-lookup"><span data-stu-id="ef098-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="ef098-150">Utwórz i szyfrowania hasła dla hello toobe certyfikat używany przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="ef098-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="ef098-151">Tworzenie klastra hello i jego certyfikat, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ef098-151">Create hello cluster and its certificate by running hello following command:</span></span>

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
   ><span data-ttu-id="ef098-152">Witaj `-CertificateSubjectName` parametru powinno odpowiadać parametr NazwaKlastra hello określony w pliku parametrów hello, jak również jako hello toohello domeny powiązane region platformy Azure została wybrana opcja, takich jak: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ef098-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="ef098-153">Po zakończeniu konfiguracji hello generuje informacje o klastrze hello utworzona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ef098-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="ef098-154">Kopiuje hello klastra certyfikatu toohello - CertificateOutputFolder katalogu na powitania ścieżka określona dla tego parametru.</span><span class="sxs-lookup"><span data-stu-id="ef098-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="ef098-155">Należy to tooaccess certyfikat kondycji hello Service Fabric Explorer i Widok klastra.</span><span class="sxs-lookup"><span data-stu-id="ef098-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="ef098-156">Zanotuj adres URL klastra, który może być podobne toohello hello następującego adresu URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="ef098-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="ef098-157">Dostęp do Eksploratora usługi sieć szkieletowa & modyfikowanie hello certyfikatu</span><span class="sxs-lookup"><span data-stu-id="ef098-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="ef098-158">Kliknij dwukrotnie hello certyfikatu tooopen hello Kreatora importu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="ef098-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="ef098-159">Użyj ustawień domyślnych, ale upewnij się, że hello toocheck **Oznacz ten klucz jako eksportowalny.**</span><span class="sxs-lookup"><span data-stu-id="ef098-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="ef098-160">pole wyboru w hello **ochrony klucza prywatnego** kroku.</span><span class="sxs-lookup"><span data-stu-id="ef098-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="ef098-161">Program Visual Studio musi tooexport hello certyfikatu podczas konfigurowania uwierzytelniania klastra sieci szkieletowej tooService rejestru kontenera platformy Azure w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="ef098-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="ef098-162">Teraz możesz otworzyć Eksploratora usługi sieć szkieletowa w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ef098-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="ef098-163">toodo tak, przejdź toohello **ManagementEndpoint** adres URL dla klastra przy użyciu przeglądarki sieci web i hello wybierz certyfikat, który został zapisany na komputerze.</span><span class="sxs-lookup"><span data-stu-id="ef098-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="ef098-164">Podczas otwierania Service Fabric Explorer, zobacz błąd certyfikatu, ponieważ używasz certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="ef098-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="ef098-165">W programie Edge, masz tooclick *szczegóły* , a następnie hello *przejdź na stronę sieci Web toohello* łącza.</span><span class="sxs-lookup"><span data-stu-id="ef098-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="ef098-166">W przeglądarce Chrome, masz tooclick *zaawansowane* , a następnie hello *kontynuować* łącza.</span><span class="sxs-lookup"><span data-stu-id="ef098-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="ef098-167">W przypadku niepowodzenia tworzenia klastra hello zawsze można ponownie uruchomić polecenie hello aktualizacji zasobów hello już wdrożone.</span><span class="sxs-lookup"><span data-stu-id="ef098-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="ef098-168">Jeśli certyfikat został utworzony jako część wdrożenia hello nie powiodło się, zostanie wygenerowany nowy.</span><span class="sxs-lookup"><span data-stu-id="ef098-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="ef098-169">Tworzenie klastra tootroubleshoot, zobacz [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ef098-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="ef098-170">Połącz toohello bezpiecznego klastra</span><span class="sxs-lookup"><span data-stu-id="ef098-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="ef098-171">Połącz toohello klastra przy użyciu modułu PowerShell sieci szkieletowej usług hello z hello zestawu SDK usług sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="ef098-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="ef098-172">Najpierw zainstaluj hello certyfikatu do magazynu osobistego (Mój) hello hello bieżącego użytkownika na komputerze.</span><span class="sxs-lookup"><span data-stu-id="ef098-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="ef098-173">Uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="ef098-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="ef098-174">Wszystko jest teraz gotowy tooconnect tooyour bezpiecznego klastra.</span><span class="sxs-lookup"><span data-stu-id="ef098-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="ef098-175">Witaj **sieci szkieletowej usług** modułu programu PowerShell zawiera wiele poleceń cmdlet do zarządzania klastrami, aplikacji i usług sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="ef098-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="ef098-176">Użyj hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) polecenia cmdlet tooconnect toohello bezpiecznego klastra.</span><span class="sxs-lookup"><span data-stu-id="ef098-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="ef098-177">Witaj odcisk palca certyfikatu i szczegóły punktu końcowego połączenia można znaleźć w danych wyjściowych hello z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="ef098-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="ef098-178">Sprawdź, czy nawiązano połączenie i hello klastra jest w dobrej kondycji, przy użyciu hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef098-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="ef098-179">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="ef098-179">Clean up resources</span></span>

<span data-ttu-id="ef098-180">Klaster składa się z innych zasobów platformy Azure oprócz zasobu klastra toohello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="ef098-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="ef098-181">Hello najprostszy sposób toodelete hello klaster i wszystkie zużywanych zasobach hello jest grupa zasobów hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="ef098-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="ef098-182">Zaloguj się za tooAzure i wybierz hello identyfikator subskrypcji, z którym ma zostać tooremove hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ef098-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="ef098-183">Identyfikator subskrypcji można znaleźć po zalogowaniu się toohello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef098-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ef098-184">Usuń grupę zasobów hello i wszystkich zasobów klastra hello przy użyciu hello [polecenia cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="ef098-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="ef098-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef098-185">Next steps</span></span>
<span data-ttu-id="ef098-186">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ef098-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ef098-187">Tworzenie klastra sieci szkieletowej usług na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ef098-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="ef098-188">Zabezpieczanie klastra hello za pomocą certyfikatu X.509</span><span class="sxs-lookup"><span data-stu-id="ef098-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="ef098-189">Połącz toohello klastra przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef098-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="ef098-190">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="ef098-190">Remove a cluster</span></span>

<span data-ttu-id="ef098-191">Następnie poprawić toohello po toolearn samouczek jak toodeploy istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ef098-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ef098-192">Wdrażanie istniejącą aplikację .NET z rozwiązania Docker Compose</span><span class="sxs-lookup"><span data-stu-id="ef098-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
