---
title: "Skrypt programu PowerShell Azure przykładowe — łączenie aplikacji sieci web z bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — łączenie aplikacji sieci web z bazy danych SQL"
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
ms.openlocfilehash: 5312bf6b81d1cc48490b71c3f77323cca23e1559
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="7c4e4-103">Łączenie aplikacji sieci web z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="7c4e4-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="7c4e4-104">W tym scenariuszu dowiesz się, jak utworzyć bazę danych Azure SQL i aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="7c4e4-105">Następnie zostaną połączone z bazą danych SQL do aplikacji sieci web, przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="7c4e4-106">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="7c4e4-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="7c4e4-107">Sample script</span></span>

<span data-ttu-id="7c4e4-108">[!code-powershell[główne](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "łączenie aplikacji sieci web z bazy danych SQL")]</span><span class="sxs-lookup"><span data-stu-id="7c4e4-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7c4e4-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="7c4e4-109">Clean up deployment</span></span> 

<span data-ttu-id="7c4e4-110">Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="7c4e4-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="7c4e4-111">Script explanation</span></span>

<span data-ttu-id="7c4e4-112">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-112">This script uses the following commands.</span></span> <span data-ttu-id="7c4e4-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7c4e4-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="7c4e4-114">Command</span></span> | <span data-ttu-id="7c4e4-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7c4e4-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c4e4-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c4e4-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7c4e4-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7c4e4-118">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="7c4e4-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="7c4e4-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="7c4e4-120">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7c4e4-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="7c4e4-121">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-121">Creates a web app.</span></span> |
| [<span data-ttu-id="7c4e4-122">Nowe AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="7c4e4-122">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="7c4e4-123">Tworzy serwer bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-123">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="7c4e4-124">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="7c4e4-124">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="7c4e4-125">Powoduje utworzenie reguły zapory dla serwera bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-125">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="7c4e4-126">Nowe AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="7c4e4-126">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="7c4e4-127">Tworzy bazę danych lub elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-127">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="7c4e4-128">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="7c4e4-128">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="7c4e4-129">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="7c4e4-129">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c4e4-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c4e4-130">Next steps</span></span>

<span data-ttu-id="7c4e4-131">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c4e4-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7c4e4-132">Dodatkowe przykłady programu Powershell systemu Azure dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c4e4-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
