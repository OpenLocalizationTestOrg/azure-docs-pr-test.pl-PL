---
title: "pozwala uzyskać odpowiedzi na dane pytanie - aaaAsk danych nauki problemów — usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pytanie tooformulate nauki sharp danych w w nauce danych dla początkujących 3 wideo. Zawiera porównanie pytania klasyfikacji i regresji."
keywords: "dane nauki problemów, pytania dotyczące analizy danych, sformułować pytania, pytania regresji, klasyfikacji pytania, sharp zapytania"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 00c328f51e6d9ff6654b5966eb97d6762582f7e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a>Zadawanie pytań, na które można odpowiedzieć za pomocą danych
## <a name="video-3-data-science-for-beginners-series"></a>Wideo 3: Nauki danych serii dla początkujących
Dowiedz się, jak tooformulate problem nauki danych do zapytania w nauce danych dla początkujących 3 wideo. Ten film zawiera porównanie pytania dotyczące algorytmów klasyfikacji i regresji.

Witaj tooget wykorzystanie serii hello, obejrzyj je wszystkie. [Przejdź do listy toohello filmów wideo](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>Inne pliki wideo w tej serii
*Nauki danych dla początkujących* to nauka toodata szybkie wprowadzenie w pięciu krótkie wideo.

* Wideo 1: [danych nauki odpowiedzi na pytania hello 5](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sek.)*
* Wideo 2: [jest gotowy do analizy danych danych?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 s 56 min)*
* Wideo 3: Zadaj pytanie, które mogą odpowiedzieć z danymi
* Wideo 4: [prognozowania odpowiedzi z modelu prostego](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 s 42 min)*
* Wideo 5: [skopiować inne osoby pracy toodo danych nauki](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sek.)*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>Zapis: Zadaj pytanie, które mogą odpowiedzieć z danymi
Witamy toohello trzeci wideo w serii hello "Nauki danych dla początkujących".  

W tym przypadku można uzyskać wskazówki dotyczące opracowywania pytanie, które pozwala odpowiedzieć z danymi.

Może zostać wyświetlony więcej poza ten film, jeśli najpierw Obejrzyj hello dwóch wideo wcześniej w tej serii: "hello 5 pytania dotyczące danych nauki może odpowiadać" i "Jest danych jest gotowy do analizy danych?"

## <a name="ask-a-sharp-question"></a>Zadaj pytanie sharp
Zajmowaliśmy jak nauki danych proces hello przy użyciu nazw (nazywanych również kategorii lub etykiety) i numery toopredict tooa odpowiedzi na pytanie. Ale nie można go do dowolnego zapytania; ma ona toobe *sharp pytanie.*

Niezrozumiała pytanie nie ma toobe odpowiedzi z nazwą lub liczbą. Musi być sharp pytanie.

Wyobraź sobie znalezione magic świateł genie, który będzie wyczerpujących odpowiedzi na każde pytanie zapytaniem. Jednak jest mischievous genie i on próbować toomake jego odpowiedzi jako niezrozumiała i mylące, ponieważ może on uzyskać nieobecności z. Ma toopin mu w dół do pytania tak hermetyczne nie może on pomóc ale informujące, co ma tooknow.

Gdyby tooask niezrozumiała zapytania, takie jak "Co będzie toohappen z mojej giełdowych?", hello genie może odpowiedzieć, "zmieni cen hello". To truthful odpowiedzi, ale nie jest to bardzo przydatne.

Ale jeśli były tooask sharp pytanie, jak "Co cena sprzedaży Moje giełdowych zostanie w następnym tygodniu?", hello genie nie może pomóc ale umożliwiają określonej odpowiedzi i prognozowania cen sprzedaży.

## <a name="examples-of-your-answer-target-data"></a>Przykłady odpowiedzi: dane docelowej
Po sformułować pytanie, sprawdź toosee, czy w danych znajdują się przykłady hello odpowiedzi.

W przypadku naszego pytanie "Co cena sprzedaży Moje giełdowych zostanie w następnym tygodniu?" następnie mamy toomake się, że nasze dane zawierają hello giełdowy historii.

W przypadku naszego pytanie "samochodów, które w mojej floty jest toofail będzie najpierw?" następnie mamy toomake się, że nasze dane zawierają informacje dotyczące wcześniejszych niepowodzeń.

![Dane — przykłady odpowiedzi docelowej. Formułowanie zapytania analizy danych.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

Te przykłady odpowiedzi są określane jako element docelowy. Element docelowy jest firma Microsoft są próby toopredict o punktów danych w przyszłości, kategorii lub liczbą.

Jeśli nie masz żadnych danych docelowych, konieczne będzie tooget niektóre. Użytkownik nie będzie możliwe tooanswer pytanie bez niego.

## <a name="reformulate-your-question"></a>Sformułować pytanie
Czasami może adnotacji tooget Twojego zapytania bardziej użyteczna w odpowiedzi.

pytanie Hello "jest to danych punktu A lub B?" Prognozuje hello kategorii (lub nazwę lub etykiety) elementu. tooanswer, używamy *algorytm klasyfikacji*.

Witaj pytanie "Ile?" lub "Ile?" Prognozuje kwotę. tooanswer go używamy *algorytm regresji*.

toosee jak możemy można przekształcać je, Przyjrzyjmy się pytanie Witaj, "wątku wiadomości, które jest najbardziej interesujące czytnika toothis hello?" Sprawdza, czy dla Prognozowanie pojedynczego wyboru z możliwości wielu — innymi słowy "Jest to A lub B i C lub D"? - i użyje algorytm klasyfikacji.

Jednak to pytanie może być łatwiejsze tooanswer, jeśli go jako adnotacji "jak interesujące jest każdy wątek na tej liście czytniku toothis?" Teraz możesz nadać każdego artykułu numeryczny wynik i jest łatwe tooidentify hello najwyższy oceniania artykułu. To jest ponownie sformułować pytanie klasyfikacji hello na pytanie regresji lub ile?

![Sformułować pytanie. Pytanie klasyfikacji i regresji pytanie.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

Jak zadać pytanie jest algorytm toowhich clue umożliwiają odpowiedzi.

Można znaleźć niektórych rodzin algorytmów — podobnie jak hello widocznych w naszym przykładzie wątku wiadomości - są ściśle powiązane. Można sformułować Twoje pytanie toouse hello algorytmu, który umożliwia hello najbardziej przydatne odpowiedzi.

Jednak najważniejsze poproś to pytanie sharp - hello pytanie, które pozwala odpowiedzieć z danymi. Pamiętaj, że masz tooanswer danych po prawej stronie powitania go.

Zajmowaliśmy niektórych podstawowych zasad zadać pytanie się, że można odpowiedzi z danymi.

Należy się toocheck limit hello innych plików wideo w "Danych nauki dla początkujących" z Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Następne kroki
* [Spróbuj pierwszego eksperymentu analizy danych z usługi Machine Learning Studio](machine-learning-create-experiment.md)
* [Pobierz wprowadzenie tooMachine uczenia w systemie Microsoft Azure](machine-learning-what-is-machine-learning.md)
