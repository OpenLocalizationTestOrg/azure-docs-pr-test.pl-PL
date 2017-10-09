---
title: 'Samouczek: Integracji Azure Active Directory z Dropbox dla firm | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i skrzynki dla firm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie skrzynki dla firm użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Dropbox dla firm i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooDropbox dla firm.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Dropbox dla firm jednokrotnego włączone subskrypcji.
*   Konto użytkownika w Dropbox dla firm z uprawnieniami administratora zespołu.

## <a name="assigning-users-toodropbox-for-business"></a>Przypisywanie użytkowników tooDropbox dla firm

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour Dropbox dla aplikacji biznesowych. Po decyzję, można przypisać te skrzynki tooyour użytkowników dla aplikacji biznesowych, wykonując instrukcje hello tutaj:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>Ważne porady dotyczące przypisywania tooDropbox użytkowników dla firm

*   Zalecane jest jeden użytkownik usługi Azure AD jest przypisany tooDropbox dla firm tootest hello inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooDropbox użytkownika dla firm, należy wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-automated-user-provisioning"></a>Włącz automatyczne Inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi Cię przez łączenie z tooDropbox usługi Azure AD dla konta użytkownika firmy inicjowania obsługi interfejsu API i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Dropbox dla firm, w oparciu o użytkowników i grup przypisania w usłudze Azure AD.

>[!Tip]
>Można też tooenabled na języku SAML logowania jednokrotnego dla skrzynki dla firm, hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure użytkownika automatyczne Inicjowanie obsługi konta:

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Jeśli skonfigurowano już program Dropbox dla firm dla logowania jednokrotnego, wyszukaj dla swojego wystąpienia usługi Dropbox dla firm przy użyciu pola wyszukiwania hello. W przeciwnym razie wybierz **Dodaj** i wyszukaj **Dropbox dla firm** w galerii aplikacji hello. Wybierz Dropbox dla firm z wyników wyszukiwania hello i dodać tooyour listy aplikacji.

3. Wybierz wystąpienie usługi Dropbox dla firm, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. W obszarze hello **poświadczeń administratora** kliknij **autoryzacji**. Dropbox dla okna dialogowego logowania biznesowych zostanie otwarty w nowym oknie przeglądarki.

6. Na powitania **logowania toolink tooDropbox z usługą Azure AD** dialogowym logowania tooyour Dropbox dla dzierżawy biznesowych.

     ![Inicjowanie obsługi użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Inicjowanie obsługi użytkowników")

7. Upewnij się, chcieliby tooyour zmiany toomake uprawnienia usługi Azure Active Directory toogive Dropbox dla firm dzierżawcy. Kliknij przycisk **Zezwalaj**.
    
      ![Inicjowanie obsługi użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Inicjowanie obsługi użytkowników")

8. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour Dropbox dla aplikacji biznesowych. W przypadku niepowodzenia połączenia hello zapewnić usłudze Dropbox konto firmowe, ma uprawnienia administratora zespołu i spróbuj hello **"Autoryzuj"** krok ponownie.

9. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.

10. Kliknij przycisk **zapisać.**

11. W obszarze hello sekcji mapowania, wybierz **tooDropbox synchronizacji Azure Active Directory użytkowników dla firm.**

12. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooDropbox dla firm. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom skrzynki dla firm dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

13. tooenable hello inicjowania obsługi usługi Azure AD dla skrzynki dla firm, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello

14. Kliknij przycisk **zapisać.**

Rozpoczyna się hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooDropbox dla firm w hello użytkowników i grup sekcji. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello świadczenie usługi w usłudze Dropbox dla aplikacji biznesowych.

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooDropbox dla firm.

Użytkownik pomyślnie zakończono inicjowanie obsługi cyklu wskazuje stan powiązane.

![Przypisywanie użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "przypisywanie użytkowników")


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-dropboxforbusiness-tutorial.md)