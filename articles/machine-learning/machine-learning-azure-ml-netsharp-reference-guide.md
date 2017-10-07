---
title: "toohello aaaGuide sieci Neuronowej sieci specyfikacji języka # | Dokumentacja firmy Microsoft"
description: "Składnia hello Net # neuronowej sieci specyfikacji języka, wraz z przykładami jak toocreate niestandardowe sieci neuronowej modelu w Microsoft Azure ML przy użyciu Net #"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Przewodnik tooNet sieci neuronowej specyfikacji języka # dla usługi Azure Machine Learning
## <a name="overview"></a>Omówienie
NET # jest językiem, który został opracowany przez firmę Microsoft, który jest używany toodefine architektury sieci neuronowej. Używając Net # w Microsoft Azure Machine Learning modułach sieci neuronowej.

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

W tym artykule dowiesz się, że podstawowe koncepcje potrzebne toodevelop niestandardowe sieci neuronowej: 

* Wymagania dotyczące sieci neuronowej i jak toodefine hello podstawowe składniki
* Składnia Hello i słów kluczowych występujących hello Net # specyfikacja języka
* Przykłady sieci neuronowej niestandardowe utworzone przy użyciu Net # 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>Podstawowe informacje o sieci neuronowej
Struktura sieci neuronowej składa się z ***węzłów*** który są zorganizowane w ***warstwy***i ważoną ***połączeń*** (lub ***krawędzi***) między Witaj węzłów. połączenia Hello są kierunkowe, a każde połączenie ma ***źródła*** węzła i ***docelowego*** węzła.  

Każdy ***trainable warstwy*** (ukryty lub warstwę danych wyjściowych) ma co najmniej jeden ***pakietów połączenia***. Pakiet połączenia składa się z warstwy źródła i specyfikacja hello połączeń z tym warstwy źródła. Wszystkie połączenia hello w udziale pakietu w danym hello sam ***warstwy źródła*** i hello sam ***warstwy docelowej***. W sieci # pakietu połączenia jest uznawany za należące toohello pakietu warstwy docelowej.  

NET # obsługuje różne rodzaje pakietów połączenia, co umożliwia dostosowanie sposobu hello dane wejściowe są mapowane toohidden warstwy i zmapowane toohello danych wyjściowych.   

domyślne Hello lub standardowy pakietu jest **pełny pakiet**, w których każdego węzła w hello warstwa źródłowa jest węzłem tooevery połączonych w warstwę docelową hello.  

Ponadto Net # obsługuje następujące cztery rodzaje zaawansowane połączenie pakietów hello:  

* **Filtrowane pakiety**. Hello użytkownika można określić predykat przy użyciu lokalizacji hello hello źródło warstwy węzła i hello docelowego węzła warstwy. Węzły są połączone, przy każdym predykatu hello ma wartość True.
* **Pakiety convolutional**. Hello użytkownika można zdefiniować małych klubów węzłów hello źródło warstwy. Każdy węzeł w warstwę docelową hello to środowisko tooone połączonych węzłów w warstwie źródła hello.
* **Buforowanie pakiety** i **pakiety normalizacji odpowiedzi**. Są to podobne tooconvolutional pakietów w tym hello użytkownika definiuje małych klubów węzły w warstwie źródła hello. Różnica Hello jest hello wagi hello krawędzi te pakiety nie są trainable. Zamiast tego jest stosowana funkcja wstępnie zdefiniowanych węzeł źródłowy toohello wartości toodetermine hello docelowego węzła wartość.  

Przy użyciu Net # toodefine hello struktury sieci neuronowej ułatwia toodefine możliwe złożonych struktury, takich jak sieci neuronowe głębokość lub splotowi dowolnego wymiarów, które są znane tooimprove uczenie na danych, takich jak obraz, audio i wideo.  

## <a name="supported-customizations"></a>Obsługiwane dostosowania
Architektura Hello sieci neuronowej modeli, które możesz utworzyć w usłudze Azure Machine Learning można często dostosować za pomocą Net #. Możesz:  

* Tworzenie warstw ukryte i kontroli hello liczby węzłów w każdej warstwie.
* Określ, jak warstwy są połączone toobe tooeach innych.
* Zdefiniuj struktury łączności specjalnych, takich jak splotowi i wagi udostępnianie pakietów.
* Określ inną aktywacji funkcji.  

