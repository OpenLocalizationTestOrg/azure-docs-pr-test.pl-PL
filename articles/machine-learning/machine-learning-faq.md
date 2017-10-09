---
title: "aaaAzure Machine Learning — często zadawane pytania (FAQ) | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do usługi Azure Machine Learning: odpowiedzi na często zadawane pytania dotyczące rozliczeń, możliwości i ograniczeń usługi w chmurze na potrzeby sprawnego modelowania predykcyjnego."
keywords: wprowadzenie do uczenia maszynowego,modelowanie predykcyjne,co to jest uczenie maszynowe
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Azure Machine Learning — często zadawane pytania: rozliczenia, możliwości, ograniczenia i pomoc techniczna
Przedstawione tutaj często zadawane pytania i odpowiedzi dotyczą usługi Azure Machine Learning, która jest usługą w chmurze przeznaczoną do tworzenia modeli predykcyjnych i rozwiązań operacyjnych za pośrednictwem usług sieci Web. Te często zadawane pytania Podaj pytania dotyczące sposobu toouse hello usługi, która obejmuje hello rozliczeń modelu, możliwości, ograniczeń i pomocy technicznej.

**Masz pytania, których nie możesz tu znaleźć?**

Usługa Azure Machine Learning ma forum w witrynie MSDN, gdzie członków społeczności nauki danych hello można zadawać pytania dotyczące usługi Azure Machine Learning. Zespół usługi Azure Machine Learning Hello monitoruje hello forum. Przejdź toohello [Azure Machine Learning Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch odpowiedzi lub toopost nowe pytanie własny.

## <a name="general-questions"></a>Pytania ogólne
**Co to jest Azure Machine Learning?**

Azure Machine Learning to w pełni zarządzana usługa, czy można użyć toocreate, testowanie, działania i zarządzanie rozwiązań z zakresu analiz predykcyjnych w chmurze hello. Wystarczy tylko przeglądarka, aby się zalogować, przekazać dane i natychmiast rozpocząć eksperymenty z uczeniem maszynowym. Modelowanie predykcyjne metodą „przeciągnij i upuść”, duża paleta modułów i biblioteka szablonów początkowych — wszystko to sprawia, że typowe zadania uczenia maszynowego można wykonywać prosto i szybko. Aby uzyskać więcej informacji, zobacz hello [Omówienie usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/). Learning toomachine wprowadzenie przedstawiająca kluczowe terminy i pojęcia dla [tooAzure wprowadzenie Machine Learning](machine-learning-what-is-machine-learning.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Co to jest Machine Learning Studio?**

Machine Learning Studio to środowisko robocze, do którego można uzyskiwać dostęp za pośrednictwem przeglądarki sieci Web. Usługa Machine Learning Studio udostępnia paletę modułów w interfejsem graficznym, która pomaga w utworzeniu end-to-end, przepływy pracy do analizy danych w formie hello eksperymentów.

Aby uzyskać więcej informacji o usłudze Machine Learning Studio, zobacz [What is Machine Learning Studio?](machine-learning-what-is-ml-studio.md) (Co to jest Machine Learning Studio?).

**Co to jest usługa Machine Learning API hello?**

Witaj usługa Machine Learning API umożliwia toodeploy modeli predykcyjnych, takich jak te, które są wbudowane w usłudze Machine Learning Studio, jako skalowalnych i odpornych, sieci web usługi. Witaj usług sieci web usługi Machine Learning API hello tworzy są interfejsów API REST, które zapewniają interfejs do komunikacji między aplikacjami zewnętrznymi i modelami analizy predykcyjnej.

Aby uzyskać więcej informacji, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

**Gdzie znajduje się lista klasycznych usług sieci Web? Gdzie można znaleźć wykaz nowych usług sieci Web (opartych na usłudze Azure Resource Manager)?**

Usługi sieci Web utworzony za pomocą hello klasycznego modelu i w sieci web usług wdrażania utworzone przy użyciu modelu wdrażania nowej usługi Azure Resource Manager hello są wymienione w hello [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/) portalu.

Usługi sieci web klasycznego znajdują się w [Machine Learning Studio](http://studio.azureml.net) na powitania **usług sieci Web** kartę.

## <a name="azure-machine-learning-questions"></a>Pytania dotyczące usługi Azure Machine Learning
**Co to są usługi sieci Web Azure Machine Learning?**

Usługi sieci Web Machine Learning zapewniają interfejs między aplikacją a modelem oceniania przepływu pracy usługi Machine Learning. Zewnętrznej aplikacji za pomocą usługi Azure Machine Learning toocommunicate model oceniania uczenia maszynowego przepływu pracy w czasie rzeczywistym. Tooa wywołania usługi sieci web uczenie maszynowe zwraca wyniki prognozowania tooan zewnętrznej aplikacji. toomake wywołania usługi sieci web tooa przekazać klucz interfejsu API, który został utworzony po wdrożeniu usługi sieci web hello. Usługa sieci Web Machine Learning korzysta z interfejsu REST — popularnej architektury w projektach programistycznych dla sieci Web.

Usługa Azure Machine Learning udostępnia dwa typy usług sieci Web:

* Odpowiedź na żądania usługi (RR): Małe opóźnienia wysoce skalowalna usługa, która zapewnia interfejs toohello modeli bezstanowych utworzeniu i wdrożeniu przy użyciu usługi Machine Learning Studio.
* Usługa wykonywania wsadowego (BES, Batch Execution Service): asynchroniczna usługa przeznaczona do oceniania partii rekordów danych.

Istnieje kilka sposobów tooconsume hello dostępu i interfejsu API REST hello usługi sieci web. Na przykład można napisać aplikację w języku C#, R lub Python za pomocą hello przykładowy kod, który jest generowany automatycznie podczas wdrażania usługi sieci web hello.

Witaj przykładowy kod jest dostępny na:
- Witaj Consume strony usługi sieci web hello w portalu usługi sieci Web systemu Azure Machine Learning hello
- Witaj strona pomocy interfejsu API w hello pulpit nawigacyjny usługi sieci web w usłudze Machine Learning Studio

Umożliwia także hello skoroszyt programu Microsoft Excel próbki, który jest tworzony automatycznie i jest dostępny na pulpicie nawigacyjnym usługi sieci web hello w usłudze Machine Learning Studio.

**Co to są tooAzure aktualizacji głównego hello Machine Learning?**

Aby hello najnowsze aktualizacje, zobacz [What's new in Azure Machine Learning](machine-learning-whats-new.md).

## <a name="machine-learning-studio-questions"></a>Pytania dotyczące usługi Machine Learning Studio
### <a name="import-and-export-data-for-machine-learning"></a>Importowanie i eksportowanie danych na potrzeby usługi Machine Learning
**Jakie źródła danych obsługuje usługa Machine Learning?**

Można pobrać danych tooa eksperymentu Machine Learning Studio na trzy sposoby:

- Przekazanie pliku lokalnego jako zestawu danych.
- Użyj modułu tooimport danych z usług danych w chmurze
- Zaimportowanie zestawu danych zapisanego w innym eksperymencie.

więcej informacji o toolearn obsługiwane formaty plików, zobacz [importowanie danych szkoleniowych do usługi Machine Learning Studio](machine-learning-data-science-import-data.md).

#### <a id="ModuleLimit"></a>Jak duży może hello być zestaw danych dla moich modułów?
Moduły w usłudze Machine Learning Studio obsługują zestawy danych o się too10 GB, zawierające gęsto upakowane dane typowe przypadki użycia. Jeśli moduł przyjmuje więcej niż jeden parametr wejściowy, hello 10 GB, wartość jest hello łączny rozmiar wszystkich wejściowych. Większe zestawy danych można przed pozyskaniem próbkować przy użyciu zapytań programu Hive lub usługi Azure SQL Database albo stosując przetwarzanie wstępne metodą uczenia przez liczenie.  

Witaj następujące typy danych można rozszerzyć toolarger zestawów danych w funkcji normalizacji i są ograniczone tooless niż 10 GB:

* Rozrzedzone
* Podzielone na kategorie
* Ciągi
* Dane binarne

Witaj następujące moduły są ograniczone toodatasets mniej niż 10 GB:

* Moduły polecania
* Moduł Synthetic Minority Oversampling Technique (SMOTE)
* Moduły skryptów: R, Python, SQL
* Moduły, w którym hello output rozmiar danych może być większy niż rozmiar danych wejściowych, na przykład przyłączenie lub Tworzenie skrótu funkcji
* Krzyżowe sprawdzanie poprawności, Hiperparametry modelu, Regresja porządkowa oraz Multiklasa jedna kontra wszystkie, gdy hello liczba iteracji jest bardzo duży

#### <a id="UploadLimit"></a>Jakie są limity hello danych przekazać?
W przypadku zestawów danych, które są większe niż kilka GB, przekazać dane tooAzure magazynów lub baza danych SQL Azure, lub użyj Azure HDInsight zamiast przekazywania bezpośrednio z pliku lokalnego.

**Czy mogę odczytywać dane z usługi Amazon S3?**

Jeśli masz niewielką ilość danych i chcesz tooexpose go za pomocą adresu URL HTTP, możesz użyć hello [i zaimportuj dane] [ import-data] modułu. W przypadku większych ilości danych, przenieść tooAzure magazynu najpierw, a następnie użyj hello [i zaimportuj dane] [ import-data] toobring modułu go do eksperymentu.
<!--

<SEE CLOUD DS PROCESS>
-->

**Czy istnieje wbudowana możliwość wprowadzania obrazów?**

Informacje na temat możliwości wprowadzania obrazu w hello [Import obrazów] [ image-reader] odwołania.

### <a name="modules"></a>Moduły
**Hello algorytmu, źródła danych, formatu danych lub operacji transformacji danych, które na nie znajduje się w usłudze Azure Machine Learning Studio. Jakie są moje opcje?**

Można przejść toohello [forum opinii użytkowników](http://go.microsoft.com/fwlink/?LinkId=404231) funkcji toosee żądań możemy śledzenia. Dodaj żądanie tooa głosowania, jeśli już Zażądano możliwości, którego szukasz. Jeśli nie istnieje możliwość hello, którego szukasz, Utwórz nowe żądanie. Można wyświetlić stan hello żądania zbyt na tym forum. Firma Microsoft ściśle Śledzimy tę listę i często aktualizować hello stan dostępności funkcji. Ponadto można użyć wbudowanych funkcji hello dla języków R i Python toocreate niestandardowych przekształceń w razie potrzeby.

**Czy mogę przenieść mój istniejący kod do środowiska usługi Machine Learning Studio?**

Tak, można przenieść istniejący kod R lub Python do usługi Machine Learning Studio, uruchomić go w hello sam eksperymentować uczących uczenie maszynowe Azure i wdrożyć rozwiązanie hello jako usługę sieci web za pomocą usługi Azure Machine Learning. Aby uzyskać więcej informacji, zobacz tematy [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md) (Rozszerzanie eksperymentu, korzystając z języka R) i [Execute Python machine learning scripts in Azure Machine Learning Studio](machine-learning-execute-python-scripts.md) (Wykonywanie skryptów uczenia maszynowego w języku Python w usłudze Azure Machine Learning Studio).

**Jest to możliwe toouse coś, takich jak [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine modelu?**

Nie, język PMML (Predictive Model Markup Language) nie jest obsługiwany. Można użyć niestandardowej R i Python code toodefine modułu.

**Jak wiele modułów mogę równolegle uruchomić w moim eksperymencie?**  

Można wykonywać zapasowej modułów toofour równolegle w eksperymencie.

### <a name="data-processing"></a>Przetwarzanie danych
**Istnieje możliwość toovisualize danych (poza wizualizacjami języka R) interakcyjnego w ramach eksperymentu hello?**

Kliknij przycisk hello wyjście danych hello toovisualize modułu oraz uzyskują statystyki.

**Podczas przeglądania wyników lub danych w przeglądarce, hello liczby wierszy i kolumn jest ograniczona. Dlaczego?**

Ponieważ dużych ilości danych może być wysyłane tooa przeglądarki, rozmiar danych jest ograniczona tooprevent spowolnieniem Machine Learning Studio. toovisualize hello wszystkich danych/wyników, jego lepsze toodownload hello danych i użyj programu Excel lub innego narzędzia.

### <a name="algorithms"></a>Algorytmy
**Jakie istniejące algorytmy są obsługiwane w środowisku usługi Machine Learning Studio?**

Usługa Machine Learning Studio udostępnia najnowocześniejsze algorytmy, takie jak skalowalne wzmocnione drzewa decyzyjne, bayesowskie systemy rekomendacji, głębokie sieci neuronowe i dżungle decyzyjne opracowywane w dziale badań firmy Microsoft. Dostępne są również skalowalne pakiety uczenia maszynowego typu open source, takie jak Vowpal Wabbit. Usługa Machine Learning Studio obsługuje algorytmy uczenia maszynowego na potrzeby binarnej i wieloklasowej klasyfikacji i regresji oraz klastrowania. Zobacz hello pełną listę [Machine Learning modułów][machine-learning-modules].

**Czy jest sugerowany automatycznie hello prawo Machine Learning algorithm toouse dla danych?**

Nie, ale Machine Learning Studio zawiera różne sposoby toocompare hello wyniki każdego toodetermine algorytm hello właściwy dla danego problemu.

**Czy istnieją jakiekolwiek wskazówki pobrania jednej algorytmu zamiast innego algorytmów hello podane?**

Zobacz [jak toochoose algorytm](machine-learning-algorithm-choice.md).

**Algorytmy hello podane są napisane w języku R lub Python?**

Nie, te algorytmy są w większości napisane w językach kompilowanych tooprovide lepszą wydajność.

**Są jakiekolwiek szczegóły dotyczące udostępnionych algorytmów hello?**

Hello dokumentacji udostępniono pewne informacje dotyczące algorytmów hello i dostrajanie parametrów są opisane toooptimize hello algorytmu do użycia.  

**Czy są dostępne jakieś rozwiązania do uczenia online?**

Nie. Obecnie jest obsługiwane tylko programowe ponowne trenowanie.

**Czy mogę zwizualizować warstwy modelu sieci Neuronowej hello przy użyciu modułu wbudowanego hello?**

Nie.

**Czy mogę tworzyć własne moduły w języku C# lub innym?**

Obecnie można używać tylko R toocreate nowe niestandardowe moduły.

### <a name="r-module"></a>Moduł R
**Jakie pakiety języka R są dostępne w usłudze Machine Learning Studio?**

Machine Learning Studio obsługuje ponad 400 R sieci CRAN pakietów dzisiaj, a Oto hello [bieżącą listę](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) wszystkich dostępnych pakietów. Zobacz też [rozszerzanie eksperymentu z R](machine-learning-extend-your-experiment-with-r.md) toolearn jak tooretrieve tę listę samodzielnie. Jeśli pakiet hello nie jest na liście, należy podać nazwę hello pakietu hello na powitania [forum opinii użytkowników](http://go.microsoft.com/fwlink/?LinkId=404231).

**Jest to możliwe toobuild R niestandardowego modułu?**

Tak. Zobacz temat [Author custom R modules in Azure Machine Learning](machine-learning-custom-r-modules.md) (Tworzenie niestandardowych modułów R w usłudze Azure Machine Learning).

**Czy dostępne jest środowisko REPL dla języka R?**

Nie, jest ma środowiska odczytu-Eval-drukowania-pętli (REPL) dla języka R w hello studio.

### <a name="python-module"></a>Moduł Python
**Jest to możliwe toobuild niestandardowego modułu Python?**

Aktualnie nie ale można użyć co najmniej jeden [wykonanie skryptu Python] [ python] tooget modułów hello takiego samego wyniku.

**Czy dostępne jest środowisko REPL dla języka Python?**

Można użyć hello notesów Jupyter w usłudze Machine Learning Studio. Aby uzyskać więcej informacji, zobacz temat [Manage experiment iterations in Machine Learning Studio](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx) (Zarządzanie iteracjami eksperymentów w usłudze Machine Learning Studio).

## <a name="web-service"></a>Usługa sieci Web
### <a name="retrain"></a>Ponowne próbkowanie
**W jaki sposób ponownie trenować modele usługi Azure Machine Learning programowo?**

Użyj hello ponownego trenowania interfejsów API. Aby uzyskać więcej informacji, zobacz temat [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md) (Ponowne trenowanie modeli uczenia maszynowego programowo). Przykładowy kod jest również dostępna w hello [Microsoft Azure Machine Learning demonstracji ponownego trenowania w](https://azuremlretrain.codeplex.com/).

### <a name="create"></a>Przycisk Utwórz
**Czy można wdrożyć modelu hello lokalnie lub w aplikacji, która nie ma połączenia internetowego?**

Nie.

**Czy istnieje opóźnienie bazowe oczekiwane dla wszystkich usługi sieci Web?**

Zobacz hello [limity subskrypcji platformy Azure](../azure-subscription-service-limits.md).

### <a name="use"></a>Użycie
**Kiedy należy toorun model predykcyjny jako usługę wykonywania wsadowego usługi odpowiedzi na żądanie?**

Hello usługę odpowiedzi na żądanie (RR) jest małe opóźnienia, wysokiej skali sieci web usługi, która jest używana tooprovide toostateless interfejsu modeli, które są tworzone i wdrażane ze środowiska eksperymenty hello. Witaj usługę wykonywania wsadowego (BES) to usługa, która asynchronicznie wyników partii rekordów danych. Hello danych wejściowych jest BES, takich jak dane wejściowe, która używa zasobów. Witaj podstawowa różnica polega na tym, że usługa BES odczytuje blok rekordów z różnych źródeł, takich jak magazynu obiektów Blob platformy Azure, Magazyn tabel Azure, baza danych SQL Azure, HDInsight (zapytanie hive) i źródła HTTP. Aby uzyskać więcej informacji, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

**Jak zaktualizować hello model dla usługi sieci web hello wdrożyć?**

tooupdate model predykcyjny dla już wdrożonej usługi, zmodyfikuj i uruchom ponownie eksperymentu hello użytą tooauthor i Zapisz hello trenowanego modelu. Po utworzeniu nowej wersji hello trenowanego modelu usługi Machine Learning Studio zapyta, czy ma tooupdate usługi sieci web. Aby uzyskać szczegółowe informacje o tym, jak tooupdate wdrożonej usługi sieci web, zobacz [wdrażanie usługi sieci web uczenie maszynowe](machine-learning-publish-a-machine-learning-web-service.md).

Umożliwia także hello Retraining interfejsów API.
Aby uzyskać więcej informacji, zobacz temat [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md) (Ponowne trenowanie modeli uczenia maszynowego programowo). Przykładowy kod jest również dostępna w hello [Microsoft Azure Machine Learning demonstracji ponownego trenowania w](https://azuremlretrain.codeplex.com/).

**Jak mogę monitorować moją usługę sieci Web wdrożoną w środowisku produkcyjnym?**

Po wdrożeniu modelu predykcyjnego można go monitorować z hello Azure classic portal (tylko usługi sieci web klasycznego) lub hello portal usługi sieci Web systemu Azure Machine Learning. Dla każdej wdrożonej usługi istnieje osobny pulpit nawigacyjny, w którym dostępne są informacje pozwalające na monitorowanie tej usługi. Aby uzyskać więcej informacji na temat toomanage usług wdrożonego w sieci web, zobacz temat [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md) i [Zarządzanie obszarem roboczym usługi Azure Machine Learning](machine-learning-manage-workspace.md).

**Jest to miejsce, w którym można zobaczyć hello dane wyjściowe moich usług RRS/BES?**

W przypadku usługi RRS odpowiedź usługi sieci web hello są jest zwykle gdzie zobaczyć wynik hello. Można go także zapisać tooAzure magazynu obiektów Blob. W przypadku usługi BES dane wyjściowe hello jest domyślnie zapisywane tooa obiektu blob. Można również napisać hello wyjście tooa bazy danych lub tabeli za pomocą hello [eksportowanie danych] [ export-data] modułu.

**Czy usługi sieci Web można tworzyć tylko z modeli utworzonych w usłudze Machine Learning Studio?**

Nie. Usługi sieci Web można również tworzyć bezpośrednio przy użyciu notesów Jupyter i programu RStudio.

**Gdzie można znaleźć informacje o kodach błędów?**

Listę kodów błędów i opisy zawiera temat [Machine Learning Module Error Codes](https://msdn.microsoft.com/library/azure/dn905910.aspx) (Kody błędów modułów usługi Machine Learning).

## <a name="scalability"></a>Skalowalność
**Co to jest skalowalność hello hello usługi sieci web?**

Obecnie hello domyślny punkt końcowy przydzielone jest 20 równoczesnych żądań RRS punktu końcowego. Możesz skalować w tym too200 równoczesnych żądań na punkt końcowy i można skalować każdego too10 usługi sieci web, 000 punktów końcowych dla usługi sieci web zgodnie z opisem w [skalowania usługi sieci Web](machine-learning-scaling-webservice.md). W przypadku usługi BES każdy punkt końcowy może przetwarzać 40 żądań jednocześnie, a dodatkowe żądania (po przekroczeniu 40 żądań) są dodawane do kolejki. Tych żądań w kolejce wykonywane automatycznie w miarę opróżniania kolejki hello.

**Czy zadania R są dystrybuowane między węzłami?**

Nie.  

**Ile danych mogę użyć do trenowania?**

Moduły w usłudze Machine Learning Studio obsługują zestawy danych o się too10 GB, zawierające gęsto upakowane dane typowe przypadki użycia. Jeśli moduł przyjmuje więcej niż jeden hello wejściowych, łączny rozmiar wszystkich danych wejściowych wynosi 10 GB. Większe zestawy danych można przed pozyskaniem próbkować przy użyciu zapytań programu Hive lub zapytań usługi Azure SQL Database albo stosując przetwarzanie wstępne za pomocą modułów [Uczenie przy użyciu liczenia][counts].  

Witaj następujące typy danych można rozszerzyć toolarger zestawów danych w funkcji normalizacji i są ograniczone tooless niż 10 GB:

* Rozrzedzone
* Podzielone na kategorie
* Ciągi
* Dane binarne

Witaj następujące moduły są ograniczone toodatasets mniej niż 10 GB:

* Moduły polecania
* Moduł Synthetic Minority Oversampling Technique (SMOTE)
* Moduły skryptów: R, Python, SQL
* Moduły, w którym hello output rozmiar danych może być większy niż rozmiar danych wejściowych, na przykład przyłączenie lub Tworzenie skrótu funkcji
* Krzyżowa weryfikacja, Hiperparametry modelu strojenia, Regresja porządkowa oraz Multiklasa Jedna kontra wszystkie, gdy liczba iteracji jest bardzo duża

W przypadku zestawów danych, które są większe niż kilka GB, przekazać dane tooAzure magazynów lub baza danych SQL Azure, lub użyć usługi HDInsight zamiast przekazywania bezpośrednio z pliku lokalnego.

**Czy istnieją jakiekolwiek ograniczenia dotyczące rozmiaru wektora?**

Wiersze i kolumny są każdego ograniczone toohello ograniczeniem .NET dla maksymalnej liczby całkowitej: 2 147 483 647.

**Czy można dostosować rozmiar hello hello maszyny wirtualnej, która jest uruchomiona usługa sieci web hello?**

Nie.  

## <a name="security-and-availability"></a>Bezpieczeństwo i dostępność
**Kto ma dostęp do punktu końcowego http hello usługi sieci web hello domyślnie? Jak ograniczyć dostęp toohello endpoint?**

Po wdrożeniu usługi sieci Web dla tej usługi tworzony jest domyślny punkt końcowy. Witaj domyślnego punktu końcowego można wywołać za pomocą swojego klucza interfejsu API. Można dodać więcej punktów końcowych z właściwymi dla nich kluczami z hello klasycznego portalu Azure lub programistycznie za pomocą hello interfejsów API sieci Web Service Management. Klucze dostępu są wymagane toomake wywołania usługi sieci web toohello. Aby uzyskać więcej informacji, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).

**Co się stanie, jeśli nie można odnaleźć konta magazynu platformy Azure?**

Usługa Machine Learning Studio polega na dostarczone przez użytkownika usługi Azure storage dane pośrednie toosave konta podczas wykonywania przepływu pracy hello. To konto magazynu jest udostępniane tooMachine Learning Studio po utworzeniu obszaru roboczego. Po hello obszaru roboczego jest tworzony, jeśli konto magazynu hello zostanie usunięta i nie można znaleźć, hello obszar roboczy przestanie działać i wszystkich eksperymentów, w tym obszaru roboczego zakończy się niepowodzeniem.

Jeśli przypadkowo usunięte hello konta magazynu, należy ponownie utworzyć hello konta magazynu z hello takie same nazwy hello tego samego regionu hello usunięto konto magazynu. Po wykonaniu tej ponownej synchronizacji hello klucz dostępu.

**Co się dzieje, gdy mój klucz dostępu do konta magazynu nie jest zsynchronizowany?**

Usługa Machine Learning Studio polega na dostarczone przez użytkownika usługi Azure storage dane pośrednie toostore konta podczas wykonywania przepływu pracy hello. To konto magazynu jest udostępniane tooMachine Learning Studio po utworzeniu obszaru roboczego i klucze dostępu hello są skojarzone z tym obszarem roboczym. Jeśli klucze dostępu hello zostaną zmienione po utworzeniu obszaru roboczego hello, hello obszaru roboczego dłużej korzystać z konta magazynu hello. W rezultacie przestanie działać, a wszystkie eksperymenty w tym obszarze roboczym zakończą się niepowodzeniem.

Jeśli zmienisz kluczy dostępu do konta magazynu, klucze dostępu hello ponownej synchronizacji, w obszarze roboczym hello przy użyciu hello klasycznego portalu Azure.  

## <a name="support-and-training"></a>Pomoc techniczna i szkolenia
**Gdzie można znaleźć szkolenia dotyczące usługi Azure Machine Learning?**

Witaj [Centrum dokumentacji uczenia maszynowego Azure](https://azure.microsoft.com/services/machine-learning/) hosty samouczki wideo i jak tooguides. Te przewodniki krok po kroku wprowadzić hello usług i wyjaśnić hello danych nauki cyklu życia importowanie danych, czyszczenie danych, budowanie modeli predykcyjnych i wdrażanie ich w środowisku produkcyjnym za pomocą usługi Azure Machine Learning.

Dodamy toohello materiału nowego centrum uczenia maszynowego w sposób ciągły. Można przesłać żądania dotyczące dodatkowych materiałów szkoleniowych w Centrum uczenia maszynowego na powitania [forum opinii użytkowników](https://windowsazure.uservoice.com/forums/257792-machine-learning).

Szkolenia można również znaleźć w witrynie [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).

**Jak uzyskać pomoc techniczną dotyczącą usługi Azure Machine Learning?**

tooget pomoc techniczna dla usługi Azure Machine Learning, przejdź zbyt[Azure obsługuje](/support/options/)i wybierz **uczenia maszynowego**.

Dla usługi Azure Machine Learning udostępniono również forum społeczności w witrynie MSDN, gdzie można zadawać pytania dotyczące usługi Azure Machine Learning. Zespół usługi Azure Machine Learning Hello monitoruje hello forum. Przejdź za[Azure Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).

## <a name="billing-questions"></a>Pytania dotyczące rozliczeń
**Jak działa rozliczanie w usłudze Machine Learning?**

Usługa Azure Machine Learning ma dwa składniki: usługę Machine Learning Studio i usługi sieci Web Machine Learning.

Gdy dokonujesz oceny usługi Machine Learning Studio, możesz użyć warstwę bezpłatna rozliczeń hello. Warstwa bezpłatna Hello umożliwia również wdrożyć klasycznego usługi sieci web, która ma ograniczoną pojemność.

Jeśli zdecydujesz, że usługi Azure Machine Learning spełni wymagania organizacji, możesz zarejestrować się w celu hello warstwy standardowa. toosign w górę, musi mieć subskrypcję Microsoft Azure.

W warstwie standardowa hello musisz są rozliczane co miesiąc dla każdego obszaru roboczego, który definiuje w usłudze Machine Learning Studio. Po uruchomieniu eksperymentów w hello studio są rozliczane za zasoby obliczeniowe po uruchomieniu eksperymentu. Podczas wdrażania usługi sieci web klasycznego, transakcje i obliczeń godziny są rozliczane na podstawie płatności zgodnie z rzeczywistym hello.

W nowych usługach sieci Web (opartych na usłudze Resource Manager) wprowadzono plany rozliczeniowe, które zwiększają przewidywalność kosztów. Cen warstwowych oferuje toocustomers rabaty, którzy potrzebują dużą ilość pojemności.

Po utworzeniu planu zatwierdzeniu tooa koszt dołączoną godziny obliczeń dla interfejsu API i transakcje interfejsu API w uwzględnionej ilości stały. Jeśli potrzebujesz większej ilości uwzględnione, można dodać wystąpienia tooyour planu. W przypadku konieczności dalszego zwiększenia ilości dostępnych zasobów można wybrać plan z wyższej warstwy, który zapewnia znacznie większą liczbę transakcji i oferuje korzystniejszą taryfę.

Po hello ilości uwzględnione w istniejących wystąpień wyczerpaniu dodatkowe obciążenie jest pobierana nadwyżkowe szybkością hello skojarzoną z hello rozliczeń planu warstwy.

> [!NOTE]
Ilości uwzględniane są ponownie przydzielona co 30 dni, a niewykorzystane kwoty uwzględnione nie są przerzucane toohello następnego okresu.

Dodatkowe informacje o rozliczeniach i cenach zawiera temat [Machine Learning — cennik](https://azure.microsoft.com/pricing/details/machine-learning/).

**Czy istnieje bezpłatna wersja próbna usługi Machine Learning?**

 Usługa Azure Machine Learning ma opcję bezpłatnej subskrypcji, która została wyjaśniona w temacie [Machine Learning — cennik](https://azure.microsoft.com/pricing/details/machine-learning/). Machine Learning Studio zawiera 8 godzinnym szybkiej oceny wersji próbnej, jest dostępna po zalogowaniu się za[Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2).

 Ponadto gdy utworzysz konto umożliwiające uzyskanie bezpłatnej wersji próbnej platformy Azure, możesz przez miesiąc korzystać z dowolnych usług Azure. toolearn więcej informacji na temat hello bezpłatnej wersji próbnej platformy Azure, odwiedź stronę [Azure bezpłatnej wersji próbnej — często zadawane pytania](https://azure.microsoft.com/pricing/free-trial-faq/).

**Co to jest transakcja?**

Transakcja odpowiada wywołaniu interfejsu API, na które odpowiada usługa Azure Machine Learning. Opłata za zagregowane transakcje powiązane z wywołaniami usług RRS i BES jest naliczana zgodnie z planem rozliczeniowym.

**Czy można użyć ilości transakcji hello zawarte w planie dla transakcji zarówno rekordy zasobów, jak i BES?**

Tak. Transakcje powiązane z wywołaniami usług RRS i BES są agregowane, a opłata za ich używanie jest naliczana zgodnie z planem rozliczeniowym.

**Co to jest godzina obliczeniowa interfejsu API?**

Godziny obliczeniowe interfejsu API jest jednostką rozliczeń hello raz hello zasoby obliczeniowe toorun podjęcia wywołania interfejsu API za pomocą uczenia maszynowego. Wszystkie wywołania są agregowane na potrzeby rozliczeń.

**Jak długo trwa typowe wywołanie interfejsu API w środowisku produkcyjnym?**

Czas wywołania interfejsu API produkcji może różnić się znacznie, zwykle od setki tooa milisekund po kilku sekundach. Niektóre wywołania interfejsu API może wymagać minut w zależności od złożoności hello hello przetwarzania danych i modelu uczenia maszynowego. Witaj najlepsze sposób tooestimate interfejsu API produkcji wywołanie razy jest toobenchmark modelu na powitania usługi Machine Learning.

**Co to jest godzina obliczeniowa środowiska Studio?**

Godziny obliczeniowe Studio dotyczy hello rozliczeniowym jednostki hello łączny czas, który eksperymentów używany zasobów obliczeniowych w studio.

**W nowych usług sieci web (opartej na usłudze Azure Resource Manager) co jest hello: tworzenie i testowanie warstwy przeznaczone?**

Usługi sieci web opartych na Menedżera zasobów zapewniają Konfiguracja wielu warstw, których można używać tooprovision planu rozliczeniowego. Hello: tworzenie i testowanie warstwy cenowej zapewnia ograniczony, dołączone ilości umożliwiających tootest eksperymentu jako usługę sieci web bez ponoszenia kosztów. Masz hello toosee okazji, jak to działa.

**Czy są naliczane oddzielne opłaty za magazyn?**

Machine Learning bezpłatnej warstwy Hello wymagają lub nie zezwalaj na używanie magazynu oddzielne. warstwy Machine Learning standardowe Hello wymaga toohave użytkowników konta magazynu platformy Azure. Opłata za korzystanie z usługi Azure Storage jest [naliczana oddzielnie](https://azure.microsoft.com/pricing/details/storage/).

**Czy usługa Machine Learning obsługuje wysoką dostępność?**

Tak. Aby uzyskać więcej informacji, zobacz [Machine Learning — cennik](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) opis hello Umowa dotycząca poziomu usług (SLA).

**Z jakiego konkretnego rodzaju zasobów obliczeniowych będą korzystać moje wywołania interfejsu API w środowisku produkcyjnym?**

Hello usługi Machine Learning to wielodostępna usługa. Zasoby obliczeniowe rzeczywiste, używanych na zapleczu hello zależą i są zoptymalizowane pod kątem wydajności oraz przewidywalności.

### <a name="management-of-new-resource-manager-based-web-services"></a>Zarządzanie nowymi usługami sieci Web (opartymi na usłudze Resource Manager)
**Co się stanie w przypadku usunięcia planu?**

Hello plan jest usuwany z subskrypcji i są rozliczane proporcjonalnie użycia.

> [!NOTE]
Nie można usunąć planu, którego używa usługa sieci Web. toodelete hello plan, albo Przypisz nowy plan usługi sieci web toohello lub usunąć hello usługi sieci web.

**Co to jest wystąpienie planu?**

Wystąpienie plan jest jednostką dołączone ilości dodać tooyour rozliczeń planu. Wybranie warstwy rozliczeniowej dla planu powoduje dodanie jej do jednego wystąpienia. Jeśli potrzebujesz większej ilości dołączone, można dodać wystąpienia hello wybranej warstwy tooyour plan rozliczeniowy.

**Ile wystąpień planu mogę dodać?**

Może mieć jedno wystąpienie warstwy cenowej i testowania hello w ramach subskrypcji.

W przypadku warstwy Standardowa S1, S2 i S3 możesz dodać tyle wystąpień, ile potrzebujesz.

> [!NOTE]
W zależności od przewidywanego użycie go może być bardziej ekonomiczne warstwy tooa tooupgrade dołączył większej ilości zamiast dodawać Warstwa bieżąca toohello wystąpień.

**Co się stanie w przypadku zmiany warstw planu (uaktualnienia bądź obniżenia poziomu)?**

plan starego Hello zostanie usunięty, a bieżące użycie hello jest rozliczane na podstawie proporcjonalnie. Dla rest hello okresu hello jest tworzony nowy plan hello pełnej ilości dołączone hello uaktualnione obniżenia poziomu.

> [!NOTE]
Wliczone transakcje są przydzielane na podstawie okresu, a niewykorzystane zasoby nie przechodzą na następny okres.

**Co się stanie, jeśli zwiększyć hello wystąpień w planie?**

Ilości znajdują się na zasadzie proporcjonalnie i może potrwać skuteczne toobe 24 godziny.

**Co się stanie w przypadku usunięcia wystąpienia planu?**

wystąpienie Hello jest usuwany z subskrypcją i są rozliczane proporcjonalnie użycia.

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>Subskrypcja planów nowych usług sieci Web (opartych na usłudze Resource Manager)
**Jak zasubskrybować plan?**

Użytkownik ma dwa sposoby toocreate rozliczeń plany.

Przy pierwszym wdrożeniu usługi sieci Web opartej na usłudze Resource Manager możesz wybrać istniejący plan lub utworzyć nowy.

Plany tworzone w ten sposób są w danym regionie domyślne i usługi sieci web zostaną wdrożone toothat regionu.

Jeśli chcesz toodeploy tooregions usług innych niż domyślne regionu, możesz toodefine planów rozliczeń przed wdrożeniem usługi.

W takim przypadku można zarejestrować się w portalu usługi sieci Web systemu Azure Machine Learning toohello i przejdź toohello planów strony. Pozwala ona dodawać, usuwać i modyfikować plany.

**Plan, który należy wybrać toostart poza z?**

Zalecamy rozpoczęcia z hello standardowa S1 warstwy i monitorować użycie Twojej usługi. Jeśli okaże się, że używasz programu dołączone ilości szybko, możesz dodać wystąpień lub Przenieś do wyższego poziomu tooa i uzyskać lepiej rabaty. Plan rozliczeniowy można dostosowywać zgodnie z potrzebami w całym cyklu rozliczeniowym.

**Regiony są dostępne w nowych planów hello?**

nowe plany rozliczeń Hello są dostępne w trzech regionów produkcji hello, w których obsługujemy hello nowych usług sieci web:

* Środkowo-południowe stany USA
* Europa Zachodnia
* Azja Południowo-Wschodnia

**Moje usługi sieci Web działają w kilku regionach. Czy muszę mieć plan dla każdego regionu?**

Tak. Ceny planów zależą od regionu. Podczas wdrażania region tooanother usługi sieci web należy tooassign it a plan, który jest toothat określonego regionu. Aby uzyskać więcej informacji, zobacz [Dostępność produktów według regionów]( https://azure.microsoft.com/regions/services/).

### <a name="new-web-services-overages"></a>Nowe usługi sieci Web: użycie nadwyżkowe
**Jak sprawdzić, czy przekroczono limit użycia usługi sieci Web?**

Użycie hello można wyświetlić na wszystkie plany na stronie planów hello w portalu usługi sieci Web systemu Azure Machine Learning hello. Zaloguj się w portalu toohello, a następnie kliknij przycisk hello **plany** opcji menu.

W hello **transakcji** i **obliczeniowe** kolumny tabeli hello, widać ilości hello uwzględnione hello planu i hello procent wykorzystania.

**Co się dzieje podczas używania zapasowej hello objąć ilości warstwy cenowej i testowania hello?**

Usługi, których tworzenie/testowanie toothem przypisane warstwy cenowej zostały zatrzymane do momentu hello następnym okresie lub przenieść je warstwy tooa płatnej.

**Jak są naliczane ceny obciążeń RRS (Request Response) i BES (Batch) w przypadku klasycznych usług sieci Web oraz nadwyżkowego użycia nowych usług sieci Web (opartych na usłudze Resource Manager)?**

Dla obciążenia rekordy zasobów są naliczane dla każdego wywołania interfejsu API transakcji, wprowadzone i czasu obliczeniowego hello, który został skojarzony z żądaniami. Koszty transakcji interfejsu API produkcji rekordy zasobów są obliczane zgodnie z hello łączna liczba wywołań interfejsu API, wprowadzone pomnożona przez cena hello na 1000 transakcji (obliczone proporcjonalnie według pojedynczych transakcji). Koszty godziny obliczeniowe interfejsu API produkcji API rekordy zasobów są obliczane jako hello ilość czasu wymaganego do każdego toorun wywołania interfejsu API, pomnożona przez hello całkowita liczba transakcji interfejsu API, pomnożona przez hello cenę godzinową obliczeniowe interfejsu API produkcji.

Na przykład dla nadwyżkowe elementy w warstwie standardowa S1, 1 000 000 transakcji interfejsu API, które miały 0,72 sekund każdego toorun spowodowałoby (1 000 000 * wysokości 0,50 USD, 1K transakcje interfejsu API) w wysokości 500 USD kosztów transakcji interfejsu API produkcji i (1 000 000 * 0.72 s * $2 / h) $400 w obliczeniowe interfejsu API produkcji godzin, łącznie z 900 $.

Dla obciążenia BES, naliczane są opłaty w hello sam sposób. Koszty transakcji interfejsu API hello reprezentują hello liczba zadań, które można przesłać i kosztów obliczeń hello reprezentują czasu obliczeniowego hello skojarzoną z tych zadań wsadowych. Koszty transakcji interfejsu API produkcji BES są obliczane zgodnie z hello łączna liczba zadań przesłane pomnożona przez cena hello na 1000 transakcji (obliczone proporcjonalnie według pojedynczych transakcji). Koszty godziny obliczeniowe interfejsu API produkcji interfejsu API usługi BES są obliczane jako hello ilość czasu wymagane dla każdego wiersza w Twojej toorun zadania pomnożona przez hello całkowitą liczbę wierszy w zadania pomnożona przez hello łączna liczba zadań pomnożona przez cena hello na interfejsu API produkcji obliczenia bazy danych godzinę. Gdy używasz hello Kalkulator uczenia maszynowego, hello transakcji meter reprezentuje hello liczbę zadań planujesz toosubmit, czy pole czas na transakcji hello reprezentuje hello łączyć czasu potrzebne dla wszystkich wierszy w każdym toorun zadania.

Jeśli w ramach użycia nadwyżkowego w warstwie Standardowa S1 przesyłasz na przykład 100 zadań dziennie, z których każde zawiera 500 wierszy o czasie uruchamiania 0,72 s, miesięczny koszt nadwyżkowych transakcji interfejsu API w środowisku produkcyjnym wyniesie 1,55 USD (100 zadań dziennie = 3100 zadań/mies. 0,50 USD/1000 transakcji interfejsu API), a koszt godzin obliczeniowych interfejsu API w środowisku produkcyjnym wyniesie 620 USD (500 wierszy 0,72 s 3100 zadań 2 USD/godz.), co daje łączną kwotę 621,55 USD.

### <a name="azure-machine-learning-classic-web-services"></a>Klasyczne usługi sieci Web Azure Machine Learning
**Czy model płatności zgodnie z rzeczywistym użyciem jest wciąż dostępny?**

Tak, klasyczne usługi sieci Web są wciąż dostępne w usłudze Azure Machine Learning.  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Usługa Azure Machine Learning w warstwie Bezpłatna i Standardowa
**Zawartość hello Azure Machine Learning bezpłatnej warstwy?**

Warstwa Azure Machine Learning wolnego Hello jest zamierzone tooprovide toohello szczegółowe wprowadzenie Azure Machine Learning Studio. Wystarczy działa toosign konta Microsoft. Witaj warstwę bezpłatna zawiera obszar roboczy usługi Azure Machine Learning Studio tooone bezpłatny dostęp na [konta Microsoft](https://www.microsoft.com/account/default.aspx). W tej warstwie można użyć too10 GB miejsca do magazynowania i operacjonalizuj modele jako tymczasowej interfejsów API. Obciążenia warstwy Bezpłatna nie są objęte umową SLA i są przeznaczone tylko do użytku osobistego i do opracowywania rozwiązań. 

Obszary robocze warstwa bezpłatna ma hello następujące ograniczenia:

* Obciążeń danych łącząc tooan lokalnego serwera z programem SQL Server nie ma dostępu.
* Nie można wdrażać nowych podstawowych usług sieci Web usługi Resource Manager.


**Zawartość hello Azure Machine Learning standardowe warstwy i planów?**

Warstwa Azure Machine Learning standardowe Hello jest wersja produkcyjna płatne Azure Machine Learning Studio. Hello Azure Machine Learning Studio miesięczna są rozliczane według poszczególnych na miesiąc obszaru roboczego i proporcjonalnie częściowe miesięcy. Godziny prowadzenia eksperymentów w usłudze Azure Machine Learning Studio są rozliczane na podstawie godzin obliczeniowych w ramach aktywnych eksperymentów. W przypadku niepełnych godzin opłaty są naliczane proporcjonalnie.  

Usługa Azure Machine Learning API Hello jest on rozliczany w zależności od tego, czy jest usługą sieci web klasycznego lub nową usługę sieci web (opartych na Resource Manager).

powitania po opłaty są agregowane dla obszaru roboczego dla Twojej subskrypcji.

* Machine Learning obszaru roboczego subskrypcji: hello subskrypcji obszaru roboczego uczenia maszynowego jest miesięczna udostępniający obszaru roboczego usługi Machine Learning Studio tooa dostępu. Subskrypcja Hello jest wymagana toorun eksperymenty w hello studio tooutilize hello produkcji i interfejsów API.
* Godziny prowadzenia eksperymentów w Studio: Ten licznik agreguje wszystkich opłat za obliczenia, które są naliczane za eksperymentów w usłudze Machine Learning Studio i uruchomione interfejsu API produkcji wywołań w hello przemieszczania środowiska.
* Dostęp do danych przez połączenie tooan lokalnego serwera z programem SQL Server w modelach z szkolenia i oceniania.
* W przypadku klasycznych usług sieci Web:
  * Godziny obliczeń dla interfejsu API produkcji: ten licznik obejmuje opłaty za zasoby obliczeniowe naliczane przez usługi sieci Web w środowisku produkcyjnym.
  * Transakcje interfejsu API produkcji (w 1000): Ten licznik obejmuje opłaty są naliczane dla usługi sieci web produkcji tooyour wywołania.

Oprócz hello poprzedzających opłat, w przypadku hello usługi sieci web opartych na Menedżera zasobów opłaty są agregowane toohello wybranego planu:

* Standardowa S1/S2/S3 interfejsu API planowanie (jednostki): Ten licznik reprezentuje typ hello wystąpienia, który został wybrany do usług sieci web opartych na Menedżera zasobów.
* Standardowa S1/S2/S3 nadwyżkowe godziny obliczeniowe interfejsu API: Ten licznik dotyczy opłat za obliczenia, które są naliczane przez usługi sieci web opartych na Menedżera zasobów, które są uruchamiane w środowisku produkcyjnym po ilości hello uwzględnione w istniejących wystąpień. Użycie dodatkowych Hello jest rozliczana według hello overate szybkość, z której jest skojarzony z warstwą planu S1/S2/S3.
* Standardowa S1/S2/S3 nadwyżkowe transakcje interfejsu API (w 1000): Ten licznik obejmuje opłaty są naliczane na wyczerpaniu usługi sieci web opartych na Resource Manager po hello ilości w istniejących wystąpień tooyour wywołania w środowisku produkcyjnym. Witaj dodatkowe obciążenie jest rozliczana według hello overate szybkość związane z warstwą planu S1/S2/S3.
* Uwzględniona ilość godziny obliczeń dla interfejsu API: Z usługami sieci web opartych na Menedżera zasobów, ten licznik reprezentuje hello uwzględniona ilość godziny obliczeń dla interfejsu API.
* Uwzględniona ilość transakcje interfejsu API (w 1000): na podstawie za pomocą Menedżera zasobów usługi sieci web, ten licznik reprezentuje hello uwzględniona ilość transakcje interfejsu API.

**Jak zasubskrybować usługę Azure Machine Learning w warstwie Bezpłatna?**

Do korzystania z tej usługi wystarczy konto Microsoft. Przejdź za[główną usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), a następnie kliknij przycisk **Rozpocznij teraz**. Zaloguj się przy użyciu konta Microsoft — zostanie utworzony obszar roboczy w warstwie Bezpłatna. Można uruchomić tooexplore i od razu utworzyć eksperymenty uczenia maszynowego.

**Jak zasubskrybować usługę Azure Machine Learning w warstwie Standardowa?**

Najpierw musisz toocreate subskrypcji platformy Azure tooan dostęp do obszaru roboczego uczenia maszynowego standardowa. Możesz utworzyć konto dla 30-dniowej bezpłatnej wersji próbnej subskrypcji Azure i nowszej tooa uaktualnienia płatnej subskrypcji platformy Azure lub można kupić płatną subskrypcję Azure bezpośrednich. Następnie można utworzyć obszaru roboczego uczenia maszynowego z klasycznego portalu Microsoft Azure hello po uzyskaniu dostępu toohello subskrypcji. Widok hello [instrukcje krok po kroku](https://azure.microsoft.com/trial/get-started-machine-learning-b/).

Alternatywnie możesz można zaprosić przez standardowe uczenia maszynowego obszaru roboczego właściciela tooaccess hello właściciela obszaru roboczego.

**Czy można określić własne toouse konta magazynu obiektów Blob platformy Azure, z warstwę bezpłatna hello?**

Nie, warstwy standardowa hello jest równoważne toohello wersja hello usługi Machine Learning, który był dostępny przed powitalne warstw zostały wprowadzone.

**Czy mogę wdrożyć komputerze modeli uczenia jako interfejsów API w warstwie bezpłatna hello?**

Tak, aby operacjonalizować uczenia maszynowego modele toostaging interfejsu API usługi jako część hello warstwę bezpłatna. tooput hello przemieszczania usługi interfejsu API w środowisku produkcyjnym i Pobierz punktu końcowego produkcji hello operationalized usługi, należy użyć hello warstwy standardowa.

**Jaka jest różnica hello Azure bezpłatnej wersji próbnej i warstwa Azure Machine Learning bezpłatna?**

Witaj [bezpłatna wersja próbna programu Microsoft Azure](https://azure.microsoft.com/free/) oferuje usługi środków, które można zastosować tooany Azure przez miesiąc. Hello Azure Machine Learning bezpłatnej warstwy oferty ciągłego dostępu w szczególności tooAzure uczenia maszynowego dla obciążeń nieprodukcyjnych.

**Jak przenieść doświadczenia z warstwy standardowa toohello warstwę bezpłatna hello?**

toocopy eksperymentów z warstwy standardowa toohello warstwę bezpłatna hello:

1. Zaloguj się w usłudze Machine Learning Studio tooAzure i upewnij się, że widać zarówno hello wolnego obszarów roboczych i hello standardowe w selektora obszaru roboczego hello hello górnym pasku nawigacyjnym.
2. Przełącz tooFree obszaru roboczego, jeśli są w obszarze roboczym standardowe hello.
3. W widoku listy eksperymentu hello, wybierz eksperymentu, że będzie toocopy, takich jak, a następnie kliknij przycisk hello **kopiowania** przycisku polecenia.
4. Wybierz hello standardowe obszaru roboczego z hello okno dialogowe, którego kliknięcie spowoduje otwarcie, a następnie kliknij przycisk hello **kopiowania** przycisku.
   Witaj wszystkie skojarzone zestawów danych, trenowanego modelu, itp. są kopiowane wraz z doświadczenia hello hello standardowe obszaru roboczego.
5. Należy toorerun hello eksperymentu, a następnie ponownie opublikować usługi sieci web, w obszarze roboczym standardowe hello.

### <a name="studio-workspace"></a>Obszar roboczy Studio
**Czy otrzymam różne rachunki za różne obszary robocze?**

Opłaty za obszar roboczy są naliczane oddzielnie za każdy mający zastosowanie licznik i przedstawiane na jednym rachunku.

**Z jakiego konkretnego rodzaju zasobów obliczeniowych będą korzystać moje eksperymenty?**

Hello usługi Machine Learning to wielodostępna usługa. Zasoby obliczeniowe rzeczywiste, używanych na zapleczu hello zależą i są zoptymalizowane pod kątem wydajności oraz przewidywalności.

### <a name="guest-access"></a>Dostęp gościa
**Co to jest tooAzure dostępu dla gości Machine Learning Studio?**

Dostęp gościa jest ograniczoną wersją próbną środowiska użytkownika. Możesz tworzyć i uruchamiać eksperymenty w usłudze Azure Machine Learning Studio bezpłatnie i bez uwierzytelniania. Sesje gościa są trwałe (nie można zapisać) i ograniczoną tooeight godzin. Pozostałe ograniczenia to brak obsługi języków R i Python, brak przejściowych interfejsów API oraz ograniczony rozmiar zestawów danych i przestrzeni dyskowej. W porównaniu użytkowników, którzy wybierz toosign za pomocą konta Microsoft ma warstwę bezpłatna toohello pełnego dostępu do usługi Machine Learning Studio opisanej wcześniej w tym trwałego obszaru roboczego i bardziej kompleksowe możliwości. występują toochoose Twojego wolnego Machine Learning, kliknij przycisk **wprowadzenie** na [https://studio.azureml.net](https://studio.azureml.net), a następnie wybierz **odgadnąć dostępu** lub zaloguj się przy użyciu programu Microsoft konto.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
