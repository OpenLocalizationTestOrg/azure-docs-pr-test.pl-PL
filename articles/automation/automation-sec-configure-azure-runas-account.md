---
title: aaaConfigure Azure konto Uruchom jako dla | Dokumentacja firmy Microsoft
description: "Ten samouczek przedstawia hello tworzenie, testowanie i przykład uwierzytelnianie przy użyciu podmiotu zabezpieczeń w automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "nazwa główna usługi, setspn, uwierzytelnianie azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Uwierzytelnianie elementów runbook przy użyciu konta Uruchom jako platformy Azure
W tym artykule opisano, jak konto tooconfigure usługi Automatyzacja Azure hello portalu Azure. toodo tak, hello Uruchom jako konta funkcji tooauthenticate elementy runbook służą zarządzania zasobami Azure Resource Manager lub zarządzania usługami Azure.

Podczas tworzenia konta automatyzacji w portalu Azure hello, można automatycznie utworzyć dwa konta:

* Konto Uruchom jako. To konto służy do tworzenia nazwy głównej usługi w usłudze Azure Active Directory (Azure AD) oraz certyfikatu. Przypisuje hello współautora opartej na rolach kontroli dostępu (RBAC), która zarządza zasoby usługi Resource Manager za pomocą elementów runbook.
* Klasyczne konto Uruchom jako. To konto przekazywanie certyfikatu zarządzania, który jest używany toomanage zarządzania usługami lub zasoby klasyczne za pomocą elementów runbook.

Tworzenie konta upraszcza proces hello i pomaga szybko rozpocząć tworzenie i wdrażanie toosupport elementów runbook usługi Automatyzacja z automatyzacji musi.

Używając konta Uruchom jako i klasycznego konta Uruchom jako, możesz:

* Podaj tooauthenticate sposób Zestandaryzowany z usługi Azure Resource Manager lub usługi zarządzania zasobami w przypadku zarządzania z poziomu elementów runbook w portalu Azure hello.
* Użyj hello globalne elementy runbook, które można skonfigurować w alertach Azure do automatyzacji procesu.

> [!NOTE]
> Witaj [Azure alertu funkcji integracji](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) automatyzacji elementów runbook globalnego wymaga konto automatyzacji, który skonfigurowano konto Uruchom jako i konto klasycznego Uruchom jako. Można wybrać konto automatyzacji, który został już zdefiniowany konta Uruchom jako i klasycznego Uruchom jako lub toocreate można wybrać nowe konto automatyzacji.
>  

W tym artykule przedstawiono sposób toocreate konto usługi Automatyzacja z hello portalu Azure, zaktualizuj konto automatyzacji za pomocą programu Azure PowerShell, zarządzanie konfiguracją konta hello i uwierzytelnić się w elementach runbook.

Przed rozpoczęciem tworzenia konta automatyzacji jest toounderstand dobrze i należy wziąć pod uwagę następujące hello:

* Tworzenie konta automatyzacji nie ma wpływu na kont automatyzacji, który może zostały już utworzone w klasycznym hello lub modelu wdrażania usługi Resource Manager.
* proces Hello działa tylko w przypadku kont automatyzacji, tworzone w hello portalu Azure. Próba toocreate konta z hello klasycznego portalu Azure nie jest replikowany hello Konfiguracja Uruchom jako konta.
* Jeśli masz już elementy runbook i zasoby (na przykład harmonogramy lub zmienne) w zasoby klasyczne toomanage miejsca, i chcesz tooauthenticate elementów runbook z hello nowego klasycznego konta Uruchom jako, wykonaj jedną z następujących hello:

  * toocreate klasycznego konta Uruchom jako, wykonaj instrukcje hello w sekcji "Zarządzanie Twoje konto Uruchom jako" hello. 
  * tooupdate istniejącego konta, użyj hello PowerShell skryptu w sekcji "Aktualizuj Twoje konto usługi Automatyzacja przy użyciu programu PowerShell" hello.
