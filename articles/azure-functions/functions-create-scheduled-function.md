---
title: "aaaCreate funkcję, która działa zgodnie z harmonogramem na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate funkcji na platformie Azure, który jest uruchamiany zgodnie z harmonogramem przez Ciebie."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Tworzenie funkcji wyzwalanej czasomierzem na platformie Azure

Dowiedz się, jak toocreate usługi Azure Functions toouse funkcję, która działa na podstawie zdefiniowanego harmonogramu.

![Tworzenie aplikacji funkcji w hello portalu Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka:

+ Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Tworzenie aplikacji funkcji platformy Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Tworzenie funkcji wyzwalanej czasomierzem

1. Rozwiń węzeł funkcji aplikacji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**. Jeśli hello pierwszej funkcji w funkcji aplikacji, wybierz **Niestandardowa funkcja**. Spowoduje to wyświetlenie hello pełny zestaw szablonów funkcji.

    ![Funkcje strony szybkiego startu w hello portalu Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. Wybierz hello **TimerTrigger** szablon odpowiedni język. Następnie należy użyć ustawień hello określoną w tabeli hello:

    ![Utwórz funkcję czasomierza wyzwalane w hello portalu Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Ustawienie | Sugerowana wartość | Opis |
    |---|---|---|
    | **Nazwa funkcji** | TimerTriggerCSharp1 | Definiuje nazwę hello funkcji czasomierza wyzwolone. |
    | **[Harmonogram](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Pole sześć [wyrażenie CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) która planuje toorun Twojego funkcja co minutę. |

2. Kliknij przycisk **Utwórz**. Zostanie utworzona funkcja w wybranym języku uruchamiana co minutę.

3. Wyświetlanie informacji o śledzeniu zapisane dzienniki toohello Sprawdź wykonywania.

    ![Funkcje logowania podglądu hello portalu Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Teraz można zmienić harmonogramu hello funkcji wykonywania rzadziej, takich jak co godzinę. 

## <a name="update-hello-timer-schedule"></a>Harmonogram czasomierza hello aktualizacji

1. Rozwiń swoją funkcję i kliknij pozycję **Integracja**. Jest to, którym zdefiniować dane wejściowe i wyjściowe powiązań dla funkcji i również ustawić harmonogram hello. 

2. W polu **Harmonogram** wprowadź nową wartość `0 0 */1 * * *`, a następnie kliknij przycisk **Zapisz**.  

![Funkcje zaktualizować harmonogramu czasomierza w hello portalu Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

Funkcja będzie teraz uruchamiana raz na godzinę. 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Następne kroki

Utworzono funkcję uruchamianą zgodnie z harmonogramem.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Aby uzyskać więcej informacji na temat wyzwalaczy czasomierza, zobacz [Planowanie wykonywania kodu za pomocą usługi Azure Functions](functions-bindings-timer.md).