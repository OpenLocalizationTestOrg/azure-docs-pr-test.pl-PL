---
title: Ochrona serwera kopii zapasowej aaaDPM/Azure tooAzure farmy programu SharePoint | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera omówienie ochrony serwera kopii zapasowej platformy Azure i programu DPM tooAzure farmy programu SharePoint"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 726d59320b8d9f14b38e0f041308019eebcfb77b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Wykonaj kopię zapasową tooAzure farmy programu SharePoint
Utworzono kopię zapasową programu SharePoint farmy przy użyciu System Center Data Protection Manager (DPM) w znacznie hello tooMicrosoft Azure tak samo kopii zapasowej innych źródeł danych. Kopia zapasowa Azure zapewnia elastyczność w toocreate harmonogram tworzenia kopii zapasowych hello punktów kopii zapasowej codziennie, co tydzień, miesięcznego lub rocznego i udostępnia opcje zasad przechowywania dla różnych punktów kopii zapasowej. Program DPM zapewnia kopii dysku lokalnego toostore możliwości hello szybka celami czasu odzyskiwania (RTO) i toostore kopiuje tooAzure dla ekonomiczny, długoterminowego przechowywania.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Obsługiwane wersje programu SharePoint, a powiązane scenariusze ochrony
Kopia zapasowa Azure dla programu DPM obsługuje hello następujące scenariusze:

| Obciążenie | Wersja | Wdrażanie SharePoint | Typ wdrożenia programu DPM | Program DPM — System Center 2012 R2 | Ochrona i odzyskiwanie |
| --- | --- | --- | --- | --- | --- |
| Sharepoint |SharePoint 2013, SharePoint programu SharePoint 2010, SharePoint 2007 3.0 |SharePoint wdrożony jako serwer fizyczny lub maszyny wirtualnej funkcji Hyper-V/VMware <br> -------------- <br> Funkcji SQL AlwaysOn |Serwera lub lokalnym funkcji Hyper-V virtual komputera fizycznego |Obsługuje tooAzure kopii zapasowej z pakietem zbiorczym aktualizacji 5 |Ochrona opcje odzyskiwania farmy programu SharePoint: farmy odzyskiwania bazy danych i plik lub element listy z punktów odzyskiwania dysku.  Odzyskiwania farmy i bazy danych z punktów odzyskiwania systemu Azure. |

## <a name="before-you-start"></a>Przed rozpoczęciem
Istnieje kilka sposobów niezbędne tooconfirm kopii zapasowej tooAzure farmy programu SharePoint.

