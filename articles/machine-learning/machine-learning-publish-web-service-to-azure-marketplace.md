---
title: "AAA(deprecated) publikowania machine learning tooAzure usługi sieci web portalu Marketplace | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Jak toopublish Twojego toohello Usługa sieci Web systemu Azure Machine Learning portalu Azure Marketplace"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>(przestarzałe) Publikowanie toohello Usługa sieci Web systemu Azure Machine Learning portalu Azure Marketplace

> [!NOTE]
> DataMarket i usług danych jest wycofana i istniejące subskrypcje zostaną wycofane i anulowane uruchamianie 3/31/2017 r. W związku z tym w tym artykule jest przestarzałe. 
> 
> Alternatywnie, można opublikować toohello eksperymentów z uczenia maszynowego [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) asysty hello hello danych nauki społeczności. Aby uzyskać więcej informacji, zobacz [udziału i odnajdywania zasobów w hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Hello Azure Marketplace udostępnia możliwości hello usług sieci web Azure Machine Learning toopublish płatnej, lub zwolnij usługi do użycia przez klientów zewnętrznych. Ten artykuł zawiera omówienie procesu z łącza tooguidelines tooget, który został uruchomiony. Za pomocą tego procesu, można udostępnić swoje usługi sieci web dla innych tooconsume deweloperów w swoich aplikacjach.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>Omówienie procesu publikowania hello
Hello poniżej przedstawiono kroki publikowania tooAzure usługi sieci web uczenie maszynowe Azure Marketplace hello:

1. Tworzenie i publikowanie usługi Machine Learning żądań i odpowiedzi (RR)
2. Wdrażanie hello tooproduction usługi i w zamian hello klucz interfejsu API i OData informacje o punkcie końcowym.
3. Adres URL hello Użyj hello opublikowane za toopublish usługi sieci web[portalu Azure Marketplace (rynku danych)](https://publish.windowsazure.com/workspace/) 
4. Po przesłane, przejrzeć Twoją ofertę i musi toobe zatwierdzona przed klientów można uruchomić jej zakup. proces publikowania Hello może potrwać kilka dni roboczych. 

## <a name="walk-through"></a>Przewodnik
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>Krok 1: Tworzenie i publikowanie usługi Machine Learning żądań i odpowiedzi (RR)
 Jeśli nie zostało zrobione to już, należy spojrzeć na to [przeprowadzenie](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>Krok 2: Wdrażanie hello usługi tooproduction i uzyskać informacje o punkcie końcowym klucz interfejsu API i OData hello
1. Z hello [klasycznego portalu Azure](http://manage.windowsazure.com), wybierz pozycję hello **UCZENIA MASZYNOWEGO** opcję hello na pasku nawigacyjnym po lewej stronie, a następnie wybierz obszar roboczy. 
2. Polecenie hello **usług sieci WEB** kartę i usługi sieci web wybierz hello chcesz toopublish toohello marketplace.
   
    ![Azure Marketplace][workspace]
3. Wybierz hello punktu końcowego użytkownik będzie jak toohave hello marketplace używać. Jeśli nie utworzono żadnych dodatkowych punktów końcowych, możesz wybrać hello **domyślne** punktu końcowego.
4. Po kliknięciu przycisku w punkcie końcowym hello, będą mogli toosee hello **klucz interfejsu API**. Należy ten element informacji później w kroku 3, dlatego należy kopii.
   
    ![Azure Marketplace][apikey]
5. Polecenie hello **żądanie/odpowiedź** metody, w tym punkcie nie obsługujemy publikowania wykonywania wsadowego usługi toohello marketplace. Spowoduje to strona pomocy toohello interfejsu API dla hello metoda żądania i odpowiedzi.
6. Kopiuj hello **adres punktu końcowego OData**, należy te informacje później w kroku 3.
   
    ![Azure Marketplace][odata]

Wdrażanie usługi hello w środowisku produkcyjnym.

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>Krok 3: Adres URL hello Użyj hello opublikowane tooAzure toopublish usługi sieci web witryny Marketplace (DataMarket)
1. Przejdź do zbyt[portalu Azure Marketplace (rynku danych)](http://datamarket.azure.com/home) 
2. Polecenie hello **publikowania** łącze u góry hello hello strony. Spowoduje to przejście toohello [publikowania portalu usługi Microsoft Azure](https://publish.windowsazure.com)
3. Polecenie hello **wydawców** tooregister sekcji jako wydawca.
4. Podczas tworzenia nowej oferty, wybierz **usług danych**, następnie kliknij przycisk **Utwórz nową usługę danych**. 
   
   ![Azure Marketplace][image1]
   
   <br />
5. W obszarze **plany** zawierają informacje na Twojej oferty, w tym planu cenowego. Zdecyduj, jeśli będą oferować usługę wolne lub płatną. tooget płatnej, podaj informacje dotyczące płatności, takich jak informacji bankowych i podatku.
6. W obszarze **Marketing** zawierają informacje o Twojej oferty, takie jak hello tytuł i opis dla danej oferty.
7. W obszarze **cennik** ustawić hello cen dla planów dla określonych krajów lub pozostawić hello "autoprice" ofertę.
8. Na powitania **Usługa danych** , kliknij pozycję **usługi sieci Web** jako hello **źródła danych**.
   
    ![Azure Marketplace][image2]
9. Pobierz hello klucza usługi sieci web adres URL i interfejsu API z hello klasycznego portalu Azure, zgodnie z objaśnieniem w kroku 2. powyżej.
10. W hello okno dialogowe Ustawienia usługi danych portalu Marketplace, wklej adres punktu końcowego OData hello do hello **adres URL usługi** pola tekstowego.
11. Aby uzyskać **uwierzytelniania**, wybierz **nagłówka** jako hello **schemat uwierzytelniania**.
    
    * Wprowadź "Autoryzacji" hello **nazwa nagłówka**.
    * Dla hello **wartość nagłówka**, wprowadź "Bearer" (bez cudzysłowów hello), kliknij przycisk hello **miejsca** paska, a następnie wklej klucz hello interfejsu API.
    * Wybierz hello **ta usługa jest OData** pole wyboru.
    * Kliknij przycisk **Testuj połączenie** tootest hello połączenia.
12. W obszarze **kategorii**, upewnij się, **uczenia maszynowego** jest zaznaczone.
13. Po zakończeniu wprowadzania wszystkie hello metadanych o ofertę, kliknij **publikowania**, a następnie **Push tooStaging**. W tym momencie użytkownik zostanie powiadomiony o pozostałe problemy należy toofix.
14. Po zapewnieniu ukończenia wszystkich hello nierozwiązane problemy, kliknij polecenie **żądania zatwierdzenia toopush tooProduction**. proces publikowania Hello może potrwać kilka dni roboczych. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

