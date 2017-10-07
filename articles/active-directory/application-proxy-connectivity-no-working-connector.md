---
title: "Znaleziono aaaNo pracy łącznika grupy dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Rozwiąż problemy, które mogą wystąpić po nie pracy łącznika w grupie łącznika dla aplikacji z powitania serwera Proxy aplikacji usługi Azure AD"
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
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>Nie znaleziono aplikacji serwera Proxy aplikacji grupy łącznika pracy

Ten artykuł pomocy możesz tooresolve hello typowych problemów, które muszą ponieść gdy nie jest łącznika dla aplikacji serwera Proxy aplikacji wykryte zintegrowane z usługą Azure Active Directory.

## <a name="overview-of-steps"></a>Omówienie kroków
Jeśli nie ma żadnych pracy łącznika w grupie łącznika dla aplikacji, istnieje kilka sposobów tooresolve hello problemu:

-   Jeśli w grupie hello nie łączników, można:

    -   Pobierz nowy łącznik na powitania serwera lokalnego prawo i przypisz go toothis grupy

    -   Przenieś do grupy hello łącznika usługi active

-   Jeśli nie łączniki active w grupie hello, można:

    -   Zidentyfikowanie przyczyny hello Twojego łącznika jest nieaktywny i rozwiązanie

    -   Przenieś do grupy hello łącznika usługi active

tooknow, który z nich jest hello problem, otwórz menu "Serwer Proxy aplikacji" hello w aplikacji i przyjrzyj komunikat ostrzegawczy hello grupy łącznika. Określ ją tej grupy hello wymaga co najmniej jeden łącznik (użytkownik nie masz żadnej grupy hello) lub że nie ma żadnych aktywnych łączników (Jeśli masz prawdopodobnie nieaktywne łączniki).

   ![Wybór grupy łącznika w portalu Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

Aby uzyskać szczegółowe informacje na każdej z tych opcji zobacz hello odpowiedniej sekcji poniżej. Każdy z tych przyjęto założenie, uruchamiasz ze strony Zarządzanie hello łącznika. Jeśli przeglądasz hello komunikat o błędzie powyżej, można przejść przez kliknięcie komunikatu ostrzegawczego hello toothis strony. W przeciwnym razie ten znajduje się zbyt przechodząc**usługi Azure Active Directory**, klikając pozycję na **aplikacje dla przedsiębiorstw**, następnie **serwera Proxy aplikacji.**

   ![Łącznik grupy zarządzania w portalu Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>Pobierz nowy łącznik

toodownload nowy łącznik, użyj przycisku "Pobierz łącznik" hello u góry hello hello strony.

Uwaga hello łącznika potrzeb toobe zainstalowany na komputerze z aplikacją zaplecza toohello bezpośredniego procesów z wiersza i zwykle znajduje się na hello tym samym serwerze co aplikacja hello. Po pobraniu hello łącznika powinna pojawić się w tym menu. Kliknij hello łącznika, a następnie użyj toomake listy rozwijanej "Łącznik grupy" hello się, że należy toohello prawo grupy. Zapisz zmiany hello.

   ![Pobierz łącznik hello z hello portalu Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>Przenieś łącznika usługi Active

Jeśli masz łącznika usługi active muszą należeć do grupy toohello i ma aplikacji zaplecza docelowej toohello procesów z wiersza hello łącznika można przenieść do grupy hello przypisane. toodo tak, kliknij przycisk hello łącznika. W polu "Łącznik grupy" hello Użyj hello tooselect listy rozwijanej hello prawidłowej grupy, a następnie kliknij przycisk Zapisz.

## <a name="resolve-an-inactive-connector"></a>Rozwiąż nieaktywne łącznika

Czy hello tylko łączników w grupie hello są nieaktywne, mogą mieć na komputerze, na którym nie ma odblokowany wszystkie porty niezbędne hello.

Zobacz porty hello dokumentu rozwiązywanie szczegółowe informacje dotyczące badania ten problem.

## <a name="next-steps"></a>Następne kroki
[Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)


