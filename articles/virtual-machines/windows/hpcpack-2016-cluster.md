---
title: aaaHPC 2016 pakiet klastra na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodeploy HPC Pack 2016 klastra w systemie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="542c7-103">Wdrożenie klastra HPC Pack 2016 na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="542c7-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="542c7-104">Wykonaj kroki hello w tym artykule toodeploy [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) klastra w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="542c7-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="542c7-105">HPC Pack jest bezpłatna rozwiązania HPC firmy Microsoft, oparty na technologii Microsoft Azure i Windows Server i obsługuje obciążeń szeroki zakres HPC.</span><span class="sxs-lookup"><span data-stu-id="542c7-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="542c7-106">Użyj jednej z hello [szablonów usługi Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 klastra.</span><span class="sxs-lookup"><span data-stu-id="542c7-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="542c7-107">Można wybrać kilka opcji Topologia klastra z różnymi liczbami głównymi węzłami klastra i z albo systemem Linux lub Windows węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="542c7-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="542c7-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="542c7-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="542c7-109">Certyfikatu PFX</span><span class="sxs-lookup"><span data-stu-id="542c7-109">PFX certificate</span></span>

<span data-ttu-id="542c7-110">W klastrze Microsoft HPC Pack 2016 wymaga komunikatu hello toosecure certyfikat wymiany informacji osobistych (PFX) między węzłami klastra HPC hello.</span><span class="sxs-lookup"><span data-stu-id="542c7-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="542c7-111">certyfikat Hello musi spełniać hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="542c7-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="542c7-112">Musi mieć klucz prywatny zdolny do wymiany klucza</span><span class="sxs-lookup"><span data-stu-id="542c7-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="542c7-113">Użycie klucza zawiera podpis cyfrowy i szyfrowanie klucza</span><span class="sxs-lookup"><span data-stu-id="542c7-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="542c7-114">Obejmuje ulepszonego użycia klucza uwierzytelniania serwera i uwierzytelnianie klienta</span><span class="sxs-lookup"><span data-stu-id="542c7-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="542c7-115">Jeśli nie masz jeszcze certyfikatu, który spełnia te wymagania, można zażądać hello certyfikatu od urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="542c7-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="542c7-116">Alternatywnie można użyć hello następujące polecenia toogenerate hello certyfikatu z podpisem własnym systemem operacyjnym hello, na którym Uruchom polecenie hello i wyeksportuj certyfikat format PFX hello z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="542c7-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="542c7-117">**Dla systemu Windows 10 lub Windows Server 2016**, uruchom wbudowane hello **SelfSignedCertificate nowy** polecenia cmdlet programu PowerShell w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="542c7-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="542c7-118">**W systemach operacyjnych starszych niż Windows 10 lub Windows Server 2016**, Pobierz hello [generator certyfikatu z podpisem własnym](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) z hello Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="542c7-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="542c7-119">Wyodrębnij jego zawartość, a następnie uruchom następujące polecenia w wierszu polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="542c7-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="542c7-120">Przekaż certyfikat tooan usługi Azure key vault</span><span class="sxs-lookup"><span data-stu-id="542c7-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="542c7-121">Przed wdrożeniem klastra HPC hello, Przekaż hello certyfikatu tooan [usługi Azure key vault](../../key-vault/index.md) jako poufne i rekordów hello, następujących informacji do użycia podczas wdrażania hello: **nazwę magazynu**,  **Grupa zasobów magazynu**, **adres URL certyfikatu**, i **odcisk palca certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="542c7-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="542c7-122">Certyfikat hello tooupload skrypt programu PowerShell próbki jest zgodna.</span><span class="sxs-lookup"><span data-stu-id="542c7-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="542c7-123">Aby uzyskać więcej informacji na temat przekazywania certyfikatu tooan usługi Azure key vault, zobacz [wprowadzenie do usługi Azure Key Vault](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="542c7-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="542c7-124">Obsługiwane topologie</span><span class="sxs-lookup"><span data-stu-id="542c7-124">Supported topologies</span></span>

