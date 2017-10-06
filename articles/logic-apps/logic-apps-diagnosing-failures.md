---
title: "błędy aaaDiagnose — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Typowe toounderstand metody, gdzie aplikacje logiki kończą się niepowodzeniem"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>Diagnozowanie błędów aplikacji logiki
Jeśli wystąpią problemy lub awarie z aplikacji logiki istnieje kilka metod pomaga lepiej zrozumieć, w którym błędów hello pochodzą z.  

## <a name="azure-portal-tools"></a>Narzędzia do portalu Azure
Hello portalu Azure udostępnia wiele narzędzi toodiagnose każdej aplikacji logiki w każdym kroku.

### <a name="trigger-history"></a>Historia wyzwalacza

Każda aplikacja logiki ma przynajmniej jeden wyzwalacz. Jeśli okaże się, że aplikacje nie są wyzwalania, przyjrzeć hello wyzwalacza historii, aby uzyskać więcej informacji. Jest dostępna Historia wyzwalacza hello na powitania logiki app'ss głównego bloku.

![Lokalizowanie hello wyzwalacza historii][1]

Historia wyzwalacza Hello Wyświetla wszystkie próby wyzwalacza wprowadzone przez aplikację logiki. Po kliknięciu każdego toodrill próba wyzwalacza hello uzyskać szczegółowe informacje, w szczególności, wszelkie danych wejściowych lub wygenerowane dane wyjściowe, które hello próba wyzwalacza. Jeśli okaże się wyzwalaczy nie powiodło się, zaznacz hello próba wyzwalacza i wybierz polecenie hello **dane wyjściowe** link tooreview wszelkie wygenerowane komunikaty o błędach, na przykład dla poświadczeń FTP, które nie są prawidłowe.

Witaj różne stany, które można napotkać są:

* **Pominięto**. punkt końcowy Hello został toocheck próbkowania dla danych i Odebrano odpowiedź, że dane nie zostały dostępne.
* **Pomyślnie**. wyzwalacz Hello odebrał odpowiedź, aby dane były dostępne. Ten stan może wynikać z ręcznego wyzwalacza, wyzwalacz cyklu lub wyzwalacza sondowania. Ten stan jest zazwyczaj towarzyszy hello **Fired** stanu, ale może nie być, jeśli masz warunku lub polecenia SplitOn w widoku kodu, który nie został spełniony.
* **Nie powiodło się**. Wystąpił błąd.

#### <a name="start-a-trigger-manually"></a>Ręcznie uruchomić wyzwalacz

Toocheck aplikacji logiki hello wyzwalacza dostępne natychmiast bez oczekiwania na następne wystąpienie hello, kliknij przycisk **wybierz wyzwalacz** na powitania głównego bloku tooforce wyboru. Na przykład kliknięcie tego łącza z wyzwalaczem skrzynki powoduje, że przepływ pracy hello tooimmediately sondowania skrzynki dla nowych plików.

### <a name="run-history"></a>Historia uruchomień

Każdy wypalane wyzwalacz powoduje do uruchomienia. Można uzyskać dostępu do informacji o uruchamianiu w głównym bloku hello, zawierający wiele szczegółowe informacje, które mogą pomóc Ci zrozumieć, co się stało podczas hello przepływu pracy.

![Lokalizowanie hello Historia uruchomień][2]

Uruchom wyświetli jeden z hello następujące stany:

* **Pomyślnie**. Wszystkie akcje zakończyło się pomyślnie. Jeśli wystąpił błąd, aby awaria była obsługiwana przez akcji, która wystąpiła w dalszej części hello przepływu pracy. Oznacza to błąd hello była obsługiwana przez akcję, która została ustawiona toorun po akcji nie powiodło się.
* **Nie powiodło się**. Co najmniej jedną akcję wystąpił błąd, który nie został obsłużony przez akcję później w przepływie pracy hello.
* **Anulowane**. Hello przepływu pracy została uruchomiona, ale otrzymano żądanie anulowania.
* **Uruchomiona**. Witaj w przepływie pracy jest uruchomiony. Ten stan może wystąpić dla przepływów pracy z ograniczeniem przepustowości lub z powodu hello bieżącego cennika planu. Aby uzyskać więcej informacji, zobacz [limity akcji na stronie dotyczącej cen hello](https://azure.microsoft.com/pricing/details/app-service/plans/). Konfigurowanie diagnostyki (hello wykresy, które są wyświetlane w obszarze Historia uruchomień hello) również może zawierają informacje dotyczące zdarzeń ograniczania zachodzące.

Jeśli przeglądasz Historia uruchomień mogą przejść więcej szczegółów.  

#### <a name="trigger-outputs"></a>Dane wyjściowe wyzwalacza

Wyzwalacz generuje hello danych pochodzi z hello wyzwalacza. Te dane wyjściowe może pomóc w określeniu, czy wszystkie właściwości zwracane zgodnie z oczekiwaniami.

> [!NOTE]
> Jeśli widzisz zawartość, która nie rozumie, Dowiedz się, jak Azure Logic Apps [obsługuje różne typy zawartości](../logic-apps/logic-apps-content-type.md).
> 

![Przykładowe dane wyjściowe wyzwalacza][3]

#### <a name="action-inputs-and-outputs"></a>Akcja wejścia i wyjścia

Aby przejść do szczegółów w hello wejściach i wyjściach, które otrzymały akcji. Dane te są przydatne dla zrozumienia hello wielkość i kształt hello wyniki, a także do znajdowania komunikaty o błędach, które mogą zostać wygenerowane.

![Akcja wejścia i wyjścia][4]

## <a name="debug-workflow-runtime"></a>Debugowanie przepływu pracy

Wraz z monitorowania hello wejść, wyjść i wyzwalaczy Uruchom, można dodać niektóre kroki tooa przepływ pracy pomocy z debugowaniem. 
[RequestBin](http://requestb.in) jest zaawansowanym narzędziem, które można dodać krokiem w przepływie pracy. Przy użyciu RequestBin, można skonfigurować protokołu HTTP żądania inspektora toodetermine hello dokładny rozmiar, kształt i format żądania HTTP. Można tworzyć RequestBin i wklej adres URL hello w aplikacji logiki akcji HTTP POST z zawartości treści, które mają tootest, na przykład, wyrażenie lub inny krok danych wyjściowych. Po uruchomieniu aplikacji logiki hello można odświeżyć Twojej toosee RequestBin jak Żądanie hello został utworzony podczas generowania z hello aplikacje logiki aparatu.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
