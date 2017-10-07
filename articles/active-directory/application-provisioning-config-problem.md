---
title: "Konfigurowanie inicjowania obsługi usługi Azure AD tooan galerii aplikacji użytkownika aaaProblem | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot typowych problemów, które muszą ponieść podczas konfigurowania użytkownika Inicjowanie obsługi administracyjnej aplikacji tooan już na liście galerii aplikacji hello Azure AD"
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
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>Problem podczas konfiguracji użytkownik inicjowania obsługi usługi Azure AD tooan galerii aplikacji

Konfigurowanie [użytkownika automatycznego inicjowania obsługi administracyjnej](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning) dla aplikacji (jeśli są obsługiwane), wymaga, aby uzyskać szczegółowe instrukcje aplikacji hello tooprepare użytego do automatycznego inicjowania obsługi. Następnie można użyć hello hello Azure tooconfigure portalu inicjowania obsługi usługi toosynchronize użytkownika konta toohello aplikacji.

Zawsze należy zacząć od znajdowanie hello Instalatora samouczek określonych toosetting się inicjowanie obsługi administracyjnej dla aplikacji. Należy wykonać te kroki tooconfigure zarówno aplikacji hello i inicjowania obsługi połączenia hello toocreate usługi Azure AD. Lista samouczków aplikacji można znaleźć w folderze [listy samouczki dotyczące tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

## <a name="how-toosee-if-provisioning-is-working"></a>Jak działa toosee Jeśli Inicjowanie obsługi administracyjnej 

Po skonfigurowaniu usługi hello wgląd w większości operacji hello hello usługi może być pobierana dwóch miejscach:

-   **Dzienniki inspekcji** — Witaj udostępniania rekordu dzienniki inspekcji wszystkie operacje hello wykonywane przez hello inicjowania obsługi usługi, łącznie z zapytań usługi Azure AD dla przypisane użytkowników, którzy znajdują się w zakresie udostępniania. Wyślij zapytanie do aplikacji docelowej hello hello istnienia tych użytkowników, porównanie hello obiektów użytkownika między hello systemu. Następnie dodać, zaktualizować lub wyłączyć hello konto użytkownika w systemie docelowym hello na podstawie porównania hello. Hello inicjowania obsługi dzienników inspekcji można uzyskać w portalu Azure w hello hello **usługi Azure Active Directory &gt; aplikacje przedsiębiorstwa &gt; \[Nazwa aplikacji\] &gt; dzienniki inspekcji**kartę. Filtr hello dzienniki na powitania **Inicjowanie obsługi konta** tooonly kategorii Zobacz hello inicjowania obsługi zdarzeń dla danej aplikacji.

-   **Inicjowanie obsługi administracyjnej stan —** Uruchom podsumowanie hello ostatniego udostępniania dla danej aplikacji można przeglądać w hello **usługi Azure Active Directory &gt; aplikacje przedsiębiorstwa &gt; \[Nazwa aplikacji\] &gt; Inicjowanie obsługi administracyjnej** sekcji u dołu ekranu hello w obszarze Ustawienia usługi hello hello. Ta sekcja zawiera podsumowanie, ilu użytkowników (i/lub grup) są obecnie synchronizowane między hello dwóch systemów, a jeśli wystąpiły żadne błędy. Szczegóły błędu można w dziennikach inspekcji hello. Należy pamiętać, że hello stan inicjowania obsługi administracyjnej nie można wypełnić do momentu zakończenia jednej pełnej wstępnej synchronizacji od usługi Azure AD i aplikacja hello.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Ogólnych problemów z inicjowaniem obsługi administracyjnej tooconsider

Poniżej znajduje się lista hello obszary ogólny problem, jeśli wiadomo, gdzie można wejść do toostart.

* [Inicjowanie obsługi usługi nie ma toostart](#provisioning-service-does-not-appear-to-start)
* [Nie można zapisać konfiguracji powodu poświadczenia tooapp nie działa](#can’t-save-configuration-due-to-app-credentials-not-working)
* [Dzienniki inspekcji, że użytkownicy są "pominięte" nieudostępniane, nawet jeśli są przypisane](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>Inicjowanie obsługi usługi nie ma toostart

Jeśli ustawisz hello **stan inicjowania obsługi administracyjnej** toobe **na** w hello **usługi Azure Active Directory &gt; aplikacje przedsiębiorstwa &gt; \[Nazwa aplikacji\] &gt;Inicjowania obsługi administracyjnej** sekcji hello portalu Azure. Jednak inne szczegóły stanu są wyświetlane na tej stronie po kolejne ponowne załadowanie. Istnieje prawdopodobieństwo, że usługa hello jest uruchomiona, ale nie ukończono jeszcze wstępnej synchronizacji. Sprawdź hello **dzienniki inspekcji** opisane powyżej toodetermine jakie operacje hello usługa działa, a jeśli wystąpiły żadne błędy.

>[!NOTE]
>Początkowa synchronizacja może potrwać od godziny tooseveral 20 minut, w zależności od wielkości hello hello katalog usługi Azure AD i hello liczbę użytkowników w zakresie obsługi. Kolejne synchronizacje po początkowej synchronizacji hello przebiegać szybciej, jak znaki wodne, przedstawiające stan hello obu systemów po początkowej synchronizacji hello, poprawa wydajności kolejne synchronizacje magazyny hello inicjowania obsługi usługi.
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>Nie można zapisać konfiguracji powodu poświadczenia tooapp nie działa

Aby toowork inicjowania obsługi administracyjnej usługa Azure AD wymaga prawidłowe poświadczenia umożliwiające zarządzanie użytkownikami tooa tooconnect pochodzącymi z danej aplikacji interfejsu API. Jeśli te poświadczenia nie działają lub nie znasz wat, są one, przejrzyj samouczek hello dotyczące konfigurowania tej aplikacji, opisanych powyżej.

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Dzienniki inspekcji, że użytkownicy są pomijane nieudostępniane, nawet jeśli są przypisane

Gdy użytkownik jest wyświetlany jako "pominięte" hello, dzienniki inspekcji, jest bardzo ważne tooread hello rozszerzony szczegółów w hello dziennika komunikatów toodetermine hello przyczyna. Poniżej przedstawiono typowe przyczyny i rozwiązania:

-   **Skonfigurowano zakresu filtru** **który jest filtrowanie hello użytkownika na podstawie wartości atrybutu**. Aby uzyskać więcej informacji na filtrami zakresów, zobacz <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **Witaj użytkownika "nie jest skutecznie uprawnione".** Jeśli zostanie wyświetlony ten komunikat o błędzie, to, że występuje problem z rekordem przypisanie użytkownika hello przechowywane w usłudze Azure AD. toofix ten problem, Usuń przypisanie hello z aplikacji hello użytkownik (lub grupa) i ponownie przypisać ponownie. Aby uzyskać więcej informacji na przypisanie, zobacz <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Lub nie jest wypełnione dla użytkownika jest wymagany atrybut.** Tooconsider ważne podczas konfigurowania udostępniania można tooreview i skonfigurować mapowanie atrybutów hello i przepływów pracy, definiujące które przepływ właściwości użytkownika (lub grupy) z usługi Azure AD toohello aplikacji. Obejmuje to ustawienie hello "zgodnej właściwości", który można toouniquely używane zidentyfikować a użytkowników/grupy między hello dwa systemy są takie same. Aby uzyskać więcej informacji na ten proces ważne, zobacz <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>.

   * **Mapowania dla grupy atrybutów:** udostępnianie hello grupy nazwa i grupa dane, dodanie toohello członków, jeśli są obsługiwane w przypadku niektórych aplikacji. Można włączyć lub wyłączyć tę funkcję przez włączenie lub wyłączenie hello **mapowania** dla obiektów grupy pokazano hello **inicjowania obsługi administracyjnej** kartę. Jeśli inicjowania obsługi grup jest włączona, upewnij się, że tooreview hello atrybutu mapowania tooensure odpowiednie pole jest używany przez hello "zgodnym z Identyfikatorem". Może to być hello wyświetlaną nazwę lub alias e-mail), ponieważ hello grupy i jej elementów członkowskich nie można zainicjować obsługi administracyjnej Jeśli hello dopasowania właściwości jest pusta lub nie jest wypełnione dla grupy w usłudze Azure AD.

#<a name="next-steps"></a>Następne kroki
[Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory](active-directory-saas-app-provisioning.md)
