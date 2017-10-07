---
title: "aaaCreate funkcja, która integruje się z usługą Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzy funkcję, która integruje się z usługi Azure Logic Apps i kognitywnych usług Azure toocategorize w tweet wskaźniki nastrojów klientów i wysyłania powiadomień, gdy jest słaba wskaźniki nastrojów klientów."
services: functions, logic-apps, cognitive-services
keywords: workflow, cloud apps, cloud services, business processes, system integration, enterprise application integration, EAI
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Tworzy funkcję, która integruje się z usługą Azure Logic Apps

Azure Functions można integrować z Azure Logic Apps w hello projektanta aplikacji logiki. Integracja ta umożliwia używanie hello obliczeniowych zasilania funkcji orchestrations z innymi usługami innych firm i Azure. 

W tym samouczku przedstawiono sposób toouse działa z Azure kognitywnych usługi i aplikacje logiki tooanalyze wskaźniki nastrojów klientów z wpisów Twitter. Funkcja HTTP wyzwalane kategoryzuje tweetów jako zielone, żółte lub czerwone oparte na powitania wynik wskaźniki nastrojów klientów. Zostanie wysłana wiadomość e-mail, po wykryciu niską wskaźniki nastrojów klientów. 

![pierwsze dwa kroki obrazu aplikacji w Projektancie aplikacji logiki](media/functions-twitter-email/designer1.png)

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz konto usługi kognitywnych.
> * Utwórz funkcję, który kategoryzuje tweet wskaźniki nastrojów klientów.
> * Tworzenie aplikacji logiki łączącej tooTwitter.
> * Dodaj aplikację logiki toohello wykrywania wskaźniki nastrojów klientów. 
> * Połącz hello logiki aplikacji toohello funkcji.
> * Wyślij wiadomość e-mail, oparte na powitania odpowiedzi z funkcji hello.

## <a name="prerequisites"></a>Wymagania wstępne

