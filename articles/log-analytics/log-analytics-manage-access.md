---
title: "obszary robocze aaaManage w portalu OMS Analiza dzienników Azure i hello | Dokumentacja firmy Microsoft"
description: "Obszary robocze, analiza dzienników Azure i hello portalu OMS przy użyciu różnych zadań administracyjnych na użytkowników, kont, obszarów roboczych i Azure mogą zarządzać."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>Zarządzanie obszarami roboczymi

tooLog dostępu toomanage Analytics, możesz wykonać różne zadania administracyjne tooworkspaces pokrewne. W tym artykule przedstawiono najlepsze rozwiązanie porady i procedur toomanage obszarów roboczych. Obszar roboczy jest zasadniczo kontener, który zawiera informacje o koncie i informacje o konfiguracji prostego powitania konta. Wiele obszarów roboczych toomanage różnych zestawów danych, które mają być zbierane z wszystkich lub części infrastruktury IT może użyć lub innych członków organizacji.

toocreate obszaru roboczego, musisz:

1. Mieć subskrypcję platformy Azure.
2. Wybrać nazwę obszaru roboczego.
3. Skojarz hello obszar roboczy w ramach subskrypcji.
4. Wybrać lokalizację geograficzną.

## <a name="determine-hello-number-of-workspaces-you-need"></a>Określ numer hello obszarów roboczych, które są potrzebne
Obszar roboczy jest zasobem platformy Azure i kontener, w którym dane są zbierane, zagregowane, przeanalizowane i przedstawionych w hello portalu Azure.

Może mieć wiele obszarów roboczych na subskrypcję platformy Azure i masz toomore dostępu niż jeden obszar roboczy. Minimalizowanie liczby hello obszarów roboczych pozwala tooquery i skorelowania między hello większość danych, ponieważ nie jest możliwe tooquery przez wiele obszarów roboczych. W tej sekcji opisano, kiedy może być przydatne toocreate więcej niż jeden obszar roboczy.

Obecnie obszar roboczy oferuje następujące możliwości:

* Lokalizacja geograficzna do przechowywania danych
* Poziom szczegółowości rozliczeń
* Izolacja danych
* Możliwość konfiguracji

Oparte na powitania poprzedzających właściwości, można toocreate wiele obszarów roboczych jeśli:

* Globalna firma wymaga, aby jej dane były przechowywane w określonych regionach w celu zachowania poufności danych i ich zgodności z przepisami.
* W przypadku korzystania z usługi Azure i mają transfer danych wychodzących tooavoid opłat dzięki użyciu obszaru roboczego tym samym regionie hello, jak hello zasobów platformy Azure zarządza.
* Potrzebujesz tooallocate opłat toodifferent działów lub grup biznesowych na podstawie ich użycia. Podczas tworzenia obszaru roboczego dla każdego działu lub grupie biznesowej instrukcji Azure rachunku i użycie oddzielnie pokazuje hello opłat dla każdego obszaru roboczego.
* Dostawca usługi zarządzane i potrzebne dane analizy dziennika hello tookeep dla każdego klienta, którymi można zarządzać odizolowane od danych innych klientów.
* Zarządzanie wieloma klientami, i chcesz każdego klienta / dział / biznesowa grupy toosee własne dane, ale nie hello danych dla innych użytkowników.

Podczas korzystania z agentów toocollect danych, możesz [skonfigurować tooone tooreport każdego agenta lub więcej obszarów roboczych](log-analytics-windows-agents.md).

Jeśli używasz programu System Center Operations Manager, jedna grupa zarządzania programu Operations Manager może być połączona tylko z jednym obszarem roboczym. Można zainstalować hello Microsoft Monitoring Agent na komputerach zarządzanych przez program Operations Manager i mają tooboth raport hello — agenta programu Operations Manager i inny obszar roboczy analizy dzienników.

### <a name="workspace-information"></a>Informacje o obszarze roboczym

Można wyświetlić szczegóły dotyczące obszaru roboczego w hello portalu Azure. Można również wyświetlić szczegółowe informacje w portalu OMS hello.

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Wyświetlanie obszaru roboczego informacji w hello portalu Azure

1. Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com) przy użyciu subskrypcji platformy Azure.
2. Na powitania **Centrum** menu, kliknij przycisk **więcej usług** i hello listy zasobów, wpisz **analizy dzienników**. Po rozpoczęciu wpisywania, hello listy filtry oparte na dane wejściowe. Kliknij pozycję **Log Analytics**.  
    ![Centrum platformy Azure](./media/log-analytics-manage-access/hub.png)  
