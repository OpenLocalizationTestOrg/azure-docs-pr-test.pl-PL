---
title: "Przekazywania poświadczeń na platformie Azure przy użyciu usługi Konfiguracja DSC | Dokumentacja firmy Microsoft"
description: "Omówienie w bezpieczny sposób przekazywania poświadczeń do maszyn wirtualnych platformy Azure przy użyciu konfiguracji żądanego stanu programu PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: acd768c0219ec23c0453a65c575faf5213d9c616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="passing-credentials-to-the-azure-dsc-extension-handler"></a><span data-ttu-id="e12fc-103">Przekazywania poświadczeń do obsługi rozszerzenia usługi Konfiguracja DSC Azure</span><span class="sxs-lookup"><span data-stu-id="e12fc-103">Passing credentials to the Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e12fc-104">W tym artykule omówiono rozszerzenia konfiguracji żądanego stanu dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e12fc-104">This article covers the Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="e12fc-105">Omówienie obsługi rozszerzenia DSC można znaleźć w folderze [wprowadzenie do obsługi rozszerzenia konfiguracji żądanego stanu Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e12fc-105">An overview of the DSC extension handler can be found at [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="e12fc-106">Przekazywanie poświadczeń</span><span class="sxs-lookup"><span data-stu-id="e12fc-106">Passing in credentials</span></span>
<span data-ttu-id="e12fc-107">W ramach procesu konfiguracji może skonfigurować konta użytkowników, dostęp do usług, lub zainstalować program w kontekście użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e12fc-107">As a part of the configuration process, you may need to set up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="e12fc-108">Aby wykonać te czynności, musisz podać poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="e12fc-108">To do these things, you need to provide credentials.</span></span> 

<span data-ttu-id="e12fc-109">DSC umożliwia sparametryzowane konfiguracji, w których poświadczenia są przekazywane do konfiguracji i bezpiecznie przechowywane w plikach MOF.</span><span class="sxs-lookup"><span data-stu-id="e12fc-109">DSC allows for parameterized configurations in which credentials are passed into the configuration and securely stored in MOF files.</span></span> <span data-ttu-id="e12fc-110">Obsługi rozszerzenia Azure ułatwia zarządzanie poświadczeniami, zapewniając automatyczne zarządzanie certyfikatami.</span><span class="sxs-lookup"><span data-stu-id="e12fc-110">The Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="e12fc-111">Rozważmy poniższy skrypt konfiguracji DSC tworzy konto użytkownika lokalnego z określonym hasłem:</span><span class="sxs-lookup"><span data-stu-id="e12fc-111">Consider the following DSC configuration script that creates a local user account with the specified password:</span></span>

<span data-ttu-id="e12fc-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="e12fc-112">*user_configuration.ps1*</span></span>

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

<span data-ttu-id="e12fc-113">Należy uwzględnić *localhost węzła* jako część konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e12fc-113">It is important to include *node localhost* as part of the configuration.</span></span> <span data-ttu-id="e12fc-114">W przypadku braku tej instrukcji następujące kroki nie działają zgodnie z obsługi rozszerzenia w szczególności szuka instrukcji localhost węzła.</span><span class="sxs-lookup"><span data-stu-id="e12fc-114">If this statement is missing, the following steps do not work as the extension handler specifically looks for the node localhost statement.</span></span> <span data-ttu-id="e12fc-115">Należy również uwzględnić typecast *[PsCredential]*, ponieważ rozszerzenie do szyfrowania poświadczeń wyzwala określonego typu.</span><span class="sxs-lookup"><span data-stu-id="e12fc-115">It is also important to include the typecast *[PsCredential]*, as this specific type triggers the extension to encrypt the credential.</span></span> 

<span data-ttu-id="e12fc-116">Publikuj ten skrypt do magazynu obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="e12fc-116">Publish this script to blob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="e12fc-117">Ustawienia rozszerzenia usługi Konfiguracja DSC Azure i podaj poświadczenia:</span><span class="sxs-lookup"><span data-stu-id="e12fc-117">Set the Azure DSC extension and provide the credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="e12fc-118">Jak są zabezpieczone poświadczeń</span><span class="sxs-lookup"><span data-stu-id="e12fc-118">How credentials are secured</span></span>
<span data-ttu-id="e12fc-119">Uruchomienie tego kodu wyświetla monit o podanie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e12fc-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="e12fc-120">Gdy podano, jest on przechowywany w pamięci krótko.</span><span class="sxs-lookup"><span data-stu-id="e12fc-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="e12fc-121">Jeśli jest publikowany razem `Set-AzureVmDscExtension` polecenia cmdlet, jego są przesyłane za pośrednictwem protokołu HTTPS do maszyny Wirtualnej, w przypadku, gdy usługa Azure przechowuje go szyfrowane na dysku, przy użyciu lokalnego certyfikatu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e12fc-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS to the VM, where Azure stores it encrypted on disk, using the local VM certificate.</span></span> <span data-ttu-id="e12fc-122">Następnie jest krótko odszyfrowane w pamięci i ponownie szyfrowane przekazywany do usługi Konfiguracja DSC.</span><span class="sxs-lookup"><span data-stu-id="e12fc-122">Then it is briefly decrypted in memory and re-encrypted to pass it to DSC.</span></span>

<span data-ttu-id="e12fc-123">To zachowanie różni się od [za pomocą bezpiecznej konfiguracji bez obsługi rozszerzenia](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="e12fc-123">This behavior is different than [using secure configurations without the extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="e12fc-124">Środowisko Azure udostępnia sposób przekazują dane konfiguracji w bezpieczny sposób za pomocą certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="e12fc-124">The Azure environment gives a way to transmit configuration data securely via certificates.</span></span> <span data-ttu-id="e12fc-125">Korzystając z procedury obsługi rozszerzenia DSC, nie jest konieczne do zapewnienia $CertificatePath lub $CertificateID / $Thumbprint wpis w ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="e12fc-125">When using the DSC extension handler, there is no need to provide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e12fc-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e12fc-126">Next steps</span></span>
<span data-ttu-id="e12fc-127">Aby uzyskać więcej informacji dotyczących obsługi rozszerzenia usługi Konfiguracja DSC Azure, zobacz [wprowadzenie do obsługi rozszerzenia konfiguracji żądanego stanu Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e12fc-127">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="e12fc-128">Sprawdź [szablonu usługi Azure Resource Manager dla rozszerzenia DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e12fc-128">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e12fc-129">Aby uzyskać więcej informacji o konfiguracji DSC środowiska PowerShell [odwiedź Centrum dokumentacji programu PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="e12fc-129">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="e12fc-130">Aby znaleźć dodatkowe funkcje, którymi można zarządzać w DSC środowiska PowerShell [przeglądać galerii programu PowerShell](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) więcej zasobów usługi Konfiguracja DSC.</span><span class="sxs-lookup"><span data-stu-id="e12fc-130">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

