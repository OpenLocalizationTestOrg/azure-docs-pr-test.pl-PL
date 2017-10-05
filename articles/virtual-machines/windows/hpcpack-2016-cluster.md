---
title: Klaster HPC Pack 2016 na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak wdrożyć klaster HPC Pack 2016 na platformie Azure"
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
ms.openlocfilehash: 88d1f4e29f38ba1a6bef57c2da43bee205575eee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="eb5da-103">Wdrożenie klastra HPC Pack 2016 na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eb5da-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="eb5da-104">Wykonaj kroki opisane w tym artykule, aby wdrożyć [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) klastra w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb5da-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="eb5da-105">HPC Pack jest bezpłatna rozwiązania HPC firmy Microsoft, oparty na technologii Microsoft Azure i Windows Server i obsługuje obciążeń szeroki zakres HPC.</span><span class="sxs-lookup"><span data-stu-id="eb5da-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="eb5da-106">Użyj jednej z [szablonów usługi Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) do wdrożenia klastra HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="eb5da-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="eb5da-107">Można wybrać kilka opcji Topologia klastra z różnymi liczbami głównymi węzłami klastra i z albo systemem Linux lub Windows węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="eb5da-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb5da-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eb5da-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="eb5da-109">Certyfikatu PFX</span><span class="sxs-lookup"><span data-stu-id="eb5da-109">PFX certificate</span></span>

<span data-ttu-id="eb5da-110">W klastrze Microsoft HPC Pack 2016 wymaga certyfikat wymiany informacji osobistych (PFX) do zabezpieczania komunikacji między węzłami klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="eb5da-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span></span> <span data-ttu-id="eb5da-111">Certyfikat musi spełniać następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="eb5da-111">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="eb5da-112">Musi mieć klucz prywatny zdolny do wymiany klucza</span><span class="sxs-lookup"><span data-stu-id="eb5da-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="eb5da-113">Użycie klucza zawiera podpis cyfrowy i szyfrowanie klucza</span><span class="sxs-lookup"><span data-stu-id="eb5da-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="eb5da-114">Obejmuje ulepszonego użycia klucza uwierzytelniania serwera i uwierzytelnianie klienta</span><span class="sxs-lookup"><span data-stu-id="eb5da-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="eb5da-115">Jeśli nie masz jeszcze certyfikatu, który spełnia te wymagania, należy zażądać certyfikatu od urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="eb5da-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span></span> <span data-ttu-id="eb5da-116">Alternatywnie można użyć następujących poleceń, aby wygenerować certyfikat z podpisem własnym systemem operacyjnym, na którym uruchomiono polecenie i wyeksportuj certyfikat format PFX z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="eb5da-116">Alternatively, you can use the following commands to generate the self-signed certificate based on the operating system on which you run the command, and export the PFX format certificate with private key.</span></span>

* <span data-ttu-id="eb5da-117">**Dla systemu Windows 10 lub Windows Server 2016**, uruchom wbudowane **SelfSignedCertificate nowy** polecenia cmdlet programu PowerShell w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eb5da-117">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="eb5da-118">**W systemach operacyjnych starszych niż Windows 10 lub Windows Server 2016**, Pobierz [generator certyfikatu z podpisem własnym](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) z Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="eb5da-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span></span> <span data-ttu-id="eb5da-119">Wyodrębnij jego zawartość, a następnie uruchom następujące polecenia w wierszu polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="eb5da-119">Extract its contents and run the following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-to-an-azure-key-vault"></a><span data-ttu-id="eb5da-120">Przekaż certyfikat do magazynu kluczy Azure</span><span class="sxs-lookup"><span data-stu-id="eb5da-120">Upload certificate to an Azure key vault</span></span>

