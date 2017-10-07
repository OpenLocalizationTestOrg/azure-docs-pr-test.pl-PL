---
title: "aaaRestore tooa danych systemu Windows Server lub klienta systemu Windows z platformy Azure przy użyciu hello klasycznego modelu wdrażania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toorestore z systemu Windows Server lub klienta systemu Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a>Przywróć pliki tooa systemu Windows server lub komputer kliencki z systemem Windows przy użyciu hello klasycznego modelu wdrażania
> [!div class="op_single_selector"]
> * [Portal klasyczny](backup-azure-restore-windows-server-classic.md)
> * [Witryna Azure Portal](backup-azure-restore-windows-server.md)
>
>

W tym artykule opisano sposób toorecover dane z kopii zapasowej magazynu i przywróć ją tooa serwera lub komputera. Począwszy od 2017 marca można już utworzyć magazynów kopii zapasowych w portalu klasycznym hello.

> [!IMPORTANT]
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> **15 października 2017**, użytkownik nie będzie już magazyny kopii zapasowych toocreate PowerShell toouse stanie. <br/> **Od 1 listopada 2017 roku**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
>

toorestore danych, należy użyć Kreatora odzyskiwania danych hello hello agenta usług odzyskiwania Azure firmy Microsoft (MARS). Po przywróceniu danych, istnieje możliwość:

* Wykonano przywrócenie danych toohello sam komputera, z których hello kopii zapasowych.
* Przywracanie danych tooan alternatywny maszyny.

W stycznia 2017 r firma Microsoft opublikowała agenta MARS toohello aktualizacji w wersji zapoznawczej. Wraz z poprawki, ta aktualizacja umożliwia błyskawiczne przywrócić, dzięki czemu można toomount migawki punktu odzyskiwania zapisywalny jako wolumin odzyskiwania. Następnie można eksplorować hello odzyskiwania woluminu i skopiuj pliki tooa komputera lokalnego co selektywne Przywracanie plików.

