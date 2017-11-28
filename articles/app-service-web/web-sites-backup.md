---
title: aaaBack zapasowej swojej aplikacji na platformie Azure
description: "Dowiedz się, jak toocreate kopie zapasowe aplikacji w usłudze Azure App Service."
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
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="96deb-103">Tworzenie kopii zapasowej aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="96deb-103">Back up your app in Azure</span></span>
<span data-ttu-id="96deb-104">Witaj kopii zapasowych i przywracania funkcji w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) umożliwia łatwe tworzenie kopii zapasowych aplikacji, ręcznie lub zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="96deb-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="96deb-105">Przywracanie aplikacji tooanother lub zastępowania istniejącej aplikacji hello, można przywrócić migawki tooa aplikacji hello poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="96deb-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="96deb-106">Aby uzyskać informacje na przywracanie z kopii zapasowej aplikacji, zobacz [Przywracanie aplikacji na platformie Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="96deb-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="96deb-107">Kopiami zapasowymi</span><span class="sxs-lookup"><span data-stu-id="96deb-107">What gets backed up</span></span>
<span data-ttu-id="96deb-108">Usługi aplikacji może wykonywać kopie zapasowe następujących hello informacji tooan konta magazynu Azure i kontener skonfigurowano toouse Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96deb-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="96deb-109">Konfiguracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="96deb-109">App configuration</span></span>
* <span data-ttu-id="96deb-110">Zawartość pliku</span><span class="sxs-lookup"><span data-stu-id="96deb-110">File content</span></span>
* <span data-ttu-id="96deb-111">Aplikacja tooyour połączenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="96deb-111">Database connected tooyour app</span></span>

<span data-ttu-id="96deb-112">Witaj następujące rozwiązania bazy danych są obsługiwane przy użyciu funkcji tworzenia kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="96deb-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="96deb-113">SQL Database</span><span class="sxs-lookup"><span data-stu-id="96deb-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="96deb-114">Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="96deb-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="96deb-115">Bazy danych platformy Azure dla PostgreSQL (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="96deb-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="96deb-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="96deb-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="96deb-117">MySQL w aplikacji</span><span class="sxs-lookup"><span data-stu-id="96deb-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="96deb-118">Każda kopia zapasowa jest w trybie offline pełną kopię aplikacji, nie aktualizację przyrostową.</span><span class="sxs-lookup"><span data-stu-id="96deb-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="96deb-119">Wymagania i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="96deb-119">Requirements and restrictions</span></span>
* <span data-ttu-id="96deb-120">Witaj kopii zapasowych i funkcja przywracania wymaga hello toobe planu usługi aplikacji w hello **standardowe** warstwy lub **Premium** warstwy.</span><span class="sxs-lookup"><span data-stu-id="96deb-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="96deb-121">Aby uzyskać więcej informacji na temat skalowania Twojej toouse planu usługi aplikacji wyższego poziomu, zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="96deb-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="96deb-122">**Premium** warstwy umożliwia większej liczbie codziennie kopii ups niż **standardowe** warstwy.</span><span class="sxs-lookup"><span data-stu-id="96deb-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="96deb-123">Wymagane konto magazynu Azure i kontener w hello tej samej subskrypcji co aplikacja hello, które mają toobackup.</span><span class="sxs-lookup"><span data-stu-id="96deb-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="96deb-124">Aby uzyskać więcej informacji na kontach magazynu Azure, zobacz hello [łącza](#moreaboutstorage) na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="96deb-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="96deb-125">Kopie zapasowe mogą być zapasowej GB too10 zawartości aplikacji i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="96deb-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="96deb-126">Jeśli rozmiar kopii zapasowej hello przekracza ten limit, wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="96deb-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="96deb-127">Ręczne tworzenie kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="96deb-127">Create a manual backup</span></span>
1. <span data-ttu-id="96deb-128">W hello [Azure Portal](https://portal.azure.com), przejdź do bloku tooyour aplikacji, wybierz **kopii zapasowych**.</span><span class="sxs-lookup"><span data-stu-id="96deb-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="96deb-129">Witaj **kopii zapasowych** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="96deb-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Strona kopii zapasowych][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="96deb-131">Jeśli widzisz wiadomość hello poniżej, kliknij go, tooupgrade planu usługi aplikacji przed kontynuowaniem z kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="96deb-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="96deb-132">Zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="96deb-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="96deb-133">![Wybierz konto magazynu](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="96deb-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="96deb-134">W hello **kopii zapasowej** bloku, kliknij przycisk **Konfiguruj**
![kliknij przycisk Konfiguruj.](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="96deb-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="96deb-135">W hello **konfiguracji kopii zapasowej** bloku, kliknij przycisk **magazynu: nieskonfigurowane** tooconfigure konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="96deb-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Wybierz konto magazynu][ChooseStorageAccount]
4. <span data-ttu-id="96deb-137">Wybierz miejsce docelowe kopii zapasowej, wybierając **konta magazynu** i **kontenera**.</span><span class="sxs-lookup"><span data-stu-id="96deb-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="96deb-138">Konto magazynu Hello muszą należeć toohello tej samej subskrypcji co chcesz tooback zapasowe aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="96deb-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="96deb-139">Jeśli chcesz, można utworzyć nowe konto magazynu lub nowy kontener w blokach odpowiednich hello.</span><span class="sxs-lookup"><span data-stu-id="96deb-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="96deb-140">Gdy wszystko będzie gotowe, kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="96deb-140">When you're done, click **Select**.</span></span>
   
    ![Wybierz konto magazynu](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="96deb-142">W hello **konfiguracji kopii zapasowej** bloku, który nadal pozostanie otwarty, możesz skonfigurować **instrukcji Backup Database**, następnie wybierz hello baz danych, tooinclude w hello tworzenia kopii zapasowych (baza danych SQL lub MySQL), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="96deb-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Wybierz konto magazynu](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="96deb-144">Dla tooappear bazy danych na tej liście, parametrach połączenia musi istnieć w hello **parametry połączenia** sekcji hello **ustawienia aplikacji** bloku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96deb-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="96deb-145">W hello **konfiguracji kopii zapasowej** bloku, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="96deb-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="96deb-146">W hello **kopii zapasowych** bloku, kliknij przycisk **kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="96deb-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![Przycisk BackUpNow][BackUpNow]
   
    <span data-ttu-id="96deb-148">Podczas procesu tworzenia kopii zapasowej hello zostanie wyświetlony komunikat z postępu.</span><span class="sxs-lookup"><span data-stu-id="96deb-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="96deb-149">Po skonfigurowaniu hello konto magazynu i kontener w dowolnym momencie można zainicjować ręcznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="96deb-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="96deb-150">Skonfiguruj automatyczne kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="96deb-150">Configure automated backups</span></span>
1. <span data-ttu-id="96deb-151">W hello **konfiguracji kopii zapasowej** ustawić bloku **zaplanowanej kopii zapasowej** za**na**.</span><span class="sxs-lookup"><span data-stu-id="96deb-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Wybierz konto magazynu](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="96deb-153">Ustaw harmonogram tworzenia kopii zapasowych zostaną wyświetlone opcje, **zaplanowanych kopii zapasowych** za**na**następnie skonfiguruj harmonogram tworzenia kopii zapasowych hello zgodnie z potrzebami i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="96deb-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Włącz automatyczne kopie zapasowe][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="96deb-155">Skonfiguruj częściowych kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="96deb-155">Configure Partial Backups</span></span>
<span data-ttu-id="96deb-156">Czasami nie chcesz toobackup wszystko, co w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96deb-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="96deb-157">Oto kilka przykładów:</span><span class="sxs-lookup"><span data-stu-id="96deb-157">Here are a few examples:</span></span>

* <span data-ttu-id="96deb-158">Możesz [Konfigurowanie cotygodniowe kopie zapasowe](web-sites-backup.md#configure-automated-backups) aplikacji zawierający zawartości statycznej, który nigdy nie zmienia, takich jak stare wpisy na blogu lub obrazów.</span><span class="sxs-lookup"><span data-stu-id="96deb-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="96deb-159">Aplikacja ma ponad 10 GB zawartości (hello ilość max można tworzyć kopie zapasowe w czasie).</span><span class="sxs-lookup"><span data-stu-id="96deb-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="96deb-160">Nie chcesz, aby pliki dziennika hello toobackup.</span><span class="sxs-lookup"><span data-stu-id="96deb-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="96deb-161">Umożliwia częściowych kopii zapasowych, możesz wybrać dokładnie plików, których można mają toobackup.</span><span class="sxs-lookup"><span data-stu-id="96deb-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="96deb-162">Wyklucz pliki z kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="96deb-162">Exclude files from your backup</span></span>
<span data-ttu-id="96deb-163">Załóżmy, że masz aplikację, która zawiera pliki dziennika i obrazów statycznych, które zostały kopii zapasowej raz i nie będą toochange.</span><span class="sxs-lookup"><span data-stu-id="96deb-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="96deb-164">W takim przypadku można wykluczyć tych plików i folderów z są przechowywane w kopii zapasowych w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="96deb-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="96deb-165">Utwórz tooexclude plików i folderów z kopii zapasowych `_backup.filter` pliku w hello `D:\home\site\wwwroot` folderu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96deb-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="96deb-166">Określ listę hello pliki i foldery mają tooexclude w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="96deb-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="96deb-167">Pliki jest toouse Kudu tooaccess prosty sposób.</span><span class="sxs-lookup"><span data-stu-id="96deb-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="96deb-168">Kliknij przycisk **zaawansowane narzędzia -> Przejdź** ustawienie tooaccess aplikacji sieci web Kudu.</span><span class="sxs-lookup"><span data-stu-id="96deb-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![Program kudu przy użyciu portalu][kudu-portal]

<span data-ttu-id="96deb-170">Zidentyfikuj foldery hello mają tooexclude z kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="96deb-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="96deb-171">Na przykład chcesz toofilter folderu wyróżnionego hello i plików.</span><span class="sxs-lookup"><span data-stu-id="96deb-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Folderu Obrazy][ImagesFolder]

<span data-ttu-id="96deb-173">Utwórz plik o nazwie `_backup.filter` listy hello powyżej należy umieścić w pliku hello, ale usunięcie `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="96deb-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="96deb-174">Lista jednego katalogu lub pliku w jednym wierszu.</span><span class="sxs-lookup"><span data-stu-id="96deb-174">List one directory or file per line.</span></span> <span data-ttu-id="96deb-175">Dlatego należy hello zawartość pliku hello:</span><span class="sxs-lookup"><span data-stu-id="96deb-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="96deb-176">Przekaż `_backup.filter` pliku toohello `D:\home\site\wwwroot\` katalog swoją witrynę przy użyciu [ftp](web-sites-deploy.md#ftp) lub innej metody.</span><span class="sxs-lookup"><span data-stu-id="96deb-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="96deb-177">Jeśli chcesz, można utworzyć pliku hello bezpośrednio za pomocą Kudu `DebugConsole` i Wstaw zawartość hello istnieje.</span><span class="sxs-lookup"><span data-stu-id="96deb-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="96deb-178">Wykonywanie kopii zapasowych hello sam sposób, w zwykły sposób, jak [ręcznie](#create-a-manual-backup) lub [automatycznie](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="96deb-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="96deb-179">Teraz, wszystkie pliki i foldery, które są określone w `_backup.filter` został wykluczony z hello kolejnych kopii zapasowych według harmonogramu lub ręcznie zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="96deb-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="96deb-180">Przywracanie częściowych kopii zapasowych z Twojej hello lokacji tak samo jak [przywrócić zwykłej kopii zapasowej](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="96deb-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="96deb-181">proces przywracania Hello hello co.</span><span class="sxs-lookup"><span data-stu-id="96deb-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="96deb-182">Po przywróceniu pełnej kopii zapasowej, cała zawartość w witrynie hello zastępuje się ze względu na powitania kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="96deb-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="96deb-183">Jeśli plik jest w witrynie hello, ale nie w kopii zapasowej hello zostaje usunięta.</span><span class="sxs-lookup"><span data-stu-id="96deb-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="96deb-184">Jednak po przywróceniu częściowej kopii zapasowej, pozostanie zawartość, która znajduje się w jednym z katalogów hello na liście zabronionych numerów lub dowolnego pliku zabronione, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="96deb-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="96deb-185">Jak są przechowywane kopie zapasowe</span><span class="sxs-lookup"><span data-stu-id="96deb-185">How backups are stored</span></span>
<span data-ttu-id="96deb-186">Po wybraniu jednego lub więcej kopii zapasowych dla aplikacji, kopie zapasowe hello są widoczne na powitania **kontenery** blok konta magazynu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96deb-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="96deb-187">Na koncie magazynu hello, każdej kopii zapasowej składa się z`.zip` plik zawierający dane kopii zapasowej hello i `.xml` pliku, który zawiera manifest hello `.zip` pliku zawartości.</span><span class="sxs-lookup"><span data-stu-id="96deb-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="96deb-188">Można rozpakować i przeglądanie tych plików, jeśli chcesz tooaccess kopii zapasowych bez rzeczywistego wykonania przywracania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96deb-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="96deb-189">Hello kopii zapasowej bazy danych dla aplikacji hello jest przechowywany w głównym hello the.zip pliku.</span><span class="sxs-lookup"><span data-stu-id="96deb-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="96deb-190">Bazy danych SQL jest plikiem pliku BACPAC (bez rozszerzenia pliku) i można je zaimportować.</span><span class="sxs-lookup"><span data-stu-id="96deb-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="96deb-191">toocreate hello Eksportowanie pliku BACPAC — na podstawie bazy danych SQL, zobacz [importowania pliku pliku BACPAC tooCreate nową bazę danych użytkownika](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="96deb-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="96deb-192">Zmienianie hello plików w sieci **websitebackups** kontener może spowodować toobecome kopii zapasowej hello nieprawidłowy i w związku z tym nie dostępnych.</span><span class="sxs-lookup"><span data-stu-id="96deb-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="96deb-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96deb-193">Next Steps</span></span>
<span data-ttu-id="96deb-194">Aby uzyskać informacje na przywracanie z kopii zapasowej aplikacji, zobacz [Przywracanie aplikacji na platformie Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="96deb-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="96deb-195">Można również utworzyć kopii zapasowej i przywracanie aplikacji usługi App Service przy użyciu interfejsu API REST (zobacz [REST użycia toobackup i przywracania usługi aplikacji — aplikacje](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="96deb-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


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

