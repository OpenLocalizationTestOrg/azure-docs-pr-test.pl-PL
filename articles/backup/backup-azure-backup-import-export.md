---
title: "aaaAzure Backup - kopii zapasowej w trybie Offline lub początkowego rozmieszczania użyciu hello usługi Import/Eksport Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Kopia zapasowa Azure umożliwia danych toosend hello sieci za pomocą usługi Import/Eksport Azure hello. W tym artykule opisano hello w trybie offline wstępne wypełnianie danych początkowej kopii zapasowej hello za pomocą usługi Azure Importuj Eksportuj hello."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Przepływ pracy tworzenia kopii zapasowych w trybie offline w usłudze Azure Backup
Kopia zapasowa Azure zawiera kilka wbudowanych korzyści, które zapisania koszty sieci i magazynu podczas hello początkowej pełnych kopii zapasowych danych tooAzure. Początkowa pełnych kopii zapasowych zwykle transfer dużych ilości danych i wymagają większej przepustowości sieci w porównaniu toosubsequent kopii zapasowych, które transfer tylko hello delty/przyrostowa. Kopia zapasowa Azure kompresuje hello początkowej kopii zapasowych. Proces hello obsługi w trybie offline kopia zapasowa Azure można używać dysków tooupload hello skompresowane dane początkowej kopii zapasowej w trybie offline tooAzure.  

Witaj w trybie offline wstępne wypełnianie procesu usługi Azure Backup jest ściśle zintegrowany z hello [usługi Import/Eksport Azure](../storage/common/storage-import-export-service.md) umożliwiająca tootransfer tooAzure danych przy użyciu dysków. Jeśli masz terabajtów (tabel) dane początkowej kopii zapasowej, wymagającym toobe przesyłanych przez sieć dużymi opóźnieniami i niskiej przepustowości, można użyć hello w trybie offline wstępne wypełnianie przepływu pracy tooship hello początkowa kopia zapasowa na jeden lub więcej dysków twardych tooan centrum danych Azure. Ten artykuł zawiera omówienie kroków hello, kończące ten przepływ pracy.

## <a name="overview"></a>Omówienie
Z możliwością obsługi w trybie offline hello Azure Backup i Azure importu/eksportu jest prosty tooupload hello danych w trybie offline tooAzure przy użyciu dysków. Zamiast transferowania hello początkowa pełna kopia hello sieci, dane kopii zapasowej hello napisano tooa *lokalizacji przejściowej*. Po zakończeniu kopiowania hello toohello przemieszczana lokalizacja za pomocą narzędzia Import/Eksport Azure hello te dane są zapisywane się, że dyski tooone lub SATA więcej, w zależności od hello ilości danych. Dyski te są ostatecznie dostarczana toohello najbliższego centrum danych Azure.

