---
title: "aaaOverview hello dziennika aktywności platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie hello jest dziennika aktywności platformy Azure i jak można użyć jej toounderstand zdarzeń występujących w ramach Twojej subskrypcji platformy Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>Monitorowanie aktywności subskrypcji z hello dziennika aktywności platformy Azure
Witaj **dziennika aktywności platformy Azure** jest Dziennik subskrypcji, która zapewnia wgląd w zdarzenia na poziomie subskrypcji, które wystąpiły na platformie Azure. W tym zakresie danych z usługi Azure Resource Manager tooupdates danych operacyjnych na zdarzenia kondycji usługi. Hello dziennik aktywności była wcześniej znana jako "Dzienników inspekcji" lub "Operacyjne dzienniki", ponieważ hello kategorii administracyjnej raporty płaszczyzny kontroli zdarzeń dla subskrypcji. Korzystając z hello dziennik aktywności, można określić hello ", co, która i kiedy" dla żadnego zapisu (PUT, POST, DELETE) wykonywanych na powitania zasobów w ramach subskrypcji. Można także zrozumieć hello stanu operacji hello i inne odpowiednie właściwości. Hello dziennik aktywności nie zawiera operacje odczytu (GET) lub operacji dla zasobów korzystających z klasycznej hello / modelu "RDFE".

