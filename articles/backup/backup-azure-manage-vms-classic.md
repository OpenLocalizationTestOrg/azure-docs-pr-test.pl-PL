---
title: monitor i aaaManage kopii zapasowych maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak monitor wirtualnej platformy Azure i toomanage komputera kopii zapasowych"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>Zarządzanie typowych zadań kopia zapasowa Azure i alerty wyzwalacza w portalu klasycznym hello
> [!div class="op_single_selector"]
> * [Zarządzanie kopiami zapasowymi maszyny Wirtualnej Azure](backup-azure-manage-vms.md)
> * [Zarządzanie kopiami zapasowymi klasyczne maszyny Wirtualnej](backup-azure-manage-vms-classic.md)
>
>

Ten artykuł zawiera informacje o wspólnego zarządzania i monitorowania zadań związanych z klasycznego modelu maszyny wirtualne chronione na platformie Azure.  

> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Zobacz [przygotowanie Twojego środowiska tooback zapasowych maszyn wirtualnych Azure](backup-azure-vms-prepare.md) szczegółowe informacje na temat pracy z Classic deployment model maszyn wirtualnych.
>
> [!IMPORTANT]
>Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.
>
> Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
>- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
>- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.

## <a name="manage-protected-virtual-machines"></a>Zarządzanie chronione maszyny wirtualne
toomanage chronione maszyny wirtualne:

