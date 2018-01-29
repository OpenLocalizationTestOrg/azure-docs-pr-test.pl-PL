---
title: "Azure Machine Learning Podgląd 2017 — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera często zadawane pytania i odpowiedzi dla funkcji w wersji zapoznawczej usługi Azure Machine Learning"
services: machine-learning
author: serinakaye
ms.author: serinak
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 08/30/2017
ms.openlocfilehash: 94c6576f92b5a004e0fd509c1dc6e091c294658a
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="azure-machine-learning-frequently-asked-questions"></a>Usługa Azure Machine Learning — często zadawane pytania

## <a name="general-product-questions"></a>Pytania ogólne produktu

**Co to jest Azure Machine Learning?**

Azure Machine Learning jest pełni zarządzaną usługę platformy Azure, która służy do tworzenia, testowania, zarządzania i wdrażania uczenia maszynowego i modele AI. Naszych nowych usług i aplikacji do pobrania oferują podejście pierwszy kod, który korzysta z chmury, lokalne i krawędzi Podaj pociąg, wdrażania, zarządzania i monitorowania modeli z zasilania, szybkość i elastyczność. Alternatywnie Azure Machine Learning Studio oferuje przeglądarki, visual przeciągania i upuszczania tworzenia środowisko których kodowanie nie jest wymagane. 

**Jak rozpocząć pracę z wersji zapoznawczej?**

Najłatwiejszym sposobem na rozpoczęcie pracy jest zalogowania się do usługi eksperymenty w usłudze Azure. Z portalu możesz pobrać naszej bezpłatnej aplikacji Workbench lub Załóż konto zarządzania modelu. Ponadto mogą odwiedzać witryny dokumentacji nasze artykuły, filmy wideo, pokaz kodu i inne. 

**Nie masz subskrypcji platformy Azure. Nadal można wypróbować nowych usług?**

Jako część wchodzących w skład zestawu Microsoft Azure naszej nowej usługi wymagają subskrypcji platformy Azure. Ponadto musi mieć odpowiednie uprawnienia do tworzenia zasoby, takie jak grupy zasobów, maszyny wirtualne itp. 

**W którym regiony są dostępne jest nowe usługi?**

