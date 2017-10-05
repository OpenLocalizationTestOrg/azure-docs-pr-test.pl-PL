---
title: "Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do usługi Google Apps."
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
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem tego samouczka jest opisano czynności, które należy wykonać w usługi Google Apps a usługą Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do usługi Google Apps.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz opisany w tym samouczku założono, że już następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Musi mieć prawidłową dzierżawy dla usługi Google Apps pracy lub usługi Google Apps dla instytucji edukacyjnych. Można użyć bezpłatnego konta wersji próbnej dla każdej usługi.
*   Konto użytkownika w usłudze Google Apps z uprawnieniami administratora zespołu.

## <a name="assigning-users-to-google-apps"></a>Przypisywanie użytkowników do usługi Google Apps

Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji. W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji Google Apps. Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników aplikacji Google Apps: [przypisać użytkownika lub grupy do aplikacji w przedsiębiorstwie](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać do usługi Google Apps do testowania konfiguracji inicjowania obsługi administracyjnej. Później można przypisać dodatkowych użytkowników i/lub grup.
>*   Podczas przypisywania użytkowników do usługi Google Apps, należy wybrać w oknie dialogowym przydział roli użytkownika lub "Grupy". Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-automated-user-provisioning"></a>Włącz inicjowanie obsługi użytkowników automatycznych

Przewodniki dotyczące tej sekcji przez łączenie usługi Azure AD z interfejsu API inicjowania obsługi administracyjnej konta użytkownika usługi Google Apps i konfigurowanie usługi inicjowania obsługi administracyjnej do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w usłudze Google Apps na podstawie użytkownika i przypisanie do grupy w usłudze Azure AD.

>[!Tip]
>Można też włączone na języku SAML logowania jednokrotnego dla aplikacji Google, postępując zgodnie z instrukcjami zawarte w [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="configure-automatic-user-account-provisioning"></a>Skonfiguruj użytkownika automatyczne Inicjowanie obsługi konta

> [!NOTE]
> Inny wygodną opcją do automatyzacji Inicjowanie obsługi użytkowników do usługi Google Apps jest użycie [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) który inicjuje Twoich tożsamości: lokalnej usługi Active Directory do usługi Google Apps. Natomiast rozwiązanie w tym samouczku inicjuje użytkowników usługi Azure Active Directory (w chmurze), a grupy obsługujące pocztę do usługi Google Apps. 

1. Zaloguj się do [konsoli administracyjnej usługi Google Apps](http://admin.google.com/) przy użyciu konta administratora, a następnie kliknij przycisk **zabezpieczeń**. Jeśli nie widzisz łącza może być ukryty w obszarze **więcej formantów** menu u dołu ekranu.
   
    ![Kliknij pozycję Zabezpieczenia.][10]

2. Na **zabezpieczeń** kliknij przycisk **dokumentacja interfejsu API**.
   
    ![Kliknij przycisk dokumentacja interfejsu API.][15]

3. Wybierz **dostęp włączyć API**.
   
    ![Kliknij przycisk dokumentacja interfejsu API.][16]

    > [!IMPORTANT]
    > Dla każdego użytkownika, który ma obsługiwać usługi Google Apps swoją nazwę użytkownika w usłudze Azure Active Directory *musi* ograniczeni do domeny niestandardowej. Na przykład nazwy użytkowników, które przypominają bob@contoso.onmicrosoft.com nie jest akceptowane przez usługi Google Apps, podczas gdy bob@contoso.com została zaakceptowana. Istniejącego użytkownika domeny można zmienić, edytując właściwości ich w usłudze Azure AD. Instrukcje dotyczące sposobu ustawiania domeny niestandardowej dla usługi Azure Active Directory i usługi Google Apps znajdują się w następujących czynności.
      
4. Jeśli nie dodano jeszcze niestandardowej nazwy domeny do usługi Azure Active Directory, należy wykonać następujące czynności:
  
    a. W [portalu Azure](https://portal.azure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**. Na liście katalog wybierz swój katalog. 

    b. Kliknij przycisk **nazwy domen** w lewym okienku nawigacji, a następnie kliknij przycisk **Dodaj**.
     
     ![Domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![Dodawanie domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Wpisz nazwę domeny do **nazwy domeny** pola. Ta nazwa domeny powinien być tej samej nazwy domeny, która ma być używana dla konta Google Apps. Po wykonaniu tych czynności kliknij przycisk **Dodawanie domeny** przycisku.
     
     ![Nazwa domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Kliknij przycisk **dalej** aby przejść do strony weryfikacji. Aby sprawdzić, czy jesteś właścicielem tej domeny, należy edytować rekordy DNS w domenie, zgodnie z wartościami dostępnych na tej stronie. Można sprawdzić za pomocą **rekordów MX** lub **rekordów TXT**w oparciu o wybór dla **typu rekordu** opcji. Bardziej szczegółowe instrukcje dotyczące sposobu weryfikowania nazwy domeny w usłudze Azure AD, zobacz [Dodaj własną nazwę domeny do usługi Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![Domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Powtórz poprzednie kroki dla wszystkich domen, które mają zostać dodane do katalogu.

5. Po zweryfikowaniu wszystkich domen z usługą Azure AD, należy teraz sprawdzenie je ponownie z usługi Google Apps. Dla każdej domeny, która nie jest już zarejestrowany przy użyciu usługi Google Apps wykonaj następujące czynności:
   
    a. W [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), kliknij przycisk **domen**.
     
     ![Kliknij w domenach][20]

    b. Kliknij przycisk **Dodawanie domeny lub alias domeny**.
     
     ![Dodaj nową domenę][21]

    c. Wybierz **Dodaj inną domenę**i wpisz nazwę domeny, który chcesz dodać.
     
     ![Wpisz nazwę domeny][22]

    d. Kliknij przycisk **Kontynuuj i Zweryfikuj prawo własności do domeny**. Następnie wykonaj kroki, aby sprawdzić, czy jesteś właścicielem nazwy domeny. Kompleksowe instrukcje na temat sposobu Sprawdź domenę z usługi Google Apps Zobacz. [Zweryfikowanie prawa własności lokacji z usługi Google Apps](https://support.google.com/webmasters/answer/35179).

    e. Powtórz poprzednie kroki dla dodatkowe domeny, które mają zostać dodane do usługi Google Apps.
     
     > [!WARNING]
     > Jeśli zmienisz domena podstawowa dla dzierżawy usługi Google Apps i jeśli masz już skonfigurowane logowanie jednokrotne z usługą Azure AD, a następnie trzeba powtórzyć krok #3 w obszarze [krok dwa: Włącz logowanie jednokrotne](#step-two-enable-single-sign-on).
       
6. W [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), kliknij przycisk **ról administratora**.
   
     ![Polecenie usługi Google Apps][26]

7. Określ konto administratora, które chcesz użyć do zarządzania, inicjowanie obsługi użytkowników. Aby uzyskać **rolę administratora** tego konta, Edytuj **uprawnienia** dla tej roli. Upewnij się, że zawiera wszystkie **uprawnień interfejsu API administratora** włączane tego konta można używać do inicjowania obsługi.
   
     ![Polecenie usługi Google Apps][27]
   
    > [!NOTE]
    > W przypadku konfigurowania środowiska produkcyjnego, najlepszym rozwiązaniem jest tworzenie konta administratora w usłudze Google Apps specjalnie dla tego kroku. Te konta musi mieć rolę administratora skojarzonego z nim, którą ma niezbędne uprawnienia interfejsu API.
     
8. W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

9. Jeśli został już skonfigurowany dla logowania jednokrotnego usługi Google Apps, wyszukaj dla swojego wystąpienia usługi Google Apps za pomocą pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **usługi Google Apps** w galerii aplikacji. Wybierz usługi Google Apps z wyników wyszukiwania, a następnie dodaj go do listy aplikacji.

10. Wybierz wystąpienie usługi Google Apps, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.

11. Ustaw **tryb obsługi administracyjnej** do **automatyczne**. 

     ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. W obszarze **poświadczeń administratora** kliknij **autoryzacji**. Otwiera okno dialogowe autoryzacji usługi Google Apps w nowym oknie przeglądarki.

13. Upewnij się, że chcesz nadać uprawnienia usługi Azure Active Directory, aby wprowadzić zmiany w dzierżawie usługi Google Apps. Kliknij przycisk **zaakceptować**.
    
     ![Upewnij się, uprawnienia.][28]

14. W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji Google Apps. Jeśli połączenie nie powiedzie się, upewnij się, Twoje konto usługi Google Apps ma uprawnienia administratora zespołu i spróbuj **"Autoryzuj"** krok ponownie.

15. Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru.

16. Kliknij przycisk **zapisać.**

17. W sekcji mapowania wybierz **synchronizacji Azure użytkownicy usługi Active Directory do usługi Google Apps.**

18. W **mapowań atrybutów** Przejrzyj atrybuty użytkowników, które są synchronizowane z usługi Azure AD do usługi Google Apps. Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w usługi Google Apps dla operacji update. Wybierz przycisk Zapisz, aby zatwierdzić zmiany.

19. Aby włączyć usługi Azure AD, świadczenie usługi dla usługi Google Apps, zmień **stan inicjowania obsługi administracyjnej** do **na** w sekcji Ustawienia

20. Kliknij przycisk **zapisać.**

Rozpoczyna się wstępnej synchronizacji użytkowników i/lub grupy przypisane do usługi Google Apps w sekcji Użytkownicy i grupy. Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona. Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej na aplikację usługi Google Apps.

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