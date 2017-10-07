---
title: zasoby aaaCertificate automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Certyfikaty można bezpiecznie przechowywane w usłudze Automatyzacja Azure, są one dostępne przez elementy runbook lub tooauthenticate konfiguracji DSC dla platformy Azure i zasobów firm zewnętrznych.  W tym artykule opisano szczegóły hello certyfikatów i w jaki sposób toowork z nimi w tworzeniu zarówno tekstową i graficznego."
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
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="8f77b-104">Zasoby certyfikatu usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="8f77b-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="8f77b-105">Certyfikaty mogą być bezpiecznie przechowywane w automatyzacji Azure, są one dostępne przez elementy runbook lub przy użyciu hello konfiguracji DSC **Get AzureRmAutomationRmCertificate** działania dla zasobów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8f77b-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="8f77b-106">To pozwala toocreate elementów runbook i konfiguracji DSC, które korzystają z certyfikatów do uwierzytelniania lub dodaje je tooAzure lub innych firm.</span><span class="sxs-lookup"><span data-stu-id="8f77b-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="8f77b-107">Bezpiecznych zasobów w automatyzacji Azure obejmują poświadczeń, certyfikatów, połączeń i szyfrowane zmienne.</span><span class="sxs-lookup"><span data-stu-id="8f77b-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="8f77b-108">Te zasoby są szyfrowane i przechowywane w hello automatyzacji Azure za pomocą Unikatowy klucz, który jest generowany dla każdego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="8f77b-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="8f77b-109">Ten klucz jest zaszyfrowany za pomocą certyfikatu głównego i przechowywane w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="8f77b-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="8f77b-110">Przed zapisaniem zabezpieczonym zasobem, hello klucza dla konta automatyzacji hello jest odszyfrowywany za pomocą certyfikatu głównego hello i służyły tooencrypt hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="8f77b-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="8f77b-111">Polecenia cmdlet programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f77b-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="8f77b-112">polecenia cmdlet Hello w hello w poniższej tabeli są używane toocreate i zarządzać zasobami certyfikatu usługi Automatyzacja przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f77b-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="8f77b-113">One dostarczane jako część hello [modułu Azure PowerShell](../powershell-install-configure.md) która jest dostępna na potrzeby automatyzacji elementów runbook i konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="8f77b-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="8f77b-114">Polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="8f77b-114">Cmdlets</span></span>|<span data-ttu-id="8f77b-115">Opis</span><span class="sxs-lookup"><span data-stu-id="8f77b-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="8f77b-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="8f77b-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="8f77b-117">Pobiera informacje o toouse certyfikatu, element runbook lub konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="8f77b-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="8f77b-118">Sam certyfikat hello można pobrać tylko z działania Get AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="8f77b-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="8f77b-119">Nowe AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="8f77b-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="8f77b-120">Tworzy nowy certyfikat w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="8f77b-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="8f77b-121">Usuń AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="8f77b-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="8f77b-122">Usuwa certyfikat usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="8f77b-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="8f77b-123">Tworzy nowy certyfikat w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="8f77b-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="8f77b-124">Zestaw AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="8f77b-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="8f77b-125">Ustawia właściwości hello istniejącego certyfikatu, takich jak przekazywanie pliku certyfikatu hello i ustawienie hello hasło dla pliku pfx.</span><span class="sxs-lookup"><span data-stu-id="8f77b-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="8f77b-126">Dodaj AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="8f77b-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="8f77b-127">Przekazywanie certyfikatu usługi dla hello określona usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="8f77b-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="8f77b-128">Tworzenie nowego certyfikatu</span><span class="sxs-lookup"><span data-stu-id="8f77b-128">Creating a new certificate</span></span>

