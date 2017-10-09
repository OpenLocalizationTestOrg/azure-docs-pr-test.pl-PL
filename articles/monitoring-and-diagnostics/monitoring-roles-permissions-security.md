---
title: "aaaGet pracę z ról, uprawnienia i zabezpieczeń z monitorem Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wbudowane role i uprawnienia toorestrict toouse Azure Monitor dostęp do zasobów toomonitoring."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Rozpoczynanie pracy z rolami, uprawnienia i zabezpieczeń z monitorem Azure
Wiele zespołów muszą toostrictly regulowania dostępu toomonitoring danych i ustawień. Na przykład, jeśli masz członków zespołu, którzy używają wyłącznie na monitorowanie (pracowników działu pomocy technicznej, metodyki devops engineers) lub korzystając z dostawcą usługi zarządzanej, możesz je dostęp do danych monitorowania, jednocześnie ograniczając toocreate ich możliwości tooonly toogrant, należy zmodyfikować, lub Usuwanie zasobów. W tym artykule przedstawiono sposób tooquickly zastosować wbudowane monitorowania RBAC roli tooa użytkownika na platformie Azure lub tworzenie własnych niestandardowych ról dla użytkownika, który wymaga ograniczonych uprawnień monitorowania. Następnie omówiono zagadnienia dotyczące zabezpieczeń dla zasobów związanych z monitora Azure i w jaki sposób można ograniczyć dostęp do danych toohello zawierają.

## <a name="built-in-monitoring-roles"></a>Wbudowane role monitorowania
Azure Monitor wbudowane role są odpowiedzialne za monitorowanie infrastruktury tooobtain tooresources dostępu limit toohelp zaprojektowane w ramach subskrypcji, umożliwiając nadal i skonfiguruj hello danych, które są im potrzebne. Azure Monitor oferuje dwie role poza pole: czytnik monitorowania i współautor monitorowania.

### <a name="monitoring-reader"></a>Czytnik monitorowania
Osoby przypisać rolę czytelnika monitorowania hello można wyświetlić wszystkie dane monitorowania w ramach subskrypcji, ale nie można zmodyfikować dowolnego zasobu ani edytować żadnych zasobów toomonitoring powiązane ustawienia. Ta rola jest odpowiednia dla użytkowników w organizacji, takich jak inżynierów pomocy technicznej lub operacji wymagających toobe możliwość:

* Wyświetlać pulpity nawigacyjne monitorowania w portalu hello i tworzyć własne prywatne pulpity nawigacyjne monitorowania.
* Zapytanie o metryki przy użyciu hello [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931930.aspx), [poleceń cmdlet programu PowerShell](insights-powershell-samples.md), lub [interfejsu wiersza polecenia i platform](insights-cli-samples.md).
* Zapytanie hello dziennik aktywności za pomocą portalu hello, interfejsu API REST Monitor Azure, poleceń cmdlet programu PowerShell lub interfejsu wiersza polecenia i platform.
* Widok hello [ustawień diagnostycznych](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) dla zasobu.
* Widok hello [dziennika profilu](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) dla subskrypcji.
* Wyświetl ustawienia skalowania automatycznego.
* Widok alertów działania i ustawienia.
* Dostęp do danych usługi Application Insights i wyświetlanie danych w module analiz AI.
* Wyszukiwanie w tym dane użycia dla obszaru roboczego hello danych obszaru roboczego analizy dzienników (OMS).
* Wyświetlanie grup zarządzania analizy dzienników (OMS).
* Pobieranie schematu wyszukiwania hello analizy dzienników (OMS).
* Lista pakietów analizy analizy dzienników (OMS).
* Pobierz i wykonać analizy dzienników (OMS) zapisane wyszukiwania.
* Pobieranie konfiguracji magazynu analizy dzienników (OMS) hello.