<span data-ttu-id="542c7-125">Wybierz jedną z hello [szablonów usługi Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 klastra.</span><span class="sxs-lookup"><span data-stu-id="542c7-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="542c7-126">Poniżej przedstawiono wysokiego poziomu architektury trzy obsługiwanych topologii klastrów.</span><span class="sxs-lookup"><span data-stu-id="542c7-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="542c7-127">Topologie wysokiej dostępności obejmują wiele głównymi węzłami klastra.</span><span class="sxs-lookup"><span data-stu-id="542c7-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="542c7-128">Klastra o wysokiej dostępności z domeną usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="542c7-128">High-availability cluster with Active Directory domain</span></span>

    ![Klastra HA w domenie AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="542c7-130">Wysoka dostępność klastra bez domeny usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="542c7-130">High-availability cluster without Active Directory domain</span></span>

    ![Klastra HA bez domeny usługi AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="542c7-132">Klaster z jednym węzłem głównym</span><span class="sxs-lookup"><span data-stu-id="542c7-132">Cluster with a single head node</span></span>

   ![Klaster z jednym węzłem głównym](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="542c7-134">Wdrażanie klastra</span><span class="sxs-lookup"><span data-stu-id="542c7-134">Deploy a cluster</span></span>

<span data-ttu-id="542c7-135">toocreate hello klastra, wybrać szablon i kliknij przycisk **wdrażanie tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="542c7-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="542c7-136">W hello [portalu Azure](https://portal.azure.com), określ parametry szablonu hello, zgodnie z opisem w hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="542c7-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="542c7-137">Każdy szablon tworzy wszystkich zasobów systemu Azure wymaganych przez infrastruktura klastra HPC hello.</span><span class="sxs-lookup"><span data-stu-id="542c7-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="542c7-138">Zasoby obejmują sieci wirtualnej platformy Azure, publicznego adresu IP adres usługi równoważenia obciążenia (tylko w przypadku klastra o wysokiej dostępności), interfejsów sieciowych, zestawów dostępności, kont magazynu i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="542c7-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="542c7-139">Krok 1: Wybierz subskrypcję hello, lokalizacji i grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="542c7-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="542c7-140">Witaj **subskrypcji** i hello **lokalizacji** musi być taka sama, określona po przekazaniu certyfikatu PFX (patrz wymagania wstępne).</span><span class="sxs-lookup"><span data-stu-id="542c7-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="542c7-141">Firma Microsoft zaleca utworzenie **grupy zasobów** hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="542c7-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="542c7-142">Krok 2: Określ ustawienia parametru hello</span><span class="sxs-lookup"><span data-stu-id="542c7-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="542c7-143">Wprowadź lub zmień wartości parametrów szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="542c7-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="542c7-144">Kliknij przycisk hello ikona dalej tooeach parametr informacji pomocy.</span><span class="sxs-lookup"><span data-stu-id="542c7-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="542c7-145">Zobacz też hello wskazówki dotyczące [dostępne rozmiary maszyny Wirtualnej](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="542c7-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="542c7-146">Określ wartości hello rejestrowane w hello wymagania wstępne hello następujące parametry: **nazwę magazynu**, **grupy zasobów magazynu**, **adres URL certyfikatu**i **Odcisk palca certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="542c7-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="542c7-147">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="542c7-147">Step 3.</span></span> <span data-ttu-id="542c7-148">Przejrzyj postanowienia prawne i utworzyć</span><span class="sxs-lookup"><span data-stu-id="542c7-148">Review legal terms and create</span></span>
<span data-ttu-id="542c7-149">Kliknij przycisk **Przejrzyj postanowienia prawne** tooreview hello warunki.</span><span class="sxs-lookup"><span data-stu-id="542c7-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="542c7-150">Jeśli akceptujesz, kliknij przycisk **zakupu**, a następnie kliknij przycisk **Utwórz** toostart hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="542c7-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="542c7-151">Połącz toohello klastra</span><span class="sxs-lookup"><span data-stu-id="542c7-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="542c7-152">Po wdrożeniu klastra HPC Pack hello Przejdź toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="542c7-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="542c7-153">Kliknij przycisk **grup zasobów**i grupy zasobów hello Znajdź w których hello klastra została wdrożona.</span><span class="sxs-lookup"><span data-stu-id="542c7-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="542c7-154">Hello można znaleźć węzła głównego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="542c7-154">You can find hello head node virtual machines.</span></span>

    ![Głównymi węzłami klastra w portalu hello](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="542c7-156">Kliknij przycisk jednego węzła głównego (w klastrze wysokiej dostępności kliknij dowolny z węzłów głównych hello).</span><span class="sxs-lookup"><span data-stu-id="542c7-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="542c7-157">W **Essentials**, można znaleźć hello publicznego adresu IP lub pełną nazwę DNS hello klastra.</span><span class="sxs-lookup"><span data-stu-id="542c7-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Ustawienia połączenia klastra](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="542c7-159">Kliknij przycisk **Connect** toolog na tooany hello węzłów głównych przy użyciu pulpitu zdalnego z nazwą użytkownika administratora.</span><span class="sxs-lookup"><span data-stu-id="542c7-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="542c7-160">Jeśli klaster hello wdrożono znajduje się w domenie usługi Active Directory, nazwa użytkownika hello ma formę hello <privateDomainName> \<adminUsername > (na przykład hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="542c7-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="542c7-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="542c7-161">Next steps</span></span>
* <span data-ttu-id="542c7-162">Przedstawia zadania tooyour klastra.</span><span class="sxs-lookup"><span data-stu-id="542c7-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="542c7-163">Zobacz [przesłać tooHPC zadań klastra HPC Pack na platformie Azure](hpcpack-cluster-submit-jobs.md) i [Zarządzanie klastra HPC Pack 2016 na platformie Azure przy użyciu usługi Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="542c7-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

