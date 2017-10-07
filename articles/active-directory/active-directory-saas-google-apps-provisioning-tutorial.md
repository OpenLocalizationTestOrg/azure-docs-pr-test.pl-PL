---
title: "Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooautomatically udostępniania i usuwanie użytkowników z usługi Azure AD tooGoogle aplikacji."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem Hello tego samouczka jest tooshow hello kroki potrzebne tooperform rezerw tooautomatically usługi Google Apps a usługą Azure AD i anulować aprowizację kont użytkowników z usługi Azure AD tooGoogle aplikacji.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Musi mieć prawidłową dzierżawy dla usługi Google Apps pracy lub usługi Google Apps dla instytucji edukacyjnych. Można użyć bezpłatnego konta wersji próbnej dla każdej usługi.
*   Konto użytkownika w usłudze Google Apps z uprawnieniami administratora zespołu.

## <a name="assigning-users-toogoogle-apps"></a>Przypisywanie użytkowników tooGoogle aplikacji

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentowania hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Google Apps tooyour. Po decyzję, wykonując następujące instrukcje hello tutaj można przypisać aplikacji Google Apps tooyour tych użytkowników: [przypisanie użytkownika lub grupy aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest aplikacji tooGoogle inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.
>*   Podczas przypisywania tooGoogle użytkownika aplikacji, należy wybrać w oknie dialogowym przydział hello hello użytkownika lub roli "Grupy". Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-automated-user-provisioning"></a>Włącz inicjowanie obsługi użytkowników automatycznych

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika aplikacji tooGoogle Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w usługi Google Apps na podstawie przypisań użytkowników i grup w usłudze Azure AD .

>[!Tip]
>Można też tooenabled na języku SAML logowania jednokrotnego dla aplikacji Google, hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="configure-automatic-user-account-provisioning"></a>Skonfiguruj użytkownika automatyczne Inicjowanie obsługi konta

> [!NOTE]
> Inną opcją działało do automatyzacji aprowizacji aplikacji tooGoogle użytkowników jest toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) który inicjuje tooGoogle tożsamości aplikacji z lokalnej usługi Active Directory. Z kolei hello rozwiązanie w tym samouczku udostępnia usługi Azure Active Directory (w chmurze), użytkowników i grup z włączoną obsługą poczty tooGoogle aplikacji. 

