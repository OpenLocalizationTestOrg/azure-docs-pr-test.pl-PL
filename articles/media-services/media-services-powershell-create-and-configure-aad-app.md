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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="77b3f-103">PowerShell toocreate toouse aplikacji usługi Azure AD za pomocą hello interfejsu API usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="77b3f-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="77b3f-104">Dowiedz się, jak toouse programu PowerShell skrypt toocreate aplikacji usługi Azure Active Directory (Azure AD) i tooaccess główną usługi Azure Media Services zasobów.</span><span class="sxs-lookup"><span data-stu-id="77b3f-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="77b3f-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77b3f-105">Prerequisites</span></span>

- <span data-ttu-id="77b3f-106">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="77b3f-106">An Azure account.</span></span> <span data-ttu-id="77b3f-107">Jeśli nie masz konta, Rozpocznij od [Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77b3f-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="77b3f-108">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="77b3f-108">A Media Services account.</span></span> <span data-ttu-id="77b3f-109">Aby uzyskać więcej informacji, zobacz [utworzyć konto usługi Azure Media Services w portalu Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="77b3f-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="77b3f-110">Wersja programu PowerShell Azure 0.8.8 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="77b3f-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="77b3f-111">Aby uzyskać więcej informacji, zobacz [jak toouse programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77b3f-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="77b3f-112">Polecenia cmdlet Menedżera zasobów systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="77b3f-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="77b3f-113">Utwórz aplikację usługi Azure AD za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="77b3f-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="77b3f-114">Aby uzyskać więcej informacji zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="77b3f-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="77b3f-115">Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi</span><span class="sxs-lookup"><span data-stu-id="77b3f-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="77b3f-116">Zarządzanie oparte na rolach kontroli dostępu przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77b3f-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="77b3f-117">Jak skonfigurować toomanually demon aplikacji za pomocą certyfikatów</span><span class="sxs-lookup"><span data-stu-id="77b3f-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="77b3f-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77b3f-118">Next steps</span></span>

<span data-ttu-id="77b3f-119">Rozpoczynanie pracy z [przekazywania plików konta tooyour](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="77b3f-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
