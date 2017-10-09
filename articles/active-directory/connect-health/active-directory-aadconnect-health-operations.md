---
title: operacje Active Directory Connect Health aaaAzure
description: "W tym artykule opisano dodatkowe operacje, które mogą być wykonywane po wdrożeniu usługi Azure AD Connect Health."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Operacje platformy Azure Active Directory Connect Health
W tym temacie opisano hello różne operacje można wykonywać za pomocą usługi Azure Active Directory (Azure AD) Connect Health.

## <a name="enable-email-notifications"></a>Włącz powiadomienia e-mail
Można skonfigurować powiadomienia e-mail toosend usługi Azure AD Connect Health hello, gdy alerty wskazują na to, że infrastruktury tożsamości nie jest w dobrej kondycji. Dzieje się tak, gdy alert jest generowany, a po rozwiązaniu.

![Ustawienia powiadomień pocztą e-mail programu zrzut ekranu Azure AD Connect Health](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> Powiadomienia e-mail są domyślnie włączone.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>powiadomienia e-mail tooenable usługi Azure AD Connect Health
1. Otwórz hello **alerty** bloku hello usługi, dla której ma zostać tooreceive powiadomienia e-mail.
2. Na pasku akcji powitania kliknij **ustawienia powiadomień**.
3. Przełącznik powiadomień e-mail hello, wybierz **ON**.
4. Zaznacz pole wyboru hello, jeśli chcesz, aby wszystkie powiadomienia e-mail tooreceive administratorów globalnych.
5. Chcąc tooreceive powiadomienia e-mail w inne adresy e-mail, określ je w hello **dodatkowych adresatów wiadomości E-mail** pole. tooremove adres e-mail z tej listy, kliknij prawym przyciskiem myszy wpis hello i wybierz **usunąć**.
6. toofinalize hello zmiany, kliknij przycisk **zapisać**. Zmiany zaczynają obowiązywać dopiero po zapisaniu.

## <a name="delete-a-server-or-service-instance"></a>Usuń wystąpienia usługi lub serwera

W niektórych przypadkach może być tooremove serwer z monitorowane. Oto co należy tooremove tooknow serwer z hello Azure AD Connect Health service.

W przypadku usuwania serwera, należy pamiętać o następujących hello:

* Ta akcja powoduje zatrzymanie zbierania danych z tego serwera. Ten serwer jest usuwany z hello usługi monitorowania. Po wykonaniu tej akcji nie jesteś stanie tooview nowe alerty, monitorowania lub dane analityczne użycia dla tego serwera.
* Ta akcja nie powoduje odinstalowania hello agenta programu Health z serwera. Jeśli nie odinstalowano hello agenta programu Health przed wykonaniem tej czynności, mogą występować błędy powiązane toohello agenta programu Health na powitania serwera.
* Ta akcja nie powoduje usunięcia danych hello już zebrane z tego serwera. Że dane zostaną usunięte zgodnie z hello zasady przechowywania danych platformy Azure.
* Po wykonaniu tej akcji, jeśli chcesz monitorowania toostart hello tym samym serwerze, należy odinstalować i ponownie zainstalować agenta programu Health hello na tym serwerze.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete serwer z hello Azure AD Connect Health service
Azure AD Connect Health dla usług federacyjnych Active Directory (AD FS) i Azure AD Connect (synchronizacja):

1. Otwórz hello **serwera** bloku z hello **listy serwerów** bloku, wybierając toobe nazwy serwera hello usunięte.
2. Na powitania **serwera** bloku z paska akcji hello, kliknij przycisk **usunąć**.
3. Upewnij się, wpisując nazwę serwera hello w polu potwierdzenia hello.
4. Kliknij polecenie **Usuń**.

Azure AD Connect Health dla usług domenowych w usłudze Azure Active Directory:

1. Otwórz hello **kontrolerów domeny** pulpitu nawigacyjnego.
2. Wybierz hello usunięte toobe kontrolera domeny.
3. Na pasku akcji powitania kliknij **usunąć wybrane**.
4. Potwierdź hello akcji toodelete powitania serwera.
5. Kliknij polecenie **Usuń**.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Usuń wystąpienia usługi z usługi Azure AD Connect Health
W niektórych przypadkach może być tooremove wystąpienie usługi. Oto wykonywanych muszą tooremove tooknow usługi wystąpienia z hello Azure AD Connect Health usługi.

Gdy usuwane wystąpienie usługi, należy pamiętać o następujących hello:

* Ta akcja spowoduje usunięcie bieżącego wystąpienia usługi hello z hello usługi monitorowania.
* Ta akcja nie odinstalować lub usunąć hello agenta programu Health z żadnym z serwerów hello, monitorowane w ramach tego wystąpienia usługi. Jeśli nie odinstalowano hello agenta programu Health przed wykonaniem tej czynności, mogą występować błędy powiązane toohello agenta programu Health na serwerach hello.
* Wszystkie dane z tego wystąpienia usługi zostaną usunięte zgodnie z hello zasady przechowywania danych platformy Azure.
* Po wykonaniu tej akcji, jeśli chcesz toostart monitorowanie usługi hello odinstalowanie i ponowne zainstalowanie hello agenta kondycji, na wszystkich serwerach hello. Po wykonaniu tej akcji, jeśli chcesz, aby toostart monitorowania hello na tym samym serwerze ponownie, odinstaluj, ponownie zainstaluj i zarejestruj hello agenta programu Health na tym serwerze.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete wystąpienie usługi z hello Azure AD Connect Health usługi
1. Otwórz hello **usługi** bloku z hello **listę usług** bloku, wybierając identyfikator usługi hello (nazwa farmy), które mają tooremove.
2. Na powitania **serwera** bloku z paska akcji hello, kliknij przycisk **usunąć**.
3. Upewnij się, wpisując nazwę usługi hello w polu potwierdzenia hello (na przykład: sts.contoso.com).
4. Kliknij polecenie **Usuń**.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Zarządzanie dostępem przy użyciu kontroli dostępu opartej na rolach
[Kontrola dostępu oparta na rolach (RBAC)](../role-based-access-control-configure.md) dla usługi Azure AD Connect Health udostępnia grupy innych niż administratorzy globalni i toousers dostępu. RBAC przypisuje role toohello przeznaczone użytkowników i grup i udostępnia mechanizm toolimit hello Administratorzy globalni w katalogu.

### <a name="roles"></a>Role
Azure AD Connect Health obsługuje następujące wbudowane role hello:

| Rola | Uprawnienia |
| --- | --- |
| Właściciel |Właściciele mogą *zarządzanie dostępem do* (na przykład przypisać rolę tooa użytkownika lub grupy), *wyświetlać wszystkie informacje* (na przykład wyświetlanie alertów) z portalu hello i *zmienić ustawienia* () na przykład wiadomości e-mail z powiadomieniami) w ramach usługi Azure AD Connect Health. <br>Domyślnie administratorzy globalni usługi Azure AD są przypisani do tej roli, a nie można zmienić. |
| Współautor |Współautorzy mogą *wyświetlać wszystkie informacje* (na przykład wyświetlanie alertów) z portalu hello i *zmienić ustawienia* (na przykład wiadomości e-mail z powiadomieniami) w ramach usługi Azure AD Connect Health. |
| Czytelnik |Czytelnicy mogą *wyświetlać wszystkie informacje* (na przykład wyświetlanie alertów) z portalu hello w ramach usługi Azure AD Connect Health. |

