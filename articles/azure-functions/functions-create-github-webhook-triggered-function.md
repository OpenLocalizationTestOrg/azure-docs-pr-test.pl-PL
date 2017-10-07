---
title: Funkcja w systemie Azure wyzwalane przez GitHub webhook aaaCreate | Dokumentacja firmy Microsoft
description: "Za pomocą usługi Azure Functions toocreate niekorzystającą funkcji, który jest wywoływany przez element webhook GitHub."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>Tworzenie funkcji wyzwalanej przez element webhook GitHub

Dowiedz się, jak toocreate funkcję, która jest wyzwalana przez żądanie HTTP elementu webhook z ładunku specyficzne dla usługi GitHub.

![Funkcja w portalu Azure hello wyzwolone element Github Webhook](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Wymagania wstępne

+ Konto w usłudze GitHub z przynajmniej jednym projektem.
+ Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Tworzenie aplikacji funkcji platformy Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>Tworzenie funkcji wyzwalanej przez element webhook GitHub

1. Rozwiń węzeł funkcji aplikacji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**. Jeśli hello pierwszej funkcji w funkcji aplikacji, wybierz **Niestandardowa funkcja**. Spowoduje to wyświetlenie hello pełny zestaw szablonów funkcji.

    ![Funkcje strony szybkiego startu w hello portalu Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Wybierz hello **GitHub WebHook** szablon odpowiedni język. **Nadaj nazwę funkcji**, a następnie wybierz pozycję **Utwórz**.

     ![Utwórz funkcję wyzwolone element webhook GitHub w hello portalu Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. W nowych funkcji, kliknij przycisk **adres URL funkcji <> / Get**, następnie skopiuj i Zapisz hello wartości. Witaj samo dla **<> / GitHub pobrać klucza tajnego**. Użyjesz tych wartości tooconfigure hello elementu webhook w witrynie GitHub.

    ![Przegląd kodu funkcji hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

W następnym kroku zostanie utworzony element webhook w repozytorium GitHub.

## <a name="configure-hello-webhook"></a>Skonfiguruj hello elementu webhook

1. W witrynie GitHub Przejdź repozytorium tooa, którego jesteś właścicielem. Możesz też użyć dowolnego rozwidlonego repozytorium. Jeśli potrzebujesz toofork repozytorium, użyj <https://github.com/Azure-Samples/functions-quickstart>.

1. Kliknij kolejno pozycje **Ustawienia**, **Elementy webhook** i **Dodaj element webhook**.

    ![Dodawanie elementu webhook GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Użyj ustawień określonych w tabeli hello, a następnie kliknij przycisk **Dodawanie elementu webhook**.

    ![Adres URL elementu webhook hello zestawu i klucz tajny](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Ustawienie | Sugerowana wartość | Opis |
|---|---|---|
| **Adres URL ładunku** | Skopiowana wartość | Użyj hello wartość zwrócona przez **adres URL funkcji <> / Get**. |
| **Wpis tajny**   | Skopiowana wartość | Użyj hello wartość zwrócona przez **<> / GitHub pobrać klucza tajnego**. |
| **Typ zawartości** | application/json | Funkcja Hello oczekuje ładunek JSON. |
| Wyzwalacze zdarzeń | Pozwól mi wybrać pojedyncze zdarzenia | Chcemy tylko tootrigger problem komentarz zdarzeń.  |
| | Komentarz dotyczący problemu |  |

Teraz, hello elementu webhook jest skonfigurowany tootrigger funkcji w przypadku dodania nowego komentarza problem.

## <a name="test-hello-function"></a>Funkcja hello testu

1. W repozytorium GitHub Otwórz hello **problemów** kartę w nowym oknie przeglądarki.

1. W nowym oknie powitania kliknij **nowy problem**wpisz tytuł, a następnie kliknij przycisk **przesłać nowy problem**.

1. W hello problem, wprowadź komentarz, a następnie kliknij przycisk **komentarz**.

    ![Dodawanie komentarza dotyczącego problemu w usłudze GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Toohello portal wrócić do poprzedniej strony i sprawdź dzienniki hello. Wpis śledzenia na nowy tekst komentarza hello powinna zostać wyświetlona.

     ![Wyświetl tekst komentarza hello w dziennikach hello.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Następne kroki

Utworzono funkcję, która jest uruchamiana w momencie otrzymania żądania od elementu webhook GitHub.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Aby uzyskać więcej informacji na temat wyzwalaczy elementów webhook, zobacz temat [Powiązania protokołu HTTP i elementów webhook w usłudze Azure Functions](functions-bindings-http-webhook.md).
