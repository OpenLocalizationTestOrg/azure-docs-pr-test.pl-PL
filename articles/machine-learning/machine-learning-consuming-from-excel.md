---
title: "Usługa sieci Web Machine Learning z programu Excel aaaConsume | Dokumentacja firmy Microsoft"
description: "Korzystanie z usługi sieci Web Azure Machine Learning z programu Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Korzystanie z usługi sieci Web Azure Machine Learning z poziomu programu Excel
 Azure Machine Learning Studio umożliwia łatwe toocall usług sieci web bezpośrednio z programu Excel bez hello muszą toowrite żadnego kodu.

Jeśli używasz programu Excel 2013 (lub nowszy) lub aplikacji Excel Online, a następnie zalecane jest użycie hello Excel [dodatek programu Excel](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Kroki
Publikowanie usługi sieci web. [Ta strona](machine-learning-walkthrough-5-publish-web-service.md) wyjaśniono, jak toodo go. Obecnie funkcja skoroszytu programu Excel hello jest obsługiwana tylko dla usług żądań i odpowiedzi, które mają jeden z (to znaczy pojedynczej oceniania etykiety). 

Po utworzeniu usługi sieci web, kliknij na powitania **usług sieci WEB** po lewej stronie powitania hello Studio, a następnie wybierz tooconsume usługi sieci web hello z programu Excel.

**Usługa sieci Web klasycznego**

1. Na powitania **pulpitu NAWIGACYJNEGO** karcie dla usługi sieci web hello jest wiersz hello **żądanie/odpowiedź** usługi. Jeśli ta usługa miała pojedynczego wyjścia, powinny pojawić się hello **Pobierz skoroszyt programu Excel** łącza w tym wierszu.
   
    ![][1]
2. Polecenie **Pobierz skoroszyt programu Excel**.

**Nowa usługa sieci Web**

1. Hello Azure Machine Learning sieci Web portalu, wybierz **Consume**.
2. Na stronie Consume hello na powitania **opcje przez usługę sieci Web** kliknij ikonę hello w programie Excel.

**Przy użyciu hello skoroszytu**

1. Otwórz hello skoroszytu.
2. Zostanie wyświetlone ostrzeżenie o zabezpieczeniach; polecenie hello **Włącz edytowanie** przycisku.
   
    ![][2]
3. Zostanie wyświetlone ostrzeżenie o zabezpieczeniach. Polecenie hello **Włącz zawartość** przycisk toorun makra w arkuszu kalkulacyjnym.
   
    ![][3]
4. Po włączeniu makra, jest generowany tabeli. Kolumny w niebieski są wymagane jako dane wejściowe do hello rekordy zasobów usługi sieci web, lub **parametry**. Należy pamiętać, dane wyjściowe hello hello usługi RRS **PROGNOZOWANE wartości** na zielono. Jeśli są wszystkie kolumny dla danego wiersza, skoroszytu hello automatycznie wywołuje hello oceniania interfejsu API i wyświetla hello oceniane wyniki.
   
    ![][4]
5. tooscore więcej niż jeden wiersz, wypełnienie hello drugiego wiersza z danymi i hello przewidzieć, że wartości. Jednocześnie można wkleić nawet kilka wierszy.

Można użyć dowolnego z funkcji programu Excel hello (wykresy, mapy zasilania, warunkowego formatowania itp.) z hello przewidzieć toohelp wartości wizualizacji danych hello.    

## <a name="sharing-your-workbook"></a>Udostępnianie skoroszytu
Dla hello toowork makra klucz interfejsu API musi być częścią hello w arkuszu kalkulacyjnym. Oznacza to, że tylko z jednostek/osób, którym ufa powinny współużytkować hello skoroszytu.

## <a name="automatic-updates"></a>Automatyczne aktualizacje
Rekordy zasobów wywołanie w tych dwóch sytuacji:

1. Witaj po raz pierwszy wiersz ma zawartość we wszystkich jego **parametrów**
2. Wtedy żadnego hello **parametry** zmiany w wierszu, który ma wszystkie jego **parametry** wprowadzona.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