1. tooview i zarządzanie nimi ustawienia kopii zapasowej dla maszyny wirtualnej kliknij hello **chronione elementy** kartę.
2. Kliknij nazwę hello hello toosee chronionego elementu **szczegóły kopii zapasowej** kartę, która pokazuje informacje dotyczące hello ostatniej kopii zapasowej.

    ![Kopia zapasowa maszyny wirtualnej](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview i zarządzanie nimi ustawień zasad tworzenia kopii zapasowej dla maszyny wirtualnej kliknij hello **zasady** kartę.

    ![Zasady maszyny wirtualnej](./media/backup-azure-manage-vms/manage-policy-settings.png)

    Witaj **zasady tworzenia kopii zapasowej** karcie pokazuje hello istniejące zasady. Można zmodyfikować zgodnie z potrzebami. Jeśli potrzebujesz toocreate nowych zasad kliknij **Utwórz** na powitania **zasady** strony. Należy pamiętać, że tooremove zasady go nie powinny być skojarzone z nią żadne maszyny wirtualne.

    ![Zasady maszyny wirtualnej](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. Możesz też uzyskać więcej informacji na temat akcji lub stan maszyny wirtualnej na powitania **zadania** strony. Kliknij zadanie w tooget listy hello więcej szczegółów lub filtrowania zadań dla określonej maszyny wirtualnej.

    ![Zadania](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>Na żądanie kopii zapasowej maszyny wirtualnej
Skonfigurowane dla ochrony na żądanie można wykonać kopii zapasowej maszyny wirtualnej. Jeśli trwa oczekiwanie na początkową kopię zapasową hello hello maszyny wirtualnej, tworzenia kopii zapasowej na żądanie utworzy pełną kopię hello maszyny wirtualnej w magazynie kopii zapasowej Azure. Jeśli pierwsza kopia zapasowa została wykonana, na żądanie kopii zapasowej będzie tylko do wysyłania zmiany z poprzedniej kopii zapasowej tooAzure kopii zapasowej tj. Magazyn on mają zawsze wartości rosnące.

> [!NOTE]
> Zakres przechowywania kopii zapasowej na żądanie ustawiono tooretention wartość określona dla przechowywania codziennych w toohello odpowiednie zasady tworzenia kopii zapasowej maszyny Wirtualnej.  
>
>

tootake na żądanie kopii zapasowej maszyny wirtualnej:

1. Przejdź toohello **chronione elementy** i wybrać opcję **maszyny wirtualnej Azure** jako **typu** (jeśli jeszcze nie został wybrany) i wybierz polecenie **wybierz**przycisku.

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/vm-type.png)
2. Wybierz maszynę wirtualną hello, na którym tootake na żądanie kopii zapasowej i kliknij na **Utwórz kopię zapasową teraz** przycisk u dołu hello hello strony.

    ![Wykonaj kopię zapasową teraz](./media/backup-azure-manage-vms/backup-now.png)

    Spowoduje to utworzenie zadania tworzenia kopii zapasowej na maszynie wirtualnej hello wybrane. Zakres przechowywania punktu odzyskiwania został utworzony za pomocą tego zadania będzie taka sama jak określona w zasad hello skojarzoną z maszyną wirtualną hello.

    ![Tworzenie zadania tworzenia kopii zapasowej](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > tooview hello zasady skojarzone z maszyną wirtualną, Drąż w dół do maszyny wirtualnej w hello **chronione elementy** karta zasad Przejdź toobackup i strony.
   >
   >
3. Po utworzeniu zadania hello, możesz kliknąć **zadania** przycisk wyskakujące hello paska toosee hello odpowiedniego zadania na stronie zadań hello.

    ![Utworzono zadanie kopii zapasowej](./media/backup-azure-manage-vms/created-job.png)
4. Po pomyślnym ukończeniu zadania hello, zostanie utworzony punkt odzyskiwania, którego można użyć maszyny wirtualnej hello toorestore. To powoduje również zwiększenie wartości kolumny punktu odzyskiwania hello 1 w **chronione elementy** strony.

## <a name="stop-protecting-virtual-machines"></a>Zatrzymaj ochronę maszyn wirtualnych
Możesz wybrać toostop hello kolejnych kopii zapasowych maszyny wirtualnej z hello następujące opcje:

* Zachowaj dane kopii zapasowej skojarzonego z maszyną wirtualną w magazynie usługi Kopia zapasowa Azure
* Usuwanie danych kopii zapasowej skojarzonego z maszyną wirtualną

Jeśli zostały wybrane dane kopii zapasowej tooretain skojarzoną z maszyną wirtualną, można użyć maszyny wirtualnej hello toorestore dane kopii zapasowej hello. O cenach szczegóły takich maszyn wirtualnych, kliknij przycisk [tutaj](https://azure.microsoft.com/pricing/details/backup/).

tooStop ochrony dla maszyny wirtualnej:

1. Przejdź za**chronione elementy** i wybrać opcję **maszyny wirtualnej platformy Azure** jako typ filtru hello (jeśli jeszcze nie został wybrany) i kliknięcie **wybierz** przycisku.

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/vm-type.png)
2. Wybierz maszynę wirtualną hello i wybierz polecenie **Zatrzymaj ochronę** u dołu hello hello strony.

    ![Zatrzymaj ochronę](./media/backup-azure-manage-vms/stop-protection.png)
3. Domyślnie kopia zapasowa Azure nie powoduje usunięcia danych kopii zapasowej hello skojarzoną z maszyną wirtualną hello.

    ![Upewnij się, Zatrzymaj ochronę](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    Jeśli chcesz toodelete dane kopii zapasowej, zaznacz pole wyboru hello.

    ![Pole wyboru](./media/backup-azure-manage-vms/checkbox.png)

    Wybierz przyczynę zatrzymywanie hello tworzenia kopii zapasowej. Jest to opcjonalne, podania przyczyny będzie pomocy toowork kopia zapasowa Azure na powitania opinii i priorytety hello scenariuszy.
4. Polecenie **przesyłania** hello toosubmit przycisk **Zatrzymaj ochronę** zadania. Polecenie **zadania** toosee hello odpowiedniego zadania hello w **zadania** strony.

    ![Zatrzymaj ochronę](./media/backup-azure-manage-vms/stop-protect-success.png)

    Jeśli nie wybrano **Usuń skojarzone dane kopii zapasowej** opcję podczas **Zatrzymaj ochronę** ochrony kreatora, a następnie po zakończeniu zadania, stan zmienia się zbyt**ochrony zatrzymana**. Hello dane pozostają z usługi Kopia zapasowa Azure, dopóki zostanie jawnie usunięty. Należy zawsze usunąć dane hello, wybierając hello maszyny wirtualnej w hello **chronione elementy** strony i klikając **usunąć**.

    ![Zatrzymania ochrony](./media/backup-azure-manage-vms/protection-stopped-status.png)

    Jeśli wybrano hello **Usuń skojarzone dane kopii zapasowej** opcji, hello maszyny wirtualnej nie będzie częścią hello **chronione elementy** strony.

## <a name="re-protect-virtual-machine"></a>Ponownie włączyć ochronę maszyny wirtualnej
Jeśli nie wybrano hello **Skojarz dane kopii zapasowej usunięcia** opcji w **Zatrzymaj ochronę**, można ponownie włączyć ochronę maszyny wirtualnej hello, wykonując następujące toobacking podobne kroki hello się zarejestrować wirtualnego maszyny. Gdy chroniony, tej maszyny wirtualnej zostanie zachowane dane kopii zapasowej poprzedniego toostop ochrony i punkty odzyskiwania utworzone po ponownie ochronę.

Po ponownego włączenia ochrony stanu ochrony maszyny wirtualnej hello zostaną zmienione za**chronione** jeżeli istnieją punkty odzyskiwania wcześniejsze zbyt**Zatrzymaj ochronę**.

  ![Maszyny Wirtualnej przełączonej](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> Podczas ponownie ochrona powitalnych maszyny wirtualnej, można wybrać inne zasady niż zasady hello, z którą maszyny wirtualnej został początkowo chronić.
>
>

## <a name="unregister-virtual-machines"></a>Wyrejestruj maszyny wirtualne
Jeśli chcesz, aby maszyna wirtualna hello tooremove z magazynu kopii zapasowych hello:

1. Polecenie hello **UNREGISTER** przycisk u dołu hello hello strony.

    ![Wyłącz ochronę](./media/backup-azure-manage-vms/unregister-button.png)

    Powiadomienie wyskakujące będą wyświetlane u dołu hello ekranu hello żądania potwierdzenia. Kliknij przycisk **tak** toocontinue.

    ![Wyłącz ochronę](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>Usuwanie danych kopii zapasowej
Można usunąć danych kopii zapasowej hello skojarzonych z maszyną wirtualną, albo:

* Podczas zadanie zatrzymania ochrony
* Po Zatrzymaj ochronę ukończenia zadania na maszynie wirtualnej

toodelete dane kopii zapasowej na maszynie wirtualnej, który znajduje się w hello *ochrony zatrzymana* stanu po pomyślnym zarejestrowaniu **zatrzymać kopii zapasowej** zadania:

1. Przejdź toohello **chronione elementy** i wybrać opcję **maszyny wirtualnej Azure** jako *typu* i kliknij przycisk hello **wybierz** przycisku.

    ![Typu maszyny Wirtualnej](./media/backup-azure-manage-vms/vm-type.png)
2. Wybierz maszynę wirtualną hello. Maszyna wirtualna Hello będzie w **ochrony zatrzymana** stanu.

    ![Ochrona zatrzymana](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. Kliknij przycisk hello **usunąć** przycisk u dołu hello hello strony.

    ![Usuwanie kopii zapasowej](./media/backup-azure-manage-vms/delete-backup.png)
4. W hello **usunąć danych kopii zapasowej** kreatora wybierz przyczynę usuwanie danych kopii zapasowej (zdecydowanie zalecane) i kliknij przycisk **przesyłania**.

    ![Usuwanie danych kopii zapasowej](./media/backup-azure-manage-vms/delete-backup-data.png)
5. Spowoduje to utworzenie zadania toodelete kopii zapasowych danych z wybraną maszynę wirtualną. Kliknij przycisk **zadania** toosee odpowiedniego zadania na stronie zadań.

    ![Pomyślnie usunięto danych](./media/backup-azure-manage-vms/delete-data-success.png)

    Po zakończeniu zadania hello hello wpis odpowiednią maszynę wirtualną toohello zostaną usunięte z **chronione elementy** strony.

## <a name="dashboard"></a>Pulpit nawigacyjny
Na powitania **pulpitu nawigacyjnego** stronie można przejrzeć informacje o maszynach wirtualnych platformy Azure, magazynu i zadań skojarzonych z nimi w hello ostatnich 24 godzin. Można wyświetlić stanu kopii zapasowej oraz wszelkie skojarzone błędy tworzenia kopii zapasowej.

![Pulpit nawigacyjny](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Wartości na pulpicie nawigacyjnym hello są odświeżane co 24 godziny.
>
>

## <a name="auditing-operations"></a>Operacje inspekcji
Kopia zapasowa Azure udostępnia przegląd hello "dzienniki operacji" operacje tworzenia kopii zapasowej wyzwalane przez powitania klienta, dzięki czemu można łatwo toosee dokładnie jakie operacje zarządzania były wykonywane na powitania magazynu kopii zapasowych. Dzienniki operacji włączyć doskonałe których post i inspekcji obsługę hello operacje tworzenia kopii zapasowej.

Hello następujące operacje są rejestrowane w dziennikach operacji:

* Zarejestruj subskrypcję
* Unregister
* Konfigurowanie ochrony
* Kopia zapasowa (zarówno zaplanowanych oraz kopii zapasowej na żądanie za pomocą BackupNow)
* Przywracanie
* Zatrzymaj ochronę
* Usuwanie danych kopii zapasowej
* Dodawanie zasad
* Usuń zasady
* Zaktualizuj zasady
* Anulowanie zadania

odpowiedni magazyn kopii zapasowych tooa dzienniki operacji tooview:

1. Przejdź za**usług zarządzania** w portalu Azure, a następnie kliknij przycisk hello **dzienniki operacji** kartę.

    ![Dzienniki operacji](./media/backup-azure-manage-vms/ops-logs.png)
2. Filtry hello wybierz **kopii zapasowej** jako *typu* i określ nazwę magazynu kopii zapasowych hello w *nazwa usługi* i kliknij przycisk **przesyłania**.

    ![Filtr dzienniki operacji](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. W dziennikach operacji hello, wybierz żadnej operacji, a następnie kliknij przycisk **szczegóły** toosee szczegóły odpowiadająca mu operacja tooan.

    ![Szczegóły pobierania dzienników operacji](./media/backup-azure-manage-vms/ops-logs-details.png)

    Witaj **kreatora szczegóły** zawiera informacje na temat operacji hello wyzwoleniu zadania. identyfikator zasobu, na którym ta operacja zostanie wywołany i godzina rozpoczęcia operacji hello.

    ![Szczegóły operacji](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>Powiadomienia o alertach
Niestandardowe powiadomień o alertach hello zadań można uzyskać w portalu. Jest to osiągane przez zdefiniowanie opartych na środowisku PowerShell reguł alertów na operacyjne dzienniki zdarzeń. Firma Microsoft zaleca używanie *środowiska PowerShell w wersji 1.3.0 lub nowszej*.

toodefine tooalert niestandardowe powiadomienie w przypadku niepowodzenia tworzenia kopii zapasowej będzie wyglądać przykład polecenia:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**: można uzyskać tę z menu podręczne dzienniki operacji zgodnie z opisem w powyżej sekcji. ResourceUri w oknie podręcznym szczegóły operacji jest toobe ResourceId hello podany dla tego polecenia cmdlet.

**OperationName**: są to hello formatu "Microsoft.Backup/backupvault/<EventName>" w przypadku, gdy EventName jest jednym z rejestru, Unregister, ConfigureProtection, kopii zapasowych, przywracania, StopProtection, DeleteBackupData, UpdateProtectionPolicy CreateProtectionPolicy, DeleteProtectionPolicy,

**Stan**: obsługiwane wartości są Started zakończyło się pomyślnie, a nie powiodła się.

**Grupa zasobów**: Grupa zasobów hello zasobu, na którym zostanie wywołany operacji. Możesz go uzyskać z ResourceId wartość. Wartość między polami */resourceGroups/* i */providers/* w ResourceId wartość jest wartością hello grupa zasobów.

**Nazwa**: Nazwa hello reguły alertów.

**CustomEmail**: Określ toowhich adres e-mail niestandardowych hello ma toosend powiadomień o alertach

**SendToServiceOwners**: Ta opcja wysyła powiadomienie o alercie tooall Administratorzy i współadministratorzy hello subskrypcji. Mogą być używane w **AzureRmAlertRuleEmail nowy** polecenia cmdlet

### <a name="limitations-on-alerts"></a>Ograniczenia dotyczące alertów
Alerty oparte na zdarzeniu są poddane toohello następujące ograniczenia:

1. Alerty są wyzwalane na wszystkich maszynach wirtualnych w magazynie kopii zapasowych hello. Nie można go dostosować tooget alertów dla określonej grupy maszyn wirtualnych w magazynie kopii zapasowych.
2. Ta funkcja jest dostępna w wersji zapoznawczej. [Dowiedz się więcej](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Będą wysyłane alerty z "alerts-noreply@mail.windowsazure.com". Obecnie nie można zmodyfikować hello nadawcą wiadomości e-mail.

## <a name="next-steps"></a>Następne kroki
* [Przywracanie maszyny wirtualne platformy Azure](backup-azure-restore-vms.md)
