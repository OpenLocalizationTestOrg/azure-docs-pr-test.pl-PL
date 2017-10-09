---
title: "Dodatek aaaExcel dla usługi Machine Learning Web | Dokumentacja firmy Microsoft"
description: "Jak toouse Azure Machine Learning w sieci Web usług bezpośrednio w programie Excel bez pisania żadnego kodu."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>Dodatki programu Excel do usług sieci Web Azure Machine Learning
Excel umożliwia łatwe toocall usług sieci web bezpośrednio bez hello muszą toowrite żadnego kodu.

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>Kroki tooUse usługi sieci web istniejące w hello skoroszytu

1. Otwórz hello [przykładowy plik programu Excel](http://aka.ms/amlexcel-sample-2), który zawiera hello dodatek programu Excel i dane dotyczące osób na hello Titanic.
2. Wybierz usługę sieci web hello kliknięciem — "Titanic predykcyjne renty (przykład dodatku Excel) [Wynik]" w tym przykładzie.
   
    ![Wybierz usługę sieci Web][01]
3. Powoduje to przejście toohello **Predict** sekcji.  Ten skoroszyt zawiera już dane przykładowe, ale dla pustego skoroszytu można zaznaczyć komórkę w programie Excel i kliknij przycisk **użyj przykładowych danych**.
4. Wybierz dane hello z nagłówkami i kliknij ikonę zakres danych wejściowych hello.  Upewnij się, że zaznaczone jest pole "dane ma nagłówki" hello.
5. W obszarze **dane wyjściowe**, wprowadź numer komórki hello, w której mają hello toobe danych wyjściowych, na przykład "H1" w tym miejscu.
6. Kliknij przycisk **prognozowania**.
   
    ![Przewidywanie sekcji][02]

Wdrażanie usługi sieci web, lub użyj istniejącej usługi sieci Web. Aby uzyskać więcej informacji na temat wdrażania usługi sieci web, zobacz [wskazówki krok 5: Wdrażanie usługi sieci Web Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md).

Pobierz hello klucza interfejsu API usługi sieci web. Miejsce można wykonać tej akcji zależy czy opublikowane usługi sieci web klasycznego uczenia maszynowego usługi sieci web uczenie maszynowe nowe.

**Użyj usługi sieci web klasycznego** 

1. W usłudze Machine Learning Studio, kliknij przycisk hello **usług sieci WEB** sekcji w okienku po lewej stronie powitania, a następnie wybierz hello usługi sieci web.
   
    ![Wybierz Studio usługi sieci Web][04]
2. Skopiuj klucz interfejsu API hello hello usługi sieci web.
   
    ![Klucz interfejsu API Studio][05]
3. Na powitania **pulpitu NAWIGACYJNEGO** hello usługi sieci web, kliknij pozycję hello **żądanie/odpowiedź** łącza.
4. Wyszukaj hello **przez identyfikator URI żądania** sekcji.  Skopiuj i Zapisz adres URL hello.

> [!NOTE]
> Teraz jest możliwe toosign do hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu tooobtain klucza hello interfejsu API usługi sieci web uczenie maszynowe klasycznego.
> 
> 

**Użyj nowej usługi sieci web**

1. W hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu, kliknij przycisk **usług sieci Web**, wybierz opcję usługi sieci web. 
2. Kliknij przycisk **korzystać**.
3. Wyszukaj hello **zużycie podstawowe informacje o** sekcji. Skopiuj i Zapisz hello **klucza podstawowego** i hello **żądań i odpowiedzi** adresu URL.

## <a name="steps-tooadd-a-new-web-service"></a>Kroki tooAdd nową usługę sieci web

1. Wdrażanie usługi sieci web, lub użyj istniejącej usługi sieci Web. Aby uzyskać więcej informacji na temat wdrażania usługi sieci web, zobacz [wskazówki krok 5: Wdrażanie usługi sieci Web Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md).
2. Kliknij przycisk **korzystać**.
3. Wyszukaj hello **zużycie podstawowe informacje o** sekcji. Skopiuj i Zapisz hello **klucza podstawowego** i hello **żądań i odpowiedzi** adresu URL.
4. W programie Excel Przejdź toohello **usług sieci Web** sekcji (w hello **Predict** kliknij hello strzałkę Wstecz toogo toohello listę usług sieci web).
   
    ![Przejdź tooWeb wybór usługi][03]
5. Kliknij przycisk **Dodaj usługę sieci Web**.
6. Wklej adres URL hello do hello etykietą pole tekstowe dodatek programu Excel **adres URL**.
7. Wklej klucz interfejsu API/podstawowy hello hello pole tekstowe z etykietą **klucz interfejsu API**.
8. Kliknij pozycję **Dodaj**.
   
    ![Adres URL i klucz API usługi sieci Web klasycznego.][06]
9. usługi sieci web hello toouse, wykonaj hello poprzedzających kierunków, "Kroki tooUse istniejące sieci web usługi."

## <a name="sharing-your-workbook"></a>Udostępnianie skoroszytu
Czy zapisać skoroszyt, klucz interfejsu API/podstawowy hello hello usług sieci web, które zostały dodane również jest zapisywane. Oznacza to, że skoroszytu hello powinien udostępniać tylko dla osób zaufanych.

Pytania w hello następujących sekcji komentarza lub na naszych [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
