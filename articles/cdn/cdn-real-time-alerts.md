---
title: alerty w czasie rzeczywistym CDN aaaAzure | Dokumentacja firmy Microsoft
description: "Alertów w czasie rzeczywistym w usłudze Microsoft Azure CDN. Alerty w czasie rzeczywistym udostępniają powiadomienia dotyczące wydajności hello punktów końcowych hello w Twoim profilu CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 1e85b809-e1a9-4473-b835-69d1b4ed3393
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269c90437088bbc41bf899a8c02749e8e6f3006c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-alerts-in-microsoft-azure-cdn"></a>Alerty w czasie rzeczywistym w usłudze Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Omówienie
W tym dokumencie opisano alertów w czasie rzeczywistym w usłudze Microsoft Azure CDN. Ta funkcja udostępnia w czasie rzeczywistym powiadomienia dotyczące wydajności hello punktów końcowych hello w Twoim profilu CDN.  Można skonfigurować adres e-mail lub alerty HTTP na podstawie:

* Przepustowość
* Kody stanu
* Stany pamięci podręcznej
* Połączenia

## <a name="creating-a-real-time-alert"></a>Tworzenie w czasie rzeczywistym alertu
1. W hello [Azure Portal](https://portal.azure.com), Przeglądaj tooyour profilu CDN.
   
    ![Blok profilu CDN](./media/cdn-real-time-alerts/cdn-profile-blade.png)
2. Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-real-time-alerts/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
3. Przesuń kursor myszy hello **Analytics** kartę, a następnie przesuń kursor myszy hello **statystyki w czasie rzeczywistym** wysuwane okno.  Polecenie **alertów w czasie rzeczywistym**.
   
    ![Portal zarządzania usługi CDN](./media/cdn-real-time-alerts/cdn-premium-portal.png)
   
    zostanie wyświetlona lista Hello istniejącej konfiguracji alertu (jeśli istnieje).
4. Kliknij przycisk hello **dodać alertu** przycisku.
   
    ![Dodawanie przycisku alertu](./media/cdn-real-time-alerts/cdn-add-alert.png)
   
    Zostanie wyświetlony formularz służący do tworzenia nowego alertu.
   
    ![Nowy formularz alertu](./media/cdn-real-time-alerts/cdn-new-alert.png)
5. Jeśli chcesz ten alert toobe active po kliknięciu **zapisać**, sprawdź hello **włączone Alert** wyboru.
6. Wprowadź opisową nazwę alertu w hello **nazwa** pola.
7. W hello **typ nośnika** listy rozwijanej wybierz **HTTP dużego obiektu**.
   
    ![Typ nośnika z wybranego obiektu dużych HTTP](./media/cdn-real-time-alerts/cdn-http-large.png)
   
   > [!IMPORTANT]
   > Musisz wybrać **HTTP dużego obiektu** jako hello **typ nośnika**.  Witaj inne opcje nie są używane przez **Azure CDN from Verizon**.  Błąd tooselect **HTTP dużego obiektu** spowoduje, że alert wyzwalane toonever.
   > 
   > 
8. Utwórz **wyrażenie** toomonitor wybierając **Metryka**, **Operator**, i **wyzwolenia wartość**.
   
   * Aby uzyskać **Metryka**, wybierz typ hello warunku, które mają być monitorowane.  **MB/s przepustowości** jest hello wielkość przepustowości w megabitach na sekundę.  **Całkowita liczba połączeń** jest hello liczba równoczesnych tooour połączenia HTTP serwery krawędzi.  Definicje hello różne stany pamięci podręcznej i kodów stanu, zobacz [kodów stanu systemu Azure CDN pamięci podręcznej](https://msdn.microsoft.com/library/mt759237.aspx) i [kody stanu HTTP Azure w sieci CDN](https://msdn.microsoft.com/library/mt759238.aspx)
   * **Operator** jest hello operatorów matematycznych ustanawia hello relację Metryka hello hello wyzwalacza wartość.
   * **Wyzwalanie wartość** jest wartość progu hello, które muszą zostać spełnione, zanim zostanie wysłane powiadomienie.
     
     W hello w poniższym przykładzie hello wyrażenie, które utworzono wskazuje, że chcę toobe powiadomienie, gdy liczba hello 404 kodów stanu jest większa niż 25.
     
     ![W czasie rzeczywistym alertu przykładowe wyrażenie](./media/cdn-real-time-alerts/cdn-expression.png)
9. Aby uzyskać **interwał**, wprowadź, jak często chcesz hello wyrażenia obliczonego.
10. W hello **powiadomienia na** listy rozwijanej wybierz opcję, jeśli chcesz toobe powiadomienie, gdy hello wyrażenie jest prawdziwe.
    
    * **Warunkiem rozpoczęcia** wskazuje, że powiadomienie zostanie wysłane po hello określony warunek jest pierwszy wykryty.
    * **Warunek zakończenia** wskazuje, że powiadomienie zostanie wysłane po hello określony warunek nie zostanie wykryta. To powiadomienie może być uruchomiona tylko po naszej sieci monitorowania system wykrył hello, że określony warunek.
    * **Ciągłe** wskazuje, że powiadomienie zostanie wysłane za każdym razem hello system monitorowania sieci wykrywa hello określony warunek. Należy pamiętać sieci hello monitorowania system będzie tylko wyboru raz na interwał hello określony warunek.
    * **Stan początkowy i końcowy** oznacza, że powiadomienie zostanie wysłane hello wykryte po raz pierwszy hello określony warunek i jeszcze raz, jeżeli nie zostały wykryte hello warunku.
11. Jeśli chcesz tooreceive powiadomienia pocztą e-mail, sprawdź hello **powiadamiania pocztą E-mail** wyboru.  
    
    ![Powiadomienia E-mail formularza](./media/cdn-real-time-alerts/cdn-notify-email.png)
    
    W hello **do** wprowadź adres e-mail hello miejscu powiadomienia wysłane. Dla **podmiotu** i **treści**, można pozostawić domyślne hello, lub można dostosować za pomocą hello wiadomość hello **dostępne słowa kluczowe** toodynamically lista wstawiania danych alertu po zostanie wysłana wiadomość Hello.
    
    > [!NOTE]
    > Powiadomienie e-mail hello można sprawdzić, klikając hello **testowe powiadomienie E-mail** przycisku, jednak tylko po zapisaniu hello konfiguracji alertu.
    > 
    > 
12. Toobe powiadomienia zaksięgowany tooa serwera sieci web, sprawdzić hello **powiadamiania przez HTTP Post** wyboru.
    
    ![Powiadom HTTP Post formularza](./media/cdn-real-time-alerts/cdn-notify-http.png)
    
    W hello **adres Url** wprowadź adres URL hello miejscu wiadomość hello HTTP zaksięgowania. W hello **nagłówki** pole tekstowe, wprowadź wysłanych w żądaniu hello toobe nagłówki hello HTTP.  Dla **treści** można dostosować za pomocą hello wiadomość hello **dostępne słowa kluczowe** toodynamically listy wstawiania danych alertu, gdy zostanie wysłana wiadomość hello.  **Nagłówki** i **treści** domyślne podobne toohello ładunek XML tooan poniższym przykładzie.
    
    ```
    <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
        <![CDATA[Expression=Status Code : 404 per second > 25&Metric=Status Code : 404 per second&CurrentValue=[CurrentValue]&NotificationCondition=Condition Start]]>
    </string>
    ```
    
    > [!NOTE]
    > Można sprawdzić hello powiadomień HTTP Post, klikając hello **testowe powiadomienie E-mail** przycisku, jednak tylko po zapisaniu hello konfiguracji alertu.
    > 
    > 
13. Kliknij przycisk hello **zapisać** przycisk toosave konfiguracji alertu.  Jeśli zaznaczono **włączone Alert** w kroku 5 alertu jest aktywna.

## <a name="next-steps"></a>Następne kroki
* Analizowanie [statystyki w czasie rzeczywistym w usłudze Azure CDN](cdn-real-time-stats.md)
* Dig głębiej z [zaawansowane raporty HTTP](cdn-advanced-http-reports.md)
* Analizowanie [wzorców użycia](cdn-analyze-usage-patterns.md)