Wszystkie role (na przykład Administratorzy dostępu użytkownika lub DevTest Labs użytkowników) ma nie tooaccess wpływ w ramach usługi Azure AD Connect Health, nawet jeśli hello ról są dostępne w portalu środowisko hello.

### <a name="access-scope"></a>Zakres dostępu
Azure AD Connect Health obsługuje zarządzanie dostępem na dwóch poziomach:

* **Wszystkie wystąpienia usługi**: jest to ścieżka w większości przypadków zalecane hello. Określa dostęp do wszystkich wystąpień usługi (na przykład farmy usług AD FS), wszystkich typów roli, które są monitorowane przez program Azure AD Connect Health.
* **Wystąpienie usługi**: W niektórych przypadkach może być konieczne toosegregate dostępu na podstawie typów roli lub przez wystąpienie usługi. W takim przypadku można zarządzać dostęp na poziomie wystąpienia usługi hello.  

Uprawnienie zostanie udzielone, jeśli użytkownik ma dostęp w katalogu hello lub usługi wystąpienie poziomu.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>Zezwalaj użytkownikom lub grupom dostępu tooAzure AD Connect Health
Witaj poniższej procedurze pokazano, jak uzyskać dostęp do tooallow.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>Krok 1: Wybierz zakres dostępu odpowiednie hello
tooallow użytkownikowi dostępu na powitania *wszystkich wystąpień usługi* poziomu w ramach usługi Azure AD Connect Health, otwórz hello głównego bloku w Azure AD Connect Health.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>Krok 2: Dodawanie użytkowników i grup i przypisz role
1. Z hello **Konfiguruj** kliknij **użytkowników**.<br>
   ![Zrzut ekranu Azure AD Connect Health RBAC głównego bloku użytkownikom wyróżnione](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. Wybierz pozycję **Dodaj**.
3. W hello **wybierz rolę** okienku, wybierz rolę (na przykład **właściciela**).<br>
   ![Zrzut ekranu Azure AD Connect Health RBAC użytkowników okna](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Wpisz nazwę hello lub identyfikator hello przeznaczone dla użytkownika lub grupy. Można wybrać jeden lub więcej użytkowników lub grup w hello tym samym czasie. Kliknij pozycję **Wybierz**.
   ![Zrzut ekranu Azure AD Connect Health RBAC użytkowników okna](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. Kliknij przycisk **OK**.<br>
6. Po zakończeniu przypisania roli hello hello użytkowników i grup są wyświetlane na liście hello.<br>
   ![Zrzut ekranu Azure AD Connect Health RBAC użytkowników okno, przy użyciu nowych użytkowników wyróżnione](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Teraz hello wymienione użytkownicy i grupy mają dostęp, zgodnie z tootheir przypisane role.

> [!NOTE]
> * Administratorzy globalni zawsze mają pełny dostęp tooall hello operacji, ale nie są obecne w powyższej listy hello konta administratora globalnego.
> * Funkcja zaprosić użytkowników Hello nie jest obsługiwana w ramach usługi Azure AD Connect Health.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>Krok 3: Udostępnianie lokalizacji bloku hello użytkowników lub grup
1. Po przypisaniu uprawnienia, użytkownik może uzyskać dostęp Azure AD Connect Health, przechodząc [tutaj](http://aka.ms/aadconnecthealth).
2. W bloku hello hello użytkownika można przypiąć blok hello lub różnych części toohello pulpitu nawigacyjnego. Po prostu kliknij hello **toodashboard numeru Pin** ikony.<br>
   ![Zrzut ekranu Azure AD Connect Health RBAC Przypnij blok z ikonę pinezki podświetlone](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Użytkownik z przypisać rolę czytelnika hello nie jest rozszerzeniem Azure AD Connect Health stanie tooget z hello Azure Marketplace. Witaj użytkownika nie można wykonać tak hello niezbędne "Utwórz" toodo operacji. Użytkownik Hello nadal może uzyskać bloku toohello przez przejście toohello poprzedzających łącza. Kolejne użycia hello użytkownika można przypiąć hello bloku toohello w pulpicie nawigacyjnym.
>
>

### <a name="remove-users-or-groups"></a>Usuwanie użytkowników lub grup
Można usunąć użytkownika lub grupę, dodano tooAzure AD Connect Health RBAC. Po prostu kliknij prawym przyciskiem myszy hello użytkownika lub grupy i wybierz **Usuń**.<br>
![Zrzut ekranu Azure AD Connect Health RBAC użytkowników okna, z Usuń wyróżniony](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Następne kroki
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalowanie agenta programu Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md)
* [Używanie programu Azure AD Connect Health w celu synchronizacji](active-directory-aadconnect-health-sync.md)
* [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health — często zadawane pytania](active-directory-aadconnect-health-faq.md)
* [Historia wersji programu Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
