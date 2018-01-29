---
title: "Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do usługi Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2017
ms.author: jeedes
ms.openlocfilehash: a77b5b1fff670ed7698d0ef48fa63f8a8f9be819
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-configure-google-apps-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem tego samouczka jest pokazują, jak automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure Active Directory (Azure AD) do usługi Google Apps.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz, który jest opisane w tym samouczku założono, że już następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Nieprawidłowa dzierżawy dla usługi Google Apps for Work lub usługi Google Apps dla instytucji edukacyjnych. Bezpłatne konto próbne można użyć albo usługi.
*   Konto użytkownika w usłudze Google Apps z uprawnieniami administratora zespołu.

## <a name="assign-users-to-google-apps"></a>Przypisywanie użytkowników do usługi Google Apps

Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji. W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD są synchronizowane.

Aby skonfigurować i włączyć usługę inicjowania obsługi administracyjnej, należy zdecydować, których użytkowników lub grup w usłudze Azure AD będą potrzebować dostępu do aplikacji Google Apps. Po utworzeniu tej decyzji, tych użytkowników można przypisać do aplikacji Google Apps zgodnie z instrukcjami w [przypisać użytkownika lub grupy do aplikacji przedsiębiorstwa](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

> [!IMPORTANT]
> Zalecamy, aby pojedynczego użytkownika usługi Azure AD można przypisać do usługi Google Apps do testowania konfiguracji inicjowania obsługi administracyjnej. Później można przypisać dodatkowych użytkowników i grup.

> Gdy użytkownik jest przypisany do usługi Google Apps, wybierz **użytkownika** lub **grupy** roli w oknie dialogowym przypisania. **Domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-automated-user-provisioning"></a>Włącz inicjowanie obsługi użytkowników automatycznych

Ta sekcja umożliwia łączenie usługi Azure AD z konta użytkownika, inicjowanie obsługi aplikacji interfejsu API firmy Google. Pomaga również skonfigurować usługę inicjowania obsługi administracyjnej do tworzenia, aktualizacji i wyłączenie konta użytkowników przypisane w usługi Google Apps na podstawie użytkownika i przypisanie do grupy w usłudze Azure AD.

>[!TIP]
>Można także włączyć na języku SAML rejestracji jednokrotnej dla konta Google Apps, postępując zgodnie z instrukcjami w [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="configure-automatic-user-account-provisioning"></a>Skonfiguruj użytkownika automatyczne Inicjowanie obsługi konta

> [!NOTE]
> Inny wygodną opcją do automatyzacji Inicjowanie obsługi użytkowników do usługi Google Apps jest użycie [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en). GADS inicjuje Twoich tożsamości: lokalnej usługi Active Directory do usługi Google Apps. Natomiast rozwiązanie w tym samouczku inicjuje synchronizację usługi Azure Active Directory (w chmurze) użytkowników i grup z obsługą wiadomości e-mail do usługi Google Apps. 

1. Zaloguj się do [konsoli administracyjnej aplikacji Google](http://admin.google.com/) z konta administratora, a następnie wybierz **zabezpieczeń**. Jeśli nie widzisz łącza może być ukryty w obszarze **więcej formantów** menu u dołu ekranu.
   
    ![Wybierz opcję Zabezpieczenia.][10]

2. Na **zabezpieczeń** wybierz pozycję **dokumentacja interfejsu API**.
   
    ![Wybierz odwołanie do interfejsu API.][15]

3. Wybierz **dostęp włączyć API**.
   
    ![Wybierz odwołanie do interfejsu API.][16]

    > [!IMPORTANT]
    > Dla każdego użytkownika, który chcesz udostępnić do aplikacji Google, nazwa użytkownika ich w usłudze Azure Active Directory *musi* ograniczeni do domeny niestandardowej. Na przykład użytkownik nazwy tego wygląd bob@contoso.onmicrosoft.com nie są akceptowane przez usługi Google Apps. Z drugiej strony bob@contoso.com została zaakceptowana. Istniejącego użytkownika domeny można zmienić, edytując właściwości ich w usłudze Azure AD. Dodaliśmy instrukcje dotyczące sposobu ustawiania domeny niestandardowej dla usługi Azure Active Directory i usługi Google Apps w kolejnych krokach.
      
4. Jeśli nie dodano jeszcze niestandardowej nazwy domeny do usługi Azure Active Directory, wykonaj następujące czynności:
  
    a. W [portalu Azure](https://portal.azure.com), w okienku nawigacji po lewej stronie wybierz **usługi Active Directory**. Na liście katalog wybierz swój katalog. 

    b. Wybierz **nazwy domeny** w lewym okienku nawigacji, a następnie wybierz **Dodaj**.
     
     ![Domena](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![Dodawanie domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Wpisz nazwę domeny do **nazwy domeny** pola. Ta nazwa domeny powinien być tej samej nazwy domeny, która ma być używana dla konta Google Apps. Następnie wybierz **Dodawanie domeny** przycisku.
     
     ![Nazwa domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Wybierz **dalej** aby przejść do strony weryfikacji. Aby sprawdzić, czy jesteś właścicielem tej domeny, należy edytować rekordy DNS w domenie, zgodnie z wartościami, które znajdują się na tej stronie. Można sprawdzić za pomocą **rekordów MX** lub **rekordów TXT**w oparciu o wybór dla **typu rekordu** opcji. 
    
    Aby uzyskać bardziej szczegółowe instrukcje dotyczące sposobu Sprawdź nazwy domen z usługi Azure AD, zobacz [Dodaj własną nazwę domeny do usługi Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![Domena](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Powtórz poprzednie kroki dla wszystkich domen, które mają zostać dodane do katalogu.

    > [!NOTE]
    Do przypisywania użytkowników domeny niestandardowej usługi Google Apps musi odpowiadać nazwie domeny źródła usługi Azure AD. Jeśli nie są zgodne, można rozwiązać problem, implementacja dostosowania mapowanie atrybutu.


5. Teraz, gdy została zweryfikowana wszystkich domen w usłudze Azure AD, należy sprawdzić je ponownie z usługi Google Apps. Dla każdej domeny, która nie jest już zarejestrowany przy użyciu usługi Google Apps wykonaj następujące czynności:
   
    a. W [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), wybierz pozycję **domen**.
     
     ![Wybierz domenę][20]

    b. Wybierz **Dodawanie domeny lub alias domeny**.
     
     ![Dodaj nową domenę][21]

    c. Wybierz **Dodaj inną domenę**, a następnie wpisz nazwę domeny, który chcesz dodać.
     
     ![Wpisz nazwę domeny][22]

    d. Wybierz **Kontynuuj i Zweryfikuj prawo własności do domeny**. Następnie wykonaj kroki, aby sprawdzić, czy jesteś właścicielem nazwy domeny. Kompleksowe instrukcje na temat sposobu Sprawdź domenę z usługi Google Apps, zobacz [zweryfikowanie prawa własności lokacji z usługi Google Apps](https://support.google.com/webmasters/answer/35179).

    e. Powtórz poprzednie kroki dla dodatkowe domeny, które mają zostać dodane do usługi Google Apps.
     
     > [!WARNING]
     > Jeśli zmienisz domena podstawowa dla dzierżawy usługi Google Apps i jeśli masz już skonfigurowane logowanie jednokrotne z usługą Azure AD, a następnie trzeba powtórzyć krok #3 w obszarze [krok 2: Włącz rejestrację jednokrotną](#step-two-enable-single-sign-on).
       
6. W [konsoli administracyjnej aplikacji Google](http://admin.google.com/), wybierz pozycję **ról administratora**.
   
     ![Wybierz usługi Google Apps][26]

7. Określ konto administratora, którego chcesz użyć do zarządzania, inicjowanie obsługi użytkowników. Aby uzyskać **rolę administratora** tego konta, Edytuj **uprawnienia** dla tej roli. Upewnij się włączyć wszystkie **uprawnień interfejsu API administratora** tak, aby to konto może służyć do inicjowania obsługi administracyjnej.
   
     ![Wybierz usługi Google Apps][27]
   
    > [!NOTE]
    > W przypadku konfigurowania środowiska produkcyjnego, najlepszym rozwiązaniem jest tworzenie konta administratora w usłudze Google Apps specjalnie dla tego kroku. Te konta musi mieć rolę administratora skojarzonych z nimi, który ma niezbędne uprawnienia interfejsu API.
     
8. W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory** > **aplikacje przedsiębiorstwa** > **wszystkie aplikacje** sekcji.

9. Jeśli został już skonfigurowany dla logowania jednokrotnego usługi Google Apps, wyszukaj dla swojego wystąpienia usługi Google Apps za pomocą pola wyszukiwania. W przeciwnym razie wybierz **Dodaj**, a następnie wyszukaj **usługi Google Apps** w galerii aplikacji. Wybierz **usługi Google Apps** w wynikach wyszukiwania, a następnie dodaj go do listy aplikacji.

10. Wybierz wystąpienie usługi Google Apps, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.

11. Ustaw **tryb obsługi administracyjnej** do **automatyczne**. 

     ![Inicjowanie obsługi](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. W obszarze **poświadczeń administratora** zaznacz **autoryzacji**. Okno dialogowe autoryzacji usługi Google Apps zostanie otwarty w nowym oknie przeglądarki.

13. Upewnij się, że chcesz nadać uprawnienia usługi Azure Active Directory, aby wprowadzić zmiany w dzierżawie usługi Google Apps. Wybierz **zaakceptować**.
    
     ![Upewnij się, uprawnienia.][28]

14. W portalu Azure wybierz **Testuj połączenie** do upewnij się, że połączenie usługi Azure AD do aplikacji Google Apps. Jeśli połączenie nie powiedzie się, upewnij się, że Twoje konto usługi Google Apps ma uprawnienia administratora zespołu. Spróbuj **autoryzacji** krok ponownie.

15. Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola. Następnie zaznacz pole wyboru.

16. Wybierz **zapisać.**

17. W obszarze **mapowania** zaznacz **synchronizacji Azure użytkownicy usługi Active Directory do usługi Google Apps**.

18. W **mapowań atrybutów** Przejrzyj atrybuty użytkowników, które są synchronizowane z usługi Azure AD do usługi Google Apps. Atrybuty, które są **pasujące** właściwości są używane do dopasowania kont użytkowników w usługi Google Apps dla operacji update. Wybierz **zapisać** aby zatwierdzić zmiany.

19. Aby włączyć usługi Azure AD, świadczenie usługi dla usługi Google Apps, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia**.

20. Wybierz pozycję **Zapisz**.

Ten proces jest uruchamiany wstępna synchronizacja jakichkolwiek użytkowników lub grup, które są przypisane do usługi Google Apps w sekcji Użytkownicy i grupy. Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, które są wykonywane co około 20 minut, gdy usługa jest uruchomiona. 

Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty aktywności. Te raporty opisano wszystkie akcje, które są wykonywane przez usługę inicjowania obsługi administracyjnej na aplikację usługi Google Apps.

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
