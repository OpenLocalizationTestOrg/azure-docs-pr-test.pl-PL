---
title: "autonomiczny aaaCreate konto usługi Automatyzacja Azure | Dokumentacja firmy Microsoft"
description: "Samouczek który przeprowadzi Cię przez hello tworzenie, testowanie i przykład uwierzytelnianie przy użyciu zabezpieczeń podmiotu zabezpieczeń w automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 1500d25d9565d4082768933834303a17c5e84234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-azure-automation-account"></a>Tworzenie autonomicznego konta usługi Azure Automation
W tym temacie pokazano, jak toocreate konto usługi Automatyzacja z portalu Azure tooevaluate i Dowiedz się usługi Automatyzacja Azure, bez uwzględniania rozwiązania do zarządzania dodatkowe hello lub Integracja z usługą analizy dzienników OMS tooprovide hello zaawansowanego monitorowania zadania elementu runbook.  Można dodać te rozwiązania do zarządzania lub zintegrować z analizy dzienników w dowolnym momencie w przyszłości hello.  Z hello konto automatyzacji jest elementów runbook można tooauthenticate zarządzania zasobami Azure Resource Manager lub klasycznego wdrożenia usługi Azure.

Podczas tworzenia konta automatyzacji w portalu Azure hello, automatycznie tworzy:

* Konto Uruchom jako w usłudze Azure Active Directory, certyfikat, który tworzy nową główną nazwę usługi i przypisuje hello kontroli dostępu opartej na roli współautora (RBAC), które jest używane zasoby usługi Resource Manager toomanage używanie elementów runbook.   
* Klasycznym konto Uruchom jako, przekazując certyfikat zarządzania, które jest używane zasoby klasyczne toomanage używanie elementów runbook.  

To upraszcza proces hello automatycznie i pomaga szybko rozpocząć tworzenie i wdrażanie elementów runbook toosupport Twojego Automatyzacja potrzebuje.  

## <a name="permissions-required-toocreate-automation-account"></a>Konto automatyzacji toocreate wymagane uprawnienia
toocreate lub aktualizacji konto usługi Automatyzacja, musi mieć powitania po określone uprawnienia i toocomplete wymagane uprawnienia, w tym temacie.   
 
