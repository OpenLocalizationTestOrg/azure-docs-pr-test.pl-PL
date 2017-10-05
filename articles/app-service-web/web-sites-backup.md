---
title: Tworzenie kopii zapasowej aplikacji na platformie Azure
description: "Dowiedz się, jak tworzyć kopie zapasowe aplikacji w usłudze Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 77e983afaaba8e944ab1f337e1c28ced83b63205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="d9377-103">Tworzenie kopii zapasowej aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d9377-103">Back up your app in Azure</span></span>
<span data-ttu-id="d9377-104">Wykonywanie kopii zapasowej i przywracania w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) umożliwia łatwe tworzenie kopii zapasowych aplikacji, ręcznie lub zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="d9377-104">The Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="d9377-105">Zastępowanie istniejących aplikacji lub przywracania do innej aplikacji, można przywrócić aplikację do migawki poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="d9377-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="d9377-106">Aby uzyskać informacje na przywracanie z kopii zapasowej aplikacji, zobacz [Przywracanie aplikacji na platformie Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="d9377-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="d9377-107">Kopiami zapasowymi</span><span class="sxs-lookup"><span data-stu-id="d9377-107">What gets backed up</span></span>
<span data-ttu-id="d9377-108">Usługi aplikacji może wykonywać kopie zapasowe następujące informacje, aby konto magazynu Azure i kontener, który skonfigurowano do używania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9377-108">App Service can backup the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="d9377-109">Konfiguracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9377-109">App configuration</span></span>
* <span data-ttu-id="d9377-110">Zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="d9377-110">File content</span></span>
* <span data-ttu-id="d9377-111">Bazy danych jest podłączony do aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9377-111">Database connected to your app</span></span>

