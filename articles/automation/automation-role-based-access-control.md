---
title: "Kontrola dostępu na podstawie aaaRole w automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Funkcja kontroli dostępu opartej na rolach (role-based access control, RBAC) umożliwia zarządzanie dostępem do zasobów platformy Azure. W tym artykule opisano sposób tooset się RBAC automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "automation rbac, kontrola dostępu oparta na rolach, azure rbac"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Kontrola dostępu oparta na rolach w usłudze Azure Automation
## <a name="role-based-access-control"></a>Kontrola dostępu oparta na rolach
Funkcja kontroli dostępu opartej na rolach (role-based access control, RBAC) umożliwia zarządzanie dostępem do zasobów platformy Azure. Przy użyciu [RBAC](../active-directory/role-based-access-control-configure.md), może też oddzielić obowiązków w obrębie organizacji, i udziel tylko hello ilość toousers dostępu, grup i aplikacji, że powinni tooperform swoich zadań. Dostępu na podstawie roli może zostać przydzielony toousers przy użyciu hello portalu Azure, narzędzi wiersza polecenia platformy Azure lub interfejsów API zarządzania platformy Azure.

## <a name="rbac-in-automation-accounts"></a>Funkcja RBAC w ramach kont automatyzacji
W automatyzacji Azure dostęp, przypisując hello odpowiednie RBAC roli toousers, grup i aplikacji na powitania zakres konta automatyzacji. Poniżej są hello wbudowane role obsługiwane za pomocą konta automatyzacji:  

| **Rola** | **Opis** |
|:--- |:--- |
| Właściciel |Rola właściciela Hello umożliwia dostęp do zasobów tooall i akcje w ramach konta automatyzacji, włącznie z zapewnieniem dostępu tooother użytkowników, grup i aplikacji toomanage hello konta automatyzacji. |
| Współautor |Rola współautora Hello umożliwia toomanage wszystko oprócz modyfikowania przez innego użytkownika uzyskać dostęp do konta automatyzacji tooan uprawnienia. |
| Czytelnik |rolę czytelnika Hello umożliwia tooview wszystkie zasoby hello w automatyzacji konta, ale nie można wprowadzać żadnych zmian. |
| Operator usługi |roli operatora automatyzacji Hello pozwala tooperform zadania operacyjne jak uruchamianie, zatrzymywanie, wstrzymywanie, wznowić i planowanie zadań. Ta rola jest przydatne, jeśli chcesz tooprotect zasobami konta automatyzacji, takich jak zasoby poświadczeń i elementy runbook przed wyświetlać lub modyfikować, ale nadal możliwe członkami tooexecute Twojej organizacji tych elementów runbook. |
| Administrator dostępu użytkowników |Hello roli Administrator dostępu użytkowników umożliwia kont automatyzacji tooAzure toomanage użytkownika dostępu. |

> [!NOTE]
> Nie można udzielić dostępu prawa tooa określonych lub elementy runbook, tylko toohello zasobów i akcji w ramach hello konta automatyzacji.  
> 
> 

W tym artykule firma Microsoft przeprowadzi Cię przez proces tooset się RBAC automatyzacji Azure. Jednak najpierw umożliwia podjęcie bliżej przyjrzeć się hello indywidualne uprawnienia nadanego toohello Współautor czytnik, Operator automatyzacji i Administrator dostępu użytkowników, dzięki czemu możemy uzyskać dobrą znajomością przed udzieleniem każda osoba, która praw toohello konta automatyzacji.  Zrobienie tego nieświadomie mogłoby mieć niezamierzone lub niepożądane konsekwencje.     

## <a name="contributor-role-permissions"></a>Uprawnienia roli Współautor
Witaj Poniższa tabela przedstawia hello określonych czynności, które mogą być wykonywane przez rolę współautora hello w automatyzacji.

