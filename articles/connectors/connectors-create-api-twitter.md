---
title: "aaaLearn jak toouse hello łącznik Twitter w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie łącznik Twitter z parametrami interfejsu API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Rozpoczynanie pracy z powitania łącznik Twitter
Łącznik Twitter hello można:

* Publikowanie tweetów i tweetów get
* Dostęp do osi czasu, znajomych i adherentami
* Wykonaj jedną z hello w innych działań i wyzwalaczy opisanych poniżej  

toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki. Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).  

## <a name="connect-tootwitter"></a>Połącz tooTwitter
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi. A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi.  

### <a name="create-a-connection-tootwitter"></a>Tworzenie tooTwitter połączenia
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Użyj wyzwalacz Twitter
Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

W tym przykładzie I przedstawia sposób toouse hello **po jest przesyłana z nowego tweet** wyzwolić toosearch dla #Seattle i, w przypadku znalezienia #Seattle zaktualizowany plik w Dropbox z tekstem hello hello tweet. W przykładzie przedsiębiorstwa można wyszukać hello nazwę swojej firmy i zaktualizować bazę danych SQL z tekstem hello hello tweet.

1. Wprowadź *twitter* w polu wyszukiwania hello hello logiki aplikacji designer wybierz hello **Twitter — gdy nowy tweet jest przesyłana** wyzwalacza   
   ![Obraz wyzwalacza Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)  
2. Wprowadź *#Seattle* w hello **tekst do wyszukania** formantu  
   ![Wyzwalacz Twitter — obraz 2](./media/connectors-create-api-twitter/trigger-2.png) 

W tym momencie aplikację logiki została skonfigurowana z wyzwalaczy, które rozpocznie Uruchom hello innych wyzwalacze i akcje w przepływie pracy hello. 

> [!NOTE]
> Dla logiki aplikacji toobe funkcjonalności musi ona zawierać przynajmniej jeden wyzwalacz i jedną akcję. Wykonaj kroki hello hello następnej sekcji tooadd akcji.  
> 
> 

## <a name="add-a-condition"></a>Dodaj warunek
Ponieważ tylko Dbamy o tweetów od użytkowników więcej niż 50 użytkowników, warunek, który potwierdza hello liczba adherentami najpierw należy dodać toohello aplikacji logiki.  

1. Wybierz **+ nowy krok** akcji hello tooadd chcesz tootake po znalezieniu #Seattle w nowej tweet  
   ![Obraz akcji Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. Wybierz hello **Dodaj warunek** łącza.  
   ![Obraz warunku Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   Spowoduje to otwarcie hello **warunku** kontrolki, w którym można sprawdzić warunków takich jak *jest równa*, *jest mniejsza niż*, *jest większa niż*, *zawiera*itp.  
   ![Warunek Twitter — obraz 2](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. Wybierz hello **wybierz wartość** formantu.  
   W tym formancie można wybrać jedną lub więcej właściwości hello z poprzedniej akcji lub wyzwalaczy jako wartość hello którego warunku będzie oceniana tootrue lub false.
   ![Obraz warunku Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. Wybierz hello **...**  tooexpand hello listę właściwości, dzięki czemu wszystkie właściwości hello, które są dostępne.        
   ![Stan obrazu 4 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. Wybierz hello **liczba adherentami** właściwości.    
   ![Obraz warunku Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. Zwróć uwagę, adherentami hello właściwość count jest teraz hello wartość formantu.    
   ![Stan obrazu 6 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. Wybierz **jest większa niż** z listy operatory hello.    
   ![Stan obrazu 7 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Wprowadź 50 jako argument hello hello *jest większa niż* operatora.  
   dodawany jest Hello warunku. Zapisz swoją pracę przy użyciu hello **zapisać** łącze menu hello powyżej.    
   ![Stan obrazu 8 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Za pomocą akcji usługi Twitter
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Teraz, wyzwalacz został dodany, wykonaj te kroki tooadd akcję, która zostanie wysłany nowy tweet zawartością hello tweetów hello znalezione przez wyzwalacz hello. Na potrzeby tego przewodnika hello tylko tweetów od użytkowników więcej niż 50 adherentami zostaną opublikowane.  

W następnym kroku hello doda akcji Twitter, który zostanie wysłany tweet niektórych właściwości hello każdego tweet, która została opublikowana przez użytkownika, który ma więcej niż 50 adherentami.  

1. Wybierz **Dodaj akcję**. Spowoduje to otwarcie hello formantu wyszukiwania, których można wyszukiwać innych działań i wyzwalaczy.  
   ![Obraz warunku Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. Wprowadź *twitter* do pola wyszukiwania hello wybiorą hello **Twitter — Opublikuj tweet** akcji. Spowoduje to otwarcie hello **Opublikuj tweet** kontroli, gdy zostanie wprowadź wszystkie szczegóły tweet hello ogłaszany.      
   ![Obraz akcji 1 do 5 w usłudze Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. Wybierz hello **Tweetować tekst** formantu. Wszystkie dane wyjściowe z poprzedniego działania i jest wyzwalane w aplikacji logiki hello są teraz widoczne. Można wybrać dowolny z tych i używać ich jako część hello tweet tekst hello tweet nowe.     
   ![Obraz akcji Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. Wybierz **nazwy użytkownika**   
5. Wprowadź *mówi:* hello tweet tekst formantu. W tym zaraz po nazwy użytkownika.  
6. Wybierz *Tweetować tekstu*.       
   ![Obraz akcji Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. Zapisz swoją pracę i publikowała tweet przy tooactivate hasztagiem hello #Seattle przepływ pracy.  


## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/twitterconnector/). 

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)

