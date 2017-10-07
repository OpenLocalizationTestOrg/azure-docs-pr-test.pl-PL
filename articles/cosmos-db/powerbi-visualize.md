---
title: "Samouczek BI aaaPower dla łącznika usługi Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka tooimport usługi Power BI JSON, tworzenie raportów interesującego i wizualizuj dane przy użyciu łącznika hello DB rozwiązania Cosmos Azure i usługi Power BI."
keywords: "Power samouczek analizy biznesowej, wizualizacji danych i zasilania łącznika analizy biznesowej"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Power BI samouczek dla bazy danych Azure rozwiązania Cosmos: wizualizuj dane przy użyciu łącznika usługi Power BI hello
[Witrynie PowerBI.com](https://powerbi.microsoft.com/) to usługa online, których można tworzyć i udostępniać pulpity nawigacyjne i raporty z danymi, które tooyou ważne i Twojej organizacji.  Power BI Desktop jest dedykowana narzędziu, która umożliwia tooretrieve danych raportu z różnych źródeł danych, scalić przekształcania danych hello, tworzenie zaawansowanych raportów i wizualizacje i opublikować hello tooPower raportów analizy Biznesowej.  Witaj najnowszej wersji programu Power BI Desktop teraz można podłączyć tooyour DB rozwiązania Cosmos konta za pośrednictwem łącznika DB rozwiązania Cosmos hello na usługę Power BI.   

W tym samouczku usługi Power BI możemy przeprowadzenie hello kroki tooconnect tooa konto bazy danych rozwiązania Cosmos w programie Power BI Desktop, przejdź kolekcji tooa, gdy chcemy tooextract hello danych przy użyciu hello Navigator, przekształcania danych JSON w formacie tabelarycznym za pomocą dodatku Power BI Desktop Query Edytor, tworzenie i publikowanie tooPowerBI.com raportu.

Po ukończeniu tego samouczka usługi Power BI, będziesz w stanie tooanswer hello następujące pytania:  

* Jak można utworzyć raportów z danymi z bazy danych rozwiązania Cosmos przy użyciu Power BI Desktop?
* Jak można łączyć konto bazy danych rozwiązania Cosmos tooa w programie Power BI Desktop?
* Sposób pobierania danych z kolekcji w programie Power BI Desktop
* Jak można przekształcać zagnieżdżone dane JSON w programie Power BI Desktop
* Jak opublikować i udostępniać moje raporty w witrynie PowerBI.com?

> [!NOTE]
> Łącznik usługi Power BI powitania dla bazy danych Azure rozwiązania Cosmos łączy tooPower BI Desktop wyodrębniania i przekształcania danych. Raporty utworzone w programie Power BI Desktop można następnie tooPowerBI.com opublikowane. Bezpośrednie wyodrębniania i przekształcania danych Azure rozwiązania Cosmos bazy danych nie można wykonać w witrynie PowerBI.com. 

## <a name="prerequisites"></a>Wymagania wstępne
Przed wykonaniem instrukcji hello w tym samouczku usługi Power BI, upewnij się, że masz dostęp toohello następujące zasoby:

* [Witaj najnowszej wersji programu Power BI Desktop](https://powerbi.microsoft.com/desktop).
* Konto pokaz tooour dostępu lub danych na koncie DB rozwiązania Cosmos.
  * Konto pokaz Hello jest wypełniana hello swe dzieła dane wyświetlane w tym samouczku. To konto Pokaz nie jest związana żadnych umów SLA i jest przeznaczona wyłącznie w celach demonstracyjnych.  Firma Microsoft zarezerwować hello prawo toomake modyfikacje toothis demonstracyjna konta w tym, ale nie tylko, przerywanie hello konta, modyfikowania klucza hello, ograniczanie dostępu do, zmienianie i usunąć dane hello, w dowolnym momencie bez wcześniejszego powiadomienia lub z powodu.
    * Adres URL: https://analytics.documents.azure.com
    * Klucz tylko do odczytu: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR + YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw ==
  * Lub toocreate konta użytkownika, zobacz [Tworzenie konta bazy danych DB rozwiązania Cosmos Azure przy użyciu portalu Azure hello](https://azure.microsoft.com/documentation/articles/create-account/). Następnie tooget przykładowych swe dzieła danych, które jest podobnego toowhat używane w tym samouczku (ale nie zawiera bloki GeoJSON hello), zobacz hello [lokacji NOAA](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) , a następnie zaimportować hello danych przy użyciu hello [migracji danych z bazy danych Azure rozwiązania Cosmos Narzędzie](import-data.md).

tooshare raportów w witrynie PowerBI.com, musi mieć konto w witrynie PowerBI.com.  toolearn więcej informacji na temat usługi Power BI do wolnego i Power BI Pro, odwiedź stronę [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Zacznijmy
W tym samouczku teraz załóżmy, czy geologist bada wulkany wokół hello world.  Witaj swe dzieła dane są przechowywane na koncie DB rozwiązania Cosmos i dokumentów JSON hello wyglądać powitania po przykładowy dokument.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

Ma tooretrieve hello swe dzieła danych z hello DB rozwiązania Cosmos konta i wizualizacji danych w interaktywnego raportu usługi Power BI, takich jak hello następującego raportu.

![Przez wykonanie kroków tego samouczka usługi Power BI z łącznikiem usługi Power BI hello, będziesz w stanie toovisualize danych za pomocą hello raportu swe dzieła Power BI Desktop](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Gotowe toogive it a spróbuj? Zacznijmy od początku.

1. Uruchom Power BI Desktop na stacji roboczej.
2. Po uruchomieniu Power BI Desktop, *powitalnej* ekran jest wyświetlany.
   
    ![Power BI Desktop startowa - łącznika usługi Power BI](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. Możesz **Pobierz dane**, zobacz **ostatnio używanymi źródłami**, lub **otwarte inne raporty** bezpośrednio z hello *powitalnej* ekranu.  Kliknij przycisk hello X na ekranie powitania tooclose hello w prawym górnym rogu. Witaj **raport** zostanie wyświetlony widok Power BI Desktop.
   
    ![Power BI Desktop widoku raportu - łącznika usługi Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Wybierz hello **Home** wstążki, a następnie kliknij przycisk **Pobierz dane**.  Witaj **Pobierz dane** okna powinna zostać wyświetlona.
5. Polecenie **Azure**, wybierz pozycję **Microsoft Azure DocumentDB (Beta)**, a następnie kliknij przycisk **Connect**. 

    ![Power BI Desktop Pobierz dane - łącznika usługi Power BI](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. Na powitania **łącznika Podgląd** kliknij przycisk **Kontynuuj**. Witaj **Microsoft Azure DocumentDB Connect** zostanie wyświetlone okno.
7. Określ hello DB rozwiązania Cosmos punkt końcowy adres URL konta będzie w sposób przedstawiony poniżej, takich jak dane hello tooretrieve z, a następnie kliknij **OK**. toouse własnego konta, możesz pobrać hello pole adresu URL z hello identyfikatora URI w hello  **[klucze](manage-account.md#keys)**  bloku hello portalu Azure. Witaj toouse demonstracją konta, wprowadź `https://analytics.documents.azure.com` hello adresu URL. 
   
    Puste hello Nazwa bazy danych, nazwę kolekcji i instrukcji SQL, jak te pola są opcjonalne.  Zamiast tego zostanie wykorzystany hello Navigator tooselect hello bazy danych i kolekcji tooidentify skąd pochodzą dane hello.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos bazy danych — okno połączenia pulpitu](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. Jeśli łączysz toothis punktu końcowego powitania po raz pierwszy, zostanie wyświetlony monit o hello klucz konta. Dla konta użytkownika, należy pobrać klucz hello z hello **klucza podstawowego** polu w hello  **[tylko do odczytu klucze](manage-account.md#keys)**  bloku hello portalu Azure. Dla konta pokaz hello, klucz hello jest `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Wprowadź hello odpowiedni klucz, a następnie kliknij przycisk **Connect**.
   
    Firma Microsoft zaleca użycie klucza tylko do odczytu hello podczas tworzenia raportów.  Uniemożliwi to niepotrzebnym ujawnieniem hello klucza głównego toopotential zagrożeń. klucz tylko do odczytu Hello jest dostępny z hello [klucze](manage-account.md#keys) bloku hello portalu Azure można również użyć hello: Pokaz informacje o koncie podanego powyżej.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — klucz konta](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Jeśli zostanie wyświetlony komunikat o błędzie informujący "hello określona baza danych nie został znaleziony." zobacz kroki rozwiązania hello na tym [problem w usłudze Power BI](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Kiedy konto hello pomyślnie nawiązuje połączenie, hello **Nawigator** będą wyświetlane.  Witaj **Nawigator** zostaną wyświetlone listy baz danych w ramach konta hello.
10. Kliknij i rozwiń hello bazy danych, gdzie hello danych dla raportu hello będą pochodzić, jeśli używasz konta pokaz hello, wybierz **volcanodb**.   
11. Teraz wybierz kolekcję, która pobierze dane hello z. Jeśli używasz konta pokaz hello wybierz **volcano1**.
    
    Okienko podglądu Hello pokazuje listę **rekordu** elementów.  Dokument jest reprezentowany jako **rekordu** typu w usłudze Power BI. Podobnie zagnieżdżony blok w dokumencie JSON jest również **rekordu**.
    
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB - Navigator okna](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Kliknij przycisk **Edytuj** toolaunch hello edytora zapytań w nowych danych hello tootransform okna.

## <a name="flattening-and-transforming-json-documents"></a>Spłaszczanie i przekształcanie dokumentów JSON
1. Przełącz toohello okno edytora zapytań usługi Power BI, gdzie hello **dokumentu** kolumny w okienku Centrum hello.
   ![Power BI Desktop edytora zapytań w programie](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Polecenie expander hello na powitania po prawej stronie powitania **dokumentu** nagłówka kolumny.  menu kontekstowe Hello z listy pól będą wyświetlane.  Wybierz hello pola, które są potrzebne do raportu, na przykład, nazwę swe dzieła, kraju, Region, lokalizacji, podniesienia uprawnień, typu, stanu i ostatniego wulkanu wiedzieć, a następnie kliknij **OK**.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — rozwiń dokumentów](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. Hello środkowym okienku wyświetlanie podglądu wyników hello hello pól.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — spłaszczanie wyników](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. W naszym przykładzie hello właściwość lokalizacji jest blok GeoJSON w dokumencie.  Jak widać, lokalizacji jest reprezentowany jako **rekordu** typu w programie Power BI Desktop.  
5. Polecenie expander hello nagłówek kolumny lokalizacji hello hello prawej strony.  menu kontekstowe Hello z polami typu i współrzędnych będą wyświetlane.  Teraz wybierz hello współrzędne pola i kliknij przycisk **OK**.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB - rekordu lokalizacji](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Witaj środkowym okienku zawiera obecnie kolumnę współrzędne **listy** typu.  Jak pokazano na początku hello samouczka hello, hello GeoJSON danych w tym samouczku jest typu punktu współrzędne geograficzne wartości zapisane w tablicy współrzędne hello.
   
    Hello współrzędne [0] elementu reprezentuje geograficzne podczas szerokości geograficznej reprezentuje współrzędne [1].
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB - listy współrzędnych](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. Witaj tooflatten koordynuje tablicy, utworzymy **kolumny niestandardowe** o nazwie LatLong.  Wybierz hello **Dodaj kolumnę** wstążki, a następnie kliknij polecenie **Dodaj kolumnę niestandardowe**.  Witaj **Dodaj kolumnę niestandardowe** okna powinna zostać wyświetlona.
8. Podaj nazwę hello nowej kolumny, np. LatLong.
9. Następnie określ hello formuły niestandardowej hello nowej kolumny.  W naszym przykładzie mamy połączyć hello współrzędne geograficzne wartości rozdzielonych przecinkami, jak pokazano poniżej przy użyciu następującej formuły hello: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Kliknij przycisk **OK**.
   
    Aby uzyskać więcej informacji na dane analizy wyrażenia (DAX) łącznie z funkcjami języka DAX, odwiedź stronę [podstawowe języka DAX w programie Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — Dodawanie kolumny niestandardowe](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. Teraz hello środkowym okienku wyświetli hello nową kolumnę LatLong wypełniane przy użyciu hello szerokości geograficznej i wartości długości geograficznej rozdzielonych przecinkami.
    
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB - kolumny LatLong niestandardowe](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Jeśli wystąpi błąd w nowej kolumnie hello, upewnij się, że kroki hello stosowane w obszarze Ustawienia zapytania zgodne hello następującej ilustracji:
    
    ![Zastosowane kroki należy źródła nawigacji, rozwinięta dokumentu, rozwinięty Document.Location, dodać niestandardowe](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Jeśli wszystkie czynności są różne, należy usunąć hello dodatkowych czynności, a następnie spróbuj ponownie dodać hello niestandardowych kolumny. 
11. Firma Microsoft została zakończona pomyślnie spłaszczania hello dane w formacie tabelarycznym.  Można wykorzystać wszystkie hello funkcje dostępne w hello tooshape edytora zapytań i Przekształć dane w bazie danych rozwiązania Cosmos.  Jeśli używasz próbki hello zmienić hello typu danych w celu podniesienia zbyt**liczby całkowitej** zmieniając hello **— typ danych** na powitania **Home** wstążki.
    
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — Zmień typ kolumny](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Kliknij przycisk **zamknąć i zastosować** toosave hello danych modelu.
    
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — Zamknij & Zastosuj](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>Tworzenie raportów hello
Power BI Desktop raportu widoku jest, której będzie można rozpocząć tworzenie raportów toovisualize danych.  Możesz utworzyć raporty przez przeciąganie i upuszczanie pól do hello **raport** kanwy.

![Power BI Desktop widoku raportu - łącznika usługi Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

W widoku raportu hello powinien znajdować się:

1. Witaj **pola** okienka, jest to, gdy zostanie wyświetlona lista modeli danych z polami można użyć na potrzeby raportów.
2. Witaj **wizualizacje** okienka. Raport może zawierać jedną lub wiele wizualizacji.  Wybierz typy visual hello dopasowanie potrzeb z hello **wizualizacje** okienka.
3. Hello **raport** kanwy, to gdy utworzysz hello elementy wizualne dla raportu.
4. Witaj **raport** strony. Można dodać wiele stron raportu w programie Power BI Desktop.

Oto Hello hello podstawowe kroki tworzenia prosty raport interaktywnego widoku mapy.

1. W naszym przykładzie utworzymy przedstawiający hello lokalizację każdego swe dzieła widoku mapy.  W hello **wizualizacje** okienku hello typ elementu wizualnego mapy jako wyróżnione na zrzucie ekranu hello powyżej, kliknij polecenie.  Powinien zostać wyświetlony typ visual mapy hello rysowane na powitania **raport** kanwy.  Witaj **wizualizacji** okienko również powinien być wyświetlany zestaw toohello powiązanych właściwości mapy typ elementu wizualnego.
2. Teraz, przeciągnij i upuść pola LatLong hello z hello **pola** toohello okienko **lokalizacji** właściwości w **wizualizacje** okienka.
3. Następnie przeciągnij i upuść hello swe dzieła nazwę pola toohello **legendy** właściwości.  
4. Następnie, przeciągnij i upuść hello podniesienia uprawnień pola toohello **rozmiar** właściwości.  
5. Powinna zostać wyświetlona hello visual przedstawiający zestaw bąbelków wskazującą lokalizację każdego swe dzieła hello hello Rozmiar bąbelka hello korelowanie toohello podniesienie swe dzieła hello mapy.
6. Teraz utworzyć podstawowy raport.  Można dostosować hello raportu, dodając więcej wizualizacji.  W naszym przykładzie dodano typu swe dzieła fragmentatora toomake hello raportu interaktywnego.  
   
    ![Zrzut ekranu przedstawiający raport końcowy Power BI Desktop powitania po zakończeniu samouczka hello usługi Power BI dla bazy danych Azure rozwiązania Cosmos](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Publikowanie i udostępnianie raportu
tooshare raport, użytkownik musi mieć konto w witrynie PowerBI.com.

1. W hello Power BI Desktop, kliknij na powitania **Home** wstążki.
2. Kliknij przycisk **Opublikuj**.  Zostanie wyświetlony monit o tooenter hello nazwę i hasło użytkownika będzie dla Twojego konta w witrynie PowerBI.com.
3. Po uwierzytelnieniu poświadczeń hello raportu hello jest wybranej lokalizacji opublikowanych tooyour docelowej.
4. Kliknij przycisk **Otwórz "PowerBITutorial.pbix" w usłudze Power BI** toosee i udostępniać raport w witrynie PowerBI.com.
   
    ![Publikowanie tooPower BI sukcesu! Otwórz samouczek w usłudze Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Tworzenie pulpitu nawigacyjnego w witrynie PowerBI.com
Teraz, gdy masz raportu pozwala udostępnić go w witrynie PowerBI.com

Podczas publikowania raportu z tooPowerBI.com Power BI Desktop generuje **raport** i **Dataset** w dzierżawie w witrynie PowerBI.com. Na przykład po opublikowaniu raportu o nazwie **PowerBITutorial** tooPowerBI.com, zobaczysz PowerBITutorial w obu hello **raporty** i **zestawów danych** sekcje na Witrynie PowerBI.com.

   ![Zrzut ekranu przedstawiający hello nowy raport i zestaw danych w witrynie PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate pulpit nawigacyjny zabezpieczać, kliknij przycisk hello **numeru Pin na żywo strony** przycisk w raporcie w witrynie PowerBI.com.

   ![Zrzut ekranu przedstawiający hello nowy raport i zestaw danych w witrynie PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Następnie postępuj zgodnie z instrukcjami hello [przypiąć Kafelek z raportu](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate nowego pulpitu nawigacyjnego. 

Można także utworzyć tooreport zmian ad hoc, przed utworzeniem pulpitu nawigacyjnego. Jednak zalecane jest, użyj Power BI Desktop tooperform hello modyfikacje, a następnie ponownie opublikować hello tooPowerBI.com raportu.

## <a name="refresh-data-in-powerbicom"></a>Odświeżanie danych w witrynie PowerBI.com
Istnieją dwa sposoby toorefresh danych, ad hoc i zaplanowane.

Odświeżanie ad hoc, wystarczy kliknąć na powitania eclipses (...) przez hello **Dataset**, np. PowerBITutorial. Możesz wyświetlić listę działań w tym **Odśwież teraz**. Kliknij przycisk **Odśwież teraz** toorefresh hello danych.

![Zrzut ekranu przedstawiający Odśwież teraz w witrynie PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

Zaplanowane odświeżanie hello następujące.

1. Kliknij przycisk **planowanie odświeżania** hello liście akcji. 

    ![Zrzut ekranu przedstawiający hello planowanie odświeżania w witrynie PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. W hello **ustawienia** rozwiń pozycję **poświadczenia źródła danych**. 
3. Polecenie **Edycja poświadczeń**. 
   
    pojawi się okno podręczne Konfiguruj Hello. 
4. Wprowadź hello klucza tooconnect toohello DB rozwiązania Cosmos konto dla tego zestawu danych, a następnie kliknij przycisk **Zaloguj**. 
5. Rozwiń węzeł **planowanie odświeżania** i skonfigurować harmonogram hello ma toorefresh hello dataset. 
6. Kliknij przycisk **Zastosuj** i zakończeniu konfigurowania hello zaplanowanego odświeżania.

## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn więcej informacji na temat usługi Power BI [wprowadzenie do usługi Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz hello [strony docelowej dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

