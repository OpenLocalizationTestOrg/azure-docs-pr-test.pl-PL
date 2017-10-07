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
# <a name="back-up-your-app-in-azure"></a>Tworzenie kopii zapasowej aplikacji na platformie Azure
Witaj kopii zapasowych i przywracania funkcji w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) umożliwia łatwe tworzenie kopii zapasowych aplikacji, ręcznie lub zgodnie z harmonogramem. Przywracanie aplikacji tooanother lub zastępowania istniejącej aplikacji hello, można przywrócić migawki tooa aplikacji hello poprzedniego stanu. 

Aby uzyskać informacje na przywracanie z kopii zapasowej aplikacji, zobacz [Przywracanie aplikacji na platformie Azure](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>Kopiami zapasowymi
Usługi aplikacji może wykonywać kopie zapasowe następujących hello informacji tooan konta magazynu Azure i kontener skonfigurowano toouse Twojej aplikacji. 

* Konfiguracja aplikacji
* Zawartość pliku
* Aplikacja tooyour połączenia bazy danych

Witaj następujące rozwiązania bazy danych są obsługiwane przy użyciu funkcji tworzenia kopii zapasowej: 
   - [SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)](https://azure.microsoft.com/en-us/services/mysql)
   - [Bazy danych platformy Azure dla PostgreSQL (wersja zapoznawcza)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [MySQL w aplikacji](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  Każda kopia zapasowa jest w trybie offline pełną kopię aplikacji, nie aktualizację przyrostową.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Wymagania i ograniczenia
* Witaj kopii zapasowych i funkcja przywracania wymaga hello toobe planu usługi aplikacji w hello **standardowe** warstwy lub **Premium** warstwy. Aby uzyskać więcej informacji na temat skalowania Twojej toouse planu usługi aplikacji wyższego poziomu, zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md).  
  **Premium** warstwy umożliwia większej liczbie codziennie kopii ups niż **standardowe** warstwy.
* Wymagane konto magazynu Azure i kontener w hello tej samej subskrypcji co aplikacja hello, które mają toobackup. Aby uzyskać więcej informacji na kontach magazynu Azure, zobacz hello [łącza](#moreaboutstorage) na końcu hello w tym artykule.
* Kopie zapasowe mogą być zapasowej GB too10 zawartości aplikacji i bazy danych. Jeśli rozmiar kopii zapasowej hello przekracza ten limit, wystąpi błąd.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>Ręczne tworzenie kopii zapasowej
1. W hello [Azure Portal](https://portal.azure.com), przejdź do bloku tooyour aplikacji, wybierz **kopii zapasowych**. Witaj **kopii zapasowych** zostanie wyświetlony blok.
   
    ![Strona kopii zapasowych][ChooseBackupsPage]
   
   > [!NOTE]
   > Jeśli widzisz wiadomość hello poniżej, kliknij go, tooupgrade planu usługi aplikacji przed kontynuowaniem z kopii zapasowych.
   > Zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md) Aby uzyskać więcej informacji.  
   > ![Wybierz konto magazynu](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. W hello **kopii zapasowej** bloku, kliknij przycisk **Konfiguruj**
![kliknij przycisk Konfiguruj.](./media/web-sites-backup/ClickConfigure1.png)
3. W hello **konfiguracji kopii zapasowej** bloku, kliknij przycisk **magazynu: nieskonfigurowane** tooconfigure konta magazynu.
   
    ![Wybierz konto magazynu][ChooseStorageAccount]
4. Wybierz miejsce docelowe kopii zapasowej, wybierając **konta magazynu** i **kontenera**. Konto magazynu Hello muszą należeć toohello tej samej subskrypcji co chcesz tooback zapasowe aplikacji hello. Jeśli chcesz, można utworzyć nowe konto magazynu lub nowy kontener w blokach odpowiednich hello. Gdy wszystko będzie gotowe, kliknij przycisk **wybierz**.
   
    ![Wybierz konto magazynu](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. W hello **konfiguracji kopii zapasowej** bloku, który nadal pozostanie otwarty, możesz skonfigurować **instrukcji Backup Database**, następnie wybierz hello baz danych, tooinclude w hello tworzenia kopii zapasowych (baza danych SQL lub MySQL), a następnie kliknij przycisk **OK**.  
   
    ![Wybierz konto magazynu](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Dla tooappear bazy danych na tej liście, parametrach połączenia musi istnieć w hello **parametry połączenia** sekcji hello **ustawienia aplikacji** bloku aplikacji.
   > 
   > 
6. W hello **konfiguracji kopii zapasowej** bloku, kliknij przycisk **zapisać**.    
7. W hello **kopii zapasowych** bloku, kliknij przycisk **kopii zapasowej**.
   
    ![Przycisk BackUpNow][BackUpNow]
   
    Podczas procesu tworzenia kopii zapasowej hello zostanie wyświetlony komunikat z postępu.

Po skonfigurowaniu hello konto magazynu i kontener w dowolnym momencie można zainicjować ręcznego tworzenia kopii zapasowej.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Skonfiguruj automatyczne kopie zapasowe
1. W hello **konfiguracji kopii zapasowej** ustawić bloku **zaplanowanej kopii zapasowej** za**na**. 
   
    ![Wybierz konto magazynu](./media/web-sites-backup/05ScheduleBackup1.png)
2. Ustaw harmonogram tworzenia kopii zapasowych zostaną wyświetlone opcje, **zaplanowanych kopii zapasowych** za**na**następnie skonfiguruj harmonogram tworzenia kopii zapasowych hello zgodnie z potrzebami i kliknij **OK**.
   
    ![Włącz automatyczne kopie zapasowe][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Skonfiguruj częściowych kopii zapasowych
Czasami nie chcesz toobackup wszystko, co w aplikacji. Oto kilka przykładów:

* Możesz [Konfigurowanie cotygodniowe kopie zapasowe](web-sites-backup.md#configure-automated-backups) aplikacji zawierający zawartości statycznej, który nigdy nie zmienia, takich jak stare wpisy na blogu lub obrazów.
* Aplikacja ma ponad 10 GB zawartości (hello ilość max można tworzyć kopie zapasowe w czasie).
* Nie chcesz, aby pliki dziennika hello toobackup.

Umożliwia częściowych kopii zapasowych, możesz wybrać dokładnie plików, których można mają toobackup.

### <a name="exclude-files-from-your-backup"></a>Wyklucz pliki z kopii zapasowej
Załóżmy, że masz aplikację, która zawiera pliki dziennika i obrazów statycznych, które zostały kopii zapasowej raz i nie będą toochange. W takim przypadku można wykluczyć tych plików i folderów z są przechowywane w kopii zapasowych w przyszłości. Utwórz tooexclude plików i folderów z kopii zapasowych `_backup.filter` pliku w hello `D:\home\site\wwwroot` folderu aplikacji. Określ listę hello pliki i foldery mają tooexclude w tym pliku. 

Pliki jest toouse Kudu tooaccess prosty sposób. Kliknij przycisk **zaawansowane narzędzia -> Przejdź** ustawienie tooaccess aplikacji sieci web Kudu.

![Program kudu przy użyciu portalu][kudu-portal]

Zidentyfikuj foldery hello mają tooexclude z kopii zapasowych.  Na przykład chcesz toofilter folderu wyróżnionego hello i plików.

![Folderu Obrazy][ImagesFolder]

Utwórz plik o nazwie `_backup.filter` listy hello powyżej należy umieścić w pliku hello, ale usunięcie `D:\home`. Lista jednego katalogu lub pliku w jednym wierszu. Dlatego należy hello zawartość pliku hello:
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Przekaż `_backup.filter` pliku toohello `D:\home\site\wwwroot\` katalog swoją witrynę przy użyciu [ftp](web-sites-deploy.md#ftp) lub innej metody. Jeśli chcesz, można utworzyć pliku hello bezpośrednio za pomocą Kudu `DebugConsole` i Wstaw zawartość hello istnieje.

Wykonywanie kopii zapasowych hello sam sposób, w zwykły sposób, jak [ręcznie](#create-a-manual-backup) lub [automatycznie](#configure-automated-backups). Teraz, wszystkie pliki i foldery, które są określone w `_backup.filter` został wykluczony z hello kolejnych kopii zapasowych według harmonogramu lub ręcznie zainicjowane. 

> [!NOTE]
> Przywracanie częściowych kopii zapasowych z Twojej hello lokacji tak samo jak [przywrócić zwykłej kopii zapasowej](web-sites-restore.md). proces przywracania Hello hello co.
> 
> Po przywróceniu pełnej kopii zapasowej, cała zawartość w witrynie hello zastępuje się ze względu na powitania kopii zapasowej. Jeśli plik jest w witrynie hello, ale nie w kopii zapasowej hello zostaje usunięta. Jednak po przywróceniu częściowej kopii zapasowej, pozostanie zawartość, która znajduje się w jednym z katalogów hello na liście zabronionych numerów lub dowolnego pliku zabronione, ponieważ jest.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Jak są przechowywane kopie zapasowe
Po wybraniu jednego lub więcej kopii zapasowych dla aplikacji, kopie zapasowe hello są widoczne na powitania **kontenery** blok konta magazynu i aplikacji. Na koncie magazynu hello, każdej kopii zapasowej składa się z`.zip` plik zawierający dane kopii zapasowej hello i `.xml` pliku, który zawiera manifest hello `.zip` pliku zawartości. Można rozpakować i przeglądanie tych plików, jeśli chcesz tooaccess kopii zapasowych bez rzeczywistego wykonania przywracania aplikacji.

Hello kopii zapasowej bazy danych dla aplikacji hello jest przechowywany w głównym hello the.zip pliku. Bazy danych SQL jest plikiem pliku BACPAC (bez rozszerzenia pliku) i można je zaimportować. toocreate hello Eksportowanie pliku BACPAC — na podstawie bazy danych SQL, zobacz [importowania pliku pliku BACPAC tooCreate nową bazę danych użytkownika](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> Zmienianie hello plików w sieci **websitebackups** kontener może spowodować toobecome kopii zapasowej hello nieprawidłowy i w związku z tym nie dostępnych.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>Następne kroki
Aby uzyskać informacje na przywracanie z kopii zapasowej aplikacji, zobacz [Przywracanie aplikacji na platformie Azure](web-sites-restore.md). Można również utworzyć kopii zapasowej i przywracanie aplikacji usługi App Service przy użyciu interfejsu API REST (zobacz [REST użycia toobackup i przywracania usługi aplikacji — aplikacje](websites-csm-backup.md)).


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

