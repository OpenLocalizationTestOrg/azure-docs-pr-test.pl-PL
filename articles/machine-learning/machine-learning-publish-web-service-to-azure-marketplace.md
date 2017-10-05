---
title: "(przestarzałe) Publikowanie usługi machine learning web service w portalu Azure Marketplace | Dokumentacja firmy Microsoft"
description: "(przestarzałe) Jak opublikować usługi sieci Web Azure Machine Learning w portalu Azure Marketplace"
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
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a>(przestarzałe) Publikowanie usługi sieci Web Azure Machine Learning w portalu Azure Marketplace

> [!NOTE]
> DataMarket i usług danych jest wycofana i istniejące subskrypcje zostaną wycofane i anulowane uruchamianie 3/31/2017 r. W związku z tym w tym artykule jest przestarzałe. 
> 
> Alternatywnie, można opublikować eksperymentów uczenia maszynowego do [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) dla społeczności analizy danych. Aby uzyskać więcej informacji, zobacz [udziału i odnajdywania zasobów w Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

W portalu Azure Marketplace pozwala, aby opublikować usługi sieci web Azure Machine Learning płatnej, lub zwolnij usługi do użycia przez klientów zewnętrznych. Ten artykuł zawiera omówienie procesu z łącza do wskazówki ułatwiające rozpoczęcie pracy. Za pomocą tego procesu, można udostępnić swoje usługi sieci web innych deweloperom korzystanie w swoich aplikacjach.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a>Omówienie procesu publikowania
Poniżej przedstawiono kroki publikowania usługi sieci web uczenie maszynowe Azure w portalu Azure Marketplace:

1. Tworzenie i publikowanie usługi Machine Learning żądań i odpowiedzi (RR)
2. Wdrażanie usługi do środowiska produkcyjnego i uzyskiwania informacji punktu końcowego klucz interfejsu API i OData.
3. Użyj adresu URL usługi sieci web opublikowane do publikowania [portalu Azure Marketplace (rynku danych)](https://publish.windowsazure.com/workspace/) 
4. Po przesłane, przejrzeć Twoją ofertę i wymaga zatwierdzenia przed klientów można uruchomić jej zakup. Publikowanie proces może potrwać kilka dni roboczych. 

## <a name="walk-through"></a>Przewodnik
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>Krok 1: Tworzenie i publikowanie usługi Machine Learning żądań i odpowiedzi (RR)
 Jeśli nie zostało zrobione to już, należy spojrzeć na to [przeprowadzenie](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a>Krok 2: Wdrażanie usługi do środowiska produkcyjnego i uzyskać klucz interfejsu API i informacje o punkcie końcowym OData
1. Z [klasycznego portalu Azure](http://manage.windowsazure.com), wybierz pozycję **UCZENIA MASZYNOWEGO** opcji na pasku nawigacyjnym po lewej stronie, a następnie wybierz obszar roboczy. 
2. Polecenie **usług sieci WEB** , a następnie wybierz usługę sieci web ma zostać publikowanie w portalu marketplace.
   
    ![Azure Marketplace][workspace]
3. Wybierz punkt końcowy chcesz korzystać z portalu marketplace. Jeśli nie utworzono żadnych dodatkowych punktów końcowych, możesz wybrać **domyślne** punktu końcowego.
4. Po kliknięciu przycisku w punkcie końcowym, będzie mógł wyświetlić **klucz interfejsu API**. Należy ten element informacji później w kroku 3, dlatego należy kopii.
   
    ![Azure Marketplace][apikey]
5. Polecenie **żądanie/odpowiedź** metody, w tym punkcie publikowania usługi wykonywania wsadowego w portalu Marketplace nie jest obsługiwana. Spowoduje to do strona pomocy interfejsu API dla metody żądania i odpowiedzi.
6. Kopiuj **adres punktu końcowego OData**, należy te informacje później w kroku 3.
   
    ![Azure Marketplace][odata]

Wdrażanie usługi do środowiska produkcyjnego.

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a>Krok 3: Użyj adresu URL usługi sieci web opublikowane do publikowania w portalu Azure Marketplace (DataMarket)
1. Przejdź do [witrynę Azure Marketplace (rynku danych)](http://datamarket.azure.com/home) 
2. Polecenie **publikowania** łącze w górnej części strony. Spowoduje to przejście do [publikowania portalu usługi Microsoft Azure](https://publish.windowsazure.com)
3. Polecenie **wydawców** sekcji, aby zarejestrować jako wydawca.
4. Podczas tworzenia nowej oferty, wybierz **usług danych**, następnie kliknij przycisk **Utwórz nową usługę danych**. 
   
   ![Azure Marketplace][image1]
   
   <br />
5. W obszarze **plany** zawierają informacje na Twojej oferty, w tym planu cenowego. Zdecyduj, jeśli będą oferować usługę wolne lub płatną. Aby uzyskać płatną, podaj informacje dotyczące płatności, takich jak informacji bankowych i podatek.
6. W obszarze **Marketing** zawierają informacje o Twojej oferty, takie jak tytuł i opis dla danej oferty.
7. W obszarze **cennik** można ustawić ceny dla planów dla określonych krajów lub Niech system "autoprice" ofertę.
8. Na **Usługa danych** , kliknij pozycję **usługi sieci Web** jako **źródła danych**.
   
    ![Azure Marketplace][image2]
9. Pobierz klucz adresu URL i interfejsu API usługi sieci web z klasycznego portalu Azure, zgodnie z objaśnieniem w kroku 2. powyżej.
10. W oknie dialogowym Instalator usługi danych portalu Marketplace, wklej adres punktu końcowego OData do **adres URL usługi** pola tekstowego.
11. Aby uzyskać **uwierzytelniania**, wybierz **nagłówka** jako **schemat uwierzytelniania**.
    
    * Wprowadź "Autoryzacji" **nazwa nagłówka**.
    * Dla **wartość nagłówka**wpisz "Bearer" (bez cudzysłowów), kliknij przycisk **miejsca** pasek, a następnie wklej klucz interfejsu API.
    * Wybierz **ta usługa jest OData** pole wyboru.
    * Kliknij przycisk **Testuj połączenie** testowania połączenia.
12. W obszarze **kategorii**, upewnij się, **uczenia maszynowego** jest zaznaczone.
13. Po zakończeniu wprowadzania wszystkie metadane dotyczące Twojej oferty, kliknij **publikowania**, a następnie **wypychania do przemieszczania**. W tym momencie dowiesz się wszelkie pozostałe problemy, które trzeba naprawić.
14. Po zapewnieniu ukończenia nierozwiązane problemy, kliknij polecenie **zażądać zatwierdzenia do produkcji**. Publikowanie proces może potrwać kilka dni roboczych. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

