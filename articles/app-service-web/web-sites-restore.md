---
title: Przywracanie aplikacji na platformie Azure
description: "Dowiedz się, jak przywracanie z kopii zapasowej aplikacji."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="05528-103">Przywracanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="05528-103">Restore an app in Azure</span></span>
<span data-ttu-id="05528-104">W tym artykule przedstawiono sposób przywracania aplikacji w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) , która została wcześniej utworzona kopia zapasowa (zobacz [kopii zapasowych aplikacji na platformie Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="05528-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="05528-105">Przywracanie aplikacji za pomocą jego połączonej bazy danych na żądanie do poprzedniego stanu lub Utwórz nową aplikację na podstawie jednej z aplikacji oryginalnej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="05528-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="05528-106">Usługa aplikacji Azure obsługuje następujące bazy danych dla kopii zapasowej i przywracania:</span><span class="sxs-lookup"><span data-stu-id="05528-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="05528-107">SQL Database</span><span class="sxs-lookup"><span data-stu-id="05528-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="05528-108">Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="05528-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="05528-109">Bazy danych platformy Azure dla PostgreSQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="05528-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="05528-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="05528-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="05528-111">MySQL w aplikacji</span><span class="sxs-lookup"><span data-stu-id="05528-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="05528-112">Przywracanie z kopii zapasowych jest dostępne dla aplikacji działających **standardowe** i **Premium** warstwy.</span><span class="sxs-lookup"><span data-stu-id="05528-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="05528-113">Aby uzyskać informacji na temat skalowania aplikacji w górę, zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="05528-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="05528-114">**Premium** warstwy pozwala większa liczba codziennych kopii zapasowych wykonywanych niż **standardowe** warstwy.</span><span class="sxs-lookup"><span data-stu-id="05528-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="05528-115">Przywróć aplikację z istniejącej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="05528-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="05528-116">Na **ustawienia** bloku aplikacji w portalu Azure kliknij **kopii zapasowych** do wyświetlenia **kopii zapasowych** bloku.</span><span class="sxs-lookup"><span data-stu-id="05528-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="05528-117">Następnie kliknij przycisk **przywrócić**.</span><span class="sxs-lookup"><span data-stu-id="05528-117">Then click **Restore**.</span></span>
   
    ![Wybierz polecenie Przywróć teraz][ChooseRestoreNow]
2. <span data-ttu-id="05528-119">W **przywrócić** bloku, najpierw wybierz źródłowy kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="05528-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="05528-120">**Kopii zapasowej aplikacji** opcja powoduje wyświetlenie wszystkich istniejących kopii zapasowych z bieżącej aplikacji i można łatwo wybrać.</span><span class="sxs-lookup"><span data-stu-id="05528-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="05528-121">**Magazynu** opcja umożliwia wybranie dowolnego pliku ZIP kopii zapasowej z wszelkie istniejące konto magazynu Azure i kontener w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="05528-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="05528-122">Jeśli próbujesz przywracania kopii zapasowej innej aplikacji, użyj **magazynu** opcji.</span><span class="sxs-lookup"><span data-stu-id="05528-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="05528-123">Następnie określ miejsce docelowe dla przywracania aplikacji w **docelową lokalizację przywracania**.</span><span class="sxs-lookup"><span data-stu-id="05528-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="05528-124">Jeśli wybierzesz **Zastąp**, wszystkie istniejące dane w bieżącej aplikacji jest usunięte i zastąpione.</span><span class="sxs-lookup"><span data-stu-id="05528-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="05528-125">Przed kliknięciem przycisku **OK**, upewnij się, że jest dokładnie co chcesz zrobić.</span><span class="sxs-lookup"><span data-stu-id="05528-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="05528-126">Możesz wybrać **istniejącej aplikacji** przywracania kopii zapasowej aplikacji do innej aplikacji w tej samej grupie identyczny.</span><span class="sxs-lookup"><span data-stu-id="05528-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="05528-127">Przed użyciem tej opcji należy utworzono już inną aplikację w grupie zasobów z dublowania bazy danych konfiguracji do zdefiniowana w kopii zapasowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="05528-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="05528-128">Można również utworzyć **nowy** aplikacji, aby przywrócić swoją zawartość.</span><span class="sxs-lookup"><span data-stu-id="05528-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="05528-129">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="05528-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="05528-130">Pobierz lub usunięcia kopii zapasowej z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="05528-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="05528-131">W głównym **Przeglądaj** bloku portalu Azure, wybierz opcję **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="05528-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="05528-132">Zostanie wyświetlona lista istniejących kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="05528-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="05528-133">Wybierz konto magazynu, który zawiera kopię zapasową, której chcesz pobrać lub usunąć. Zostanie wyświetlony blok dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="05528-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="05528-134">W bloku konto magazynu Wybierz kontener, który ma</span><span class="sxs-lookup"><span data-stu-id="05528-134">In the storage account blade, select the container you want</span></span>
   
    ![Kontenery widoku][ViewContainers]
4. <span data-ttu-id="05528-136">Wybierz plik kopii zapasowej, który chcesz pobrać lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="05528-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="05528-138">Kliknij przycisk **Pobierz** lub **usunąć** w zależności od tego, co chcesz zrobić.</span><span class="sxs-lookup"><span data-stu-id="05528-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="05528-139">Monitorowanie operacji przywracania</span><span class="sxs-lookup"><span data-stu-id="05528-139">Monitor a restore operation</span></span>
<span data-ttu-id="05528-140">Aby wyświetlić szczegółowe informacje o powodzeniu lub niepowodzeniu operacji przywracania aplikacji, przejdź do **dziennik aktywności** bloku w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="05528-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="05528-141">Przewiń w dół do znajdowania żądaną operację przywracania i zaznacz je.</span><span class="sxs-lookup"><span data-stu-id="05528-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="05528-142">Szczegóły blok Wyświetla dostępne informacje dotyczące operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="05528-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05528-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05528-143">Next Steps</span></span>
<span data-ttu-id="05528-144">Można utworzyć kopii zapasowej i przywracania aplikacji usługi App Service przy użyciu interfejsu API REST (zobacz [REST używany do kopii zapasowej i przywracania usługi aplikacji — aplikacje](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="05528-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
