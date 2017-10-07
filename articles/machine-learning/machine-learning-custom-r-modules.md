---
title: "aaaAuthor niestandardowych modułów R w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Szybki start do tworzenia niestandardowych modułów R w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>Tworzenie niestandardowych modułów R w usłudze Azure Machine Learning
W tym temacie opisano sposób tooauthor i wdrażanie niestandardowego modułu R w usłudze Azure Machine Learning. Wyjaśniono, co to są niestandardowych modułów R i które pliki są używane toodefine je. Go pokazano, jak tooconstruct hello pliki, które definiują modułu i jak tooregister hello modułu do wdrożenia w obszarze roboczym uczenia maszynowego. Witaj elementy i atrybuty użyte w definicji hello niestandardowego modułu hello są następnie opisane bardziej szczegółowo. Jak również omówiono funkcje pomocnicze toouse, plików i wielu wyjść. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>Co to jest niestandardowego modułu R?
A **niestandardowego modułu** jest moduł zdefiniowane przez użytkownika, które mogą być przekazywane tooyour obszaru roboczego i wykonywane w ramach eksperymentu uczenia maszynowego Azure. A **niestandardowego modułu R** jest niestandardowy moduł, który wykonuje funkcję R zdefiniowane przez użytkownika. **R** to język programowania statystyczne obliczeniowych i grafiki, powszechnie używaną służące chi i dane dotyczące implementowania algorytmów. R jest obecnie hello języka tylko obsługiwane niestandardowe moduły, ale pomocy technicznej dla dodatkowych języków zostało zaplanowane w przyszłych wersjach.

Niestandardowe moduły mają **najwyższej jakości stan** w usłudze Azure Machine Learning w hello sensie, że mogą być używane tak samo jak inne modułu. Można je wykonać na inne moduły zawarte w opublikowanych eksperymenty lub wizualizacji. Mają kontrolę nad algorytm hello zaimplementowana przez moduł hello, hello toobe porty wejściowe i wyjściowe używany, hello parametry modelowania i innych różnych zachowanie w czasie wykonywania. Eksperymentu, która zawiera niestandardowe moduły mogą być publikowane na powitania Cortana Intelligence Gallery łatwe udostępnianie.

## <a name="files-in-a-custom-r-module"></a>Pliki w niestandardowego modułu R
Niestandardowego modułu R jest zdefiniowane przez plik zip, który zawiera co najmniej dwa pliki:

* A **plik źródłowy** implementującej hello R funkcji udostępnianych przez moduł hello
* **Pliku definicji XML** , który opisuje interfejs niestandardowego modułu hello

Dodatkowe pliki pomocnicze można również uwzględnić w pliku .zip hello, który zawiera funkcje, które są dostępne z hello niestandardowego modułu. Ta opcja została szczegółowo opisana w hello **argumenty** część sekcji odwołania hello **elementów w pliku definicji XML hello** poniższy przykład szybkiego startu hello.

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>Przykład Szybki Start: zdefiniuj, pakowanie i zarejestrować niestandardowego modułu R
W tym przykładzie pokazano, jak tooconstruct hello pliki wymagane przez niestandardowego modułu R, umieścić je w pliku zip, a następnie moduł hello rejestru w obszaru roboczego uczenia maszynowego. Witaj przykład zip pakietu i przykładowe pliki można pobrać z [CustomAddRows.zip Pobierz plik](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).

## <a name="hello-source-file"></a>plik źródłowy Hello
Rozważ przykład hello **wierszy dodać niestandardowe** moduł, który modyfikuje hello standardowej implementacji hello **Dodawanie wierszy** moduł używany tooconcatenate wierszy (uwagi) z dwóch zestawów danych (danych ramki). Standardowa Hello **Dodawanie wierszy** modułu dołącza wierszy hello końca hello drugi zestaw danych wejściowych toohello hello pierwszego wejściowego zestawu danych za pomocą hello `rbind` algorytmu. Witaj, dostosowane `CustomAddRows` funkcja podobnie akceptuje dwa zestawy danych, ale również zawierać parametr wymiany logiczną jako dodatkowe dane wejściowe. Jeśli parametr wymiany hello ustawiono zbyt**FALSE**, jego zwraca hello tego samego zestawu danych, ponieważ hello standardowej implementacji. Jeśli parametr wymiany hello jest jednak **TRUE**, funkcja hello dołącza wierszy pierwszego zestawu danych wejściowych toohello koniec hello drugi zestaw danych, zamiast tego. Witaj CustomAddRows.R pliku, który zawiera implementację hello hello R `CustomAddRows` funkcji udostępnianych przez hello **wierszy dodać niestandardowe** moduł ma hello następującego kodu języka R.

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a>Plik definicji XML Hello
tooexpose to `CustomAddRows` funkcji jako moduł usługi Azure Machine Learning pliku definicji XML muszą być tworzone toospecify jak hello **wierszy dodać niestandardowe** modułu powinien wyglądu i zachowania. 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