| **Typ zasobu** | **Odczyt** | **Zapis** | **Usuwanie** | **Inne akcje** |
|:--- |:--- |:--- |:--- |:--- |
| Konto usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Zasób certyfikatu usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Zasób połączenia usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Zasób typu połączenia usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Zasób poświadczeń usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Zasób harmonogramu usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Zasób zmiennej usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Konfiguracja żądanego stanu usługi Automation | | | |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |
| Typ zasobu hybrydowego procesu roboczego elementu Runbook usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Zadanie usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |
| Strumień zadań usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Harmonogram zadań usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Moduł usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |
| Element Runbook usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |
| Próbna wersja elementu Runbook usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |
| Zadanie testowania próbnej wersji elementu Runbook usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |
| Element webhook usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Uprawnienia roli Czytelnik
Witaj Poniższa tabela przedstawia hello określonych czynności, które mogą być wykonywane przez rolę czytelnika hello w automatyzacji.

| **Typ zasobu** | **Odczyt** | **Zapis** | **Usuwanie** | **Inne akcje** |
|:--- |:--- |:--- |:--- |:--- |
| Klasyczny administrator subskrypcji |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Blokada zarządzania |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Uprawnienie |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Operacje dostawcy |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Przypisanie roli |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Definicja roli |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Uprawnienia roli Operator usługi
Witaj Poniższa tabela przedstawia hello określonych czynności, które mogą być wykonywane przez rolę operatora automatyzacji hello w automatyzacji.

| **Typ zasobu** | **Odczyt** | **Zapis** | **Usuwanie** | **Inne akcje** |
|:--- |:--- |:--- |:--- |:--- |
| Konto usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zasób certyfikatu usługi Automation | | | | |
| Zasób połączenia usługi Automation | | | | |
| Zasób typu połączenia usługi Automation | | | | |
| Zasób poświadczeń usługi Automation | | | | |
| Zasób harmonogramu usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | |
| Zasób zmiennej usługi Automation | | | | |
| Konfiguracja żądanego stanu usługi Automation | | | | |
| Typ zasobu hybrydowego procesu roboczego elementu Runbook usługi Automation | | | | |
| Zadanie usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |
| Strumień zadań usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Harmonogram zadań usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | |
| Moduł usługi Automation | | | | |
| Element Runbook usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Próbna wersja elementu Runbook usługi Automation | | | | |
| Zadanie testowania próbnej wersji elementu Runbook usługi Automation | | | | |
| Element webhook usługi Automation | | | | |

