---
title: "kopii zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów aaaMonitor | Dokumentacja firmy Microsoft"
description: "Monitorowanie zdarzeń i alertów z kopii zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów. Wyślij wiadomość e-mail na podstawie alertów."
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a>Monitorowanie alertów związanych z kopiami zapasowymi maszyny wirtualnej platformy Azure
Alerty są odpowiedzi z usługi hello, że próg zdarzenia zostały spełnione lub przekroczenia. Uzyskiwanie informacji o tym, gdy rozpoczęcia problemów może być krytyczne tookeeping koszty biznesowych w dół. Alerty zwykle nie występują zgodnie z harmonogramem, a jest przydatne tooknow jak najszybciej po wystąpieniu alerty. Na przykład jeśli zadania tworzenia kopii zapasowej lub przywracania nie powiodło się, w ciągu pięciu minut hello błąd pojawia się alert. Na pulpicie nawigacyjnym magazynu hello powitalne Kafelek alerty kopii zapasowej Wyświetla zdarzeń krytycznych i poziom ostrzeżeń. W ustawieniach alerty kopii zapasowej hello można wyświetlić wszystkie zdarzenia. Ale co zrobić, jeśli alarm występuje, gdy pracujesz na oddzielnych problem? Jeśli nie znasz w przypadku alertu hello, może to być pomocnicza niedogodności lub może naruszyć bezpieczeństwo danych. Jeśli występuje on toomake czy osobom hello wiedzą alertu — skonfiguruj hello usługi toosend powiadomienia o alertach pocztą e-mail. Aby uzyskać więcej informacji na temat konfigurowania powiadomień e-mail, zobacz [skonfigurować powiadomienia](backup-azure-monitor-vms.md#configure-notifications).

## <a name="how-do-i-find-information-about-hello-alerts"></a>Jak znaleźć informacje o alertach hello?
tooview informacji o zdarzeniu hello, która wywołała alert, należy otworzyć hello blok alerty kopii zapasowej. Istnieją dwa sposoby tooopen hello blok alerty kopii zapasowej: z hello Kafelek alerty kopii zapasowej na pulpicie nawigacyjnym magazynu hello lub za pomocą bloku hello alertów i zdarzeń.

Kafelek blok alerty kopii zapasowej hello tooopen z kopii zapasowej alertów:

* Na powitania **alerty kopii zapasowej** kafelka na pulpicie nawigacyjnym magazynu hello, kliknij przycisk **krytyczny** lub **ostrzeżenie** tooview hello zdarzenia operacyjne dla tego poziomu ważności.

    ![Kafelek alerty kopii zapasowej](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

tooopen hello blok alerty kopii zapasowej za pomocą bloku hello alerty i zdarzenia:

1. Z pulpitem nawigacyjnym magazynu hello, kliknij przycisk **wszystkie ustawienia**. ![Przycisk wszystkie ustawienia](./media/backup-azure-monitor-vms/all-settings-button.png)
2. Na powitania **ustawienia** bloku, kliknij przycisk **alerty i zdarzenia**. ![Przycisk alertów i zdarzeń](./media/backup-azure-monitor-vms/alerts-and-events-button.png)
3. Na powitania **alerty i zdarzenia** bloku, kliknij przycisk **alerty kopii zapasowej**. ![Przycisk tworzenia kopii zapasowej alertów](./media/backup-azure-monitor-vms/backup-alerts.png)

    Witaj **alerty kopii zapasowej** zostanie otwarty blok i wyświetla hello filtrowane alerty.

    ![Kafelek alerty kopii zapasowej](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. tooview szczegółowe informacje dotyczące konkretnego alertu, z listy hello zdarzeń, kliknij przycisk tooopen alertu hello jego **szczegóły** bloku.

    ![Szczegóły zdarzenia](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    Zobacz atrybuty hello toocustomize wyświetlane na liście hello [wyświetlić atrybuty dodatkowe zdarzenia](backup-azure-monitor-vms.md#view-additional-event-attributes)

## <a name="configure-notifications"></a>Konfigurowanie powiadomień
 Można skonfigurować powiadomienia e-mail toosend hello Usługa alertów hello, które wystąpiły na powitania Ostatnia godzina lub w przypadku wystąpienia określonych typach zdarzeń.

tooset powiadomienia e-mail dla alertów

1. Polecenie menu alerty kopii zapasowej hello **skonfigurować powiadomienia**

    ![Menu alerty kopii zapasowej](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    zostanie otwarty blok powiadomienia Konfiguruj Hello.

    ![Konfigurowanie powiadomień bloku](./media/backup-azure-monitor-vms/configure-notifications.png)
2. W bloku powiadomienia Konfiguruj hello, powiadomień E-mail kliknij **na**.

    Hello adresatów i oknach dialogowych ważność ma gwiazdy toothem dalej, ponieważ te informacje są wymagane. Podaj co najmniej jeden adres e-mail, a następnie wybierz co najmniej jeden ważność.
3. W hello **adresatów (Poczta E-mail)** okna dialogowego, wpisz adresy e-mail hello dla kto otrzymywać powiadomienia hello. Użyj formatu hello: username@domainname.com. Oddzielaj adresy e-mail średnikami (;).
4. W hello **powiadamiania** obszaru, wybierz **Alert na** toosend powiadomienie, gdy hello określony występuje alert, lub **co godzinę szyfrowanego** toosend podsumowania hello ostatniej godziny.
5. W hello **ważność** okno dialogowe, wybierz co najmniej jeden poziom, które mają tootrigger powiadomienia e-mail.
6. Kliknij pozycję **Zapisz**.

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a>Jakie typy alertów są dostępne dla kopii zapasowych maszyn wirtualnych IaaS platformy Azure?
   | Poziom alertu | Wysyłania alertów |
   | --- | --- |
   | Krytyczne |Niepowodzenia wykonywania kopii zapasowej, niepowodzenia odzyskiwania |
   | Ostrzeżenie |Brak |
   | Informacyjny |Brak |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a>Czy występują sytuacje, w których wiadomość e-mail nie jest wysyłana, mimo że powiadomienia zostały skonfigurowane?
Istnieją sytuacje, w którym alert nie są wysyłane, nawet jeśli hello powiadomienia zostały prawidłowo skonfigurowane. W hello sytuacjach powiadomień poczty e-mail nie są wysyłane tooavoid szumu alertu:

* Jeśli powiadomienia są skonfigurowane tooHourly szyfrowane, a alert jest uruchamiany i rozpoznać w ciągu godziny hello.
* Witaj zadanie zostało anulowane.
* Zadanie tworzenia kopii zapasowej zostanie wywołany, a następnie nie, a inne zadanie tworzenia kopii zapasowej jest w toku.
* Uruchamia zaplanowane zadanie tworzenia kopii zapasowej dla maszyny Wirtualnej z obsługą usługi Resource Manager, ale hello wirtualna już nie istnieje.

## <a name="customize-your-view-of-events"></a>Dostosowywanie widoku zdarzeń
Witaj **dzienniki inspekcji** ustawienie zawiera zestaw wstępnie zdefiniowanych filtry i kolumny pokazywane są informacje zdarzeń operacyjnych. Widok hello można dostosować, aby po hello **zdarzenia** zostanie otwarty blok, przedstawia on hello informacje mają.

1. W hello [pulpitem nawigacyjnym magazynu](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), kliknij tooand przeglądania **dzienników inspekcji** tooopen hello **zdarzenia** bloku.

    ![Dzienniki inspekcji](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Witaj **zdarzenia** toohello zdarzenia operacyjne filtrowane tylko dla bieżącego magazynu hello zostanie otwarty blok.

    ![Filtr dzienniki inspekcji](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    Blok Hello lista hello krytyczny, błąd, ostrzeżenie i zdarzenia informacyjne, które wystąpiły w hello zeszłym tygodniu. Witaj przedział czasu jest domyślnie ustawiony w hello **filtru**. Witaj **zdarzenia** blok zawiera także wykres słupkowy śledzenia hello zdarzenia wystąpiły. Jeśli nie chcesz toosee wykres słupkowy hello, w hello **zdarzenia** menu, kliknij przycisk **wykresu Ukryj** tootoggle poza hello wykresu. Widok domyślny Hello zdarzeń pokazuje informacje operacji, poziom, stan, zasobów i czasu. Aby dowiedzieć się, jak udostępnianie dodatkowe atrybuty zdarzeń, zobacz sekcję hello [rozszerzanie informacji o zdarzeniu](backup-azure-monitor-vms.md#view-additional-event-attributes).
2. Aby uzyskać dodatkowe informacje dotyczące zdarzenia operacyjne, w hello **operacji** kolumny, kliknij jego bloku tooopen zdarzeń operacyjnych. Blok Hello zawiera szczegółowe informacje o zdarzeniach hello. Zdarzenia są pogrupowane według ich identyfikator korelacji i listy hello zdarzeń, które wystąpiły w hello przedział czasu.

    ![Szczegóły operacji](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. tooview szczegółowe informacje dotyczące konkretnego zdarzenia, z listy hello zdarzeń, kliknij przycisk tooopen zdarzeń hello jego **szczegóły** bloku.

    ![Szczegóły zdarzenia](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    informacje o poziom zdarzenia Hello są szczegółowych hello pobiera informacje. Jeśli preferowane jest wyświetlany tyle informacji na temat każdego zdarzenia, a chcesz tooadd to znacznie szczegółów toohello **zdarzenia** bloku, w sekcji hello [rozszerzanie informacji o zdarzeniu](backup-azure-monitor-vms.md#view-additional-event-attributes).

## <a name="customize-hello-event-filter"></a>Dostosowywanie hello filtr zdarzeń
Użyj hello **filtru** tooadjust lub wybierz hello informacje wyświetlane w szczególności bloku. informacje dotyczące zdarzenia hello toofilter:

1. W hello [pulpitem nawigacyjnym magazynu](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard), kliknij tooand przeglądania **dzienników inspekcji** tooopen hello **zdarzenia** bloku.

    ![Dzienniki inspekcji](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    Witaj **zdarzenia** toohello zdarzenia operacyjne filtrowane tylko dla bieżącego magazynu hello zostanie otwarty blok.

    ![Filtr dzienniki inspekcji](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. Na powitania **zdarzenia** menu, kliknij przycisk **filtru** tooopen tego bloku.

    ![otwarcie bloku filtru](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. Na powitania **filtru** bloku, Dostosuj hello **poziom**, **przedział czasu**, i **wywołującego** filtrów. Witaj inne filtry są niedostępne, ponieważ ich magazyn usług odzyskiwania hello zostały ustawione tooprovide hello bieżących informacji.

    ![Szczegóły zapytania dzienniki inspekcji](./media/backup-azure-monitor-vms/filter-blade.png)

    Można określić hello **poziom** zdarzenia: krytyczny, błąd, ostrzeżenie lub komunikat informacyjny. Można wybrać dowolną kombinację poziomów zdarzeń, ale musisz mieć co najmniej jeden wybrany poziom. Przełącz hello poziom lub wyłączyć. Witaj **przedział czasu** filtr zezwala toospecify hello długość czasu dla przechwytywania zdarzeń. Jeśli używasz niestandardowego przedział czasu, można ustawić hello rozpoczęcia i zakończenia godzin.
4. Po przejściu dzienników operacji hello gotowe tooquery przy użyciu filtru, kliknij przycisk **aktualizacji**. Witaj wyniki są wyświetlane w hello **zdarzenia** bloku.

    ![Szczegóły operacji](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a>Widok zdarzeń dodatkowe atrybuty
Przy użyciu hello **kolumn** przycisku, można włączyć tooappear atrybuty dodatkowe zdarzenia na liście hello na powitania **zdarzenia** bloku. Witaj domyślnej listy zdarzeń wyświetla informacje dotyczące operacji, poziom, stan, zasobów i czasu. tooenable dodatkowe atrybuty:

1. Na powitania **zdarzenia** bloku, kliknij przycisk **kolumn**.

    ![Otwórz kolumn](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    Witaj **wybierz kolumny** zostanie otwarty blok.

    ![Blok kolumn](./media/backup-azure-monitor-vms/columns-blade.png)
2. Witaj tooselect atrybutu, kliknij pole wyboru hello. Hello atrybut wyboru włącza i wyłącza.
3. Kliknij przycisk **zresetować** tooreset hello lista atrybutów w hello **zdarzenia** bloku. Po dodaniu lub usunięciu atrybutów z listy hello, użyj **zresetować** tooview hello nową listę atrybutów zdarzeń.
4. Kliknij przycisk **aktualizacji** tooupdate hello danych w atrybutach zdarzeń hello. Witaj w poniższej tabeli informacje na temat każdego atrybutu.

| Nazwa kolumny | Opis |
| --- | --- |
| Operacja |Nazwa Hello hello operacji |
| Poziom |Witaj poziom operacji hello, możliwe wartości: informacyjny, ostrzeżenie, błąd lub krytyczny |
| Stan |Opis stanu operacji hello |
| Zasób |Adres URL identyfikujący zasób hello; znany również jako identyfikator zasobu hello |
| Time |Czas zmierzony od hello bieżący czas, kiedy wystąpiło zdarzenie hello |
| Obiekt wywołujący |Kto lub co o nazwie lub wyzwolone hello zdarzeń; może być hello system lub użytkownik |
| Znacznik czasu |czas powitania po wyzwolone hello zdarzenie |
| Grupa zasobów |Hello grupy zasobów |
| Typ zasobu |Witaj wewnętrzny typ zasobu używany przez Menedżera zasobów |
| Identyfikator subskrypcji |Witaj skojarzony identyfikator subskrypcji |
| Kategoria |Kategoria zdarzenia hello |
| Identyfikator korelacji |Identyfikator wspólnej dla zdarzenia powiązane |

## <a name="use-powershell-toocustomize-alerts"></a>Użyj programu PowerShell toocustomize alertów
Niestandardowe powiadomień o alertach hello zadań można uzyskać w portalu hello. tooget te zadania, zdefiniuj opartych na środowisku PowerShell alert reguły na powitania operacyjne dzienniki zdarzeń. Użyj *środowiska PowerShell w wersji 1.3.0 lub nowszym*.

toodefine tooalert niestandardowe powiadomienie dla niepowodzenia tworzenia kopii zapasowej, należy użyć polecenia takie jak hello następującego skryptu:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

**ResourceId** : można uzyskać ResourceId hello dzienników inspekcji. Witaj ResourceId jest adresem URL podany w kolumnie zasobów hello hello dzienników operacji.

**OperationName** : OperationName jest w formacie hello "Microsoft.RecoveryServices/recoveryServicesVault/*EventName*" gdzie *EventName* może być:<br/>

* Zarejestruj subskrypcję <br/>
* Unregister <br/>
* ConfigureProtection <br/>
* Tworzenie kopii zapasowych <br/>
* Przywracanie <br/>
* StopProtection <br/>
* DeleteBackupData <br/>
* CreateProtectionPolicy <br/>
* DeleteProtectionPolicy <br/>
* UpdateProtectionPolicy <br/>

**Stan** : obsługiwane wartości to rozpoczęte, Powodzenie lub niepowodzenie.

**Grupa zasobów** : jest hello grupy zasobów, należy toowhich hello zasobów. Możesz dodać hello grupy zasobów kolumny toohello wygenerowane dzienniki. Grupa zasobów jest jeden z dostępnych typów hello zdarzeń informacji.

**Nazwa** : Nazwa hello reguły alertów.

**CustomEmail** : Określ toowhich adres e-mail niestandardowych hello ma toosend powiadomień o alertach

**SendToServiceOwners** : Ta opcja wysyła powiadomienia o alertach tooall Administratorzy i współadministratorzy hello subskrypcji. Mogą być używane w **AzureRmAlertRuleEmail nowy** polecenia cmdlet

### <a name="limitations-on-alerts"></a>Ograniczenia dotyczące alertów
Alerty oparte na zdarzeniu są toohello podmiotu następujące ograniczenia:

1. Alerty są wyzwalane na wszystkich maszynach wirtualnych w powitalne magazyn usług odzyskiwania. Nie można dostosować hello alert dla podzbioru maszyn wirtualnych w magazynie usług odzyskiwania.
2. Ta funkcja jest dostępna w wersji zapoznawczej. [Dowiedz się więcej](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Alerty są wysyłane z "alerts-noreply@mail.windowsazure.com". Obecnie nie można zmodyfikować hello nadawcą wiadomości e-mail.

## <a name="next-steps"></a>Następne kroki
Dzienniki zdarzeń włączyć doskonałe których post i inspekcji obsługę hello operacje tworzenia kopii zapasowej. rejestrowane są następujące operacje Hello:

* Zarejestruj subskrypcję
* Unregister
* Konfigurowanie ochrony
* Kopia zapasowa (zarówno zaplanowanych oraz kopii zapasowej na żądanie)
* Przywracanie
* Zatrzymaj ochronę
* Usuwanie danych kopii zapasowej
* Dodawanie zasad
* Usuń zasady
* Zaktualizuj zasady
* Anulowanie zadania

Szerokie opis zdarzenia, operacje i dzienników inspekcji na powitania usług platformy Azure, zobacz artykuł hello, [wyświetlania zdarzeń i dzienniki inspekcji](../monitoring-and-diagnostics/insights-debugging-with-events.md).

Informacje dotyczące ponownego tworzenia maszyny wirtualnej z punktu odzyskiwania, zapoznaj się z [przywracanie maszyn wirtualnych Azure](backup-azure-restore-vms.md). Jeśli potrzebujesz informacji na temat ochrony maszyn wirtualnych, zobacz [Pierwsze spojrzenie: Utwórz kopię zapasową maszyn wirtualnych tooa magazyn usług odzyskiwania i](backup-azure-vms-first-look-arm.md). Dowiedz się więcej o zadaniach zarządzania hello kopii zapasowych maszyn wirtualnych w artykule hello [kopii zapasowych maszyn wirtualnych Azure zarządzanie](backup-azure-manage-vms.md).
