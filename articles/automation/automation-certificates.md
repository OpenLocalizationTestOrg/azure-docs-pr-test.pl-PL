---
title: Zasoby w automatyzacji Azure certyfikatu | Dokumentacja firmy Microsoft
description: "Certyfikaty można bezpiecznie przechowywane w usłudze Automatyzacja Azure, są one dostępne przez elementy runbook lub konfiguracji DSC do uwierzytelniania Azure i innych firm zasobów.  W tym artykule szczegółowo opisano certyfikaty i sposobu pracy z nimi w tworzeniu zarówno tekstową i graficznego."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="75e28-104">Zasoby certyfikatu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="75e28-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="75e28-105">Certyfikaty mogą być bezpiecznie przechowywane w automatyzacji Azure, są one dostępne przez elementy runbook lub przy użyciu konfiguracji DSC **Get AzureRmAutomationRmCertificate** działania dla zasobów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="75e28-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="75e28-106">Służy do tworzenia elementów runbook i konfiguracji DSC, które korzystają z certyfikatów do uwierzytelniania, lub dodaje je do platformy Azure lub innej zasobów.</span><span class="sxs-lookup"><span data-stu-id="75e28-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="75e28-107">Bezpiecznych zasobów w automatyzacji Azure obejmują poświadczeń, certyfikatów, połączeń i szyfrowane zmienne.</span><span class="sxs-lookup"><span data-stu-id="75e28-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="75e28-108">Te zasoby są szyfrowane i przechowywane w automatyzacji Azure za pomocą Unikatowy klucz, który jest generowany dla każdego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="75e28-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="75e28-109">Ten klucz jest zaszyfrowany za pomocą certyfikatu głównego i przechowywane w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="75e28-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="75e28-110">Przed zapisaniem zabezpieczonym zasobem, klucza dla konta automatyzacji zostaną odszyfrowane przy użyciu certyfikatu głównego, a następnie używany do szyfrowania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="75e28-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="75e28-111">Polecenia cmdlet programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="75e28-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="75e28-112">Polecenia cmdlet w poniższej tabeli służą do tworzenia i zarządzania zasobami certyfikatu usługi Automatyzacja przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="75e28-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="75e28-113">One dostarczane jako część [modułu Azure PowerShell](../powershell-install-configure.md) która jest dostępna na potrzeby automatyzacji elementów runbook i konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="75e28-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="75e28-114">Polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="75e28-114">Cmdlets</span></span>|<span data-ttu-id="75e28-115">Opis</span><span class="sxs-lookup"><span data-stu-id="75e28-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="75e28-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="75e28-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="75e28-117">Pobiera informacje o certyfikat do użycia w element runbook lub konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="75e28-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="75e28-118">Sam certyfikat można pobierać tylko z działania Get AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="75e28-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="75e28-119">Nowe AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="75e28-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="75e28-120">Tworzy nowy certyfikat w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="75e28-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="75e28-121">Usuń AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="75e28-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="75e28-122">Usuwa certyfikat usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="75e28-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="75e28-123">Tworzy nowy certyfikat w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="75e28-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="75e28-124">Zestaw AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="75e28-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="75e28-125">Ustawia właściwości istniejącego certyfikatu, włącznie z przekazywaniem pliku certyfikatu i ustawianiem hasła dla pliku pfx.</span><span class="sxs-lookup"><span data-stu-id="75e28-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="75e28-126">Dodaj AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="75e28-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="75e28-127">Przekazywanie certyfikatu usługi dla usługi określonej chmury.</span><span class="sxs-lookup"><span data-stu-id="75e28-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="75e28-128">Tworzenie nowego certyfikatu</span><span class="sxs-lookup"><span data-stu-id="75e28-128">Creating a new certificate</span></span>

