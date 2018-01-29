---
title: Kopii zapasowej platformy Azure i programu DPM w celu ochrony farmy programu SharePoint do platformy Azure | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera omówienie kopii zapasowej platformy Azure i programu DPM w celu ochrony farmy programu SharePoint do platformy Azure"
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
ms.openlocfilehash: 1bbf3233169fa9966e3dd0fac18ee448f26caa6b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a>Tworzenie kopii zapasowych farmy programu SharePoint na platformie Azure
Kopię zapasową można farmy programu SharePoint do systemu Microsoft Azure przy użyciu System Center Data Protection Manager (DPM) w znacznie tak samo jak wykonanie kopii zapasowej innych źródeł danych. Kopia zapasowa Azure zapewnia elastyczność w harmonogram tworzenia kopii zapasowych, aby utworzyć codziennie, co tydzień, miesięcznego lub rocznego kopii zapasowej wskazuje i udostępnia opcje zasad przechowywania dla różnych punktów kopii zapasowej. Program DPM udostępnia możliwość przechowywania kopii dysku lokalnym dla szybka celami czasu odzyskiwania (RTO) i Zapisz kopie Azure ekonomiczny, długoterminowego przechowywania.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Obsługiwane wersje programu SharePoint, a powiązane scenariusze ochrony
Kopia zapasowa Azure dla programu DPM obsługuje następujące scenariusze:

| Obciążenie | Wersja | Wdrażanie SharePoint | Typ wdrożenia programu DPM | Program DPM — System Center 2012 R2 | Ochrona i odzyskiwanie |
| --- | --- | --- | --- | --- | --- |
| Sharepoint |SharePoint 2013, SharePoint programu SharePoint 2010, SharePoint 2007 3.0 |SharePoint wdrożony jako serwer fizyczny lub maszyny wirtualnej funkcji Hyper-V/VMware <br> -------------- <br> Funkcji SQL AlwaysOn |Serwera lub lokalnym funkcji Hyper-V virtual komputera fizycznego |Obsługa tworzenia kopii zapasowej Azure z pakietem zbiorczym aktualizacji 5 |Ochrona opcje odzyskiwania farmy programu SharePoint: farmy odzyskiwania bazy danych i plik lub element listy z punktów odzyskiwania dysku.  Odzyskiwania farmy i bazy danych z punktów odzyskiwania systemu Azure. |

## <a name="before-you-start"></a>Przed rozpoczęciem
Istnieje kilka rzeczy, które trzeba upewnić się, aby wykonać kopię zapasową farmy programu SharePoint do platformy Azure.

