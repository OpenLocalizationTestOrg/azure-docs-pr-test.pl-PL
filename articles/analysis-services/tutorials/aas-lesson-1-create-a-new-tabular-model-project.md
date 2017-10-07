---
title: aaa "lekcji samouczka usług Azure Analysis Services 1: Tworzenie nowego projektu modelu tabelarycznego | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate nowe Azure Analysis Services projekt samouczka. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-06/01: owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>Lekcja 1. Tworzenie projektu modelu tabelarycznego

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji należy użyć programu SQL Server Data Tools (SSDT) toocreate nowy projekt modelu tabelarycznego na poziomie zgodności 1400 hello. Po utworzeniu nowego projektu będzie można rozpocząć dodawanie danych i tworzenie modelu. W tej lekcji daje również krótkie wprowadzenie toohello modelu tabelarycznego, środowisko w narzędzia SSDT tworzenia.  
  
Szacowany czas toocomplete tej lekcji: **10 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat jest Pierwsza lekcja hello w modelu tabelarycznego samouczek tworzenia. toocomplete to lekcja, istnieje kilka wymagań wstępnych należy toohave w miejscu. toolearn więcej, zobacz [usług Azure Analysis Services — samouczek Adventure Works](../tutorials/aas-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Tworzenie nowego projektu modelu tabelarycznego  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>toocreate nowy projekt modelu tabelarycznego  
  
1.  Programu SSDT na powitania **pliku** menu, kliknij przycisk **nowy** > **projektu**.  
  
2.  W hello **nowy projekt** okna dialogowego rozwiń **zainstalowana** > **Business Intelligence** > **usług Analysis Services**, a następnie kliknij przycisk **projektu tabelarycznego usług analizy**.  
  
3.  W **nazwa**, typ **sprzedaży Internet AW**, a następnie określ lokalizację plików projektu hello.  
  
    Domyślnie **Nazwa rozwiązania** jest hello takie same jak nazwa projektu hello; jednak, należy wpisać nazwę inne rozwiązanie.  
  
4.  Kliknij przycisk **OK**.  
  
5.  W hello **Projektant modelu tabelarycznego** okno dialogowe, wybierz opcję **zintegrowanego obszaru roboczego**.  
  
    obszar roboczy Hello jest hostowana baza danych modelu tabelarycznego z hello takie same nazwy co projekt hello podczas tworzenia modelu. Zintegrowane obszaru roboczego oznacza, że SSDT używa wbudowanego wystąpienia, eliminując hello tooinstall konieczność osobnego wystąpienia serwera usług Analysis Services tylko do tworzenia modelu.
      
6.  W polu **Poziom zgodności** wybierz pozycję **SQL Server 2017/Azure Analysis Services (1400)**.   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    Jeśli nie widzisz 2017 / Azure Analysis Services serwera SQL (1400) w listbox poziomu zgodności hello nie używasz hello najnowszej wersji programu SQL Server Data Tools. tooget hello najnowszej wersji, zobacz [narzędzia zainstalować danych programu SQL Server](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>Opis modelu tabelarycznego SSDT hello środowisko tworzenia  
Teraz, po utworzeniu nowego projektu modelu tabelarycznego, wytłumaczone obecnie tooexplore hello modelu tabelarycznego środowisko w narzędzia SSDT tworzenia.  
  
Utworzony projekt zostanie otwarty w programie SSDT. Na powitania po prawej stronie w **Eksplorator modelu tabelarycznego**, zostanie wyświetlony widok drzewa obiektów hello w modelu. Ponieważ danych jeszcze nie zostały zaimportowane, foldery hello są puste. Możesz kliknąć prawym przyciskiem myszy obiekt folderu tooperform akcje, podobne paska menu toohello. Podczas wykonywania kroków opisanych w tym samouczku użyjesz hello Eksplorator modelu tabelarycznego toonavigate różnych obiektów w projekcie modelu.

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

Kliknij przycisk hello **Eksploratora rozwiązań** kartę. Widoczny będzie plik **Model.bim**. Jeśli nie widzisz hello okno projektanta toohello lewej (hello puste okno z kartą Model.bim hello), w **Eksploratora rozwiązań**w obszarze **AW Internet sprzedaży projektu**, kliknij dwukrotnie hello  **Model.bim** pliku. Plik Model.bim Hello zawiera hello metadanych dla modelu projektu. 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
Kliknij plik **Model.bim**. W hello **właściwości** wyświetlane właściwości modelu hello, najważniejsze jest hello **trybu zapytania bezpośredniego** właściwości. Ta właściwość określa, czy hello model jest wdrożony w trybie w pamięci (wyłączone) lub w trybie zapytania bezpośredniego (włączone). Na potrzeby tego samouczka utworzysz i wdrożysz model w trybie w pamięci.

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
Po utworzeniu projektu modelu niektórych właściwości modelu są ustawiane automatycznie zgodnie z toohello ustawienia modelowania danych, które można określić w hello **narzędzia** menu > **opcje** okno dialogowe. Właściwości danych kopii zapasowej, przechowywanie obszaru roboczego i serwer obszaru roboczego Określ sposób i gdzie hello bazy danych obszaru roboczego (model tworzenia bazy danych) jest wykonywana kopia zapasowa, przechowywane w pamięci i skompilowany. W razie potrzeby możesz zmienić te ustawienia później, ale na razie pozostaw je bez zmian.  

W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy projekt **AW Internet Sales** (Sprzedaż internetowa AW), a następnie kliknij przycisk **Właściwości**. Witaj **strony właściwości sprzedaży Internet AW** zostanie wyświetlone okno dialogowe. Niektóre z tych właściwości ustawisz później podczas wdrażania modelu.  
  
Po zainstalowaniu narzędzi SSDT, środowiska Visual Studio toohello dodano kilka nowych elementów menu. Kliknij przycisk hello **modelu** menu. W tym miejscu można importować dane, odświeżanie danych obszaru roboczego, Przeglądaj modelu w programie Excel, Tworzenie perspektyw i ról, wybierz hello modelu widoku i ustaw opcje obliczania. Kliknij przycisk hello **tabeli** menu. Z poziomu tego menu możesz tworzyć relacje i zarządzać nimi, określać ustawienia tabeli dat, tworzyć partycje i edytować właściwości tabeli. Jeśli klikniesz przycisk hello **kolumny** menu, można dodać i usunąć kolumny w tabeli, blokowania kolumn i określić kolejność sortowania. Program SSDT dodaje również pewne pasek toohello przycisków. Najbardziej przydatne jest toocreate funkcja Autosumowania hello miary standardowe agregacji dla wybranej kolumny. Zapewniają innych przycisków paska narzędzi Szybki dostęp toofrequently użyć funkcji i poleceń.  
  
Poznaj niektóre z okien dialogowych hello i lokalizacje różne modele tabelaryczne tooauthoring określonych funkcji. Gdy niektóre elementy nie są jeszcze aktywne, możesz uzyskać dobrze hello modelu tabelarycznego środowisko tworzenia.  
  

## <a name="whats-next"></a>Co dalej?
[Lekcja 2. Pobieranie danych](../tutorials/aas-lesson-2-get-data.md).

  
  
  