Szczegółowe informacje o składni języka specyfikacji hello, zobacz [specyfikacji struktury](#Structure-specifications).  

Przykłady Definiowanie sieci neuronowe dla niektórych typowych maszyny uczenia zadania z jednostronne toocomplex znaleźć [przykłady](#Examples-of-Net#-usage).  

## <a name="general-requirements"></a>Wymagania ogólne
* Musi to być dokładnie jeden wyjściowy warstwy, co najmniej jedną warstwę wejściowego i zero lub więcej warstwy ukryte. 
* Każda warstwa ma stała liczba węzłów, koncepcyjnie ułożone w tablicy regularnej dowolnego wymiarów. 
* Warstwy wejściowy nie może mieć skojarzone przeszkolone parametrów i reprezentują punktu hello, gdzie dane wystąpienia wpływa hello sieci. 
* Skojarzony przeszkolone parametrów, znany jako obciążeń i odchyleń trainable warstwy (hello warstwy ukryte i wyjścia). 
* Hello węzły źródłowe i docelowe muszą być w oddzielnym warstwy. 
* Połączenia muszą być acykliczne; innymi słowy nie może być łańcuch połączeń prowadzącego wstecz toohello węzeł źródłowy początkowy.
* Warstwa danych wyjściowych Hello nie może być warstwę źródła pakietu połączenia.  

## <a name="structure-specifications"></a>Specyfikacje — struktura
Specyfikacja struktury sieci neuronowej składa się z trzech części: hello **deklaracji stałej**, hello **warstwy deklaracji**, hello **deklaracji połączenia**. Istnieje również opcjonalny **udostępnianie deklaracji** sekcji. sekcje Hello można określić w dowolnej kolejności.  

## <a name="constant-declaration"></a>Deklaracja stałej
Deklaracja stałej jest opcjonalna. Zapewnia on toodefine oznacza, że wartości używane w innym miejscu w definicji sieci neuronowej hello. instrukcji deklaracji Hello składa się z identyfikatorem następuje znak równości i wyrażenie wartości.   

Na przykład po instrukcji hello definiuje stałą **x**:  

    Const X = 28;  

toodefine co najmniej dwie stałe jednocześnie, ujmij hello identyfikator nazwy i wartości w nawiasach klamrowych i oddziel je średnikami. Na przykład:  

    Const { X = 28; Y = 4; }  

prawa strona wyrażenia każdego przypisania Hello może być liczbą całkowitą, liczba rzeczywista, wartość logiczna (True lub False) lub wyrażeniu matematycznym. Na przykład:  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>Deklaracja warstwy
Deklaracja warstwy Hello jest wymagana. Definiuje hello rozmiar i źródło warstwy hello, łącznie z pakietów połączenia i ich atrybutów. Witaj deklaracji instrukcji rozpoczyna się od ciągu hello nazwa warstwy hello (dane wejściowe, ukryty lub dane wyjściowe), a następnie wymiarów hello hello warstwy (krotki dodatnie liczby całkowite). Na przykład:  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* produkt Hello wymiarów hello jest hello liczby węzłów w warstwie hello. W tym przykładzie istnieją dwa wymiary [5,20], co oznacza, że istnieją 100 węzły w warstwie hello.
* Witaj warstw mogą być deklarowane w dowolnej kolejności, z jednym wyjątkiem: Jeśli zdefiniowano więcej niż jedną warstwę wejściowych, hello kolejność, w którym jest zadeklarowany musi odpowiadać kolejności hello funkcji w danych wejściowych hello.  

toospecify, który można hello liczby węzłów w warstwie ustalany automatycznie, użyj hello **automatycznie** — słowo kluczowe. Witaj **automatycznie** — słowo kluczowe ma wpływ różne, w zależności od warstwy hello:  

* W deklaracji wejściowych warstwy hello liczba węzłów to hello liczba funkcji w danych wejściowych hello.
* W deklaracji ukrytej warstwie hello liczba węzłów to numer hello, określonym przez wartość parametru hello **liczba węzłów**. 
* W deklaracji warstwy danych wyjściowych hello liczba węzłów to 2 dwuklasowych klasyfikacji, 1 regresji i równy toohello liczba węzłów wyjściowych wieloklasowej klasyfikacji.   

Na przykład hello następującą definicję sieci umożliwia hello rozmiar wszystkich toobe warstwy ustalany automatycznie:  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


Deklaracja warstwy trainable warstwy (hello warstwy ukryte lub wyjściowe) można opcjonalnie dołączyć dane wyjściowe hello funkcji (nazywanych również funkcję aktywacji), która domyślnie przyjmowana jest zbyt**sigmoid** modele klasyfikacji i **liniowy** dla modeli regresji. (Nawet jeśli korzystasz z domyślnego hello, możesz można jawnie stanu hello aktywacji funkcji, w razie potrzeby dla uzyskania przejrzystości.)

Witaj następujące dane wyjściowe funkcje są obsługiwane:  

* sigmoid
* liniowy
* softmax
* rlinear
* kwadratowe
* SQRT
* srlinear
* ABS
* TANH 
* brlinear  

Na przykład po deklaracji hello używa hello **softmax** funkcji:  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>Deklaracja połączenia
Natychmiast po zdefiniowaniu warstwy trainable hello, musisz zadeklarować połączeń między warstwami hello, które zostały zdefiniowane. Deklaracja pakietu połączenia Hello rozpoczyna się od słowa kluczowego hello **z**, a następnie według nazwy hello hello pakietu źródłowego warstwy i hello rodzaju połączenia toocreate pakietu.   

Obecnie są obsługiwane pięć rodzajów pakietów połączenia:  

* **Pełna** pakiety wskazane przez hello — słowo kluczowe **wszystkie**
* **Filtrowane** pakiety wskazane przez hello — słowo kluczowe **gdzie**, a następnie wyrażenie predykatu
* **Convolutional** pakiety wskazane przez hello — słowo kluczowe **convolve**, a następnie hello konwolucji atrybutów
* **Buforowanie** pakiety wskazane według słów kluczowych hello **maksymalnej liczby puli** lub **oznacza puli**
* **Odpowiedź normalizacji** pakiety wskazane przez hello — słowo kluczowe **normy odpowiedzi**      

## <a name="full-bundles"></a>Pełna pakietów
Pakiet pełne połączenie zawiera połączenia z każdego węzła w hello źródło warstwy tooeach w węźle hello warstwy docelowej. Jest to hello domyślny typ połączenia sieciowego.  

## <a name="filtered-bundles"></a>Pakiety filtrowane
Specyfikacja pakietu połączenia filtrowanego obejmuje predykatu, wyrażona składnię, bardzo podobnie jak wyrażenia lambda C#. Witaj poniższy przykład definiuje dwie filtrowanych pakietów:  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* W predykacie powitania dla *ByRow*, **s** parametr reprezentujący indeks w tablicy regularnej hello węzłów wejściowych warstwy hello, *pikseli*, i **d**  parametr reprezentujący indeks w tablicy hello węzłów w ukrytej warstwie hello *ByRow*. Witaj typu obu **s** i **d** jest krotka liczb całkowitych o długości dwa. Koncepcyjnie **s** zakresów przez wszystkie pary liczb całkowitych z *0 < = s [0] < 10* i *0 < = s[1] < 20*, i **d** zakresów przez wszystkie pary liczb całkowitych, z *0 < = [0] d < 10* i *0 < = d[1] < 12*. 
* Na powitania prawej stronie powitania wyrażenie predykatu jest warunek. W tym przykładzie dla każdej wartości **s** i **d** tak, aby hello wynikiem warunku jest PRAWDA, to krawędzi, z węzła warstwy docelowej toohello węzła hello źródło warstwy. W związku z tym tego wyrażenia filtru wskazuje pakietu hello obejmuje połączenie z węzła hello zdefiniowane przez **s** zdefiniowane przez węzeł toohello **d** we wszystkich przypadkach, gdy s [0] jest równy tood [0].  

Opcjonalnie można określić zestaw wag dla filtrowanego pakietu. Witaj wartość hello **wagi** atrybut musi być krotki liczącej zmiennoprzecinkowych wartości o długości, która zastępuje hello liczbę połączeń zdefiniowanych przez hello pakietu. Domyślnie generowany losowo wagi.  

Wartości wag są pogrupowane według indeksu węzła docelowego hello. Oznacza to, że jeśli hello pierwszy węzeł docelowy jest połączony trwało węzły źródłowe hello najpierw *K* elementy hello **wagi** hello wag dla hello pierwszy węzeł docelowy, w kolejności indeksu źródła są spójnej kolekcji. powitalne samo dotyczy hello pozostałych węzłów docelowego.  

Wagi toospecify możliwe jest bezpośrednio jako wartości stałych. Na przykład jeśli znasz wag hello wcześniej, można je określić jako stałe przy użyciu tej składni:

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>Pakiety convolutional
Dane szkoleniowe powitania po jednorodnych struktury convolutional połączeń są toolearn często używane funkcje wysokiego poziomu hello danych. Na przykład w obrazie, audio i wideo, danych przestrzennych lub danych czasowych wymiary może być dość uniform.  

Pakiety convolutional stosować prostokątne **jądra** który są przesuwać za pośrednictwem hello wymiarów. Zasadniczo każda jądra definiuje zestaw wagi stosowane w lokalnym klubów, tooas określonego **aplikacji jądra**. Każda aplikacja jądra odpowiada tooa węzła w hello źródło warstwy, która jest hello określonego tooas **centralnej węzła**. Witaj wagi jądra są współużytkowane przez wiele połączeń. W pakiecie convolutional, każdy jądra jest prostokątny i wszystkie aplikacje jądra są takie same hello rozmiar.  

Pakiety convolutional obsługuje hello następujące atrybuty:

**InputShape** definiuje wymiary hello hello źródło warstwy hello celów tej convolutional pakietu. Witaj, wartość musi być krotka dodatnie liczby całkowite. Hello iloczyn liczb całkowitych hello musi być równa hello liczby węzłów w warstwie źródła hello, ale w przeciwnym razie nie jest konieczne wymiarach hello toomatch zadeklarowany hello źródło warstwy. Hello długość to tuple staje się hello **argumentów** wartość hello convolutional pakietu. (Zwykle argumentów oznacza toohello liczbę argumentów lub argumentów operacji, które można wykonać funkcji).  

kształt hello toodefine i lokalizacje jądra hello używać atrybutów hello **KernelShape**, **Stride**, **Padding**, **LowerPad**, i **UpperPad**:   

* **KernelShape**: (wymagane) definiuje hello wymiary poszczególnych jądra dla hello convolutional pakietu. wartość Hello musi być krotka dodatnie liczby całkowite o długości, która jest równa argumentów hello hello pakietu. Każdy element tej spójnej kolekcji musi być nie większy niż hello odpowiadającego składnika **InputShape**. 
* **STRIDE**: (opcjonalnie) hello definiuje przedłużanie krok rozmiary konwolucji hello (rozmiar krok dla każdego wymiaru), jest hello odległość między węzłami centralnej hello. wartość Hello musi być krotka dodatnie liczby całkowite o długości, która jest argumentów hello hello pakietu. Każdy element tej spójnej kolekcji musi być nie większy niż hello odpowiadającego składnika **KernelShape**. Wartość domyślna Hello to krotka z wszystkich składników tooone takie same. 
* **Udostępnianie**: (opcjonalnie) definiuje hello wagi udostępniania dla każdego wymiaru konwolucji hello. wartość Hello może być pojedynczą wartością logiczną lub krotka z wartościami logicznymi o długości, która jest argumentów hello hello pakietu. Pojedynczą wartość logiczną jest rozszerzona toobe krotki o długości poprawne hello ze wszystkimi składnikami toohello równa określonej wartości. Witaj, wartość domyślna to spójnej kolekcji, która składa się ze wszystkich wartości True. 
* **MapCount**: (opcjonalnie) definiuje hello liczbę funkcji mapy dla hello convolutional pakietu. wartość Hello może być jednym dodatnią liczbą całkowitą lub krotka dodatnie liczby całkowite o długości, która jest argumentów hello hello pakietu. Jedną wartość całkowitą rozszerzony toobe krotki o długości poprawne hello z pierwszego toohello równy hello składniki określona wartość, a wszystkie pozostałe składniki tooone równy hello. Witaj domyślna wartość to jeden. Hello łączna liczba map funkcji jest produktem hello hello składników hello spójnej kolekcji. Hello factoring tej liczby całkowitej między składnikami hello określa sposób grupowania wartości mapy funkcji hello w węzłach docelowego hello. 
* **Wagi**: (opcjonalnie) definiuje hello początkowej wag dla hello pakietu. Witaj, wartość musi być krotki liczącej zmiennoprzecinkowych wartości o długości, która jest hello liczby jądra razy hello wagi na jądra, zgodnie z definicją w dalszej części tego artykułu. losowo generowane są Hello domyślnych wag.  

Istnieją dwa zestawy właściwości sterujące dopełnienie właściwości hello są wzajemnie:

* **Dopełnienie**: (opcjonalnie) określa, czy dane wejściowe hello powinien dopełniane przy użyciu **domyślny schemat dopełnienie**. wartość Hello może być pojedynczą wartość logiczna lub może być krotka z wartościami logicznymi o długości, która jest argumentów hello hello pakietu. Pojedynczą wartość logiczną jest rozszerzona toobe krotki o długości poprawne hello ze wszystkimi składnikami toohello równa określonej wartości. Jeśli wartość hello wymiaru ma wartość PRAWDA, hello źródła logicznie jest uzupełniana w tym wymiarze z aplikacji jądra dodatkowe toosupport komórek o wartości zero, której hello centralnej węzłów hello imię i nazwisko jądra w tym wymiarze hello węzłów imię i nazwisko w tym wymiarze hello źródło warstwy. W związku z tym hello liczba węzłów "zastępczego" każdego wymiaru jest ustalany automatycznie, toofit dokładnie *(InputShape [d] - 1) / Stride [d] + 1* jądra do hello dopełniane źródło warstwy. Jeśli wartość hello wymiaru ma wartość False, powitalne jądra są zdefiniowane tak, aby hello liczbę węzłów na każdej stronie, które pozostało limit hello takie same (w górę różnica tooa 1). Hello wartość domyślna tego atrybutu jest krotka z wszystkich składników tooFalse takie same.
* **UpperPad** i **LowerPad**: (opcjonalnie) Podaj większą kontrolę nad hello ilość toouse dopełnienia. **Ważne:** te atrybuty mogą być definiowane w przypadku i tylko wtedy, gdy hello **Padding** właściwość powyżej jest ***nie*** zdefiniowane. Witaj wartości powinny być wyliczaną krotki o długości będących argumentów hello hello pakietu. Jeśli te atrybuty są określone, dodawania węzłów "zastępczego" toohello dolnej i górny końce każdego wymiaru hello wejściowych warstwy. Hello liczba węzłów dodany toohello dolnej i górnej kończy się każdego wymiaru jest określany przez **LowerPad**[i] i **UpperPad**[i] odpowiednio. muszą być spełnione tooensure że jądra odpowiadają tylko za "rzeczywiste" węzły i węzłów nie zbyt "zastępczego" hello następujące warunki:
  * Każdy składnik **LowerPad** musi być ściśle mniejsza niż KernelShape [d] / 2. 
  * Każdy składnik **UpperPad** musi być większa niż KernelShape [d] / 2. 
  * Wartość domyślna Hello tych atrybutów to krotka z wszystkich składników too0 takie same. 

Ustawienie Hello **Padding** = true umożliwia odpowiednio dużo uzupełnienie jest hello tookeep "center" hello jądra wewnątrz hello "w rzeczywistym" danych wejściowych. Spowoduje to zmianę matematyczne hello nieco dla przetwarzania hello rozmiar danych wyjściowych. Ogólnie rzecz biorąc, hello output rozmiar *D* jest obliczana jako *D = (I - K) / S + 1*, gdzie *I* rozmiar wejściowe hello *K* rozmiar jądra hello *S* jest hello stride i  */*  jest dzielenie liczby całkowitej (round w kierunku zera). Jeśli ustawisz UpperPad = [1, 1], rozmiar danych wejściowych hello *I* jest skutecznie 29 i w związku z tym *D = (29-5) / 2 + 1 = 13*. Jednakże, gdy **dopełnienie** zasadniczo = true, *I* pobiera upadku przez *K - 1*; dlatego *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*. Określenie wartości **UpperPad** i **LowerPad** uzyskać większą kontrolę nad hello dopełnienie niż w przypadku należy po prostu zestaw **Padding** = true.

Aby uzyskać więcej informacji o sieciach convolutional i aplikacjach zobacz następujące artykuły:  

* [http://deeplearning.NET/Tutorial/lenet.HTML](http://deeplearning.net/tutorial/lenet.html)
* [http://Research.microsoft.com/pubs/68920/icdar03.PDF](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://People.csail.mit.edu/jvb/Papers/cnn_tutorial.PDF](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>Korzystanie z puli pakietów
A **buforowanie pakietu** stosuje podobne łączności tooconvolutional geometry, ale używa wstępnie zdefiniowane funkcje toosource węzeł wartości tooderive hello docelowego węzła wartości. W związku z tym korzystanie z puli pakietów ma bez trainable stanu (wag lub odchyleń). Buforowanie obsługi pakietów hello wszystkie atrybuty convolutional z wyjątkiem **udostępniania**, **MapCount**, i **wagi**.  

Zazwyczaj jądra hello podsumowane według sąsiadujących jednostki buforowania nie pokrywają się. Jeśli krok [d] jest równy tooKernelShape [d] w każdego wymiaru, warstwy hello uzyskane jest hello tradycyjnych lokalnego buforowania warstwy, która jest często stosowanych w convolutional sieci neuronowej. Każdy węzeł docelowy oblicza maksymalną hello lub średniej hello działań hello jego jądra hello źródło warstwy.  

Witaj poniższy przykład przedstawia buforowania pakietu: 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* Liczba argumentów Hello hello pakietu wynosi 3 (hello długości krotek hello **InputShape**, **KernelShape**, i **Stride**). 
* Witaj liczba węzłów w warstwie źródła hello jest *5 * 24 * 24 = 2880*. 
* To tradycyjnej warstwy buforowania lokalnego, dlatego **KernelShape** i **Stride** są takie same. 
* Hello liczba węzłów w warstwie docelowego hello jest *5 * 12 * 12 = 1440*.  

Aby uzyskać więcej informacji na temat warstwy buforowania zobacz następujące artykuły:  

* [http://www.cs.Toronto.edu/~hinton/absps/imagenet.PDF](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (sekcji 3.4)
* [http://CS.nyu.edu/~koray/Publis/lecun-iscas-10.PDF](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://CS.nyu.edu/~koray/Publis/jarrett-iccv-09.PDF](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>Pakiety normalizacji odpowiedzi
**Odpowiedź normalizacji** jest schemat normalizacji lokalnej, która została wprowadzona przez Geoffrey Hinton i inni, w dokumencie hello [ImageNet Classiﬁcation z głębokie sieci neuronowe Convolutional](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf). Normalizacji odpowiedzi jest generalizacji tooaid używanych w sieci neuronowej. Po jednej neuronu jest uruchamiane na poziomie bardzo duże aktywacji, warstwy normalizacji lokalnego odpowiedzi pomija poziomu aktywacji hello hello otaczające grupy neuronów. Odbywa się przy użyciu trzech parametrów (***α***, ***poziom***, i ***k***) i struktura convolutional (lub otoczenie kształt). Co neuronu w warstwie docelowego hello ***y*** odpowiada neuronu tooa ***x*** hello źródło warstwy. Witaj poziomu aktywacji ***y*** jest określany przez hello następującej formuły, gdzie ***f*** poziom aktywacji hello neuronu, i ***Nx*** hello jądra (lub zestaw hello, który zawiera hello grupy neuronów w otoczeniu hello z ***x***), zgodnie z definicją w następującej struktury convolutional hello:  

![][1]  

Pakiety normalizacji odpowiedzi obsługuje wszystkie atrybuty convolutional hello z wyjątkiem **udostępniania**, **MapCount**, i **wagi**.  

* Jeśli jądra hello zawiera grupy neuronów w hello sam Mapuj jako ***x***, schemat normalizacji hello jest określony tooas **sam mapy normalizacji**. toodefine sam mapy normalizacji współrzędnych pierwszy hello **InputShape** musi mieć wartość hello 1.
* Jeśli jądra hello zawiera grupy neuronów w hello tej samej pozycji przestrzennych jako ***x***, ale grupy hello neuronów inne mapy, schemat normalizacji hello jest wywoływana **w poprzek mapuje normalizacji**. Ten typ odpowiedzi normalizacji implementuje formę penetracji niemożność wykonania przez typ hello w rzeczywistych grupy neuronów, tworzenie konkurencji poziomów big aktywacji wśród wyjść neuronu obliczonych na różnych mapy. toodefine między mapuje normalizacji, współrzędnych pierwszy hello musi być liczbą całkowitą więcej niż jeden oraz nie większa niż liczba hello map i rest hello współrzędnych hello musi mieć wartość hello 1.  

Ponieważ pakiety normalizacji odpowiedzi zastosować wstępnie zdefiniowanych toosource węzeł wartości toodetermine hello docelowego węzła wartością funkcji, mają one żadnego trainable stanu (wag lub odchyleń).   

**Alert**: hello węzłów w warstwie docelowego hello odpowiada tooneurons, które są węzłami centralnej hello hello jądra. Na przykład, jeśli KernelShape [d] jest nieparzysta, następnie *KernelShape [d] / 2* odpowiada toohello centralnej jądra węzła. Jeśli *KernelShape [d]* jest parzysta, węzeł centralnej hello jest na *KernelShape [d] / 2-1*. W związku z tym jeśli **Padding**[d] ma wartość FAŁSZ, najpierw hello i hello ostatnio *KernelShape [d] / 2* węzły nie mają odpowiadających im węzłów w warstwie docelowego hello. tooavoid tej sytuacji, zdefiniuj **Padding** jako [true ma wartość true, true,...].  

Ponadto toohello cztery atrybuty opisanego wcześniej pakiety normalizacji odpowiedzi również hello pomocy technicznej następujące atrybuty:  

* **Alpha**: (wymagane) określa wartość zmiennoprzecinkowa, która odpowiada za***α*** hello poprzedniej formuły. 
* **W wersji beta**: (wymagane) określa wartość zmiennoprzecinkowa, która odpowiada za***poziom*** hello poprzedniej formuły. 
* **Przesunięcie**: Określa (opcjonalnie) wartość zmiennoprzecinkowa, która odpowiada za***k*** hello poprzedniej formuły. Domyślnie too1.  

Witaj poniższym przykładzie zdefiniowano pakietu normalizacji odpowiedzi, za pomocą tych atrybutów:  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* warstwa źródła Hello zawiera pięć maps, każdy z wymiarów aof 12 x 12, sumowanie w węzłach 1440. 
* Witaj wartość **KernelShape** wskazuje, że jest tej samej warstwie normalizacji mapy, gdzie otoczenie hello jest prostokąt 3 x 3. 
* Witaj wartość domyślną **Padding** ma wartość False, w związku z tym warstwy docelowej hello ma tylko 10 węzłów w każdego wymiaru. tooinclude jednego węzła w hello docelowego warstwy, która odpowiada tooevery węzła w warstwie źródła hello, Dodaj uzupełnienie = [true, true, true]; i zmień rozmiar hello RN1 zbyt [5, 12, 12].  

## <a name="share-declaration"></a>Deklaracja udziału
NET # obsługuje opcjonalnie Definiowanie kilka pakietów o wagach udostępnionego. może być udostępniony Hello wagi żadnych dwa pakiety, jeśli ich struktur są takie same hello. Witaj składni definiuje pakiety o wagach udostępnionego:  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

Na przykład hello następujące oświadczenie udziału określa hello nazwy warstw, wskazującą, czy należy udostępnić zarówno wagi i odchyleń:  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* Funkcje wejściowych Hello są dzielone na taki sam rozmiar warstwy wejściowego. 
* Witaj ukryte warstwy należy obliczyć wyższej poziomu funkcji na dwóch warstwach wejściowych hello. 
* Deklaracja udziału Hello Określa, że *H1* i *H2* musi być obliczonych hello tak samo ich odpowiednich danych wejściowych.  

Alternatywnie to może być określony z dwa osobne deklaracje udziału w następujący sposób:  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

Krótka forma hello można użyć tylko w przypadku warstwy hello zawierać pojedynczy pakiet. Ogólnie rzecz biorąc jest możliwe udostępnianie tylko wtedy, gdy odpowiednia struktura hello jest taki sam, co oznacza, że hello sam rozmiar, tym samym convolutional geometry i tak dalej.  

## <a name="examples-of-net-usage"></a>Przykłady użycia Net #
Ta sekcja zawiera przykłady korzystania z Net # warstwy tooadd ukryte zdefiniować sposób hello warstwy ukryte interakcji z innych warstw i kompilacji convolutional sieci.   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>Zdefiniuj proste niestandardowe sieci neuronowej: przykładu "Hello World"
Tym prostym przykładzie pokazano, jak toocreate a neuronowej sieci modelu, która zawiera jedną warstwę ukryte.  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

przykład Witaj przedstawiono niektóre podstawowe polecenia w następujący sposób:  

* Witaj pierwszy wiersz definiuje warstwę wejściowych hello (o nazwie *danych*). Jeśli używasz hello **automatycznie** — słowo kluczowe, sieci neuronowej hello automatycznie zawiera wszystkie kolumny funkcji w przykładach wejściowych hello. 
* Witaj drugi wiersz tworzy hello ukrytej warstwie. Nazwa Hello *H* przypisano ukrytej warstwie toohello, którego węzły 200. Ta warstwa to warstwa wejściowych pełni połączonych toohello.
* trzeci wiersz Hello definiuje warstwę danych wyjściowych hello (o nazwie *O*), który zawiera 10 węzłów wyjściowych. Jeśli sieć neuronowa hello jest używany do klasyfikacji, istnieje jeden węzeł danych wyjściowych dla klasy. Witaj — słowo kluczowe **sigmoid** oznacza, że funkcja dane wyjściowe hello zastosowane toohello warstwy danych wyjściowych.   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>Zdefiniuj wielu warstw ukrytych: przykład vision komputera
Witaj poniższym przykładzie pokazano, jak toodefine nieco bardziej skomplikowane sieci neuronowej z wielu warstw ukrytych niestandardowych.  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

W tym przykładzie przedstawiono kilka funkcji hello sieci neuronowe specyfikacji języka:  

* Struktura Hello ma dwie warstwy wejściowych, *pikseli* i *metadanych*.
* Witaj *pikseli* warstwa jest warstwą źródła dla pakietów dwa połączenia, z warstwami docelowego *ByRow* i *ByCol*.
* Witaj warstwy *zebrać* i *wynik* są warstwy docelowej w wielu pakietów połączenia.
* Warstwa danych wyjściowych Hello, *wynik*, to warstwa docelowego w dwóch pakietów połączenia; jedna z hello drugi poziom ukryte (zbieranie) jako warstwę docelową i hello drugiej warstwy wejściowych hello (metadanymi) jako warstwy docelowej.
* Witaj warstwy ukryte *ByRow* i *ByCol*, określ filtrowane łączności za pomocą wyrażeń predykatu. Dokładnie hello węzła w *ByRow* w [x, y] jest toohello połączonych węzłów w *pikseli* , która ma x współrzędnych, pierwszy hello pierwszego indeksu współrzędnych toohello równy węzła. Podobnie hello w węźle *ByCol w [x, y] jest toohello połączonych węzłów _Pixels* , która ma hello drugi indeks współrzędnych w ramach jednej współrzędnych drugiego węzła hello, y.  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>Definiowanie sieci convolutional wieloklasowej klasyfikacji: przykład rozpoznawanie cyfr
Definicja Hello powitania po sieci jest zaprojektowana toorecognize liczby i zastosowano niektórych zaawansowanych technik dostosowywania sieci neuronowej.  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* Struktura Hello zawiera jedną warstwę wejściowych, *obrazu*.
* Witaj — słowo kluczowe **convolve** wskazuje, że hello warstwy o nazwie *Conv1* i *Conv2* są convolutional warstwy. Każdy z tych deklaracji warstwy następuje listę atrybutów konwolucji hello.
* Witaj net ma trzeciego ukryte warstwy, *Hid3*, która jest w pełni połączone toohello drugi ukrytej warstwie, *Conv2*.
* Warstwa danych wyjściowych Hello, *cyfrę*, jest połączony tylko toohello trzeci ukrytej warstwie, *Hid3*. Witaj — słowo kluczowe **wszystkie** wskazuje tej warstwy danych wyjściowych hello podłączona zbyt*Hid3*.
* Witaj argumentów konwolucji hello jest trzy (hello długości krotek hello **InputShape**, **KernelShape**, **Stride**, i **udostępniania**). 
* Liczba Hello wag na jądra jest *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26. Lub 26 * 50 = 1300*.
* Węzły hello w każdej warstwie ukryte można obliczyć w następujący sposób:
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[(13 – 5) = 1] / 2 + 1 = 5. 
  * **NodeCount**\[2] (13 – 5) = / 2 + 1 = 5. 
* Hello łączna liczba węzłów, może zostać obliczona przy użyciu hello zadeklarowany wymiarach hello warstwy, [50, 5, 5], w następujący sposób:  ***MapCount** * **NodeCount** \[ 0] * **NodeCount**\[1] * **NodeCount**\[10 * 5 * 5 * 5 = 2]*
* Ponieważ **udostępniania**[d] ma wartość FAŁSZ tylko w przypadku *d == 0*, liczba hello jądra jest  ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*. 

## <a name="acknowledgements"></a>Potwierdzeń
Hello Net # — język dostosowywania hello architektury sieci neuronowej został opracowany przez firmę Microsoft przez Shon Katzenberger (architektów, Machine Learning) i Alexey Kamenev (inżynier oprogramowania, Microsoft Research). Jest ona używana wewnętrznie do machine learning projektów i aplikacje od analytics tootext wykrywania obrazu. Aby uzyskać więcej informacji, zobacz [sieci Neuronowej na uczenie Maszynowe Azure — wprowadzenie tooNet #](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