Wyszukaj obsługiwane regiony platformy Azure dla eksperymenty i model usługi zarządzania w ramach usługi Azure Machine Learning [produkty Azure według regionu](https://azure.microsoft.com/regions/services/) strony.

Będzie można dodać kolejnych regionach, ponieważ opracowywania produktu.  Możesz pomóc nam priorytety regiony do wdrożenia na naszych [Azure Machine Learning opinii](https://feedback.azure.com/forums/257792-machine-learning) lokacji. 

**Jakie innymi usługami platformy Azure są potrzebne?**

Pełni występują wszystkie funkcje usługi Azure Machine Learning, Azure maszyny Learnign użyje Visual Studio VSTS konto, magazyn obiektów Blob Azure rejestru kontenera platformy Azure, obliczeń maszyny Wirtualnej nauki danych lub HDInsight i usługi kontenera platformy Azure.

**Jak związek między Microsoft Machine Learning usług w 2017 serwera SQL Azure Machine Learning?**   

Usługi Machine Learning w 2017 serwera SQL to rozszerzalny, skalowalna platforma zintegrować machine learning zadania przepływów pracy bazy danych. Jest dokładne dopasowanie dla scenariuszy, w których jest wymagane, na przykład gdy przepływu danych jest kosztowna lub trudną rozwiązania lokalnego. Z kolei obciążeń w chmurze czy hybrydowa są doskonałe dopasowanie dla naszego nowego usług Azure. 

**Są obsługiwane zarówno w przypadku języka Python, jak i R? Informacje o innych języków programowania, takich jak C++**

Firma Microsoft obsługuje obecnie środowiska Python tylko. Firma Microsoft pracuje nad integracji R i oczekiwaną będzie dostępna wkrótce. 

**Jak uczenie maszynowe Azure odnosi się do uczenia maszynowego Microsoft Spark?**

A: MMLSpark zapewnia głębokie uczenie i narzędzia nauki danych platformy Apache Spark, ze szczególnym uwzględnieniem wydajność, łatwość eksperymenty i algorytmy stanu grafiki. MMLSpark oferuje integrację potoków Spark Machine Learning z kognitywnych zestaw narzędzi firmy Microsoft i OpenCV. Można tworzyć zaawansowane, skalowalnej modeli predykcyjnych i analitycznych danych obrazu i tekstu. MMLSpark jest dostępna na licencji open source i znajduje się w AML Workbench jako zestaw eksploatacyjny modeli i algorytmów. Więcej informacji o MMLSpark można znaleźć w naszej dokumentacji produktu. 

**Które wersje Spark są obsługiwane przez nowe narzędzia i usługi? Pierwsza sekcja**

Obecnie Workbench obejmuje i obsługuje MMLSpark wersji 0,8, który jest zgodny z Apache Spark 2.1. Istnieje również możliwość użycia obraz włączone GPU Docker MMLSpark 0,8 na maszynach wirtualnych systemu Linux.

## <a name="experimentation-service"></a>Usługa eksperymenty

**Co to jest usługa eksperymenty Azure Machine Learning?**

Usługa eksperymenty jest zarządzana usługa platformy Azure, która przyjmuje machine learning eksperymenty na następny poziom. Mogą być tworzone eksperymentów, lokalnie lub w chmurze. Szybkie prototypu na pulpicie, następnie skalowanie do maszyn wirtualnych lub klastry Spark. Maszyny wirtualne platformy Azure z najnowszych technologii procesora GPU umożliwiają prowadzenia głębokie uczenia szybkie i skuteczne. Dołączono również głęboką integrację z usługą Git, można łatwo podłączyć do istniejących przepływów pracy dla śledzenia kodu, konfiguracji i współpracy. 

**Jak mogę obciążymy usługi eksperymenty?**

Pierwsze dwa użytkowników skojarzonych z usługą Azure Machine Learning eksperymenty są wolne. Dodatkowych użytkowników zostanie naliczona opłata w wysokości 50 miesięcznie publicznej wersji zapoznawczej. Aby uzyskać więcej informacji na cennik i rozliczenia odwiedź stronę cennik.

**Zostanie I być naliczane na podstawie eksperymentów ile uruchomić?**

Nie, usługę eksperymenty umożliwia tyle eksperymenty podczas potrzeby i opłat tylko na podstawie liczby użytkowników. Opłaty za zasoby obliczeniowe usługi Eksperymentowanie są naliczane oddzielnie. Firma Microsoft zachęca do wykonywania wielu eksperymentów, aby umożliwić znalezienie najlepsze dopasowanie modelu do rozwiązania.   

**Jakie określone zasoby obliczeniowe i magazynujące można użyć?**

Usługa eksperymenty można wykonać eksperymentów na maszynach lokalnych (bezpośrednio lub na podstawie Docker), [maszyny wirtualne Azure](https://azure.microsoft.com/services/virtual-machines/), i [HDInsight](https://azure.microsoft.com/services/hdinsight/). Usługa również uzyskuje dostęp do [usługi Azure Storage](https://azure.microsoft.com/services/storage/) konta do przechowywania danych wyjściowych wykonywania i mogą korzystać z [programu Visual Studio Team Service](https://azure.microsoft.com/services/visual-studio-team-services/) konta w celu kontroli wersji i magazynu Git. Należy pamiętać, że opłaty będą naliczane osobno dla dowolnego wykorzystanych zasoby obliczeniowe i magazynowe, oparte na poszczególnych cennik.  


## <a name="model-management"></a>Zarządzanie modelami

**Co to jest Azure Machine Learning Model zarządzania?**

Azure Machine Learning modelu Management jest zarządzana usługa platformy Azure, która umożliwia danych i analityków ops deweloperów zespołom niezawodnie wdrażanie modeli predykcyjnych w różnych środowiskach. Repozytoria Git i kontenery Docker zapewnia możliwości śledzenia i powtarzalności. Modele można wdrożyć niezawodnie w chmurze, lokalnymi lub krawędzi. Raz w środowisku produkcyjnym, możesz zarządzać wydajności modelu, a następnie aktywnego retrain jeśli powoduje spadek wydajności. Modele na komputerach, można wdrożyć do [maszynach wirtualnych platformy Azure](https://azure.microsoft.com/services/virtual-machines/), Spark na [HDInsight](https://azure.microsoft.com/services/hdinsight/) lub zorkiestrowana Kubernetes [usługi kontenera platformy Azure](https://azure.microsoft.com/services/container-service/) klastrów.  

**Co to jest "modelu"?**

Model jest dane wyjściowe eksperymenty, w którym został podniesiony do zarządzania w modelu. Model, który jest zarejestrowany w ramach konta hostingu jest uwzględniane planu, łącznie z modeli zaktualizowane do ponownego trenowania wersji lub iteracji.

**Co to jest "model zarządzanego?"**

Model to wynik procesu uczenia, który jest zastosowaniem algorytmu uczenia maszynowego do danych treningowych. Model zarządzania umożliwia wdrażanie modeli jako usługi sieci web, zarządzanie różnymi wersjami modeli i monitorowanie ich wydajności i metryki. Modele "Zarządzany" zostały zarejestrowane przy użyciu konta Azure Machine Learning Model zarządzania. Jako przykład rozważ scenariusz, w którym próbujesz prognozować sprzedaż. Podczas fazy eksperymenty przy użyciu różnych zestawów danych lub algorytmy generowania wielu modeli. Wygenerowano cztery modele z różnymi dokładności, ale zdecyduje się zarejestrować tylko modelu z najwyższym dokładności. Model, który jest zarejestrowany staje się pierwszym model zarządzanego.
 
**Co to jest "wdrożenia?"**

Model zarządzania umożliwia wdrażanie modeli jako kontenery usługi spakowanych sieci web na platformie Azure. Te usługi sieci web mogą być wywoływane przy użyciu interfejsów API REST. Każdą usługę sieci web będzie traktowany jako pojedynczego wdrożenia, a całkowita liczba aktywnych wdrożeń są zliczane kierunku planu. Przy użyciu sprzedaży prognozowania przykład wdrażając najlepszym wykonywania modelu, plan jest zwiększany o jedno wdrożenie. Następnie ponownie ucz i wdrożyć innej wersji, użytkownik ma dwa wdrożenia. Jeśli okaże się, że lepiej jest nowsza modelu i usunięcia oryginał, liczba wdrożenia jest zmniejszana o jeden.  

**Jakie zasoby obliczeniowe określonych są dostępne dla moich wdrożenia?** 

Model zarządzania można uruchomić wdrożeń kontenery Docker zarejestrowany do [usługi kontenera platformy Azure](https://azure.microsoft.com/services/container-service/), jako [maszyny wirtualne Azure](https://azure.microsoft.com/services/virtual-machines/), lub na komputerach lokalnych. Wkrótce zostaną dodane cele dodatkowe wdrożenia. Należy pamiętać, że opłaty będą naliczane osobno dla wszystkich zasobów obliczeniowych wykorzystanych, oparte na poszczególnych cennik.     

**Do wdrażania modeli utworzony przy użyciu narzędzia innego niż usługi eksperymenty można użyć usługi Azure Machine Learning modelu Management?**

Możesz uzyskać najlepsze doświadczenia, podczas wdrażania modeli utworzonych przy użyciu usługi eksperymenty. Jednak można wdrożyć modeli utworzony przy użyciu innych platform i narzędzi. Firma Microsoft obsługuje różne modele w tym MMLSpark, TensorFlow, Microsoft kognitywnych Toolkit, scikit — Dowiedz się, Keras itp. 

**Można użyć własnych zasobów platformy Azure?**

Tak, usługa eksperymenty i Model zarządzania działa w połączeniu z wielu magazynów danych Azure, obliczeniowe obciążeń i innych usług. Odwoływać się do naszej dokumentacji technicznej, aby uzyskać więcej szczegółowych informacji dotyczących wymaganych usług Azure.

**Obsługuje zarówno lokalnie i w chmurze, scenariusze wdrażania?**

Tak. Firma Microsoft obsługuje lokalnie i w chmurze wdrożeń za pomocą kontenerów Docker. Wykonanie lokalne obiekty docelowe obejmują: wdrożenia Docker w pojedynczym węźle [programu Microsoft SQL Server z usługami ML](https://docs.microsoft.com/sql/advanced-analytics/r/r-services), Hadoop lub Spark. Obsługujemy również chmura wdrożenia za pośrednictwem Docker, w tym: wdrożeń w klastrze za pomocą usługi kontenera platformy Azure i Kubernetes, HDInsight lub Spark klastrów. Krawędź scenariusze są obsługiwane za pośrednictwem kontenery Docker i Azure IOT krawędzi. 

**Czy można uruchomić obrazu Docker, który został utworzony na innym hoście za pomocą interfejsu wiersza polecenia Azure Machine Learning?**

Tak. Obraz służy jako usługę sieci web na żadnym hoście docker tak długo, jak host ma wystarczające zasoby obliczeniowe do obsługi obrazów docker.

**Czy ponownego trenowania wdrożonej modeli są obsługiwane?**

Tak, można wdrożyć wiele wersji tego samego modelu. Model administracyjny będzie obsługiwać aktualizacje usługi wszystkie zaktualizowane modele i obrazów.

## <a name="workbench"></a>Workbench

**Co to jest Azure Machine Learning Workbench?**

Azure Machine Learning Workbench jest aplikacją pomocnika skompilowany dla analityków danych professional. Dostępne dla systemu Windows i Mac, Machine Learning Workbench zawiera przegląd, zarządzania i kontroli machine learning rozwiązań. Machine Learning Workbench obejmuje dostęp do struktur AI najnowocześniejszych przez firmę Microsoft i społecznością typu open source. Dodaliśmy najpopularniejszych narzędzi nauki danych, takich jak TensorFlow, kognitywnych zestaw narzędzi firmy Microsoft, Spark ML, scikit — Dowiedz się więcej i inne. Integracja z popularnych danych nauki IDEs notesów Jupyter, PyCharm i Visual Studio Code również włączono. Machine Learning Workbench ma wbudowane danych przygotowania funkcje szybko przykładowe, zrozumieć i przygotowania danych, czy strukturalnych lub bez struktury. Nasze nowe narzędzie przygotowywania danych, o nazwie [PROZIE](https://microsoft.github.io/prose/), jest oparty na technologii najnowocześniejsze Microsoft Research.  

**Jest Workbench IDE?**

Nie. Machine Learning Workbench został zaprojektowany jako dodatek do popularnych IDEs notesów Jupyter, Visual Studio Code i PyCharm, ale nie jest pełną funkcjonalność IDE. Machine Learning Workbench oferuje niektórych tekst podstawowych funkcji edytowania, ale debugowania, intellisense i inne często używane funkcje IDE nie są obsługiwane. Zalecane jest użycie Twoje ulubione IDE dla rozwoju kodu, edytowanie i debugowanie. 

**Czy istnieje opłata za pomocą Azure Machine Learning Workbench?**

Nie. Azure Machine Learning Workbench to bezpłatna aplikacja. Możesz ją pobrać dla tylu komputerów i użytkowników, dla ilu potrzebujesz. Aby korzystać z aplikacji Azure Machine Learning Workbench, musisz mieć konto usługi Eksperymentowanie. .  

**Czy są obsługiwane funkcje wiersza polecenia?**

A: tak, usługa Azure Machine Learning zapewnia pełne interfejsu CLI. Machine Learning interfejsu wiersza polecenia jest instalowany domyślnie z Azure Machine Learning Workbench. Jest również udostępniany w ramach maszyny wirtualnej systemu Linux nauki danych na platformie Azure i będzie można zintegrować [wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/overview?view=azure-cli-latest)


**Czy za pomocą notesów Jupyter z Workbench?**

Tak! Można uruchomić notesów Jupyter w Workbench z Workbench jako aplikacja obsługi klienta, tak samo, jak używasz przeglądarki jako klienta. 

**Jądra notesu Jupyter, które są obsługiwane?**

Odpowiedź: Bieżąca wersja Jupyter dołączonego Workbench uruchamia jądra Python 3 i dodatkowe jądra dla każdego pliku "runconfig" w folderze aml_config. Obsługiwane konfiguracje obejmują:
- Lokalne Python
- Python w lokalnym lub zdalnym Docker

## <a name="data-formats-and-capabilities"></a>Formaty danych i możliwości

**Formaty plików, które są obecnie obsługiwane przez pozyskiwanie danych w Workbench?**

Narzędzia przygotowywania danych w Workbench obsługuje obecnie wprowadzanie w następujących formatach: 
- Rozdzielone pliki CSV TSV, np.  
- Pliki o stałej szerokości
- Pliki w formacie zwykłego tekstu
- Program Excel (xls/xlsx)
- Pliki JSON
- Pliki parquet 
- Niestandardowe pliki (skrypty), jeśli rozwiązanie wymaga wprowadzanie danych z dodatkowych źródeł kodu Python może służyć do... 

**Lokalizacji magazynu danych, które są obecnie obsługiwane?**

Dla publicznej wersji zapoznawczej Workbench obsługuje wprowadzanie danych z: 
- Lokalny dysk twardy lub lokalizacji magazynu mapowanej sieci
- Azure BLOB lub magazynu Azure (wymaga subskrypcji platformy Azure)
- Serwer usługi SQL Azure
- Microsoft SQL Server


**Jakie dane wrangling, przygotowywania i przekształceń są dostępne?**

Publicznej wersji zapoznawczej Workbench obsługuje "Pochodzi kolumny według przykładu", "Podziału kolumny według przykładu", "Klaster tekst", "Obsługi brakuje wartości" i wielu innych.  Workbench obsługuje również konwersja typu danych, agregacja danych (liczba, średnia, odchylenie itp.) i danych złożonych sprzężeń. Pełną listę obsługiwanych możliwości można znaleźć w naszej dokumentacji produktu. 

**Czy istnieją żadnych limity rozmiaru danych, wymuszane przez usługi Azure Machine Learning Workbench, eksperymenty lub modelu administracyjnego?**

Odpowiedź: nie nowych usług nie nakładają żadnych ograniczeń danych. Istnieją jednak ograniczenia wprowadzone przez środowisko, w którym działają Przygotowanie danych, szkolenia modelu, eksperymenty lub wdrożenia. Na przykład jeśli ma być przeznaczona dla lokalnego środowiska szkolenia, możesz jest ograniczona ilość wolnego miejsca na dysku twardym. Jeśli ma być przeznaczona dla usługi HDInsight, możesz są ograniczone przez wszystkie skojarzone rozmiar lub obliczeniowe ograniczenia. 

## <a name="algorithms-and-libraries"></a>Algorytmy i biblioteki

**Jakie algorytmy są obsługiwane w konsoli usługi Azure Machine Learning Workbench?**

Podgląd produktów i usług obejmują najlepiej społeczności typu open source. Firma Microsoft obsługuje szeroką gamę algorytmów i biblioteki w tym TensorFlow, scikit — Dowiedz się, Apache Spark i kognitywnych zestaw narzędzi firmy Microsoft. Azure Machine Learning Workbench również pakiety [Microsoft revoscalepy](https://docs.microsoft.com/sql/advanced-analytics/python/what-is-revoscalepy) pakietu.

**Jak związek między kognitywnych zestaw narzędzi firmy Microsoft Azure Machine Learning?**

[Kognitywnych zestaw narzędzi firmy Microsoft](https://www.microsoft.com/cognitive-toolkit/) jest jednym z wielu platform obsługiwanych przez naszych nowych narzędzi i usług. Kognitywnych Toolkit to ujednoliconego learning głębokiego pakiet narzędzi umożliwiający zużywają i połączyć maszyny popularnych głębokie sieci neuronowe do przodu źródła danych, Convolutional sieci, w tym modeli uczenia sekwencji do sekwencji i powtarzającego się sieci. Aby uzyskać więcej informacji na kognitywnych zestaw narzędzi firmy Microsoft można znaleźć w naszych [dokumentacji produktu](https://docs.microsoft.com/cognitive-toolkit/). 

## <a name="pricing-and-billing"></a>Cennik i rozliczenia

**Czy można opłat za usługi Azure Machine Learning wersji zapoznawczej?** 

Aplikacja Azure Machine Learning Workbench A: jest dostępna bezpłatnie do subskrybenci platformy Azure. Model zarządzania i usługi eksperymenty oferują warstwy bezpłatna, oprócz warstw płatnych będzie avialable rabatem w publicznej wersji zapoznawczej.

**Zostanie I być naliczane na podstawie eksperymentów ile uruchomić?**

Nie. Usługa Eksperymentowanie umożliwia wykonanie dowolnej liczby eksperymentów w zależności od potrzeb, a opłaty są naliczane wyłącznie na podstawie liczby użytkowników. Opłaty za zasoby obliczeniowe usługi Eksperymentowanie są naliczane oddzielnie.  Firma Microsoft zachęca do wykonywania wielu eksperymenty w modelu najlepsze rozwiązania. 

**Jest nazywana będzie I naliczane na podstawie na ile razy moich usług sieci web?**

Nie. Usługi sieci Web można wywołać tak często, zgodnie z wymaganiami, bez konieczność zarządzania modelu rozliczeń. Masz pełną kontrolę nad skalowaniem swoich wdrożeń, aby spełniały wymagania aplikacji.

**Jak można skalować liczbę jednostek zakupionymi w pakiecie administracyjnym modelu Azure Machine Learning?**

Można zmienić liczbę jednostek, w górę lub w dół, za pomocą portalu Azure lub interfejsu wiersza polecenia. 

**Zostanie mojego rachunku jak wygląda?**

Opłaty są produkowane codziennie. Dla celów rozliczeniowych dzień rozpoczyna się o północy (czas UTC). Rachunki są generowane raz w miesiącu. Oddzielne jest obciążany dla wszystkich usług platformy Azure, używane w połączeniu z usługi Azure Machine Learning. Opłaty mogą obejmować, ale nie są ograniczone do: 
- Opłaty za obliczenia bazy danych
- HDInsight
- Azure Container Service
- Azure Container Registry 
- Azure Blob Storage
- Application Insights
- W usłudze Azure Key Vault
- Visual Studio Team Services
- Centrum zdarzeń platformy Azure
- Azure analizy strumienia dla bardziej szczegółowe informacje, lub aby wyświetlić zestawienie przykładowe, odwiedź stronę dotyczącą cen. 

## <a name="support-and-training"></a>Pomoc techniczna i szkolenia

**Gdzie można znaleźć szkolenia dotyczące usługi Azure Machine Learning?**

[Centrum dokumentacji usługi Azure Machine Learning](./overview-what-is-azure-ml.md) udostępnia samouczki wideo i przewodniki dotyczące wykonywania określonych zadań. Te przewodniki krok po kroku wprowadzić usług i wyjaśnić cyklu życia analizy danych. Stale wzbogacamy centrum usługi Machine Learning o nowe materiały. Można przesłać żądania dotyczące dodatkowych materiałów szkoleniowych na forum opinii użytkowników.

**Jak uzyskać pomoc techniczną dotyczącą usługi Azure Machine Learning?**

Aby uzyskać pomoc techniczną przejdź do obsługi usługi Azure, a następnie wybierz uczenia maszynowego. Azure Machine Learning udostępniono również aktywną społeczność [StackOverflow](https://stackoverflow.com/questions/tagged/azure-machine-learning) oznaczone przy użyciu "Azure-Machine-Learning", monitorowana przez zespół.  Sugestie i żądania funkcji można przesłać na [Azure Machine Learning opinii](https://feedback.azure.com/forums/257792-machine-learning) lokacji. 
