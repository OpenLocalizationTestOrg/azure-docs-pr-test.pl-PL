---
title: "Inicjowanie obsługi administracyjnej zarządzania dla aplikacji przedsiębiorstwa w hello Azure Active Directory aaaUser | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak inicjowania obsługi administracyjnej dla aplikacji przedsiębiorstwa przy użyciu usługi Azure Active Directory hello konta użytkownika toomanage"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>Zarządzanie kontami użytkowników, inicjowanie obsługi administracyjnej dla aplikacji przedsiębiorstwa w hello portalu Azure
W tym artykule opisano sposób toouse hello [portalu Azure](https://portal.azure.com) konta użytkownika automatyczne toomanage aprowizację i anulowanie obsługi aplikacji obsługujących go, zwłaszcza tych, które zostały dodane z hello "witryny" kategorii Witaj [galerii aplikacji usługi Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). toolearn więcej informacji na temat Inicjowanie obsługi konta użytkowników i sposobie ich działania, zobacz [tooSaaS zautomatyzować Inicjowanie obsługi użytkowników i anulowania zastrzeżenia aplikacji za pomocą usługi Azure Active Directory](active-directory-saas-app-provisioning.md).

## <a name="finding-your-apps-in-hello-portal"></a>Znajdowanie aplikacji w portalu hello
Wszystkie aplikacje, które są skonfigurowane dla rejestracji jednokrotnej w katalogu, administrator katalogu przy użyciu hello [galerii aplikacji usługi Azure Active Directory](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), można wyświetlać i zarządzane w hello [portalu Azure](https://portal.azure.com). aplikacji Hello znajdują się w hello **więcej usług** &gt; **aplikacje dla przedsiębiorstw** sekcji hello portalu. Enterprise aplikacje to aplikacje, które są wdrożone i używane w organizacji.

![Blok aplikacje dla przedsiębiorstw][0]

Wybór hello **wszystkie aplikacje** link po lewej stronie powitania zawiera listę wszystkich aplikacji, które zostały skonfigurowane, w tym aplikacji, które dodano z galerii hello. Wybieranie aplikacji ładuje hello bloku zasobów dla danej aplikacji, w którym raporty można wyświetlać dla danej aplikacji i różne ustawienia mogą być zarządzane.

Inicjowanie obsługi administracyjnej ustawienia konta użytkownika mogą być zarządzane przez wybranie **inicjowania obsługi administracyjnej** powitania po lewej stronie.

![Bloku zasobów aplikacji][1]

## <a name="provisioning-modes"></a>Tryby inicjowania obsługi administracyjnej
Witaj **inicjowania obsługi administracyjnej** bloku rozpoczyna się od **tryb** menu, które pokazuje, jakie tryby inicjowania obsługi administracyjnej są obsługiwane w przypadku aplikacji dla przedsiębiorstw oraz pozwala toobe skonfigurowany. Witaj dostępne opcje to:

* **Automatyczne** — ta opcja jest dostępna w przypadku usługi Azure AD obsługuje automatyczne udostępnianie oparty na interfejsach API i/lub anulowanie obsługi aplikacji toothis konta użytkownika. Wybranie tego trybu powoduje wyświetlenie interfejs, który prowadzi administratorów za pośrednictwem interfejsu API zarządzania użytkownika aplikacji usługi Azure AD tooconnect toohello Konfigurowanie, tworzenie mapowania konta i przepływy pracy, które określają, jak dane konto użytkownika należy przepływ między usługą Azure AD i Aplikacja Hello i zarządzanie hello Azure AD inicjowania obsługi administracyjnej usługi.
* **Ręczne** — ta opcja jest wyświetlana, jeśli usługi Azure AD nie obsługuje automatyczne udostępnianie aplikacji toothis konta użytkownika. Ta opcja oznacza, że rekordy kont użytkowników przechowywanych w aplikacji hello musi być zarządzane przy użyciu procesu zewnętrznego, oparte na hello użytkownika zarządzania i inicjowania obsługi administracyjnej możliwości zapewniane przez aplikację (co może obejmować udostępniania SAML just in Time).

## <a name="configuring-automatic-user-account-provisioning"></a>Konfigurowanie konta użytkownika automatycznego inicjowania obsługi administracyjnej
Wybór hello **automatyczne** opcja powoduje wyświetlenie ekranu, który jest podzielony na cztery sekcje:

### <a name="admin-credentials"></a>Poświadczenia administratora
Jest to, gdzie są wprowadzane hello poświadczenia wymagane do zarządzania użytkownikami aplikacji usługi Azure AD tooconnect toohello interfejsu API. wymagane dane wejściowe Hello różni się w zależności od aplikacji hello. toolearn o typach poświadczeń hello i wymagań dotyczących konkretnych aplikacji, zobacz hello [samouczek konfiguracji dla tej konkretnej aplikacji](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning).

Wybór hello **Testuj połączenie** przycisk umożliwia poświadczenia hello tootest dzięki użyciu usługi Azure AD, spróbuj tooconnect toohello aplikacji przez aprowizowane aplikacji przy użyciu hello dostarczonych poświadczeń.

### <a name="mappings"></a>Mapowania
Jest to, gdzie Administratorzy można wyświetlać i edytować jakie przepływu atrybutów użytkownika między usługą Azure AD i hello aplikacji docelowej, gdy konta użytkowników są lub aktualizacji.

Brak zestawu wstępnie skonfigurowanych mapowania między obiektami użytkownika usługi Azure AD i każda aplikacja SaaS użytkownika. Niektóre aplikacje zarządzania innych typów obiektów, takich jak grup ani kontaktów. Wybranie jednego z tych mapowania tabeli hello Pokazuje edytor mapowania hello toohello prawo, gdzie można je wyświetlać i dostosować.

![Bloku zasobów aplikacji][2]

Obsługiwane dostosowania obejmują:

* Włączanie i wyłączanie mapowań określonych obiektów, takich jak aplikacji hello usługi Azure AD użytkownika obiektu toohello SaaS obiektu user.
* Edycja atrybutów, które przepływać z obiektu użytkownika hello Azure AD użytkownika obiektu toohello aplikacji. Aby uzyskać więcej informacji na mapowanie atrybutu, zobacz [opis atrybutu mapowania typów](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types).
* Inicjowanie obsługi akcji wykonywanych przez usługę Azure AD na powitania hello filtru przeznaczone dla aplikacji. Zamiast usługi Azure AD, w pełni synchronizowania obiektów, można ograniczyć hello akcje wykonywane. Na przykład, wybierając tylko **aktualizacji**, usługi Azure AD tylko aktualizacji istniejącego użytkownika konta w aplikacji i nie tworzyć nowe. Tylko wybierając **Utwórz**, Azure tylko tworzy nowe konta użytkowników, ale nie aktualizuje istniejące. Ta funkcja służy do mapowania różnych toocreate Administratorzy konta przepływy pracy tworzenia i aktualizacji.

### <a name="settings"></a>Ustawienia
Ta sekcja umożliwia toostart Administratorzy i Zatrzymaj hello inicjowania obsługi usługi Azure AD dla aplikacji hello zaznaczone, a także Opcjonalnie wyczyść hello inicjowania obsługi pamięci podręcznej i ponownie uruchom usługę hello.

Jeśli Inicjowanie obsługi administracyjnej jest włączana na potrzeby powitania po raz pierwszy dla aplikacji, należy włączyć usługę hello zmieniając hello **stan inicjowania obsługi administracyjnej** za**na**. Powoduje to hello Azure AD inicjowania obsługi usługi tooperform początkowej synchronizacji, w przypadku tekstu hello użytkownicy przypisani w hello **użytkowników i grup** sekcji, odpytuje hello aplikacji docelowej dla nich, a następnie wykonuje hello inicjowania obsługi administracyjnej akcje zdefiniowane w hello Azure AD **mapowania** sekcji. W trakcie tego procesu hello świadczenie usługi przechowuje dane buforowane dotyczące konta użytkownika zarządza, co nie zarządzanymi kontami wewnątrz hello docelowy aplikacje, które były nigdy nie w zakresie przypisania nie dotyczą anulowanie obsługi operacji. Po hello synchronizacji początkowej hello świadczenie usługi automatycznie synchronizuje obiektów użytkowników i grup na 10 minut.

Zmiana hello **stan inicjowania obsługi administracyjnej** za**poza** po prostu pauzy hello inicjowania obsługi usługi. W tym stanie Azure nie utworzyć, zaktualizować lub usunąć wszystkich użytkowników lub grupy obiektów w aplikacji hello. Zmiana tooon wstecz stanu hello powoduje toopick usługi hello instalacji którym przerwał pracę.

Wybór hello **wyczyścić bieżący stan i ponownie uruchomić synchronizację** wyboru i zapisywanie zatrzymuje hello inicjowania obsługi usługi, zrzuty hello w pamięci podręcznej dane dotyczące konta usługi Azure AD jest zarządzany, uruchamia ponownie usługi hello i wykonuje hello ponownie synchronizacji początkowej. Ta opcja umożliwia hello toostart Administratorzy ponownego inicjowania obsługi procesu wdrażania.

### <a name="synchronization-details"></a>Szczegóły synchronizacji
W tej sekcji przedstawiono dodanie szczegóły działania hello hello inicjowania obsługi usługi, tym hello razy imię i nazwisko hello inicjowania obsługi usługi przeprowadzony na aplikacji hello i są zarządzane jak wiele obiektów użytkowników i grup.

Łącza są udostępniane toohello **inicjowania obsługi administracyjnej raport aktywności**, zapewniające dziennik wszystkich użytkowników i grup utworzonych, zaktualizowane i usunięty między usługą Azure AD i hello aplikacji docelowej i toohello **inicjowania obsługi błędów Raport** zapewniające bardziej szczegółowe komunikaty o błędach dla użytkowników i grupy obiekty tego toobe nie powiodło się odczytać, tworzyć, zaktualizowane lub usunięte. 

##<a name="feedback"></a>Opinia

Mamy nadzieję jak środowiska usługi Azure AD. Pamiętaj o opinie hello przesyłanych! Opublikuj Twoje opinie i pomysły dotyczące poprawy na powitania **portalu administracyjnego** sekcji naszych [forum opinii](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Firma Microsoft jest podekscytowani, informacje o kompilowaniu chłodnych nowości codziennie i użyj tooshape Twojego wskazówki i zdefiniować, co mamy utworzyć w następnej kolejności.


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
