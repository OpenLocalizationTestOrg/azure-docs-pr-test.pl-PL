---
title: "aaaPassing poświadczeń przy użyciu usługi Konfiguracja DSC tooAzure | Dokumentacja firmy Microsoft"
description: "Omówienie w bezpieczny sposób przekazywania poświadczeń tooAzure maszyn wirtualnych przy użyciu konfiguracji żądanego stanu programu PowerShell"
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
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="b1a10-103">Przekazywanie obsługi rozszerzenia usługi Konfiguracja DSC Azure toohello poświadczeń</span><span class="sxs-lookup"><span data-stu-id="b1a10-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b1a10-104">W tym artykule omówiono hello konfiguracji żądanego stanu rozszerzenia dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a10-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="b1a10-105">Omówienie hello DSC rozszerzenia obsługi można znaleźć w folderze [wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1a10-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="b1a10-106">Przekazywanie poświadczeń</span><span class="sxs-lookup"><span data-stu-id="b1a10-106">Passing in credentials</span></span>
<span data-ttu-id="b1a10-107">W ramach procesu konfiguracji hello, może być konieczne tooset do kont użytkowników, dostęp do usług, lub zainstaluj program w kontekście użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b1a10-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="b1a10-108">toodo elementy potrzebne tooprovide poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="b1a10-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="b1a10-109">DSC umożliwia sparametryzowane konfiguracji, w których poświadczenia są przekazywane do konfiguracji hello i bezpiecznie przechowywane w plikach MOF.</span><span class="sxs-lookup"><span data-stu-id="b1a10-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="b1a10-110">Hello Azure rozszerzenia obsługi ułatwia zarządzanie poświadczeniami, zapewniając automatyczne zarządzanie certyfikatami.</span><span class="sxs-lookup"><span data-stu-id="b1a10-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="b1a10-111">Należy wziąć pod uwagę hello następującego skryptu konfiguracji DSC, która tworzy konto użytkownika lokalnego z hello określone hasło:</span><span class="sxs-lookup"><span data-stu-id="b1a10-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="b1a10-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="b1a10-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="b1a10-113">Jest ważne tooinclude *localhost węzła* w ramach konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="b1a10-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="b1a10-114">W przypadku braku tej instrukcji hello następujące kroki nie działają jako hello rozszerzenia obsługi specjalnie szuka hello węzła localhost instrukcji.</span><span class="sxs-lookup"><span data-stu-id="b1a10-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="b1a10-115">Rzutowanie typu tooinclude hello ważna jest również *[PsCredential]*, ponieważ poświadczenia hello tooencrypt rozszerzenia hello wyzwala określonego typu.</span><span class="sxs-lookup"><span data-stu-id="b1a10-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="b1a10-116">Publikuj ten magazyn tooblob skryptu:</span><span class="sxs-lookup"><span data-stu-id="b1a10-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="b1a10-117">Ustaw hello rozszerzenia usługi Konfiguracja DSC Azure i podaj poświadczenia, hello:</span><span class="sxs-lookup"><span data-stu-id="b1a10-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="b1a10-118">Jak są zabezpieczone poświadczeń</span><span class="sxs-lookup"><span data-stu-id="b1a10-118">How credentials are secured</span></span>
<span data-ttu-id="b1a10-119">Uruchomienie tego kodu wyświetla monit o podanie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b1a10-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="b1a10-120">Gdy podano, jest on przechowywany w pamięci krótko.</span><span class="sxs-lookup"><span data-stu-id="b1a10-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="b1a10-121">Jeśli jest publikowany razem `Set-AzureVmDscExtension` polecenia cmdlet, jego są przesyłane za pośrednictwem protokołu HTTPS toohello maszyny Wirtualnej, w przypadku, gdy Azure przechowuje go szyfrowane na dysku, przy użyciu hello lokalnego certyfikatu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1a10-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="b1a10-122">A następnie jest krótko odszyfrowane w pamięci i ponownie szyfrować toopass go tooDSC.</span><span class="sxs-lookup"><span data-stu-id="b1a10-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="b1a10-123">To zachowanie różni się od [za pomocą bezpiecznej konfiguracji bez obsługi rozszerzenia hello](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="b1a10-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="b1a10-124">Witaj środowiska platformy Azure zapewnia dane konfiguracji tootransmit w sposób bezpieczny sposób za pomocą certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="b1a10-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="b1a10-125">Przy użyciu obsługi rozszerzenia hello DSC, nie ma żadnych tooprovide potrzeby $CertificatePath lub $CertificateID / $Thumbprint wpis w ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="b1a10-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1a10-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1a10-126">Next steps</span></span>
<span data-ttu-id="b1a10-127">Aby uzyskać więcej informacji dotyczących obsługi rozszerzenia usługi Konfiguracja DSC Azure hello, zobacz [wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1a10-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="b1a10-128">Sprawdź hello [szablonu usługi Azure Resource Manager dla rozszerzenia hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1a10-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="b1a10-129">Aby uzyskać więcej informacji o konfiguracji DSC środowiska PowerShell [odwiedź Centrum dokumentacji programu PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="b1a10-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="b1a10-130">dodatkowe funkcje toofind można zarządzać w usłudze Konfiguracja DSC środowiska PowerShell, [Przejrzyj galerię programu PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) więcej zasobów usługi Konfiguracja DSC.</span><span class="sxs-lookup"><span data-stu-id="b1a10-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

