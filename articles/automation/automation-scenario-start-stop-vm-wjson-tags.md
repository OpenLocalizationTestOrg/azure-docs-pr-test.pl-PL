---
title: "Stan maszyny Wirtualnej Azure tooschedule tagów w formacie JSON aaaUse | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono, jak ciągi toouse JSON na tagi tooautomate hello planowanie uruchamiania maszyny Wirtualnej i zamykania."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Scenariusz automatyzacji Azure: przy użyciu formacie JSON tagów toocreate harmonogram uruchamiania maszyny Wirtualnej platformy Azure i zamykania
Klienci często mają tooschedule hello uruchamiania i zamykania maszyn wirtualnych toohelp obniżenie kosztów subskrypcji lub obsługuje wymagań technicznych i biznesowych.

Witaj następujący scenariusz umożliwia tooset się automatycznego uruchamiania i wyłączania maszyn wirtualnych przy użyciu tagu o nazwie harmonogram na poziomie grupy zasobów lub maszyny wirtualnej na platformie Azure. Ten harmonogram można skonfigurować w niedzielę tooSaturday czas uruchamiania i czasu zamykania.

Mamy niektóre opcje poza pole. Należą do nich:

* [Zestawy skalowania maszyny wirtualnej](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) przy użyciu ustawień automatycznego skalowania, które pozwalają tooscale przychodzący lub wychodzący.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) usługi, która ma wbudowaną funkcję hello planowania operacji uruchamiania i wyłączania.

Jednak te opcje obsługują tylko określonych scenariuszy i nie może być zastosowane tooinfrastructure jako — usługa (IaaS), maszynach wirtualnych.

Podczas hello tag harmonogramu jest stosowane tooa grupy zasobów, jest również zastosowane tooall maszyn wirtualnych w tej grupie zasobów. Jeśli harmonogram jest również tooa bezpośrednio zastosowane maszyny Wirtualnej, harmonogram ostatniego hello ma pierwszeństwo przed w hello w następującej kolejności:

1. Grupa zasobów zastosowane tooa harmonogramu
2. Zaplanuj grupy zasobów tooa zastosowane i maszyny wirtualnej w grupie zasobów hello
3. Maszyna wirtualna tooa harmonogram stosowane

W tym scenariuszu zasadniczo przyjmuje ciągu JSON w określonym formacie i dodaje go jako wartość hello tagu o nazwie harmonogramu. Następnie element runbook zawiera listę wszystkich grup zasobów i maszyn wirtualnych i identyfikuje hello harmonogramy dla każdej maszyny Wirtualnej, oparte na scenariusze hello wymienione wcześniej. Następnie hello maszyn wirtualnych, które mają harmonogramy dołączony w pętli i ocenia, jakie działania należy podjąć. Na przykład określają one, które maszyny wirtualne muszą toobe zatrzymana, zamknięta lub ignorowane.

