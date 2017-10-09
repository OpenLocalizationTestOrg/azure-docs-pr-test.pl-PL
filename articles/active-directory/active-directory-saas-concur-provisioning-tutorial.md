---
title: 'Samouczek: Integracji Azure Active Directory z Concur | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a>Samouczek: Konfigurowanie cząstkowe do inicjowania obsługi użytkowników

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Concur i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooConcur.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Concur logowanie jednokrotne włączone subskrypcji.
*   Konto użytkownika w Concur z uprawnieniami administratora zespołu.

## <a name="assigning-users-tooconcur"></a>Przypisywanie użytkowników tooConcur

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Concur tooyour. Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Concur aplikacji:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a>Ważne porady dotyczące przypisywania tooConcur użytkowników

*   Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest tooConcur inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooConcur użytkownika, należy wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-user-provisioning"></a>Włącz inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooConcur programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Concur w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

> [!Tip] 
> Można też tooenabled na języku SAML logowania jednokrotnego dla Concur hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-user-account-provisioning"></a>Przypisywanie konta użytkowników tooconfigure:

Celem Hello w tej sekcji jest toooutline jak tooConcur kont tooenable Inicjowanie obsługi administracyjnej użytkownika usługi Active Directory.

aplikacje tooenable w hello usługi wydatków, ma prawidłową konfigurację toobe i korzystania z profilem administrator usługi sieci Web. Nie dodawaj hello WS Admin roli tooyour istniejący profil administratora używanej do T & j funkcji administracyjnych.

Cząstkowe konsultantów lub powitania klienta administrator musi utworzyć różne profilu administratora usługi sieci Web i powitania klienta administrator musi używać tego profilu dla funkcji administratora usługi sieci Web hello (na przykład włączenie aplikacje). Te profile muszą być przechowywane oddzielnie od powitania klienta administrator codzienne T & E admin profilu (hello T & E profilu administratora nie powinny mieć przypisanej roli WSAdmin hello).

Podczas tworzenia toobe profilu hello używane do włączania aplikacji hello nazwę administratora powitania klienta do pól profilu użytkownika hello. W ten sposób własność toohello profilu. Po utworzeniu co najmniej jeden profil powitania klienta musi Zaloguj się za pomocą tego profilu hello tooclick "*włączyć*" przycisk aplikacji partnera w hello menu usługi sieci Web.

Dla następujących powodów hello ta akcja nie można wykonać z profilem hello, używanego do normalnej T & E administracji.

* Witaj klient ma toobe Witaj, który kliknie "*tak*" w oknie dialogu hello, w którym jest wyświetlany po włączeniu aplikacji. Kliknij ten przycisk uznaje się, że powitania klienta jest gotowi dla tooaccess aplikacji partnera hello ich danych, więc możesz lub hello partnera nie kliknij odpowiedni przycisk Tak.

* Jeśli administrator klienta, która włączyła aplikację przy użyciu hello T & E profilu administratora pozostawia hello firmy (co w profilu hello jest dezaktywowane), wszystkie aplikacje włączone za pomocą tego profilu nie działa, aż do włączenia aplikacji hello z innym administratorem WS active profil. Jest to, dlaczego powinni toocreate różne profile WS administratora.

* Jeśli administrator pozostawia hello firmy, nazwę hello skojarzone toohello profilu WS administratora może być toohello zmienionych administratora zastąpienia, w razie potrzeby bez wpływu na powitania włączone, że aplikacji, ponieważ ten profil nie jest konieczne dezaktywowane.

**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**

1. Zaloguj się na tooyour **Concur** dzierżawy.

2. Z hello **administracji** menu, wybierz opcję **usług sieci Web**.
   
    ![Dzierżawy Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur dzierżawy")

3. Na powitania po lewej stronie, z hello **usług sieci Web** okienku wybierz **Włącz aplikacji partnera**.
   
    ![Włączanie aplikacji partnera](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "włączyć partnera aplikacji")

4. Z hello **Włącz aplikacji** listy, wybierz **usługi Azure Active Directory**, a następnie kliknij przycisk **włączyć**.
   
    ![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")

5. Kliknij przycisk **tak** tooclose hello **potwierdzenie akcji** okna dialogowego.
   
    ![Potwierdzenie akcji](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "potwierdzenie akcji")

6. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

7. Concur został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem Concur za pomocą hello pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **Concur** w galerii aplikacji hello. Wybierz Concur z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.

8. Wybierz wystąpienia programu Concur, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

9. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 
 
    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. W obszarze hello **poświadczeń administratora** wprowadź hello **nazwy użytkownika** i hello **hasło** administratora Concur.

11. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour Concur aplikację. Jeśli hello połączenia nie powiedzie się, upewnij się, że Twoje konto Concur ma uprawnienia administratora zespołu.

12. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.

13. Kliknij przycisk **zapisać.**

14. W obszarze hello sekcji mapowania, wybierz **tooConcur synchronizacji Azure Active Directory użytkowników.**

15. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooConcur. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom Concur dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

16. tooenable hello inicjowania obsługi usługi Azure AD dla Concur, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji

17. Kliknij przycisk **zapisać.**

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooConcur.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-concur-tutorial.md)

