---
title: "Problem podczas dodawania aplikacji z systemem innym niż galerii | Dokumentacja firmy Microsoft"
description: "Zrozumienie kroju osób typowe problemy podczas dodawania niestandardowych aplikacji z systemem innym niż galerii"
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
ms.openlocfilehash: bb3fc7877f4e7cafc3904fc67abd87b897874d8a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-a-non-gallery-application"></a>Problem podczas dodawania aplikacji z systemem innym niż galerii

Ten artykuł ułatwia zrozumienie kroju osób typowe problemy przy dodawaniu **niestandardowych aplikacji z systemem innym niż galerii** i sposoby ich rozwiązywania. 

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a>Po kliknięciu przycisku "Dodaj" i Moja aplikacja przez długi czas i pojawienie się

W pewnych okolicznościach, może upłynąć 1 – 2 minuty (i czasami dłużej) do pojawiają się po dodaniu go do katalogu aplikacji. Chociaż nie jest to normalne obniżenie wydajności widać dodawania aplikacji jest w toku, klikając **powiadomienia** ikonę (dzwonka) w prawym górnym rogu [Azure Portal](https://portal.azure.com/) i wyszukując **w toku** lub **Ukończono** powiadomień z etykietą **tworzenie aplikacji**.

Aplikacja nigdy nie zostanie dodany, czy w przypadku wystąpienia błędu podczas klikania **Dodaj** przycisku, zobaczysz **powiadomień** w **błąd** stanu. Jeśli chcesz szczegółowe informacje o błędzie, aby dowiedzieć się więcej na temat lub udostępniać engingeer pomocy technicznej, wykonując kroki opisane w widać więcej informacji o błędzie [sposób wyświetlić szczegóły powiadomieniu portalu](#how-to-see-the-details-of-a-portal-notification) sekcji.

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a>Po kliknięciu przycisku "Dodaj" i nie pojawił się Moja aplikacja

Czasami z powodu przejściowych problemów, problemy z siecią lub usterki, dodawanie błędów aplikacji. Można ustalić dzieje się tak po kliknięciu **powiadomienia** ikonę (dzwonka) w prawym górnym rogu portalu Azure, a ikona jest widoczna czerwony (!) obok pozycji z **tworzenie aplikacji** powiadomień. Oznacza to, że wystąpił błąd podczas tworzenia aplikacji.

Jeśli wystąpi błąd, po kliknięciu przycisku **Dodaj** przycisku, zobaczysz **powiadomień** w **błąd** stanu. Jeśli chcesz szczegółowe informacje o błędzie, aby dowiedzieć się więcej na temat lub udostępniać engingeer pomocy technicznej, wykonując kroki opisane w widać więcej informacji o błędzie [sposób wyświetlić szczegóły powiadomieniu portalu](#how-to-see-the-details-of-a-portal-notification) sekcji.

## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a>I nie wiadomo, jak skonfigurować aplikację, gdy został dodany

Jeśli potrzebujesz pomocy, informacje o niestandardowych aplikacji [biblioteki dokumentów aplikacji w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) pomoc, aby dowiedzieć się więcej o rejestracji jednokrotnej z usługą Azure AD i jak działa.

## <a name="how-to-see-the-details-of-a-portal-notification"></a>Jak wyświetlić szczegóły powiadomieniu portalu

Szczegółowe informacje o każdym powiadomieniu portalu można wyświetlić, wykonując poniższe kroki:

1.  Kliknij przycisk **powiadomienia** ikonę (dzwonka) w prawym górnym rogu portalu Azure

2.  Wybierz wszystkich powiadomień w **błąd** stanu (te z czerwonym znakiem (!) obok nich).

   >[!NOTE]
   >Nie można kliknąć powiadomienia w **Powodzenie** lub **w toku** stanu.
   >
   >

3.  Otwórz ten **szczegóły powiadomienia** bloku.

4.  Dzięki tym informacjom samodzielnie, aby poznać więcej szczegółów o problemie.

5.  Jeśli nadal potrzebujesz pomocy, te informacje mogą również współużytkować z pracownikiem pomocy technicznej lub grupa produktów, aby uzyskać pomoc dotyczącą tego problemu.

6.  Kliknij przycisk **ikonę kopiowania** z prawej strony **błąd kopiowania** skopiuj wszystkie szczegóły powiadomienia na udostępnianie z pracownikiem pomocy technicznej lub produkt grupy w polu tekstowym.

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a>Jak uzyskać pomoc, wysyłając szczegóły powiadomienia do pracownika pomocy technicznej

Jest bardzo ważne, aby udostępniać **poniższymi szczegółami** z pracownikiem pomocy technicznej, jeśli potrzebujesz pomocy, dzięki czemu mogą one ułatwić szybkie. Możesz to zrobić w prosty sposób przez **zrobieniem zrzutu ekranu,** lub przez kliknięcie przycisku **ikony błędu kopiowania**, liczba znalezionych na prawo od **błąd kopiowania** pola tekstowego.

## <a name="notification-details-explained"></a>Szczegóły powiadomienia wyjaśniono

Poniżej przedstawiono więcej funkcji każdego, powiadomienia elementów oznacza i zawiera przykłady każdego z nich.

### <a name="essential-notification-items"></a>Elementy podstawowych powiadomień

-   **Tytuł** — opisowy tytuł powiadomienia
   *  Przykład — **ustawienia serwera proxy aplikacji**

-   **Opis elementu** — opis co nastąpiło w wyniku operacji

   *  Przykład — **wewnętrzny wprowadzony adres url jest już używana przez inną aplikację**

-   **Identyfikator powiadomień** — Unikatowy identyfikator powiadomienia.

   *  Przykład — **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Identyfikator żądania klienta** — identyfikator określonego żądania przez przeglądarkę

   *  Przykład — **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Czas UTC sygnatury** — znacznik czasu, w którym wystąpił powiadomienia, w formacie UTC

   *  Przykład — **2017-03-23T19:50:43.7583681Z**

-   **Wewnętrzny identyfikator transakcji** — wewnętrzny identyfikator możemy użyć do wyszukiwania błąd w naszym systemie

   *  Przykład — **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **Nazwa UPN** — użytkownik, który wykonał działanie

   *  Przykład —**tperkins@f128.info**

-   **Identyfikator dzierżawy** — Unikatowy identyfikator dzierżawy, który użytkownik, który wykonał działanie był członkiem

   *  Przykład — **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Identyfikator obiektu użytkownika** — Unikatowy identyfikator użytkownika, który wykonał działanie

 *  Przykład — **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Elementy szczegółowe powiadomienia

-   **Nazwa wyświetlana** — **(może być pusta)** nazwę wyświetlaną bardziej szczegółowy kod błędu

  *  Przykład — **ustawienia serwera proxy aplikacji**

-   **Stan** — stan określonego powiadomienia

   *  Przykład — **nie powiodło się**

-   **Obiekt o identyfikatorze** — **(może być pusta)** Identyfikatora obiektu, względem którego wykonano operację

   *  Przykład — **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Szczegóły** — szczegółowy opis co nastąpiło w wyniku operacji

   *  Przykład — **wewnętrznego adresu url "http://bing.com/" jest nieprawidłowy, ponieważ jest już używana**

-   **Błąd kopiowania** — kliknij przycisk **ikonę kopiowania** z prawej strony **błąd kopiowania** pole tekstowe, aby skopiować wszystkie szczegóły powiadomienia na udostępnianie z pracownikiem pomocy technicznej lub produkt grupy

   *  Przykład```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)



