---
title: "Użytkownicy aaaNo są udostępnione tooan usługi Azure AD galerii aplikacji | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot typowych problemów, które muszą ponieść Jeśli nie widzisz użytkowników znajdujących się w moduł usługi Azure AD galerii aplikacji została skonfigurowana dla Inicjowanie obsługi użytkowników z usługą Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Użytkownicy nie są udostępnione tooan usługi Azure AD galerii aplikacji

Raz automatycznego inicjowania obsługi administracyjnej został skonfigurowany dla aplikacji (w tym sprawdzania, czy poświadczenia aplikacji hello podane aplikacji toohello tooconnect tooAzure AD są prawidłowe). Następnie użytkowników i grupy są udostępnione toohello aplikacji i jest określany przez hello następujące czynności:

-   Które użytkowników i grup **przypisane** toohello aplikacji. Aby uzyskać więcej informacji na przypisanie, zobacz [przypisać użytkownika lub grupę tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

-   Określa, czy **mapowania atrybutów** są włączone i skonfigurowane toosync prawidłowe atrybuty z aplikacji toohello usługi Azure AD. Aby uzyskać więcej informacji o mapowaniu atrybutu, zobacz [Dostosowywanie inicjowania obsługi administracyjnej atrybutu mapowania użytkowników dla aplikacji SaaS w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

-   Czy istnieje **zakresu filtru** obecna, który jest filtrowania użytkowników na podstawie określonej wartości atrybutu. Aby uzyskać więcej informacji na filtrami zakresów, zobacz [udostępniania aplikacji na podstawie atrybutów z filtrami zakresów](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

Po stwierdzeniu, że użytkownicy nie jest zainicjowana, sprawdź w dziennikach inspekcji hello w usłudze Azure AD i Wyszukaj wpisy dziennika dla określonego użytkownika.

Hello inicjowania obsługi dzienników inspekcji można uzyskać w portalu Azure w hello hello **usługi Azure Active Directory &gt; aplikacje przedsiębiorstwa &gt; \[Nazwa aplikacji\] &gt; dzienniki inspekcji**kartę. Filtr hello dzienniki na powitania **Inicjowanie obsługi konta** tooonly kategorii Zobacz hello inicjowania obsługi zdarzeń dla danej aplikacji. Można wyszukiwać użytkowników na podstawie hello "dopasowania Identyfikatora" skonfigurowanego dla nich w hello atrybutu mapowania. Na przykład, jeśli skonfigurowano hello "główna nazwa użytkownika" lub "adres e-mail" jako hello dopasowanie atrybutu na stronie powitania usługi Azure AD, a użytkownik hello udostępniania nie ma wartość "audrey@contoso.com". Następnie wyszukania w dziennikach inspekcji hello "audrey@contoso.com" i przeglądu, a następnie wpisy zwracane.

Witaj udostępniania inspekcji rejestruje rekord hello wszystkich operacji wykonywanych przez usługę inicjowania obsługi administracyjnej hello, łącznie z zapytań usługi Azure AD dla przypisanych użytkowników, które znajdują się w zakresie udostępniania zapytań hello docelowej aplikacji hello istnienia tych użytkowników, porównanie hello obiekty użytkownika między hello systemu. Następnie dodać, zaktualizować lub wyłączyć hello konto użytkownika w systemie docelowym hello na podstawie porównania hello.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Ogólne obszarów problemów z inicjowaniem obsługi administracyjnej tooconsider

Poniżej znajduje się lista hello obszary ogólny problem, jeśli wiadomo, gdzie można wejść do toostart.

* [Inicjowanie obsługi usługi nie ma toostart](#provisioning-service-does-not-appear-to-start)
* [Dzienniki inspekcji, że użytkownicy są pominięte nieudostępniane, nawet jeśli są przypisane](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Inicjowanie obsługi usługi nie ma toostart

Jeśli ustawisz hello **stan inicjowania obsługi administracyjnej** toobe **na** w hello **usługi Azure Active Directory &gt; aplikacje przedsiębiorstwa &gt; \[Nazwa aplikacji\] &gt;Inicjowania obsługi administracyjnej** sekcji hello portalu Azure. Jednak żaden inny stan są wyświetlane szczegóły na tej stronie po kolejne ponowne załadowanie, istnieje duże prawdopodobieństwo, że usługa hello jest uruchomiona, ale nie ukończono jeszcze wstępnej synchronizacji. Sprawdź hello **dzienniki inspekcji** opisane powyżej toodetermine jakie operacje hello usługa działa, a jeśli wystąpiły żadne błędy.

>[!NOTE]
>Początkowa synchronizacja może potrwać od godziny tooseveral 20 minut, w zależności od wielkości hello hello katalog usługi Azure AD i hello liczbę użytkowników w zakresie obsługi. Kolejne synchronizacje po początkowej synchronizacji hello są szybsze, jako hello świadczenie usługi przechowuje znaki wodne, przedstawiające stan hello obu systemów po początkowej synchronizacji hello. Poprawia to wydajność kolejne synchronizacje.
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Dzienniki inspekcji, że użytkownicy są pomijane nieudostępniane, nawet jeśli są przypisane

Gdy użytkownik jest wyświetlany jako "pominięte" hello, dzienniki inspekcji, jest bardzo ważne tooread hello rozszerzony szczegółów w hello dziennika komunikatów toodetermine hello przyczyna. Poniżej przedstawiono typowe przyczyny i rozwiązania:

-   **Skonfigurowano zakresu filtru** **który jest filtrowanie hello użytkownika na podstawie wartości atrybutu**. Aby uzyskać więcej informacji na filtrami zakresów, zobacz <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **Witaj użytkownika "nie jest skutecznie uprawnione".** Jeśli zostanie wyświetlony ten komunikat o błędzie, to, że występuje problem z rekordem przypisanie użytkownika hello przechowywane w usłudze Azure AD. toofix ten problem, Usuń przypisanie hello z aplikacji hello użytkownik (lub grupa) i ponownie przypisać ponownie. Aby uzyskać więcej informacji na przypisanie, zobacz <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Lub nie jest wypełnione dla użytkownika jest wymagany atrybut.** Tooconsider ważne podczas konfigurowania udostępniania można tooreview i skonfigurować mapowanie atrybutów hello i przepływów pracy, definiujące które przepływ właściwości użytkownika (lub grupy) z usługi Azure AD toohello aplikacji. Obejmuje to ustawienie hello "zgodnej właściwości", który można toouniquely używane zidentyfikować a użytkowników/grupy między hello dwa systemy są takie same. Aby uzyskać więcej informacji na ten proces ważne, zobacz [Dostosowywanie inicjowania obsługi administracyjnej atrybutu mapowania użytkowników dla aplikacji SaaS w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

  * **Mapowania dla grupy atrybutów:** udostępnianie hello grupy nazwa i grupa dane, dodanie toohello członków, jeśli są obsługiwane w przypadku niektórych aplikacji. Można włączyć lub wyłączyć tę funkcję przez włączenie lub wyłączenie hello **mapowania** dla obiektów grupy pokazano hello **inicjowania obsługi administracyjnej** kartę. Jeśli inicjowania obsługi grup jest włączona, upewnij się, że tooreview hello atrybutu mapowania tooensure odpowiednie pole jest używany przez hello "zgodnym z Identyfikatorem". Może to być hello wyświetlaną nazwę lub alias e-mail), ponieważ hello grupy i jej elementów członkowskich nie można zainicjować obsługi administracyjnej Jeśli hello dopasowania właściwości jest pusta lub nie jest wypełnione dla grupy w usłudze Azure AD.

## <a name="next-steps"></a>Następne kroki
[Synchronizacja programu Azure AD Connect: opis Aprowizacją deklaratywną](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

