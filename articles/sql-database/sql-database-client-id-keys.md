---
title: "Pobiera wartości do uwierzytelniania aplikacji, usługi Azure SQL Database | Dokumentacja firmy Microsoft"
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
ms.workload: Inactive
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: e76144bcb65da992c6d723d7333b4db8aa1ca488
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/31/2017
---
# <a name="get-the-required-values-for-authenticating-an-application-to-access-sql-database-from-code"></a>Pobiera wartości wymagane do uwierzytelniania aplikacji dostęp do bazy danych SQL z kodu
Tworzenie i zarządzanie nimi bazy danych SQL z kodu, należy zarejestrować aplikację w domenie usługi Azure Active Directory (AAD) w subskrypcji, gdzie zostały utworzone zasobów platformy Azure.

## <a name="create-a-service-principal-to-access-resources-from-an-application"></a>Tworzenie nazwy głównej usługi dostępu do zasobów z aplikacji
Musisz mieć najnowszej [programu Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) zainstalowana i uruchomiona. Aby uzyskać szczegółowe informacje, zobacz artykuł [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (Instalowanie i konfigurowanie programu Azure PowerShell).

Poniższy skrypt środowiska PowerShell tworzy aplikację usługi Active Directory (AD) oraz jednostkę usługi wymaganą do uwierzytelnienia aplikacji w języku C#. Skrypt generuje wartości wyjściowe potrzebne w poprzednim przykładzie w języku C#. Aby uzyskać szczegółowe informacje, zobacz [Tworzenie usługi podmiotu używanej do uzyskiwania dostępu do zasobów przy użyciu programu Azure PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret




## <a name="see-also"></a>Zobacz też
* [Tworzenie bazy danych SQL w języku C#](sql-database-get-started-csharp.md)
* [Łączenie z bazą danych SQL przy użyciu uwierzytelniania usługi Azure Active Directory](sql-database-aad-authentication.md)

