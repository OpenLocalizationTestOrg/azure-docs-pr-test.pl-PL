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
# <a name="restore-an-app-in-azure"></a>Przywracanie aplikacji na platformie Azure
W tym artykule przedstawiono sposób przywracania aplikacji w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) , która została wcześniej utworzona kopia zapasowa (zobacz [kopii zapasowych aplikacji na platformie Azure](web-sites-backup.md)). Przywracanie aplikacji za pomocą jego połączonej bazy danych na żądanie do poprzedniego stanu lub Utwórz nową aplikację na podstawie jednej z aplikacji oryginalnej kopii zapasowej. Usługa aplikacji Azure obsługuje następujące bazy danych dla kopii zapasowej i przywracania:
- [SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)
- [Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)](https://azure.microsoft.com/en-us/services/mysql)
- [Bazy danych platformy Azure dla PostgreSQL (wersja zapoznawcza)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [MySQL w aplikacji](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

Przywracanie z kopii zapasowych jest dostępne dla aplikacji działających **standardowe** i **Premium** warstwy. Aby uzyskać informacji na temat skalowania aplikacji w górę, zobacz [skalowanie w górę aplikacji na platformie Azure](web-sites-scale.md). **Premium** warstwy pozwala większa liczba codziennych kopii zapasowych wykonywanych niż **standardowe** warstwy.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Przywróć aplikację z istniejącej kopii zapasowej
1. Na **ustawienia** bloku aplikacji w portalu Azure kliknij **kopii zapasowych** do wyświetlenia **kopii zapasowych** bloku. Następnie kliknij przycisk **przywrócić**.
   
    ![Wybierz polecenie Przywróć teraz][ChooseRestoreNow]
2. W **przywrócić** bloku, najpierw wybierz źródłowy kopii zapasowej.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    **Kopii zapasowej aplikacji** opcja powoduje wyświetlenie wszystkich istniejących kopii zapasowych z bieżącej aplikacji i można łatwo wybrać.
    **Magazynu** opcja umożliwia wybranie dowolnego pliku ZIP kopii zapasowej z wszelkie istniejące konto magazynu Azure i kontener w ramach subskrypcji.
    Jeśli próbujesz przywracania kopii zapasowej innej aplikacji, użyj **magazynu** opcji.
3. Następnie określ miejsce docelowe dla przywracania aplikacji w **docelową lokalizację przywracania**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Jeśli wybierzesz **Zastąp**, wszystkie istniejące dane w bieżącej aplikacji jest usunięte i zastąpione. Przed kliknięciem przycisku **OK**, upewnij się, że jest dokładnie co chcesz zrobić.
   > 
   > 
   
    Możesz wybrać **istniejącej aplikacji** przywracania kopii zapasowej aplikacji do innej aplikacji w tej samej grupie identyczny. Przed użyciem tej opcji należy utworzono już inną aplikację w grupie zasobów z dublowania bazy danych konfiguracji do zdefiniowana w kopii zapasowej aplikacji. Można również utworzyć **nowy** aplikacji, aby przywrócić swoją zawartość.

4. Kliknij przycisk **OK**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Pobierz lub usunięcia kopii zapasowej z konta magazynu
1. W głównym **Przeglądaj** bloku portalu Azure, wybierz opcję **kont magazynu**. Zostanie wyświetlona lista istniejących kont magazynu.
2. Wybierz konto magazynu, który zawiera kopię zapasową, której chcesz pobrać lub usunąć. Zostanie wyświetlony blok dla konta magazynu.
3. W bloku konto magazynu Wybierz kontener, który ma
   
    ![Kontenery widoku][ViewContainers]
4. Wybierz plik kopii zapasowej, który chcesz pobrać lub usunąć.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Kliknij przycisk **Pobierz** lub **usunąć** w zależności od tego, co chcesz zrobić.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Monitorowanie operacji przywracania
Aby wyświetlić szczegółowe informacje o powodzeniu lub niepowodzeniu operacji przywracania aplikacji, przejdź do **dziennik aktywności** bloku w portalu Azure.  
 

Przewiń w dół do znajdowania żądaną operację przywracania i zaznacz je.

Szczegóły blok Wyświetla dostępne informacje dotyczące operacji przywracania.

## <a name="next-steps"></a>Następne kroki
Można utworzyć kopii zapasowej i przywracania aplikacji usługi App Service przy użyciu interfejsu API REST (zobacz [REST używany do kopii zapasowej i przywracania usługi aplikacji — aplikacje](websites-csm-backup.md)).


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
