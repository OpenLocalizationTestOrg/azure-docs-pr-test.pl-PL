---
title: "połączenia aaaITSM w OMS IT usługi zarządzania łącznika | Dokumentacja firmy Microsoft"
description: "Połączenie Zarządzanie usługami IT — produktów/usług z łącznika zarządzania usługi IT w monitorze toocentrally OMS i elementy robocze hello Zarządzanie usługami IT — zarządzanie."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>Zarządzanie usługami IT — produktów/usług Uzyskuj dostęp do łącznika zarządzania usługi IT (wersja zapoznawcza)
Ten artykuł zawiera informacje o tym, jak tooconnect Twojego tooIT produktów i usług Zarządzanie usługami IT — usługi zarządzania łącznika w OMS i centralnie zarządzać elementami pracy. Więcej informacji na temat łącznika zarządzania usługi IT, zobacz [omówienie](log-analytics-itsmc-overview.md).

obsługiwane są Hello następujących produktów i usług:

- [Program System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [Usługi ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>Połącz tooIT System Center Service Manager łącznik usługi zarządzania w OMS

Witaj poniższe sekcje zawierają szczegółowe informacje na temat tooconnect Twojego toohello produktu System Center Service Manager Łącznik zarządzania usługi IT w OMS.

### <a name="prerequisites"></a>Wymagania wstępne

Upewnij się, że masz hello następujące wymagania wstępne zostały spełnione:

- Zainstalowany łącznik zarządzania usługi IT.
Więcej informacji: [konfiguracji](log-analytics-itsmc-overview.md#configuration).
- Witaj aplikacji sieci Web programu Service Manager (aplikacja sieci Web) jest wdrożone i skonfigurowane. Informacje dotyczące aplikacji sieci Web jest [tutaj](#create-and-deploy-service-manager-web-app-service).
- Połączenia hybrydowe utworzone i skonfigurowane. Więcej informacji: [skonfiguruj hybrydowych hello połączenia](#configure-the-hybrid-connection).
- Obsługiwane wersje programu Service Manager: 2012 R2 lub 2016.
- Rola użytkownika: [operator zaawansowany](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Procedura połączenia

Użyj programu System Center Service Manager toohello wystąpienia łącznika zarządzania usługi IT powitania po tooconnect procedury:

1. Przejdź za**OMS** >**ustawienia** > **połączonych źródeł**.
2. Wybierz **łącznika Zarządzanie usługami IT —** kliknij **Dodawanie nowego połączenia**.

    ![Programu Service manager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. Podaj informacje hello, zgodnie z opisem w poniższej tabeli hello, a następnie kliknij przycisk **zapisać** toocreate hello połączenia:

> [!NOTE]
> Te parametry są obowiązkowe.

| **Pole** | **Opis** |
| --- | --- |
| **Nazwa**   | Wpisz nazwę wystąpienia programu System Center Service Manager hello, które mają tooconnect z hello łącznika zarządzania usługi IT.  Możesz użyć tej nazwy później skonfigurować elementy robocze w tym wystąpieniu / wyświetlić szczegółowy dziennik analizy. |
| **Wybierz typ połączenia**   | Wybierz **programu System Center Service Manager**. |
| **Adres URL serwera**   | Wpisz adres URL hello hello aplikacji sieci Web programu Service Manager. Więcej informacji na temat aplikacji sieci Web programu Service Manager jest [tutaj](#create-and-deploy-service-manager-web-app-service).
| **Identyfikator klienta**   | Wpisz identyfikator klienta hello możesz wygenerowania (przy użyciu skryptu automatycznego hello) w celu uwierzytelniania aplikacji sieci Web hello. Więcej informacji na temat skryptu automatycznego hello jest [tutaj.](log-analytics-itsmc-service-manager-script.md)|
| **Klucz tajny klienta**   | Typ klucza tajnego klienta hello, generowany dla tego identyfikatora.   |
| **Zakres synchronizacji danych**   | Wybierz elementy robocze programu Service Manager hello, które mają toosync za pośrednictwem hello łącznika zarządzania usługi IT.  Pracy, te elementy są importowane do analizy dzienników. **Opcje:** incydenty, żądania zmiany.|
| **Synchronizowanie danych** | Wpisz numer hello hello dane z ostatnich dni. **Maksymalny limit**: 120 dni. |
| **Utwórz nowy element konfiguracji w rozwiązaniu Zarządzanie usługami IT —** | Wybierz tę opcję, jeśli chcesz, aby elementy konfiguracji hello toocreate w produkcie Zarządzanie usługami IT — Witaj. Po wybraniu pakietu OMS tworzy hello dotyczy konfiguracji (ci) jako elementy konfiguracji (w przypadku nieistniejących SIC) w hello obsługiwane zarządzanie usługami IT — system. **Domyślna**: wyłączone. |

Gdy pomyślnie nawiązano połączenie i zsynchronizowane:

- Wybrane elementy robocze z programu Service Manager są importowane do OMS **analizy dzienników.** Można wyświetlić podsumowanie hello tych elementów roboczych na powitania kafelka łącznika zarządzania usługi IT.

- Z usługą OMS można utworzyć zdarzenia z alertów OMS lub wyszukiwania dziennika, w tym wystąpieniu programu Service Manager.

Więcej informacji: [Zarządzanie usługami IT — tworzenie elementów roboczych dla alertów OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) i [Zarządzanie usługami IT — tworzenie elementów roboczych z dzienników OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Tworzenie i wdrażanie aplikacji sieci web programu Service Manager

tooconnect hello lokalnymi Service Manager z hello IT usługi zarządzania łącznika na OMS, firma Microsoft opracowała aplikację sieci Web programu Service Manager na powitania GitHub.

tooset zapasowej aplikacji sieci Web Zarządzanie usługami IT — Witaj dla programu Service Manager, hello następujące:

- **Aplikacja sieci Web Deploy hello** — wdrażanie aplikacji sieci Web hello, ustaw właściwości hello i uwierzytelniania za pomocą usługi Azure AD. Możesz wdrożyć aplikację sieci web hello przy użyciu hello [zautomatyzowanego skryptu](log-analytics-itsmc-service-manager-script.md) że firma Microsoft udostępnia należy.
- **Skonfiguruj połączenie hybrydowe hello** - [Skonfiguruj połączenie z tym](#configure-the-hybrid-connection), ręcznie.

#### <a name="deploy-hello-web-app"></a>Wdrażanie aplikacji sieci web hello
Użyj hello automatycznego [skryptu](log-analytics-itsmc-service-manager-script.md) toodeploy hello aplikacji sieci Web, ustaw właściwości hello i uwierzytelniania za pomocą usługi Azure AD.

Uruchom skrypt hello zapewniając hello następujące wymagane szczegóły:

- Szczegóły subskrypcji platformy Azure
- Nazwa grupy zasobów
- Lokalizacja
- Szczegóły serwera programu Service Manager (nazwa serwera, domeny, nazwę użytkownika i hasło)
- Prefiks nazwy witryny dla aplikacji sieci Web
- Namespace magistrali usług.

Witaj skrypt tworzy hello aplikacji sieci Web przy użyciu podanej nazwy hello (wraz z kilku toomake dodatkowe ciągi on unikatowy). Generuje hello **adres URL aplikacji sieci Web**, **identyfikator klienta** i **klucz tajny klienta**.

Zapisz hello wartości możesz użyć ich podczas tworzenia połączenia z łącznikiem zarządzania usługi IT.

**Sprawdź instalację aplikacji sieci Web hello**

1. Przejdź za**portalu Azure** > **zasobów**.
2. Wybierz aplikację sieci Web hello, kliknij przycisk **ustawienia** > **ustawienia aplikacji**.
3. Potwierdź hello informacji na temat wystąpienia programu Service Manager hello podane w czasie hello wdrażania aplikacji hello za pośrednictwem hello skryptu.

### <a name="configure-hello-hybrid-connection"></a>Skonfiguruj połączenie hybrydowe hello

Użyj hello następujące procedury tooconfigure hello hybrydowego połączenie, które łączy hello wystąpienia programu Service Manager z hello łącznika zarządzania usługi IT w OMS.

1. Znajdź hello aplikacji sieci Web programu Service Manager w obszarze **zasobów Azure**.
2. Kliknij przycisk **ustawienia** > **sieci**.
3. W obszarze **połączeń hybrydowych**, kliknij przycisk **skonfiguruj punkty końcowe połączenia hybrydowego**.

    ![Sieciowe połączenie hybrydowe](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. W hello **połączeń hybrydowych** bloku, kliknij przycisk **Dodaj połączenie hybrydowe**.

    ![Dodaj połączenie hybrydowe](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. W hello **dodać połączeń hybrydowych** bloku, kliknij przycisk **tworzenie hybrydowych nowego połączenia**.

    ![Nowe połączenie hybrydowe](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Wpisz hello następujące wartości:

    - **Nazwa punktu końcowego**: Określ nazwę dla nowego połączenia hybrydowe hello.
    -  **Punkt końcowy hosta**: nazwa FQDN serwera zarządzania programu Service Manager hello.
    - **Port punktu końcowego**: wpisz 5724
    - **Przestrzeń nazw magistrali usług**: Użyj istniejącej przestrzeni nazw magistrali usług lub Utwórz nową.
    - **Lokalizacja**: Wybierz lokalizację hello.
    -  **Nazwa**: Określ magistrali toohello nazwę, jeśli jej tworzenia.

    ![Wartości połączenia hybrydowego](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Kliknij przycisk **OK** tooclose hello **Tworzenie połączenia hybrydowego** bloku i rozpocząć tworzenie połączenia hybrydowego hello.

    Po utworzeniu połączenia hybrydowego hello jest wyświetlany w obszarze hello bloku.

7. Po utworzeniu połączenia hybrydowego hello wybierz hello połączeń i kliknij przycisk **Dodaj wybrane połączenie hybrydowe**.

    ![Nowe połączenie hybrydowe](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Skonfiguruj ustawienia odbiornika hello

Po zakończeniu instalacji odbiornika hello tooconfigure procedury połączenia hybrydowego hello hello użycia.

1. W hello **połączeń hybrydowych** bloku, kliknij przycisk **hello pobierania Menedżera połączeń** i zainstaluj go na komputerze hello, w którym jest uruchomione wystąpienie programu System Center Service Manager.

    Po zakończeniu instalacji hello **interfejsu użytkownika Menedżera połączeń hybrydowych** opcja jest dostępna w obszarze **Start** menu.

2. Kliknij przycisk **interfejsu użytkownika Menedżera połączeń hybrydowych** , zostanie wyświetlony monit o podanie poświadczeń platformy Azure.

3. Logowanie przy użyciu poświadczeń platformy Azure i wybierz subskrypcję, w której został utworzony hello połączenia hybrydowego.

4. Kliknij pozycję **Zapisz**.

Połączenia hybrydowe został pomyślnie połączony.

![połączenia hybrydowe powiodło się](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Po utworzeniu połączenia hybrydowego hello Sprawdź i Testuj połączenie hello odwiedzając hello wdrożonych aplikacji sieci Web programu Service Manager. Upewnij się, że połączenie hello zostanie nawiązane, przed podjęciem próby toohello tooconnect łącznika zarządzania usługi IT w OMS.

Witaj poniższy obraz przedstawia szczegóły hello połączenia:

![Testowanie połączenia hybrydowego](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>Połączenie usługi ServiceNow tooIT łącznika usługi zarządzania w OMS

Witaj poniższe sekcje zawierają szczegółowe informacje na temat tooconnect Twojego toohello produktu usługi ServiceNow łącznika zarządzania usługi IT w OMS.

### <a name="prerequisites"></a>Wymagania wstępne

Upewnij się, że masz hello następujące wymagania wstępne zostały spełnione:

- Zainstalowany łącznik zarządzania usługi IT. Więcej informacji: [konfiguracji.](log-analytics-itsmc-overview.md#configuration)
- Usługi ServiceNow obsługiwane wersje — Fuji, serwera Geneva, Helsinkach.

Administratorzy usługi ServiceNow należy wykonać hello następujący po ich wystąpienia usługi ServiceNow:
- Generuj identyfikator klienta i klucz tajny klienta hello usługi ServiceNow produktu. Aby uzyskać informacje dotyczące sposobu toogenerate identyfikator klienta i klucz tajny, zobacz [instalacji uwierzytelniania OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup).
- Zainstaluj hello użytkownika aplikacji do integracji OMS firmy Microsoft (usługi ServiceNow aplikacji). [Dowiedz się więcej](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).
- Utworzenie roli użytkownika integracji dla hello użytkownika aplikacja jest zainstalowana. Informacje o jak rola użytkownika integracji hello toocreate jest [tutaj](#create-integration-user-role-in-servicenow-app).


### <a name="connection-procedure"></a>**Procedura połączenia**

Użyj hello następujące procedury toocreate połączenie usługi ServiceNow:

1. Przejdź za**OMS** > **ustawienia** > **połączonych źródeł**.
2. Wybierz **łącznika Zarządzanie usługami IT —** kliknij **Dodawanie nowego połączenia**.

    ![Połączenie usługi ServiceNow](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. Podaj informacje hello, zgodnie z opisem w poniższej tabeli hello, a następnie kliknij przycisk **zapisać** toocreate hello połączenia:

> [!NOTE]
> Te parametry są obowiązkowe.

| **Pole** | **Opis** |
| --- | --- |
| **Nazwa**   | Wpisz nazwę wystąpienia usługi ServiceNow hello, które mają tooconnect z hello łącznika zarządzania usługi IT.  Ta nazwa można użyć w dalszej części OMS, podczas konfigurowania elementów roboczych w tym zarządzanie usługami IT — / wyświetlić szczegółowy dziennik analizy. |
| **Wybierz typ połączenia**   | Wybierz **ServiceNow**. |
| **Nazwa użytkownika**   | Wpisz nazwę użytkownika integracji hello utworzony w hello usługi ServiceNow aplikacji toosupport hello połączenia toohello łącznika zarządzania usługi IT. Więcej informacji: [roli użytkownika aplikacji tworzenia usługi ServiceNow](#create-integration-user-role-in-servicenow-app).|
| **Hasło**   | Wpisz hasło hello skojarzone z tą nazwą użytkownika. **Uwaga**: nazwa użytkownika i hasło są używane do generowania tokenów uwierzytelniania tylko, a nie są przechowywane w dowolnym miejscu w hello usługę.  |
| **Adres URL serwera**   | Wpisz adres URL hello hello wystąpienia usługi ServiceNow, które mają tooIT tooconnect łącznika usługi zarządzania. |
| **Identyfikator klienta**   | Wpisz identyfikator klienta hello, który ma toouse do uwierzytelniania protokołu OAuth2, który można wygenerować wcześniej.  Więcej informacji na temat generowania identyfikator klienta i klucz tajny: [instalacji uwierzytelniania OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup). |
| **Klucz tajny klienta**   | Typ klucza tajnego klienta hello, generowany dla tego identyfikatora.   |
| **Zakres synchronizacji danych**   | Wybierz elementy robocze usługi ServiceNow hello, które mają tooOMS toosync, za pośrednictwem hello łącznika zarządzania usługi IT.  Witaj wybrane wartości są importowane do analizy dzienników.   **Opcje:** zdarzenia i żądania zmiany.|
| **Synchronizowanie danych** | Wpisz numer hello hello dane z ostatnich dni. **Maksymalny limit**: 120 dni. |
| **Utwórz nowy element konfiguracji w rozwiązaniu Zarządzanie usługami IT —** | Wybierz tę opcję, jeśli chcesz, aby elementy konfiguracji hello toocreate w produkcie Zarządzanie usługami IT — Witaj. Po wybraniu pakietu OMS tworzy hello dotyczy konfiguracji (ci) jako elementy konfiguracji (w przypadku nieistniejących SIC) w hello obsługiwane zarządzanie usługami IT — system. **Domyślna**: wyłączone. |


Gdy pomyślnie nawiązano połączenie i zsynchronizowane:

- Wybrane elementy z połączenia usługi ServiceNow są importowane do analizy dzienników OMS pracy.  Można wyświetlić podsumowanie hello tych elementów roboczych na powitania kafelka łącznika zarządzania usługi IT.
- Można utworzyć zdarzenia, alerty i zdarzenia z alertów OMS lub dziennik wyszukiwania w tym wystąpieniu usługi ServiceNow.  


Więcej informacji: [Zarządzanie usługami IT — tworzenie elementów roboczych dla alertów OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) i [Zarządzanie usługami IT — tworzenie elementów roboczych z dzienników OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-integration-user-role-in-servicenow-app"></a>Utworzenie roli użytkownika integracji usługi ServiceNow aplikacji

Witaj użytkownika następujące procedury:

1.  Odwiedź hello [magazynu usługi ServiceNow](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) i zainstaluj hello **użytkownika aplikacji dla usługi ServiceNow i integracja z usługą OMS Microsoft** do swojego wystąpienia usługi ServiceNow.
2.  Po zakończeniu instalacji odwiedź stronę hello pozostałych pasku nawigacyjnym hello wystąpienia usługi ServiceNow, wyszukaj i wybierz integrator OMS firmy Microsoft.  
3.  Kliknij przycisk **listy kontrolnej instalacji**.

    zostanie wyświetlony stan Hello **nie zakończyć** Jeśli hello roli użytkownika jest jeszcze utworzone toobe.

4.  W tekście hello pola, obok zbyt**tworzenia integracji użytkownika**, wprowadź nazwę użytkownika hello hello użytkownik, który można połączyć toohello łącznika zarządzania usługi IT w OMS.
5.  Wprowadź hasło powitania dla tego użytkownika, a następnie kliknij przycisk **OK**.  

>[!NOTE]

> Połączenia te poświadczenia toomake hello usługi ServiceNow w OMS.

Witaj nowo utworzony użytkownik zostanie wyświetlony z hello domyślne role przypisane.

Domyślne role:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.user
-   ITIL
-   template_editor
-   view_changer

Po pomyślnym utworzeniu użytkownika hello hello stan **Sprawdź listę kontrolną instalacji** tooCompleted, wyświetlania szczegółów hello hello roli użytkownika utworzone dla aplikacji hello są przenoszone.

> [!NOTE]

> tooallow toocreate użytkownika **alerty** i **zdarzenia** w usługi ServiceNow z usługą OMS:

> - Upewnij się, że moduł zarządzania zdarzeniami hello zainstalowane w wystąpieniu usługi ServiceNow.

> - Dodaj następujące role toohello integracji użytkownika hello:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>Połącz tooIT Provance łącznika usługi zarządzania w OMS

Witaj poniższe sekcje zawierają szczegółowe informacje na temat tooconnect Twojego toohello produktu Provance łącznika zarządzania usługi IT w OMS.

### <a name="prerequisites"></a>Wymagania wstępne

Upewnij się, że masz hello następujące wymagania wstępne zostały spełnione:

- Zainstalowany łącznik zarządzania usługi IT. Więcej informacji: [konfiguracji](log-analytics-itsmc-overview.md#configuration).
- Provance aplikacji powinny zostać zarejestrowane w usłudze Azure AD - oraz Identyfikatora klienta jest dostępna. Aby uzyskać szczegółowe informacje, zobacz [sposób uwierzytelniania usługi active directory tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
- Rola: Administrator.

### <a name="connection-procedure"></a>Procedura połączenia

Użyj hello następujące procedury toocreate połączenia Provance:

1. Przejdź za**OMS** > **ustawienia** > **połączonych źródeł**.
2. Wybierz **łącznika Zarządzanie usługami IT —** kliknij **Dodawanie nowego połączenia**.  

    ![Provance połączenia](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. Podaj informacje hello, zgodnie z opisem w poniższej tabeli hello, a następnie kliknij przycisk **zapisać** toocreate hello połączenia.

> [!NOTE]
> Te parametry są obowiązkowe.

| **Pole** | **Opis** |
| --- | --- |
| **Nazwa**   | Wpisz nazwę wystąpienia Provance hello, które mają tooconnect z hello łącznika zarządzania usługi IT.  Ta nazwa można użyć w dalszej części OMS, podczas konfigurowania elementów roboczych w tym zarządzanie usługami IT — / wyświetlić szczegółowy dziennik analizy. |
| **Wybierz typ połączenia**   | Wybierz **Provance**. |
| **Nazwa użytkownika**   | Wpisz nazwę użytkownika hello podłączoną toohello łącznika zarządzania usługi IT.    |
| **Hasło**   | Wpisz hasło hello skojarzone z tą nazwą użytkownika. **Uwaga:** nazwę użytkownika i hasło są używane do generowania tokenów uwierzytelniania tylko, a nie są przechowywane w dowolnym miejscu w usługę hello. _|
| **Adres URL serwera**   | Wpisz adres URL hello Provance wystąpienia, które mają tooIT tooconnect łącznika usługi zarządzania. |
| **Identyfikator klienta**   | Wpisz identyfikator klienta hello do uwierzytelniania połączenia, który można wygenerować wystąpienia Provance.  Więcej informacji na temat Identyfikatora klienta, zobacz [sposób uwierzytelniania usługi active directory tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Zakres synchronizacji danych**   | Wybierz elementy robocze Provance hello, które mają tooOMS toosync, za pośrednictwem hello łącznika zarządzania usługi IT.  Pracy, te elementy są importowane do analizy dzienników.   **Opcje:** incydenty, żądania zmiany.|
| **Synchronizowanie danych** | Wpisz numer hello hello dane z ostatnich dni. **Maksymalny limit**: 120 dni. |
| **Utwórz nowy element konfiguracji w rozwiązaniu Zarządzanie usługami IT —** | Wybierz tę opcję, jeśli chcesz, aby elementy konfiguracji hello toocreate w produkcie Zarządzanie usługami IT — Witaj. Po wybraniu pakietu OMS tworzy hello dotyczy konfiguracji (ci) jako elementy konfiguracji (w przypadku nieistniejących SIC) w hello obsługiwane zarządzanie usługami IT — system. **Domyślna**: wyłączone.|

Gdy pomyślnie nawiązano połączenie i zsynchronizowane:

- Wybrane elementy robocze z połączenia Provance są importowane do OMS **analizy dzienników.**  Można wyświetlić podsumowanie hello tych elementów roboczych na powitania kafelka łącznika zarządzania usługi IT.
- W tym wystąpieniu Provance można utworzyć zdarzenia i zdarzenia z alertów OMS lub dziennik wyszukiwania.

Więcej informacji: [Zarządzanie usługami IT — tworzenie elementów roboczych dla alertów OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) i [Zarządzanie usługami IT — tworzenie elementów roboczych z dzienników OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Połącz tooIT Cherwell łącznika usługi zarządzania w OMS

Witaj poniższe sekcje zawierają szczegółowe informacje na temat tooconnect Twojego toohello produktu Cherwell łącznika zarządzania usługi IT w OMS.

### <a name="prerequisites"></a>Wymagania wstępne

Upewnij się, że masz hello następujące wymagania wstępne zostały spełnione:

- Zainstalowany łącznik zarządzania usługi IT. Więcej informacji: [konfiguracji](log-analytics-itsmc-overview.md#configuration).
- Wygenerowany identyfikator klienta. Więcej informacji: [generowania Identyfikatora klienta dla Cherwell](#generate-client-id-for-cherwell).
- Rola: Administrator.

### <a name="connection-procedure"></a>Procedura połączenia

Użyj hello następujące procedury toocreate połączenia Cherwell:

1. Przejdź za**OMS** >  **ustawienia** > **połączonych źródeł**.
2. Wybierz **łącznika Zarządzanie usługami IT —** kliknij **Dodawanie nowego połączenia**.  

    ![Identyfikator użytkownika Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. Podaj informacje hello, zgodnie z opisem w poniższej tabeli hello, a następnie kliknij przycisk **zapisać** toocreate hello połączenia.

> [!NOTE]
> Te parametry są obowiązkowe.

| **Pole** | **Opis** |
| --- | --- |
| **Nazwa**   | Wpisz nazwę wystąpienia Cherwell hello, które mają toohello tooconnect łącznika zarządzania usługi IT.  Ta nazwa można użyć w dalszej części OMS, podczas konfigurowania elementów roboczych w tym zarządzanie usługami IT — / wyświetlić szczegółowy dziennik analizy. |
| **Wybierz typ połączenia**   | Wybierz **Cherwell.** |
| **Nazwa użytkownika**   | Wpisz nazwę użytkownika Cherwell hello podłączoną toohello łącznika zarządzania usługi IT. |
| **Hasło**   | Wpisz hasło hello skojarzone z tą nazwą użytkownika. **Uwaga:** nazwę użytkownika i hasło są używane do generowania tokenów uwierzytelniania tylko, a nie są przechowywane w dowolnym miejscu w hello usługę.|
| **Adres URL serwera**   | Wpisz adres URL hello Cherwell wystąpienia, które mają tooIT tooconnect łącznika usługi zarządzania. |
| **Identyfikator klienta**   | Wpisz identyfikator klienta hello do uwierzytelniania połączenia, który można wygenerować wystąpienia Cherwell.   |
| **Zakres synchronizacji danych**   | Wybierz elementy robocze Cherwell hello, które mają toosync za pośrednictwem hello łącznika zarządzania usługi IT.  Pracy, te elementy są importowane do analizy dzienników.   **Opcje:** incydenty, żądania zmiany. |
| **Synchronizowanie danych** | Wpisz numer hello hello dane z ostatnich dni. **Maksymalny limit**: 120 dni. |
| **Utwórz nowy element konfiguracji w rozwiązaniu Zarządzanie usługami IT —** | Wybierz tę opcję, jeśli chcesz, aby elementy konfiguracji hello toocreate w produkcie Zarządzanie usługami IT — Witaj. Po wybraniu pakietu OMS tworzy hello dotyczy konfiguracji (ci) jako elementy konfiguracji (w przypadku nieistniejących SIC) w hello obsługiwane zarządzanie usługami IT — system. **Domyślna**: wyłączone. |

Gdy pomyślnie nawiązano połączenie i zsynchronizowane:

- Wybrane elementy z tego połączenia Cherwell są importowane do analizy dzienników OMS pracy. Można wyświetlić podsumowanie hello tych elementów roboczych na powitania kafelka łącznika zarządzania usługi IT.
- Można utworzyć zdarzenia i zdarzeń w tym wystąpieniu Cherwell z usługą OMS. Więcej informacji: tworzenie elementów roboczych Zarządzanie usługami IT — OMS alertów i zarządzanie usługami IT — tworzenie elementach z dzienników OMS.

Więcej informacji: [Zarządzanie usługami IT — tworzenie elementów roboczych dla alertów OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) i [Zarządzanie usługami IT — tworzenie elementów roboczych z dzienników OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="generate-client-id-for-cherwell"></a>Generuj identyfikator klienta dla Cherwell

toogenerate powitania klienta identyfikator/klucz Cherwell, hello użyj następującej procedury:

1. Zaloguj się w tooyour Cherwell wystąpienia jako administrator.
2. Kliknij przycisk **zabezpieczeń** > **ustawień klienta interfejsu API REST Edytuj**.
3. Wybierz **Utwórz nowy klient** > **klucz tajny klienta**.

    ![Identyfikator użytkownika Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Następne kroki
 - [Tworzenie elementów roboczych Zarządzanie usługami IT — OMS alertów](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [Tworzenie elementów roboczych Zarządzanie usługami IT — z dzienników OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [Widok analizy dzienników dla połączenia](log-analytics-itsmc-overview.md#using-the-solution)