1. Zaloguj się na powitania [konsoli administracyjnej usługi Google Apps](http://admin.google.com/) przy użyciu konta administratora, a następnie kliknij przycisk **zabezpieczeń**. Jeśli nie widzisz hello łącza może być ukryty w obszarze hello **więcej formantów** menu u dołu hello hello ekranu.
   
    ![Kliknij pozycję Zabezpieczenia.][10]

2. Na powitania **zabezpieczeń** kliknij przycisk **dokumentacja interfejsu API**.
   
    ![Kliknij przycisk dokumentacja interfejsu API.][15]

3. Wybierz **dostęp włączyć API**.
   
    ![Kliknij przycisk dokumentacja interfejsu API.][16]

    > [!IMPORTANT]
    > Dla każdego użytkownika, który ma tooGoogle tooprovision aplikacji, swoją nazwę użytkownika w usłudze Azure Active Directory *musi* można wiązanej tooa domeny niestandardowej. Na przykład nazwy użytkowników, które przypominają bob@contoso.onmicrosoft.com nie jest akceptowane przez usługi Google Apps, podczas gdy bob@contoso.com została zaakceptowana. Istniejącego użytkownika domeny można zmienić, edytując właściwości ich w usłudze Azure AD. Instrukcje dla jak tooset domeny niestandardowej dla usługi Azure Active Directory i usługi Google Apps znajdują się w następujących krokach.
      
4. Nie dodano jeszcze tooyour nazwy domeny niestandardowej usługi Azure Active Directory, wykonaj następujące kroki hello:
  
    a. W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**. Na liście hello katalogu wybierz swój katalog. 

    b. Kliknij przycisk **nazwy domen** na hello w lewym okienku nawigacji, a następnie kliknij przycisk **Dodaj**.
     
     ![Domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![Dodawanie domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Wpisz nazwę domeny do hello **nazwy domeny** pola. Ta nazwa domeny musi być hello tej samej nazwy domeny czy zamierzasz toouse usługi Google Apps. Po wykonaniu tych czynności kliknij przycisk hello **Dodawanie domeny** przycisku.
     
     ![Nazwa domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Kliknij przycisk **dalej** toogo toohello weryfikacji strony. tooverify, że jesteś właścicielem tej domeny, należy edytować rekordy DNS domeny hello zgodnie z wartościami toohello na tej stronie. Możesz wybrać tooverify za pomocą **rekordów MX** lub **rekordów TXT**w oparciu o wybór dla hello **typu rekordu** opcji. Bardziej szczegółowe instrukcje dotyczące sposobu nazwa domeny tooverify z usługą Azure AD, zobacz [dodać własne tooAzure nazwy domeny AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![Domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Powtórz hello w poprzednich krokach dla wszystkich domen hello, który ma tooadd tooyour katalogu.

5. Po zweryfikowaniu wszystkich domen z usługą Azure AD, należy teraz sprawdzenie je ponownie z usługi Google Apps. Dla każdej domeny, która nie jest już zarejestrowany przy użyciu usługi Google Apps wykonaj następujące kroki hello:
   
    a. W hello [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), kliknij przycisk **domen**.
     
     ![Kliknij w domenach][20]

    b. Kliknij przycisk **Dodawanie domeny lub alias domeny**.
     
     ![Dodaj nową domenę][21]

    c. Wybierz **Dodaj inną domenę**i wpisz nazwę hello hello domeny, które chcesz tooadd.
     
     ![Wpisz nazwę domeny][22]

    d. Kliknij przycisk **Kontynuuj i Zweryfikuj prawo własności do domeny**. Następnie wykonaj tooverify kroki hello czy własnej nazwy domeny hello. Kompleksowe instrukcje na tooverify domeny usługi Google Apps, zobacz temat. [Zweryfikowanie prawa własności lokacji z usługi Google Apps](https://support.google.com/webmasters/answer/35179).

    e. Powtórz hello w poprzednich krokach dla dodatkowe domeny, który ma tooGoogle tooadd aplikacji.
     
     > [!WARNING]
     > Jeśli zmienisz hello domena podstawowa dla dzierżawy usługi Google Apps i jeśli masz już skonfigurowane logowanie jednokrotne z usługą Azure AD, a następnie masz toorepeat krok #3 w obszarze [krok dwa: Włącz logowanie jednokrotne](#step-two-enable-single-sign-on).
       
6. W hello [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), kliknij przycisk **ról administratora**.
   
     ![Polecenie usługi Google Apps][26]

7. Określić, które administrator konta ma Inicjowanie obsługi użytkowników toomanage toouse. Dla hello **rolę administratora** tego konta, Edytuj hello **uprawnienia** dla tej roli. Upewnij się, że ma ona wszystkie hello **uprawnień interfejsu API administratora** włączane tego konta można używać do inicjowania obsługi.
   
     ![Polecenie usługi Google Apps][27]
   
    > [!NOTE]
    > W przypadku konfigurowania środowiska produkcyjnego, hello najlepszym rozwiązaniem jest toocreate konto administratora usługi Google Apps specjalnie dla tego kroku. Te konta musi mieć rolę administratora skojarzonego z nim, którą ma niezbędne uprawnienia interfejsu API hello.
     
8. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

9. Jeśli został już skonfigurowany dla logowania jednokrotnego usługi Google Apps, wyszukaj dla swojego wystąpienia usługi Google Apps za pomocą pola wyszukiwania hello. W przeciwnym razie wybierz **Dodaj** i wyszukaj **usługi Google Apps** w galerii aplikacji hello. Wybierz usługi Google Apps z wyników wyszukiwania hello i dodać tooyour listy aplikacji.

10. Wybierz wystąpienie usługi Google Apps, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

11. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 

     ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. W obszarze hello **poświadczeń administratora** kliknij **autoryzacji**. Otwiera okno dialogowe autoryzacji usługi Google Apps w nowym oknie przeglądarki.

13. Upewnij się, chcieliby toogive usługi Azure Active Directory uprawnienia toomake zmiany dzierżawy tooyour usługi Google Apps. Kliknij przycisk **zaakceptować**.
    
     ![Upewnij się, uprawnienia.][28]

14. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć aplikację usługi Google Apps tooyour. Jeśli hello połączenia nie powiedzie się, upewnij się, Twoje konto usługi Google Apps ma uprawnienia administratora zespołu i spróbuj hello **"Autoryzuj"** krok ponownie.

15. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.

16. Kliknij przycisk **zapisać.**

17. W obszarze hello sekcji mapowania, wybierz **tooGoogle synchronizacji Azure Active Directory użytkowników aplikacji.**

18. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługi Azure AD tooGoogle aplikacji. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom usługi Google Apps dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

19. tooenable hello inicjowania obsługi usługi Azure AD dla usługi Google Apps hello zmiany **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello

20. Kliknij przycisk **zapisać.**

Rozpoczyna hello wstępnej synchronizacji użytkowników i/lub grupy przypisane aplikacje tooGoogle w sekcji hello użytkowników i grup. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello świadczenie usługi w aplikacji usługi Google Apps.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png