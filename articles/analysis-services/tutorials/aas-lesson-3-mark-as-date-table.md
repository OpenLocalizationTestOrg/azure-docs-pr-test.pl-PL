---
title: aaa "lekcji samouczka usług Azure Analysis Services 3: Oznacz jako tabelę dat | Opis elementu Microsoft Docs": w tym artykule opisano, jak toomark datę w tabeli projekt samouczka hello Azure Analysis Services. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-06/01: owend
---
# <a name="lesson-3-mark-as-date-table"></a>Lekcja 3. Oznaczanie jako tabeli dat

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W lekcji 2 dotyczącej pobierania danych została zaimportowana tabela wymiarów o nazwie DimDate. W modelu tabela ta nosi nazwę DimDate, ale jest również nazywana *tabelą dat*, ponieważ zawiera dane dotyczące dat i godzin.  
  
Zawsze gdy używasz funkcji analizy czasowej języka DAX (np. podczas opisanego poniżej tworzenia miar), należy określić właściwości, które obejmują *tabelę dat* i unikatowy identyfikator *kolumny dat* w tej tabeli.
  
W tej lekcji oznaczyć hello DimDate tabeli jako hello *tabelę dat* i kolumnę dat hello (w tabeli danych hello) jako hello *kolumnę dat* (unikatowy identyfikator).  

Zanim oznaczenie kolumny tabeli i Data Data hello jest toodo odpowiedni moment, nieco housekeeping toomake Twojego toounderstand łatwiejsze modelu. Zwróć uwagę, w tabeli DimDate hello kolumny o nazwie **FullDateAlternateKey**. Ta kolumna zawiera jeden wiersz dla każdego dnia w każdym roku kalendarzowym uwzględnione w tabeli hello. Ta kolumna jest bardzo często używana w formułach miar i w raportach. Jednak „FullDateAlternateKey” nie jest najlepszym identyfikatorem dla tej kolumny. Możesz zmienić jego nazwę za**data**, dzięki czemu można łatwiej tooidentify i obejmują w formułach. Jeśli to możliwe, jest toorename dobrze obiekty takie jak tabele i kolumny toomake je łatwiej tooidentify SSDT i klientach raportowania aplikacji, takich jak usługi Power BI i Excel. 
  
Szacowany czas toocomplete tej lekcji: **trzy minuty**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [Lekcja 2: pobieranie danych](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>toorename hello FullDateAlternateKey kolumny

1.  W Konstruktorze modelu powitania kliknij hello **DimDate** tabeli.

2.  Kliknij dwukrotnie nagłówek hello hello **FullDateAlternateKey** kolumny, a następnie zmień zbyt**data**.

  
### <a name="tooset-mark-as-date-table"></a>tooset Oznacz jako tabela dat.  
  
1.  Wybierz hello **data** kolumny, a następnie w hello **właściwości** okna, w obszarze **— typ danych**, upewnij się, że **data** wybrano.  
  
2.  Kliknij hello **tabeli** menu, następnie kliknij przycisk **data**, a następnie kliknij przycisk **Oznacz jako tabelę dat**.  
  
3.  W hello **Oznacz jako tabelę dat** okno dialogowe, w hello **data** listbox, zaznacz hello **data** kolumny hello Unikatowy identyfikator. Zazwyczaj jest ona zaznaczona domyślnie. Kliknij przycisk **OK**. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>Co dalej?
[Lekcja 4. Tworzenie relacji](../tutorials/aas-lesson-4-create-relationships.md).
  