+ Aktywny [Twitter](https://twitter.com/) konta. 
+ [Outlook.com](https://outlook.com/) konta (w przypadku wysyłania powiadomień).
+ W tym temacie używa jako początkowy punkt zasobów hello utworzone w [tworzenie pierwszej funkcji z portalu Azure hello](functions-create-first-azure-function.md).  
Jeśli jeszcze tego nie zrobiono, wykonaj te kroki teraz toocreate aplikacji funkcji.

## <a name="create-a-cognitive-services-account"></a>Utwórz konto usługi kognitywnych

Konto usługi kognitywnych jest wymagane toodetect hello wskaźniki nastrojów klientów tweetów monitorowane.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).

2. Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.

3. Kliknij przycisk **dane i analiza** > **kognitywnych usług**. Następnie użyj ustawień hello jako określone w tabeli hello zaakceptować hello i sprawdź **toodashboard numeru Pin**.

    ![Tworzenie bloku kognitywnych konta](media/functions-twitter-email/cog_svcs_account.png)

    | Ustawienie      |  Sugerowana wartość   | Opis                                        |
    | --- | --- | --- |
    | **Nazwa** | MyCognitiveServicesAccnt | Wybierz unikatową nazwę konta. |
    | **Typ interfejsu API** | Interfejs API analizy tekstu | Interfejs API używany tooanalyze tekstu.  |
    | **Lokalizacja** | Zachodnie stany USA | Obecnie tylko **zachodnie stany USA** jest dostępna dla Analiza tekstu. |
    | **Warstwa cenowa** | F0 | Rozpocznij od hello najniższej warstwy. Po uruchomieniu poza wywołania skalować tooa wyższego poziomu.|
    | **Grupa zasobów** | myResourceGroup | Użyj hello sama grupa zasobów dla wszystkich usług w tym samouczku.|

4. Kliknij przycisk **Utwórz** toocreate Twojego konta. Po utworzeniu konta powitania kliknij pulpitu nawigacyjnego przypiętych toohello nowego konta usługi kognitywnych. 

5. Hello konta, kliknij przycisk **klucze**, a następnie skopiuj wartość hello **klucz 1** i zapisz go. Możesz użyć tego klucza tooconnect hello logiki aplikacji tooyour konta usług kognitywnych. 
 
    ![Klucze](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>Utwórz hello — funkcja

Funkcje zawiera toooffload doskonały sposób przetwarzania zadania w przepływie pracy aplikacji logiki. W tym samouczku używana HTTP wyzwalane funkcja tooprocess tweet wskaźniki nastrojów klientów wyniki z kognitywnych usług i zwrócenie wartości kategorii.  

1. Rozwiń funkcji aplikacji, kliknij hello  **+**  obok przycisku zbyt**funkcje**, kliknij przycisk hello **HTTPTrigger** szablonu. Typ `CategorizeSentiment` dla funkcji hello **nazwa** i kliknij przycisk **Utwórz**.

    ![Funkcja blok aplikacje, funkcje +](media/functions-twitter-email/add_fun.png)

2. Zamień zawartość hello pliku run.csx hello hello następującego kodu, a następnie kliknij przycisk **zapisać**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    Ten kod funkcja zwraca oparte na wynik wskaźniki nastrojów klientów hello uzyskany w żądaniu hello kategorii koloru. 

3. Funkcja hello tootest, kliknij przycisk **testu** na powitania prawej tooexpand hello testu kartę. Wpisz wartość `0.2` dla hello **treść żądania**, a następnie kliknij przycisk **Uruchom**. Wartość **czerwony** jest zwracany w treści hello hello odpowiedzi. 

    ![Funkcja hello testu w hello portalu Azure](./media/functions-twitter-email/test.png)

Zostanie zainstalowana funkcja, który kategoryzuje wyniki wskaźniki nastrojów klientów. Następnie należy utworzyć aplikację logiki, która integruje się funkcji z konta usługi kognitywnych i Twitter. 

## <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki   

1. W portalu Azure Witaj, kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.

2. Kliknij przycisk **integracji przedsiębiorstwa** > **aplikacji logiki**. Następnie sprawdź ustawienia hello używany jako określone w tabeli hello **toodashboard numeru Pin**i kliknij przycisk **Utwórz**.
 
4. Następnie wpisz **nazwa** jak `TweetSentiment`, użyj hello ustawień określonych w tabeli hello zaakceptować hello i sprawdź **toodashboard numeru Pin**.

    ![Tworzenie aplikacji logiki w hello portalu Azure](./media/functions-twitter-email/new_logicApp.png)

    | Ustawienie      |  Sugerowana wartość   | Opis                                        |
    | ----------------- | ------------ | ------------- |
    | **Nazwa** | TweetSentiment | Wybierz odpowiednią nazwę aplikacji. |
    | **Grupa zasobów** | myResourceGroup | Interfejs API używany tooanalyze tekstu.  |
    | **Lokalizacja** | Wschodnie stany USA | Wybierz lokalizację tooyou Zamknij. |
    | **Grupa zasobów** | myResourceGroup | Wybierz jak poprzednio hello tego samego istniejącą grupę zasobów.|

4. Kliknij przycisk **Utwórz** toocreate aplikacji logiki. Po utworzeniu aplikacji hello, kliknij pozycję pulpit nawigacyjny przypiętych toohello nowej aplikacji logiki. Następnie w hello projektanta aplikacji logiki, przewiń w dół i kliknij przycisk hello **pustą aplikację logiki** szablonu. 

    ![Pusty szablon aplikacji logiki](media/functions-twitter-email/blank.png)

Możesz teraz użyć hello projektanta aplikacji logiki tooadd usługi i wyzwalacze tooyour aplikacji.

## <a name="connect-tootwitter"></a>Połącz tooTwitter

Najpierw utwórz tooyour połączenia konta w usłudze Twitter. Aplikacja logiki Hello sonduje wyszukiwane tweety, które wyzwolenia toorun aplikacji hello.

1. W Projektancie powitania kliknij hello **Twitter** usługi, a następnie kliknij przycisk hello **po jest przesyłana z nowego tweet** wyzwalacza. Zaloguj się tooyour konta w usłudze Twitter i autoryzować Logic Apps toouse Twojego konta.

2. Użyj ustawienia wyzwalacza Twitter hello określoną w tabeli hello. 

    ![Ustawienia łącznika usługi Twitter](media/functions-twitter-email/azure_tweet.png)

    | Ustawienie      |  Sugerowana wartość   | Opis                                        |
    | ----------------- | ------------ | ------------- |
    | **Wyszukiwanie tekstu** | #Azure | Użyj hasztagiem, będącą popularnych dla nowych tweetów toogenerate w polu Interwał powitania wybrany. Gdy przy użyciu warstwę bezpłatna hello i z hasztagiem jest zbyt popularne, możesz szybko zużywać hello transakcji na koncie usługi kognitywnych. |
    | **Częstotliwość** | Minuta | Jednostka częstotliwość Hello używana do sondowania Twitter.  |
    | **Interwał** | 15 | Witaj czas między żądania usługi Twitter, w jednostkach częstotliwości. |

3.  Kliknij przycisk **zapisać** tooyour tooconnect konta w usłudze Twitter. 

Aplikacja jest teraz połączony tooTwitter. Następnie połączenie tootext analytics toodetect hello wskaźniki nastrojów klientów tweetów zebrane.

## <a name="add-sentiment-detection"></a>Dodaj wykrywania wskaźniki nastrojów klientów

1. Kliknij przycisk **nowy krok**, a następnie **Dodaj akcję**.

    ![Nowy krok, a następnie dodaj akcję](media/functions-twitter-email/new_step.png)

2. W **wybierz akcję**, kliknij przycisk **Analiza tekstu**, a następnie kliknij przycisk hello **wykrywa wskaźniki nastrojów klientów** akcji.

    ![Wykrywa wskaźniki nastrojów klientów](media/functions-twitter-email/detect_sent.png)

3. Wpisz nazwę połączenia, takich jak `MyCognitiveServicesConnection`, Wklej hello klucza dla usługi kognitywnych konta zapisane i kliknij przycisk **Utwórz**.  

4. Kliknij przycisk **tooanalyze tekst** > **Tweetować tekst**, a następnie kliknij przycisk **zapisać**.  

    ![Wykrywa wskaźniki nastrojów klientów](media/functions-twitter-email/ds_tta.png)

Teraz, gdy skonfigurowano wykrywania wskaźniki nastrojów klientów, można dodać funkcji tooyour połączenia, który wykorzystuje hello wskaźniki nastrojów klientów wynik w danych wyjściowych.

## <a name="connect-sentiment-output-tooyour-function"></a>Połącz funkcja tooyour dane wyjściowe wskaźniki nastrojów klientów

1. W hello projektanta aplikacji logiki, kliknij przycisk **nowy krok** > **Dodaj akcję**, a następnie kliknij przycisk **usługi Azure Functions**. 

2. Kliknij przycisk **należy wybrać funkcję Azure**, wybierz pozycję hello **CategorizeSentiment** funkcja utworzony wcześniej.  

    ![Azure funkcja okno Wybierz funkcję platformy Azure](media/functions-twitter-email/choose_fun.png)

3. W **treść żądania**, kliknij przycisk **wynik** , a następnie **zapisać**.

    ![Wynik](media/functions-twitter-email/trigger_score.png)

Teraz funkcja jest wyzwalane, gdy wynik wskaźniki nastrojów klientów są wysyłane z hello logiki aplikacji. Oznaczone kolorami kategorii jest zwracana aplikacji logiki toohello przez funkcję hello. Następnie dodaj powiadomienie e-mail, który jest wysyłany, gdy wartość wskaźniki nastrojów klientów **czerwony** zostanie zwrócona przez funkcję hello. 

## <a name="add-email-notifications"></a>Dodawanie powiadomień e-mail

Ostatnia część przepływu pracy hello Hello jest tootrigger wiadomość e-mail, gdy hello wskaźniki nastrojów klientów są oceniane jako _czerwony_. W tym temacie używa łącznika usługi Outlook.com. Można wykonać podobne kroki toouse łącznika usługi Gmail lub Office 365 Outlook.   

1. W hello projektanta aplikacji logiki, kliknij przycisk **nowy krok** > **Dodaj warunek**. 

2. Kliknij przycisk **wybierz wartość**, następnie kliknij przycisk **treści**. Wybierz **jest równa**, kliknij przycisk **wybierz wartość** i typ `RED`i kliknij przycisk **zapisać**. 

    ![Dodaj aplikację logiki toohello warunku.](media/functions-twitter-email/condition.png)

3. W **Jeśli tak, nic nie RÓB**, kliknij przycisk **Dodaj akcję**, wyszukaj `outlook.com`, kliknij przycisk **wysłać wiadomość e-mail**i zaloguj się na tooyour konta w usłudze Outlook.com.
    
    ![Wybierz akcję hello warunku.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Jeśli nie masz konta usługi Outlook.com, można wybrać innego łącznika, takich jak usługi Gmail lub Office 365 Outlook

4. W hello **wysłać wiadomość e-mail** działania, użyj ustawienia poczty e-mail hello jako określone w tabeli hello. 

    ![Skonfiguruj hello wiadomości e-mail w przypadku wysyłania hello akcji poczty e-mail.](media/functions-twitter-email/sendemail.png)

    | Ustawienie      |  Sugerowana wartość   | Opis  |
    | ----------------- | ------------ | ------------- |
    | **Aby** | Wpisz swój adres e-mail | adres e-mail Hello, która odbiera powiadomienia hello. |
    | **Temat** | Ujemna tweet wykryto wskaźniki nastrojów klientów  | wiersz tematu Hello hello powiadomienia pocztą e-mail.  |
    | **Treści** | Tekst tweet, lokalizacji | Kliknij przycisk hello **Tweetować tekst** i **lokalizacji** parametrów. |

5.  Kliknij pozycję **Zapisz**.

Teraz, hello przepływ pracy zostanie zakończone, można włączyć aplikacji logiki hello i można znaleźć funkcji hello w miejscu pracy.

## <a name="test-hello-workflow"></a>Przepływ testowej pracy w hello

1. W hello projektanta aplikacji logiki, kliknij przycisk **Uruchom** toostart hello aplikacji.

2. W kolumnie po lewej stronie powitania kliknij **omówienie** toosee stan hello hello logiki aplikacji. 
 
    ![Stan wykonania aplikacji logiki](media/functions-twitter-email/over1.png)

3. (Opcjonalnie) Kliknij jeden z hello działa toosee szczegóły hello wykonywania.

4. Przejdź tooyour funkcji, sprawdź dzienniki hello i sprawdź, czy wskaźniki nastrojów klientów wartości były odbierane i przetwarzane.
 
    ![Wyświetl dzienniki — funkcja](media/functions-twitter-email/sent.png)

5. Po wykryciu potencjalnie ujemna wskaźniki nastrojów klientów, otrzymasz wiadomość e-mail. Jeśli nie otrzymasz wiadomość e-mail, można zmienić hello funkcja kodu tooreturn czerwony zawsze:

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    Po zweryfikowaniu powiadomienia e-mail, należy zmienić wstecz toohello oryginalny kod:

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Po ukończeniu tego samouczka, należy wyłączyć hello aplikacji logiki. Wyłączenie aplikacji hello, można uniknąć obciążona do wykonania i wykorzystuje się hello transakcji na koncie usługi kognitywnych.

Teraz już wspomniano, jak łatwo jest funkcji toointegrate w przepływie pracy Logic Apps.

## <a name="disable-hello-logic-app"></a>Wyłącz hello aplikacji logiki

toodisable hello aplikacji logiki, kliknij przycisk **omówienie** , a następnie kliknij przycisk **wyłączyć** u góry hello hello ekranu. Powoduje to zatrzymanie hello aplikacji logiki z systemem i bez usuwania aplikacji hello są naliczane opłaty. 

![Dzienniki funkcji](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz konto usługi kognitywnych.
> * Utwórz funkcję, który kategoryzuje tweet wskaźniki nastrojów klientów.
> * Tworzenie aplikacji logiki łączącej tooTwitter.
> * Dodaj aplikację logiki toohello wykrywania wskaźniki nastrojów klientów. 
> * Połącz hello logiki aplikacji toohello funkcji.
> * Wyślij wiadomość e-mail, oparte na powitania odpowiedzi z funkcji hello.

Jak przejść dalej toolearn samouczka toohello toocreate niekorzystającą interfejsu API dla funkcji.

> [!div class="nextstepaction"] 
> [Tworzenie bezserwerowego interfejsu API za pomocą usługi Azure Functions](functions-create-serverless-api.md)

toolearn więcej informacji na temat aplikacji logiki, zobacz [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).