<span data-ttu-id="eb5da-121">Przed wdrożeniem klastra HPC, Przekaż certyfikat do [usługi Azure key vault](../../key-vault/index.md) jako klucz tajny i rekord następujące informacje do użycia podczas wdrażania: **nazwę magazynu**, **magazynu Grupa zasobów**, **adres URL certyfikatu**, i **odcisk palca certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="eb5da-121">Before deploying the HPC cluster, upload the certificate to an [Azure key vault](../../key-vault/index.md) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="eb5da-122">Przykładowy skrypt programu PowerShell w celu przekazania certyfikatu jest zgodna.</span><span class="sxs-lookup"><span data-stu-id="eb5da-122">A sample PowerShell script to upload the certificate follows.</span></span> <span data-ttu-id="eb5da-123">Aby uzyskać więcej informacji na temat przekazywania certyfikatu do usługi Azure key vault, zobacz [wprowadzenie do usługi Azure Key Vault](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb5da-123">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give the following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate the pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode the JSON object
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
#Create an Azure key vault and upload the certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"The following Information will be used in the deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="eb5da-124">Obsługiwane topologie</span><span class="sxs-lookup"><span data-stu-id="eb5da-124">Supported topologies</span></span>

<span data-ttu-id="eb5da-125">Wybierz jedną z [szablonów usługi Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) do wdrożenia klastra HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="eb5da-125">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="eb5da-126">Poniżej przedstawiono wysokiego poziomu architektury trzy obsługiwanych topologii klastrów.</span><span class="sxs-lookup"><span data-stu-id="eb5da-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="eb5da-127">Topologie wysokiej dostępności obejmują wiele głównymi węzłami klastra.</span><span class="sxs-lookup"><span data-stu-id="eb5da-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="eb5da-128">Klastra o wysokiej dostępności z domeną usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb5da-128">High-availability cluster with Active Directory domain</span></span>

    ![Klastra HA w domenie AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="eb5da-130">Wysoka dostępność klastra bez domeny usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb5da-130">High-availability cluster without Active Directory domain</span></span>

    ![Klastra HA bez domeny usługi AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="eb5da-132">Klaster z jednym węzłem głównym</span><span class="sxs-lookup"><span data-stu-id="eb5da-132">Cluster with a single head node</span></span>

   ![Klaster z jednym węzłem głównym](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="eb5da-134">Wdrażanie klastra</span><span class="sxs-lookup"><span data-stu-id="eb5da-134">Deploy a cluster</span></span>

<span data-ttu-id="eb5da-135">Aby utworzyć klaster, wybierz szablon, a następnie kliknij przycisk **wdrażanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="eb5da-135">To create the cluster, choose a template and click **Deploy to Azure**.</span></span> <span data-ttu-id="eb5da-136">W [portalu Azure](https://portal.azure.com), określ parametry szablonu, zgodnie z opisem w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="eb5da-136">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span></span> <span data-ttu-id="eb5da-137">Każdy szablon tworzy wszystkich zasobów systemu Azure wymaganych przez infrastruktura klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="eb5da-137">Each template creates all Azure resources required for the HPC cluster infrastructure.</span></span> <span data-ttu-id="eb5da-138">Zasoby obejmują sieci wirtualnej platformy Azure, publicznego adresu IP adres usługi równoważenia obciążenia (tylko w przypadku klastra o wysokiej dostępności), interfejsów sieciowych, zestawów dostępności, kont magazynu i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="eb5da-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-the-subscription-location-and-resource-group"></a><span data-ttu-id="eb5da-139">Krok 1: Wybierz subskrypcję, lokalizację i grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="eb5da-139">Step 1: Select the subscription, location, and resource group</span></span>

<span data-ttu-id="eb5da-140">**Subskrypcji** i **lokalizacji** musi być taka sama, określona po przekazaniu certyfikatu PFX (patrz wymagania wstępne).</span><span class="sxs-lookup"><span data-stu-id="eb5da-140">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="eb5da-141">Firma Microsoft zaleca utworzenie **grupy zasobów** dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eb5da-141">We recommend that you create a **Resource group** for the deployment.</span></span>

### <a name="step-2-specify-the-parameter-settings"></a><span data-ttu-id="eb5da-142">Krok 2: Określ ustawienia parametru</span><span class="sxs-lookup"><span data-stu-id="eb5da-142">Step 2: Specify the parameter settings</span></span>

<span data-ttu-id="eb5da-143">Wprowadź lub zmień wartości parametrów szablonu.</span><span class="sxs-lookup"><span data-stu-id="eb5da-143">Enter or modify values for the template parameters.</span></span> <span data-ttu-id="eb5da-144">Kliknij ikonę obok każdego parametru, aby uzyskać pomoc.</span><span class="sxs-lookup"><span data-stu-id="eb5da-144">Click the icon next to each parameter for help information.</span></span> <span data-ttu-id="eb5da-145">Zobacz też wskazówki dotyczące [dostępne rozmiary maszyny Wirtualnej](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="eb5da-145">Also see the guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="eb5da-146">Określ wartości zanotowanych w wymaganiach wstępnych dotyczących następujących parametrów: **nazwę magazynu**, **grupy zasobów magazynu**, **adres URL certyfikatu**, i  **Odcisk palca certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="eb5da-146">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="eb5da-147">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="eb5da-147">Step 3.</span></span> <span data-ttu-id="eb5da-148">Przejrzyj postanowienia prawne i utworzyć</span><span class="sxs-lookup"><span data-stu-id="eb5da-148">Review legal terms and create</span></span>
<span data-ttu-id="eb5da-149">Kliknij przycisk **Przejrzyj postanowienia prawne** Aby przejrzeć postanowienia.</span><span class="sxs-lookup"><span data-stu-id="eb5da-149">Click **Review legal terms** to review the terms.</span></span> <span data-ttu-id="eb5da-150">Jeśli akceptujesz, kliknij przycisk **zakupu**, a następnie kliknij przycisk **Utwórz** do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eb5da-150">If you agree, click **Purchase**, and then click **Create** to start the deployment.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="eb5da-151">Łączenie z klastrem</span><span class="sxs-lookup"><span data-stu-id="eb5da-151">Connect to the cluster</span></span>
1. <span data-ttu-id="eb5da-152">Po wdrożeniu klastra HPC Pack, przejdź do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eb5da-152">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="eb5da-153">Kliknij przycisk **grup zasobów**i Znajdź grupę zasobów, w którym została wdrożona klastra.</span><span class="sxs-lookup"><span data-stu-id="eb5da-153">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span></span> <span data-ttu-id="eb5da-154">Można znaleźć węzła głównego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="eb5da-154">You can find the head node virtual machines.</span></span>

    ![Głównymi węzłami klastra w portalu](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="eb5da-156">Kliknij przycisk jednego węzła głównego (w klastrze wysokiej dostępności kliknij dowolny z węzłów głównych).</span><span class="sxs-lookup"><span data-stu-id="eb5da-156">Click one head node (in a high-availability cluster, click any of the head nodes).</span></span> <span data-ttu-id="eb5da-157">W **Essentials**, można znaleźć publicznego adresu IP lub pełną nazwę DNS klastra.</span><span class="sxs-lookup"><span data-stu-id="eb5da-157">In **Essentials**, you can find the public IP address or full DNS name of the cluster.</span></span>

    ![Ustawienia połączenia klastra](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="eb5da-159">Kliknij przycisk **Connect** aby zalogować się do żadnego z węzłów głównych przy użyciu pulpitu zdalnego z nazwą użytkownika administratora.</span><span class="sxs-lookup"><span data-stu-id="eb5da-159">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="eb5da-160">W przypadku klastra została wdrożona w domenie usługi Active Directory, nazwa użytkownika jest w formie <privateDomainName> \<adminUsername > (na przykład hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="eb5da-160">If the cluster you deployed is in an Active Directory Domain, the user name is of the form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb5da-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb5da-161">Next steps</span></span>
* <span data-ttu-id="eb5da-162">Przesyłanie zadań do klastra.</span><span class="sxs-lookup"><span data-stu-id="eb5da-162">Submit jobs to your cluster.</span></span> <span data-ttu-id="eb5da-163">Zobacz [przesyłania zadań HPC HPC Pack klastra w systemie Azure](hpcpack-cluster-submit-jobs.md) i [Zarządzanie klastra HPC Pack 2016 na platformie Azure przy użyciu usługi Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="eb5da-163">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

