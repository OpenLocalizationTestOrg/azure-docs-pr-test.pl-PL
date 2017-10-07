---
title: "wartości aaaGet do uwierzytelniania aplikacji, usługi Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Tworzenie nazwy głównej usługi do uzyskiwania dostępu do bazy danych SQL z kodu."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: b57dc075ec9e679da9f2f5fa53e02312539cdf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a><span data-ttu-id="4eed0-103">Pobiera wartości hello wymagane do uwierzytelniania tooaccess aplikacji bazy danych SQL z kodu</span><span class="sxs-lookup"><span data-stu-id="4eed0-103">Get hello required values for authenticating an application tooaccess SQL Database from code</span></span>
<span data-ttu-id="4eed0-104">toocreate i zarządzanie bazą danych SQL z kodu, należy zarejestrować aplikację w hello Azure Active Directory (AAD) domeny w ramach subskrypcji hello gdzie zostały utworzone zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4eed0-104">toocreate and manage SQL Database from code you must register your app in hello Azure Active Directory (AAD) domain  in hello subscription where your Azure resources have been created.</span></span>

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a><span data-ttu-id="4eed0-105">Utwórz zasoby tooaccess główna usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="4eed0-105">Create a service principal tooaccess resources from an application</span></span>
<span data-ttu-id="4eed0-106">Najnowsza wersja należy toohave hello [programu Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) zainstalowana i uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="4eed0-106">You need toohave hello latest [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) installed and running.</span></span> <span data-ttu-id="4eed0-107">Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="4eed0-107">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="4eed0-108">Witaj następujący skrypt programu PowerShell tworzy hello aplikacji usługi Active Directory (AD) i usługi hello główna, że potrzebujemy tooauthenticate aplikacji C#.</span><span class="sxs-lookup"><span data-stu-id="4eed0-108">hello following PowerShell script creates hello Active Directory (AD) application and hello service principal that we need tooauthenticate our C# app.</span></span> <span data-ttu-id="4eed0-109">Witaj skrypt generuje wartości, które firma Microsoft wymagane dla hello poprzedzających C# przykładowe.</span><span class="sxs-lookup"><span data-stu-id="4eed0-109">hello script outputs values we need for hello preceding C# sample.</span></span> <span data-ttu-id="4eed0-110">Aby uzyskać szczegółowe informacje, zobacz [toocreate programu Azure PowerShell Użyj nazwy głównej usługi zasobów tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="4eed0-110">For detailed information, see [Use Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a><span data-ttu-id="4eed0-111">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4eed0-111">See also</span></span>
* [<span data-ttu-id="4eed0-112">Tworzenie bazy danych SQL w języku C#</span><span class="sxs-lookup"><span data-stu-id="4eed0-112">Create a SQL database with C#</span></span>](sql-database-get-started-csharp.md)
* [<span data-ttu-id="4eed0-113">Łączenie tooSQL bazy danych przy użyciu usługi Azure uwierzytelnianie usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="4eed0-113">Connecting tooSQL Database By Using Azure Active Directory Authentication</span></span>](sql-database-aad-authentication.md)

