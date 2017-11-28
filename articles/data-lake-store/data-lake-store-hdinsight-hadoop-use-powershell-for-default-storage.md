---
title: "Tworzenie klastrów usługi HDInsight z usługą Data Lake Store jako domyślny magazyn przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Tworzenie i korzystanie z usługi Azure Data Lake Store klastrów usługi HDInsight przy użyciu programu Azure PowerShell"
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
ms.openlocfilehash: 77eb83b80312eca401e6f60d57ed6a5668ea442e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="333c8-103">Tworzenie klastrów usługi HDInsight z usługą Data Lake Store jako domyślny magazyn przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="333c8-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="333c8-104">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="333c8-104">Use the Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="333c8-105">Przy użyciu programu PowerShell (do magazynu domyślnego)</span><span class="sxs-lookup"><span data-stu-id="333c8-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="333c8-106">Przy użyciu programu PowerShell (dla dodatkowego magazynu)</span><span class="sxs-lookup"><span data-stu-id="333c8-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="333c8-107">Użyj Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="333c8-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="333c8-108">Dowiedz się, jak skonfigurować klastry usługi HDInsight Azure z usługi Azure Data Lake Store jako domyślny magazyn przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="333c8-108">Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="333c8-109">Aby uzyskać instrukcje dotyczące tworzenia klastra usługi HDInsight z usługą Data Lake Store jako dodatkowego miejsca do magazynowania, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store jako dodatkowego magazynu](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="333c8-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="333c8-110">Poniżej przedstawiono kilka istotnych kwestii dotyczących z usługą Data Lake Store za pomocą usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="333c8-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="333c8-111">Możliwość tworzenia klastrów usługi HDInsight z dostępem do usługi Data Lake Store jako domyślnego magazynu jest dostępna dla usługi HDInsight w wersji 3.5 i 3,6.</span><span class="sxs-lookup"><span data-stu-id="333c8-111">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="333c8-112">Opcja tworzenia HDInsight klastrów z dostępem do usługi Data Lake Store jako domyślnego magazynu jest *nie jest dostępny* klastrów HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="333c8-112">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="333c8-113">Aby skonfigurować HDInsight do pracy z usługą Data Lake Store za pomocą programu PowerShell, postępuj zgodnie z instrukcjami w sekcji następnych pięciu.</span><span class="sxs-lookup"><span data-stu-id="333c8-113">To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="333c8-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="333c8-114">Prerequisites</span></span>
<span data-ttu-id="333c8-115">Przed rozpoczęciem tego samouczka, upewnij się, czy zostały spełnione następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="333c8-115">Before you begin this tutorial, make sure that you meet the following requirements:</span></span>

* <span data-ttu-id="333c8-116">**Subskrypcja platformy Azure**: Przejdź do [Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="333c8-116">**An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="333c8-117">**Program Azure PowerShell 1.0 lub nowszego**: zobacz [jak instalowanie i konfigurowanie programu PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="333c8-117">**Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="333c8-118">**Windows Software Development Kit (SDK)**: Aby zainstalować zestaw Windows SDK, przejdź do [pliki do pobrania i narzędzi dla systemu Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="333c8-118">**Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="333c8-119">Zestaw SDK służy do tworzenia certyfikatu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="333c8-119">The SDK is used to create a security certificate.</span></span>
* <span data-ttu-id="333c8-120">**Nazwy głównej usługi Azure Active Directory**: w tym samouczku opisano sposób tworzenia nazwy głównej usługi w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="333c8-120">**Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="333c8-121">Jednak można utworzyć nazwy głównej usługi, musi być administratorem usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="333c8-121">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="333c8-122">Jeśli jesteś administratorem, możesz pominąć te wymagania wstępne i kontynuować samouczka.</span><span class="sxs-lookup"><span data-stu-id="333c8-122">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="333c8-123">Usługi można utworzyć podmiot, tylko wtedy, gdy administrator usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="333c8-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="333c8-124">Administrator usługi Azure AD należy utworzyć usługę podmiotu zabezpieczeń przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="333c8-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="333c8-125">Nazwy głównej usługi należy utworzyć przy użyciu certyfikatu zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="333c8-125">The service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="333c8-126">Tworzenie konta usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="333c8-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="333c8-127">Aby utworzyć konto usługi Data Lake Store, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="333c8-127">To create a Data Lake Store account, do the following:</span></span>

1. <span data-ttu-id="333c8-128">Na pulpicie otwórz okno programu PowerShell, a następnie wprowadź poniższe fragmenty kodu.</span><span class="sxs-lookup"><span data-stu-id="333c8-128">From your desktop, open a PowerShell window, and then enter the snippets below.</span></span> <span data-ttu-id="333c8-129">Po wyświetleniu monitu zaloguj się, zaloguj się jako jeden z administratorów subskrypcji lub właścicieli.</span><span class="sxs-lookup"><span data-stu-id="333c8-129">When you are prompted to sign in, sign in as one of the subscription administrators or owners.</span></span> 

        # Sign in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="333c8-130">Jeśli rejestrowanie dostawcy zasobów usługi Data Lake Store i komunikat o błędzie podobny do `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, subskrypcja może nie być białej dla usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="333c8-130">If you register the Data Lake Store resource provider and receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="333c8-131">Aby włączyć Twojej subskrypcji platformy Azure dla publicznej wersji zapoznawczej usługi Data Lake Store, postępuj zgodnie z instrukcjami [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="333c8-131">To enable your Azure subscription for the Data Lake Store public preview, follow the instructions in [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="333c8-132">Konto usługi Data Lake Store jest skojarzona z grupą zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="333c8-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="333c8-133">Rozpocznij od utworzenia grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="333c8-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="333c8-134">Powinny pojawić się dane wyjściowe podobne to:</span><span class="sxs-lookup"><span data-stu-id="333c8-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="333c8-135">Utwórz konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="333c8-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="333c8-136">Nazwa konta, które określisz musi zawierać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="333c8-136">The account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="333c8-137">Powinny pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="333c8-137">You should see an output like the following:</span></span>

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

4. <span data-ttu-id="333c8-138">Za pomocą usługi Data Lake Store jako domyślny magazyn wymaga określenia ścieżki katalogu głównego, do którego kopiowania plików specyficznych dla klastra podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="333c8-138">Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="333c8-139">Aby utworzyć ścieżki katalogu głównego, który jest **/klastrów/hdiadlcluster** we fragmencie, użyj następujących poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="333c8-139">To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="333c8-140">Konfigurowanie uwierzytelniania opartego na rolach dostępu do usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="333c8-140">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="333c8-141">Każda subskrypcja platformy Azure jest skojarzony z jednostką usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="333c8-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="333c8-142">Użytkowników i usług, które uzyskują dostęp do zasobów subskrypcji przy użyciu portalu Azure lub interfejsu API Azure Resource Manager muszą najpierw uwierzytelnić w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="333c8-142">Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="333c8-143">Dostęp do usług i subskrypcji platformy Azure przez przypisywanie ich odpowiedniej roli na zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="333c8-143">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span> <span data-ttu-id="333c8-144">W przypadku usług nazwy głównej usługi identyfikuje usługę w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="333c8-144">For services, a service principal identifies the service in Azure AD.</span></span>

<span data-ttu-id="333c8-145">W tej części przedstawiono sposób przyznania usługi aplikacji, takie jak usługi HDInsight, dostęp do zasobów platformy Azure (konta Data Lake Store, który został utworzony wcześniej).</span><span class="sxs-lookup"><span data-stu-id="333c8-145">This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="333c8-146">Można to zrobić przez utworzenie usługi głównej aplikacji i przypisywanie ról do niego za pośrednictwem programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="333c8-146">You do so by creating a service principal for the application and assigning roles to it via PowerShell.</span></span>

<span data-ttu-id="333c8-147">Aby skonfigurować uwierzytelnianie usługi Active Directory dla usługi Azure Data Lake, należy wykonać zadania w następujących sekcjach.</span><span class="sxs-lookup"><span data-stu-id="333c8-147">To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="333c8-148">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="333c8-148">Create a self-signed certificate</span></span>
<span data-ttu-id="333c8-149">Upewnij się, że masz [zestaw Windows SDK](https://dev.windows.com/en-us/downloads) zainstalowany, przed wykonaniem czynności w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="333c8-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="333c8-150">Należy także utworzyć katalogu, takie jak *C:\mycertdir*, w którym można utworzyć certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="333c8-150">You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.</span></span>

1. <span data-ttu-id="333c8-151">W oknie programu PowerShell przejdź do lokalizacji, w której zainstalowany zestaw Windows SDK (zazwyczaj *\Windows Kits\10\bin\x86 C:\Program Files (x86)*) i używać [MakeCert] [ makecert] narzędzie do utworzenia certyfikatu z podpisem własnym oraz klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="333c8-151">From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="333c8-152">Użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="333c8-152">Use the following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="333c8-153">Pojawi się monit o wprowadzenie hasło klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="333c8-153">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="333c8-154">Po polecenie zostanie wykonane pomyślnie, powinien zostać wyświetlony **CertFile.cer** i **mykey.pvk** w katalogu określonego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="333c8-154">After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.</span></span>
2. <span data-ttu-id="333c8-155">Użyj [Pvk2Pfx] [ pvk2pfx] narzędzie do konwersji plików .pvk i .cer, które MakeCert utworzone do pliku .pfx.</span><span class="sxs-lookup"><span data-stu-id="333c8-155">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="333c8-156">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="333c8-156">Run the following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="333c8-157">Po wyświetleniu monitu wprowadź określone wcześniej hasło klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="333c8-157">When you are prompted, enter the private key password that you specified earlier.</span></span> <span data-ttu-id="333c8-158">Wartość określona dla **— po** parametr jest hasło skojarzone z pliku pfx.</span><span class="sxs-lookup"><span data-stu-id="333c8-158">The value you specify for the **-po** parameter is the password that's associated with the .pfx file.</span></span> <span data-ttu-id="333c8-159">Po polecenie zostało zakończone pomyślnie, powinien również zostać wyświetlony **CertFile.pfx** w katalogu określonego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="333c8-159">After the command has been completed successfully, you should also see a **CertFile.pfx** in the certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="333c8-160">Tworzenie usługi Azure AD i nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="333c8-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="333c8-161">W tej sekcji Tworzenie nazwy głównej usługi dla aplikacji usługi Azure AD, przypisać rolę do nazwy głównej usługi i Uwierzytelnij się jako nazwy głównej usługi zapewniając certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="333c8-161">In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="333c8-162">Aby utworzyć aplikację w usłudze Azure AD, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="333c8-162">To create an application in Azure AD, run the following commands:</span></span>

1. <span data-ttu-id="333c8-163">Wklej następujące polecenia cmdlet w oknie konsoli programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="333c8-163">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="333c8-164">Upewnij się, że wartości określonej dla **— Nazwa wyświetlana** właściwości jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="333c8-164">Make sure that the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="333c8-165">Wartości **— strona główna** i **- IdentiferUris** są symbole zastępcze i nie są weryfikowane.</span><span class="sxs-lookup"><span data-stu-id="333c8-165">The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

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
2. <span data-ttu-id="333c8-166">Tworzenie nazwy głównej usługi za pomocą identyfikatora aplikacji.</span><span class="sxs-lookup"><span data-stu-id="333c8-166">Create a service principal by using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="333c8-167">Udziel dostępu główną usługi do katalogu głównego usługi Data Lake Store i wszystkie foldery w ścieżce katalogu głównego, określony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="333c8-167">Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier.</span></span> <span data-ttu-id="333c8-168">Użyj następujących poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="333c8-168">Use the following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-the-default-storage"></a><span data-ttu-id="333c8-169">Tworzenie klastra usługi HDInsight Linux z usługą Data Lake Store jako domyślnego magazynu</span><span class="sxs-lookup"><span data-stu-id="333c8-169">Create an HDInsight Linux cluster with Data Lake Store as the default storage</span></span>

<span data-ttu-id="333c8-170">W tej sekcji utworzysz klaster usługi HDInsight Hadoop Linux z usługą Data Lake Store jako domyślnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="333c8-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage.</span></span> <span data-ttu-id="333c8-171">W tej wersji klaster usługi HDInsight i Data Lake — Magazyn musi być w tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="333c8-171">For this release, the HDInsight cluster and Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="333c8-172">Pobierz identyfikator subskrypcji dzierżawcy i zapisać go do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="333c8-172">Retrieve the subscription tenant ID, and store it to use later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="333c8-173">Tworzenie klastra usługi HDInsight przy użyciu następujących poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="333c8-173">Create the HDInsight cluster by using the following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
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

    <span data-ttu-id="333c8-174">Po pomyślnym zakończeniu polecenia cmdlet powinny być widoczne dane wyjściowe, która wyświetla szczegóły klastra.</span><span class="sxs-lookup"><span data-stu-id="333c8-174">After the cmdlet has been successfully completed, you should see an output that lists the cluster details.</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-store"></a><span data-ttu-id="333c8-175">Uruchom zadania testowe w klastrze usługi HDInsight do użycia usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="333c8-175">Run test jobs on the HDInsight cluster to use Data Lake Store</span></span>
<span data-ttu-id="333c8-176">Po skonfigurowaniu klastra usługi HDInsight można uruchomić zadania testowe w celu zapewnienia, że można uzyskać dostępu do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="333c8-176">After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store.</span></span> <span data-ttu-id="333c8-177">Aby to zrobić, uruchom przykładowe zadania Hive, aby utworzyć tabelę, która używa przykładowych danych, który jest już dostępne w usłudze Data Lake Store w  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="333c8-177">To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="333c8-178">W tej sekcji należy utworzyć połączenie Secure Shell (SSH) do utworzonego klastra usługi HDInsight w systemie Linux, a następnie uruchom przykładowe zapytanie Hive.</span><span class="sxs-lookup"><span data-stu-id="333c8-178">In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="333c8-179">Jeśli używasz klienta systemu Windows do nawiązania połączenia SSH do klastra, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="333c8-179">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="333c8-180">Jeśli połączenie SSH w klastrze za pomocą klienta systemu Linux, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight w systemie Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="333c8-180">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="333c8-181">Po dokonaniu połączenie, uruchomić Hive interfejsu wiersza polecenia (CLI) za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="333c8-181">After you have made the connection, start the Hive command-line interface (CLI) by using the following command:</span></span>

        hive
2. <span data-ttu-id="333c8-182">Użyj interfejsu wiersza polecenia, aby wprowadzić poniższe instrukcje, aby utworzyć nową tabelę o nazwie **pojazdów** przy użyciu przykładowych danych w usłudze Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="333c8-182">Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="333c8-183">Wynik kwerendy powinna zostać wyświetlona w konsoli programu SSH.</span><span class="sxs-lookup"><span data-stu-id="333c8-183">You should see the query output on the SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="333c8-184">Ścieżka do przykładowych danych w poprzednim poleceniu CREATE TABLE jest `adl:///example/data/`, gdzie `adl:///` jest głównym klastra.</span><span class="sxs-lookup"><span data-stu-id="333c8-184">The path to the sample data in the preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is the cluster root.</span></span> <span data-ttu-id="333c8-185">Poniższy przykład głównego klastra, określonego w tym samouczku, to polecenie jest `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="333c8-185">Following the example of the cluster root that's specified in this tutorial, the command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="333c8-186">Możesz użyć alternatywnej krótszy lub podaj pełną ścieżkę do katalogu głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="333c8-186">You can either use the shorter alternative or provide the complete path to the cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="333c8-187">Dostęp do usługi Data Lake Store za pomocą poleceń systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="333c8-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="333c8-188">Po skonfigurowaniu klastra usługi HDInsight do użycia usługi Data Lake Store możesz używać poleceń powłoki systemu Distributed plików Hadoop (HDFS), dostęp do sklepu z.</span><span class="sxs-lookup"><span data-stu-id="333c8-188">After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.</span></span>

<span data-ttu-id="333c8-189">W tej sekcji należy połączenie SSH do utworzonego klastra usługi HDInsight w systemie Linux, a następnie uruchom polecenia systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="333c8-189">In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.</span></span>

* <span data-ttu-id="333c8-190">Jeśli używasz klienta systemu Windows do nawiązania połączenia SSH do klastra, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="333c8-190">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="333c8-191">Jeśli połączenie SSH w klastrze za pomocą klienta systemu Linux, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight w systemie Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="333c8-191">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="333c8-192">Po utworzeniu połączenia, listę plików w usłudze Data Lake Store za pomocą następującego polecenia systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="333c8-192">After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="333c8-193">Można również użyć `hdfs dfs -put` polecenie, aby przekazać pliki do usługi Data Lake Store, a następnie użyj `hdfs dfs -ls` Aby sprawdzić, czy pliki zostały pomyślnie przekazane.</span><span class="sxs-lookup"><span data-stu-id="333c8-193">You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="333c8-194">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="333c8-194">See also</span></span>
* [<span data-ttu-id="333c8-195">Portalu Azure: Tworzenie klastra usługi HDInsight do użycia usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="333c8-195">Azure portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
