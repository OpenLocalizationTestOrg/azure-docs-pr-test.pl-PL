---
title: "Samouczek: Konfigurowanie centralnego Cerner dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooautomatically usługi Azure Active Directory tooconfigure obsługi administracyjnej użytkowników tooa spisu w środkowej Cerner."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie centralnego Cerner dla użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w środkowej Cerner i usługi Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooa użytkownika spisu w środkowej Cerner. 


## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active Directory
*   Dzierżawy Cerner środkowe 

> [!NOTE]
> Usługa Azure Active Directory integruje się z centralnego Cerner przy użyciu hello [SCIM](http://www.simplecloud.info/) protokołu.

## <a name="assigning-users-toocerner-central"></a>Przypisywanie użytkowników tooCerner środkowe

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD są synchronizowane. 

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy podjąć decyzję dotyczącą jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooCerner centralnego. Po decyzję, można przypisać tych użytkowników tooCerner centralnego, wykonując instrukcje hello tutaj:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>Ważne porady dotyczące przypisywania użytkowników tooCerner środkowe

*   Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello centralnej tootest tooCerner inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

* Po zakończeniu testowania początkowej dla pojedynczego użytkownika centralnego Cerner zaleca przypisywanie hello całą listę użytkowników przeznaczonych tooaccess żadnych Cerner rozwiązanie (nie tylko Cerner centralnego) toobe elastycznie tooCerner przez użytkownika spisu.  Inne rozwiązania Cerner korzystać z tej listy użytkowników w hello użytkownika spisu.

*   Podczas przypisywania tooCerner użytkownika środkowe, musisz wybrać hello **użytkownika** roli w oknie dialogowym przydział hello. Użytkownicy z rolą "Domyślnego dostępu" hello są wykluczone z inicjowania obsługi administracyjnej.


## <a name="configuring-user-provisioning-toocerner-central"></a>Konfigurowanie inicjowania obsługi administracyjnej tooCerner centralnego użytkownika

Ta sekcja przeprowadzi Cię przez łączenie spisu użytkownika centralnego tooCerner usługi Azure AD przy użyciu konta użytkownika SCIM Cerner przez Inicjowanie obsługi interfejsu API i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz przypisany użytkownik kont w środkowej Cerner oparte na przydziału użytkowników i grup w usłudze Azure AD.

> [!TIP]
> Można też tooenabled na języku SAML logowania jednokrotnego dla siedziby Cerner, zgodnie z instrukcjami hello [portalu Azure (https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, że te dwie funkcje uzupełniają. Aby uzyskać więcej informacji, zobacz hello [Cerner centralnego pojedynczego logowania jednokrotnego samouczek](active-directory-saas-cernercentral-tutorial.md).


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>konto użytkownika automatyczne tooconfigure udostępniania tooCerner centralnego w usłudze Azure AD:


W kolejności tooprovision użytkownika konta tooCerner środkowa będzie muszą toorequest konto systemowe centralnego Cerner z Cerner, a Generowanie usługi Azure AD za pomocą punktu końcowego SCIM tooconnect tooCerner tokenu elementu nośnego OAuth. Zalecane jest również, że hello integracji można wykonać w środowisku piaskownicy Cerner przed wdrożeniem tooproduction.

1.  pierwszym krokiem Hello jest osób hello tooensure Zarządzanie hello Cerner i integracji z usługą Azure AD ma konto CernerCare, która jest wymagana tooaccess hello dokumentacji niezbędne toocomplete hello instrukcje. W razie potrzeby użyj adresów URL hello poniżej toocreate CernerCare kont w każdym środowisku zastosowania.

   * Piaskownicy: https://sandboxcernercare.com/accounts/create

   * Produkcji: https://cernercare.com/accounts/create  

2.  Następnie należy utworzyć konta systemu dla usługi Azure AD. Skorzystaj z instrukcji hello poniżej toorequest konto systemowe środowiska izolowanego i produkcji.

   * Instrukcje: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * Piaskownicy: https://sandboxcernercentral.com/system-accounts/

   * Produkcji: https://cernercentral.com/system-accounts/

3.  Następnie można wygenerować tokenu elementu nośnego OAuth dla każdego konta użytkownika systemu. toodo tego hello wykonaj instrukcje poniżej.

   * Instrukcje: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * Piaskownicy: https://sandboxcernercentral.com/system-accounts/

   * Produkcji: https://cernercentral.com/system-accounts/

4. Na koniec należy tooacquire identyfikatory obszaru spisu dla obu hello piaskownicy i środowiska produkcyjne w Cerner toocomplete hello konfiguracji. Aby uzyskać informacje na temat tooacquire tego, zobacz: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM. 

5. Teraz można skonfigurować tooCerner konta użytkownika tooprovision usługi Azure AD. Zaloguj się toohello [portalu Azure](https://portal.azure.com)i Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

6. Środkowe Cerner został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienia przy użyciu pola wyszukiwania hello środkowej Cerner. W przeciwnym razie wybierz **Dodaj** i wyszukaj **centralnego Cerner** w galerii aplikacji hello. Wybierz Cerner centralnego z wyników wyszukiwania hello i dodać tooyour listę aplikacji.

7.  Wybierz wystąpienie Cerner środkowej, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

8.  Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.

   ![Środkowe Cerner inicjowania obsługi administracyjnej](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  Wypełnij następujące pola w obszarze hello **poświadczeń administratora**:

   * W hello **adres URL dzierżawy** wprowadź adres URL w formacie hello poniżej, zastępując "Użytkownik-spisu-obszaru-ID" z Identyfikatorem obszaru hello uzyskaną w kroku #4.

> Piaskownicy: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> Produkcji: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * W hello **klucz tajny tokenu** wprowadź token elementu nośnego OAuth hello wygenerowany w kroku #3 i kliknij przycisk **Testuj połączenie**.

   * Powiadomienie Powodzenie powinna zostać wyświetlona po stronie upperright hello portalu usługi.

10. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i zaznacz pole wyboru hello poniżej.

11. Kliknij pozycję **Zapisz**. 

12. W hello **mapowań atrybutów** Przejrzyj hello użytkowników i grupy atrybutów toobe synchronizowane z usługi Azure AD tooCerner centralnego. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kont i grup użytkowników w centralnych Cerner dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

13. tooenable hello inicjowania obsługi usługi Azure AD dla siedziby Cerner, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji

14. Kliknij pozycję **Zapisz**. 

Spowoduje to uruchomienie synchronizacji początkowej hello żadnych użytkowników i/lub grupy przypisane tooCerner centralnego w sekcji hello użytkowników i grup. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, jak długo działa hello inicjowania obsługi usługi Azure AD. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi w aplikacji Cerner centralnego.

Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Środkowe Cerner: Publikowania danych tożsamości za pomocą usługi Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [Samouczek: Konfigurowanie centralnego Cerner na potrzeby rejestracji jednokrotnej z usługą Azure Active Directory](active-directory-saas-cernercentral-tutorial.md)
* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-enterprise-apps-manage-provisioning.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się, jak dzienniki tooreview i get raport dotyczący inicjowania obsługi administracyjnej działania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).