Te elementy runbook uwierzytelniania za pomocą hello [konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Pobierz elementy runbook hello hello scenariusza
Ten scenariusz obejmuje cztery elementy runbook przepływu pracy programu PowerShell, które można pobrać z hello [galerii TechNet](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) lub hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repozytorium dla tego projektu.

| Element Runbook | Opis |
| --- | --- |
| ResourceSchedule testu |Sprawdza harmonogram każdej maszyny wirtualnej, a następnie wykonuje zamykania lub uruchamiania w zależności od hello harmonogramu. |
| Dodaj ResourceSchedule |Dodaje hello harmonogram tag tooa maszyny Wirtualnej lub grupy zasobów. |
| ResourceSchedule aktualizacji |Modyfikuje hello istniejącego harmonogramu znacznika przez zamianę nowy. |
| Usuń ResourceSchedule |Usuwa hello harmonogram tagu z maszyny Wirtualnej lub grupy zasobów. |

## <a name="install-and-configure-this-scenario"></a>Instalowanie i konfigurowanie tego scenariusza
### <a name="install-and-publish-hello-runbooks"></a>Instalowanie i publikować elementy runbook hello
Po pobraniu hello elementów runbook, można je zaimportować za pomocą procedury hello w [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Każdy element runbook należy opublikować po jego został pomyślnie zaimportowany na koncie automatyzacji.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Dodaj element runbook toohello ResourceSchedule testu harmonogramu
Wykonaj te kroki tooenable hello harmonogramu dla elementu runbook ResourceSchedule testu hello. Jest to hello elementu runbook, która sprawdza maszyn wirtualnych powinny być uruchamiane, zamknięta, lub w lewo, ponieważ jest.

1. Z hello portalu Azure, otwórz Twoje konto usługi Automatyzacja, a następnie kliknij hello **elementów Runbook** kafelka.
2. Na powitania **ResourceSchedule testu** bloku, kliknij przycisk hello **harmonogramy** kafelka.
3. Na powitania **harmonogramy** bloku, kliknij przycisk **Dodaj harmonogram**.
4. Na powitania **harmonogramy** bloku, wybierz opcję **powiązania elementu runbook tooyour harmonogram**. Następnie wybierz **Utwórz nowy harmonogram**.
5. Na powitania **nowy harmonogram** bloku, wpisz nazwę hello tego harmonogramu, na przykład: *HourlyExecution*.
6. Dla harmonogramu hello **Start**, ustaw hello początkowy czas tooan godzina przyrostu.
7. Wybierz **cyklu**, a następnie **powtarzanie co interwał**, wybierz pozycję **1 godzina**.
8. Sprawdź, czy **ustawienia okresu ważności** ustawiono zbyt**nr**, a następnie kliknij przycisk **Utwórz** toosave nowego harmonogramu.
9. Na powitania **Runbook harmonogram** bloku opcji wybierz **parametry i ustawienia uruchamiania**. W hello testu ResourceSchedule **parametry** bloku, wprowadź nazwę hello subskrypcji w hello **Nazwa subskrypcji** pola.  Jest to parametr tylko hello, która jest wymagana dla elementu runbook hello.  Po zakończeniu kliknij przycisk **OK**.

po jego ukończeniu harmonogram Hello powinna wyglądać hello poniżej:

![Skonfigurowany ResourceSchedule testu elementu runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Witaj formatu ciągu JSON
To rozwiązanie zasadniczo ma JSON ciągu na określony format i dodaje go jako wartość hello tagu o nazwie harmonogramu. Następnie element runbook zawiera listę wszystkich grup zasobów i maszyn wirtualnych i identyfikuje hello harmonogramy dla każdej maszyny wirtualnej.

Element runbook Hello pętli hello maszyn wirtualnych, które mają harmonogramy dołączona i sprawdza, jakie działania należy podjąć. Witaj poniżej znajduje się przykład sposobu rozwiązania hello powinien być sformatowany:

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

Oto niektóre szczegółowe informacje na temat tej struktury:

1. format Hello tej struktury JSON jest zoptymalizowany toowork wokół hello 256 znaków ograniczenie wartości jeden tag na platformie Azure.
2. *TzId* reprezentuje hello strefy czasowej hello maszyny wirtualnej. Ten identyfikator można uzyskać za pomocą klasy TimeZoneInfo .NET hello w sesji programu PowerShell —**[System.TimeZoneInfo]:: GetSystemTimeZones()**.

   ![GetSystemTimeZones w programie PowerShell](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Dni robocze są reprezentowane z wartością liczbową zero toosix. Witaj zero jest równa niedzielę.
   * Witaj godzina rozpoczęcia jest reprezentowana z hello **S** atrybutu i jego wartość jest w formacie 24-godzinnym.
   * Witaj czas zakończenia lub zamknięcie odpowiada z hello **E** atrybutu i jego wartość jest w formacie 24-godzinnym.

     Jeśli hello **S** i **E** atrybuty każdego mają wartość zero (0), hello maszyny wirtualnej pozostanie w jej obecnym stanie w czasie hello szacowania.
3. Jeśli chcesz tooskip oceny dla określonego dnia tygodnia hello, nie dodawaj sekcji za ten dzień tygodnia hello. Poniższy przykład, tylko poniedziałek jest oceniane hello i hello innych dni tygodnia hello są ignorowane:

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Tag grupy zasobów lub maszyny wirtualne
tooshut dół maszyn wirtualnych, należy tootag hello maszyn wirtualnych lub hello grup zasobów, w których są przechowywane. Maszyny wirtualne, które nie mają znacznika harmonogramu nie są uwzględniane. W związku z tym nie jest uruchomiona lub zamknięta.

Istnieją dwa sposoby tootag zasobów grup lub maszyn wirtualnych w tym rozwiązaniu. Należy go bezpośrednio z portalu hello. Lub może używać hello Dodaj ResourceSchedule, ResourceSchedule aktualizacji i Usuń ResourceSchedule elementów runbook.

### <a name="tag-through-hello-portal"></a>Tag za pośrednictwem portalu hello
Wykonaj te kroki tootag maszyny wirtualnej lub grupy zasobów w portalu hello:

1. Spłaszczanie hello ciągu JSON i sprawdź, czy nie ma żadnych spacji.  Ciągu JSON powinien wyglądać następująco:

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Wybierz hello **Tag** ikony dla maszyny Wirtualnej lub zasób grupy tooapply tego harmonogramu.

   ![Opcja tag maszyny Wirtualnej](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. Tagi są definiowane po parę klucz/wartość. Typ **harmonogram** w hello **klucza** pola, a następnie wklej ciągu JSON hello na powitania **wartość** pola. Kliknij pozycję **Zapisz**. Twoje nowy znacznik powinien zostać wyświetlony na liście hello znaczników dla zasobu.

   ![Tag harmonogram maszyny Wirtualnej](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>Znacznik z programu PowerShell
Wszystkie zaimportowane elementy runbook zawierają informacje pomocy na początku hello hello skryptu, który opisuje, jak tooexecute hello elementy runbook bezpośrednio z programu PowerShell. Witaj ScheduleResource Dodaj i ScheduleResource aktualizacji elementów runbook można wywołać z programu PowerShell. Można to zrobić przez przekazanie wymaganych parametrów, które pozwalają toocreate lub aktualizacji tag harmonogram hello na maszyny Wirtualnej lub zasobów w grupie poza hello portalu.

toocreate, dodawanie i usuwanie tagów za pomocą programu PowerShell, należy najpierw zbyt[konfigurowania środowiska PowerShell dla usługi Azure](/powershell/azure/overview). Po zakończeniu konfiguracji hello może kontynuować hello następujące kroki.

### <a name="create-a-schedule-tag-with-powershell"></a>Utwórz harmonogram tag przy użyciu programu PowerShell
1. Otwórz sesję programu PowerShell. Następnie użyj powitania po tooauthenticate przykład przy użyciu konta Uruchom jako i toospecify subskrypcji:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Zdefiniuj harmonogram tablicy skrótów. Poniżej przedstawiono przykładowy sposób wykonane:

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Zdefiniuj parametry hello, które są wymagane przez element runbook hello. W hello poniższy przykład możemy przeznaczona dla maszyny Wirtualnej:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Jeśli w przypadku znakowanie grupę zasobów, Usuń hello *VMName* parametru z skrótu hello $params tabeli w następujący sposób:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Uruchom hello ResourceSchedule Dodaj element runbook z hello następujące parametry toocreate hello harmonogram tagu:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. tooupdate tag maszyną wirtualną lub grupy zasobów, wykonywanie hello **ResourceSchedule aktualizacji** elementu runbook o hello następujące parametry:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>Usuń znacznik harmonogramu przy użyciu programu PowerShell
1. Otwórz sesję programu PowerShell i uruchom następujące tooauthenticate przy użyciu konta Uruchom jako i tooselect hello i określ subskrypcję:

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Zdefiniuj parametry hello, które są wymagane przez element runbook hello. W hello poniższy przykład możemy przeznaczona dla maszyny Wirtualnej:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    Jeśli usuwasz tag z grupy zasobów, Usuń hello *VMName* parametru z skrótu hello $params tabeli w następujący sposób:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Wykonaj hello ResourceSchedule Usuń element runbook tooremove hello harmonogram tagu:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate tag maszyną wirtualną lub grupy zasobów, wykonywane hello ResourceSchedule Usuń element runbook za pomocą hello następujące parametry:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> Zaleca się, że aktywne i można monitorować te elementy runbook (hello stany maszyny wirtualnej) zamknąć tooverify, które są maszyny wirtualne i odpowiednio uruchomiona.
>

Szczegóły hello tooview hello ResourceSchedule testu elementu runbook zadania w hello portalu Azure, wybierz hello **zadania** kafelka hello elementu runbook. Parametry wejściowe Wyświetla podsumowanie hello Hello zadania i dane wyjściowe hello strumienia, oprócz toogeneral informacje o zadaniu hello oraz wszystkie wyjątki jeśli takie były.

Witaj **Podsumowanie zadania** obejmuje wiadomości powitania strumienie danych wyjściowych, ostrzeżeń i błędów. Wybierz hello **dane wyjściowe** kafelka tooview szczegółowe wyniki z hello wykonanie elementu runbook.

![Dane wyjściowe ResourceSchedule testu](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Następne kroki
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md).
* toolearn więcej informacji na temat typów elementów runbook i ich zalety i ograniczenia, zobacz [typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md).
* Aby uzyskać więcej informacji o funkcji obsługi skryptów programu PowerShell, zobacz [Obsługa skryptów PowerShell natywnego automatyzacji Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).
* toolearn więcej informacji na temat rejestrowania elementu runbook i wychodzących, zobacz [Runbook dane wyjściowe i komunikaty w automatyzacji Azure](automation-runbook-output-and-messages.md).
* więcej informacji na temat konta Uruchom jako platformy Azure i tooauthenticate elementy runbook za pomocą, zobacz temat toolearn [uwierzytelniania elementy runbook za pomocą konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).
