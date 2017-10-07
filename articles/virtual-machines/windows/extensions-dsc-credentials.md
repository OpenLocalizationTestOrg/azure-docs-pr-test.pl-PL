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
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>Przekazywanie obsługi rozszerzenia usługi Konfiguracja DSC Azure toohello poświadczeń
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

W tym artykule omówiono hello konfiguracji żądanego stanu rozszerzenia dla platformy Azure. Omówienie hello DSC rozszerzenia obsługi można znaleźć w folderze [wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Przekazywanie poświadczeń
W ramach procesu konfiguracji hello, może być konieczne tooset do kont użytkowników, dostęp do usług, lub zainstaluj program w kontekście użytkownika. toodo elementy potrzebne tooprovide poświadczenia. 

DSC umożliwia sparametryzowane konfiguracji, w których poświadczenia są przekazywane do konfiguracji hello i bezpiecznie przechowywane w plikach MOF. Hello Azure rozszerzenia obsługi ułatwia zarządzanie poświadczeniami, zapewniając automatyczne zarządzanie certyfikatami. 

Należy wziąć pod uwagę hello następującego skryptu konfiguracji DSC, która tworzy konto użytkownika lokalnego z hello określone hasło:

*user_configuration.ps1*

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

Jest ważne tooinclude *localhost węzła* w ramach konfiguracji hello. W przypadku braku tej instrukcji hello następujące kroki nie działają jako hello rozszerzenia obsługi specjalnie szuka hello węzła localhost instrukcji. Rzutowanie typu tooinclude hello ważna jest również *[PsCredential]*, ponieważ poświadczenia hello tooencrypt rozszerzenia hello wyzwala określonego typu. 

Publikuj ten magazyn tooblob skryptu:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Ustaw hello rozszerzenia usługi Konfiguracja DSC Azure i podaj poświadczenia, hello:

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>Jak są zabezpieczone poświadczeń
Uruchomienie tego kodu wyświetla monit o podanie poświadczeń. Gdy podano, jest on przechowywany w pamięci krótko. Jeśli jest publikowany razem `Set-AzureVmDscExtension` polecenia cmdlet, jego są przesyłane za pośrednictwem protokołu HTTPS toohello maszyny Wirtualnej, w przypadku, gdy Azure przechowuje go szyfrowane na dysku, przy użyciu hello lokalnego certyfikatu maszyny Wirtualnej. A następnie jest krótko odszyfrowane w pamięci i ponownie szyfrować toopass go tooDSC.

To zachowanie różni się od [za pomocą bezpiecznej konfiguracji bez obsługi rozszerzenia hello](https://msdn.microsoft.com/powershell/dsc/securemof). Witaj środowiska platformy Azure zapewnia dane konfiguracji tootransmit w sposób bezpieczny sposób za pomocą certyfikatów. Przy użyciu obsługi rozszerzenia hello DSC, nie ma żadnych tooprovide potrzeby $CertificatePath lub $CertificateID / $Thumbprint wpis w ConfigurationData.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji dotyczących obsługi rozszerzenia usługi Konfiguracja DSC Azure hello, zobacz [wprowadzenie toohello Azure konfiguracji żądanego stanu rozszerzenia obsługi](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Sprawdź hello [szablonu usługi Azure Resource Manager dla rozszerzenia hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Aby uzyskać więcej informacji o konfiguracji DSC środowiska PowerShell [odwiedź Centrum dokumentacji programu PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

dodatkowe funkcje toofind można zarządzać w usłudze Konfiguracja DSC środowiska PowerShell, [Przejrzyj galerię programu PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) więcej zasobów usługi Konfiguracja DSC.

