---
title: "aaaPredict odpowiedzi z modelu regresji proste — usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Jak toocreate regresji prosty model toopredict cen w nauce danych dla początkujących 4 wideo. Obejmuje regresji liniowej z danych docelowych."
keywords: Tworzenie modelu, modelu prostego, prognozowanie cen, model regresji proste
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a>Prognozowanie odpowiedzi za pomocą prostego modelu
## <a name="video-4-data-science-for-beginners-series"></a>Wideo 4: Nauki danych serii dla początkujących
Dowiedz się, jak toocreate toopredict modelu regresji proste hello cen romb w nauce danych dla początkujących 4 wideo. Firma Microsoft będzie Rysuj modelu regresji z danych docelowych.

Witaj tooget wykorzystanie serii hello, obejrzyj je wszystkie. [Przejdź do listy toohello filmów wideo](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>Inne pliki wideo w tej serii
*Nauki danych dla początkujących* to nauka toodata szybkie wprowadzenie w pięciu krótkie wideo.

* Wideo 1: [danych nauki odpowiedzi na pytania hello 5](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sek.)*
* Wideo 2: [jest gotowy do analizy danych danych?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 s 56 min)*
* Wideo 3: [Zadaj pytanie może odpowiedzieć z danymi](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 s 17 min)*
* Wideo 4: Odpowiedź z prostego modelu prognozowania
* Wideo 5: [skopiować inne osoby pracy toodo danych nauki](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sek.)*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>Zapis: Przewidywanie odpowiedzi z modelu prostego
Zapraszamy toohello czwarty wideo w serii "Danych nauki dla początkujących" hello. W tym przypadku firma Microsoft budowanie prostego modelu i prognozowanie.

A *modelu* jest uproszczone artykuł o naszych danych. Będzie można wyświetlić I znaczenie.

## <a name="collect-relevant-accurate-connected-enough-data"></a>Zbieranie odpowiednich, dokładne, połączenie, jest za mało danych
Załóżmy, że chcę tooshop romb. Mam pierścień, który należał babcia toomy z ustawieniem dla romb 1.35 karatach i ma tooget informacje o tym, jaki będzie koszt. I uwzględniać Notatnik i pióra hello biżuteria magazynu i I Zanotuj cen hello wszystkich karo hello w przypadku hello i ile porównać w carats. Począwszy od pierwszego romb hello - carats 1.01 jego i 7,366 $.

Teraz przejdź i wykonaj dla wszystkich hello innych diamentów w magazynie hello.

![Kolumny danych romb](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

Zwróć uwagę, że naszej listy ma dwie kolumny. Każda kolumna ma inny atrybut — wagę carats i cen — oraz każdy wiersz jest pojedynczego punktu danych reprezentujący pojedynczego romb.

Faktycznie utworzyliśmy małą tutaj — zestawu danych tabeli. Zwróć uwagę, że spełnia kryteriów jakości:

* dane Hello są **odpowiednich** -waga jest ostatecznie powiązanych tooprice
* Ma ona **dokładne** -możemy dokładnie sprawdzone ceny hello możemy zapisać
* Ma ona **połączone** — istnieją nie spacji w dowolnej z tych kolumn
* I jak zajmiemy się tym, ma **za mało** tooanswer danych naszych zapytania

## <a name="ask-a-sharp-question"></a>Zadaj pytanie sharp
Obecnie firma Microsoft będzie stanowić naszych zapytania w sposób sharp: "jaka będzie koszt toobuy romb karatach 1.35?"

Naszej listy nie ma romb 1.35 karatach, dlatego firma Microsoft zapewnia toouse hello reszty tooget naszych danych toohello odpowiedzi na pytanie.

## <a name="plot-hello-existing-data"></a>Wykreślenia hello istniejących danych
Witaj najpierw robimy jest poziomej linii numer o nazwie osi toochart hello wagi. Hello zakres wag hello jest 0 too2, dlatego firma Microsoft będzie rysowanie linii obejmujący zakresu i umieścić znaczniki dla każdego połowa karatach.

Następnie firma Microsoft będzie rysowanie cenę hello toorecord osi pionowej i podłącz go osi poziomej wagi toohello. Są to w jednostkach kwoty. Teraz mamy zestaw współrzędnych osi.

![Osie wagi i cen](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

Firma Microsoft jest tootake będzie teraz te dane i wyłączyć go do *wykres punktowy*. Jest to liczbowe zestawów danych doskonały sposób toovisualize.

Dla pierwszego punktu danych hello możemy eyeball pionowych linii w 1.01 carats. Następnie możemy eyeball poziomych linii w 7,366 $. Jeżeli spełniają one możemy zwrócić kropką. Reprezentuje naszym pierwszym romb.

Teraz możemy przejść przez każdego romb na tej liście i hello samo. Kiedy jesteśmy za pośrednictwem jest będziemy mieć: licznych kropkami, jeden dla każdej romb.

![Wykres punktowy](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Rysuj modelu hello hello punktów danych
Teraz można spojrzeć na powitania kropki i squint kolekcji hello wygląda jak linia fat, rozmytego. Możemy zająć naszych znacznika i rysowanie linii prostej za jego pośrednictwem.

Za pomocą rysowania linii, utworzyliśmy *modelu*. Należy traktować jako biorąc Witaj świecie rzeczywistym i wersji simplistic kreskówki go. Teraz kreskówki hello jest nieprawidłowy — hello wiersza nie jest akceptowana wszystkich hello punktów danych. Jednak jest przydatne uproszczenia.

![Regresji liniowej](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

Witaj fakt, że kropki hello nie przechodzą dokładnie wiersza hello jest OK. Analityków danych opisano to przez informujący model hello - wiersza hello —, a następnie każdego punktu ma niektóre *szumu* lub *wariancji* skojarzonych z nim. Brak hello doskonałe relacji podstawowej i oznacza to, że Witaj świecie do obsługi niepowtarzalne, rzeczywista dodające szumu i niedokładność.

Ponieważ próbujemy pytanie hello tooanswer *ile?* jest to *regresji*. I dlatego firma Microsoft korzysta z prostej, jest *regresji liniowej*.

## <a name="use-hello-model-toofind-hello-answer"></a>Użyj hello modelu toofind hello odpowiedzi
Teraz mamy modelu i poprosimy go naszych pytanie: jaka będzie romb 1.35 karatach koszt?

tooanswer nasze pytanie, możemy oka 1.35 carats i rysowanie linii pionowej. W przypadku, gdy jego przecina hello modelu wiersza, firma Microsoft eyeball osią linia pozioma toohello dolara ($). Trafienia jego prawej strony na 10 000. Wysięgnik! To już odpowiedzi hello: romb 1.35 karatach koszty około 10 000.

![Znajdź odpowiedzi hello na powitania modelu](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>Utwórz przedział ufności
Jest fizyczną toowonder jak ta prognozy są dokładne. Jest przydatne tooknow czy romb 1.35 karatach hello będą bardzo Zamknij za 10 000 lub wiele większej lub mniejszej. toofigure tego, umożliwia rysowanie koperty wokół hello regresji wiersz, który zawiera większość hello kropek. Ten koperty jest wywoływana naszych *przedział ufności*: jest dość pewność, że ceny mieszczą się w tym koperty, ponieważ w przeszłości hello większość z nich. Firma Microsoft Rysuj dwóch więcej poziome linie, z których wiersza 1.35 karatach hello przecina hello górny i dolny hello tego koperty protokołu.

![Przedział ufności](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

Teraz możemy powiedzieć coś o naszych przedział ufności: możemy powiedzieć bez obaw czy cena hello romb 1.35 karatach jest około $ 10 000 -, ale może być możliwie jak $8000 i może być możliwie jak 12 000.

## <a name="were-done-with-no-math-or-computers"></a>Skończymy, bez matematyczne lub komputerów
Robiliśmy, jakie analityków danych uzyskać płatną toodo i robiliśmy tylko za pomocą rysowania:

* Firma Microsoft zadawane pytania firma Microsoft może odpowiedzi z danymi
* Budujemy *modelu* przy użyciu *regresji liniowej*
* Wprowadziliśmy *prognozowania*, wraz z *przedział ufności*

I nie używamy matematyczne lub komputery toodo go.

Teraz, jeśli tak samo, jak gdyby było więcej informacji...

* Wytnij Hello z romb hello
* kolory (jak blisko romb hello jest białe toobeing)
* Liczba Hello dołączenia w romb hello

.. .i firma musiałaby większą liczbę kolumn. W takim przypadku matematyczne staje się przydatne. Jeśli masz więcej niż dwie kolumny jest toodraw twardym kropki w dokumencie. matematyczne Hello umożliwia bardzo dobrze nadające się tego wiersza lub dane tooyour płaszczyzny.

Ponadto jeśli zamiast tylko kilku karo, było dwa tysiące lub dwóch milionów, a następnie wykonaj pracy znacznie szybciej z komputerem.

Obecnie zajmowaliśmy jak regresji liniowej toodo i my wprowadzone prognozowania, przy użyciu danych.

Należy się toocheck limit hello innych plików wideo w "Danych nauki dla początkujących" z Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Następne kroki
* [Spróbuj pierwszego eksperymentu analizy danych z usługi Machine Learning Studio](machine-learning-create-experiment.md)
* [Pobierz wprowadzenie tooMachine uczenia w systemie Microsoft Azure](machine-learning-what-is-machine-learning.md)