* W kolejności toocreate konto usługi Automatyzacja, Twoje konto użytkownika AD musi toobe tooa dodano rolę z rolę właściciela toohello równoważne uprawnienia Microsoft.Automation zasobów zgodnie z opisem w artykule [kontroli dostępu opartej na rolach w usłudze Automatyzacja Azure ](automation-role-based-access-control.md).  
* Jeśli ustawienie rejestracji aplikacji hello ustawiono zbyt**tak**, użytkownicy inni niż administratorzy w Twojej dzierżawie usługi Azure AD można [rejestrowania aplikacji AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Jeśli ustawienie rejestracji aplikacji hello ustawiono zbyt**nr**, wykonanie tej czynności użytkownika hello musi być administratorem globalnym w usłudze Azure AD. 

Jeśli nie jesteś członkiem wystąpienia usługi Active Directory hello subskrypcji przed dodaniem toohello globalnego administratora/drugi-administrator roli hello subskrypcji, zostaną dodane tooActive katalogu jako Gość. W takiej sytuacji pojawi się "nie ma uprawnień toocreate..." Ostrzeżenie dotyczące hello **Dodaj konto automatyzacji** bloku. Użytkownicy, którzy dodano toohello globalnego administratora/drugi-administrator roli najpierw można usunąć z wystąpienia usługi Active Directory hello subskrypcji i ponownie dodano toomake ich pełną użytkownika w usłudze Active Directory. tooverify takiej sytuacji z hello **usługi Azure Active Directory** okienka w hello portalu Azure, wybierz opcję **użytkowników i grup**, wybierz pozycję **wszyscy użytkownicy** i po wybraniu hello określony użytkownik, wybierz opcję **profilu**. Witaj wartość hello **typ użytkownika** atrybutu na liście profilów użytkowników hello nie powinna być równa **gościa**.

## <a name="create-a-new-automation-account-from-hello-azure-portal"></a>Utwórz nowe konto automatyzacji z hello portalu Azure
W tej sekcji wykonaj następujące kroki toocreate konto usługi Automatyzacja Azure w portalu Azure hello hello.    

1. Zaloguj się toohello portalu Azure przy użyciu konta, które jest członkiem roli Administratorzy subskrypcji hello i współadministratorem subskrypcji hello.
2. Kliknij przycisk **Nowy**.<br><br> ![Wybieranie opcji Nowy w witrynie Azure Portal](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  
3. Wyszukaj **automatyzacji** , a następnie w hello w wynikach wyszukiwania wybierz **Automatyzacja i kontrola***.<br><br> ![Wyszukiwanie i wybieranie usługi Automation w witrynie Marketplace](media/automation-create-standalone-account/automation-marketplace-select-create-automationacct.png)<br> 
3. W bloku konta automatyzacji powitania kliknij **Dodaj**.<br><br>![Dodawanie konta usługi Automation](media/automation-create-standalone-account/automation-create-automationacct-properties.png)
   
   > [!NOTE]
   > Jeśli widzisz hello następujące ostrzeżenie w hello **Dodaj konto automatyzacji** bloku to, że konto użytkownika nie jest członkiem roli Administratorzy subskrypcji hello i współadministrator subskrypcji hello.<br><br>![Ostrzeżenie podczas dodawania konta usługi Automation](media/automation-create-standalone-account/create-account-without-perms.png)
   > 
   > 
4. W hello **Dodaj konto automatyzacji** bloku w hello **nazwa** wpisz nazwę nowego konta automatyzacji.
5. Jeśli masz więcej niż jedną subskrypcję, określ jedną hello nowego konta, a nowy lub istniejący **grupy zasobów** i centrum danych Azure **lokalizacji**.
6. Sprawdź wartość hello **tak** został wybrany do hello **tworzenia konta Uruchom jako Azure** opcji, a następnie kliknij przycisk hello **Utwórz** przycisku.  
   
   > [!NOTE]
   > Po wybraniu toonot utworzyć hello konta Uruchom jako, wybierając opcję hello **nr**, otrzymasz komunikat ostrzegawczy w hello **Dodaj konto automatyzacji** bloku.  Gdy konto hello jest tworzone w portalu Azure hello, nie ma odpowiedniego tożsamość uwierzytelniania w ramach Twojej klasycznego lub usługa katalogowa subskrypcji Menedżera zasobów i w związku z tym nie tooresources dostępu w ramach subskrypcji.  To zapobiega żadnych elementów runbook odwołuje się do tego konta jest w stanie tooauthenticate i wykonywać zadania dotyczące zasobów w tych modelach wdrażania.
   > 
   > ![Ostrzeżenie podczas dodawania konta usługi Automation](media/automation-create-standalone-account/create-account-decline-create-runas-msg.png)<br>
   > Gdy hello nazwy głównej usługi nie jest utworzona Rola współautora hello nie jest przypisany.
   > 

7. Gdy Azure tworzy konto automatyzacji hello, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.

### <a name="resources-included"></a>Zasoby dołączone
Po pomyślnym utworzeniu konta automatyzacji hello kilka zasoby są tworzone automatycznie dla Ciebie.  Witaj w poniższej tabeli znajduje się podsumowanie zasobów dla hello konta Uruchom jako.<br>

| Zasób | Opis |
| --- | --- |
| AzureAutomationTutorial Runbook |Przykład graficzny element runbook, który pokazuje, jak za pomocą tooauthenticate hello konta Uruchom jako i pobiera wszystkie zasoby usługi Resource Manager hello. |
| AzureAutomationTutorialScript Runbook |Runbook programu PowerShell przykładzie pokazano, jak za pomocą tooauthenticate hello konta Uruchom jako, który pobiera wszystkie zasoby usługi Resource Manager hello. |
| AzureRunAsCertificate |Zasób certyfikatu automatycznie utworzone podczas tworzenia konta automatyzacji lub za pomocą skryptu PowerShell hello poniżej dla istniejącego konta.  Pozwala ona tooauthenticate z platformy Azure, dzięki czemu zasoby usługi Azure Resource Manager można zarządzać z poziomu elementów runbook.  Ten certyfikat ma roczny okres obowiązywania. |
| AzureRunAsConnection |Zasób połączenia automatycznie utworzone podczas tworzenia konta automatyzacji lub za pomocą skryptu PowerShell hello poniżej dla istniejącego konta. |

Witaj w poniższej tabeli zawiera podsumowanie zasobów dla hello konto klasycznego Uruchom jako.<br>

| Zasób | Opis |
| --- | --- |
| AzureClassicAutomationTutorial Runbook |Przykładowy graficzny element runbook, który pobiera wszystkich maszyn wirtualnych klasycznego hello w ramach subskrypcji przy użyciu hello klasycznego konta Uruchom jako (certyfikatu), a następnie generuje hello nazwę maszyny Wirtualnej i stan. |
| AzureClassicAutomationTutorial Script Runbook |Przykład runbook programu PowerShell, który pobiera wszystkich maszyn wirtualnych klasycznego hello w ramach subskrypcji przy użyciu hello klasycznego konta Uruchom jako (certyfikatu), a następnie generuje hello nazwę maszyny Wirtualnej i stan. |
| AzureClassicRunAsCertificate |Automatycznie utworzone oznacza to zasób certyfikatu używane tooauthenticate z platformy Azure, tak, aby można było zarządzać Azure zasoby klasyczne z poziomu elementów runbook.  Ten certyfikat ma roczny okres obowiązywania. |
| AzureClassicRunAsConnection |Automatycznie utworzone oznacza to zasób połączenia używane tooauthenticate z platformy Azure, tak, aby można było zarządzać Azure zasoby klasyczne z poziomu elementów runbook. |


## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn więcej informacji na temat tworzenia graficznego [tworzenia graficznego automatyzacji Azure](automation-graphical-authoring-intro.md).
* tooget pracę z elementów runbook programu PowerShell, zobacz [Moje pierwszego elementu runbook programu PowerShell](automation-first-runbook-textual-powershell.md).
* tooget pracy z elementami runbook przepływu pracy programu PowerShell, zobacz [Mój pierwszy element runbook przepływu pracy programu PowerShell](automation-first-runbook-textual.md).
