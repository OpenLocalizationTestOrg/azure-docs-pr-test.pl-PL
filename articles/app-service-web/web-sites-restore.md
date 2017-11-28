---
title: aaaRestore aplikacji na platformie Azure
description: "Dowiedz się, jak toorestore aplikacji z kopii zapasowej."
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
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="8dbec-103">Przywracanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="8dbec-103">Restore an app in Azure</span></span>
<span data-ttu-id="8dbec-104">W tym artykule opisano sposób toorestore jako aplikacja w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) , która została wcześniej utworzona kopia zapasowa (zobacz [kopii zapasowych aplikacji na platformie Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="8dbec-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="8dbec-105">Przywróć aplikację z poprzedniego stanu na żądanie tooa połączonej bazy danych lub Utwórz nową aplikację na podstawie jednej z aplikacji oryginalnej kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8dbec-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="8dbec-106">Usługa aplikacji Azure obsługuje następujące bazy danych dla kopii zapasowej i przywracania hello:</span><span class="sxs-lookup"><span data-stu-id="8dbec-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="8dbec-107">SQL Database</span><span class="sxs-lookup"><span data-stu-id="8dbec-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="8dbec-108">Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="8dbec-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="8dbec-109">Bazy danych platformy Azure dla PostgreSQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="8dbec-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="8dbec-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="8dbec-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="8dbec-111">MySQL w aplikacji</span><span class="sxs-lookup"><span data-stu-id="8dbec-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="8dbec-112">Przywracanie z kopii zapasowych jest dostępne tooapps uruchomionych w **standardowe** i **Premium** warstwy.</span><span class="sxs-lookup"><span data-stu-id="8dbec-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="8dbec-113">Aby uzyskać informacji na temat skalowania aplikacji w górę, zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="8dbec-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="8dbec-114">**Premium** warstwy umożliwia większej liczbie codzienne toobe kopie zapasowe wykonane niż **standardowe** warstwy.</span><span class="sxs-lookup"><span data-stu-id="8dbec-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="8dbec-115">Przywróć aplikację z istniejącej kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="8dbec-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="8dbec-116">Na powitania **ustawienia** bloku aplikacji w hello portalu Azure kliknij **kopii zapasowych** toodisplay hello **kopii zapasowych** bloku.</span><span class="sxs-lookup"><span data-stu-id="8dbec-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="8dbec-117">Następnie kliknij przycisk **przywrócić**.</span><span class="sxs-lookup"><span data-stu-id="8dbec-117">Then click **Restore**.</span></span>
   
    ![Wybierz polecenie Przywróć teraz][ChooseRestoreNow]
2. <span data-ttu-id="8dbec-119">W hello **przywrócić** bloku, pierwsze hello wybierz źródło kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8dbec-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="8dbec-120">Witaj **kopii zapasowej aplikacji** opcja powoduje wyświetlenie wszystkich hello istniejące kopie zapasowe bieżącej aplikacji hello i można łatwo wybrać.</span><span class="sxs-lookup"><span data-stu-id="8dbec-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="8dbec-121">Witaj **magazynu** opcja umożliwia wybranie dowolnego pliku ZIP kopii zapasowej z wszelkie istniejące konto magazynu Azure i kontener w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8dbec-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="8dbec-122">Jeśli próbujesz toorestore kopii zapasowej innej aplikacji, użyj hello **magazynu** opcji.</span><span class="sxs-lookup"><span data-stu-id="8dbec-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="8dbec-123">Następnie określ lokalizację docelową hello Przywracanie aplikacji hello w **docelową lokalizację przywracania**.</span><span class="sxs-lookup"><span data-stu-id="8dbec-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="8dbec-124">Jeśli wybierzesz **Zastąp**, wszystkie istniejące dane w bieżącej aplikacji jest usunięte i zastąpione.</span><span class="sxs-lookup"><span data-stu-id="8dbec-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="8dbec-125">Przed kliknięciem przycisku **OK**, upewnij się, że jest dokładnie co chcesz toodo.</span><span class="sxs-lookup"><span data-stu-id="8dbec-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="8dbec-126">Możesz wybrać **istniejącej aplikacji** toorestore hello aplikację tooanother kopii zapasowej aplikacji w hello tej samej grupie identyczny.</span><span class="sxs-lookup"><span data-stu-id="8dbec-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="8dbec-127">Przed użyciem tej opcji należy utworzono już inną aplikację w grupie zasobów z dublowania bazy danych konfiguracji toohello, zdefiniowanych w aplikacji hello tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="8dbec-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="8dbec-128">Można również utworzyć **nowy** toorestore aplikacji swoją zawartość.</span><span class="sxs-lookup"><span data-stu-id="8dbec-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="8dbec-129">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8dbec-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="8dbec-130">Pobierz lub usunięcia kopii zapasowej z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="8dbec-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="8dbec-131">Z głównego hello **Przeglądaj** bloku hello portalu Azure, wybierz opcję **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="8dbec-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="8dbec-132">Zostanie wyświetlona lista istniejących kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="8dbec-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="8dbec-133">Wybierz konto magazynu hello, które zawiera kopię zapasową hello, interesujące toodownload lub delete.hello bloku dla konta magazynu hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="8dbec-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="8dbec-134">W bloku konto magazynu hello Wybierz kontener hello, który ma</span><span class="sxs-lookup"><span data-stu-id="8dbec-134">In hello storage account blade, select hello container you want</span></span>
   
    ![Kontenery widoku][ViewContainers]
4. <span data-ttu-id="8dbec-136">Wybierz plik kopii zapasowej toodownload lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="8dbec-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="8dbec-138">Kliknij przycisk **Pobierz** lub **usunąć** w zależności od tego, jakie użytkownik ma toodo.</span><span class="sxs-lookup"><span data-stu-id="8dbec-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="8dbec-139">Monitorowanie operacji przywracania</span><span class="sxs-lookup"><span data-stu-id="8dbec-139">Monitor a restore operation</span></span>
<span data-ttu-id="8dbec-140">Szczegóły toosee hello powodzenie lub Niepowodzenie operacji przywracania aplikacji hello Przejdź toohello **dziennik aktywności** bloku w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8dbec-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="8dbec-141">Przewiń w dół toofind hello potrzeby przywracania działania i kliknij przycisk tooselect go.</span><span class="sxs-lookup"><span data-stu-id="8dbec-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="8dbec-142">Witaj szczegóły blok Wyświetla hello dostępne informacje związane z toohello operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="8dbec-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dbec-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8dbec-143">Next Steps</span></span>
<span data-ttu-id="8dbec-144">Można utworzyć kopii zapasowej i przywracania aplikacji usługi App Service przy użyciu interfejsu API REST (zobacz [tooback REST użycia zapasowych i przywracania usługi aplikacji — aplikacje](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="8dbec-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