* tooauthenticate przy użyciu hello nowego konta Uruchom jako i konto klasycznego Uruchom jako automatyzacji, należy toomodify istniejące elementy runbook z hello przykładowy kod podany w sekcji hello [przykłady kodu uwierzytelniania](#authentication-code-examples).

    >[!NOTE]
    >Hello konta Uruchom jako jest uwierzytelniania przy użyciu nazwy głównej usługi oparte na certyfikatach hello zasoby usługi Resource Manager. Witaj konto klasycznego Uruchom jako jest do uwierzytelniania względem zasobów usługi zarządzania z certyfikatem zarządzania.

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Utwórz konto automatyzacji z hello portalu Azure
W tej sekcji utworzysz konto usługi Automatyzacja Azure z hello portalu Azure, który z kolei tworzy zarówno konto Uruchom jako, jak i konto klasycznego Uruchom jako.

>[!NOTE]
>toocreate konto usługi Automatyzacja, musi być członkiem roli Administratorzy usługi hello lub współadministratorem subskrypcji hello, która udziela dostępu toohello subskrypcji. Należy również dodać jako subskrypcji toothat użytkownika domyślnego wystąpienia usługi Active Directory. konta Hello toobe przypisane do ról uprzywilejowanych nie jest konieczne.
>
>Jeśli nie jesteś członkiem wystąpienia usługi Active Directory hello subskrypcji przed dodaniem roli administratora współpracującego toohello hello subskrypcji, użytkownik zostanie dodany tooActive katalogu jako Gość. W takim przypadku otrzymasz "nie ma uprawnień toocreate..." Ostrzeżenie dotyczące hello **Dodaj konto automatyzacji** bloku.
>
>Użytkownicy, którzy dodano rolę administratora współpracującego toohello najpierw można usunąć z wystąpienia usługi Active Directory hello subskrypcji i ponownie dodany toomake ich pełną użytkownika w usłudze Active Directory. tooverify tej sytuacji z hello **usługi Azure Active Directory** okienku w portalu Azure, wybierając hello **użytkowników i grup**, wybierając żądane **wszyscy użytkownicy** i po wybraniu Witaj określonego użytkownika, wybierając **profilu**. Witaj wartość hello **typ użytkownika** atrybutu na liście profilów użytkowników hello nie powinna być równa **gościa**.
>

1. Zaloguj się w portalu Azure przy użyciu konta, które jest członkiem grupy administratorów subskrypcji hello i współadministratorem subskrypcji hello toohello.

2. Wybierz opcję **Konta automatyzacji**.

3. Na powitania **kont automatyzacji** bloku, kliknij przycisk **Dodaj**.
Witaj **Dodaj konto automatyzacji** zostanie otwarty blok.

 ![Blok "Dodaj konto automatyzacji" Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > Jeśli Twoje konto nie jest członkiem roli Administratorzy subskrypcji hello i współadministratorem subskrypcji hello, hello następujące ostrzeżenie jest wyświetlane na powitania **Dodaj konto automatyzacji** bloku:
   >
   >![Ostrzeżenie podczas dodawania konta usługi Automation](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. Na powitania **Dodaj konto automatyzacji** bloku w hello **nazwa** wpisz nazwę nowego konta automatyzacji.

5. Jeśli masz więcej niż jedną subskrypcję, hello następujące:

    a. W obszarze **subskrypcji**, określ jedną hello nowego konta.

    b. W obszarze **Grupa zasobów** kliknij pozycję **Utwórz nową** lub **Użyj istniejącej**.

    c. W obszarze **Lokalizacja** określ centrum danych platformy Azure.

6. W obszarze **Tworzenie konta Uruchom jako platformy Azure** wybierz pozycję **Tak**, a następnie kliknij pozycję **Utwórz**.

   > [!NOTE]
   > Jeśli wybierzesz nie toocreate hello konta Uruchom jako, wybierając **nr**, zostanie wyświetlony komunikat ostrzegawczy hello **Dodaj konto automatyzacji** bloku. Mimo że hello konto jest tworzone w portalu Azure hello, nie ma odpowiedniego tożsamość uwierzytelniania w ramach Twojej classic lub usługa katalogowa subskrypcji Menedżera zasobów. W rezultacie hello konto ma nie tooresources dostępu w ramach subskrypcji. Ten scenariusz zapobiega sytuacji, w której wszelkie elementy runbook odwołujące się do tego konta miałyby możliwość uwierzytelniania i wykonywania zadań w odniesieniu do zasobów w tych modelach wdrożenia.
   >
   > ![Komunikat ostrzegawczy w bloku "Dodaj konto automatyzacji" hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > Ponadto ponieważ hello nazwy głównej usługi nie jest tworzony, nie jest przypisana rola współautora hello.
   >

7. Gdy Azure tworzy konto automatyzacji hello, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.

### <a name="resources"></a>Zasoby
Po pomyślnym utworzeniu konta automatyzacji hello kilka zasoby są tworzone automatycznie dla Ciebie. zasoby Hello podsumowano w hello następujących tabel:

#### <a name="run-as-account-resources"></a>Zasoby konta Uruchom jako

| Zasób | Opis |
| --- | --- |
| AzureAutomationTutorial Runbook | Przykład graficzny element runbook, który demonstruje sposób tooauthenticate przy użyciu hello konta Uruchom jako i pobiera wszystkie zasoby usługi Resource Manager hello. |
| AzureAutomationTutorialScript Runbook | Runbook programu PowerShell przykładzie pokazano, jak tooauthenticate przy użyciu hello konta Uruchom jako, który pobiera wszystkie zasoby usługi Resource Manager hello. |
| AzureRunAsCertificate | zasób certyfikatu Hello jest tworzony automatycznie podczas tworzenia konta automatyzacji lub użyj następującego skryptu PowerShell do istniejącego konta hello. Hello certyfikatu umożliwia tooauthenticate z platformy Azure, dzięki czemu zasoby usługi Azure Resource Manager można zarządzać z poziomu elementów runbook. Witaj certyfikat ma żywotność jednego roku. |
| AzureRunAsConnection | zasób połączenia Hello jest tworzony automatycznie podczas tworzenia konta automatyzacji lub użyj skryptu programu PowerShell hello do istniejącego konta. |

#### <a name="classic-run-as-account-resources"></a>Zasoby klasycznego konta Uruchom jako

| Zasób | Opis |
| --- | --- |
| AzureClassicAutomationTutorial Runbook | Przykład graficzny element runbook, który pobiera wszystkich maszyn wirtualnych hello, które są tworzone przy użyciu hello klasycznego modelu wdrażania w ramach subskrypcji przy użyciu konta hello klasycznego Uruchom jako (certyfikatów), a następnie zapisuje hello nazwę maszyny Wirtualnej i stanu. |
| AzureClassicAutomationTutorial Script Runbook | Przykład runbook programu PowerShell, która pobiera wszystkie hello klasycznych maszyn wirtualnych w ramach subskrypcji przy użyciu konta hello klasycznego Uruchom jako (certyfikatów), a następnie zapisuje hello nazwę maszyny Wirtualnej i stanu. |
| AzureClassicRunAsCertificate | Witaj, automatycznie tworzony zasób certyfikatu Użyj tooauthenticate z platformy Azure, dzięki czemu można zarządzać Azure zasoby klasyczne z elementów runbook. Witaj certyfikat ma żywotność jednego roku. |
| AzureClassicRunAsConnection | trwały Hello automatycznie utworzone połączenie, użyj tooauthenticate z platformy Azure, dzięki czemu można zarządzać Azure zasoby klasyczne z elementów runbook. |

## <a name="verify-run-as-authentication"></a>Sprawdzanie uwierzytelniania Uruchom jako
Wykonaj tooconfirm teście małych, który może pomyślnie wykonać uwierzytelnienia za pomocą hello nowego konta Uruchom jako.

1. Hello portalu Azure Otwórz konto automatyzacji hello, który został utworzony wcześniej.

2. Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.

3. Wybierz hello **AzureAutomationTutorialScript** runbook, a następnie kliknij przycisk **Start** toostart hello runbook. wykonywane Hello następujące zdarzenia:
 * A [zadanie elementu runbook](automation-runbook-execution.md) utworzeniu hello **zadania** zostanie wyświetlony blok i stan zadania hello jest wyświetlany w hello **Podsumowanie zadania** kafelka.
 * Stan zadania Hello początkowo **w kolejce**, wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne.
 * Stan Hello staje się **uruchamianie** gdy pracownik oświadczeń hello zadania.
 * Stan Hello staje się **systemem** , gdy element runbook hello zacznie działać.
 * Gdy zadanie elementu runbook hello zakończył działanie, powinien zostać wyświetlony stan **Ukończono**.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee hello szczegółowe wyniki hello elementu runbook, kliknij przycisk hello **dane wyjściowe** kafelka.  
Witaj **dane wyjściowe** bloku zostanie wyświetlone hello elementu runbook pomyślnie uwierzytelniony i zwrócona lista wszystkich dostępnych w grupie zasobów hello zasobów.

5. Zamknij hello **dane wyjściowe** toohello tooreturn bloku **Podsumowanie zadania** bloku.

6. Zamknij hello **Podsumowanie zadania** bloku i hello odpowiadającego **AzureAutomationTutorialScript** bloku elementu runbook.

## <a name="verify-classic-run-as-authentication"></a>Sprawdzanie klasycznego uwierzytelniania Uruchom jako
Wykonaj podobne małą test tooconfirm, który może pomyślnie wykonać uwierzytelnienia za pomocą hello nowego klasycznego konta Uruchom jako.

1. Hello portalu Azure Otwórz konto automatyzacji hello, który został utworzony wcześniej.

2. Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.

3. Wybierz hello **AzureClassicAutomationTutorialScript** elementu runbook, a następnie kliknij przycisk **Start** zbyt uruchomić elementu runbook hello. wykonywane Hello następujące zdarzenia:

 * A [zadanie elementu runbook](automation-runbook-execution.md) utworzeniu hello **zadania** zostanie wyświetlony blok i stan zadania hello jest wyświetlany w hello **Podsumowanie zadania** kafelka.
 * Stan zadania Hello początkowo **w kolejce**, wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne.
 * Stan Hello staje się **uruchamianie** gdy pracownik oświadczeń hello zadania.
 * Stan Hello staje się **systemem** , gdy element runbook hello zacznie działać.
 * Gdy zadanie elementu runbook hello zakończył działanie, powinien zostać wyświetlony stan **Ukończono**.

    ![Test elementu Runbook zabezpieczeń](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee hello szczegółowe wyniki hello elementu runbook, kliknij przycisk hello **dane wyjściowe** kafelka.  
Witaj **dane wyjściowe** bloku zostanie wyświetlone pomyślnie uwierzytelniony i zwracane listę wszystkich klasycznych maszyn wirtualnych w subskrypcji hello hello elementu runbook.

5. Zamknij hello **dane wyjściowe** toohello tooreturn bloku **Podsumowanie zadania** bloku.

6. Zamknij hello **Podsumowanie zadania** bloku i hello odpowiadającego **AzureAutomationTutorialScript** bloku elementu runbook.

## <a name="managing-your-run-as-account"></a>Zarządzanie kontem Uruchom jako
W pewnym momencie przed upływem Twoje konto usługi Automatyzacja, konieczne będzie toorenew hello certyfikatu. Jeśli uważasz, że naruszono tego hello konta Uruchom jako, można usunąć i ponownie go utworzyć. W tej sekcji omówiono sposób tooperform te operacje.

### <a name="self-signed-certificate-renewal"></a>Odnawianie certyfikatu z podpisem własnym
Witaj podpisem utworzony certyfikat dla hello konta Uruchom jako wygasa rok z daty utworzenia hello. Można go odnowić w dowolnym momencie przed wygaśnięciem jego ważności. Podczas odnawiania go hello bieżącego prawidłowy certyfikat jest zachowanych tooensure, że wszystkie elementy runbook umieszczonych w kolejce maksymalnie lub aktywnie działa i że uwierzytelniania za pomocą hello konta Uruchom jako nie negatywnie zainfekowane. certyfikat Hello pozostaje ważny aż do daty jego wygaśnięcia.

> [!NOTE]
> Jeśli zostały skonfigurowane z automatyzacji Uruchom jako konta toouse certyfikat wystawiony przez urząd certyfikacji w Twojej organizacji, możesz użyć tej opcji hello firmowy certyfikat zostanie zastąpione przez certyfikatu z podpisem własnym.

Witaj toorenew certyfikatów, hello następujące:

1. Hello portalu Azure Otwórz hello konta automatyzacji.

2. Na powitania **konto automatyzacji** bloku w hello **konta właściwości** okienku w obszarze **ustawienia konta**, wybierz pozycję **konta Uruchom jako**.

    ![Okienko właściwości konta usługi Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. Na powitania **konta Uruchom jako** bloku właściwości, wybierz albo hello Uruchom jako konta lub hello klasycznego konto Uruchom jako ma toorenew hello certyfikat dla.

4. Na powitania **właściwości** bloku hello wybranego konta, kliknij przycisk **odnawiania certyfikatu**.

    ![Odnawianie certyfikatu konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. Gdy hello certyfikat zostanie odnowiony, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.

### <a name="delete-a-run-as-or-classic-run-as-account"></a>Usuwanie konta Uruchom jako lub klasycznego konta Uruchom jako
W tej sekcji opisano sposób toodelete i ponownie utwórz konto Uruchom jako lub klasycznego Uruchom jako. Podczas wykonywania tej akcji jest zachowywana hello konta automatyzacji. Po usunięciu konta Uruchom jako lub klasycznego Uruchom jako, można go utworzyć ponownie w hello portalu Azure.

1. Hello portalu Azure Otwórz hello konta automatyzacji.

2. Na powitania **konto automatyzacji** bloku w hello konta w okienku właściwości, wybierz opcję **konta Uruchom jako**.

3. Na powitania **konta Uruchom jako** bloku właściwości, albo hello Uruchom jako konto klasycznego konto Uruchom jako lub wybierz konto, które mają toodelete. Następnie na powitania **właściwości** bloku hello wybranego konta, kliknij przycisk **usunąć**.

 ![Usuwanie konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Gdy konto hello jest usuwany, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.

5. Po usunięciu konta hello, można go ponownie utworzyć na powitania **konta Uruchom jako** opcja tworzenia bloku właściwości, wybierając hello **Azure konta Uruchom jako**.

 ![Ponownie utwórz konto Uruchom jako automatyzacji hello](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>Błąd konfiguracji
Niektóre elementy konfiguracji niezbędne do toofunction konta Uruchom jako klasycznego konto Uruchom jako lub hello prawidłowo może zostały usunięte lub nieprawidłowo utworzone podczas instalacji początkowej. elementy Hello obejmują:

* Zasób certyfikatu
* Zasób połączenia
* Konto Uruchom jako zostało usunięte z hello roli współautora
* Nazwa główna usługi lub aplikacji w usłudze Azure AD

W poprzednim hello i inne wystąpienia błędnej konfiguracji hello konta automatyzacji wykrywa hello zmiany i ma stan *niepełnym* na powitania **konta Uruchom jako** bloku właściwości hello konto.

![Stan Niekompletne dla konfiguracji konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

Po wybraniu konta Uruchom jako hello hello konta **właściwości** okienko zawierające hello następujący komunikat o błędzie:

![Komunikat ostrzegawczy Niekompletne dla konfiguracji konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

Przez usunięcie i ponowne utworzenie konta hello można szybko rozwiązać te problemy Uruchom jako konta.

## <a name="update-your-automation-account-by-using-powershell"></a>Aktualizacja konta usługi Automation przy użyciu programu PowerShell
Możesz za pomocą programu PowerShell tooupdate istniejącego konta automatyzacji:

* Utwórz konto usługi Automatyzacja, ale odrzucić konta Uruchom jako hello toocreate.
* Zasoby usługi Resource Manager toomanage konto automatyzacji jest już używana, i chcesz tooupdate hello konta tooinclude hello konta Uruchom jako dla uwierzytelniania elementu runbook.
* Używasz toomanage konta automatyzacji dla zasoby klasyczne i chcesz tooupdate go hello toouse konta w klasycznym Uruchom jako, zamiast tworzenia nowego konta i migrację z tooit elementy runbook i zasoby.   
* Ma toocreate Uruchom jako, a konto klasycznego Uruchom jako za pomocą certyfikatu wystawionego przez urząd certyfikacji (CA) przedsiębiorstwa.

skrypt Hello ma hello następujące wymagania wstępne:

* skrypt Hello można uruchomić tylko w systemie Windows 10 i Windows Server 2016 z modułami usługi Azure Resource Manager 2.01 lub nowszy. Nie jest obsługiwany przez wcześniejsze wersje systemu Windows.
* Program Azure PowerShell 1.0 lub nowszy. Aby uzyskać informacje o wersji hello PowerShell 1.0, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* Konto automatyzacji, który jest określany jako wartość hello hello *— AutomationAccountName* i *- ApplicationDisplayName* parametrów w hello następującego skryptu programu PowerShell.

wartości tooget hello *SubscriptionID*, *ResourceGroup*, i *AutomationAccountName*, które są wymagane parametry hello skryptów, hello następujące:
1. W hello portalu Azure, wybierz konto Automatyzacja na powitania **konto automatyzacji** bloku, a następnie wybierz **wszystkie ustawienia**. 
2. Na powitania **wszystkie ustawienia** bloku, w obszarze **ustawienia konta**, wybierz pozycję **właściwości**. 
3. Należy pamiętać, wartości hello na powitania **właściwości** bloku.

![Blok "Właściwości" konto automatyzacji Hello](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>Tworzenie skryptu programu PowerShell konta Uruchom jako
Ten skrypt programu PowerShell obejmuje obsługę hello następujące konfiguracje:

* Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.
* Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.
* Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa.
* Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych.

W zależności od opcji konfiguracji hello wybranej hello skrypt tworzy hello następujące elementy.

**W przypadku kont Uruchom jako:**

* Tworzy Azure AD aplikacji toobe wyeksportowany z obu hello z podpisem własnym lub klucz publiczny certyfikatu przedsiębiorstwa, tworzy konto główne usługi dla aplikacji hello w usłudze Azure AD i przypisuje hello roli współautora dla konta hello w bieżącym Subskrypcja. Możesz zmienić to ustawienie tooOwner ani żadnych innych ról. Aby uzyskać więcej informacji, zobacz [Kontrola dostępu oparta na rolach w usłudze Azure Automation](automation-role-based-access-control.md).
* Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureRunAsCertificate* hello określono konto automatyzacji. zasób certyfikatu Hello przechowuje hello certyfikatu klucza prywatnego, który jest używany przez aplikację hello Azure AD.
* Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureRunAsConnection* hello określono konto automatyzacji. zasób połączenia Hello przechowuje identyfikator aplikacji hello, identyfikatora dzierżawcy, identyfikator subskrypcji i odcisk palca certyfikatu.

**W przypadku klasycznych kont Uruchom jako:**

* Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureClassicRunAsCertificate* hello określono konto automatyzacji. zasób certyfikatu Hello zawiera klucz prywatny certyfikatu hello używane przez hello certyfikat zarządzania.
* Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureClassicRunAsConnection* hello określono konto automatyzacji. zasób połączenia Hello przechowuje hello Nazwa subskrypcji, identyfikator subskrypcji i certyfikat nazwa zasobów.

>[!NOTE]
> Jeśli wybierzesz opcję tworzenia klasycznego konta Uruchom jako, po wykonaniu skryptu hello, przekazywanie hello publicznego zarządzania toohello (rozszerzenie nazwy pliku cer) magazynu certyfikatów dla subskrypcji hello tego konta automatyzacji hello został utworzony w.
> 

tooexecute hello skryptu i przekaż certyfikat hello, hello następujące:

1. Zapisz hello następującego skryptu na komputerze. W tym przykładzie, zapisać go z nazwą pliku hello *RunAsAccount.ps1 nowy*.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. Na komputerze kliknij przycisk **Start**, a następnie uruchom program **Windows PowerShell** z podwyższonym poziomem uprawnień użytkownika.

3. Z hello z podwyższonym poziomem uprawnień, powłoka wiersza polecenia programu PowerShell, przejdź toohello folderu, który zawiera hello skryptu, który został utworzony w kroku 1.

4. Uruchom skrypt hello przy użyciu wartości parametrów hello hello konfiguracji, które są wymagane.

    **Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Po wykonaniu skryptu hello, będzie tooauthenticate zostanie wyświetlony monit o systemie Azure. Zaloguj się przy użyciu konta, które jest członkiem grupy administratorów subskrypcji hello i współadministratorem subskrypcji hello.
    >
    >

Po pomyślnym wykonaniu hello script należy zwrócić uwagę na następujące hello:
* Jeśli utworzono konto klasycznego Uruchom jako z publicznego certyfikatu z podpisem własnym (plik cer) hello skrypt tworzy i zapisuje go toohello folder plików tymczasowych na komputerze w obszarze profil użytkownika hello *%USERPROFILE%\AppData\Local\Temp*, używany sesji programu PowerShell hello tooexecute.
* Jeśli zostało utworzone klasyczne konto Uruchom jako z publicznym certyfikatem przedsiębiorstwa (plik CER), użyj tego certyfikatu. Wykonaj instrukcje hello [przekazywania toohello certyfikat interfejsu API zarządzania klasycznego portalu Azure](../azure-api-management-certs.md), a następnie zweryfikować hello konfigurację poświadczeń z usługi zarządzania zasobami przy użyciu hello [przykładowy kod tooauthenticate z usługi zarządzania zasobami](#sample-code-to-authenticate-with-service-management-resources). 
* Jeśli tak, *nie* Utwórz konto klasycznego Uruchom jako, uwierzytelniania za pomocą zasoby usługi Resource Manager i sprawdzić poprawność konfiguracji poświadczeń hello przy użyciu hello [przykładowy kod w celu uwierzytelniania z usługi zarządzania zasoby](#sample-code-to-authenticate-with-resource-manager-resources).

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>Przykładowy kod tooauthenticate z zasobami usługi Resource Manager
Można użyć następujących hello zaktualizowany przykładowy kod z hello *AzureAutomationTutorialScript* Przykładowy element runbook, tooauthenticate za pomocą hello Uruchom jako konta toomanage zasoby usługi Resource Manager elementy runbook.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

toohelp tooeasily możesz pracy między wiele subskrypcji, skrypt hello zawiera dwa wiersze kodu obsługujących odwołujące się do kontekstu subskrypcji. Zasób zmiennej o nazwie *SubscriptionId* zawiera identyfikator hello hello subskrypcji. Po hello `Add-AzureRmAccount` instrukcji polecenia cmdlet hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) polecenia cmdlet jest podany zestaw parametrów hello *- SubscriptionId*. Jeśli nazwa zmiennej hello jest zbyt ogólne, można poprawić go tooinclude prefiksu lub użyj innego toomake konwencji nazewnictwa go tooidentify łatwiejsze. Alternatywnie można użyć zestaw parametrów hello *— Nazwa subskrypcji* zamiast *- SubscriptionId* z odpowiedniej zawartości zmiennej.

polecenia cmdlet służące do uwierzytelniania w hello runbook Hello `Add-AzureRmAccount`, używa hello *ServicePrincipalCertificate* zestaw parametrów. Jest uwierzytelniany przy użyciu hello certyfikat główny usługi, nie hello poświadczeń użytkownika.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>Przykładowy kod tooauthenticate z zasobami usługi zarządzania
Można użyć powitania po przykładowy kod, który jest pobierana z hello *AzureClassicAutomationTutorialScript* Przykładowy element runbook, tooauthenticate przy użyciu hello klasycznego Uruchom jako konta toomanage zasoby klasyczne z sieci elementy runbook.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>Następne kroki
* [Application and service principal objects in Azure AD](../active-directory/active-directory-application-objects.md) (Obiekty aplikacji i nazwy głównej usługi w usłudze Azure AD)
* [Kontrola dostępu oparta na rolach w usłudze Azure Automation](automation-role-based-access-control.md)
* [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md) (Omówienie certyfikatów usług Azure Cloud Services)
