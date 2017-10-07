---
title: "powiadomienia aaaConfigure i szablonów w usłudze Azure API Management wiadomości e-mail | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure powiadomienia i szablonów w usłudze Azure API Management wiadomości e-mail."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>Jak tooconfigure powiadomienia i szablonów w usłudze Azure API Management wiadomości e-mail
Zarządzanie interfejsami API umożliwia określenie hello tooconfigure powiadomienia dla określonych zdarzeń i tooconfigure hello e-mail szablonów, które są używane toocommunicate z hello Administratorzy i deweloperzy wystąpienia interfejsu API zarządzania. W tym temacie pokazano, jak tooconfigure powiadomienia dla hello zdarzenia dostępne i zawiera omówienie konfigurowania hello szablonów wiadomości e-mail używany dla tych zdarzeń.

## <a name="publisher-notifications"></a>Skonfigurować powiadomienia o wydawcy
tooconfigure powiadomień, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API. Trwa toohello zarządzanie interfejsami API wydawcy portalu.

![Portal wydawcy][api-management-management-console]

> [!NOTE] 
> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.

Kliknij przycisk **powiadomienia** z hello **zarządzanie interfejsami API** menu na powitania pozostałych tooview hello dostępnych powiadomień.

![Wydawcy powiadomień][api-management-publisher-notifications]

Witaj Poniższa lista zdarzeń można skonfigurować dla powiadomienia.

* **Żądania subskrypcji (wymaganie zatwierdzenia)** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail o żądaniach subskrypcji dla produktów interfejsu API, wymaganie zatwierdzenia.
* **Nowe subskrypcje** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail o nowe subskrypcje produktu interfejsu API.
* **Żądania galerii aplikacji** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail, gdy nowe aplikacje są przesłane toohello galerii aplikacji.
* **UDW** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać wiadomości e-mail kopie z wszystkich wiadomości e-mail wysyłanych toodevelopers.
* **Nowy problem lub komentarz** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail, gdy nowy problem lub komentarz jest przesyłane na powitania portalu dla deweloperów.
* **Komunikat zamknięcia konta** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia pocztą e-mail, po zamknięciu konta.
* **Limit przydziału subskrypcji o** — Witaj następujących adresatów wiadomości e-mail, a użytkownicy otrzymają powiadomienia e-mail, gdy użycie subskrypcji pobiera przydział toousage Zamknij.

Dla każdego zdarzenia można określić adresatów wiadomości e-mail przy użyciu pole tekstowe adresu e-mail hello lub użytkownicy mogą wybrać z listy.

toospecify hello e-mail adresy toobe powiadomienie, wprowadź je w polu tekstowym adres e-mail hello. Jeśli masz wiele adresów e-mail, oddzielając je przecinkami.

![Adresatów powiadomień][api-management-email-addresses]

toobe użytkowników hello toospecify powiadomienie, kliknij przycisk **Dodaj adresata**hello pole obok toobe użytkowników hello powiadomienie wyboru i kliknij przycisk **OK**.

> [!NOTE] 
> Tylko administratorzy są wyświetlane na liście hello.


Po skonfigurowaniu hello odbiorców powiadomień, kliknij przycisk **zapisać** tooapply hello zaktualizować odbiorców powiadomień.

> [!NOTE] 
> Jeśli opuścisz hello **wydawcy powiadomień** portal wydawcy hello kartę alerty, jeśli istnieją niezapisane zmiany.


## <a name="email-templates"></a>Konfigurowanie szablonów wiadomości e-mail
Zarządzanie interfejsami API udostępnia szablony wiadomości e-mail dla hello wiadomości e-mail, które są wysyłane w toku hello zarządzania i korzystania z usługi hello. podano Hello następujące szablony wiadomości e-mail.

* Zatwierdzone przesyłanie galerii aplikacji
* Litera farewell Developer
* Limit przydziału Developer zbliża się powiadomień
* Zaproś użytkownika
* Nowy komentarz dodany tooan problem
* Nowy problem odebranych
* Nowa subskrypcja aktywowany
* Potwierdzenie odnowić subskrypcję
* Odrzuci to żądanie subskrypcji
* Odebrano żądanie subskrypcji

Te szablony mogą być modyfikowane pożądane.

tooview i skonfigurować hello szablonów wiadomości e-mail dla swojego wystąpienia usługi API Management, kliknij **powiadomienia** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie wybierz hello **szablony wiadomości E-mail**  kartę.

![Szablony wiadomości e-mail][api-management-email-templates]

tooview lub zmodyfikować szablon, wybierz ją z hello **szablony** listy rozwijanej.

![Lista szablonów wiadomości e-mail][api-management-email-templates-list]

Każdy szablon wiadomości e-mail ma podmiotu w postaci zwykłego tekstu i definicji treści w formacie HTML. Każdy element można dostosować pożądane.

![Edytor szablonu wiadomości e-mail][api-management-email-template]

Witaj **parametry** lista zawiera listę parametrów, służący do hello tematu ani treści, będzie wartość zastąpionego Witaj wyznaczone, po wysłaniu wiadomości e-mail hello. tooinsert parametr, umieść kursor hello, której chcesz hello toogo parametru, a następnie kliknij hello Strzałka toohello po lewej stronie powitania parametru nazwy.

Kliknij przycisk **Podgląd** lub **wysłać teście** toosee jak hello poczty e-mail będzie wyglądać lub Wyślij testową wiadomość e-mail.

> [!NOTE] 
> Parametry Hello nie są zastępowane rzeczywistymi wartościami podczas przeglądania lub wysyłanie testu.

toohello szablon wiadomości e-mail toosave hello zmiany, kliknij przycisk **Zapisz**, lub kliknij przycisk zmiany hello toocancel **anulować**.
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