### <a name="prerequisites"></a>Wymagania wstępne
Przed kontynuowaniem upewnij się, że zostały spełnione wszystkie [wymagań wstępnych dotyczących używania kopia zapasowa Microsoft Azure](backup-azure-dpm-introduction.md#prerequisites) ochrony obciążeń. Niektóre zadania wymagania wstępne, między innymi: Utwórz magazyn kopii zapasowych, pobrać poświadczenia magazynu, zainstalować agenta kopii zapasowej Azure i Zarejestruj serwer kopii zapasowej platformy Azure i programu DPM w magazynie.

### <a name="dpm-agent"></a>Agent programu DPM
Musi być zainstalowany agent programu DPM na serwerze, który jest uruchomiony, SharePoint, serwery z programem SQL Server i wszystkich serwerów, które należą do farmy programu SharePoint. Aby uzyskać więcej informacji na temat sposobu konfigurowania agenta ochrony, zobacz [instalacji agenta ochrony](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Jedynym wyjątkiem jest, zainstaluj agenta tylko na jednym serwerze sieci web frontonu (WFE). Program DPM wymaga agenta na jednym serwerze WFE tylko służy jako punkt wejścia do ochrony.

### <a name="sharepoint-farm"></a>Farma programu SharePoint
Dla każdych 10 milionów elementów w farmie musi istnieć co najmniej 2 GB miejsca na woluminie, w którym znajduje się folder programu DPM. Ta przestrzeń jest wymagany do generowania katalogu. Programu DPM odzyskać określone elementy (zbiory witryn, witryn listy, biblioteki dokumentów, foldery, pojedyncze dokumenty i elementy listy) generowania katalogu tworzy listę adresów URL, które są zawarte w każdej bazie danych zawartości. Można wyświetlić listę adresów URL w okienku elementy możliwe do odzyskania w **odzyskiwania** zadań konsoli administratora programu DPM.

### <a name="sql-server"></a>Oprogramowanie SQL Server
Program DPM działa jako konto systemu lokalnego. Aby utworzyć kopię zapasową bazy danych programu SQL Server, program DPM wymaga uprawnień administratora na tym koncie dla serwera, na którym działa program SQL Server. Ustaw Zarządzanie NT\System *sysadmin* na serwerze, na którym działa program SQL Server przed jego kopię zapasową.

Jeśli farma programu SharePoint zawiera bazy danych programu SQL Server, które skonfigurowano z aliasami programu SQL Server, należy zainstalować składniki klienta programu SQL Server na serwerze frontonu sieci Web, które będzie chronione przez program DPM.

### <a name="sharepoint-server"></a>Oprogramowanie SharePoint Server
Gdy wydajność zależy od wielu czynników, takich jak rozmiar farmy programu SharePoint, stanowią ogólne wskazówki jeden serwer programu DPM może chronić farmy programu SharePoint 25 TB.

### <a name="dpm-update-rollup-5"></a>Program DPM pakiet zbiorczy aktualizacji 5
Aby rozpocząć ochronę farmy programu SharePoint do platformy Azure, musisz zainstalować pakiet zbiorczy aktualizacji programu DPM 5 lub nowszy. Pakiet zbiorczy aktualizacji 5 zapewnia możliwość ochrony farmy programu SharePoint do platformy Azure, jeśli farmy jest konfigurowana przy użyciu funkcji SQL AlwaysOn.
Aby uzyskać więcej informacji znajduje się we wpisie post wprowadzającej [pakiet zbiorczy aktualizacji programu DPM 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)

### <a name="whats-not-supported"></a>Jakie operacje nie są obsługiwane
* Program DPM, który zapewnia ochronę farmy programu SharePoint nie chroni indeksy wyszukiwania lub bazy danych aplikacji usługi. Należy skonfigurować osobno ochrony tych baz danych.
* Program DPM nie ma kopii zapasowej baz danych serwera SQL programu SharePoint, które znajdują się udziałach plików skalowalnego w poziomie serwera (SOFS).

## <a name="configure-sharepoint-protection"></a>Konfigurowanie ochrony programu SharePoint
Przed użyciem programu DPM do ochrony programu SharePoint należy skonfigurować usługę składnika zapisywania usługi VSS programu SharePoint (usługa składnika zapisywania programu WSS) przy użyciu **ConfigureSharePoint.exe**.

Można znaleźć **ConfigureSharePoint.exe** w folderze \bin [ścieżka instalacji programu DPM] na serwerze frontonu sieci web. To narzędzie udostępnia agentowi ochrony poświadczenia farmy programu SharePoint. Możesz uruchomić na jednym serwerze WFE. Jeśli masz wiele serwerów WFE, należy wybrać jeden z nich podczas konfigurowania grupy ochrony.

### <a name="to-configure-the-sharepoint-vss-writer-service"></a>Aby skonfigurować usługę składnika zapisywania usługi VSS programu SharePoint
1. Na serwerze WFE, w wierszu polecenia przejdź do \bin\ [Lokalizacja instalacji programu DPM]
2. Wprowadź ConfigureSharePoint - EnableSharePointProtection.
3. Wprowadź poświadczenia administratora farmy. To konto powinno być członkiem lokalnej grupy administratorów na serwerze WFE. Jeśli administrator farmy nie jest lokalnym administratorem Przyznaj poniższe uprawnienia na serwerze WFE:
   * Przyznaj grupie WSS_ADMIN_WPG uprawnienia Pełna kontrola do folderu programu DPM (% Program Files%\Microsoft Data Protection Manager\DPM).
   * Przyznaj grupie WSS_ADMIN_WPG uprawnienia odczytu do klucza rejestru programu DPM (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Musisz ponownie uruchomić ConfigureSharePoint.exe, gdy istnieje zmiana poświadczeń administratora farmy programu SharePoint.
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a>Tworzenie kopii zapasowej farmy programu SharePoint za pomocą programu DPM
Po skonfigurowaniu programu DPM i farmy programu SharePoint, jak opisano wcześniej, SharePoint mogą być chronione przez program DPM.

### <a name="to-protect-a-sharepoint-farm"></a>Aby chronić farmy programu SharePoint
1. Z **ochrony** kartę konsoli administratora programu DPM, kliknij przycisk **nowy**.
    ![Nowa karta ochrony](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. Na **wybierz typ grupy ochrony** strony **tworzenia nowej grupy ochrony** kreatora, zaznacz **serwerów**, a następnie kliknij przycisk **dalej**.
   
    ![Wybierz grupę ochrony typu](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. Na **Wybierz członków grupy** ekranu, zaznacz pole wyboru dla serwera programu SharePoint chcesz chronić, a następnie kliknij przycisk **dalej**.
   
    ![Wybierz członków grupy](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > Używając zainstalowany agent programu DPM można zobaczyć serwer w kreatorze. Program DPM wyświetla również jego struktury. Ponieważ uruchomiono ConfigureSharePoint.exe, program DPM komunikuje się z usługą składnik zapisywania usługi VSS programu SharePoint i jego odpowiednie baz danych programu SQL Server i rozpoznaje struktury farmy programu SharePoint i skojarzonych baz danych zawartości oraz wszystkie odpowiednie elementy.
   > 
   > 
4. Na **wybierz metodę ochrony danych** strony, wprowadź nazwę **grupy ochrony**i wybierz preferowany *metody ochrony*. Kliknij przycisk **Dalej**.
   
    ![Wybierz metodę ochrony danych](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > Metoda ochrony dysku pozwala osiąganie celów czasu odzyskiwania krótki. Platforma Azure jest obiekt docelowy ekonomiczny, długoterminowej ochrony w porównaniu do taśmy. Aby uzyskać więcej informacji, zobacz [kopia zapasowa Azure używany do zastąpienia infrastruktury taśm](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)
   > 
   > 
5. Na **Określ cele krótkoterminowe** wybierz preferowany **zakres przechowywania** i ustalić, kiedy chcesz, aby tworzenie kopii zapasowej.
   
    ![Określanie celów krótkoterminowych](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > Ponieważ odzyskiwania najczęściej jest wymagana dla danych, która jest mniejsza niż pięć dni, możemy wybrany zakres przechowywania 5 dni na dysku i zapewnić, że tworzenie kopii zapasowej odbywa się podczas nieprodukcyjnych godzin, w tym przykładzie.
   > 
   > 
6. Przejrzyj miejsce przydzielone do grupy ochrony na dysku puli magazynów, a następnie kliknij przycisk **dalej**.
7. Dla każdej grupy ochrony program DPM przydziela miejsce na dysku do przechowywania replik. W tym momencie Program DPM musi utworzyć kopię wybranych danych. Wybierz, jak i kiedy chcesz utworzyć replikę, a następnie kliknij przycisk **dalej**.
   
    ![Wybierz metodę tworzenia repliki](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > Aby upewnić się, że ruch sieciowy nie jest wykonywane, wybierz godzinę poza godzinami produkcji.
   > 
   > 
8. Program DPM zapewnia integralność danych poprzez przeprowadzenie sprawdzania spójności w replice. Dostępne są dwie opcje dostępne. Można zdefiniować harmonogram wykonywania sprawdzania spójności lub programu DPM można uruchomić sprawdzania spójności automatycznie w replice zawsze, gdy stanie się niespójna. Wybierz preferowaną opcję, a następnie kliknij przycisk **dalej**.
   
    ![Sprawdzanie spójności](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. Na **Określ dane chronione Online** farmy programu SharePoint, które chcesz chronić, a następnie kliknij przycisk Wybierz **dalej**.
   
    ![Program DPM Protection1 programu SharePoint](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. Na **Określanie harmonogramu tworzenia kopii zapasowej Online** , wybierz preferowany harmonogram, a następnie kliknij przycisk **dalej**.
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > Program DPM udostępnia maksymalnie dwóch kopii zapasowych codziennie na platformie Azure w różnym czasie. Kopia zapasowa Azure można również sterować ilość przepustowości sieci WAN, który może służyć do przechowywania kopii zapasowych w szczycie i poza godzinami pracy przy użyciu [ograniczania sieci kopia zapasowa Azure](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling).
    > 
    > 
11. W zależności od harmonogram tworzenia kopii zapasowych, zostanie wybrany na **Określanie zasad przechowywania Online** wybierz zasady przechowywania dla punktów kopii zapasowej codziennie, co tydzień, miesięcznych i rocznych.
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > Program DPM używa schemat przechowywania dziadek ojciec syn., w którym można wybrać zasady przechowywania różne dla różnych punktów kopii zapasowej.
    > 
    > 
12. Podobnie jak dysk, replika punktu początkowego odwołanie musi zostać utworzona na platformie Azure. Wybierz preferowaną opcję tworzenia początkowej kopii zapasowej na platformie Azure, a następnie kliknij przycisk **dalej**.
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Przejrzyj wybrane ustawienia na **Podsumowanie** , a następnie kliknij przycisk **Utwórz grupę**. Po utworzeniu grupy ochrony, zobaczą komunikat z potwierdzeniem.
    
    ![Podsumowanie](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a>Przywróć element programu SharePoint z dysku za pomocą programu DPM
W poniższym przykładzie *element odzyskiwanie programu SharePoint* został przypadkowo usunięty i mają zostać odzyskane.
![Program DPM Protection4 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Otwórz **konsoli administratora programu DPM**. Wszystkie farmy programu SharePoint, które są chronione przez program DPM są wyświetlane w **ochrony** kartę.
   
    ![Program DPM Protection3 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. Aby rozpocząć odzyskać element, wybierz **odzyskiwania** kartę.
   
    ![Program DPM Protection5 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. Umożliwia wyszukiwanie programu SharePoint dla *element odzyskiwanie programu SharePoint* przy użyciu symboli wieloznacznych na podstawie wyszukiwania w ramach odzyskiwania punktu zakresu.
   
    ![Program DPM Protection6 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Wybierz punkt odzyskiwania odpowiednie w wynikach wyszukiwania, kliknij element prawym przyciskiem myszy, a następnie wybierz **odzyskać**.
5. Można również przejrzeć różnych punktów odzyskiwania i wybierz bazę danych lub element, aby odzyskać. Wybierz **Data > Godzina odzyskiwania**, a następnie wybierz poprawny **bazy danych > farmy programu SharePoint > punktu odzyskiwania > elementu**.
   
    ![Program DPM Protection7 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Kliknij element prawym przyciskiem myszy, a następnie wybierz **odzyskać** otworzyć **Kreatora odzyskiwania**. Kliknij przycisk **Dalej**.
   
    ![Przegląd wybranego elementu odzyskiwania](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Wybierz typ odzyskiwania, które chcesz przeprowadzić, a następnie kliknij przycisk **dalej**.
   
    ![Typ odzyskiwania](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > Wybór **Odzyskaj do oryginalnego** w przykładzie odzyskuje element do oryginalnej witryny programu SharePoint.
   > 
   > 
8. Wybierz **proces odzyskiwania** którego chcesz używać.
   
   * Wybierz **odzyskać bez używania farmy odzyskiwania** Jeśli farma programu SharePoint nie została zmieniona i jest taki sam jak punkt odzyskiwania, który jest przywracana.
   * Wybierz **odzyskać za pomocą farmy odzyskiwania** Jeśli farma SharePoint zmieniła się od czasu utworzenia punktu odzyskiwania.
     
     ![Proces odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Podaj tymczasowej lokalizacji wystąpienia programu SQL Server tymczasowo przywrócić bazę danych, a następnie podaj przemieszczania udziału plików na serwerze DPM i serwerze z programem SharePoint, aby odzyskać elementu.
   
    ![Location1 przemieszczania](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    Program DPM dołącza bazy danych zawartości, który jest hostem element programu SharePoint do tymczasowego wystąpienia programu SQL Server. Z bazy danych zawartości serwer programu DPM przywraca element i umieszcza je na tymczasowej lokalizacji pliku na serwerze programu DPM. Odzyskiwanego elementu, która jest teraz w tymczasowej lokalizacji serwera programu DPM musi zostać wyeksportowany do lokalizacji tymczasowej na farmie SharePoint.
   
    ![Location2 przemieszczania](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Wybierz **Określ opcje odzyskiwania**i stosuje ustawienia zabezpieczeń do farmy programu SharePoint lub Zastosuj ustawienia zabezpieczeń dla punktu odzyskiwania. Kliknij przycisk **Dalej**.
    
    ![Opcje odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > Istnieje możliwość ograniczania użycia przepustowości sieci. Pozwala to zmniejszyć wpływ na serwerze produkcyjnym poza godzinami produkcji.
    > 
    > 
11. Sprawdź informacje, a następnie kliknij przycisk **odzyskać** aby rozpocząć odzyskiwanie pliku.
    
    ![Podsumowanie odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Teraz wybierz **monitorowanie** karcie **konsoli administratora programu DPM** Aby wyświetlić **stan** odzyskiwania.
    
    ![Stan odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > Plik jest przywrócone. Można odświeżać Sprawdź przywróconych plików witryny programu SharePoint.
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Przywróć bazę danych programu SharePoint z platformy Azure za pomocą programu DPM
1. Aby odzyskać bazę danych zawartości programu SharePoint, przejdź przez różne punkty odzyskiwania (jak pokazano wcześniej), a następnie wybierz punkt odzyskiwania, który chcesz przywrócić.
   
    ![Program DPM Protection8 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Kliknij dwukrotnie punkt odzyskiwania SharePoint, aby wyświetlić dostępne informacje o katalogu programu SharePoint.
   
   > [!NOTE]
   > Ponieważ farmy programu SharePoint jest chroniony w celu przechowywania długoterminowego na platformie Azure, informacje katalogu (metadanych) są niedostępne na serwerze programu DPM. W związku z tym zawsze, gdy baza danych zawartości programu SharePoint w momencie mają zostać odzyskane, musisz ponownie w katalogu farmy programu SharePoint.
   > 
   > 
3. Kliknij przycisk **ponownego katalogowania**.
   
    ![Program DPM Protection10 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    **Ponownie skatalogować chmury** otwiera się okno stanu.
   
    ![Program DPM Protection11 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    Po zakończeniu skatalogowania stan zmienia się na *Powodzenie*. Kliknij przycisk **Zamknij**.
   
    ![Program DPM Protection12 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Kliknij obiekt SharePoint pokazano DPM **odzyskiwania** kartę, aby pobrać struktury bazy danych zawartości. Kliknij element prawym przyciskiem myszy, a następnie kliknij przycisk **odzyskać**.
   
    ![Program DPM Protection13 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. W tym momencie wykonać [opisane w tym artykule](#restore-a-sharepoint-item-from-disk-using-dpm) odzyskać bazę danych zawartości programu SharePoint z dysku.

## <a name="faqs"></a>Często zadawane pytania
Pytanie: które wersje programu DPM obsługuje program SQL Server 2014 i SQL 2012 (SP2)?<br>
Odpowiedź: DPM 2012 R2 z pakietem zbiorczym aktualizacji w wersji 4 obsługuje zarówno.

Pytanie: czy element programu SharePoint do oryginalnej lokalizacji można odzyskać skonfigurowanie programu SharePoint przy użyciu funkcji SQL AlwaysOn (Ochrona na dysku)?<br>
Odpowiedź: tak elementu można odzyskać do oryginalnej witryny programu SharePoint.

Pytanie: czy bazy danych programu SharePoint do oryginalnej lokalizacji można odzyskać Jeśli programu SharePoint została skonfigurowana przy użyciu funkcji SQL AlwaysOn?<br>
Odpowiedź: ponieważ baz danych programu SharePoint są konfigurowane w funkcji SQL AlwaysOn, nie można modyfikować, chyba że zostanie usunięta grupa dostępności. W związku z tym program DPM nie można przywrócić bazę danych do oryginalnej lokalizacji. Można odzyskać bazy danych programu SQL Server do innego wystąpienia programu SQL Server.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej na temat ochrony programu DPM programu SharePoint — zobacz [wideo serii — Program DPM ochronę programu SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
* Przegląd [informacje o wersji programu System Center 2012 — Data Protection Manager](https://technet.microsoft.com/library/jj860415.aspx)
* Przegląd [informacje o wersji programu Data Protection Manager w programie System Center 2012 SP1](https://technet.microsoft.com/library/jj860394.aspx)