<span data-ttu-id="75e28-129">Podczas tworzenia nowego certyfikatu, możesz przekazać plik cer lub PFX do automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="75e28-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="75e28-130">Jeśli zostanie oznaczony jako możliwy do wyeksportowania certyfikatu, następnie można przenieść go z magazynu certyfikatów usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="75e28-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="75e28-131">Jeśli nie jest możliwy do wyeksportowania, następnie można można używać tylko do podpisywania w ramach elementu runbook lub konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="75e28-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="75e28-132">Aby utworzyć nowy certyfikat za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="75e28-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="75e28-133">Twoje konto usługi Automatyzacja kliknij **zasoby** Kafelek, aby otworzyć **zasoby** bloku.</span><span class="sxs-lookup"><span data-stu-id="75e28-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="75e28-134">Kliknij przycisk **certyfikaty** Kafelek, aby otworzyć **certyfikaty** bloku.</span><span class="sxs-lookup"><span data-stu-id="75e28-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="75e28-135">Kliknij przycisk **Dodawanie certyfikatu** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="75e28-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="75e28-136">Wpisz nazwę certyfikatu w **nazwa** pole.</span><span class="sxs-lookup"><span data-stu-id="75e28-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="75e28-137">Kliknij przycisk **wybierz plik** w obszarze **przekazać plik certyfikatu** do Przeglądaj w poszukiwaniu pliku cer lub pfx.</span><span class="sxs-lookup"><span data-stu-id="75e28-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="75e28-138">W przypadku wybrania pliku PFX, określ hasło oraz czy powinno być dozwolone do wyeksportowania.</span><span class="sxs-lookup"><span data-stu-id="75e28-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="75e28-139">Kliknij przycisk **Utwórz** do zapisywania nowego elementu zawartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="75e28-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="75e28-140">Aby utworzyć nowy certyfikat za pomocą środowiska Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="75e28-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="75e28-141">W poniższym przykładzie pokazano sposób tworzenia nowego certyfikatu usługi Automatyzacja i oznacz ją jako eksportowalny.</span><span class="sxs-lookup"><span data-stu-id="75e28-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="75e28-142">To importuje istniejący plik pfx.</span><span class="sxs-lookup"><span data-stu-id="75e28-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="75e28-143">Przy użyciu certyfikatu</span><span class="sxs-lookup"><span data-stu-id="75e28-143">Using a certificate</span></span>

<span data-ttu-id="75e28-144">Należy użyć **Get AutomationCertificate** działanie do używania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="75e28-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="75e28-145">Nie można użyć [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) polecenia cmdlet, ponieważ zwraca informacje o zasób certyfikatu, ale nie sam certyfikat.</span><span class="sxs-lookup"><span data-stu-id="75e28-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="75e28-146">Przykład tekstowy</span><span class="sxs-lookup"><span data-stu-id="75e28-146">Textual runbook sample</span></span>

<span data-ttu-id="75e28-147">Następujący przykładowy kod przedstawia sposób dodawania certyfikatu do usługi w chmurze w elemencie runbook.</span><span class="sxs-lookup"><span data-stu-id="75e28-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="75e28-148">W tym przykładzie hasło jest pobierana z zmiennej automatyzacji zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="75e28-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="75e28-149">Przykładowe graficznym elementem runbook</span><span class="sxs-lookup"><span data-stu-id="75e28-149">Graphical runbook sample</span></span>

<span data-ttu-id="75e28-150">Możesz dodać **Get-AutomationCertificate** na graficzny element runbook prawym przyciskiem myszy certyfikat w okienku Biblioteka edytora graficznego i wybierając **Dodaj do kanwy**.</span><span class="sxs-lookup"><span data-stu-id="75e28-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![Dodawanie certyfikatu do obszaru roboczego](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="75e28-152">Na poniższej ilustracji przedstawiono przykład za pomocą certyfikatu w graficznym elementem runbook.</span><span class="sxs-lookup"><span data-stu-id="75e28-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="75e28-153">To jest tym samym przykładzie pokazano powyżej dla Dodawanie certyfikatu usługi w chmurze z tekstowy.</span><span class="sxs-lookup"><span data-stu-id="75e28-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="75e28-154">Przykład tworzenia graficznego</span><span class="sxs-lookup"><span data-stu-id="75e28-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="75e28-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="75e28-155">Next steps</span></span>

- <span data-ttu-id="75e28-156">Aby dowiedzieć się więcej o pracy z łącza w celu kontroli przepływu logicznego wynikającego z elementem runbook służy do wykonywania działań, zobacz [łącza w tworzeniu graficznego](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="75e28-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