Jest toonote krytyczny, który hello wartość hello **identyfikator** atrybuty hello **dane wejściowe** i **Arg** elementów w pliku XML hello musi odpowiadać nazwy parametrów funkcji hello hello R kod w pliku CustomAddRows.R hello dokładnie: (*dataset1*, *dataset2*, i *wymiany* w przykładzie hello). Podobnie, hello wartość hello **punktu wejścia** atrybutu hello **języka** elementu muszą być zgodne hello nazwę funkcji hello w skrypcie hello R: (*CustomAddRows* w przykładzie hello). 

Z kolei hello **identyfikator** atrybutu hello **dane wyjściowe** elementu nie odpowiada tooany zmienne w skrypcie hello R. Jeśli wymagane jest więcej niż jedno wyjście, po prostu zwraca listę z funkcji hello R z wynikami umieszczone *w hello tej samej kolejności* jako **dane wyjściowe** elementy są zadeklarowane w pliku XML hello.

### <a name="package-and-register-hello-module"></a>Moduł hello pakietu i rejestrowanie
Zapisz te dwa pliki jako *CustomAddRows.R* i *CustomAddRows.xml* , a następnie zip hello dwa pliki ze sobą w *CustomAddRows.zip* pliku.

tooregister je w obszarze roboczym uczenia maszynowego, obszar roboczy tooyour Przejdź w hello Machine Learning Studio, kliknij przycisk hello **+ nowy** znajdującego się na dole hello i wybierz polecenie **modułu -> z pakietu ZIP** tooupload nowe Hello **wierszy dodać niestandardowe** modułu.