3. W bloku subskrypcji analizy dzienników hello wybierz obszar roboczy.
4. Witaj bloku obszaru roboczego są wyświetlane szczegóły dotyczące hello obszaru roboczego i linki do dodatkowych informacji.  
    ![szczegóły obszaru roboczego](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>Zarządzanie kontami i użytkownikami
Każdy obszar roboczy może mieć wiele skojarzonych z nim kont, a każde konto (konta Microsoft lub konta organizacyjnego) mogą mieć obszarów roboczych toomultiple dostępu.

Domyślnie hello konta Microsoft lub konta organizacyjnego, tworzącą roboczym hello staje się hello administratora hello obszaru roboczego.

Istnieją dwa modele uprawnienie kontrolujące obszaru roboczego analizy dzienników tooa dostępu:

1. Starsze role użytkownika usługi Log Analytics
2. [Dostęp oparty na rolach na platformie Azure](../active-directory/role-based-access-control-configure.md)

Witaj w poniższej tabeli przedstawiono hello dostępu, który można ustawić za pomocą każdego modelu uprawnień:

|                          | Portal usługi Log Analytics | Azure Portal | Interfejs API (w tym program PowerShell) |
|--------------------------|----------------------|--------------|----------------------------|
| Role użytkownika usługi Log Analytics | Tak                  | Nie           | Nie                         |
| Dostęp oparty na rolach na platformie Azure  | Tak                  | Tak          | Tak                        |

> [!NOTE]
> Analizy dzienników jest przenoszona toouse dostępu opartej na rolach na platformie Azure jako model uprawnień hello, zastępując ról użytkownika hello analizy dzienników.
>
>

Witaj starszych ról użytkownika analizy dzienników kontrolować tooactivities dostępu w hello [portalu usługi Analiza dzienników](https://mms.microsoft.com).

Witaj również następujące działania wymagają uprawnień do platformy Azure:

| Akcja                                                          | Wymagane uprawnienia platformy Azure | Uwagi |
|-----------------------------------------------------------------|--------------------------|-------|
| Dodawanie i usuwanie rozwiązań do zarządzania                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| Zmiana warstwy cenowej hello                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| Wyświetlanie danych w hello *kopii zapasowej* i *usługi Site Recovery* Kafelki rozwiązania | Administrator/współadministrator | Wdrożone uzyskuje dostęp do zasobów przy użyciu hello klasycznego modelu wdrażania |
| Tworzenie obszaru roboczego w hello portalu Azure                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>Zarządzanie dostępu tooLog Analytics przy użyciu platformy Azure uprawnień
toogrant dostępu toohello obszaru roboczego analizy dzienników przy użyciu platformy Azure uprawnień, wykonaj kroki hello w [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](../active-directory/role-based-access-control-configure.md).

Platforma Azure ma dwie wbudowane role użytkownika w usłudze Log Analytics:
- Czytelnik usługi Log Analytics
- Współautor usługi Log Analytics

Elementy członkowskie hello *Log Analytics Reader* roli można:
- Wyświetlanie i wyszukiwanie wszystkich monitorowanych danych 
- Widok monitorowania ustawień, takich jak przeglądanie konfiguracji hello diagnostyki Azure wszystkich zasobów platformy Azure.

| Typ    | Uprawnienie | Opis |
| ------- | ---------- | ----------- |
| Akcja | `*/read`   | Możliwość tooview wszystkich zasobów i konfiguracji zasobu. Obejmuje wyświetlanie następujących elementów: <br> Stan rozszerzenia maszyny wirtualnej <br> Konfiguracja diagnostyki platformy Azure dla zasobów <br> Wszystkie właściwości i ustawienia wszystkich zasobów |
| Akcja | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | Możliwość tooperform v2 wyszukiwania dziennika zapytań |
| Akcja | `Microsoft.OperationalInsights/workspaces/search/action` | Możliwość tooperform v1 wyszukiwania dziennika zapytań |
| Akcja | `Microsoft.Support/*` | Możliwość tooopen obsługa przypadków |
|Inne | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | Zapobiega odczytu obszaru roboczego klucza toouse wymagane hello danych interfejsu API i tooinstall agenci |


Elementy członkowskie hello *współautora analizy dziennika* roli można:
- Odczytywanie wszystkich danych monitorowania 
- Tworzenie i konfigurowanie kont usługi Automation
- Dodawanie i usuwanie rozwiązań do zarządzania
- Odczytywanie kluczy kont magazynu 
- Konfigurowanie kolekcji dzienników z usługi Azure Storage
- Edytowanie ustawień monitorowania dla zasobów platformy Azure, w tym:
  - Dodawanie tooVMs rozszerzenia maszyny Wirtualnej hello
  - Konfigurowanie diagnostyki platformy Azure dla wszystkich zasobów platformy Azure

> [!NOTE] 
> Możesz użyć hello tooadd możliwości maszyny wirtualnej rozszerzenia tooa maszyny wirtualnej toogain pełną kontrolę nad maszyną wirtualną.

| Uprawnienie | Opis |
| ---------- | ----------- |
| `*/read`     | Możliwość tooview wszystkich zasobów i konfiguracji zasobu. Obejmuje wyświetlanie następujących elementów: <br> Stan rozszerzenia maszyny wirtualnej <br> Konfiguracja diagnostyki platformy Azure dla zasobów <br> Wszystkie właściwości i ustawienia wszystkich zasobów |
| `Microsoft.Automation/automationAccounts/*` | Możliwość toocreate i konfigurowanie kont automatyzacji platformy Azure, w tym dodawanie i edytowanie elementów runbook |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | Dodawanie, aktualizowanie i usuwanie rozszerzenia maszyny wirtualnej, w tym rozszerzenia programu Microsoft Monitoring Agent hello i hello Agent pakietu OMS dla rozszerzenia systemu Linux |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | Widok hello klucz konta magazynu. Wymagane tooconfigure analizy dzienników tooread dzienniki z kontami magazynu Azure |
| `Microsoft.Insights/alertRules/*` | Dodawanie, aktualizowanie i usuwanie reguł alertu |
| `Microsoft.Insights/diagnosticSettings/*` | Dodawanie, aktualizowanie i usuwanie ustawień diagnostycznych dla zasobów platformy Azure |
| `Microsoft.OperationalInsights/*` | Dodawanie, aktualizowanie i usuwanie konfiguracji dla obszarów roboczych usługi Log Analytics |
| `Microsoft.OperationsManagement/*` | Dodawanie i usuwanie rozwiązań do zarządzania |
| `Microsoft.Resources/deployments/*` | Tworzenie i usuwanie wdrożeń. Wymagane w celu dodawania i usuwania rozwiązań, obszarów roboczych oraz kont usługi Automation |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | Tworzenie i usuwanie wdrożeń. Wymagane w celu dodawania i usuwania rozwiązań, obszarów roboczych oraz kont usługi Automation |

tooadd i Usuń tooa rola użytkownika, konieczne jest toohave `Microsoft.Authorization/*/Delete` i `Microsoft.Authorization/*/Write` uprawnienia.

Użyj tych ról użytkowników toogive na uzyskiwanie dostępu do różnych zakresów:
- Subskrypcja — obszary robocze tooall dostępu hello subskrypcji
- Grupa zasobów — roboczym tooall dostępu w grupie zasobów hello
- Zasób - hello tooonly dostępu określony obszar roboczy

Użyj [role niestandardowe](../active-directory/role-based-access-control-custom-roles.md) toocreate ról hello uprawnienia wymagane.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Role użytkownika platformy Azure oraz role użytkownika portalu usługi Log Analytics
Jeśli masz w Azure co najmniej uprawnienie do odczytu w obszarze roboczym analizy dzienników hello, portalu usługi Analiza dzienników hello można otworzyć, klikając hello **portalu OMS** zadań podczas wyświetlania hello obszaru roboczego analizy dzienników.

Podczas otwierania portalu usługi Analiza dzienników hello, możesz przełączyć toousing hello starszych ról użytkownika analizy dzienników. Jeśli nie masz przypisanie roli w portalu usługi Analiza dzienników hello, hello usługi [kontroli hello Azure uprawnienia w obszarze roboczym hello](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource).
Przypisanie roli w portalu usługi Analiza dzienników hello jest określany przy użyciu w następujący sposób:

| Warunki                                                   | Przypisana rola użytkownika usługi Log Analytics | Uwagi |
|--------------------------------------------------------------|----------------------------------|-------|
| Używane konto należy tooa starszej wersji analizy dzienników roli użytkownika     | Witaj określona rola użytkownika analizy dzienników | |
| Twoje konto nie należy tooa starszej wersji analizy dzienników roli użytkownika <br> Obszar roboczy toohello uprawnień pełnej Azure (`*` uprawnienia <sup>1</sup>) | Administrator ||
| Twoje konto nie należy tooa starszej wersji analizy dzienników roli użytkownika <br> Obszar roboczy toohello uprawnień pełnej Azure (`*` uprawnienia <sup>1</sup>) <br> *nie akcje* elementów `Microsoft.Authorization/*/Delete` i `Microsoft.Authorization/*/Write` | Współautor ||
| Twoje konto nie należy tooa starszej wersji analizy dzienników roli użytkownika <br> Uprawnienia platformy Azure do odczytu | Tylko do odczytu ||
| Twoje konto nie należy tooa starszej wersji analizy dzienników roli użytkownika <br> Uprawnienia platformy Azure są niezrozumiałe | Tylko do odczytu ||
| Zarządzane subskrypcje dostawcy rozwiązań w chmurze (CSP) <br> Witaj konto, które są podpisane za pomocą znajduje się w hello Azure Active Directory połączone toohello roboczym | Administrator | Zwykle powitania klienta dostawcy usług Kryptograficznych |
| Zarządzane subskrypcje dostawcy rozwiązań w chmurze (CSP) <br> Konto Hello są podpisane za pomocą nie jest w obszarze roboczym toohello usługi Azure Active Directory połączone hello | Współautor | Zwykle hello dostawcy usług Kryptograficznych |

<sup>1</sup> odwoływać się za[Azure uprawnienia](../active-directory/role-based-access-control-custom-roles.md) uzyskać więcej informacji o definicji roli. Podczas obliczania ról, Akcja `*` nie jest równoważna wartości zbyt`Microsoft.OperationalInsights/workspaces/*`.

Niektóre punkty tookeep pamiętać o hello portalu Azure:

* Po zarejestrowaniu się w portalu OMS toohello za pomocą http://mms.microsoft.com, zobacz hello **wybierz obszar roboczy** listy. Ta lista zawiera tylko obszary robocze, w których masz rolę użytkownika usługi Log Analytics. obszary robocze hello toosee masz dostęp toowith Azure subskrypcji, należy toospecify dzierżawcy jako część hello adresu URL. Przykład: `mms.microsoft.com/?tenant=contoso.com`. Identyfikator dzierżawy Hello jest często ostatnia część adresu e-mail hello używanej toosign w.
* Jeśli chcesz toonavigate bezpośrednio toousing Azure dostęp do portalu tooa, czy masz uprawnienia, możesz muszą toospecify hello zasobu jako część hello adresu URL. Jego jest możliwe tooget ten adres URL przy użyciu programu PowerShell.

  Na przykład `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  adres URL Hello wygląda następująco:`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>Zarządzanie użytkownikami w portalu OMS hello
Zarządzanie użytkownikami i grupy na powitania **Zarządzanie użytkownikami** kartę w obszarze hello **kont** kartę na stronie ustawień hello.   

![zarządzanie użytkownikami](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>Dodaj użytkownika tooan istniejący obszar roboczy
Użyj hello następujące kroki tooadd obszaru roboczego tooa użytkownika lub grupy.

1. W portalu OMS hello, kliknij przycisk hello **ustawienia** kafelka.
2. Kliknij przycisk hello **kont** a następnie kliknij pozycję hello **Zarządzanie użytkownikami** kartę.
3. W hello **Zarządzanie użytkownikami** wybierz tooadd typu konta hello: **konta organizacyjnego**, **Account Microsoft**, **Microsoft Support**.

   * Jeśli wybierzesz Account firmy Microsoft, wpisz adres e-mail hello hello użytkownika skojarzonego z hello Account Microsoft.
   * Jeśli wybierzesz konto organizacyjne, wprowadź część hello użytkownika / grupy nazwę lub alias e-mail oraz listę zgodnych użytkowników i grup jest wyświetlana w polu listy rozwijanej. Wybierz użytkownika lub grupę.
   * Za pomocą toogive Microsoft Support inżyniera Support firmy Microsoft lub innych Microsoft pracownika tymczasowego dostępu tooyour obszaru roboczego toohelp rozwiązywania problemów.

     > [!NOTE]
     > Aby uzyskać najlepszą wydajność hello, Ogranicz liczbę hello grup usługi Active Directory skojarzonych z jednym toothree konta OMS — jeden dla administratorów: jeden dla współautorów i jeden dla użytkowników tylko do odczytu. Przy użyciu więcej grup może wpłynąć na wydajność hello analizy dziennika.
     >
     >
4. Wybierz typ użytkownika lub grupę tooadd hello: **administratora**, **współautora**, lub **użytkownika tylko do odczytu**.  
5. Kliknij pozycję **Dodaj**.

   W przypadku dodawania konta Microsoft, obszar roboczy hello toojoin zaproszenia są wysyłane wiadomości e-mail toohello, podane. Po hello użytkownik wykonuje instrukcje hello hello zaproszenia toojoin OMS, hello użytkownik może uzyskać dostęp hello obszaru roboczego.
   W przypadku dodawania konta organizacyjnego hello użytkownik może uzyskać dostęp analizy dzienników natychmiast.  

#### <a name="edit-an-existing-user-type"></a>Edytowanie istniejącego typu użytkownika
Możesz zmienić hello Rola konta użytkownika skojarzonego z kontem OMS. Dostępne są następujące opcje roli hello:

* *Administrator*: może zarządzać użytkownikami, wyświetlać wszystkie alerty i wykonywać na nich operacje oraz dodawać i usuwać serwery
* *Współautor*: może wyświetlać wszystkie alerty i wykonywać na nich operacje oraz dodawać i usuwać serwery
* *Użytkownik tylko do odczytu*: użytkownicy oznaczeni jako tylko do odczytu mają następujące ograniczenia:

  1. Nie mogą dodawać ani usuwać rozwiązań. Galeria rozwiązań Hello jest ukryty.
  2. Nie mogą dodawać, modyfikować ani usuwać kafelków na stronie **Mój pulpit nawigacyjny**.
  3. Widok hello **ustawienia** stron. strony Hello są ukryte.
  4. W widoku wyszukiwania hello, konfiguracji usługi Power BI, zapisane wyszukiwania i alerty zadania są ukryte.

#### <a name="tooedit-an-account"></a>tooedit konta
1. W portalu OMS hello, kliknij przycisk hello **ustawienia** kafelka.
2. Kliknij przycisk hello **kont** a następnie kliknij pozycję hello **Zarządzanie użytkownikami** kartę.
3. Wybierz rolę hello hello użytkownika, które mają toochange.
4. Okno dialogowe potwierdzenia hello, kliknij przycisk **tak**.

### <a name="remove-a-user-from-a-workspace"></a>Usuwanie użytkownika z obszaru roboczego
Użyj hello poniższych kroków tooremove użytkownika z obszaru roboczego. Usunięcie użytkownika hello nie zamyka hello obszaru roboczego. Zamiast tego usuwa skojarzenie hello tego użytkownika i hello obszaru roboczego. Jeśli użytkownik jest skojarzony z wiele obszarów roboczych, aby użytkownik mógł nadal Zaloguj tooOMS i wyświetlić ich innych obszarów roboczych.

1. W portalu OMS hello, kliknij przycisk hello **ustawienia** kafelka.
2. Kliknij przycisk hello **kont** a następnie kliknij pozycję hello **Zarządzanie użytkownikami** kartę.
3. Kliknij przycisk **Usuń** dalej toohello nazwę użytkownika, które mają tooremove.
4. Okno dialogowe potwierdzenia hello, kliknij przycisk **tak**.

### <a name="add-a-group-tooan-existing-workspace"></a>Dodaj grupy tooan istniejący obszar roboczy
1. W powyższej sekcji "tooadd użytkownika tooan istniejący obszar roboczy" hello wykonaj kroki 1 – 4.
2. W obszarze **Wybierz użytkownika/grupę** wybierz pozycję **Grupa**.  
   ![Dodaj grupy tooan istniejący obszar roboczy](./media/log-analytics-manage-access/add-group.png)
3. Wprowadź adres E-mail lub nazwa wyświetlana hello hello grupy chcesz tooadd.
4. Wybierz grupę hello hello listy wyników, a następnie kliknij przycisk **Dodaj**.

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>Połącz istniejącą tooan obszaru roboczego subskrypcji platformy Azure
Wszystkie obszary robocze utworzone po 26 września 2016 musi być połączone tooan subskrypcji platformy Azure w czasie tworzenia. Obszary robocze utworzone przed tą datą musi być połączone tooa obszaru roboczego podczas logowania. Po utworzeniu obszaru roboczego hello z hello portalu Azure lub podczas łączenia z obszaru roboczego tooan subskrypcji platformy Azure, Azure Active Directory jest połączony jako konta organizacyjnego.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink tooan obszaru roboczego subskrypcji platformy Azure w portalu OMS hello

- Po zalogowaniu się do portalu OMS hello, to zostanie wyświetlony monit o tooselect subskrypcji platformy Azure. Wybierz subskrypcję hello mają toolink tooyour roboczym, a następnie kliknij przycisk **łącze**.  
    ![łączenie subskrypcji platformy Azure](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > toolink obszaru roboczego konta platformy Azure musi mieć już dostępu toohello roboczym chcesz toolink.  Innymi słowy, hello Użyj hello tooaccess portalu Azure, musi być ono **hello sam** jako konto hello Użyj obszaru roboczego hello tooaccess. Jeśli nie, zobacz [Dodaj użytkownika tooan istniejący obszar roboczy](#add-a-user-to-an-existing-workspace).

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink tooan obszaru roboczego subskrypcji platformy Azure w portalu Azure hello
1. Zaloguj się na powitania [portalu Azure](http://portal.azure.com).
2. Wyszukaj pozycję **Log Analytics** i wybierz ją.
3. Zostanie wyświetlona lista istniejących obszarów roboczych. Kliknij pozycję **Dodaj**.  
   ![lista obszarów roboczych](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. W obszarze **Obszar roboczy pakietu OMS** kliknij pozycję **Lub połącz istniejący**.  
   ![łączenie istniejącego obszaru roboczego](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. Kliknij pozycję **Skonfiguruj wymagane ustawienia**.  
   ![konfigurowanie wymaganych ustawień](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. Zobaczysz hello listę obszarów roboczych, które nie są jeszcze połączone tooyour konto platformy Azure. Wybierz obszar roboczy.  
   ![wybieranie obszarów roboczych](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. W razie potrzeby można zmienić wartości hello następujące elementy:
   * Subskrypcja
   * Grupa zasobów
   * Lokalizacja
   * Warstwa cenowa  
     ![zmienianie wartości](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. Kliknij przycisk **OK**. obszar roboczy Hello jest teraz tooyour połączonego konta platformy Azure.

> [!NOTE]
> Jeśli nie widzisz roboczym hello chcesz toolink, a następnie subskrypcji platformy Azure nie ma dostępu toohello roboczym utworzonej przy użyciu portalu OMS hello.  Zobacz toogrant dostępu toothis konta w portalu OMS hello [Dodaj użytkownika tooan istniejący obszar roboczy](#add-a-user-to-an-existing-workspace).
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>Uaktualnij tooa obszaru roboczego, płatną planu
Dostępne są trzy typy planów obszarów roboczych dla pakietu OMS: **Bezpłatny**, **Autonomiczny** i **OMS**.  Jeśli jesteś na powitania *wolne* plan, jest ograniczona do 500 MB danych na dzień wysyłane tooLog Analytics.  Przekracza tę wartość, należy najpierw toochange Twojego planu tooavoid tooa płatnej obszaru roboczego nie zbiera danych po przekroczeniu tego limitu. Typ planu można zmienić w dowolnym momencie.  Aby uzyskać więcej informacji o cenach pakietu OMS, zobacz [szczegółowe informacje o cenach](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing).

### <a name="using-entitlements-from-an-oms-subscription"></a>Używanie uprawnień z subskrypcji pakietu OMS
toouse hello uprawnień, które pochodzą z zakupem OMS E1, OMS E2 OMS lub OMS dodatek dla programu System Center wybierz hello *OMS* planu analizy dzienników OMS.

W przypadku zakupu subskrypcji na OMS hello uprawnienia są dodawane tooyour umowy Enterprise Agreement. Subskrypcji platformy Azure, który jest tworzony w ramach niniejszej umowy służy hello uprawnień. Wszystkie obszary robocze na te subskrypcje Użyj hello OMS uprawnień.

tooensure, że użycie obszaru roboczego jest uprawnień zastosowanych tooyour z hello OMS subskrypcji, musisz:

1. Tworzenie obszaru roboczego w subskrypcji platformy Azure, który jest częścią hello umowy Enterprise Agreement, zawierającą hello OMS subskrypcji
2. Wybierz hello *OMS* planu dla obszaru roboczego hello

> [!NOTE]
> Jeśli obszar roboczy został utworzony przed 26 września 2016 i jest z analizy dzienników cenową planu *Premium*, a następnie ten obszar roboczy używa uprawnień z hello OMS dodatek dla programu System Center. Umożliwia także uprawnień użytkownika, zmieniając toohello *OMS* warstwy cenowej.
>
>

uprawnienia do subskrypcji OMS Hello nie są widoczne w hello Azure lub w portalu OMS. Widać, uprawnień i użycie hello Enterprise Portal.  

Jeśli potrzebujesz hello toochange subskrypcji platformy Azure, połączonej z obszaru roboczego, można użyć hello Azure PowerShell [AzureRmResource przenoszenia](https://msdn.microsoft.com/library/mt652516.aspx) polecenia cmdlet.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>Korzystanie z zobowiązania platformy Azure w ramach umowy Enterprise Agreement
Jeśli nie masz subskrypcję pakietu OMS, płacisz dla każdego składnika OMS oddzielnie i użycia hello pojawi się na rachunku platformy Azure.

Jeśli masz Azure zobowiązaniom pieniężnym na toowhich rejestracji enterprise hello subskrypcji platformy Azure są połączone, użycie analizy dzienników zostanie automatycznie obciążania przed hello pozostałych pieniężnego zatwierdzania.

Jeśli potrzebujesz toochange hello subskrypcji Azure, która hello obszaru roboczego jest połączony, możesz użyć hello Azure PowerShell [AzureRmResource przenoszenia](https://msdn.microsoft.com/library/mt652516.aspx) polecenia cmdlet.  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>Zmień tooa obszaru roboczego, płatną warstwy cenowej w hello portalu Azure
1. Zaloguj się na powitania [portalu Azure](http://portal.azure.com).
2. Wyszukaj pozycję **Log Analytics** i wybierz ją.
3. Zostanie wyświetlona lista istniejących obszarów roboczych. Wybierz obszar roboczy.  
4. W bloku obszaru roboczego hello w obszarze **ogólne**, kliknij przycisk **warstwa cenowa**.  
5. W obszarze **Warstwa cenowa** kliknij warstwę cenową, a następnie kliknij przycisk **Wybierz**.  
    ![wybieranie planu](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. Odświeżenie widoku w hello portalu Azure, zobacz **warstwa cenowa** zaktualizowano w celu wybrania warstwy hello.  
    ![zaktualizowany plan](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> Obszar roboczy w przypadku tooan połączonego konta automatyzacji, przed wybraniem hello *autonomiczne (GB na)* warstwy cenowej należy usunąć wszelkie **Automatyzacja i kontrola** rozwiązań i odłączyć hello automatyzacji konto. W bloku obszaru roboczego hello w obszarze **ogólne**, kliknij przycisk **rozwiązań** toosee i usuwania rozwiązania. toounlink hello konta automatyzacji, kliknij nazwę hello hello konta automatyzacji na powitania **warstwa cenowa** bloku.
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>Zmień tooa obszaru roboczego, płatną warstwy cenowej w portalu OMS hello

toochange hello warstwy cenowej za pomocą portalu OMS hello, musisz mieć subskrypcję platformy Azure.

1. W portalu OMS hello, kliknij przycisk hello **ustawienia** kafelka.
2. Kliknij przycisk hello **kont** a następnie kliknij pozycję hello **subskrypcji platformy Azure i Plan danych** kartę.
3. Kliknij przycisk hello ma toouse warstwy cenowej.
4. Kliknij pozycję **Zapisz**.  
   ![subskrypcja i plany taryfowe](./media/log-analytics-manage-access/subscription-tab.png)

Nowy plan danych jest wyświetlany w hello wstążki portalu OMS u góry hello strony sieci web.

![Wstążka pakietu OMS](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Zmiana czasu przechowywania danych przez usługę Log Analytics

Na powitania bezpłatnej warstwy cenowej analizy dzienników sprawia, że dostępne hello ostatnich siedmiu dni danych.
W warstwie cenowej standardowa hello analizy dzienników sprawia, że dostępne hello ostatnich 30 dni danych.
W warstwie cenowej Premium hello analizy dzienników sprawia, że dostępne hello ostatnich 365 dni danych.
Na powitania autonomicznych i OMS ceny warstw, domyślnie analizy dzienników sprawia, że dostępne hello ostatnich 31 dni danych.

Gdy używasz hello autonomicznych i OMS warstw cenowych, można nadąża lat too2 danych (730 dni). Dane przechowywane dłużej niż domyślne hello 31 dni wiąże opłat przechowywania danych. Aby uzyskać więcej informacji na temat cen, zobacz [opłaty za użycie nadwyżkowe](https://azure.microsoft.com/pricing/details/log-analytics/).

Długość hello toochange przechowywanie danych:

1. Zaloguj się na powitania [portalu Azure](http://portal.azure.com).
2. Wyszukaj pozycję **Log Analytics** i wybierz ją.
3. Zostanie wyświetlona lista istniejących obszarów roboczych. Wybierz obszar roboczy.  
4. W bloku obszaru roboczego hello w obszarze **ogólne**, kliknij przycisk **przechowywania**.  
5. Użyj tooincrease suwaka hello lub Zmniejsz hello liczba dni przechowywania, a następnie kliknij przycisk **zapisać**.  
    ![zmiana okresu przechowywania](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>Zmienianie organizacji usługi Azure Active Directory dla obszaru roboczego

Organizację usługi Azure Active Directory obszaru roboczego można zmienić. Zmiana hello Azure Active Directory organizacji pozwala tooadd użytkowników i grup z tego obszaru roboczego toohello katalogu.

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>toochange hello Azure Active Directory organizacji obszaru roboczego

1. Na stronie Ustawienia hello w portalu OMS powitania kliknij **kont** , a następnie kliknij przycisk hello **Zarządzanie użytkownikami** kartę.  
2. Przejrzyj hello informacje dotyczące konta organizacyjne, a następnie kliknij przycisk **zmiany organizacji**.  
    ![zmienianie organizacji](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Wprowadź informacje o tożsamości hello hello administratora domeny usługi Azure Active Directory. W efekcie zostanie wyświetlony potwierdzenia stwierdzający, że obszar roboczy jest tooyour połączonej usługi Azure Active Directory domeny.  
    ![potwierdzenie dotyczące połączonego obszaru roboczego](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Usuwanie obszaru roboczego usługi Log Analytics
Po usunięciu obszaru roboczego analizy dzienników wszystkie dane związane z obszaru roboczego tooyour są usuwane z hello usługę w ciągu 30 dni.

Jeśli jesteś administratorem, jest wielu użytkowników skojarzonych z obszarem roboczym hello hello skojarzenie tych użytkowników i hello obszaru roboczego zostało przerwane. Jeśli użytkownicy hello są skojarzone z innych obszarów roboczych, następnie można przejść za pomocą pakietu OMS z tych obszarów roboczych. Jednakże jeżeli nie są one powiązane z innych obszarów roboczych następnie muszą toocreate toouse obszar roboczy OMS.

### <a name="toodelete-a-workspace"></a>toodelete obszaru roboczego
1. Zaloguj się na powitania [portalu Azure](http://portal.azure.com).
2. Wyszukaj pozycję **Log Analytics** i wybierz ją.
3. Zostanie wyświetlona lista istniejących obszarów roboczych. Wybierz obszar roboczy hello, które mają toodelete.
4. W bloku hello obszaru roboczego kliknij **usunąć**.  
    ![usuwanie](./media/log-analytics-manage-access/delete-workspace01.png)
5. W hello usuwanie obszaru roboczego okno dialogowe potwierdzenia, kliknij przycisk **tak**.

## <a name="next-steps"></a>Następne kroki
* Zobacz [tooLog komputerów Windows połączyć Analytics](log-analytics-windows-agents.md) tooadd agentów i zebrać dane.
* [Dodawanie rozwiązania analizy dzienników z galerii rozwiązań hello](log-analytics-add-solutions.md) tooadd funkcjonalność i zbieranie danych.
* [Skonfiguruj ustawienia serwera proxy i zapory w analizy dzienników](log-analytics-proxy-firewall.md) Jeśli organizacja używa serwera proxy lub zapory, dzięki czemu agenci mogą komunikować się z hello usługi analizy dzienników.
