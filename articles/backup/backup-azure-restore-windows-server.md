---
title: dane aaaRestore Azure tooa systemu Windows Server lub komputer z systemem Windows | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorestore dane przechowywane w Azure tooa systemu Windows Server lub komputer z systemem Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>Przywróć pliki tooa systemu Windows server lub komputer kliencki z systemem Windows przy użyciu modelu wdrażania usługi Resource Manager
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](backup-azure-restore-windows-server.md)
> * [Portal klasyczny](backup-azure-restore-windows-server-classic.md)
>
>

W tym artykule opisano sposób toorestore danych z magazynu kopii zapasowych. toorestore danych, należy użyć Kreatora odzyskiwania danych hello hello agenta usług odzyskiwania Azure firmy Microsoft (MARS). Po przywróceniu danych, istnieje możliwość:

* Wykonano przywrócenie danych toohello sam komputera, z których hello kopii zapasowych.
* Przywracanie danych tooan alternatywny maszyny.

W stycznia 2017 r firma Microsoft opublikowała agenta MARS toohello aktualizacji w wersji zapoznawczej. Wraz z poprawki, ta aktualizacja umożliwia błyskawiczne przywrócić, dzięki czemu można toomount migawki punktu odzyskiwania zapisywalny jako wolumin odzyskiwania. Następnie można eksplorować hello odzyskiwania woluminu i skopiuj pliki tooa komputera lokalnego co selektywne Przywracanie plików.

> [!NOTE]
> Witaj [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) jest wymagany, jeśli chcesz, aby toouse błyskawicznych przywracania toorestore danych. Również dane kopii zapasowej hello muszą być chronione w magazynach wymienione w artykule pomocy technicznej hello ustawień regionalnych. Zapoznaj się hello [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) hello aktualną listę ustawień regionalnych, obsługujących błyskawicznych przywracania. Przywracanie błyskawicznych jest **nie** dostępne dla wszystkich ustawień regionalnych.
>

Błyskawicznych Przywracanie jest dostępne do użycia w Magazyny usług odzyskiwania w hello portalu Azure i magazyny kopii zapasowych w portalu klasycznym hello. Jeśli chcesz przywrócić błyskawicznych toouse, Pobierz aktualizację MARS hello i postępuj zgodnie z procedurami hello, w których występuje błyskawicznych przywracania.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>Użyj błyskawicznych przywrócić toohello danych toorecover tym samym komputerze

Jeśli przypadkowo usunięto toorestore plików i chcą go toohello kroki tej samej maszyny (z którego hello tworzenia kopii zapasowej), po hello pomoże Ci odzyskać dane hello.

1. Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w. Jeśli nie znasz, którym zainstalowano przystawkę hello, wyszukaj hello komputerze lub serwerze dla **kopia zapasowa Microsoft Azure**.

    Aplikacja klasyczna Hello powinny być wyświetlane w wynikach wyszukiwania hello.

2. Kliknij przycisk **odzyskać dane** toostart hello kreatora.

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

