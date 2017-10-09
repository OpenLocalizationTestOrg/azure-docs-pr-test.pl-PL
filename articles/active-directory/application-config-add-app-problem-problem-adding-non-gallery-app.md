---
title: "Dodawanie aplikacji z systemem innym niż galerii aaaProblem | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello typowych problemów osób krój podczas dodawania niestandardowych aplikacji z systemem innym niż galerii"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: cfe9b657ae18cbacaddbd85658471a2c57c9cf95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-a-non-gallery-application"></a>Problem podczas dodawania aplikacji z systemem innym niż galerii

W tym artykule pomóc toounderstand hello typowych problemów osób krój podczas dodawania **niestandardowych aplikacji z systemem innym niż galerii** i co można zrobić tooresolve je. 

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a>Po kliknięciu hello "Dodaj", że przycisk i Moja aplikacja tooappear długo trwało

W pewnych okolicznościach, może upłynąć 1 – 2 minuty (i czasami dłużej) dla aplikacji tooappear po dodaniu tooyour katalogu. Chociaż nie jest to normalne obniżenie wydajności hello widać, dodanie aplikacji hello jest w toku, klikając hello **powiadomienia** ikonę (hello dzwonka) w hello górnym rogu hello [Azure Portal](https://portal.azure.com/)i wyszukując **w toku** lub **Ukończono** powiadomień z etykietą **tworzenie aplikacji**.

Jeśli aplikacja nigdy nie zostanie dodany lub w przypadku wystąpienia błędu podczas klikania hello **Dodaj** przycisku, zobaczysz **powiadomień** w **błąd** stanu. Jeśli chcesz, aby więcej szczegółów na temat toolearn błąd hello więcej tooor udostępniać engingeer pomocy technicznej, wykonując kroki hello w hello widać więcej informacji o błędzie hello [jak toosee szczegóły hello powiadomieniu portalu](#how-to-see-the-details-of-a-portal-notification) sekcji.

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a>Po kliknięciu przycisku "Dodaj" hello, a nie pojawił się Moja aplikacja

Czasami powodu tootransient problemy, problemy z siecią lub usterki, dodawanie błędów aplikacji. Można ustalić dzieje się tak po kliknięciu hello **powiadomienia** ikonę (hello dzwonka) w prawym górnym rogu hello hello portalu Azure, a wyświetlony czerwony (!) ikona dalej tooyour **tworzenie aplikacji** powiadomień. Oznacza to, że wystąpił błąd podczas tworzenia aplikacji hello.

Jeśli wystąpi błąd podczas klikania hello **Dodaj** przycisku, zobaczysz **powiadomień** w **błąd** stanu. Jeśli chcesz, aby więcej szczegółów na temat toolearn błąd hello więcej tooor udostępniać engingeer pomocy technicznej, wykonując kroki hello w hello widać więcej informacji o błędzie hello [jak toosee szczegóły hello powiadomieniu portalu](#how-to-see-the-details-of-a-portal-notification) sekcji.

## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a>Nie wiadomo jak tooset zapasową mojej aplikacji raz zostały dodane go

Jeśli potrzebujesz pomocy, informacje o niestandardowych aplikacji hello [biblioteki dokumentów aplikacji w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) ułatwiają toolearn więcej informacji na temat rejestracji jednokrotnej z usługą Azure AD i jej działania.

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Jak toosee szczegóły hello powiadomieniu portalu

Szczegóły hello powiadomienia portalu można wyświetlić, wykonując poniższe kroki hello:

1.  Kliknij przycisk hello **powiadomienia** ikonę (hello dzwonka) w prawym górnym rogu portalu Azure hello hello

2.  Wybierz wszystkich powiadomień w **błąd** stanu (te z toothem dalej czerwony (!)).

   >[!NOTE]
   >Nie można kliknąć powiadomienia w **Powodzenie** lub **w toku** stanu.
   >
   >

3.  Ta Otwórz hello **szczegóły powiadomienia** bloku.

4.  Dzięki tym informacjom samodzielnie toounderstand więcej szczegółowych informacji o hello problem.

5.  Jeśli nadal potrzebujesz pomocy, można również udostępniać te informacje pomocy technicznej odtwarzania lub hello grupy tooget Pomoc produktu o problemie.

6.  Kliknij hello **ikonę kopiowania** toohello rogu hello **błąd kopiowania** toocopy pole tekstowe wszystkich hello tooshare szczegóły powiadomienia o z pracownikiem pomocy technicznej lub produkt grupy.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Jak tooget pomóc, wysyłając powiadomienia szczegóły tooa specjaliście pomocy technicznej

Jest bardzo ważne, aby udostępniać **hello wszystkie dane przedstawione poniżej** z pracownikiem pomocy technicznej, jeśli potrzebujesz pomocy, dzięki czemu mogą one ułatwić szybkie. Możesz to zrobić w prosty sposób przez **zrobieniem zrzutu ekranu,** lub przez kliknięcie przycisku hello **ikony błędu kopiowania**, znaleziono prawej toohello hello **błąd kopiowania** pola tekstowego.

## <a name="notification-details-explained"></a>Szczegóły powiadomienia wyjaśniono

Hello poniżej opisano bardziej jakie poszczególnych elementów powiadomień hello oznacza oraz przykłady zapewnia każdego z nich.

### <a name="essential-notification-items"></a>Elementy podstawowych powiadomień

-   **Tytuł** — Witaj opisowy tytuł hello powiadomień
   *  Przykład — **ustawienia serwera proxy aplikacji**

-   **Opis elementu** — Witaj opis co nastąpiło w wyniku operacji hello

   *  Przykład — **wewnętrzny wprowadzony adres url jest już używana przez inną aplikację**

-   **Identyfikator powiadomień** — Unikatowy identyfikator hello hello powiadomienia

   *  Przykład — **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Identyfikator żądania klienta** — identyfikator określonego żądania hello wprowadzone przez przeglądarkę

   *  Przykład — **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Czas UTC sygnatury** — Witaj znaczników czasu, w którym wystąpił hello powiadomień, w formacie UTC

   *  Przykład — **2017-03-23T19:50:43.7583681Z**

-   **Wewnętrzny identyfikator transakcji** — Witaj wewnętrzny identyfikator możemy użyć błąd hello toolook w naszych systemów

   *  Przykład — **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **Nazwa UPN** — Witaj użytkownika, który wykonał operację hello

   *  Przykład —**tperkins@f128.info**

-   **Identyfikator dzierżawy** — Unikatowy identyfikator dzierżawy hello, która hello użytkownika wykonującego operację hello hello był członkiem

   *  Przykład — **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Identyfikator obiektu użytkownika** — Witaj Unikatowy identyfikator hello użytkownika, który wykonał operację hello

 *  Przykład — **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Elementy szczegółowe powiadomienia

-   **Nazwa wyświetlana** — **(może być pusta)** nazwę wyświetlaną bardziej szczegółowy błąd hello

  *  Przykład — **ustawienia serwera proxy aplikacji**

-   **Stan** — Witaj określonego stanu hello powiadomień

   *  Przykład — **nie powiodło się**

-   **Obiekt o identyfikatorze** — **(może być pusta)** hello Identyfikatora obiektu, względem których hello wykonano operację

   *  Przykład — **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Szczegóły** — Witaj szczegółowy opis co nastąpiło w wyniku operacji hello

   *  Przykład — **wewnętrznego adresu url "http://bing.com/" jest nieprawidłowy, ponieważ jest już używana**

-   **Błąd kopiowania** — kliknij hello **ikonę kopiowania** toohello rogu hello **błąd kopiowania** toocopy pole tekstowe wszystkich hello tooshare szczegóły powiadomienia o inżyniera grupa pomocy technicznej lub produktu

   *  Przykład```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)



