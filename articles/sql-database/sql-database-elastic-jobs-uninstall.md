---
title: "Narzędzie zadania elastycznej bazy danych toouninstall aaaHow"
description: "Jak toouninstall hello narzędzia zadania elastycznej bazy danych"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="8dd9d-103">Odinstaluj składniki zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="8dd9d-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="8dd9d-104">**Zadania elastyczne bazy danych** składniki można odinstalować za pomocą portalu hello lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8dd9d-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="8dd9d-105">Odinstaluj składniki zadania elastycznej bazy danych przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8dd9d-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="8dd9d-106">Otwórz hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8dd9d-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8dd9d-107">Przejdź toohello subskrypcji, która zawiera **zadania elastycznej bazy danych** składniki, to znaczy hello subskrypcji, w których elastycznej bazy danych zostały zainstalowane składniki zadania.</span><span class="sxs-lookup"><span data-stu-id="8dd9d-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="8dd9d-108">Kliknij przycisk **Przeglądaj** i kliknij przycisk **grup zasobów**.</span><span class="sxs-lookup"><span data-stu-id="8dd9d-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="8dd9d-109">Witaj wybierz grupę zasobów o nazwie "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="8dd9d-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="8dd9d-110">Usuń grupę zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="8dd9d-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="8dd9d-111">Odinstaluj składniki zadania elastycznej bazy danych przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="8dd9d-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="8dd9d-112">Uruchom okno poleceń programu PowerShell usługi Microsoft Azure i przejdź toohello narzędzia podkatalogu w folderze Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x hello: typ **narzędzia cd**.</span><span class="sxs-lookup"><span data-stu-id="8dd9d-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="8dd9d-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > Narzędzia dysku cd</span><span class="sxs-lookup"><span data-stu-id="8dd9d-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="8dd9d-114">Uruchom skrypt programu PowerShell.\UninstallElasticDatabaseJobs.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="8dd9d-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="8dd9d-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > C:.\UninstallElasticDatabaseJobs.ps1 PS odblokowanie pliku\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >. \ UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="8dd9d-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="8dd9d-116">Lub po prostu wykonać hello następującego skryptu, przy założeniu, domyślne wartości w przypadku na instalację składników hello:</span><span class="sxs-lookup"><span data-stu-id="8dd9d-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="8dd9d-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8dd9d-117">Next steps</span></span>
<span data-ttu-id="8dd9d-118">Zainstaluj toore zadania elastycznej bazy danych, zobacz [instalowania usługi zadania elastycznej bazy danych hello](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="8dd9d-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="8dd9d-119">Omówienie zadania elastycznej bazy danych, zobacz [omówienie zadania elastycznej bazy danych](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8dd9d-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


