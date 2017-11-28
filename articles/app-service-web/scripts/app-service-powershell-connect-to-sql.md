---
title: "Przykładowy skrypt programu PowerShell - aaaAzure połączenia bazy danych SQL tooa aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Połącz z bazą danych SQL tooa aplikacji sieci web"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8f80b940378d020cbcaec2c1bbc28bae1a3ef35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="8e481-103">Połącz z bazą danych SQL tooa aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="8e481-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="8e481-104">W tym scenariuszu dowiesz się, jak toocreate bazy danych Azure SQL i usługi Azure web app.</span><span class="sxs-lookup"><span data-stu-id="8e481-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="8e481-105">Następnie zostanie Połącz hello SQL bazy danych toohello web app przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8e481-105">Then you will link hello SQL database toohello web app using app settings.</span></span>

<span data-ttu-id="8e481-106">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="8e481-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="8e481-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="8e481-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app tooa SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8e481-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="8e481-108">Clean up deployment</span></span> 

<span data-ttu-id="8e481-109">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="8e481-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="8e481-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="8e481-110">Script explanation</span></span>

<span data-ttu-id="8e481-111">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="8e481-111">This script uses hello following commands.</span></span> <span data-ttu-id="8e481-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="8e481-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8e481-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="8e481-113">Command</span></span> | <span data-ttu-id="8e481-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="8e481-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8e481-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8e481-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8e481-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="8e481-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8e481-117">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="8e481-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="8e481-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="8e481-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="8e481-119">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8e481-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="8e481-120">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e481-120">Creates a web app.</span></span> |
| [<span data-ttu-id="8e481-121">Nowe AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="8e481-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8e481-122">Tworzy serwer bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="8e481-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="8e481-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="8e481-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="8e481-124">Powoduje utworzenie reguły zapory dla serwera bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="8e481-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="8e481-125">Nowe AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="8e481-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="8e481-126">Tworzy bazę danych lub elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8e481-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="8e481-127">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="8e481-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="8e481-128">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8e481-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8e481-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e481-129">Next steps</span></span>

<span data-ttu-id="8e481-130">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e481-130">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8e481-131">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8e481-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
