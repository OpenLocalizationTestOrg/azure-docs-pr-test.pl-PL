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
# <a name="restore-an-app-in-azure"></a>Przywracanie aplikacji na platformie Azure
W tym artykule opisano sposób toorestore jako aplikacja w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) , która została wcześniej utworzona kopia zapasowa (zobacz [kopii zapasowych aplikacji na platformie Azure](web-sites-backup.md)). Przywróć aplikację z poprzedniego stanu na żądanie tooa połączonej bazy danych lub Utwórz nową aplikację na podstawie jednej z aplikacji oryginalnej kopii zapasowej. Usługa aplikacji Azure obsługuje następujące bazy danych dla kopii zapasowej i przywracania hello:
- [SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)
- [Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)](https://azure.microsoft.com/en-us/services/mysql)
- [Bazy danych platformy Azure dla PostgreSQL (wersja zapoznawcza)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [MySQL w aplikacji](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

Przywracanie z kopii zapasowych jest dostępne tooapps uruchomionych w **standardowe** i **Premium** warstwy. Aby uzyskać informacji na temat skalowania aplikacji w górę, zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md). **Premium** warstwy umożliwia większej liczbie codzienne toobe kopie zapasowe wykonane niż **standardowe** warstwy.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Przywróć aplikację z istniejącej kopii zapasowej
1. Na powitania **ustawienia** bloku aplikacji w hello portalu Azure kliknij **kopii zapasowych** toodisplay hello **kopii zapasowych** bloku. Następnie kliknij przycisk **przywrócić**.
   
    ![Wybierz polecenie Przywróć teraz][ChooseRestoreNow]
2. W hello **przywrócić** bloku, pierwsze hello wybierz źródło kopii zapasowej.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    Witaj **kopii zapasowej aplikacji** opcja powoduje wyświetlenie wszystkich hello istniejące kopie zapasowe bieżącej aplikacji hello i można łatwo wybrać.
    Witaj **magazynu** opcja umożliwia wybranie dowolnego pliku ZIP kopii zapasowej z wszelkie istniejące konto magazynu Azure i kontener w ramach subskrypcji.
    Jeśli próbujesz toorestore kopii zapasowej innej aplikacji, użyj hello **magazynu** opcji.
3. Następnie określ lokalizację docelową hello Przywracanie aplikacji hello w **docelową lokalizację przywracania**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Jeśli wybierzesz **Zastąp**, wszystkie istniejące dane w bieżącej aplikacji jest usunięte i zastąpione. Przed kliknięciem przycisku **OK**, upewnij się, że jest dokładnie co chcesz toodo.
   > 
   > 
   
    Możesz wybrać **istniejącej aplikacji** toorestore hello aplikację tooanother kopii zapasowej aplikacji w hello tej samej grupie identyczny. Przed użyciem tej opcji należy utworzono już inną aplikację w grupie zasobów z dublowania bazy danych konfiguracji toohello, zdefiniowanych w aplikacji hello tworzenia kopii zapasowej. Można również utworzyć **nowy** toorestore aplikacji swoją zawartość.

4. Kliknij przycisk **OK**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Pobierz lub usunięcia kopii zapasowej z konta magazynu
1. Z głównego hello **Przeglądaj** bloku hello portalu Azure, wybierz opcję **kont magazynu**. Zostanie wyświetlona lista istniejących kont magazynu.
2. Wybierz konto magazynu hello, które zawiera kopię zapasową hello, interesujące toodownload lub delete.hello bloku dla konta magazynu hello są wyświetlane.
3. W bloku konto magazynu hello Wybierz kontener hello, który ma
   
    ![Kontenery widoku][ViewContainers]
4. Wybierz plik kopii zapasowej toodownload lub usunąć.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Kliknij przycisk **Pobierz** lub **usunąć** w zależności od tego, jakie użytkownik ma toodo.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Monitorowanie operacji przywracania
Szczegóły toosee hello powodzenie lub Niepowodzenie operacji przywracania aplikacji hello Przejdź toohello **dziennik aktywności** bloku w hello portalu Azure.  
 

Przewiń w dół toofind hello potrzeby przywracania działania i kliknij przycisk tooselect go.

Witaj szczegóły blok Wyświetla hello dostępne informacje związane z toohello operacji przywracania.

## <a name="next-steps"></a>Następne kroki
Można utworzyć kopii zapasowej i przywracania aplikacji usługi App Service przy użyciu interfejsu API REST (zobacz [tooback REST użycia zapasowych i przywracania usługi aplikacji — aplikacje](websites-csm-backup.md)).


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