### <a name="prerequisites"></a>Wymagania wstępne
Przed kontynuowaniem upewnij się, że spełniono wszystkie hello [wymagań wstępnych dotyczących używania kopia zapasowa Microsoft Azure](backup-azure-dpm-introduction.md#prerequisites) tooprotect obciążeń. Niektóre zadania wymagania wstępne, między innymi: Utwórz magazyn kopii zapasowych, Pobierz poświadczenia magazynu, zainstalować agenta kopii zapasowej Azure i Zarejestruj serwer kopii zapasowej platformy Azure i programu DPM w magazynie hello.

### <a name="dpm-agent"></a>Agent programu DPM
musi być zainstalowany Hello DPM agent na serwerze hello, z programem SharePoint, hello serwerów z systemem programu SQL Server i wszystkich serwerów, które są częścią farmy programu SharePoint hello. Aby uzyskać więcej informacji o tym, jak tooset hello agenta ochrony, zobacz [instalacji agenta ochrony](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Jedynym wyjątkiem Hello jest, należy zainstalować agenta hello tylko na jednym serwerze sieci web frontonu (WFE). Program DPM wymaga agenta hello na jeden tooserve tylko serwer WFE jako punkt wejścia hello do ochrony.

### <a name="sharepoint-farm"></a>Farma programu SharePoint
Dla każdych 10 milionów elementów w farmie hello musi istnieć co najmniej 2 GB miejsca w woluminie hello, w którym znajduje się folder programu DPM hello. Ta przestrzeń jest wymagany do generowania katalogu. Dla programu DPM toorecover określone elementy (zbiory witryn, witryn listy, biblioteki dokumentów, foldery, pojedyncze dokumenty i elementy listy) generowania katalogu tworzy listę adresów URL hello, które są zawarte w każdej bazie danych zawartości. Witaj listę adresów URL można wyświetlić w okienku elementy możliwe do odzyskania hello hello **odzyskiwania** zadań konsoli administratora programu DPM.

### <a name="sql-server"></a>Oprogramowanie SQL Server
Program DPM działa jako konto systemu lokalnego. tooback zapasową baz danych programu SQL Server, program DPM wymaga uprawnień administratora na tym koncie hello serwerze, na którym działa program SQL Server. Ustaw NT AUTHORITY\SYSTEM zbyt*sysadmin* na serwerze hello, na którym działa program SQL Server przed jego kopię zapasową.

Jeśli hello farmy programu SharePoint zawiera bazy danych programu SQL Server, które skonfigurowano z aliasami programu SQL Server, należy zainstalować składniki klienta programu SQL Server hello na powitania serwerze frontonu sieci Web chroniącym programu DPM.

### <a name="sharepoint-server"></a>Oprogramowanie SharePoint Server
Gdy wydajność zależy od wielu czynników, takich jak rozmiar farmy programu SharePoint, stanowią ogólne wskazówki jeden serwer programu DPM może chronić farmy programu SharePoint 25 TB.

### <a name="dpm-update-rollup-5"></a>Program DPM pakiet zbiorczy aktualizacji 5
Ochrona toobegin tooAzure farmy programu SharePoint, należy tooinstall pakiet zbiorczy aktualizacji programu DPM 5 lub nowszym. Pakiet zbiorczy aktualizacji 5 zawiera hello możliwości tooprotect tooAzure farmy programu SharePoint Jeśli farma hello jest skonfigurowana przy użyciu funkcji SQL AlwaysOn.
Aby uzyskać więcej informacji, zobacz wpis w blogu wprowadzającej hello [pakiet zbiorczy aktualizacji programu DPM 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)

### <a name="whats-not-supported"></a>Jakie operacje nie są obsługiwane
* Program DPM, który zapewnia ochronę farmy programu SharePoint nie chroni indeksy wyszukiwania lub bazy danych aplikacji usługi. Konieczne będzie tooconfigure hello ochrony tych baz danych oddzielnie.
* Program DPM nie ma kopii zapasowej baz danych serwera SQL programu SharePoint, które znajdują się udziałach plików skalowalnego w poziomie serwera (SOFS).

## <a name="configure-sharepoint-protection"></a>Konfigurowanie ochrony programu SharePoint
Przed użyciem programu DPM tooprotect programu SharePoint, należy skonfigurować usługę składnika zapisywania usługi VSS programu SharePoint hello (usługa składnika zapisywania programu WSS) przy użyciu **ConfigureSharePoint.exe**.

Można znaleźć **ConfigureSharePoint.exe** w folderze \bin hello [ścieżka instalacji programu DPM] na powitania serwera frontonu sieci web. To narzędzie umożliwia hello agenta ochrony za pomocą poświadczeń hello hello farmy programu SharePoint. Możesz uruchomić na jednym serwerze WFE. Jeśli masz wiele serwerów WFE, należy wybrać jeden z nich podczas konfigurowania grupy ochrony.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>Witaj tooconfigure usługi składnika zapisywania usługi VSS programu SharePoint
1. Na serwerze WFE hello, w wierszu polecenia przejdź zbyt \bin\ [Lokalizacja instalacji programu DPM]
2. Wprowadź ConfigureSharePoint - EnableSharePointProtection.
3. Wprowadź poświadczenia administratora farmy hello. To konto powinno być członkiem hello lokalnej grupy administratorów na serwerze WFE hello. Jeśli administrator farmy hello nie hello grant administratora lokalnego, następujących uprawnień na serwerze WFE hello:
   * Udziel hello WSS_ADMIN_WPG uprawnienia pełnej kontroli toohello DPM folderu grupy (% Program Files%\Microsoft Data Protection Manager\DPM).
   * Przyznać dostęp do odczytu grupie WSS_ADMIN_WPG uprawnienia hello toohello klucza rejestru programu DPM (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Gdy istnieje zmiana poświadczeń administratora farmy programu SharePoint hello należy toorerun ConfigureSharePoint.exe.
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a>Tworzenie kopii zapasowej farmy programu SharePoint za pomocą programu DPM
Po skonfigurowaniu programu DPM i hello farmy programu SharePoint, jak opisano wcześniej, SharePoint mogą być chronione przez program DPM.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect farmy programu SharePoint
1. Z hello **ochrony** kartę hello konsoli administratora programu DPM, kliknij przycisk **nowy**.
    ![Nowa karta ochrony](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. Na powitania **wybierz typ grupy ochrony** strony hello **tworzenia nowej grupy ochrony** kreatora, zaznacz **serwerów**, a następnie kliknij przycisk **dalej** .
   
    ![Wybierz grupę ochrony typu](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. Na powitania **Wybierz członków grupy** ekranu, hello zaznacz pole wyboru dla hello programu SharePoint server tooprotect i kliknij **dalej**.
   
    ![Wybierz członków grupy](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > Z zainstalowanym agentem DPM hello widać serwera powitania w Kreatorze hello. Program DPM wyświetla również jego struktury. Ponieważ uruchomiono ConfigureSharePoint.exe, program DPM komunikuje się z hello usługi składnika zapisywania usługi VSS programu SharePoint i jego odpowiednie baz danych programu SQL Server i rozpoznaje struktura farmy programu SharePoint hello, hello skojarzonych baz danych zawartości, a wszelkie odpowiednie elementy.
   > 
   > 
4. Na powitania **wybierz metodę ochrony danych** strony, wprowadź nazwę hello hello **grupy ochrony**i wybierz preferowany *metody ochrony*. Kliknij przycisk **Dalej**.
   
    ![Wybierz metodę ochrony danych](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > Metoda ochrony dysku Hello pomaga toomeet krótki czas odzyskiwania celów. Platforma Azure jest tootapes docelowej porównaniu ekonomiczny, długoterminowej ochrony. Aby uzyskać więcej informacji, zobacz [tooreplace kopia zapasowa Azure użycie infrastruktury taśmy](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)
   > 
   > 
5. Na powitania **Określ cele krótkoterminowe** wybierz preferowany **zakres przechowywania** i ustalić, kiedy chcesz toooccur kopii zapasowych.
   
    ![Określanie celów krótkoterminowych](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > Ponieważ odzyskiwania najczęściej jest wymagana dla danych, która jest mniejsza niż pięć dni, możemy wybrany zakres przechowywania 5 dni na dysku i zapewnić, że możliwość tworzenia kopii zapasowych hello odbywa się podczas nieprodukcyjnych godzin, w tym przykładzie.
   > 
   > 
6. Przejrzyj hello dysku miejsca w puli magazynu przydzielone hello grupie ochrony, a następnie kliknij przycisk **dalej**.
7. Dla każdej grupy ochrony program DPM przydziela toostore miejsca na dysku i zarządzanie replik. W tym momencie Program DPM musi utworzyć kopii danych hello wybrane. Wybierz, jak i kiedy chcesz utworzyć replikę hello, a następnie kliknij przycisk **dalej**.
   
    ![Wybierz metodę tworzenia repliki](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > toomake się upewnić, że nie odbywa się ruch sieciowy, wybierz godzinę poza godzinami produkcji.
   > 
   > 
8. Program DPM zapewnia integralność danych poprzez przeprowadzenie sprawdzania spójności w replice hello. Dostępne są dwie opcje dostępne. Można zdefiniować sprawdzania spójności toorun harmonogramu lub programu DPM można uruchomić sprawdzania spójności automatycznie w replice hello zawsze, gdy stanie się niespójna. Wybierz preferowaną opcję, a następnie kliknij przycisk **dalej**.
   
    ![Sprawdzanie spójności](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. Na powitania **Określ dane chronione Online** hello farmy programu SharePoint mają tooprotect, a następnie kliknij przycisk Wybierz **dalej**.
   
    ![Program DPM Protection1 programu SharePoint](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. Na powitania **Określanie harmonogramu tworzenia kopii zapasowej Online** , wybierz preferowany harmonogram, a następnie kliknij przycisk **dalej**.
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > Program DPM udostępnia maksymalnie dwóch tooAzure codzienne kopie zapasowe w różnym czasie. Kopia zapasowa Azure można również sterować hello ilość przepustowości sieci WAN, który może służyć do przechowywania kopii zapasowych w szczycie i poza godzinami pracy przy użyciu [ograniczania sieci kopia zapasowa Azure](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).
    > 
    > 
11. W zależności od hello harmonogram tworzenia kopii zapasowych, która została wybrana na powitania **Określanie zasad przechowywania Online** strony, wybierz hello zasad przechowywania dla punktów kopii zapasowej codziennie, co tydzień, miesięcznych i rocznych.
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > Program DPM używa schemat przechowywania dziadek ojciec syn., w którym można wybrać zasady przechowywania różne dla różnych punktów kopii zapasowej.
    > 
    > 
12. Podobne toodisk repliki punktu początkowego odwołanie musi toobe utworzona na platformie Azure. Wybierz toocreate Twojego preferowaną opcję tooAzure początkowej kopii zapasowej, a następnie kliknij przycisk **dalej**.
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Przejrzyj wybrane ustawienia na powitania **Podsumowanie** , a następnie kliknij przycisk **Utwórz grupę**. Po utworzeniu grupy ochrony hello, zobaczą komunikat z potwierdzeniem.
    
    ![Podsumowanie](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a>Przywróć element programu SharePoint z dysku za pomocą programu DPM
W hello poniższy przykład, hello *element odzyskiwanie programu SharePoint* został przypadkowo usunięty i musi toobe odzyskane.
![Program DPM Protection4 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Otwórz hello **konsoli administratora programu DPM**. Wszystkie farmy programu SharePoint, które są chronione przez program DPM są wyświetlane w hello **ochrony** kartę.
   
    ![Program DPM Protection3 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. Element hello toorecover toobegin, wybierz hello **odzyskiwania** kartę.
   
    ![Program DPM Protection5 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. Umożliwia wyszukiwanie programu SharePoint dla *element odzyskiwanie programu SharePoint* przy użyciu symboli wieloznacznych na podstawie wyszukiwania w ramach odzyskiwania punktu zakresu.
   
    ![Program DPM Protection6 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Wybierz punkt odzyskiwania odpowiednią hello z hello wyniki wyszukiwania, kliknij prawym przyciskiem myszy element hello, a następnie wybierz **odzyskać**.
5. Można również przejrzeć różnych punktów odzyskiwania i wybierz toorecover bazy danych lub elementów. Wybierz **Data > czasu odzyskiwania**, a następnie wybierz poprawny hello **bazy danych > farmy programu SharePoint > punktu odzyskiwania > elementu**.
   
    ![Program DPM Protection7 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Kliknij prawym przyciskiem myszy element hello, a następnie wybierz **odzyskać** tooopen hello **Kreatora odzyskiwania**. Kliknij przycisk **Dalej**.
   
    ![Przegląd wybranego elementu odzyskiwania](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Wybierz typ odzyskiwania mają tooperform, a następnie kliknij przycisk hello **dalej**.
   
    ![Typ odzyskiwania](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > Witaj wybór **odzyskać toooriginal** w hello przykład odzyskuje hello elementu toohello oryginalnej witryny programu SharePoint.
   > 
   > 
8. Wybierz hello **proces odzyskiwania** , które mają toouse.
   
   * Wybierz **odzyskać bez używania farmy odzyskiwania** Jeśli hello farmy programu SharePoint nie został zmieniony i hello identyczny odzyskiwania hello punkt będący jest przywracana.
   * Wybierz **odzyskać za pomocą farmy odzyskiwania** Jeśli hello farmy programu SharePoint uległ zmianie od czasu utworzenia punktu odzyskiwania hello.
     
     ![Proces odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Dostarczenie przemieszczania wystąpienia lokalizacji toorecover hello bazy danych SQL Server i podaj przemieszczania udziału plików na serwerze programu DPM hello i hello działającej element hello toorecover programu SharePoint.
   
    ![Location1 przemieszczania](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    Program DPM dołącza bazy danych zawartości hello, który jest hostem hello SharePoint elementu toohello tymczasowego wystąpienia programu SQL Server. Z bazy danych zawartości hello serwer DPM hello odzyskuje elementu hello i umieszcza je na powitania tymczasowej lokalizacji pliku na serwerze DPM hello. Witaj odzyskiwanego elementu, znajdującego się na powitania teraz tymczasowej lokalizacji serwera programu DPM hello musi toohello toobe wyeksportowane tymczasowej lokalizacji na powitania farmy programu SharePoint.
   
    ![Location2 przemieszczania](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Wybierz **Określ opcje odzyskiwania**i zastosować toohello ustawień zabezpieczeń farmy programu SharePoint lub Zastosuj ustawienia zabezpieczeń hello hello punktu odzyskiwania. Kliknij przycisk **Dalej**.
    
    ![Opcje odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > Możesz wybrać toothrottle hello przepustowości. Pozwala to zmniejszyć wpływ toohello produkcji serwera poza godzinami produkcji.
    > 
    > 
11. Przejrzyj podsumowanie hello, a następnie kliknij przycisk **odzyskać** odzyskiwania toobegin hello pliku.
    
    ![Podsumowanie odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Teraz wybierz hello **monitorowanie** kartę w hello **konsoli administratora programu DPM** tooview hello **stan** hello odzyskiwania.
    
    ![Stan odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > Plik Hello jest przywrócone. Można odświeżać hello SharePoint lokacji toocheck hello przywrócić pliku.
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Przywróć bazę danych programu SharePoint z platformy Azure za pomocą programu DPM
1. toorecover bazę danych programu SharePoint, przejdź przez różne punkty odzyskiwania (jak pokazano wcześniej) i wybierz hello punkt odzyskiwania, które mają toorestore.
   
    ![Program DPM Protection8 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Kliknij dwukrotnie hello SharePoint odzyskiwania tooshow punktu hello dostępne SharePoint informacji o katalogu.
   
   > [!NOTE]
   > Ponieważ hello farmy programu SharePoint jest chroniony w celu przechowywania długoterminowego na platformie Azure, informacje katalogu (metadanych) są niedostępne na powitania serwera DPM. W związku z tym zawsze, gdy baza danych zawartości programu SharePoint w momencie musi toobe odzyskane, należy farmy programu SharePoint hello toocatalog ponownie.
   > 
   > 
3. Kliknij przycisk **ponownego katalogowania**.
   
    ![Program DPM Protection10 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    Witaj **ponownie skatalogować chmury** otwiera się okno stanu.
   
    ![Program DPM Protection11 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    Po zakończeniu skatalogowania hello stan zmienia się zbyt*Powodzenie*. Kliknij przycisk **Zamknij**.
   
    ![Program DPM Protection12 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Kliknij obiekt SharePoint hello pokazano hello DPM **odzyskiwania** karcie tooget hello bazy danych zawartości struktury. Kliknij prawym przyciskiem myszy element hello, a następnie kliknij przycisk **odzyskać**.
   
    ![Program DPM Protection13 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. W tym momencie wykonać hello [opisane w tym artykule](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover bazy danych zawartości programu SharePoint z dysku.

## <a name="faqs"></a>Często zadawane pytania
Pytanie: które wersje programu DPM obsługuje program SQL Server 2014 i SQL 2012 (SP2)?<br>
Odpowiedź: DPM 2012 R2 z pakietem zbiorczym aktualizacji w wersji 4 obsługuje zarówno.

Pytanie: czy SharePoint lokalizacji oryginalnego elementu toohello można odzyskać skonfigurowanie programu SharePoint przy użyciu funkcji SQL AlwaysOn (Ochrona na dysku)?<br>
A: tak hello elementu może być odzyskane toohello oryginalnej witryny programu SharePoint.

Pytanie: czy oryginalnej lokalizacji toohello bazy danych programu SharePoint można odzyskać Jeśli programu SharePoint została skonfigurowana przy użyciu funkcji SQL AlwaysOn?<br>
Odpowiedź: ponieważ baz danych programu SharePoint są konfigurowane w funkcji SQL AlwaysOn, nie można modyfikować, chyba że zostanie usunięta grupa dostępności hello. W związku z tym program DPM nie można przywrócić oryginalnej lokalizacji toohello bazy danych. Wystąpienie programu SQL Server tooanother bazy danych programu SQL Server można odzyskać.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej na temat ochrony programu DPM programu SharePoint — zobacz [wideo serii — Program DPM ochronę programu SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
* Przegląd [informacje o wersji programu System Center 2012 — Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)
* Przegląd [informacje o wersji programu Data Protection Manager w programie System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)