![Vs Dzienniki aktywności innych typów dzienników ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

Rysunek 1: Dzienniki aktywności vs innych typów dzienników

Witaj dziennik aktywności różni się od [dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md). Dzienniki aktywności zawierają dane dotyczące operacji hello w zasobie z hello poza (hello "kontroli płaszczyzny"). Dzienniki diagnostyczne są emitowane przez zasób i podaj informacje na temat operacji hello tego zasobu (hello "płaszczyzna danych").

Można pobrać zdarzenia z dziennika aktywności za pomocą hello portalu Azure, interfejsu wiersza polecenia, poleceń cmdlet programu PowerShell i interfejsu API REST Monitor Azure.


> [!WARNING]
> Witaj dziennika aktywności platformy Azure jest przeznaczone głównie dla działania wykonywane w usłudze Azure Resource Manager. Nie śledzi zasobów przy użyciu modelu klasycznego/frontonu REDDOG hello. Niektóre typy zasobów Classic ma dostawcy zasobów serwera proxy w usłudze Azure Resource Manager (na przykład obszar Microsoft.ClassicCompute). Jeśli w interakcję z typem zasobu Classic za pośrednictwem usługi Azure Resource Manager przy użyciu tych dostawców zasobów serwera proxy, operacje hello są wyświetlane w hello dziennik aktywności. Jeśli interakcji z typ zasobu klasycznej w portalu klasycznym hello lub w przeciwnym razie poza hello serwerów proxy usługi Azure Resource Manager, czynności użytkownika są tylko rejestrowane w hello dziennika operacji. Witaj dziennika operacji jest dostępna tylko w portalu klasycznym hello.
>
>

Widok hello po hello wprowadzenie wideo dziennik aktywności.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Kategorie hello dziennik aktywności
Witaj dziennik aktywności zawiera kilka kategorii danych. Aby uzyskać szczegółowe informacje na powitania schematów z tych kategorii [znajduje się w artykule](monitoring-activity-log-schema.md). Należą do nich:
* **Administracyjne** — ta kategoria zawiera rekord hello wszystkich utworzyć, update, delete i akcji operacje wykonywane za pomocą Menedżera zasobów. Przykłady powitalne typy zdarzeń, które można zobaczyć w tej kategorii "Utwórz maszynę wirtualną" i "usunąć grupy zabezpieczeń sieci" każdej akcji podjętej przez użytkownika lub aplikacji przy użyciu usługi Resource Manager ma formę operację określonego typu zasobu. Jeśli typ operacji hello jest zapisu, usuwania lub działania, rekordy hello hello start i powodzenie lub niepowodzenie tej operacji są rejestrowane w hello kategorii administracyjnej. Kategoria administracyjna Hello także żadnych kontroli dostępu na podstawie toorole zmian w subskrypcji.
* **Kondycja usługi** — ta kategoria zawiera rekord hello określone zdarzenia kondycji usługi, które wystąpiły na platformie Azure. Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "Azure SQL w wschodnie stany USA występuje Przestój." Zdarzenia kondycji usługi są dostępne w pięciu odmian: wymagana akcja, wspierana odzyskiwania, zdarzenie, konserwacji, informacje lub zabezpieczeń i są wyświetlane tylko, jeśli zasób hello subskrypcji, która może wpływać na powitania zdarzeń.
* **Alert** — ta kategoria zawiera rekord hello aktywacji wszystkich alertów platformy Azure. Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "procent użycia procesora CPU na myVM została ponad 80 dla hello ostatnich 5 minut." Z różnymi systemami Azure ma alertów koncepcji — można zdefiniować regułę jakiegoś i otrzymasz powiadomienie, gdy warunki reguły są zgodne. Zawsze Azure obsługiwanego typu alertu "aktywuje," lub hello są warunki niespełnienia toogenerate powiadomienie, rekord aktywacji hello również spoczywa toothis kategorii hello dziennik aktywności.
* **Funkcja automatycznego skalowania** — ta kategoria zawiera rekord hello żadnych operacji toohello powiązane zdarzenia aparatu skalowania automatycznego hello oparte na wszystkie ustawienia skalowania automatycznego zdefiniowane w ramach subskrypcji. Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "Skalowania automatycznego skalowania w górę akcja nie powiodła się". Przy użyciu automatycznego skalowania, można automatycznie skalować w poziomie lub skalować w hello liczbę wystąpień w typie zasobów obsługiwanych na podstawie czasu dnia i/lub obciążenia () dane przy użyciu ustawienia skalowania automatycznego. Po spełnieniu warunków hello tooscale w górę lub w dół, hello start i Zakończono powodzeniem lub niepowodzeniem zdarzenia są rejestrowane w tej kategorii.
* **Zalecenie** — ta kategoria zawiera zalecenia zdarzenia z określonych typów zasobów, takich jak witryny sieci web i serwerami programu SQL Server. Zdarzenia te oferują zalecenia dotyczące sposobu toobetter wykorzystanie zasobów. Jeśli masz zasoby, które Emituj zalecenia tylko odbierać zdarzenia tego typu.
* **Zasady zabezpieczeń i kondycja zasobów** -tych kategorii nie zawierają żadnych zdarzeń; są one zarezerwowane do użytku w przyszłości.

## <a name="event-schema-per-category"></a>Schemat zdarzenia według kategorii
[Zobacz ten artykuł toounderstand hello dziennik aktywności zdarzeń schemat według kategorii.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>Co można zrobić hello dziennik aktywności
Poniżej podano niektóre czynności hello, które można wykonać za pomocą hello dziennik aktywności:

![Dziennik aktywności platformy Azure](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* Zapytania i wyświetlać go w hello **portalu Azure**.
* [Utwórz alert na zdarzenie dziennika aktywności.](monitoring-activity-log-alerts.md)
* [Strumienia go tooan **Centrum zdarzeń** ](monitoring-stream-activity-logs-event-hubs.md) dla wprowadzanie przez usługi innej firmy lub rozwiązania analizy niestandardowych, takich jak usługi Power BI.
* Analizować w usługi Power BI przy użyciu hello [ **pakiet zawartości usługi Power BI**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).
* [Zapisz go tooa **konta magazynu** inspekcji archiwizacji lub ręcznie](monitoring-archive-activity-log.md). Można określić hello czas przechowywania (w dniach) przy użyciu hello **profilu dziennika**.
* Zapytanie go za pomocą polecenia Cmdlet programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST.

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>Zapytanie hello dziennik aktywności w hello portalu Azure
W ramach hello portalu Azure można wyświetlić dziennik aktywności w kilku miejscach:
* Witaj **bloku dziennika aktywności**, otwieranego wyszukując hello dziennik aktywności w obszarze "Więcej usług" w okienku nawigacji po lewej stronie powitania.
* Witaj **bloku Monitor**, która jest wyświetlana w okienku nawigacji po lewej stronie powitania domyślnie. Dziennik aktywności Hello jest jedną sekcję tego bloku Azure Monitor.
* Dowolnego zasobu **bloku zasobów**, na przykład hello blok konfiguracji maszyny wirtualnej. Hello dziennik aktywności jest sekcji hello na większości tych blokach zasobów i kliknięcie jej automatycznie filtruje zdarzenia hello toothose powiązane toothat określonego zasobu.

W portalu Azure hello można filtrować dziennik aktywności przez te pola:
* TimeSpan — Witaj początkową i końcową czasu zdarzeń.
* Kategoria — Kategoria zdarzenia hello zgodnie z powyższym opisem.
* Subskrypcja — co najmniej jedną nazwę subskrypcji platformy Azure.
* Grupa zasobów — co najmniej jeden zasób grupuje się w tych subskrypcjach.
* Zasób (nazwa) — nazwa hello określonego zasobu.
* Typ zasobu — Witaj typ zasobu, na przykład Microsoft.Compute/virtualmachines.
* Operacja nazwa hello operacji usługi Azure Resource Manager, na przykład Microsoft.SQL/servers/Write.
* Ważność — poziom ważności hello hello zdarzenia (krytyczny komunikat informacyjny, ostrzeżenie, błąd,).
* Zdarzenie inicjowane przez - wywołującego"hello" lub użytkownik, który wykonał hello operacji.
* Otwórz wyszukiwanie — jest to pole wyszukiwania tekstu Otwórz szuka tego ciągu we wszystkich pól w wszystkie zdarzenia.

Po zdefiniowaniu zestaw filtrów można zapisać go jako kwerendę, która jest zachowywane między sesjami, jeśli kiedykolwiek zajdzie tooperform hello samo zapytanie z tych filtrów ponownie w przyszłości hello. Możesz również przypiąć zapytania tooyour pulpitu nawigacyjnego Azure tooalways zachować oka na określone zdarzenia.

Klikając przycisk "Zastosuj" uruchamia kwerendy i Pokaż wszystkie zdarzenia dopasowania. Kliknięcie dowolnego zdarzenia na liście hello pokazuje hello podsumowanie tego zdarzenia, a także hello pełnej nieprzetworzone dane JSON tego zdarzenia.

Jeszcze więcej zasilania, możesz kliknąć hello **wyszukiwania dziennika** ikony, który zawiera dane dziennika aktywności w hello [rozwiązania analizy dziennika aktywności analizy dziennika](../log-analytics/log-analytics-activity.md). blok dziennika aktywności Hello umożliwia podstawowe filtru/przeglądania dzienników, ale umożliwia analizy dzienników toopivot można wysyłać zapytania i wizualizować dane w bardziej wydajny sposób.

## <a name="export-hello-activity-log-with-a-log-profile"></a>Hello Eksport dziennika aktywności z profilem dziennika
A **profilu dziennika** kontroluje sposób eksportowania jest dziennik aktywności. Przy użyciu profilu dziennika, można skonfigurować:

* Gdzie mają być wysyłane hello dziennik aktywności (konta magazynu lub Event Hubs)
* Kategorie zdarzeń (Akcja zapisu, usuwanie i) powinny być przesyłane. *różni się znaczenie Hello "kategorii" w profilach dziennika i dziennik zdarzeń. W profilu dziennika hello "Kategorii" reprezentuje typ operacji hello (Akcja zapisu, usuwanie i). W przypadku dziennika aktywności właściwości "kategorii" hello reprezentuje hello źródła lub typu zdarzenia (na przykład administracji, ServiceHealth Alert i więcej).*
* Regiony (lokalizacja) powinny być wyeksportowane. Należy wprowadzić tooinclude się "globalne" wiele zdarzeń w hello dziennik aktywności są globalne zdarzenia.
* Jak długo hello dziennik aktywności powinny być przechowywane na koncie magazynu.
    - Przechowywanie 0 oznacza, że dzienniki są przechowywane w nieskończoność. W przeciwnym razie wartość hello może być dowolną liczbę dni od 1 do 2147483647.
    - Jeśli zasady przechowywania są skonfigurowane, ale przechowywanie dzienniki na koncie magazynu jest wyłączone (na przykład, jeśli tylko opcje usługi Event Hubs lub OMS są zaznaczone), zasad przechowywania hello nie obowiązują.
    - Zasady przechowywania są stosowane na dzień, więc na powitania koniec dnia (UTC), rejestruje od dnia hello, która jest teraz poza zasady przechowywania hello są usuwane. Na przykład jeśli masz zasady przechowywania jeden dzień początku hello dzisiaj dzień hello hello dzienniki hello dzień przed wczoraj zostaną usunięte.

Możesz użyć konta magazynu lub przestrzeni nazw do Centrum zdarzeń, która nie znajduje się w tej samej subskrypcji Witaj, zgodnie z jedną emitowanie dzienniki hello. Witaj, użytkownik konfiguruje ustawienie hello musi mieć hello odpowiednie RBAC dostępu tooboth subskrypcji.

Te ustawienia można skonfigurować przy użyciu opcji "Eksportuj" hello, w bloku dziennika aktywności hello w portalu hello. Ich można również skonfigurować programowo [przy użyciu hello interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931927.aspx), poleceń cmdlet programu PowerShell lub interfejsu wiersza polecenia. Subskrypcja może mieć tylko jeden profil dziennika.

### <a name="configure-log-profiles-using-hello-azure-portal"></a>Konfigurowanie profilów dziennika przy użyciu hello portalu Azure
Możesz strumienia hello dziennik aktywności tooan Centrum zdarzeń lub przechowywać je w ramach konta magazynu przy użyciu opcji "Eksportuj" hello w hello portalu Azure.

1. Przejdź toohello **dziennik aktywności** przy użyciu hello menu na powitania po lewej stronie portalu hello bloku.

    ![Przejdź tooActivity dziennika w portalu](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Kliknij przycisk hello **wyeksportować** u góry hello hello bloku.

    ![Przycisk Eksportuj w portalu](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. W wyświetlonym bloku hello można wybrać:  
  * regiony, dla których chcesz tooexport zdarzeń
  * Witaj toowhich konto magazynu ma toosave zdarzeń
  * Witaj liczbę dni ma tooretain tych zdarzeń w magazynie. Wartość 0 dni zachowuje dzienniki hello nieskończona.
  * Witaj w którym chcesz toobe Centrum zdarzeń utworzonych dla przesyłania strumieniowego te zdarzenia Namespace magistrali usługi.

     ![Eksport dziennika aktywności bloku](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Kliknij przycisk **zapisać** toosave te ustawienia. Ustawienia Hello są natychmiast być zastosowane tooyour subskrypcji.

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>Konfigurowanie profilów dziennika przy użyciu hello Azure poleceń cmdlet programu PowerShell
#### <a name="get-existing-log-profile"></a>Pobierz profil dziennika
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Dodawanie profilu dziennika
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Właściwość | Wymagane | Opis |
| --- | --- | --- |
| Nazwa |Tak |Nazwa profilu dziennika. |
| StorageAccountId |Nie |Identyfikator zasobu hello konta magazynu toowhich hello dziennik aktywności ma zostać zapisany. |
| serviceBusRuleId |Nie |Identyfikator reguły magistrali usługi dla przestrzeni nazw usługi Service Bus hello ma zostać utworzone w usłudze event hubs toohave. Ciąg w formacie: `{service bus resource ID}/authorizationrules/{key name}`. |
| Lokalizacje |Tak |Rozdzielana przecinkami lista regionów, dla których chcesz toocollect dziennik zdarzeń. |
| retentionInDays |Tak |Liczba dni dla zdarzenia, które mają być przechowywane, od 1 do 2147483647. Wartość zero przechowuje dzienniki hello nieskończoność (zawsze). |
| Kategorie |Nie |Rozdzielana przecinkami lista kategorii zdarzeń, które powinny być zbierane. Możliwe wartości to zapisu, usuwania i akcji. |

#### <a name="remove-a-log-profile"></a>Usuń profil dziennika
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>Konfigurowanie profilów dziennika hello Using Azure CLI między platformami
#### <a name="get-existing-log-profile"></a>Pobierz profil dziennika
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
Witaj `name` właściwość powinna być nazwą hello profilu dziennika.

#### <a name="add-a-log-profile"></a>Dodawanie profilu dziennika
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Właściwość | Wymagane | Opis |
| --- | --- | --- |
| name |Tak |Nazwa profilu dziennika. |
| storageId |Nie |Identyfikator zasobu hello konta magazynu toowhich hello dziennik aktywności ma zostać zapisany. |
| serviceBusRuleId |Nie |Identyfikator reguły magistrali usługi dla przestrzeni nazw usługi Service Bus hello ma zostać utworzone w usłudze event hubs toohave. Ciąg w formacie: `{service bus resource ID}/authorizationrules/{key name}`. |
| Lokalizacje |Tak |Rozdzielana przecinkami lista regionów, dla których chcesz toocollect dziennik zdarzeń. |
| retentionInDays |Tak |Liczba dni dla zdarzenia, które mają być przechowywane, od 1 do 2147483647. Wartość zero przechowuje dzienniki hello nieskończoność (zawsze). |
| Kategorie |Nie |Rozdzielana przecinkami lista kategorii zdarzeń, które powinny być zbierane. Możliwe wartości to zapisu, usuwania i akcji. |

#### <a name="remove-a-log-profile"></a>Usuń profil dziennika
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się więcej o hello dziennik aktywności (dawniej dzienników inspekcji)](../azure-resource-manager/resource-group-audit.md)
* [Strumienia tooEvent dziennika aktywności platformy Azure hello koncentratory](monitoring-stream-activity-logs-event-hubs.md)