![Przekaż Zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

Witaj **wierszy dodać niestandardowe** modułu jest teraz gotowy toobe dostęp do eksperymentów uczenia maszynowego.

## <a name="elements-in-hello-xml-definition-file"></a>Elementy w pliku definicji XML hello
### <a name="module-elements"></a>Moduł elementów
Witaj **modułu** element jest używany toodefine niestandardowego modułu w pliku XML hello. Można zdefiniować wiele modułów w jednym pliku XML przy użyciu wielu **modułu** elementów. Każdy moduł w obszarze roboczym musi mieć unikatową nazwę. Zarejestruj niestandardowego modułu z hello sama nazwę istniejącej niestandardowego modułu i jego zastępuje istniejący moduł hello hello nową. Niestandardowe moduły można jednak zarejestrowany hello sama nazwa jak istniejący moduł usługi Azure Machine Learning. Jeśli tak, pojawią się one w hello **niestandardowy** kategorii hello palety modułów.

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


W ramach hello **modułu** elementu, można określić dwa dodatkowe elementy opcjonalne:

* **właściciela** element, który jest osadzony w hello module  
* **opis** element zawierający tekst, który jest wyświetlany w szybką pomoc dla modułu hello i po umieszczeniu na powitania modułu w hello Machine Learning w interfejsie użytkownika.

Zasady ograniczeń znaków w elementach modułu hello:

* Witaj wartość hello **nazwa** atrybutu w hello **modułu** element nie może przekraczać 64 znaków. 
* Witaj zawartości hello **opis** element nie może przekraczać 128 znaków.
* Witaj zawartości hello **właściciela** element nie może przekraczać 32 znaków.

Moduł wyniki mogą być deterministyczna lub nondeterministic.* * Domyślnie, wszystkie moduły są traktowane jako toobe deterministyczna. Oznacza to mając niezmiennych zestaw parametrów wejściowych i danych, modułu hello powinien zwrócić hello takie same wyniki eacRAND lub czas functionh, który jest uruchomiony. To zachowanie, Azure Machine Learning Studio zwracające tylko moduły oznaczona jako deterministyczna, jeśli parametr lub danych wejściowych hello została zmieniona. Zwracania wyników hello w pamięci podręcznej udostępnia znacznie szybsze wykonywanie eksperymentów.

Brak funkcji, które są niedeterministyczne, takich jak RAND lub funkcji, która zwraca hello bieżącą datę lub godzinę. Jeśli niedeterministyczna funkcja korzysta z modułu, można określić tego modułu hello jest deterministyczna przez ustawienie opcjonalne hello **isDeterministic** atrybutu zbyt**FALSE**. Dzięki temu, że ten moduł hello jest ponownie uruchamiany przy każdym uruchomieniu eksperymentu hello, nawet jeśli hello wejścia modułu i parametrów nie uległy zmianie. 

### <a name="language-definition"></a>Język definicji
Witaj **języka** elementu w pliku definicji XML jest używane toospecify hello niestandardowego modułu języka. Obecnie R jest hello tylko obsługiwanego języka. Witaj wartość hello **sourceFile** atrybutu musi być nazwą hello hello R zawierający toocall funkcja powitania po uruchomieniu hello modułu. Ten plik musi być częścią pakietu zip hello. Witaj wartość hello **punktu wejścia** atrybut jest hello nazwę wywoływanej funkcji hello i musi być zgodna z prawidłową funkcji zdefiniowanej przy w pliku źródłowym hello.

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>Porty
Witaj porty wejściowe i wyjściowe dla niestandardowego modułu są określone w elementach podrzędnych hello **porty** sekcja pliku definicji XML hello. kolejność Hello tych elementów określa hello układu doświadczonym (UX) przez użytkowników. pierwszym elementem podrzędnym Hello **wejściowych** lub **dane wyjściowe** hello na liście **porty** element pliku XML hello staje się hello lewej portu wejściowego w hello Machine Learning UX.
Każdy wejściowy i port wyjściowy może być opcjonalny **opis** element podrzędny, który określa hello tekst wyświetlany, gdy Przesuń wskaźnik myszy hello za pośrednictwem portu hello w hello Machine Learning w interfejsie użytkownika.

**Porty reguły**:

* Maksymalna liczba **porty wejściowe i wyjściowe** to 8 dla każdego.

### <a name="input-elements"></a>Elementów wejściowych
Porty wejściowe pozwalają toopass danych tooyour R funkcji i obszaru roboczego. Witaj **typy danych** obsługiwanych dla porty wejściowe są następujące: 

**Element DataTable:** tego typu jest przekazywana funkcja tooyour R jako data.frame. W rzeczywistości żadnych typów (na przykład plików CSV lub pliki ARFF), które są obsługiwane przez uczenia maszynowego i które są zgodne z **DataTable** są automatycznie data.frame tooa przekonwertowany. 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

Witaj **identyfikator** atrybut skojarzony z poszczególnymi **DataTable** port wejściowy musi mieć unikatową wartość i wartość ta musi odpowiadać odpowiadającego nazwany parametr w funkcji R.
Opcjonalne **DataTable** portów, które nie są przekazywane jako dane wejściowe w eksperymencie ma wartość hello **NULL** funkcja przekazany toohello R i zip opcjonalne porty są ignorowane, jeśli hello danych wejściowych nie jest połączona. Witaj **isOptional** atrybutu jest opcjonalny w przypadku obu hello **DataTable** i **Zip** typów i jest *false* domyślnie.

**ZIP:** niestandardowe moduły można zaakceptować plik zip jako dane wejściowe. Tych danych wejściowych jest rozpakowane do katalogu roboczego hello R funkcji

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

Dla niestandardowych modułów R identyfikator hello portu Zip ma toomatch parametrów funkcji hello R. Jest to spowodowane plik zip hello jest automatycznie wyodrębnionego toohello R katalog roboczy.

**Reguły wprowadzania:**

* Witaj wartość hello **identyfikator** atrybutu hello **dane wejściowe** element musi być prawidłową nazwą zmiennej języka R.
* Witaj wartość hello **identyfikator** atrybutu hello **dane wejściowe** element nie może być dłuższa niż 64 znaki.
* Witaj wartość hello **nazwa** atrybutu hello **dane wejściowe** element nie może być dłuższa niż 64 znaki.
* Witaj zawartości hello **opis** element nie może być dłuższa niż 128 znaków
* Witaj wartość hello **typu** atrybutu hello **dane wejściowe** element musi być *Zip* lub *DataTable*.
* Witaj wartość hello **isOptional** atrybutu hello **dane wejściowe** element nie jest wymagana (i jest *false* domyślnie, gdy nie określono); ale jeśli jest określona, musi ona być *true* lub *false*.

### <a name="output-elements"></a>Elementy danych wyjściowych
**Standardowe dane wyjściowe porty:** porty dane wyjściowe są mapowane toohello wartości zwracanych z funkcji R, które mogą być następnie używane przez kolejne modułów. *Element DataTable* jest typ portu tylko standardowe wyjście hello obecnie obsługiwane. (Obsługę *uczących* i *przekształca* nadchodzi.) A *DataTable* danych wyjściowych jest zdefiniowany jako:

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

Dla danych wyjściowych w niestandardowych modułów R, hello wartość hello **identyfikator** atrybut nie ma w skrypcie hello R toocorrespond przy użyciu innych, ale musi być unikatowa. Dla wyjścia pojedynczy moduł, musi być hello wartość zwrócona przez funkcję hello R *data.frame*. W kolejność toooutput więcej niż jeden obiekt obsługiwany typ danych, hello odpowiednie dane wyjściowe porty muszą toobe określony w pliku definicji XML hello i hello obiekty wymagają toobe zwracane w postaci listy. obiekty danych wyjściowych Hello są przypisywane porty toooutput z tooright po lewej stronie, odzwierciedlający hello kolejność, w którym obiekty hello są umieszczane w hello zwrócił listę.

Na przykład, jeśli chcesz toomodify hello **niestandardowe Dodawanie wierszy** toooutput modułu hello oryginalnego dwóch zestawów danych, *dataset1* i *dataset2*, ponadto przyłączone toohello nowego zestaw danych, *zestawu danych*, (w kolejności od lewej tooright jako: *dataset*, *dataset1*, *dataset2*), następnie zdefiniuj hello dane wyjściowe porty w pliku CustomAddRows.xml hello w następujący sposób:

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


I zwróć hello listy obiektów na liście w kolejności poprawne hello w "CustomAddRows.R":

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**Wizualizacja danych wyjściowych:** można także określić port wyjściowy typu *wizualizacji*, który zawiera dane wyjściowe hello hello R grafiki urządzenia i konsola danych wyjściowych. Ten port nie jest częścią dane wyjściowe funkcji hello R i nie zakłóca hello kolejność hello inne typy portów output. Dodaj wizualizacji portu toohello niestandardowe moduły tooadd **dane wyjściowe** element o wartości *wizualizacji* dla jego **typu** atrybutu:

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**Dane wyjściowe reguły:**

* Witaj wartość hello **identyfikator** atrybutu hello **dane wyjściowe** element musi być prawidłową nazwą zmiennej języka R.
* Witaj wartość hello **identyfikator** atrybutu hello **dane wyjściowe** element nie może być dłuższa niż 32 znaki.
* Witaj wartość hello **nazwa** atrybutu hello **dane wyjściowe** element nie może być dłuższa niż 64 znaki.
* Witaj wartość hello **typu** atrybutu hello **dane wyjściowe** element musi być *wizualizacji*.

### <a name="arguments"></a>Argumenty
Dodatkowe dane mogą być przekazywane toohello R funkcji za pośrednictwem modułu parametrów, które są zdefiniowane w hello **argumenty** elementu. Te parametry są wyświetlane w okienku po prawej stronie właściwości hello hello Machine Learning w interfejsie użytkownika w przypadku wybrania modułu hello. Argumenty mogą być dowolnego typu hello obsługiwane lub można utworzyć niestandardowe wyliczenie w razie potrzeby. Podobne toohello **porty** elementów **argumenty** elementy mogą mieć opcjonalny **opis** element, który określa hello tekst wyświetlany, gdy wskaźnik myszy hello za pośrednictwem hello Nazwa parametru.
Opcjonalne właściwości dla modułu, na przykład defaultValue minValue i maxValue można dodać argument tooany jako atrybuty tooa **właściwości** elementu. Prawidłowe właściwości hello **właściwości** elementu są zależne od typu argumentu hello i opisano z typami argumentów hello obsługiwane w następnej sekcji hello. Argumenty z hello **isOptional** właściwość zbyt**"true"** hello użytkownika tooenter wartość nie jest wymagana. Jeśli wartość nie zostanie podany toohello argument, następnie hello argument nie zostanie przekazany funkcję punktu wejścia toohello. Argumenty funkcji punktu wejścia hello, które są toobe opcjonalne muszą jawnie obsługiwany przez funkcję hello przypisane np. domyślna wartość NULL w definicji funkcji punktu wejścia hello. Opcjonalny argument będzie tylko wymuszać hello innych ograniczeń argumentu, tj. min lub max, jeśli wartość jest podana przez użytkownika hello.
Zgodnie z wejściami i wyjściami jest krytyczny, że parametrów hello mieć skojarzone z nimi wartości unikatowego identyfikatora. W naszym szybki start zostało przykład hello skojarzony identyfikator i parametru *wymiany*.

### <a name="arg-element"></a>ARG — element
Parametr modułu jest definiowana za pomocą hello **Arg** elementem podrzędnym hello **argumenty** sekcja pliku definicji XML hello. Jak hello elementy podrzędne w hello **porty** sekcji, hello kolejność parametrów na powitania **argumenty** sekcja definiuje układ hello w hello UX. Witaj parametry są wyświetlane od góry w dół w hello interfejsu użytkownika w hello sam porządek, w którym są zdefiniowane w pliku XML hello. obsługiwane przez usługi Machine Learning parametrów typów Hello są wyświetlane tutaj. 

**int** — parametr (32-bitowy) typu Liczba całkowita.

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *Opcjonalne właściwości*: **min**, **max**, **domyślne** i **isOptional**

**Podwójna** — parametr typu double.

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *Opcjonalne właściwości*: **min**, **max**, **domyślne** i **isOptional**

**wartość logiczna** — parametrem logicznym reprezentowanego przez pole wyboru w UX.

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *Opcjonalne właściwości*: **domyślne** — wartość false, gdy nie jest ustawiona

**ciąg**: ciąg standardowy

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *Opcjonalne właściwości*: **domyślne** i **isOptional**

**ColumnPicker**: parametr wybór kolumny. Ten typ renderowania w hello UX jako selektora kolumn. Witaj **właściwości** element jest używany tutaj toospecify identyfikator hello hello portu, z której są wybierane kolumny, której typ port docelowy hello musi być *DataTable*. wynik Hello hello kolumnę zaznaczenia jest przekazywana funkcja toohello R jako lista ciągów zawierająca nazwy kolumn hello wybrane. 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *Wymagane właściwości*: **portId** -dopasowań hello identyfikator elementu danych wejściowych z typem *DataTable*.
* *Opcjonalne właściwości*:
  
  * **allowedTypes** — filtry hello kolumny typów, z której można wybrać. Prawidłowe wartości to: 
    
    * numeryczne
    * Wartość logiczna
    * Podzielone na kategorie
    * Ciąg
    * Etykieta
    * Funkcja
    * Wynik
    * Wszystkie
  * **domyślne** -prawidłowy domyślny wybór selektor kolumn hello obejmują: 
    
    * Brak
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * Wszystkie

**Lista rozwijana**: listę wyliczany określone przez użytkownika (rozwijaną). elementy listy rozwijanej Hello są określone w hello **właściwości** przy użyciu elementu **elementu** elementu. Witaj **identyfikator** dla każdego **elementu** musi być unikatowa i prawidłową zmienną R. Witaj wartość hello **nazwa** z **elementu** służy jako tekst hello widoczny i wartość hello przekazywana funkcja toohello R.

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *Opcjonalne właściwości*:
  * **domyślne** — Witaj wartość dla właściwości domyślnej hello musi być zgodna z wartość jednego z hello **elementu** elementów.

### <a name="auxiliary-files"></a>Pliki pomocnicze
Każdego pliku, który znajduje się w pliku ZIP niestandardowego modułu jest toobe będzie dostępna do użycia w czasie wykonywania. Wszelkich struktur katalogów obecne są zachowywane. Oznacza to, że działa źródeł pliku hello sam lokalnie i w usłudze Azure Machine Learning na wykonanie. 

> [!NOTE]
> Zwróć uwagę, że wszystkie pliki zostały wyodrębnione too'src "katalogu, więc wszystkie ścieżki powinny mieć" src / "prefiks.
> 
> 

Na przykład chcesz tooremove wszystkie wiersze z NAs z hello zestawu danych, a także usunąć wszystkie zduplikowane wiersze przed wyprowadzanie go do CustomAddRows i zostały już zapisane funkcję R, która robi to w pliku RemoveDupNARows.R:

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
Może pobierać hello dodatkowego pliku RemoveDupNARows.R w hello CustomAddRows funkcji:

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

Następnie przekaż plik zip zawierający "CustomAddRows.R", "CustomAddRows.xml" i "RemoveDupNARows.R" jako niestandardowego modułu R.

## <a name="execution-environment"></a>Środowiska wykonawczego
środowiska wykonawczego Hello skryptu hello R używa hello tej samej wersji elementu R, co hello **wykonanie skryptu języka R** modułu i można Użyj hello same domyślne pakiety. Można również dodać dodatkowe pakiety tooyour niestandardowego modułu R przez włączenie ich do pakietu zip hello niestandardowego modułu. Wystarczy załadować je w skrypcie R tak jak w środowisku R. 

**Ograniczenia środowiska wykonawczego hello** obejmują:

* System plików nie trwała: pliki napisane po uruchomieniu hello niestandardowego modułu nie są zachowywane w wielu uruchomień hello tego samego modułu.
* Nie dostępu do sieci