3. Na powitania **wprowadzenie** okienka, toorestore hello danych toohello tego samego serwera lub komputera, wybierz **tego serwera (`<server name>`)** i kliknij przycisk **dalej**.

    ![Wybierz ten serwer opcja toorestore hello danych toohello tym samym komputerze](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. Na powitania **wybierz tryb odzyskiwania** okienku wybierz **poszczególnych plików i folderów** , a następnie kliknij przycisk **dalej**.

    ![Przeglądanie plików](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. Na powitania **Wybierz wolumin i data** okienku, wybierz hello wolumin, który zawiera hello pliki lub foldery mają toorestore.

    Witaj kalendarza wybierz punkt odzyskiwania. Można przywrócić z dowolnego punktu odzyskiwania w czasie. Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania. Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.

    ![Data i woluminu](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. Po wybraniu toorestore punktu odzyskiwania powitania kliknij **instalacji**.

    Kopia zapasowa Azure instaluje punkt odzyskiwania lokalne powitania i używa go jako wolumin odzyskiwania.

7. Na powitania **przeglądania i odzyskiwanie plików** okienku, kliknij przycisk **Przeglądaj** tooopen Eksploratora Windows i Znajdź hello pliki i foldery ma.

    ![Opcje odzyskiwania](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. W Eksploratorze Windows, skopiować pliki hello i/lub folderów toorestore a następnie wkleić je tooany lokalizacji toohello lokalnego serwera lub komputera. Można otworzyć lub strumienia hello pliki bezpośrednio z hello odzyskiwania woluminu i zweryfikować hello prawidłowe wersje są odzyskiwane.

    ![Skopiuj i Wklej pliki i foldery z lokalizacji toolocal zainstalowanego woluminu](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. Po zakończeniu przywracania plików hello i/lub foldery na powitania **przeglądania i pliki odzyskiwania** okienku, kliknij przycisk **Odinstaluj**. Następnie kliknij przycisk **tak** tooconfirm, które mają toounmount hello woluminu.

    ![Odinstaluj hello woluminu i Potwierdź](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > Jeśli nie klikniesz odinstalowywania, hello odzyskiwania woluminu pozostanie zainstalowanych przez 6 godzin od czasu hello, gdy został zainstalowany. Jednak hello czas instalacji jest maksymalnie rozszerzonej maksymalnie 24 godziny, w przypadku bieżących kopiowania plików. Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin hello jest zainstalowany. Wszelkie toorun zaplanowanych operacji tworzenia kopii zapasowej w czasie hello, gdy wolumin hello jest zainstalowany, zostanie uruchomiony po hello odzyskiwania woluminu jest odinstalowane.
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>Użyj błyskawicznych przywrócić toorestore danych tooan alternatywny maszyny
W przypadku utraty cały serwer, można jednak odzyskać dane z innego komputera tooa kopia zapasowa Azure. następujące kroki Hello ilustrują hello przepływu pracy.


obejmuje Hello terminologią używaną w następujące kroki:

* *Maszyna źródłowa* — podjęto hello oryginalnego komputera z kopii zapasowej które hello i który jest obecnie niedostępny.
* *Maszyna docelowa* — Witaj maszyny toowhich hello dane są odzyskiwane.
* *Przykładowe magazynu* — hello toowhich magazyn usług odzyskiwania hello *maszyny źródłowej* i *maszyny docelowej* są rejestrowane. <br/>

> [!NOTE]
> Tworzenie kopii zapasowych nie może być przywrócona tooa komputera docelowego ze starszą wersją systemu operacyjnego hello. Na przykład kopii zapasowej z systemu Windows 7, komputer może być przywrócona w systemie Windows 8 lub nowszym, komputer. Kopii zapasowej z komputera z systemem Windows 8 nie może być komputer przywróconej tooa systemu Windows 7.
>
>

1. Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w na powitania *maszyny docelowej*.

2. Upewnij się, hello *maszyny docelowej* i hello *maszyny źródłowej* są zarejestrowane toohello magazyn usług odzyskiwania tego samego.

3. Kliknij przycisk **odzyskać dane** tooopen hello **Kreatora odzyskiwania danych**.

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server/recover.png)

4. Na powitania **wprowadzenie** okienku wybierz **innego serwera**

    ![Inny serwer](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. Podaj plik poświadczeń magazynu hello, która odpowiada toohello *magazynu próbki*i kliknij przycisk **dalej**.

    Jeśli plik poświadczeń magazynu hello jest nieprawidłowa (lub wygasła), Pobierz plik poświadczeń magazynu z hello *magazynu próbki* w hello portalu Azure. Po podaniu poświadczeń ważny magazyn, pojawi się nazwa hello hello odpowiadającego magazyn kopii zapasowych.


6. Na powitania **wybierz serwer zapasowy** okienku, wybierz hello *maszyny źródłowej* z listy hello wyświetlanych maszyn i podaj hasło hello. Następnie kliknij przycisk **Next** (Dalej).

    ![Lista komputerów](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. Na powitania **wybierz tryb odzyskiwania** okienku, wybierz **poszczególnych plików i folderów** i kliknij przycisk **dalej**.

    ![Wyszukiwanie](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. Na powitania **Wybierz wolumin i data** okienku, wybierz hello wolumin, który zawiera hello pliki lub foldery mają toorestore.

    Witaj kalendarza wybierz punkt odzyskiwania. Można przywrócić z dowolnego punktu odzyskiwania w czasie. Daty w **bold** wskazać hello dostępności co najmniej jeden punkt odzyskiwania. Po wybraniu Data, jeśli dostępnych jest wiele punktów odzyskiwania, wybierz hello określony punkt odzyskiwania z hello **czasu** menu rozwijanego.

    ![Wyszukiwanie elementów](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. Kliknij przycisk **instalacji** punkt odzyskiwania hello instalacji toolocally jako wolumin odzyskiwania na Twojej *maszyny docelowej*.

10. Na powitania **przeglądania i odzyskiwanie plików** okienku, kliknij przycisk **Przeglądaj** tooopen Eksploratora Windows i Znajdź hello pliki i foldery ma.

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. W Eksploratorze Windows, skopiuj hello pliki lub foldery z hello odzyskiwania woluminu i wklej je tooyour *maszyny docelowej* lokalizacji. Można otworzyć lub strumienia hello pliki bezpośrednio z hello odzyskiwania woluminu i zweryfikować hello prawidłowe wersje są odzyskiwane.

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. Po zakończeniu przywracania plików hello i/lub foldery na powitania **przeglądania i pliki odzyskiwania** okienku, kliknij przycisk **Odinstaluj**. Następnie kliknij przycisk **tak** tooconfirm, które mają toounmount hello woluminu.

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > Jeśli nie klikniesz odinstalowywania, hello odzyskiwania woluminu pozostanie zainstalowanych przez 6 godzin od czasu hello, gdy został zainstalowany. Jednak hello czas instalacji jest maksymalnie rozszerzonej maksymalnie 24 godziny, w przypadku bieżących kopiowania plików. Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin hello jest zainstalowany. Wszelkie toorun zaplanowanych operacji tworzenia kopii zapasowej w czasie hello, gdy wolumin hello jest zainstalowany, zostanie uruchomiony po hello odzyskiwania woluminu jest odinstalowane.
    >

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli kopia zapasowa Azure nie jest pomyślnie instalowany hello odzyskiwania woluminu nawet po kilku minutach klikanie **instalacji** lub kończy się niepowodzeniem toomount hello odzyskiwania woluminu z co najmniej jeden błąd, wykonaj kroki hello poniżej toobegin odzyskiwanie normalnie.

1.  Anuluj proces instalacji trwającą hello na wypadek, gdyby była uruchomiona na kilka minut.

2.  Upewnij się, że znajdują się na powitania najnowszą wersję agenta usługi Kopia zapasowa Azure hello. toofind limit hello informacje o wersji agenta usługi Kopia zapasowa Azure, wybierz polecenie **o Microsoft agenta usług odzyskiwania Azure** na powitania **akcje** okienko kopia zapasowa Microsoft Azure konsoli i upewnij się, że hello  **Wersja** liczba jest równa tooor wyższa niż wersja hello wymienionych w [w tym artykule](https://go.microsoft.com/fwlink/?linkid=229525). Możesz pobrać najnowszą wersję hello z [tutaj](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  Przejdź za**Menedżera urządzeń** -> **kontrolerów magazynu** i upewnij się, że można zlokalizować **inicjatora iSCSI firmy Microsoft**. Jeśli mogą ją odnaleźć, przejdź bezpośrednio toostep 7 poniżej. 

4.  Jeśli nie można zlokalizować Usługa inicjatora iSCSI firmy Microsoft, jak wspomniano w kroku 3, określ, czy toosee można odnaleźć wpisu w obszarze **Menedżera urządzeń** -> **kontrolerów magazynu** o nazwie  **Nieznane urządzenie** o identyfikatorze sprzętu **ROOT\ISCSIPRT**.

5.  Kliknij prawym przyciskiem myszy **nieznane urządzenie** i wybierz **aktualizacji sterowników**.

6.  Sterownik hello aktualizacji, wybierając opcję hello zbyt **Wyszukaj automatycznie zaktualizowane sterowniki**. Należy zmienić ukończenia aktualizacji hello **nieznane urządzenie** za**inicjatora iSCSI firmy Microsoft** jak pokazano poniżej. 

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  Przejdź za**Menedżera zadań** -> **usługi (lokalne)** -> **Usługa inicjatora iSCSI firmy Microsoft**. 

    ![Szyfrowanie](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  Uruchom ponownie usługę inicjatora iSCSI firmy Microsoft hello przez usługę hello, klikając prawym przyciskiem myszy **zatrzymać** i ponowne kliknięcie prawym przyciskiem myszy, a następnie klikając **Start**.

9.  Ponów odzyskiwanie przy użyciu błyskawicznych przywracania. 

Jeśli nadal nie hello odzyskiwania, ponowny rozruch serwera/klienta. Jeśli ponowne uruchomienie komputera nie jest pożądane lub hello odzyskiwania nadal kończy się niepowodzeniem nawet po ponowny rozruch serwera hello, spróbuj przeprowadzić odzyskiwanie z alternatywnych maszyny i skontaktuj się z Azure obsługuje przechodząc zbyt[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) i przesyłanie żądania pomocy technicznej.

## <a name="next-steps"></a>Następne kroki
* Teraz, gdy zostały odzyskane pliki i foldery, możesz [Zarządzanie kopii zapasowych](backup-azure-manage-windows-server.md).