> [!NOTE]
> Ta rola nie daje dostęp do odczytu toolog dane, które zostało Centrum zdarzeń tooan przesyłanej strumieniowo lub przechowywane na koncie magazynu. [Zobacz poniżej](#security-considerations-for-monitoring-data) informacji na temat konfigurowania dostępu toothese zasobów.
> 
> 

### <a name="monitoring-contributor"></a>Monitorowanie współautora
Osoby przypisane hello monitorowania współautora roli można wyświetlić wszystkie dane monitorowania w ramach subskrypcji i utworzyć lub ustawień monitorowania, ale nie można modyfikować żadnych innych zasobów. Ta rola jest nadzbiorem rolę czytelnika monitorowania hello i jest odpowiednia dla członków zespołu monitorowania lub dostawcy usług zarządzanych, potrzebują, oprócz uprawnień toohello powyżej, również toobe możliwość organizacji:

* Pulpity nawigacyjne monitorowania należy opublikować jako udostępnionego pulpitu nawigacyjnego.
* Ustaw [ustawień diagnostycznych](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) dla resource.*
* Zestaw hello [dziennika profilu](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) dla subscription.*
* Ustaw działania alertów i ustawienia.
* Tworzenie testów sieci web usługi Application Insights i składniki.
* Obszar roboczy analizy dzienników (OMS) listy udostępnionych kluczy.
* Włącz lub wyłącz pakiety analizy analizy dzienników (OMS).
* Tworzenie i usuwanie i wykonywanie analizy dzienników (OMS) zapisane wyszukiwania.
* Tworzenie i usuwanie konfiguracji magazynu analizy dzienników (OMS) hello.

* użytkownika również oddzielnie musi dysponować uprawnieniami ListKeys na powitania docelowych zasobów (magazynu konta lub zdarzenia koncentratora przestrzeń nazw) tooset profilu dziennika lub ustawienie diagnostyczne.

> [!NOTE]
> Ta rola nie daje dostęp do odczytu toolog dane, które zostało Centrum zdarzeń tooan przesyłanej strumieniowo lub przechowywane na koncie magazynu. [Zobacz poniżej](#security-considerations-for-monitoring-data) informacji na temat konfigurowania dostępu toothese zasobów.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>Monitorowanie uprawnienia i niestandardowe role RBAC
Jeśli hello powyżej wbudowane role nie spełniają wymagań dokładne hello zespołu, możesz [utworzenia niestandardowej roli zabezpieczeń RBAC](../active-directory/role-based-access-control-custom-roles.md) z bardziej szczegółowe uprawnienia. Poniżej przedstawiono hello typowych operacji Azure RBAC monitora z ich opisy.

| Operacja | Opis |
| --- | --- |
| Usuń Microsoft.Insights/AlertRules/[Read, zapisu] |Odczyt/zapis/usuwania reguł alertów. |
| Microsoft.Insights/AlertRules/Incidents/Read |Lista zdarzeń (Historia hello reguły alertów są wyzwalane) dla reguł alertów. Dotyczy to tylko toohello portalu. |
| Usuń Microsoft.Insights/AutoscaleSettings/[Read, zapisu] |Ustawienia skalowania automatycznego odczytu/zapisu/usuwania. |
| Usuń Microsoft.Insights/DiagnosticSettings/[Read, zapisu] |Ustawienia diagnostyki odczytu/zapisu/usuwania. |
| Microsoft.Insights/eventtypes/digestevents/Read |To uprawnienie jest wymagane dla użytkowników, którzy wymagają dostępu tooActivity dzienniki za pośrednictwem portalu hello. |
| Microsoft.Insights/eventtypes/values/Read |Wyświetl zdarzenia dziennika aktywności (zdarzeń zarządzania) w ramach subskrypcji. To uprawnienie jest zastosowanie tooboth dostęp programistyczny i portalu toohello dziennik aktywności. |
| Microsoft.Insights/LogDefinitions/Read |To uprawnienie jest wymagane dla użytkowników, którzy wymagają dostępu tooActivity dzienniki za pośrednictwem portalu hello. |
| Microsoft.Insights/MetricDefinitions/Read |Odczytaj definicje metryki (listy dostępnych typów metryki dla zasobu). |
| Microsoft.Insights/Metrics/Read |Odczytać metryki dla zasobu. |

> [!NOTE]
> Tooalerts dostępu, ustawienia diagnostyki i metryki dla zasobu wymaga tego użytkownika hello ma typ zasobu toohello dostęp do odczytu i zakres tego zasobu. Tworzenie ("zapis") profil diagnostyczny ustawienie lub dziennika czy archiwa tooa magazynu konta lub strumieni tooevent koncentratory wymaga hello tooalso użytkownika ma uprawnienia ListKeys na powitania zasobu docelowego.
> 
> 

Przy użyciu hello powyżej tabeli można na przykład utworzyć niestandardowej roli zabezpieczeń RBAC dla "działania czytnik dziennika" następująco:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Zagadnienia dotyczące zabezpieczeń dla danych monitorowania
Dane monitorowania — szczególnie pliki dziennika — mogą zawierać poufne informacje, takie jak adresy IP lub nazwy użytkownika. Monitorowanie danych z platformy Azure składa się z trzech podstawowych formularzy:

1. Witaj dziennika aktywności, który opisuje wszystkie akcje płaszczyzny kontroli w ramach subskrypcji platformy Azure.
2. Dzienniki diagnostyczne, które są emitowane przez zasób dzienników.
3. Metryki, które są emitowane przez zasoby.

Wszystkie trzy typy danych mogą być przechowywane na koncie magazynu lub przesyłane strumieniowo tooEvent koncentratora, które są ogólnego przeznaczenia zasobów platformy Azure. Ponieważ są to zasoby ogólnego przeznaczenia, tworzenie, usuwanie i uzyskiwanie dostępu do nich jest uprzywilejowana operacja zazwyczaj zastrzeżone przez administratora. Zalecamy używanie hello następujące wskazówki dotyczące zasobów związanych z monitorowaniem tooprevent nadużycia:

* Użyj konta magazynu jednego, przeznaczonego dla danych monitorowania. Tooseparate monitorowania danych do wielu kont magazynu, należy nigdy nie udostępniaj użycia konta magazynu między monitorowania i -monitorowania danych, jak to przypadkowo może dać tych, którzy tylko muszą uzyskać dostęp do danych toomonitoring (np. SIEM innych firm) dostęp do danych monitorowania toonon.
* Użyj jednego, przeznaczonego nazw usługi Service Bus lub Centrum zdarzeń na wszystkich ustawień diagnostycznych dla tej samej przyczyny jak wyżej hello.
* Ograniczenie konta dostępu do magazynu powiązane toomonitoring lub usługi event hubs trzymając je w oddzielnej grupie zasobów, i [Użyj zakresu](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) na poszczególnych ról monitorowania toolimit dostęp tooonly tej grupy zasobów.
* Nigdy nie należy udzielić uprawnień ListKeys hello konta magazynu lub centra zdarzeń w zakresie subskrypcji, gdy użytkownik potrzebuje tylko dane toomonitoring dostępu. Zamiast tego należy podać te uprawnienia użytkownika toohello na zasób lub grupa zasobów (Jeśli masz dedykowane monitorowania grupy zasobów) zakresu.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Ograniczenie konta dostępu do magazynu powiązane toomonitoring
Gdy użytkownik lub aplikacja potrzebuje dostęp do danych toomonitoring na koncie magazynu, należy [Generowanie sygnatury dostępu Współdzielonego konta](https://msdn.microsoft.com/library/azure/mt584140.aspx) na koncie magazynu hello zawierający dane monitorowania z magazynem tooblob dostępu tylko do odczytu na poziomie usługi. W programie PowerShell może to wyglądać tak:

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

Można następnie przekazać hello tokenu toohello jednostki, która wymaga tooread z tego konta magazynu i można wyświetlić listę i odczytywać wszystkie obiekty BLOB na tym koncie magazynu.

Alternatywnie należy toocontrol to uprawnienie z RBAC można przyznać hello tej jednostki Microsoft.Storage/storageAccounts/listkeys/action uprawnień na tym koncie magazynu określonym. Jest to niezbędne do użytkowników, którzy potrzebują tooset stanie toobe diagnostycznych ustawienie lub dziennika profilu tooarchive tooa konta magazynu. Na przykład można utworzyć powitania po niestandardowe role RBAC dla użytkownika lub aplikacji, która potrzebuje tylko tooread z jedno konto magazynu:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> Witaj uprawnienia ListKeys umożliwia klucze konta magazynu podstawowych i pomocniczych hello hello użytkownika toolist. Te klucze udzielanie użytkownikowi hello wszystkie podpisane uprawnienia (Odczyt, zapis, tworzenie obiektów blob, Usuń obiekty BLOB itp.) we wszystkich podpisany usług (obiektu blob, kolejki, tabeli, plik) na tym koncie magazynu. Zalecamy używanie sygnatury dostępu Współdzielonego konta opisane powyżej, gdy jest to możliwe.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Ograniczanie dostępu centra zdarzeń związanych z toomonitoring
Z usługą event hubs można wykonać tego samego typu, ale najpierw należy toocreate dedykowanych reguły autoryzacji nasłuchiwania. Jeśli chcesz toogrant dostępu tooan aplikacji, która musi tylko centra zdarzeń związanych z toomonitoring toolisten hello następujące:

1. Utwórz zasady dostępu współużytkowanego na powitania koncentratory zdarzeń, które zostały utworzone dla strumienia danych monitorowania z tylko oświadczenia nasłuchiwania. Można to zrobić w portalu hello. Na przykład użytkownik może wywołać ją "monitoringReadOnly." Jeśli to możliwe należy toogive klucza bezpośrednio toohello konsumenta i Pomiń hello następnego kroku.
2. Jeśli powitania klienta wymaga toobe tooget stanie hello klucza ad hoc, przyznaj hello hello ListKeys akcja ze strony użytkownika dla tego Centrum zdarzeń. To jest również dla użytkowników, którzy muszą tooset stanie toobe ustawienie diagnostyczne lub logowania koncentratory tooevent toostream profilu. Na przykład można utworzyć regułę RBAC:
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Następne kroki
* [Przeczytaj informacje o RBAC i uprawnienia w programie Menedżer zasobów](../active-directory/role-based-access-control-what-is.md)
* [Omówienie hello odczytu monitorowania na platformie Azure](monitoring-overview.md)

