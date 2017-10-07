---
title: "aaaUse toocreate środowiska PowerShell usługi Azure AD tooaccess aplikacji hello interfejsu API usługi Azure Media Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse PowerShell toocreate aplikację usługi Azure Active Directory (Azure AD) i skonfiguruj tooaccess hello Azure Media Services API."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>PowerShell toocreate toouse aplikacji usługi Azure AD za pomocą hello interfejsu API usługi Azure Media Services

Dowiedz się, jak toouse programu PowerShell skrypt toocreate aplikacji usługi Azure Active Directory (Azure AD) i tooaccess główną usługi Azure Media Services zasobów.  

## <a name="prerequisites"></a>Wymagania wstępne

- Konto platformy Azure. Jeśli nie masz konta, Rozpocznij od [Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). 
- Konto usługi Media Services. Aby uzyskać więcej informacji, zobacz [utworzyć konto usługi Azure Media Services w portalu Azure hello](media-services-portal-create-account.md).
- Wersja programu PowerShell Azure 0.8.8 lub nowszym. Aby uzyskać więcej informacji, zobacz [jak toouse programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Polecenia cmdlet Menedżera zasobów systemu Azure.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Utwórz aplikację usługi Azure AD za pomocą programu PowerShell  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

Aby uzyskać więcej informacji zobacz następujące artykuły hello:

- [Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Zarządzanie oparte na rolach kontroli dostępu przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Jak skonfigurować toomanually demon aplikacji za pomocą certyfikatów](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Następne kroki

Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-portal-upload-files.md).