Witaj [sierpnia 2016 aktualizacji z usługi Kopia zapasowa Azure (i nowszych)](http://go.microsoft.com/fwlink/?LinkID=229525) obejmuje hello *narzędzie do przygotowywania dysków Azure*, o nazwie AzureOfflineBackupDiskPrep, który:

* Pomaga przygotować dysków dla importu platformy Azure przy użyciu narzędzia Import/Eksport Azure hello.
* Automatycznie tworzy zadania importu platformy Azure dla usługi Import/Eksport Azure hello na powitania [klasycznego portalu Azure](https://manage.windowsazure.com) jako toocreating min. hello sam ręcznie ze starszymi wersjami programu Kopia zapasowa Azure.

Po zakończeniu przekazywania hello hello tooAzure dane kopii zapasowej, kopia zapasowa Azure kopiuje hello magazynu kopii zapasowych toohello dane kopii zapasowej i hello przyrostowych kopii zapasowych.

> [!NOTE]
> hello toouse narzędzie do przygotowywania dysków Azure, sprawdź, czy zainstalowano hello sierpnia 2016 aktualizacji z usługi Kopia zapasowa Azure (lub nowsza) i wykonaj wszystkie czynności hello przepływu pracy hello z nim. Jeśli używasz starszej wersji programu Kopia zapasowa Azure, można przygotować dysk SATA hello za pomocą narzędzia Import/Eksport Azure hello zgodnie z opisem w kolejnych sekcjach niniejszego artykułu.
>
>

## <a name="prerequisites"></a>Wymagania wstępne
* [Zapoznaj się z przepływem pracy Import/Eksport Azure hello](../storage/common/storage-import-export-service.md).
* Przed rozpoczęciem powitalne przepływu pracy, upewnij się, hello następujące czynności:
  * Utworzono magazynie usługi Kopia zapasowa Azure.
  * Pobrano poświadczenia magazynu.
  * Hello Azure Backup agent został zainstalowany na systemu Windows Server/Windows klienta lub serwera programu System Center Data Protection Manager, a komputer hello jest zarejestrowany w magazynie kopii zapasowej Azure hello.
* [Pobieranie ustawień publikowania na platformie Azure pliku hello](https://manage.windowsazure.com/publishsettings) na komputerze hello, z którego planujesz tooback danych.
* Przygotuj tymczasowej lokalizacji, która może być udziału sieciowego lub dodatkowego dysku na komputerze hello. Hello tymczasowej lokalizacji przejściowej magazynu i jest używana tymczasowo w tym przepływie pracy. Upewnij się, że hello lokalizacji wystawiania ma za mało toohold miejsca na dysku do początkowej kopii. Na przykład jeśli próbujesz tooback serwera plików 500 GB, upewnij się, że obszaru przemieszczania hello jest co najmniej 500 GB. (Mniejszą ilość jest używany z powodu toocompression.)
* Upewnij się, że dysk obsługiwane. Tylko 2,5 SSD lub 2,5 lub 3,5 cala SATA II/III wewnętrzne dyski twarde są obsługiwane do używania z hello usługi Import/Eksport. Można użyć dysków zapasowych too10 TB. Sprawdź hello [dokumentację usługi Import/Eksport Azure](../storage/common/storage-import-export-service.md#hard-disk-drives) hello najnowsze zestawu dysków, które hello obsługuje usługi.
* Włącz funkcję BitLocker na powitania toowhich komputer jest połączony moduł zapisujący dysków SATA hello.
* [Pobierz narzędzie Import/Eksport Azure hello](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) toohello komputera toowhich hello SATA dysku writer jest połączony. Ten krok nie jest wymagane, jeśli zostały pobrane i zainstalowane hello sierpnia 2016 aktualizacji z usługi Kopia zapasowa Azure (lub nowsza).

## <a name="workflow"></a>Przepływ pracy
Witaj informacje w tej sekcji pomaga ukończenia przepływu pracy w trybie offline z kopii zapasowej hello tak, aby dane mogą być dostarczane tooan centrum danych Azure i przekazać tooAzure magazynu. Jeśli masz pytania dotyczące usługi Import hello lub dowolnego aspektu hello procesu, zobacz hello [Import — Omówienie usługi](../storage/common/storage-import-export-service.md) dokumentacji odwołuje się do wcześniej.

### <a name="initiate-offline-backup"></a>Inicjowanie kopii zapasowej w trybie offline
1. Podczas planowania kopii zapasowej, zostanie wyświetlony powitania po ekranu (w systemie Windows Server, klient systemu Windows lub System Center Data Protection Manager).

    ![Importuj ekranu](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    Oto odpowiedniego ekranie powitania w System Center Data Protection Manager: <br/>
    ![Program DPM importu ekranu](./media/backup-azure-backup-import-export/dpmoffline.png)

    Opis Hello hello danych wejściowych jest następujący:

    * **Miejsce przemieszczania**: hello tymczasowej lokalizacji toowhich hello początkowa kopia zapasowa zostanie zapisany. Może to być na komputerze lokalnym lub w udziale sieciowym. Witaj kopiowania komputera i komputera źródłowego są różne, zaleca się że podajesz hello pełną ścieżkę sieciową hello tymczasowej lokalizacji.
    * **Nazwa zadania importowania platformy Azure**: hello unikatową nazwę importu platformy Azure, które usługi i kopia zapasowa Azure śledzić hello transferu danych przesyłanych na tooAzure dysków.
    * **Ustawień publikowania platformy Azure**: plik XML, który zawiera informacje o profilu subskrypcji. Zawiera ona także bezpiecznych poświadczeń, które są skojarzone z subskrypcją. Możesz [Pobierz plik hello](https://manage.windowsazure.com/publishsettings). Podaj plik ustawień publikowania hello toohello ścieżkę lokalną.
    * **Identyfikator subskrypcji platformy Azure**: hello identyfikator subskrypcji platformy Azure dla subskrypcji hello, w którym planujesz zadania importu platformy Azure hello tooinitiate. Jeśli masz wiele subskrypcji Azure, należy użyć Identyfikatora hello hello subskrypcji, które mają tooassociate z zadaniem importu hello.
    * **Konto usługi Azure Storage**: hello klasycznego typu konta magazynu w hello podane subskrypcji platformy Azure, która zostanie skojarzona z zadaniem importu platformy Azure hello.
    * **Kontener magazynu Azure**: hello nazwa obiektu blob magazynu docelowego hello w hello kontem magazynu platformy Azure, w którym będą importowane dane tego zadania.

    > [!NOTE]
    > Jeśli zarejestrowano tooan Twojego serwera magazyn usług odzyskiwania Azure i z hello [portalu Azure](https://portal.azure.com) dla kopii zapasowych i nie są w subskrypcji Cloud Solution Provider (CSP), można tworzyć klasycznego typu konta magazynu z hello Portalu Azure i użyć jej do przepływu pracy w trybie offline z kopii zapasowej hello.
    >
    >

     Zapisz te informacje, ponieważ potrzebna tooenter go ponownie następujące kroki. Tylko hello *lokalizacji przejściowej* jest wymagany, jeśli używasz hello Azure przygotowanie dysku narzędzia tooprepare hello dysków.    
2. Ukończyć powitalnych przepływu pracy, a następnie wybierz **wykonaj kopię zapasową teraz** kopii hello kopia zapasowa Azure management konsoli tooinitiate hello — kopia zapasowa offline. Początkowa kopia zapasowa Hello są zapisywane obszaru przemieszczania toohello w ramach tego kroku.

    ![Wykonaj kopię zapasową](./media/backup-azure-backup-import-export/backupnow.png)

    toocomplete hello odpowiedniego przepływu pracy w System Center Data Protection Manager, kliknij prawym przyciskiem myszy hello **grupy ochrony**, a następnie wybierz pozycję hello **Utwórz punkt odzyskiwania** opcji. Następnie wybierz pozycję hello **ochrony w trybie Online** opcji.

    ![Natychmiastowe tworzenie kopii zapasowej programu DPM](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Po zakończeniu działania hello hello tymczasowej lokalizacji jest gotowy toobe używane w celu przygotowania dysku.

    ![Postęp tworzenia kopii zapasowej](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>Przygotowanie dysków SATA i Utwórz zadania importu platformy Azure przy użyciu narzędzia przygotowywania dysków Azure hello
Narzędzie do przygotowywania dysków Azure Hello jest dostępny w katalogu instalacji agenta usług odzyskiwania hello (aktualizacja z sierpnia 2016 lub nowszy) w hello ze ścieżką.

   *\Microsoft* *azure* *odzyskiwania* *usług* * Agent\Utils\*

1. Przejdź toohello katalogu, a kopia hello **AzureOfflineBackupDiskPrep** katalogu tooa kopii komputera, na które hello przygotowane toobe dyski są zainstalowane. Upewnij się, hello następujące — z uwzględnieniem toohello kopiowania komputera:

    * Witaj kopiowania komputer ma dostęp do tymczasowej lokalizacji dla przepływu pracy w trybie offline wstępne wypełnianie w hello przy użyciu hello sam sieci ścieżkę zapewnionej w programie hello hello **zainicjować kopię zapasową offline** przepływu pracy.
    * Funkcja BitLocker jest włączona na komputerze hello.
    * Witaj komputer ma dostęp do hello portalu Azure.

    W razie potrzeby hello kopiowania komputera można hello w taki sam jak hello komputera źródłowego.
2. Otwórz wiersz polecenia z podwyższonym poziomem uprawnień na komputerze kopii hello katalog narzędzie przygotowywania dysków Azure hello hello bieżącego katalogu, a następnie uruchom następujące polecenie hello:

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | Parametr | Opis |
    | --- | --- |
    | s:&lt;*ścieżka lokalizacji przemieszczania*&gt; |Obowiązkowe danych wejściowych został użyty toohello ścieżka hello tooprovide tymczasowej lokalizacji, wprowadzony w hello **zainicjować kopię zapasową offline** przepływu pracy. |
    | p:&lt;*tooPublishSettingsFile ścieżki*&gt; |Opcjonalne dane wejściowe, do których został użyty tooprovide hello ścieżki toohello **ustawień publikowania platformy Azure** pliku wprowadzony w hello **zainicjować kopię zapasową offline** przepływu pracy. |

    > [!NOTE]
    > Witaj &lt;tooPublishSettingFile ścieżki&gt; wartość jest konieczny, gdy hello kopiowania komputera i komputera źródłowego są różne.
    >
    >

    Po uruchomieniu polecenia hello narzędzia hello żądań hello wybór hello zadania importu platformy Azure, który odpowiada toohello dysków, które należy przygotować toobe. Jeśli tylko zadania importu pojedynczego jest skojarzona z hello podane tymczasowej lokalizacji, pojawia się ekran, takich jak hello, który jest zgodny.

    ![Azure wprowadzania narzędzie przygotowanie dysku](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Wprowadź literę dysku hello bez hello kończyć dwukropkiem dla zainstalowanego dysku hello mają tooprepare dla tooAzure transferu. Potwierdź hello formatowania dysku powitania po wyświetleniu monitu.

    Narzędzie Hello następnie rozpoczyna tooprepare hello dysk z hello dane kopii zapasowej. Może być konieczne dodatkowe dyski tooattach po wyświetleniu monitu przez narzędzie hello w przypadku hello pod warunkiem, że dysk nie ma wystarczającą ilość miejsca na powitania dane kopii zapasowej. <br/>

    Na końcu hello pomyślnego wykonania narzędzia hello jeden lub więcej dysków, które są przygotowywane dla tooAzure wysyłki. Ponadto zadania importu o nazwie hello podany podczas hello **zainicjować kopię zapasową offline** przepływu pracy jest tworzona na powitania klasycznego portalu Azure. Na koniec hello narzędzie wyświetla hello toohello adres wysyłkowy centrum danych Azure, której hello dyski muszą toobe wysłane i hello zadania importu hello toolocate łącza na powitania klasycznego portalu Azure.

    ![Zakończenie przygotowywania dysku platformy Azure](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. Toohello dysków hello statku narzędzia hello podany adres i przechowywać hello śledzenia numer do użytku w przyszłości.<br/>

5. Po przejściu toohello połączyć tego narzędzia hello wyświetlane, zobacz konto magazynu Azure hello określonej w hello **zainicjować kopię zapasową offline** przepływu pracy. W tym miejscu można wyświetlić zadania importu hello nowo utworzony na powitania **IMPORTU/eksportu** kartę hello konta magazynu.

    ![Zadania utworzone importu](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. Kliknij przycisk **WYSYŁANIA informacji** u dołu hello tooupdate strony hello kontaktu szczegółów, pokazane na powitania po ekranie. Firma Microsoft używa tego tooship informacje o Twojej tooyou wstecz dysków po hello Importuj zadanie zostało zakończone.

    ![Informacje kontaktowe](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Wprowadź szczegóły wysyłki na następnym ekranie powitania hello. Podaj hello **operatora dostarczania** i **numer identyfikacyjny** szczegółowe informacje, które odpowiadają toohello dyski zostały wydane toohello centrum danych Azure.

    ![Wysyłanie informacji o](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>Hello ukończenia przepływu pracy
Po zakończeniu zadania importu hello danych początkowej kopii zapasowej jest dostępna na koncie magazynu. Witaj agenta usług odzyskiwania, a następnie zawartość hello kopii danych hello z tego magazynu kopii zapasowych toohello konta lub usług odzyskiwania magazyn, którekolwiek ma zastosowanie. W czasie tworzenia kopii zapasowej hello harmonogramem hello agenta kopii zapasowej Azure wykonuje hello przyrostowej kopii zapasowej za pośrednictwem hello początkowa kopia zapasowa.

> [!NOTE]
> Witaj sekcje mają zastosowanie toousers wcześniejszych wersjach programu Kopia zapasowa Azure, którzy nie mają narzędzie przygotowywania dysków Azure toohello dostępu.
>
>

### <a name="prepare-a-sata-drive"></a>Przygotowanie dysków SATA
1. Pobierz hello [narzędzie importu/eksportu pakietu Microsoft Azure](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) toohello kopiowania komputera. Upewnij się, że hello lokalizacji wystawiania jest dostępny z komputera hello, w którym planujesz toorun hello dalej zestaw poleceń. W razie potrzeby hello kopiowania komputera można hello w taki sam jak hello komputera źródłowego.

2. Rozpakuj plik WAImportExport.zip hello. Uruchom narzędzie WAImportExport hello, które formatuje dysk SATA hello, zapisuje hello dane kopii zapasowej toohello SATA dysku i szyfruje go. Przed uruchomieniem hello następujące polecenia, upewnij się, czy funkcja BitLocker jest włączona na komputerze hello. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Po zainstalowaniu aktualizacji sierpnia 2016 hello kopia zapasowa Azure (lub nowsza), upewnij się, tym hello tymczasowej lokalizacji, wprowadzony jest taki sam, jak hello na powitania hello **wykonaj kopię zapasową teraz** ekranu i zawiera pliki AIB i obiektów Blob Base.
    >
    >

| Parametr | Opis |
| --- | --- |
| /j: <*JournalFile*> |Witaj ścieżki pliku dziennika toohello. Każdy dysk musi mieć dokładnie jeden plik dziennika. plik dziennika Hello musi znajdować się na dysku docelowego hello. rozszerzenie pliku dziennika Hello jest .jrn i zostanie utworzony jako część tego polecenia. |
| / Identyfikator: <*SessionId*> |Identyfikator sesji Hello identyfikuje sesję kopiowania. Jest używane tooensure odzyskiwania dokładne kopiowania przerwania sesji. Pliki, które są kopiowane w ramach sesji kopiowania są przechowywane w katalogu o nazwie po hello identyfikator sesji na dysku docelowym hello. |
| /SK: <*StorageAccountKey*> |klucz konta Hello hello magazynu konta toowhich hello danych zostaną zaimportowane. Witaj Witaj toobe klucza potrzeb tak samo jak została podana podczas tworzenia grupy ochrony zasad tworzenia kopii zapasowej. |
| / BlobType |Typ Hello obiektu blob. Ten przepływ pracy zakończy się powodzeniem, tylko wtedy, gdy **PageBlob** jest określona. To nie jest opcją domyślną hello i powinny być podane w tego polecenia. |
| / t: <*TargetDriveLetter*> |litera dysku Hello bez hello końcowe dwukropek hello docelowy dysk hello bieżącej sesji kopiowania. |
| / Format |Witaj opcja tooformat hello dysku. Określ ten parametr, gdy hello potrzebuje toobe sformatowana; w przeciwnym razie Pomiń go. Zanim narzędzie hello formatuje dysk hello, wyświetli monit o potwierdzenie hello konsoli. toosuppress hello potwierdzenia, określ parametr /silentmode hello. |
| / szyfrowania |Witaj opcja tooencrypt hello dysku. Określ ten parametr, gdy hello dysku nie ma jeszcze szyfrowane z funkcją BitLocker i potrzeb toobe szyfrowane przez narzędzie hello. Jeśli dysk hello już został zaszyfrowany za pomocą funkcji BitLocker, Pomiń ten parametr, określ parametr /bk hello i podaj hello istniejącego klucza funkcji BitLocker. Jeśli określono parametr/format hello, możesz określić hello / zaszyfrować parametru. |
| /srcdir: <*SourceDirectory*> |katalog źródłowy Hello, który zawiera pliki toobe kopiowane toohello dysk docelowy. Upewnij się, że nazwa określonego katalogu tego hello ma pełne zamiast względną ścieżkę. |
| /dstdir: <*DestinationBlobVirtualDirectory*> |Hello ścieżka toohello wirtualny katalog docelowy na koncie magazynu Azure. Można toouse się, że nazwy kontenera prawidłowe po określeniu katalogi wirtualne docelowego hello lub obiektów blob. Należy pamiętać, że nazwy kontenerów muszą być małymi literami.  Ta nazwa kontenera musi być hello, co wprowadzony podczas tworzenia grupy ochrony zasad tworzenia kopii zapasowej. |

> [!NOTE]
> Plik dziennika jest tworzony w folderze WAImportExport hello, który przechwytuje informacje całego hello hello przepływu pracy. Należy korzystać z tego pliku podczas tworzenia zadania importu w hello portalu Azure.
>
>

  ![Dane wyjściowe programu PowerShell](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Utwórz zadania importu w hello portalu Azure
1. Przejdź tooyour konta magazynu w hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **importu/eksportu**, a następnie **Tworzenie zadania importu** w okienku zadań hello.

    ![Karta importu/eksportu w hello portalu Azure](./media/backup-azure-backup-import-export/azureportal.png)

2. W kroku 1 Kreatora hello wskazują przygotowaniu dysku i że masz dostępny plik dziennika dysku hello.

3. W kroku 2 hello kreatora podaj informacje kontaktowe osoby hello, kto jest odpowiedzialny za tego zadania importu.

4. W kroku 3 należy przekazać pliki dziennika na dysku hello uzyskane w poprzedniej sekcji hello.

5. W kroku 4 wprowadź nazwę opisową dla zadania importu hello wprowadzonej podczas tworzenia grupy ochrony zasad tworzenia kopii zapasowej. Wprowadzona nazwa Hello może zawierać tylko małe litery, cyfry, łączniki i podkreślenia, musi zaczynać się literą i nie może zawierać spacji. Witaj nazwy jest używane tootrack zadań, a w toku, a po ich wykonaniu.

6. Następnie wybierz region centrum danych z listy hello. Hello datacenter region wskazuje hello centrum danych i adres toowhich muszą dostarczać pakietu.

    ![Wybierz region, w centrum danych](./media/backup-azure-backup-import-export/dc.png)

7. W kroku 5 wybierz z listy hello zwracany operatora, a następnie wprowadź numer swojego konta operatora. Firma Microsoft korzysta z tego konta tooship dysków z powrotem tooyou po zakończeniu zadania importu.

8. Wyślij hello dysku, a następnie wprowadź hello stan hello tootrack numeru wydania hello śledzenia. Po odebraniu dysku hello w centrum danych hello jest kopiowany toohello konta magazynu, a hello stan zostanie zaktualizowany.

    ![Stan zakończenia](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>Hello ukończenia przepływu pracy
Po danych początkowej kopii zapasowej hello jest dostępny na koncie magazynu hello agenta usług odzyskiwania Microsoft Azure kopiuje zawartość hello hello danych tego magazynu kopii zapasowych toohello konta lub magazyn usług odzyskiwania, którekolwiek ma zastosowanie. W hello kolejny harmonogram wykonywania kopii zapasowej, hello agenta kopii zapasowej Azure wykonuje hello przyrostowej kopii zapasowej za pośrednictwem hello początkowej kopii zapasowej.

## <a name="next-steps"></a>Następne kroki
* Wszelkie pytania w przepływie pracy Import/Eksport Azure hello odwoływać się za[Użyj hello Import/Eksport Microsoft Azure service tootransfer tooBlob pamięci masowej](../storage/common/storage-import-export-service.md).
* Zobacz sekcję kopia zapasowa offline toohello hello Azure Backup [— często zadawane pytania](backup-azure-backup-faq.md) dla odpowiedzi na pytania dotyczące hello przepływu pracy.
