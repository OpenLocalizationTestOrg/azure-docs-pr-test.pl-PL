---
title: "klastry aaaCreate HDInsight z usługą Data Lake Store jako domyślny magazyn przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell toocreate i klastry usługi HDInsight za pomocą usługi Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="70603-103">Tworzenie klastrów usługi HDInsight z usługą Data Lake Store jako domyślny magazyn przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="70603-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70603-104">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="70603-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="70603-105">Przy użyciu programu PowerShell (do magazynu domyślnego)</span><span class="sxs-lookup"><span data-stu-id="70603-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="70603-106">Przy użyciu programu PowerShell (dla dodatkowego magazynu)</span><span class="sxs-lookup"><span data-stu-id="70603-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="70603-107">Użyj Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="70603-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="70603-108">Dowiedz się, jak toouse tooconfigure programu Azure PowerShell Azure HDInsight clusters z usługi Azure Data Lake Store jako domyślnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="70603-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="70603-109">Aby uzyskać instrukcje dotyczące tworzenia klastra usługi HDInsight z usługą Data Lake Store jako dodatkowego miejsca do magazynowania, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store jako dodatkowego magazynu](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="70603-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="70603-110">Poniżej przedstawiono kilka istotnych kwestii dotyczących z usługą Data Lake Store za pomocą usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="70603-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="70603-111">klastry usługi HDInsight toocreate opcji Hello z dostępem do tooData Lake Store jako domyślny magazyn jest dostępny dla usługi HDInsight w wersji 3.5 i 3,6.</span><span class="sxs-lookup"><span data-stu-id="70603-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="70603-112">toocreate opcja Hello klastrów usługi HDInsight z dostęp tooData Lake Store jako domyślnego magazynu jest *nie jest dostępny* klastrów HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="70603-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="70603-113">tooconfigure toowork HDInsight z usługą Data Lake Store za pomocą programu PowerShell, wykonaj instrukcje hello w sekcjach następnych pięciu hello.</span><span class="sxs-lookup"><span data-stu-id="70603-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70603-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="70603-114">Prerequisites</span></span>
<span data-ttu-id="70603-115">Przed rozpoczęciem tego samouczka, upewnij się, czy zostały spełnione następujące wymagania hello:</span><span class="sxs-lookup"><span data-stu-id="70603-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="70603-116">**Subskrypcja platformy Azure**: Przejdź zbyt[Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70603-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="70603-117">**Program Azure PowerShell 1.0 lub nowszego**: zobacz [jak tooinstall i konfigurowanie programu PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="70603-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="70603-118">**Windows Software Development Kit (SDK)**: tooinstall zestaw Windows SDK, przejdź zbyt[pliki do pobrania i narzędzi dla systemu Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="70603-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="70603-119">Witaj zestawu SDK jest używane toocreate certyfikatu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="70603-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="70603-120">**Nazwy głównej usługi Azure Active Directory**: w tym samouczku opisano sposób toocreate nazwy głównej usługi w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70603-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="70603-121">Jednak toocreate nazwy głównej usługi, musisz być administratorem usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70603-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="70603-122">Jeśli jesteś administratorem, możesz pominąć te wymagania wstępne i kontynuować hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="70603-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="70603-123">Usługi można utworzyć podmiot, tylko wtedy, gdy administrator usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70603-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="70603-124">Administrator usługi Azure AD należy utworzyć usługę podmiotu zabezpieczeń przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="70603-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="70603-125">Witaj nazwy głównej usługi należy utworzyć przy użyciu certyfikatu zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="70603-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="70603-126">Tworzenie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="70603-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="70603-127">Konto usługi Data Lake Store toocreate hello następujące:</span><span class="sxs-lookup"><span data-stu-id="70603-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="70603-128">Na pulpicie otwórz okno programu PowerShell, a następnie wprowadź poniższe fragmenty kodu hello.</span><span class="sxs-lookup"><span data-stu-id="70603-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="70603-129">Jeśli jesteś zostanie wyświetlony monit o toosign w Zaloguj się jako jeden z administratorów subskrypcji hello lub właścicieli.</span><span class="sxs-lookup"><span data-stu-id="70603-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="70603-130">Jeśli rejestrowanie dostawcy zasobów usługi Data Lake Store hello i komunikat o błędzie podobny zbyt`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, subskrypcja może nie być białej dla usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="70603-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="70603-131">tooenable subskrypcji platformy Azure hello usługi Data Lake Store publicznej wersji zapoznawczej, wykonaj te instrukcje hello [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="70603-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="70603-132">Konto usługi Data Lake Store jest skojarzona z grupą zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="70603-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="70603-133">Rozpocznij od utworzenia grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="70603-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="70603-134">Powinny pojawić się dane wyjściowe podobne to:</span><span class="sxs-lookup"><span data-stu-id="70603-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="70603-135">Utwórz konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="70603-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="70603-136">Konto Hello nazwa musi zawierać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="70603-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="70603-137">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="70603-137">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

4. <span data-ttu-id="70603-138">Za pomocą usługi Data Lake Store jako domyślny magazyn wymaga toospecify możesz plików specyficznych dla klastra głównego ścieżki toowhich hello zostały skopiowane podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="70603-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="70603-139">Ścieżka katalogu głównego, który jest toocreate **/klastrów/hdiadlcluster** we fragmencie hello, użyj następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="70603-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="70603-140">Konfigurowanie uwierzytelniania opartego na rolach dostępu tooData Lake — Magazyn</span><span class="sxs-lookup"><span data-stu-id="70603-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="70603-141">Każda subskrypcja platformy Azure jest skojarzony z jednostką usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70603-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="70603-142">Użytkowników i usług, czy dostęp do zasobów subskrypcji przy użyciu portalu Azure hello lub hello interfejsu API usługi Azure Resource Manager muszą najpierw uwierzytelnić w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70603-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="70603-143">Dostęp tooAzure subskrypcji i usług przez przypisywanie ich odpowiednią rolę hello na zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="70603-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="70603-144">W przypadku usług nazwy głównej usługi identyfikuje hello usługi w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70603-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="70603-145">W tej części przedstawiono, jak usługa toogrant aplikacji, takich jak usługi HDInsight, tooan dostępu do zasobów platformy Azure (hello utworzone wcześniej konto usługi Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="70603-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="70603-146">Można to zrobić, tworząc usługi głównej aplikacji hello i przypisywania ról tooit za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="70603-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="70603-147">tooset się uwierzytelnianie usługi Active Directory dla usługi Azure Data Lake wykonywanie zadań hello w hello następujące dwie sekcje.</span><span class="sxs-lookup"><span data-stu-id="70603-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="70603-148">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="70603-148">Create a self-signed certificate</span></span>
<span data-ttu-id="70603-149">Upewnij się, że masz [zestaw Windows SDK](https://dev.windows.com/en-us/downloads) zainstalowany przed rozpoczęciem powitalne kroki opisane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="70603-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="70603-150">Należy także utworzyć katalogu, takie jak *C:\mycertdir*, w którym można utworzyć certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="70603-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="70603-151">W oknie programu PowerShell hello przejść toohello lokalizacji, w której zainstalowany zestaw Windows SDK (zazwyczaj *\Windows Kits\10\bin\x86 C:\Program Files (x86)*) i używać hello [MakeCert] [ makecert] toocreate narzędzie certyfikatu z podpisem własnym oraz klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="70603-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="70603-152">Witaj Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="70603-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="70603-153">Hasło klucza prywatnego hello zostanie wyświetlony monit o tooenter będzie.</span><span class="sxs-lookup"><span data-stu-id="70603-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="70603-154">Po pomyślnym wykonaniu polecenia hello, powinien zostać wyświetlony **CertFile.cer** i **mykey.pvk** w katalogu certyfikatu hello określonym.</span><span class="sxs-lookup"><span data-stu-id="70603-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="70603-155">Użyj hello [Pvk2Pfx] [ pvk2pfx] .pvk hello tooconvert narzędzia i .cer pliki tego pliku pfx utworzony tooa MakeCert.</span><span class="sxs-lookup"><span data-stu-id="70603-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="70603-156">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="70603-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="70603-157">Po wyświetleniu monitu wprowadź hello hasło klucza prywatnego określone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="70603-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="70603-158">wartość określona dla hello Hello **— po** parametru jest hello hasło skojarzone z pliku PFX hello.</span><span class="sxs-lookup"><span data-stu-id="70603-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="70603-159">Po polecenie hello zostało pomyślnie ukończone, należy również wyświetlić **CertFile.pfx** w katalogu certyfikatu hello określonym.</span><span class="sxs-lookup"><span data-stu-id="70603-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="70603-160">Tworzenie usługi Azure AD i nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="70603-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="70603-161">W tej sekcji Tworzenie nazwy głównej usługi dla aplikacji usługi Azure AD, przypisz nazwy głównej usługi roli toohello i Uwierzytelnij się jako nazwy głównej usługi hello zapewniając certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="70603-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="70603-162">toocreate aplikacji w usłudze Azure AD, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="70603-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="70603-163">Wklej hello następującego polecenia cmdlet w oknie konsoli programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="70603-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="70603-164">Upewnij się, tę wartość hello Określ hello **— Nazwa wyświetlana** właściwości jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="70603-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="70603-165">Witaj wartości **— strona główna** i **- IdentiferUris** są symbole zastępcze i nie są weryfikowane.</span><span class="sxs-lookup"><span data-stu-id="70603-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="70603-166">Tworzenie nazwy głównej usługi za pomocą identyfikatora aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="70603-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="70603-167">Udziel katalogu głównego usługi Data Lake Store toohello hello usługi dostępu głównej i wszystkich folderów hello hello ścieżki katalogu głównego, określony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="70603-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="70603-168">Użyj następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="70603-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="70603-169">Tworzenie klastra usługi HDInsight Linux z usługą Data Lake Store jako hello domyślny magazyn</span><span class="sxs-lookup"><span data-stu-id="70603-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="70603-170">W tej sekcji utworzysz klaster usługi HDInsight Hadoop Linux z usługą Data Lake Store jako hello domyślny magazyn.</span><span class="sxs-lookup"><span data-stu-id="70603-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="70603-171">W tej wersji hello klastra usługi HDInsight i Data Lake — Magazyn musi być w hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="70603-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="70603-172">Pobierz identyfikator dzierżawy subskrypcji hello i zapisać go toouse później.</span><span class="sxs-lookup"><span data-stu-id="70603-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="70603-173">Tworzenie klastra usługi HDInsight hello za pomocą następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="70603-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="70603-174">Po pomyślnym zakończeniu hello polecenia cmdlet powinny być widoczne dane wyjściowe z listą hello szczegółów klastra.</span><span class="sxs-lookup"><span data-stu-id="70603-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="70603-175">Uruchom zadania testowe na toouse klastra usługi HDInsight hello usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="70603-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="70603-176">Po skonfigurowaniu klastra usługi HDInsight można uruchomić zadania testowe na nim tooensure, że można uzyskać dostępu do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="70603-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="70603-177">toodo tak, uruchom toocreate zadania Hive przykładowej tabeli, która używa hello przykładowych danych, który jest już dostępne w usłudze Data Lake Store w  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="70603-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="70603-178">W tej sekcji należy utworzyć połączenie Secure Shell (SSH) do hello utworzonego klastra usługi HDInsight w systemie Linux, a następnie uruchom przykładowe zapytanie Hive.</span><span class="sxs-lookup"><span data-stu-id="70603-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="70603-179">Jeśli korzystasz z systemu Windows klienta toomake połączenie SSH do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="70603-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="70603-180">Jeśli korzystasz z systemu Linux toomake klienta połączenia SSH do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight w systemie Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="70603-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="70603-181">Po dokonaniu hello połączenia, należy uruchomić hello gałąź o interfejsu wiersza polecenia (CLI) przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="70603-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="70603-182">Użyj hello CLI tooenter hello następujące instrukcje toocreate nowej tabeli o nazwie **pojazdów** przy użyciu hello przykładowych danych w usłudze Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="70603-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="70603-183">W konsoli SSH hello powinna zostać wyświetlona hello wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="70603-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="70603-184">Witaj ścieżki toohello przykładowe dane w hello poprzedzających polecenia CREATE TABLE jest `adl:///example/data/`, gdzie `adl:///` jest hello klastra głównego.</span><span class="sxs-lookup"><span data-stu-id="70603-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="70603-185">Następujący przykład hello hello głównego klastra, który jest określony w tym samouczku, polecenie hello jest `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="70603-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="70603-186">Można użyć zamiast krótszą hello lub podaj hello pełną ścieżkę toohello klastra głównego.</span><span class="sxs-lookup"><span data-stu-id="70603-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="70603-187">Dostęp do usługi Data Lake Store za pomocą poleceń systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="70603-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="70603-188">Po skonfigurowaniu hello HDInsight klastra toouse Data Lake Store, można użyć systemu plików rozproszonych Hadoop (HDFS) powłoki poleceń tooaccess hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="70603-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="70603-189">W tej sekcji podczas nawiązywania połączenia SSH do hello utworzonego klastra usługi HDInsight w systemie Linux, a następnie uruchom hello poleceń systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="70603-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="70603-190">Jeśli korzystasz z systemu Windows klienta toomake połączenie SSH do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="70603-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="70603-191">Jeśli korzystasz z systemu Linux toomake klienta połączenia SSH do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight w systemie Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="70603-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="70603-192">Po utworzeniu połączenia hello, listy hello plików w usłudze Data Lake Store za pomocą następującego polecenia systemu plików HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="70603-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="70603-193">Można również użyć hello `hdfs dfs -put` polecenia tooupload niektóre pliki tooData Lake — magazyn, a następnie użyj `hdfs dfs -ls` tooverify czy hello pliki zostały pomyślnie przekazane.</span><span class="sxs-lookup"><span data-stu-id="70603-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="70603-194">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="70603-194">See also</span></span>
* [<span data-ttu-id="70603-195">Portalu Azure: Utwórz toouse klastra usługi HDInsight usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="70603-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