<span data-ttu-id="8f77b-129">Podczas tworzenia nowego certyfikatu, możesz przekazać cer lub PFX pliku tooAzure automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="8f77b-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="8f77b-130">Jeśli certyfikat hello jako możliwy do wyeksportowania, następnie można przenieść go z magazynu certyfikatów usługi Automatyzacja Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8f77b-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="8f77b-131">Jeśli nie jest możliwy do wyeksportowania, następnie można można używać tylko do podpisywania w ramach elementu runbook hello lub konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="8f77b-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="8f77b-132">toocreate nowy certyfikat z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8f77b-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="8f77b-133">Twoje konto usługi Automatyzacja kliknij hello **zasoby** hello tooopen kafelka **zasoby** bloku.</span><span class="sxs-lookup"><span data-stu-id="8f77b-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="8f77b-134">Kliknij przycisk hello **certyfikaty** hello tooopen kafelka **certyfikaty** bloku.</span><span class="sxs-lookup"><span data-stu-id="8f77b-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="8f77b-135">Kliknij przycisk **Dodawanie certyfikatu** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="8f77b-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="8f77b-136">Wpisz nazwę certyfikatu hello hello **nazwa** pole.</span><span class="sxs-lookup"><span data-stu-id="8f77b-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="8f77b-137">Kliknij przycisk **wybierz plik** w obszarze **przekazać plik certyfikatu** toobrowse dla pliku cer lub pfx.</span><span class="sxs-lookup"><span data-stu-id="8f77b-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="8f77b-138">W przypadku wybrania pliku PFX, określ hasło oraz czy jej powinno być dozwolone toobe wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="8f77b-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="8f77b-139">Kliknij przycisk **Utwórz** toosave hello nowy zasób certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="8f77b-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="8f77b-140">toocreate nowy certyfikat przy użyciu programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f77b-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="8f77b-141">Hello poniższym przykładzie pokazano, jak toocreate automatyzacji nowego certyfikatu i oznacz ją jako eksportowalny.</span><span class="sxs-lookup"><span data-stu-id="8f77b-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="8f77b-142">To importuje istniejący plik pfx.</span><span class="sxs-lookup"><span data-stu-id="8f77b-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="8f77b-143">Przy użyciu certyfikatu</span><span class="sxs-lookup"><span data-stu-id="8f77b-143">Using a certificate</span></span>

<span data-ttu-id="8f77b-144">Należy użyć hello **Get-AutomationCertificate** toouse działania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="8f77b-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="8f77b-145">Nie można użyć hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) polecenia cmdlet, ponieważ zwraca informacje o hello zasób certyfikatu, ale nie hello sam certyfikat.</span><span class="sxs-lookup"><span data-stu-id="8f77b-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="8f77b-146">Przykład tekstowy</span><span class="sxs-lookup"><span data-stu-id="8f77b-146">Textual runbook sample</span></span>

<span data-ttu-id="8f77b-147">powitania po przykładowy kod pokazuje, jak tooadd tooa certyfikatu w chmurze usługi w elemencie runbook.</span><span class="sxs-lookup"><span data-stu-id="8f77b-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="8f77b-148">W tym przykładzie hasło hello jest pobierana z zmiennej automatyzacji zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="8f77b-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="8f77b-149">Przykładowe graficznym elementem runbook</span><span class="sxs-lookup"><span data-stu-id="8f77b-149">Graphical runbook sample</span></span>

<span data-ttu-id="8f77b-150">Możesz dodać **Get-AutomationCertificate** tooa graficznym elementem runbook, klikając prawym przyciskiem myszy na powitania certyfikatu w okienku Biblioteka hello hello edytora graficznego i wybierając **dodać toocanvas**.</span><span class="sxs-lookup"><span data-stu-id="8f77b-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Dodaj certyfikat toohello kanwy](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="8f77b-152">Witaj poniższej ilustracji przedstawiono przykład za pomocą certyfikatu w graficznym elementem runbook.</span><span class="sxs-lookup"><span data-stu-id="8f77b-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="8f77b-153">Jest to hello tym samym przykładzie pokazano powyżej dodawania usługi w chmurze tooa certyfikatu z poziomu tekstowy.</span><span class="sxs-lookup"><span data-stu-id="8f77b-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="8f77b-154">Przykład tworzenia graficznego</span><span class="sxs-lookup"><span data-stu-id="8f77b-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="8f77b-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8f77b-155">Next steps</span></span>

- <span data-ttu-id="8f77b-156">więcej informacji na temat pracy z łącza toocontrol hello logicznego przepływu działania elementu runbook jest toolearn zaprojektowane tooperform, zobacz [łącza w tworzeniu graficznego](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="8f77b-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