<span data-ttu-id="d9377-112">Obsługiwane są następujące rozwiązania bazy danych przy użyciu funkcji tworzenia kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="d9377-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="d9377-113">SQL Database</span><span class="sxs-lookup"><span data-stu-id="d9377-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="d9377-114">Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d9377-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="d9377-115">Bazy danych platformy Azure dla PostgreSQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d9377-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="d9377-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="d9377-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="d9377-117">MySQL w aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9377-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="d9377-118">Każda kopia zapasowa jest w trybie offline pełną kopię aplikacji, nie aktualizację przyrostową.</span><span class="sxs-lookup"><span data-stu-id="d9377-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="d9377-119">Wymagania i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d9377-119">Requirements and restrictions</span></span>
* <span data-ttu-id="d9377-120">Wykonywanie kopii zapasowych i przywracania funkcja wymaga planu usługi aplikacji w **standardowe** warstwy lub **Premium** warstwy.</span><span class="sxs-lookup"><span data-stu-id="d9377-120">The Back up and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="d9377-121">Aby uzyskać więcej informacji na temat skalowania swój plan usługi aplikacji, aby użyć wyższego poziomu, zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d9377-121">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="d9377-122">**Premium** warstwy umożliwia większej liczbie codziennie kopii ups niż **standardowe** warstwy.</span><span class="sxs-lookup"><span data-stu-id="d9377-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="d9377-123">Wymagane konto magazynu Azure i kontener w tej samej subskrypcji co aplikację, którą chcesz utworzyć kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="d9377-123">You need an Azure storage account and container in the same subscription as the app that you want to backup.</span></span> <span data-ttu-id="d9377-124">Aby uzyskać więcej informacji o kontach magazynu Azure, zobacz [łącza](#moreaboutstorage) na końcu tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="d9377-124">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="d9377-125">Kopie zapasowe mogą być zawartości aplikacji i bazy danych do 10 GB.</span><span class="sxs-lookup"><span data-stu-id="d9377-125">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="d9377-126">Jeśli rozmiar kopii zapasowej przekracza ten limit, wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="d9377-126">If the backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="d9377-127">Ręczne tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="d9377-127">Create a manual backup</span></span>
1. <span data-ttu-id="d9377-128">W [Azure Portal](https://portal.azure.com), przejdź do bloku aplikacji, wybierz **kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="d9377-128">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Backups**.</span></span> <span data-ttu-id="d9377-129">**Kopii zapasowych** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="d9377-129">The **Backups** blade will be displayed.</span></span>
   
    ![Strona kopii zapasowych][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="d9377-131">Jeśli zostanie wyświetlony następujący komunikat, kliknij go, aby uaktualnić swój plan usługi aplikacji, aby móc kontynuować wykonywanie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="d9377-131">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="d9377-132">Zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d9377-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="d9377-133">![Wybierz konto magazynu](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="d9377-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="d9377-134">W **kopii zapasowej** bloku, kliknij przycisk **Konfiguruj**
![kliknij przycisk Konfiguruj.](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="d9377-134">In the **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="d9377-135">W **konfiguracji kopii zapasowej** bloku, kliknij przycisk **magazynu: nieskonfigurowane** konfigurowania konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d9377-135">In the **Backup Configuration** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Wybierz konto magazynu][ChooseStorageAccount]
4. <span data-ttu-id="d9377-137">Wybierz miejsce docelowe kopii zapasowej, wybierając **konta magazynu** i **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="d9377-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="d9377-138">Konto magazynu muszą należeć do tej samej subskrypcji co aplikacja, którą chcesz utworzyć kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="d9377-138">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="d9377-139">Jeśli chcesz, można utworzyć nowe konto magazynu lub nowy kontener w odpowiednich bloków.</span><span class="sxs-lookup"><span data-stu-id="d9377-139">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="d9377-140">Gdy wszystko będzie gotowe, kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="d9377-140">When you're done, click **Select**.</span></span>
   
    ![Wybierz konto magazynu](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="d9377-142">W **konfiguracji kopii zapasowej** bloku, który nadal pozostanie otwarty, możesz skonfigurować **instrukcji Backup Database**, następnie wybierz bazy danych mają być uwzględnione w kopii zapasowych (baza danych SQL lub MySQL), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9377-142">In the **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Wybierz konto magazynu](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="d9377-144">Aby baza danych ma na liście, parametrach połączenia musi istnieć w **parametry połączenia** sekcji **ustawienia aplikacji** bloku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9377-144">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="d9377-145">W **konfiguracji kopii zapasowej** bloku, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d9377-145">In the **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="d9377-146">W **kopii zapasowych** bloku, kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="d9377-146">In the  **Backups** blade, click **Backup**.</span></span>
   
    ![Przycisk BackUpNow][BackUpNow]
   
    <span data-ttu-id="d9377-148">Zostanie wyświetlony komunikat z postępu podczas procesu tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="d9377-148">You see a progress message during the backup process.</span></span>

<span data-ttu-id="d9377-149">Po skonfigurowaniu konta magazynu i kontener w dowolnym momencie można zainicjować ręcznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="d9377-149">Once the storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="d9377-150">Skonfiguruj automatyczne kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="d9377-150">Configure automated backups</span></span>
1. <span data-ttu-id="d9377-151">W **konfiguracji kopii zapasowej** ustawić bloku **zaplanowanej kopii zapasowej** do **na**.</span><span class="sxs-lookup"><span data-stu-id="d9377-151">In the **Backup Configuration** blade, set **Scheduled backup** to **On**.</span></span> 
   
    ![Wybierz konto magazynu](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="d9377-153">Ustaw harmonogram tworzenia kopii zapasowych zostaną wyświetlone opcje, **zaplanowanych kopii zapasowych** do **na**następnie skonfiguruj harmonogram tworzenia kopii zapasowych zgodnie z potrzebami i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9377-153">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Włącz automatyczne kopie zapasowe][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="d9377-155">Skonfiguruj częściowych kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="d9377-155">Configure Partial Backups</span></span>
<span data-ttu-id="d9377-156">Czasami nie chcesz kopii zapasowej wszystko w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9377-156">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="d9377-157">Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="d9377-157">Here are a few examples:</span></span>

* <span data-ttu-id="d9377-158">Możesz [Konfigurowanie cotygodniowe kopie zapasowe](web-sites-backup.md#configure-automated-backups) aplikacji zawierający zawartości statycznej, który nigdy nie zmienia, takich jak stare wpisy na blogu lub obrazów.</span><span class="sxs-lookup"><span data-stu-id="d9377-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="d9377-159">Aplikacja ma ponad 10 GB zawartości (wartość maksymalna, którą można tworzyć kopie zapasowe w czasie).</span><span class="sxs-lookup"><span data-stu-id="d9377-159">Your app has over 10 GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="d9377-160">Nie chcesz utworzyć kopię zapasową plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="d9377-160">You don't want to backup the log files.</span></span>

<span data-ttu-id="d9377-161">Umożliwia częściowych kopii zapasowych, możesz wybrać dokładnie plików, których można chcesz utworzyć kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="d9377-161">Partial backups allows you choose exactly which files you want to backup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="d9377-162">Wyklucz pliki z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="d9377-162">Exclude files from your backup</span></span>
<span data-ttu-id="d9377-163">Załóżmy, że masz aplikację, która zawiera pliki dziennika i obrazów statycznych, które zostały kopii zapasowej raz i nie będzie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="d9377-163">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="d9377-164">W takim przypadku można wykluczyć tych plików i folderów z są przechowywane w kopii zapasowych w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="d9377-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="d9377-165">Aby wykluczyć pliki i foldery z kopii zapasowych, należy utworzyć `_backup.filter` w pliku `D:\home\site\wwwroot` folderu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9377-165">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="d9377-166">Określ listę plików i folderów, które chcesz wykluczyć w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="d9377-166">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="d9377-167">Jest łatwy sposób uzyskać dostęp do plików do użycia Kudu.</span><span class="sxs-lookup"><span data-stu-id="d9377-167">An easy way to access your files is to use Kudu .</span></span> <span data-ttu-id="d9377-168">Kliknij przycisk **zaawansowane narzędzia -> Przejdź** ustawienie Kudu dostępu do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d9377-168">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![Program kudu przy użyciu portalu][kudu-portal]

<span data-ttu-id="d9377-170">Określ foldery, które chcesz wykluczyć z kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="d9377-170">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="d9377-171">Na przykład chcesz filtrować wyróżnione folderów i plików.</span><span class="sxs-lookup"><span data-stu-id="d9377-171">For example , you want to filter out the highlighted folder and files.</span></span>

![Folderu Obrazy][ImagesFolder]

<span data-ttu-id="d9377-173">Utwórz plik o nazwie `_backup.filter` na liście powyżej należy umieścić w pliku, ale usunięcie `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="d9377-173">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="d9377-174">Lista jednego katalogu lub pliku w jednym wierszu.</span><span class="sxs-lookup"><span data-stu-id="d9377-174">List one directory or file per line.</span></span> <span data-ttu-id="d9377-175">Aby zawartość pliku powinna być:</span><span class="sxs-lookup"><span data-stu-id="d9377-175">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="d9377-176">Przekaż `_backup.filter` pliku `D:\home\site\wwwroot\` katalog swoją witrynę przy użyciu [ftp](web-sites-deploy.md#ftp) lub innej metody.</span><span class="sxs-lookup"><span data-stu-id="d9377-176">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="d9377-177">Jeśli chcesz, można utworzyć pliku bezpośrednio za pomocą Kudu `DebugConsole` i Wstaw zawartość istnieje.</span><span class="sxs-lookup"><span data-stu-id="d9377-177">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="d9377-178">Uruchamianie tworzenia kopii zapasowych w taki sam sposób, w zwykły sposób, jak [ręcznie](#create-a-manual-backup) lub [automatycznie](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="d9377-178">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="d9377-179">Teraz, wszystkie pliki i foldery, które są określone w `_backup.filter` został wykluczony z kolejnych kopii zapasowych według harmonogramu lub ręcznie zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="d9377-179">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="d9377-180">Przywróć częściowych kopii zapasowych lokacji tak samo jak [przywrócić zwykłej kopii zapasowej](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="d9377-180">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="d9377-181">Proces przywracania nie co.</span><span class="sxs-lookup"><span data-stu-id="d9377-181">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="d9377-182">Po przywróceniu pełnej kopii zapasowej, cała zawartość w witrynie zastępuje się ze względu na w kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="d9377-182">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="d9377-183">Jeśli plik jest w lokacji, ale nie w kopii zapasowej zostaje usunięta.</span><span class="sxs-lookup"><span data-stu-id="d9377-183">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="d9377-184">Jednak po przywróceniu częściowej kopii zapasowej, pozostanie zawartość, która znajduje się w jednym z katalogów zabronione lub dowolnego pliku zabronione, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="d9377-184">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="d9377-185">Jak są przechowywane kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="d9377-185">How backups are stored</span></span>
<span data-ttu-id="d9377-186">Po wybraniu jednego lub więcej kopii zapasowych dla aplikacji, kopie zapasowe są widoczne na **kontenery** blok konta magazynu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9377-186">After you have made one or more backups for your app, the backups are visible on the **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="d9377-187">Na koncie magazynu każdej kopii zapasowej składa się z`.zip` plik zawierający dane kopii zapasowej i `.xml` pliku, który zawiera manifest z `.zip` pliku zawartości.</span><span class="sxs-lookup"><span data-stu-id="d9377-187">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="d9377-188">Można rozpakować i przeglądanie tych plików, aby uzyskać dostęp do kopii zapasowych bez rzeczywistego wykonania przywracania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9377-188">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="d9377-189">Kopia zapasowa bazy danych dla aplikacji są przechowywane w katalogu głównym pliku the.zip.</span><span class="sxs-lookup"><span data-stu-id="d9377-189">The database backup for the app is stored in the root of the.zip file.</span></span> <span data-ttu-id="d9377-190">Bazy danych SQL jest plikiem pliku BACPAC (bez rozszerzenia pliku) i można je zaimportować.</span><span class="sxs-lookup"><span data-stu-id="d9377-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="d9377-191">Aby utworzyć oparte na eksportowanie pliku BACPAC bazy danych SQL, zobacz [Importowanie pliku pliku BACPAC, aby utworzyć nową bazę danych użytkownika](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9377-191">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="d9377-192">Zmienianie plików w sieci **websitebackups** kontener może spowodować stała się nieprawidłowa i w związku z tym nie-umożliwiająca przywrócenie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="d9377-192">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="d9377-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9377-193">Next Steps</span></span>
<span data-ttu-id="d9377-194">Aby uzyskać informacje na przywracanie z kopii zapasowej aplikacji, zobacz [Przywracanie aplikacji na platformie Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="d9377-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="d9377-195">Można również utworzyć kopii zapasowej i przywracanie aplikacji usługi App Service przy użyciu interfejsu API REST (zobacz [REST użyj kopii zapasowej i przywracania usługi aplikacji — aplikacje](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="d9377-195">You can also backup and restore App Service apps using REST API (see [Use REST to backup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