Aby uzyskać dodatkowe szczegóły hello [akcje operator automatyzacji](../active-directory/role-based-access-built-in-roles.md#automation-operator) list hello akcji obsługiwanych przez rolę operatora automatyzacji hello na konto automatyzacji hello i jej zasobach.

## <a name="user-access-administrator-role-permissions"></a>Uprawnienia roli Administrator dostępu użytkowników
Witaj Poniższa tabela przedstawia hello określonych czynności, które mogą być wykonywane przez hello rolę Administrator dostępu użytkowników w usłudze Automatyzacja.

| **Typ zasobu** | **Odczyt** | **Zapis** | **Usuwanie** | **Inne akcje** |
|:--- |:--- |:--- |:--- |:--- |
| Konto usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zasób certyfikatu usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zasób połączenia usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zasób typu połączenia usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zasób poświadczeń usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zasób harmonogramu usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zasób zmiennej usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Konfiguracja żądanego stanu usługi Automation | | | | |
| Typ zasobu hybrydowego procesu roboczego elementu Runbook usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zadanie usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Strumień zadań usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Harmonogram zadań usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Moduł usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Element Runbook usługi Azure Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Próbna wersja elementu Runbook usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Zadanie testowania próbnej wersji elementu Runbook usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Element webhook usługi Automation |![Status zielony](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Konfigurowanie funkcji RBAC dla konta usługi Automation za pomocą portalu Azure
1. Zaloguj się za toohello [Azure Portal](https://portal.azure.com/) , a następnie otwórz Twoje konto usługi Automatyzacja w bloku konta automatyzacji hello.  
2. Polecenie hello **dostępu** kontroli na powitania prawym górnym rogu. Spowoduje to otwarcie hello **użytkowników** bloku, w którym można dodawać nowych użytkowników, grup i aplikacji toomanage ich w Twoje konto usługi Automatyzacja i widoku istniejących ról, które można skonfigurować dla hello konta automatyzacji.  
   
   ![Przycisk Dostęp](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Administratorzy subskrypcji** już istnieje jako hello domyślny użytkownik. Grupa usługi active directory Administratorzy subskrypcji Hello zawiera hello administratorów usługi i co-administrator(s) dla subskrypcji platformy Azure. Witaj, Administratorze usługi jest właścicielem hello subskrypcji platformy Azure i jej zasobach i będą mieć rolę właściciela hello dziedziczone kont automatyzacji hello zbyt. Oznacza to, że dostęp hello jest **dziedziczonych** dla **usługi Administratorzy i współadministratorzy** subskrypcji i jej **przypisane** dla wszystkich hello innych użytkowników. Kliknij przycisk **Administratorzy subskrypcji** tooview bardziej szczegółowych informacji o ich uprawnienia.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Dodawanie nowego użytkownika i przypisywanie roli
1. Blok użytkownicy hello, kliknij **Dodaj** tooopen hello **bloku dostępu Dodaj** której można dodać użytkownika, grupę lub aplikację, a następnie przypisać toothem roli.  
   
   ![Dodawanie użytkownika](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Wybierz rolę z listy dostępnych ról hello. Wybierzemy hello **czytnika** roli, ale można wybrać dowolną hello dostępne wbudowane role, które obsługuje konto usługi Automatyzacja lub dowolnej roli niestandardowe zostały zdefiniowane.  
   
   ![Wybór roli](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Polecenie **dodawania użytkowników** tooopen hello **dodawania użytkowników** bloku. Po dodaniu żadnych użytkowników, grup lub aplikacje toomanage subskrypcję, a następnie tych użytkowników są wyświetlane i można je wybrać tooadd dostęp. Jeśli nie ma żadnych użytkowników na liście lub jeśli planuje się dodanie użytkownika hello nie ma na liście kliknij **zaprosić** tooopen hello **zaprosić Gość** bloku, w którym można zaprosić użytkowników przy użyciu prawidłowego konta Microsoft adres e-mail, takich jak Outlook.com, OneDrive lub Xbox Live ID. Po wprowadzeniu adresu e-mail hello hello użytkownika, kliknij przycisk **wybierz** tooadd hello użytkownika, a następnie kliknij przycisk **OK**. 
   
   ![Dodawanie użytkowników](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Teraz powinien zostać wyświetlony dodanego użytkownika, powitalne toohello **użytkowników** blok hello **czytnika** przypisanej roli.  
   
   ![Wyświetlanie użytkowników](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   Można także przypisać rolę użytkownika toohello z hello **ról** bloku. 
4. Kliknij przycisk **ról** z hello użytkowników bloku tooopen hello **bloku ról**. Z tego bloku można wyświetlić nazwę hello hello liczbę użytkowników i grup przypisaną rolę toothat hello roli.
   
    ![Przypisywanie roli w bloku użytkowników](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Kontrola dostępu oparta na rolach można ustawić tylko na powitania poziom konta automatyzacji i nie na wszystkich zasobów poniżej hello konta automatyzacji.
   > 
   > 
   
    Można przypisać więcej niż jednego użytkownika tooa roli, grupy lub aplikacji. Na przykład, jeśli dodamy hello **Operator automatyzacji** roli wraz z hello **rolę czytelnika** toohello użytkownika, a następnie ich można wyświetlić wszystkie zasoby automatyzacji hello, a także uruchomić hello zadania elementu runbook. Można rozwinąć hello listy rozwijanej tooview listę ról przypisane toohello użytkownika.  
   
    ![Przeglądanie wielu ról](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Usuwanie użytkownika
Możesz usunąć hello uprawnień dostępu dla użytkownika, który nie jest zarządzany hello konta automatyzacji lub który nie działa w przypadku organizacji hello. Poniżej są hello tooremove czynności użytkownika: 

1. Z hello **użytkowników** bloku, że chcesz tooremove przypisania roli hello wybierz.
2. Kliknij przycisk hello **Usuń** przycisk w bloku szczegółów przypisania hello.
3. Kliknij przycisk **tak** tooconfirm usuwania. 
   
   ![Usuwanie użytkowników](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Użytkownik przypisany do roli
Gdy loguje się użytkownik, któremu przypisano rolę tooa tootheir konto automatyzacji, będą teraz widoczne hello właściciela konta na liście Lista hello **domyślne katalogi**. W kolejności tooview hello konta automatyzacji, które zostały dodane do ich przełącznika hello domyślnego katalogu toohello właściciela domyślny katalog.  

![Katalog domyślny](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Środowisko użytkownika dla roli operatora usługi
Gdy użytkownik, który jest przypisany widoków roli operatora automatyzacji toohello hello automatyzacji konta, które są przypisane, mogą tylko hello wyświetlanie listy elementów runbook, zadania elementów runbook i harmonogramy utworzono w hello konta automatyzacji, ale nie można wyświetlić ich definicji. Ich uruchomić, zatrzymać, wstrzymać, wznowić lub zaplanować zadanie elementu runbook hello. Witaj, użytkownik nie będzie miał dostępu tooother automatyzacji zasoby, takie jak konfiguracje, hybrydowego procesu roboczego grupy lub węzłów DSC.  

![Nie tooresourcres dostępu](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Gdy hello użytkownik kliknie hello elementu runbook, hello poleceń tooview hello źródła lub edytować hello runbook nie są dostarczane jako roli operatora automatyzacji hello nie zezwala na dostęp toothem.  

![Nie elementu runbook tooedit dostępu](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

Hello użytkownika będą miały dostępu do harmonogramów tooview i toocreate, ale nie będą miały dostępu tooany, inny typ zasobu.  

![Nie tooassets dostępu](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Ponadto ten użytkownik nie ma dostępu tooview hello elementów webhook skojarzone z elementu runbook

![Nie toowebhooks dostępu](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Konfiguracja funkcji RBAC dla konta usługi Automation przy użyciu programu Azure PowerShell
Dostęp oparty na roli można też tooan skonfigurowanego konta automatyzacji za pomocą następujących hello [poleceń cmdlet programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).

• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) wyświetla wszystkie role RBAC, które są dostępne w usłudze Azure Active Directory. Można użyć tego polecenia, wraz z hello **nazwa** toolist właściwości hello wszystkie akcje, które mogą być wykonywane przez określoną rolę.  
    **Przykład:**  
    ![Pobranie definicji roli](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) list Azure AD RBAC przypisania ról na powitania określony zakres. Bez żadnych parametrów to polecenie zwraca wszystkie przypisania roli hello wprowadzonych w węźle hello subskrypcji. Użyj hello **ExpandPrincipalGroups** parametru toolist dostępu przydziały hello określić użytkownika, a także grupy hello hello użytkownika jest członkiem.  
    **Przykład:** Użyj hello następujące polecenie toolist, wszyscy użytkownicy hello i ich role w ramach konta automatyzacji.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Pobranie przypisania roli](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [AzureRmRoleAssignment nowy](https://msdn.microsoft.com/library/mt603580.aspx) tooassign toousers, grup i aplikacji tooa określonego zakresu dostępu.  
    **Przykład:** Użyj hello następujące polecenie roli "Automatyzacji operatora" hello tooassign dla użytkownika w hello zakres konta automatyzacji.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Przypisanie nowej roli](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Użyj [AzureRmRoleAssignment Usuń](https://msdn.microsoft.com/library/mt603781.aspx) tooremove dostępu określonego użytkownika, grupy lub aplikacji z określonego zakresu.  
    **Przykład:** Użyj hello następujące polecenie tooremove hello użytkownika z roli "Automatyzacji operatora" hello w hello zakres konta automatyzacji.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

W hello powyżej przykłady, Zastąp **zaloguj identyfikator**, **identyfikator subskrypcji**, **Nazwa grupy zasobów** i **nazwa konta automatyzacji** z sieci Szczegóły konta. Wybierz **tak** po wyświetleniu tooconfirm przed kontynuowaniem przypisania roli użytkownika tooremove.   

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać informacje na różne sposoby tooconfigure RBAC usługi Automatyzacja Azure, można znaleźć zbyt[Zarządzanie RBAC przy użyciu programu Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md).
* Aby uzyskać więcej informacji na różne sposoby toostart elementu runbook, zobacz [uruchamianie elementu runbook](automation-starting-a-runbook.md)
* Informacje na temat typów innego elementu runbook można znaleźć zbyt[typy elementu runbook usługi Automatyzacja Azure](automation-runbook-types.md)

