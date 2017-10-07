---
title: "aaaSet WinRM dostępu dla maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Konfiguracja dostępu do usługi WinRM do użytku z maszyny wirtualnej platformy Azure utworzonych w modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="ada22-103">Konfigurowanie usługi WinRM dostępu dla maszyn wirtualnych w usłudze Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ada22-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="ada22-104">Usługa WinRM w programie vs zarządzania usługą Azure usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ada22-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="ada22-105">Omówienie hello Azure Resource Manager, zobacz to [artykułu](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ada22-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="ada22-106">Różnice między zarządzania usługą Azure i usługi Azure Resource Manager, zobacz to [artykułu](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="ada22-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="ada22-107">Witaj klucza różnica w Określanie konfiguracji usługi WinRM między dwa stosy hello jest jak hello certyfikatu są instalowane na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ada22-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="ada22-108">W stosie usługi Azure Resource Manager hello certyfikaty hello są modelowane jako zasobów zarządzanych przez hello dostawcy zasobów magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="ada22-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="ada22-109">W związku z tym hello użytkownika wymaga tooprovide własnych certyfikatów i przekaż go tooa Key Vault przed jego użyciem w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ada22-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="ada22-110">Poniżej przedstawiono kroki hello należy tooset tootake w górę Maszynę wirtualną z połączeniem WinRM</span><span class="sxs-lookup"><span data-stu-id="ada22-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="ada22-111">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="ada22-111">Create a Key Vault</span></span>
2. <span data-ttu-id="ada22-112">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="ada22-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="ada22-113">Przekaż tooKey Twojego certyfikatu z podpisem własnym magazynie</span><span class="sxs-lookup"><span data-stu-id="ada22-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="ada22-114">Uzyskać adres URL hello z certyfikatu z podpisem własnym w hello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="ada22-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="ada22-115">Odwołanie adres URL certyfikaty z podpisem własnym podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ada22-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="ada22-116">Krok 1: Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="ada22-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="ada22-117">Można użyć hello poniżej polecenia toocreate hello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="ada22-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="ada22-118">Krok 2: Tworzenie certyfikatu z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="ada22-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="ada22-119">Można utworzyć certyfikatu z podpisem własnym za pomocą tego skryptu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ada22-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="ada22-120">Krok 3: Przekaż toohello Twojego certyfikatu z podpisem własnym magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="ada22-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="ada22-121">Przed przekazywania hello toohello certyfikatu usługi Key Vault utworzonego w kroku 1, musi on tooconverted w formacie hello będzie zrozumiałe dostawcy zasobów Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="ada22-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="ada22-122">zezwala na powitania poniższego skryptu programu PowerShell można to zrobić</span><span class="sxs-lookup"><span data-stu-id="ada22-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="ada22-123">Krok 4: Uzyskać adres URL hello z certyfikatu z podpisem własnym w hello magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="ada22-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="ada22-124">dostawcy zasobów Microsoft.Compute Hello musi mieć klucz tajny toohello adres URL wewnątrz hello Key Vault podczas inicjowania obsługi administracyjnej hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ada22-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="ada22-125">To umożliwia Microsoft.Compute hello zasobów toodownload dostawcy hello klucz tajny i utworzyć certyfikat równoważne hello na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ada22-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="ada22-126">adres URL Hello hello klucz tajny musi również tooinclude hello wersji.</span><span class="sxs-lookup"><span data-stu-id="ada22-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="ada22-127">Przykładowy adres URL wygląda jak poniżej https://contosovault.vault.azure.net:443/klucze tajne/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="ada22-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="ada22-128">Szablony</span><span class="sxs-lookup"><span data-stu-id="ada22-128">Templates</span></span>
<span data-ttu-id="ada22-129">Adres URL toohello łącza hello można uzyskać w szablonie hello przy użyciu hello poniższego kodu</span><span class="sxs-lookup"><span data-stu-id="ada22-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="ada22-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ada22-130">PowerShell</span></span>
<span data-ttu-id="ada22-131">Możesz uzyskać ten adres URL przy użyciu hello poniżej polecenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ada22-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="ada22-132">Krok 5: Odwołanie adres URL certyfikaty z podpisem własnym podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ada22-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="ada22-133">Szablony usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ada22-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="ada22-134">Podczas tworzenia maszyny Wirtualnej za pomocą szablonów, certyfikat hello pobiera odwołanie do w hello kluczy tajnych i hello winRM sekcji zgodnie z poniższymi instrukcjami:</span><span class="sxs-lookup"><span data-stu-id="ada22-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="ada22-135">Przykładowy szablon dla hello powyżej można znaleźć tutaj na [201 vm-winrm-keyvault — windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="ada22-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="ada22-136">Kod źródłowy dla tego szablonu można znaleźć w [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="ada22-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="ada22-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ada22-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="ada22-138">Krok 6: Łączenie toohello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ada22-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="ada22-139">Zanim będzie można połączyć toohello maszyny Wirtualnej należy toomake się, że komputer jest skonfigurowany do zdalnego zarządzania usługi WinRM.</span><span class="sxs-lookup"><span data-stu-id="ada22-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="ada22-140">Uruchom program PowerShell jako administrator, a następnie wykonaj hello poniżej polecenia toomake się, że jest skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="ada22-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="ada22-141">Może być konieczne toomake się, że hello Usługa WinRM jest uruchomiona, jeśli hello powyżej nie działa.</span><span class="sxs-lookup"><span data-stu-id="ada22-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="ada22-142">Możesz zrobić tego za pomocą`Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="ada22-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="ada22-143">Po zakończeniu instalacji hello możesz połączyć toohello maszyny Wirtualnej przy użyciu hello poniżej polecenia</span><span class="sxs-lookup"><span data-stu-id="ada22-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