> [!NOTE]
> Witaj [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) jest wymagany, jeśli chcesz, aby toouse błyskawicznych przywracania toorestore danych. Również dane kopii zapasowej hello muszą być chronione w magazynach wymienione w artykule pomocy technicznej hello ustawień regionalnych. Zapoznaj się hello [stycznia 2017 aktualizacji kopia zapasowa Azure](https://support.microsoft.com/en-us/help/3216528?preview) hello aktualną listę ustawień regionalnych, obsługujących błyskawicznych przywracania. Przywracanie błyskawicznych jest **nie** dostępne dla wszystkich ustawień regionalnych.
>

Błyskawicznych Przywracanie jest dostępne do użycia w Magazyny usług odzyskiwania w hello portalu Azure i magazyny kopii zapasowych w portalu klasycznym hello. Jeśli chcesz przywrócić błyskawicznych toouse, Pobierz aktualizację MARS hello i postępuj zgodnie z procedurami hello, w których występuje błyskawicznych przywracania.


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
    > Jeśli nie klikniesz odinstalowywania, hello odzyskiwania woluminu pozostanie zainstalowanego przez 6 godzin od czasu hello, gdy został zainstalowany. Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin hello jest zainstalowany. Wszelkie toorun zaplanowanych operacji tworzenia kopii zapasowej w czasie hello, gdy wolumin hello jest zainstalowany, zostanie uruchomiony po hello odzyskiwania woluminu jest odinstalowane.
    >


## <a name="recover-data-toohello-same-machine"></a>Odzyskiwanie danych toohello tym samym komputerze
Jeśli przypadkowo usunięto toorestore plików i chcą go toohello kroki tej samej maszyny (z którego hello tworzenia kopii zapasowej), po hello pomoże Ci odzyskać dane hello.

1. Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w.
2. Kliknij przycisk **odzyskać dane** tooinitiate hello w przepływie pracy.

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server-classic/recover.png)
3. Wybierz hello  **tego serwera (*yourmachinename*) ** hello toorestore opcji kopii zapasowej pliku na powitania sam maszyny.

    ![Tym samym komputerze](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. Wybierz zbyt**Przeglądaj w poszukiwaniu plików** lub **wyszukiwania plików**.

    Pozostaw opcję domyślną hello Jeśli planujesz toorestore jeden lub więcej plików, których ścieżką jest znany. Jeśli nie pewności o hello struktury folderów, ale chcesz toosearch dla pliku, wybierz hello **wyszukiwania plików** opcji. W tej sekcji w celu hello firma Microsoft będzie kontynuować hello opcji domyślnej.

    ![Przeglądanie plików](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. Wybierz wolumin hello, z którego chcesz toorestore hello pliku.

    Można przywrócić z dowolnego punktu w czasie. Daty, które są wyświetlane w **bold** w formancie kalendarza hello wskazać hello dostępność punktu przywracania. Po wybraniu daty są oparte na harmonogram tworzenia kopii zapasowych (i hello powodzenie operacji tworzenia kopii zapasowej), można wybrać punkt w czasie z hello **czasu** listy rozwijanej.

    ![Data i woluminu](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. Wybierz hello toorecover elementów. Możesz wybrać wiele folderów/plików mają toorestore.

    ![Wybieranie pozycji Pliki](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. Określ parametry odzyskiwania hello.

    ![Opcje odzyskiwania](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * Istnieje możliwość przywrócenia oryginalnej lokalizacji toohello (w którym hello plik lub folder, zostaną zastąpione) lub lokalizacji tooanother w hello tym samym komputerze.
   * Jeśli hello plik lub folder ma toorestore istnieje w miejscu docelowym hello, można tworzyć kopie (Witaj dwie wersje tego samego pliku), Zastąp hello pliki w miejscu docelowym hello lub pominąć odzyskiwanie hello hello plików, które istnieją w celu hello.
   * Zdecydowanie zaleca się pozostawienie hello domyślną opcją Przywracanie listy ACL hello na powitania pliki, które są odzyskiwane.
8. Gdy te dane wejściowe są dostarczane, kliknij przycisk **dalej**. przepływu pracy odzyskiwania Hello, które przywraca hello pliki toothis maszyny, zostanie rozpoczęta.

## <a name="recover-tooan-alternate-machine"></a>Odzyskiwanie maszyny alternatywny tooan
W przypadku utraty cały serwer, można jednak odzyskać dane z innego komputera tooa kopia zapasowa Azure. następujące kroki Hello ilustrują hello przepływu pracy.  

obejmuje Hello terminologią używaną w następujące kroki:

* *Maszyna źródłowa* — podjęto hello oryginalnego komputera z kopii zapasowej które hello i który jest obecnie niedostępny.
* *Maszyna docelowa* — Witaj maszyny toowhich hello dane są odzyskiwane.
* *Przykładowe magazynu* — hello toowhich magazynu kopii zapasowej hello *maszyny źródłowej* i *maszyny docelowej* są rejestrowane. <br/>

> [!NOTE]
> Nie można przywrócić kopii zapasowych wykonanych na komputerze, na komputerze, na którym jest uruchomiony program wcześniejszej wersji systemu operacyjnego hello. Na przykład jeśli kopie zapasowe są wykonywane z komputera z systemem Windows 7, jego można przywracać w systemie Windows 8 lub nowszym maszyny. Jednak hello odwrotnie nie posiada wartość true.
>
>

1. Otwórz hello **kopia zapasowa Microsoft Azure** przyciągania w na powitania *maszyny docelowej*.
2. Upewnij się, że hello *maszyny docelowej* i hello *maszyny źródłowej* zarejestrowanych toohello są tego samego magazynu kopii zapasowych.
3. Kliknij przycisk **odzyskać dane** tooinitiate hello w przepływie pracy.

    ![Odzyskiwanie danych](./media/backup-azure-restore-windows-server-classic/recover.png)
4. Wybierz **innego serwera**

    ![Inny serwer](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. Podaj plik poświadczeń magazynu hello, która odpowiada toohello *magazynu próbki*. Jeśli plik poświadczeń magazynu hello jest nieprawidłowa (lub wygasła) Pobierz plik poświadczeń magazynu z hello *magazynu próbki* w hello klasycznego portalu Azure. Gdy podany plik poświadczeń magazynu hello hello magazynu kopii zapasowych przed plik poświadczeń magazynu hello jest wyświetlany.
6. Wybierz hello *maszyny źródłowej* z listy hello wyświetlanych maszyn.

    ![Lista komputerów](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. Wybierz albo hello **wyszukiwania plików** lub **Przeglądaj w poszukiwaniu plików** opcji. W celu hello przedstawione w tej sekcji użyjemy hello **wyszukiwania plików** opcji.

    ![Wyszukiwanie](./media/backup-azure-restore-windows-server-classic/search.png)
8. W następnym ekranie powitania, wybierz wolumin hello i daty. Wyszukiwania dla nazwy pliku/folderu hello ma toorestore.

    ![Wyszukiwanie elementów](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. Wybierz lokalizację hello gdzie hello pliki muszą toobe przywrócona.

    ![Przywracanie w lokalizacji](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. Podaj hasło szyfrowania hello, które zostało podane podczas *maszyny źródłowej* rejestracji zbyt*magazynu próbki*.

    ![Szyfrowanie](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. Po wprowadzono powitania kliknij **odzyskać**, która przywracania kopii zapasowej plików toohello miejsca docelowego określonego hello hello wyzwalaczy.

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
    > Jeśli nie klikniesz odinstalowywania, hello odzyskiwania woluminu pozostanie zainstalowanego przez 6 godzin od czasu hello, gdy został zainstalowany. Nie operacji tworzenia kopii zapasowej zostanie uruchomiony, gdy wolumin hello jest zainstalowany. Wszelkie toorun zaplanowanych operacji tworzenia kopii zapasowej w czasie hello, gdy wolumin hello jest zainstalowany, zostanie uruchomiony po hello odzyskiwania woluminu jest odinstalowane.
    >


## <a name="next-steps"></a>Następne kroki
* [Azure — często zadawane pytania kopii zapasowej](backup-azure-backup-faq.md)
* Odwiedź hello [Forum kopia zapasowa Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).

## <a name="learn-more"></a>Dowiedz się więcej
* [Omówienie kopii zapasowych Azure](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [Kopii zapasowych maszyn wirtualnych platformy Azure](backup-azure-vms-introduction.md)
* [Wykonywanie kopii zapasowej obciążeń firmy Microsoft](backup-azure-dpm-introduction.md)
