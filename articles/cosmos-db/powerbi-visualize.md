---
title: "Power BI samouczek bazy danych Azure rozwiązania Cosmos łącznika | Dokumentacja firmy Microsoft"
description: "W tym samouczku usługi Power BI umożliwia importowanie JSON i tworzenia raportów interesującego oraz wizualizuj dane przy użyciu łącznika DB rozwiązania Cosmos Azure i usługi Power BI."
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
ms.openlocfilehash: 6414cdc942c43f6eb13ca8f050d6503bdd3e0b42
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-the-power-bi-connector"></a>Power BI samouczek dla bazy danych Azure rozwiązania Cosmos: wizualizuj dane przy użyciu łącznika usługi Power BI
[Witrynie PowerBI.com](https://powerbi.microsoft.com/) to usługa online, których można tworzyć i udostępniać pulpity nawigacyjne i raporty z danych, które są istotne dla Ciebie i Twojej organizacji.  Power BI Desktop jest dedykowany raport narzędziu, która umożliwia pobieranie danych z różnych źródeł danych, scalić przekształcania danych, tworzenie zaawansowanych raportów i wizualizacje i opublikować raporty do usługi Power BI.  Do najnowszej wersji programu Power BI Desktop teraz można podłączyć do swojego konta rozwiązania Cosmos bazy danych za pośrednictwem łącznika DB rozwiązania Cosmos dla usługi Power BI.   

W tym samouczku usługi Power BI możemy wykonać kroki łączenie z kontem DB rozwiązania Cosmos w programie Power BI Desktop, przejdź do kolekcji, gdy chcemy, aby wyodrębnić dane przy użyciu nawigatora, Przekształć dane JSON w formacie tabelarycznym przy użyciu edytora zapytań Power BI Desktop, kompilacji i opublikowania raportu w witrynie PowerBI.com.

Ten samouczek usługi Power BI, będziesz mieć możliwość odpowiedzieć na następujące pytania:  

* Jak można utworzyć raportów z danymi z bazy danych rozwiązania Cosmos przy użyciu Power BI Desktop?
* Jak można łączyć z kontem DB rozwiązania Cosmos w programie Power BI Desktop?
* Sposób pobierania danych z kolekcji w programie Power BI Desktop
* Jak można przekształcać zagnieżdżone dane JSON w programie Power BI Desktop
* Jak opublikować i udostępniać moje raporty w witrynie PowerBI.com?

> [!NOTE]
> Łącznik usługi Power BI dla bazy danych Azure rozwiązania Cosmos łączy się Power BI Desktop wyodrębniania i przekształcania danych. Następnie można opublikować raporty utworzone w programie Power BI Desktop w witrynie PowerBI.com. Bezpośrednie wyodrębniania i przekształcania danych Azure rozwiązania Cosmos bazy danych nie można wykonać w witrynie PowerBI.com. 

> [!NOTE]
> Aby połączyć bazy danych rozwiązania Cosmos Azure do usługi Power BI przy użyciu interfejsu API bazy danych MongoDB, należy użyć [sterownika ODBC bazy danych MongoDB Simba](http://www.simba.com/drivers/mongodb-odbc-jdbc/).

## <a name="prerequisites"></a>Wymagania wstępne
Przed wykonaniem instrukcji zawartych w tym samouczku usługi Power BI, upewnij się, że masz dostęp do następujących zasobów:

* [Najnowszą wersję programu Power BI Desktop](https://powerbi.microsoft.com/desktop).
* Dostęp do naszej demonstracyjna konta lub danych na koncie DB rozwiązania Cosmos.
  * Wersja demonstracyjna konta jest wypełniana swe dzieła dane wyświetlane w tym samouczku. To konto Pokaz nie jest związana żadnych umów SLA i jest przeznaczona wyłącznie w celach demonstracyjnych.  Firma Microsoft zarezerwować prawo do wprowadzania zmian do tej demonstracyjna konta, w tym, ale nie są ograniczone do zakończenia konta, modyfikowania klucza, ograniczanie dostępu do, zmienianie i usuwania danych, w dowolnym momencie bez wcześniejszego powiadomienia lub z powodu.
    * Adres URL: https://analytics.documents.azure.com
    * Klucz tylko do odczytu: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR + YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw ==
  * Lub, aby utworzyć konta użytkownika, zobacz [Tworzenie konta bazy danych DB rozwiązania Cosmos Azure przy użyciu portalu Azure](https://azure.microsoft.com/documentation/articles/create-account/). Następnie, aby uzyskać przykładowy swe dzieła danych, która jest podobna do co jest używana w tym samouczku (ale nie zawiera bloki GeoJSON), zobacz [lokacji NOAA](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) , a następnie zaimportować danych przy użyciu [narzędzia migracji danych bazy danych Azure rozwiązania Cosmos](import-data.md).

Aby udostępnić raportów w witrynie PowerBI.com, musi mieć konto w witrynie PowerBI.com.  Aby dowiedzieć się więcej o usłudze Power BI wolnego i usługi Power BI Pro, odwiedź stronę [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Zacznijmy
W tym samouczku teraz załóżmy, czy geologist bada wulkany na całym świecie.  Dane swe dzieła są przechowywane na koncie DB rozwiązania Cosmos i dokumentów JSON wygląda jak następujący przykładowy dokument.

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

Chcesz pobrać dane swe dzieła konto rozwiązania Cosmos bazy danych i wizualizacji danych w interaktywnego raportu usługi Power BI, takich jak następujący raport.

![Przez wykonanie kroków tego samouczka usługi Power BI z łącznikiem usługi Power BI, będziesz mieć możliwość wizualizuj dane z raportu programu Power BI Desktop swe dzieła](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Czy chcesz go wypróbować? Zacznijmy od początku.

1. Uruchom Power BI Desktop na stacji roboczej.
2. Po uruchomieniu Power BI Desktop, *powitalnej* ekran jest wyświetlany.
   
    ![Power BI Desktop startowa - łącznika usługi Power BI](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. Możesz **Pobierz dane**, zobacz **ostatnio używanymi źródłami**, lub **otwarte inne raporty** bezpośrednio z *powitalnej* ekranu.  Kliknij przycisk X w prawym górnym rogu, aby zamknąć ekran. **Raport** zostanie wyświetlony widok Power BI Desktop.
   
    ![Power BI Desktop widoku raportu - łącznika usługi Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Wybierz **Home** wstążki, a następnie kliknij przycisk **Pobierz dane**.  **Pobierz dane** okna powinna zostać wyświetlona.
5. Polecenie **Azure**, wybierz pozycję **Microsoft Azure DocumentDB (Beta)**, a następnie kliknij przycisk **Connect**. 

    ![Power BI Desktop Pobierz dane - łącznika usługi Power BI](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. Na **łącznika Podgląd** kliknij przycisk **Kontynuuj**. **Microsoft Azure DocumentDB Connect** zostanie wyświetlone okno.
7. Określ rozwiązania Cosmos DB punkt końcowy adres URL konta czy chcesz pobrać dane, jak pokazano poniżej, a następnie kliknij przycisk **OK**. Aby korzystać z konta użytkownika, można pobrać adresu URL w polu identyfikatora URI w  **[klucze](manage-account.md#keys)**  bloku portalu Azure. Aby użyć konta demonstracyjnej, wprowadź `https://analytics.documents.azure.com` dla adresu URL. 
   
    Puste nazwy bazy danych, nazwę kolekcji i instrukcji SQL, jak te pola są opcjonalne.  Zamiast tego nawigatora zostanie wykorzystany do wybierz bazę danych i kolekcję, aby określić, skąd pochodzą dane.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos bazy danych — okno połączenia pulpitu](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. Jeśli łączysz się ten punkt końcowy po raz pierwszy, zostanie wyświetlony monit o klucz konta. Dla konta użytkownika, należy pobrać klucza z **klucza podstawowego** polu  **[tylko do odczytu klucze](manage-account.md#keys)**  bloku portalu Azure. Dla konta pokaz klucz jest `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Wprowadź odpowiedni klucz, a następnie kliknij przycisk **Connect**.
   
    Firma Microsoft zaleca użycie klucza tylko do odczytu, podczas tworzenia raportów.  Uniemożliwi to niepotrzebnym ujawnieniem klucza głównego na potencjalne zagrożenia bezpieczeństwa. Klucz tylko do odczytu jest dostępny z [klucze](manage-account.md#keys) bloku portalu Azure lub można użyć informacji o koncie pokaz podanego powyżej.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — klucz konta](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Jeśli zostanie wyświetlony komunikat o błędzie informujący, "nie znaleziono określonej bazy danych." Zobacz obejście kroków w tym [problem w usłudze Power BI](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Jeśli konto jest pomyślnie połączony, **Nawigator** będą wyświetlane.  **Nawigator** zostaną wyświetlone listy baz danych w ramach konta.
10. Kliknij i rozwiń węzeł bazy danych, gdzie dane raportu będą pochodzić, jeśli używasz konta pokaz wybierz **volcanodb**.   
11. Teraz wybierz kolekcję, która będzie pobierać dane. Jeśli używasz konta demonstracyjnej, wybierz **volcano1**.
    
    W okienku Podgląd pokazuje listę **rekordu** elementów.  Dokument jest reprezentowany jako **rekordu** typu w usłudze Power BI. Podobnie zagnieżdżony blok w dokumencie JSON jest również **rekordu**.
    
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB - Navigator okna](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Kliknij przycisk **Edytuj** można uruchomić edytora zapytań w nowym oknie do przekształcania danych.

## <a name="flattening-and-transforming-json-documents"></a>Spłaszczanie i przekształcanie dokumentów JSON
1. Przełącz do okna edytora zapytań usługi Power BI, gdzie **dokumentu** kolumny w środkowym okienku.
   ![Power BI Desktop edytora zapytań w programie](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Polecenie expander w prawej części **dokumentu** nagłówka kolumny.  Menu kontekstowe z listy pól będą wyświetlane.  Wybierz pola, które są potrzebne do raportu, na przykład, nazwę swe dzieła, kraju, Region, lokalizacji, podniesienia uprawnień, typu, stanu i ostatniego wulkanu wiedzieć, a następnie kliknij **OK**.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — rozwiń dokumentów](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. W okienku Centrum zostaną wyświetlone Podgląd wyników z polami wybrane.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — spłaszczanie wyników](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. W naszym przykładzie właściwość lokalizacji jest blok GeoJSON w dokumencie.  Jak widać, lokalizacji jest reprezentowany jako **rekordu** typu w programie Power BI Desktop.  
5. Polecenie expander po prawej stronie lokalizacji nagłówka kolumny.  Menu kontekstowe z polami typu i współrzędnych będą wyświetlane.  Teraz wybierz pola współrzędnych i kliknij przycisk **OK**.
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB - rekordu lokalizacji](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. W okienku Centrum zawiera obecnie kolumnę współrzędne **listy** typu.  Jak pokazano na początku tego samouczka, GeoJSON dane w tym samouczku jest typu punktu współrzędne geograficzne wartości zapisane w tablicy współrzędnych.
   
    Element współrzędne [0] reprezentuje geograficzne, gdy szerokość reprezentuje współrzędne [1].
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB - listy współrzędnych](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. Do spłaszczenia tablicy współrzędne, utworzymy **kolumny niestandardowe** o nazwie LatLong.  Wybierz **Dodaj kolumnę** wstążki, a następnie kliknij polecenie **Dodaj kolumnę niestandardowe**.  **Dodaj kolumnę niestandardowe** okna powinna zostać wyświetlona.
8. Podaj nazwę dla nowej kolumny, np. LatLong.
9. Następnie określ formuły niestandardowej dla nowej kolumny.  W naszym przykładzie mamy łączenie współrzędne geograficzne wartości rozdzielonych przecinkami, jak pokazano poniżej przy użyciu następującej formuły: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Kliknij przycisk **OK**.
   
    Aby uzyskać więcej informacji na dane analizy wyrażenia (DAX) łącznie z funkcjami języka DAX, odwiedź stronę [podstawowe języka DAX w programie Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — Dodawanie kolumny niestandardowe](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. Teraz środkowym okienku zostaną wyświetlone w kolumnie LatLong wypełniane przy użyciu współrzędne geograficzne wartości rozdzielonych przecinkami.
    
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB - kolumny LatLong niestandardowe](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Jeśli zostanie wyświetlony błąd w nowej kolumnie, upewnij się, że zastosowane kroki w obszarze Ustawienia zapytania zgodne poniższej ilustracji:
    
    ![Zastosowane kroki należy źródła nawigacji, rozwinięta dokumentu, rozwinięty Document.Location, dodać niestandardowe](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Jeśli wszystkie czynności są różne, Usuń dodatkowe czynności, a następnie spróbuj ponownie dodać niestandardowe kolumny. 
11. Firma Microsoft została zakończona pomyślnie spłaszczanie dane w formacie tabelarycznym.  Możesz korzystać ze wszystkich funkcji dostępnych w edytorze zapytań do kształtu i Przekształć dane w bazie danych rozwiązania Cosmos.  Jeśli używasz próbki, należy zmienić typ danych dla podniesienia uprawnień na **liczby całkowitej** zmieniając **— typ danych** na **Home** wstążki.
    
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — Zmień typ kolumny](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Kliknij przycisk **zamknąć i zastosować** można zapisać danych modelu.
    
    ![Power BI samouczek dla łącznika usługi Power BI Azure rozwiązania Cosmos DB — Zamknij & Zastosuj](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-the-reports"></a>Tworzenie raportów
Power BI Desktop raportu widoku jest, gdzie można rozpocząć tworzenie raportów do wizualizacji danych.  Możesz utworzyć raporty przez przeciąganie i upuszczanie pól do **raport** kanwy.

![Power BI Desktop widoku raportu - łącznika usługi Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

W widoku raportu należy odnaleźć:

1. **Pola** okienka, jest to, gdy zostanie wyświetlona lista modeli danych z polami można użyć na potrzeby raportów.
2. **Wizualizacje** okienka. Raport może zawierać jedną lub wiele wizualizacji.  Wybierz typy visual dopasowanie potrzeb z **wizualizacje** okienka.
3. **Raport** kanwy, to gdy utworzysz wizualnych raportu.
4. **Raport** strony. Można dodać wiele stron raportu w programie Power BI Desktop.

Poniżej przedstawiono podstawowe kroki tworzenia prosty raport interaktywnego widoku mapy.

1. W naszym przykładzie utworzymy wskazuje lokalizację każdego swe dzieła widoku mapy.  W **wizualizacje** okienku kliknij typ visual mapy jako wyróżnione na zrzucie ekranu powyżej.  Powinien zostać wyświetlony typ visual mapy rysowane na **raport** kanwy.  **Wizualizacji** okienko również powinien być wyświetlany zestaw właściwości powiązanej z typem visual mapy.
2. Teraz, przeciągnij i upuść pola LatLong **pola** okienko, aby **lokalizacji** właściwości w **wizualizacje** okienka.
3. Następnie przeciągnij i upuść pola Nazwa swe dzieła **legendy** właściwości.  
4. Następnie, przeciągnij i upuść pola podniesienia uprawnień do **rozmiar** właściwości.  
5. Powinien zostać wyświetlony mapy visual przedstawiający zestaw bąbelków wskazującą lokalizację każdego swe dzieła Rozmiar bąbelka korelowanie do podniesienia swe dzieła.
6. Teraz utworzyć podstawowy raport.  Można dostosować raport, dodając więcej wizualizacji.  W naszym przykładzie dodano fragmentator typu swe dzieła dokonanie interaktywnego raportu.  
   
    ![Zrzut ekranu przedstawiający raport końcowy Power BI Desktop po zakończeniu tego samouczka usługi Power BI dla bazy danych Azure rozwiązania Cosmos](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Publikowanie i udostępnianie raportu
Aby udostępnić raport, musi mieć konto w witrynie PowerBI.com.

1. W programie Power BI Desktop, kliknij **Home** wstążki.
2. Kliknij przycisk **Opublikuj**.  Pojawi się monit o wprowadzenie nazwy użytkownika i hasło dla swojego konta w witrynie PowerBI.com.
3. Po uwierzytelnieniu poświadczeń raportu jest publikowany z wybranej lokalizacji docelowej.
4. Kliknij przycisk **Otwórz "PowerBITutorial.pbix" w usłudze Power BI** Zobacz i udostępnianie raport w witrynie PowerBI.com.
   
    ![Publikowanie Power BI sukcesu! Otwórz samouczek w usłudze Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Tworzenie pulpitu nawigacyjnego w witrynie PowerBI.com
Teraz, gdy masz raportu pozwala udostępnić go w witrynie PowerBI.com

Podczas publikowania z raportu programu Power BI Desktop do witryny PowerBI.com, generuje **raport** i **Dataset** w dzierżawie w witrynie PowerBI.com. Na przykład po opublikowaniu raportu o nazwie **PowerBITutorial** do witryny PowerBI.com, zobaczysz PowerBITutorial zarówno **raporty** i **zestawów danych** sekcje w witrynie PowerBI.com.

   ![Zrzut ekranu przedstawiający nowy raport i zestaw danych w witrynie PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

Aby utworzyć pulpit nawigacyjny zabezpieczać, kliknij przycisk **numeru Pin na żywo strony** przycisk w raporcie w witrynie PowerBI.com.

   ![Zrzut ekranu przedstawiający nowy raport i zestaw danych w witrynie PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Następnie postępuj zgodnie z instrukcjami [przypiąć Kafelek z raportu](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) do utworzenia nowego pulpitu nawigacyjnego. 

Przed utworzeniem pulpitu nawigacyjnego, można także utworzyć ad hoc zmiany do raportu. Zaleca się jednak użyć Power BI Desktop wykonywania zmiany i ponownie opublikować raport w witrynie powerbi.com.

## <a name="refresh-data-in-powerbicom"></a>Odświeżanie danych w witrynie PowerBI.com
Istnieją dwa sposoby, aby odświeżyć dane, jak i ad hoc zaplanowane.

Odświeżanie ad hoc, wystarczy kliknąć na eclipses (...) przez **Dataset**, np. PowerBITutorial. Możesz wyświetlić listę działań w tym **Odśwież teraz**. Kliknij przycisk **Odśwież teraz** odświeżania danych.

![Zrzut ekranu przedstawiający Odśwież teraz w witrynie PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

Zaplanowane odświeżanie wykonaj następujące czynności.

1. Kliknij przycisk **planowanie odświeżania** na liście akcji. 

    ![Zrzut ekranu przedstawiający Odśwież harmonogramu w witrynie PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. W **ustawienia** rozwiń pozycję **poświadczenia źródła danych**. 
3. Polecenie **Edycja poświadczeń**. 
   
    Pojawi się okno podręczne Konfigurowanie. 
4. Wprowadź klucz, aby nawiązać połączenie konto rozwiązania Cosmos bazy danych dla tego zestawu danych, a następnie kliknij przycisk **Zaloguj**. 
5. Rozwiń węzeł **planowanie odświeżania** i skonfigurować harmonogram do odświeżenia zestawu danych. 
6. Kliknij przycisk **Zastosuj** i zakończeniu konfigurowania zaplanowanego odświeżania.

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej o usłudze Power BI, zobacz [wprowadzenie do usługi Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* Aby dowiedzieć się więcej na temat rozwiązania Cosmos bazy danych, zobacz [strony docelowej dokumentacji bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/documentation/services/cosmos-db/).

