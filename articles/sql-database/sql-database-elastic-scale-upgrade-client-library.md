---
title: Uaktualnij do najnowszej biblioteki klienta elastycznej bazy danych | Dokumentacja firmy Microsoft
description: "Uaktualnianie aplikacji i bibliotek przy użyciu narzędzia Nuget"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: 7e28d128645e856c0efa6e4f78d8f9f36982a76c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-an-app-to-use-the-latest-elastic-database-client-library"></a><span data-ttu-id="6b8ba-103">Uaktualnij aplikację do korzystania z najnowszych biblioteki klienta elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="6b8ba-103">Upgrade an app to use the latest elastic database client library</span></span>
<span data-ttu-id="6b8ba-104">Nowe wersje [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md) są dostępne za pośrednictwem NuGetand interfejsu Menedżera NuGetPackage w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-104">New versions of the [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand the NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="6b8ba-105">Uaktualnień obsługę nowych funkcji biblioteki klienta oraz zawierać poprawki błędów.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-105">Upgrades contain bug fixes and support for new capabilities of the client library.</span></span>

<span data-ttu-id="6b8ba-106">**Aby uzyskać najnowszą wersję:** przejdź do [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="6b8ba-106">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="6b8ba-107">Odbuduj aplikacji przy użyciu nowej biblioteki, a także zmienić istniejące metadanych Menedżera Map niezależnego fragmentu przechowywane w bazach danych SQL Azure do obsługi nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-107">Rebuild your application with the new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases to support new features.</span></span>

<span data-ttu-id="6b8ba-108">Te kroki są wykonywane w kolejności gwarantuje, że starsze wersje biblioteki klienta nie są już dostępne w danym środowisku po zaktualizowaniu obiektów metadanych, co oznacza, że po uaktualnieniu nie można utworzyć obiektów stara wersja metadanych.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-108">Performing these steps in order ensures that old versions of the client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="6b8ba-109">Kroki uaktualniania</span><span class="sxs-lookup"><span data-stu-id="6b8ba-109">Upgrade steps</span></span>
<span data-ttu-id="6b8ba-110">**1. Uaktualnienie aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="6b8ba-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="6b8ba-111">W programie Visual Studio Pobierz i odwołać się do wszystkich projektów programowanie korzystające z biblioteki; najnowszą wersję klienta w bibliotece następnie ponownie skompilować i wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-111">In Visual Studio, download and reference the latest client library version into all of your development projects that use the library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="6b8ba-112">W rozwiązaniu programu Visual Studio wybierz **narzędzia** --> **Menedżera pakietów NuGet** -->  **Zarządzaj pakietami NuGet dla rozwiązania**.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="6b8ba-113">(Visual Studio 2013) W lewym panelu, wybierz **aktualizacje**, a następnie wybierz **aktualizacji** przycisk pakietu **SQL bazy danych elastyczne skalowanie biblioteki klienta usługi Azure** wyświetlany w oknie.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-113">(Visual Studio 2013) In the left panel, select **Updates**, and then select the **Update** button on the package **Azure SQL Database Elastic Scale Client Library** that appears in the window.</span></span>
* <span data-ttu-id="6b8ba-114">(Visual Studio 2015) Wartość w polu filtru **uaktualnienia dostępne**.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-114">(Visual Studio 2015) Set the Filter box to **Upgrade available**.</span></span> <span data-ttu-id="6b8ba-115">Wybierz pakiet aktualizacji, a następnie kliknij przycisk **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-115">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="6b8ba-116">(Visual Studio 2017) W górnej części okna dialogowego, wybierz **aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-116">(Visual Studio 2017) At the top of the dialog, select **Updates**.</span></span> <span data-ttu-id="6b8ba-117">Wybierz pakiet aktualizacji, a następnie kliknij przycisk **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-117">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="6b8ba-118">Tworzenie i wdrażanie.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-118">Build and Deploy.</span></span> 

<span data-ttu-id="6b8ba-119">**2. Uaktualnij skryptów.**</span><span class="sxs-lookup"><span data-stu-id="6b8ba-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="6b8ba-120">Jeśli używasz **PowerShell** skryptów służących do zarządzania odłamków, [pobrać nową wersję biblioteki](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) i skopiować go do katalogu, z którego wykonywanie skryptów.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-120">If you are using **PowerShell** scripts to manage shards, [download the new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into the directory from which you execute scripts.</span></span> 

<span data-ttu-id="6b8ba-121">**3. Uaktualnij usługę podziału scalania.**</span><span class="sxs-lookup"><span data-stu-id="6b8ba-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="6b8ba-122">Jeśli za pomocą narzędzia scalania podziału elastycznej bazy danych można zreorganizować danych podzielonej [pobrać i zainstalować najnowszą wersję narzędzia](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span><span class="sxs-lookup"><span data-stu-id="6b8ba-122">If you use the elastic database split-merge tool to reorganize sharded data, [download and deploy the latest version of the tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="6b8ba-123">Szczegółowe kroki uaktualniania można znaleźć usługi [tutaj](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="6b8ba-123">Detailed upgrade steps for the Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="6b8ba-124">**4. Uaktualnienie bazy danych Menedżera Map niezależnego fragmentu**.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="6b8ba-125">Uaktualnij metadanych Obsługa map niezależnego fragmentu w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-125">Upgrade the metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="6b8ba-126">Istnieją dwa sposoby, można to zrobić, za pomocą programu PowerShell lub C#.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="6b8ba-127">Poniżej przedstawiono obie opcje.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-127">Both options are shown below.</span></span>

<span data-ttu-id="6b8ba-128">***Opcja 1: Metadane aktualizacji przy użyciu programu PowerShell***</span><span class="sxs-lookup"><span data-stu-id="6b8ba-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="6b8ba-129">Pobierz najnowsze narzędzia wiersza polecenia programu NuGet z [tutaj](http://nuget.org/nuget.exe) i zapisać w folderze.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-129">Download the latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save to a folder.</span></span> 
2. <span data-ttu-id="6b8ba-130">Otwórz wiersz polecenia, przejdź do folderu i wydać polecenie:`nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="6b8ba-130">Open a Command Prompt, navigate to the same folder, and issue the command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="6b8ba-131">Przejdź do podfolderu zawierający nową wersję klienta biblioteki DLL, po prostu pobrany, na przykład:`cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="6b8ba-131">Navigate to the subfolder containing the new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="6b8ba-132">Pobierz skryptlet uaktualnienia klienta elastycznej bazy danych z [Centrum skryptów](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9)i zapisz go do folderu zawierającego plik DLL.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-132">Download the elastic database client upgrade scriptlet from the [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into the same folder containing the DLL.</span></span>
5. <span data-ttu-id="6b8ba-133">Z tego folderu Uruchom ".\upgrade.ps1 programu PowerShell" w wierszu polecenia, a następnie postępuj zgodnie z monitami.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-133">From that folder, run “PowerShell .\upgrade.ps1” from the command prompt and follow the prompts.</span></span>

<span data-ttu-id="6b8ba-134">***Opcja 2: Uaktualnienie metadanych za pomocą języka C#***</span><span class="sxs-lookup"><span data-stu-id="6b8ba-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="6b8ba-135">Można również utworzyć aplikację programu Visual Studio, która otwiera ShardMapManager Twojego, przechodzi przez wszystkie odłamków i przeprowadza uaktualnienie metadanych przez wywołanie metody [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) i [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6b8ba-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs the metadata upgrade by calling the methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="6b8ba-136">Techniki metadane uaktualnienia można zastosować wiele razy bez problemów.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="6b8ba-137">Na przykład jeśli starsza wersja klienta tworzy przypadkowo niezależnych po zaktualizowaniu już, można uruchomić uaktualnienia ponownie we wszystkich fragmentów, aby upewnić się, że znajduje się w całej infrastrukturze najnowsze wersja metadanych.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards to ensure that the latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="6b8ba-138">**Uwaga:** nowych wersji biblioteki klienta opublikowana do daty nadal działać we wcześniejszych wersjach metadanych Menedżera Map niezależnego fragmentu bazy danych SQL Azure i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-138">**Note:**  New versions of the client library published to-date continue to work with prior versions of the Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="6b8ba-139">Jednak aby skorzystać z niektórych nowych funkcji w najnowszego klienta, metadane musi zostać uaktualniony.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-139">However to take advantage of some of the new features in the latest client, metadata needs to be upgraded.</span></span>   <span data-ttu-id="6b8ba-140">Należy pamiętać, że metadane uaktualnienia nie wpłynie na wszystkie dane użytkownika lub dane specyficzne dla aplikacji, tylko obiekty tworzone i używane przez Menedżera Map niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by the Shard Map Manager.</span></span>  <span data-ttu-id="6b8ba-141">I aplikacje w dalszym ciągu działać przez sekwencji uaktualniania opisany powyżej.</span><span class="sxs-lookup"><span data-stu-id="6b8ba-141">And applications continue to operate through the upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="6b8ba-142">Historia wersji klienta elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="6b8ba-142">Elastic database client version history</span></span>
<span data-ttu-id="6b8ba-143">Historia wersji, aby uzyskać [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="6b8ba-143">For version history, go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

