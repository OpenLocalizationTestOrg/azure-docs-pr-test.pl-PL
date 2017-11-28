---
<span data-ttu-id="ea1cd-101">title: aaa "środowiska PowerShell: klaster Azure HDInsight z usługi Data Lake Store jako magazyn dodatków | Usługi Microsoft Docs": documentationcenter hdinsight dane lake — Magazyn:" Autor: nitinme Menedżera: Edytor jhubbard: cgronlun</span><span class="sxs-lookup"><span data-stu-id="ea1cd-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="ea1cd-102">MS.AssetID: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: ms.devlang data lake magazynu: na ms.topic: artykuł ms.tgt_pltfrm: na ms.workload: danych big data ms.date: ms.author 06/08/2017: nitinme</span><span class="sxs-lookup"><span data-stu-id="ea1cd-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ea1cd-103">Użyj programu Azure PowerShell toocreate klastra usługi HDInsight z usługą Data Lake Store (jako dodatkowego magazynu)</span><span class="sxs-lookup"><span data-stu-id="ea1cd-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea1cd-104">Korzystanie z portalu</span><span class="sxs-lookup"><span data-stu-id="ea1cd-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="ea1cd-105">Przy użyciu programu PowerShell (do magazynu domyślnego)</span><span class="sxs-lookup"><span data-stu-id="ea1cd-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="ea1cd-106">Przy użyciu programu PowerShell (dla dodatkowego magazynu)</span><span class="sxs-lookup"><span data-stu-id="ea1cd-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="ea1cd-107">Za pomocą Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="ea1cd-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="ea1cd-108">Dowiedz się, jak klaster toouse tooconfigure programu PowerShell usługi Azure HDInsight z usługi Azure Data Lake Store, **jako dodatkowego magazynu**.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="ea1cd-109">Aby uzyskać instrukcje dotyczące sposobu toocreate HDInsight klaster z usługi Azure Data Lake Store jako domyślnego magazynu, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store jako domyślny magazyn](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ea1cd-110">Jeśli zamierzasz toouse Azure Data Lake Store jako dodatkowego magazynu dla klastra usługi HDInsight, zdecydowanie zaleca się to zrobić podczas tworzenia klastra hello zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="ea1cd-111">Dodawanie usługi Azure Data Lake Store jako dodatkowego magazynu tooan istniejącym klastrze usługi HDInsight to skomplikowany proces i tooerrors podatnych na błędy.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="ea1cd-112">Dla typów obsługiwanych klastra usługi Data Lake Store może służyć jako domyślnego magazynu lub konto dodatkowego miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="ea1cd-113">W przypadku usługi Data Lake Store jako dodatkowego magazynu hello domyślne konto magazynu dla klastrów hello będzie nadal Azure blob Storage (WASB) i hello plików związanych z klastrem (takich jak dzienniki, itp.) są zapisywane nadal toohello domyślny magazyn, podczas danych hello które Chcę tooprocess mogą być przechowywane w ramach konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="ea1cd-114">Za pomocą usługi Data Lake Store jako dodatkowego magazynu konta nie wpływa na wydajność lub pamięć masową toohello tooread/zapisu możliwości hello z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="ea1cd-115">W magazynie klastra usługi HDInsight przy użyciu usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ea1cd-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="ea1cd-116">Poniżej przedstawiono kilka istotnych kwestii dotyczących z usługą Data Lake Store za pomocą usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="ea1cd-117">Klastry HDInsight toocreate opcji z dostępem do tooData Lake Store jako dodatkowego magazynu jest dostępna dla usługi HDInsight w wersji 3.2, 3.4, 3.5 i 3,6.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="ea1cd-118">Konfigurowanie usługi HDInsight toowork z Data Lake Store za pomocą programu PowerShell obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="ea1cd-119">Tworzenie usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ea1cd-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="ea1cd-120">Konfigurowanie uwierzytelniania opartego na rolach dostępu tooData Lake — Magazyn</span><span class="sxs-lookup"><span data-stu-id="ea1cd-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="ea1cd-121">Tworzenie klastra usługi HDInsight z usługą uwierzytelniania tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="ea1cd-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="ea1cd-122">Uruchom zadanie testowe w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="ea1cd-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea1cd-123">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ea1cd-123">Prerequisites</span></span>
<span data-ttu-id="ea1cd-124">Przed rozpoczęciem tego samouczka wymagane są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="ea1cd-125">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-125">**An Azure subscription**.</span></span> <span data-ttu-id="ea1cd-126">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ea1cd-127">**Program Azure PowerShell 1.0 lub nowszy**.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="ea1cd-128">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ea1cd-129">**Zestaw Windows SDK**.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-129">**Windows SDK**.</span></span> <span data-ttu-id="ea1cd-130">Możesz zainstalować ją z [tutaj](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="ea1cd-131">Możesz użyć tego toocreate certyfikatu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="ea1cd-132">**Nazwy głównej usługi Azure Active Directory usługi**.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="ea1cd-133">Kroki opisane w tym samouczku zawierają instrukcje na temat toocreate nazwy głównej usługi w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="ea1cd-134">Jednak należy usługi Azure AD administratora toobe stanie toocreate nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="ea1cd-135">Jeśli jesteś administratorem usługi Azure AD, możesz pominąć te wymagania wstępne i kontynuować hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="ea1cd-136">**Jeśli nie jesteś administratorem usługi Azure AD**, nie będą mogli tooperform hello kroki wymagane toocreate nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="ea1cd-137">W takim przypadku administrator usługi Azure AD należy najpierw utworzyć nazwy głównej usługi przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="ea1cd-138">Także hello nazwy głównej usługi muszą zostać utworzone za pomocą certyfikatu, zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="ea1cd-139">Tworzenie usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ea1cd-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="ea1cd-140">Wykonaj te kroki toocreate usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="ea1cd-141">Na pulpicie otwórz nowe okno programu Azure PowerShell, a następnie wprowadź hello następującego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="ea1cd-142">Gdy zostanie wyświetlony monit o toolog, upewnij się, że logujesz się jako jeden właściciel administratora subskrypcji hello:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="ea1cd-143">Jeśli zostanie wyświetlony błąd podobny zbyt`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` podczas rejestrowania dostawcy zasobów usługi Data Lake Store hello, istnieje możliwość, że Twoja subskrypcja nie jest białej dla usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="ea1cd-144">Upewnij się, że Włącz subskrypcji platformy Azure dla publicznej wersji zapoznawczej usługi Data Lake Store wykonując te [instrukcje](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="ea1cd-145">Konto usługi Azure Data Lake Store jest skojarzone z grupą zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="ea1cd-146">Rozpocznij od utworzenia grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="ea1cd-147">Powinny pojawić się dane wyjściowe podobne to:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="ea1cd-148">Utwórz konto usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="ea1cd-149">Konto Hello się, że nazwa użytkownika musi zawierać tylko małe litery i cyfry.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="ea1cd-150">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-150">You should see an output like hello following:</span></span>

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

5. <span data-ttu-id="ea1cd-151">Przekaż niektóre przykładowe dane tooAzure usługi Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="ea1cd-152">Użyjemy w dalszej części tego tooverify artykułu, czy dane hello jest dostępny z klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="ea1cd-153">Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="ea1cd-154">Konfigurowanie uwierzytelniania opartego na rolach dostępu tooData Lake — Magazyn</span><span class="sxs-lookup"><span data-stu-id="ea1cd-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="ea1cd-155">Każda subskrypcja platformy Azure jest skojarzony z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="ea1cd-156">Użytkowników i usług, które uzyskują dostęp do zasobów przy użyciu hello klasycznego portalu Azure lub interfejsu API usługi Azure Resource Manager subskrypcji hello muszą najpierw zostać uwierzytelnione z tej usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="ea1cd-157">Dostęp tooAzure subskrypcji i usług przez przypisywanie ich odpowiednią rolę hello na zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="ea1cd-158">W przypadku usług nazwy głównej usługi identyfikuje usługi hello w hello Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="ea1cd-159">W tej części przedstawiono, jak usługa toogrant aplikacji, takich jak usługa HDInsight, tooan dostępu do zasobów platformy Azure (hello utworzonego wcześniej konta usługi Azure Data Lake Store) przez tworzenie nazwy głównej usługi dla aplikacji hello i przypisywanie ról toothat za pośrednictwem usługi Azure Środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="ea1cd-160">tooset się uwierzytelnianie usługi Active Directory dla usługi Azure Data Lake, należy wykonać następujące zadania hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="ea1cd-161">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="ea1cd-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="ea1cd-162">Tworzenie aplikacji w usłudze Azure Active Directory i nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="ea1cd-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="ea1cd-163">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="ea1cd-163">Create a self-signed certificate</span></span>
<span data-ttu-id="ea1cd-164">Upewnij się, że masz [zestaw Windows SDK](https://dev.windows.com/en-us/downloads) zainstalowany przed rozpoczęciem powitalne kroki opisane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="ea1cd-165">Należy także utworzyć katalogu, takie jak **C:\mycertdir**, w której zostanie utworzona hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="ea1cd-166">W oknie programu PowerShell hello Przejdź toohello lokalizacji, w której zainstalowany zestaw Windows SDK (zazwyczaj `C:\Program Files (x86)\Windows Kits\10\bin\x86` i użyj hello [MakeCert] [ makecert] toocreate narzędzie certyfikatu z podpisem własnym i klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="ea1cd-167">Użyj następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="ea1cd-168">Hasło klucza prywatnego hello zostanie wyświetlony monit o tooenter będzie.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="ea1cd-169">Po hello polecenie zostało wykonane pomyślnie, powinien zostać wyświetlony **CertFile.cer** i **mykey.pvk** w katalogu certyfikatu hello określona.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="ea1cd-170">Użyj hello [Pvk2Pfx] [ pvk2pfx] .pvk hello tooconvert narzędzia i .cer pliki tego pliku pfx utworzony tooa MakeCert.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="ea1cd-171">Uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="ea1cd-172">Po wyświetleniu monitu wprowadź hasło klucza z prywatnego hello określone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="ea1cd-173">wartość określona dla hello Hello **— po** hello hasło skojarzone z plikiem PFX hello jest parametr.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="ea1cd-174">Po pomyślnym zakończeniu hello polecenia, zobacz też CertFile.pfx w katalogu certyfikatu hello, określona.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="ea1cd-175">Tworzenie usługi Azure Active Directory i nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="ea1cd-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="ea1cd-176">W tej sekcji wykonać hello kroki toocreate nazwy głównej usługi dla aplikacji usługi Azure Active Directory, przypisać nazwy głównej usługi roli toohello i Uwierzytelnij się jako nazwy głównej usługi hello zapewniając certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="ea1cd-177">Uruchom następujące polecenia toocreate hello aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="ea1cd-178">Wklej hello następującego polecenia cmdlet w oknie konsoli programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="ea1cd-179">Upewnij się, że wartość hello określona dla hello **— Nazwa wyświetlana** właściwości jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="ea1cd-180">Ponadto hello wartości **— strona główna** i **- IdentiferUris** są symbole zastępcze i nie są weryfikowane.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="ea1cd-181">Tworzenie nazwy głównej usługi przy użyciu identyfikatora hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="ea1cd-182">Udziel hello usługi głównej dostępu toohello usługi Data Lake Store folderu i pliku hello, dostępnej z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="ea1cd-183">Poniższy fragment Hello zapewnia dostęp głównym toohello hello Data Lake Store konta (którego skopiowano hello przykładowy plik danych) i hello sam plik.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="ea1cd-184">Tworzenie klastra usługi HDInsight Linux z usługą Data Lake Store jako dodatkowego miejsca do magazynowania</span><span class="sxs-lookup"><span data-stu-id="ea1cd-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="ea1cd-185">W tej sekcji utworzymy klastra usługi HDInsight Hadoop Linux z usługą Data Lake Store jako dodatkowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="ea1cd-186">W tej wersji hello klaster usługi HDInsight i hello Data Lake — Magazyn musi być w hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="ea1cd-187">Zaczynać się podczas pobierania identyfikatora hello subskrypcji dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="ea1cd-188">Który będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="ea1cd-189">W tej wersji dla klastra usługi Hadoop, Data Lake Store można użyć tylko jako dodatkowego magazynu hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="ea1cd-190">Witaj domyślnego magazynu będą nadal hello blob magazynu Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="ea1cd-191">Tak najpierw utworzymy hello kontenery konta i przechowywania magazynu wymaganych dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="ea1cd-192">Tworzenie klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="ea1cd-193">Użyj następującego polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="ea1cd-194">Po pomyślnym zakończeniu hello polecenia cmdlet, powinny zostać wyświetlone dane wyjściowe, wyświetlania szczegółów klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="ea1cd-195">Uruchom zadania testowe na powitania HDInsight klastra toouse hello usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ea1cd-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="ea1cd-196">Po skonfigurowaniu klastra usługi HDInsight można uruchamiać zadania testowego na powitania klastra tootest tego hello HDInsight klastra mogą uzyskiwać dostęp do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="ea1cd-197">toodo tak, zostanie uruchomiony przykładowe zadania Hive, która tworzy tabelę przy użyciu hello przykładowych danych, aby przekazać wcześniejszych tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="ea1cd-198">W tej sekcji do klastra HDInsight Linux, możesz utworzyć i uruchomić przykładowe zapytanie Hive hello hello będzie SSH.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="ea1cd-199">Jeśli używasz tooSSH klienta systemu Windows do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ea1cd-200">Jeśli używasz tooSSH klient systemu Linux w klastrze hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ea1cd-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="ea1cd-201">Po nawiązaniu połączenia, należy uruchomić hello Hive interfejsu wiersza polecenia przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="ea1cd-202">Używając hello interfejsu wiersza polecenia, wprowadź następujące instrukcje toocreate nowej tabeli o nazwie hello **pojazdów** przy użyciu hello przykładowe dane w hello usługi Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="ea1cd-203">Powinny być widoczne następujące dane wyjściowe podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="ea1cd-203">You should see an output similar toohello following:</span></span>

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="ea1cd-204">Dostęp Data Lake Store za pomocą poleceń systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="ea1cd-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="ea1cd-205">Po skonfigurowaniu hello HDInsight klastra toouse Data Lake Store można użyć hello systemu plików HDFS powłoki poleceń tooaccess hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="ea1cd-206">W tej sekcji do klastra HDInsight Linux, możesz utworzyć i uruchamiania poleceń systemu plików HDFS hello hello będzie SSH.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="ea1cd-207">Jeśli używasz tooSSH klienta systemu Windows do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ea1cd-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="ea1cd-208">Jeśli używasz tooSSH klient systemu Linux w klastrze hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ea1cd-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="ea1cd-209">Po nawiązaniu połączenia użyj hello następujące pliki poleceń systemu plików HDFS hello toolist w hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="ea1cd-210">Powinny pojawić się plik hello czy przesłany wcześniejszych toohello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="ea1cd-211">Można również użyć hello `hdfs dfs -put` polecenia tooupload toohello niektórych plików usługi Data Lake Store, a następnie użyj `hdfs dfs -ls` tooverify czy hello pliki zostały pomyślnie przekazane.</span><span class="sxs-lookup"><span data-stu-id="ea1cd-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="ea1cd-212">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ea1cd-212">See Also</span></span>
* [<span data-ttu-id="ea1cd-213">Portal: Tworzenie toouse klastra usługi HDInsight usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ea1cd-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
