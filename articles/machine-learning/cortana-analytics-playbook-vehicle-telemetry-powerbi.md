---
title: aaaPower BI pulpit nawigacyjny kondycji vehicle i kierowania zwyczaje - Azure | Dokumentacja firmy Microsoft
description: "Korzystanie z możliwości hello wgląd w czasie rzeczywistym oraz predykcyjnej toogain Cortana Intelligence na kondycji vehicle i wspierającym zwyczaje."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>Instrukcje instalacji pulpitu nawigacyjnego programu Power BI szablon rozwiązania vehicle telemetrii analityka
To **menu** toohello rozdziałów tego podręcznika dotyczącego łączy. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

ilustrację Hello rozwiązania analizy Telemetrii Vehicle jak przedstawicielstw samochodu handlowych, producentów samochodów i ubezpieczeń mogą korzystać z możliwości hello Cortana Intelligence toogain w czasie rzeczywistym oraz predykcyjnej rozeznanie vehicle kondycji i wspierającym ulepszenia toodrive zwyczaje w obszarze powitania klienta wystąpić R & D i kampanii marketingowych. Ten dokument zawiera instrukcje krok po kroku dotyczące sposobu konfigurowania raportów usługi Power BI hello i pulpitu nawigacyjnego po wdrożeniu rozwiązania hello w ramach subskrypcji. 

## <a name="prerequisites"></a>Wymagania wstępne
1. Wdrażanie hello [analizy Telemetrii](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) rozwiązania  
2. [Zainstaluj program Microsoft Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331)
3. [Subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/). Jeśli nie masz subskrypcji platformy Azure, Rozpoczynanie pracy z bezpłatnej subskrypcji Azure
4. Konto usługi Microsoft Power BI

## <a name="cortana-intelligence-suite-components"></a>Składników pakietu Cortana Intelligence
W ramach szablon rozwiązania analizy Telemetrii Vehicle hello hello następujące usługi Cortana Intelligence są wdrażane w ramach subskrypcji.

* **Centrum zdarzeń** służy do wprowadzania miliony zdarzeń telemetrii vehicle na platformie Azure.
* **Analiza strumienia** do uzyskania wgląd w czasie rzeczywistym w kondycję vehicle i będzie się powtarzał tych danych do długoterminowego przechowywania dla bardziej zaawansowane funkcje analizy partii.
* **Machine Learning** wykrywania anomalii w czasie rzeczywistym i insights predykcyjnej toogain przetwarzania wsadowego.
* **HDInsight** jest wykorzystywana tootransform danych na dużą skalę
* **Fabryka danych** obsługuje aranżacji, potoku przetwarzania wsadowego hello monitorowania i planowania zarządzania zasobami.

**Power BI** daje to rozwiązanie sformatowanego pulpitu nawigacyjnego w czasie rzeczywistym danych i wizualizacji analizy predykcyjnej. 

rozwiązanie Hello używa dwóch różnych źródeł danych: **symulowane sygnały vehicle i danych diagnostycznych** i **katalogu vehicle**.

Symulator telematyki vehicle wchodzi w skład tego rozwiązania. Emituje informacje diagnostyczne, a sygnały odpowiadający mu stan toohello hello vehicle i kierowania wzorca w danym punkcie w czasie. 

Witaj Vehicle katalogu jest odwołanie do zestawu danych zawierającego VIN toomodel mapowania

## <a name="power-bi-dashboard-preparation"></a>Power BI pulpitu nawigacyjnego przygotowania
### <a name="setup-power-bi-real-time-dashboard"></a>Pulpit nawigacyjny Instalatora Power BI w czasie rzeczywistym

**Uruchom aplikację w czasie rzeczywistym pulpitu nawigacyjnego hello** po zakończeniu wdrażania hello należy wykonać instrukcje działania ręcznego hello

* Pobierz aplikację pulpitu nawigacyjnego w czasie rzeczywistym RealtimeDashboardApp.zip i Rozpakuj go.
*  W folderze rozpakowane hello należy otworzyć pliku konfiguracji aplikacji 'RealtimeDashboardApp.exe.config' appSettings Zamień połączeń usługi Eventhub, magazynu obiektów Blob i ML wartościami hello w hello instrukcje działania ręcznego, a następnie zapisz zmiany.
* Uruchom aplikację RealtimeDashboardApp.exe. Podręczne, podaj prawidłowe poświadczenia usługi Power Bi i kliknij przycisk hello okna logowania **Akceptuj** przycisku. Następnie aplikacja hello rozpocznie toorun.

   ![Logowanie tooPower analizy Biznesowej](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI pulpitu nawigacyjnego uprawnień](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* Logowania tooPowerBI witryny sieci Web i utworzyć pulpit nawigacyjny w czasie rzeczywistym.

Teraz są tooconfigure gotowy pulpit nawigacyjny usługi Power BI hello z toogain zaawansowane wizualizacje w czasie rzeczywistym i zwyczaje predykcyjnej rozeznanie vehicle kondycji i wspierającym. Trwa około 45 minut tooan godzina toocreate hello wszystkich raportów i skonfigurować hello pulpitu nawigacyjnego. 

### <a name="configure-power-bi-reports"></a>Konfigurowanie raportów usługi Power BI
Witaj w czasie rzeczywistym raporty i pulpit nawigacyjny hello zająć o toocomplete 30-45 minut. Przeglądaj zbyt[http://powerbi.com](http://powerbi.com) i logowania.

![Logowanie tooPower analizy Biznesowej](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

Nowy zestaw danych jest generowany w usłudze Power BI. Kliknij przycisk hello **ConnectedCarsRealtime** zestawu danych.

![Zestaw danych w czasie rzeczywistym samochodów połączone zaznaczeniu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Zapisz przy użyciu pustego raportu hello **Ctrl + s**.

![Zapisz raport puste](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

Podaj nazwę raportu *Vehicle Telemetrii Analytics online w czasie rzeczywistym - raporty*.

![Podaj nazwę raportu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>Raporty w czasie rzeczywistym
Istnieją trzy raporty w czasie rzeczywistym, w tym rozwiązaniu:

1. Pojazdów w operacji
2. Pojazdów wymagających konserwacji
3. Statystyki kondycji pojazdów

Wybierz tooconfigure wszystkie hello trzy raporty w czasie rzeczywistym lub po każdym etapie i kontynuować toohello następnej sekcji konfiguracji hello partii raportów. Zalecamy toocreate wszystkie hello trzy raporty toovisualize hello pełny wgląd hello ścieżki w czasie rzeczywistym hello rozwiązania.  

### <a name="1-vehicles-in-operation"></a>1. Pojazdów w operacji
Kliknij dwukrotnie **strona 1** i zmień jego nazwę za "Pojazdów w operacji"  
    ![Połączone samochodów - pojazdów w operacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

Wybierz **vin** pola **pola** i wybierz typ wizualizacji jako **"Karta"**.  

Wizualizacja karty jest tworzony, jak pokazano na rysunku.  
    ![Połączone samochodów — wybierz vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.  

Wybierz **miasta** i **vin** z pól. Zmień wizualizacji zbyt**"Map"**. Przeciągnij **vin** w obszarze wartości. Przeciągnij **miasta** z pól zbyt**legendy** obszaru.   
    ![Połączone samochodów — karta wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

Wybierz **format** sekcji z **wizualizacje**, kliknij przycisk **tytuł** i zmień hello **tekst** zbyt**"pojazdów Operacja przez Miasto"**.  
    ![Połączone samochodów - pojazdów w operacji przez miasta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

Wizualizacja końcowego wygląda jak pokazano na rysunku.    
    ![Połączone samochodów - końcowego wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.  

Wybierz **miasta** i **vin**, Zmień typ wizualizacji zbyt**wykres kolumnowy grupowany**. Upewnij się, **miasta** w **osi obszaru** i **vin** w **wartość obszaru**  

Wykres sortowania według **"Liczba vin"**  
    ![Połączone samochodów — liczba vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

Zmień wykres **tytuł** zbyt**"Pojazdów w operacji według miast."**  

Kliknij hello **Format** sekcji, a następnie wybierz **kolory danych**, kliknij przycisk hello **"Na"** zbyt**Pokaż wszystko**  
    ![Połączone samochodów — Pokaż wszystkie kolory danych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

Zmiana koloru hello poszczególnych Miasto, klikając ikonę kolorów.  
    ![Połączone samochodów - Zmienianie kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.  

Wybierz **wykres kolumnowy grupowany** wizualizacji z wizualizacji, przeciągnij **miasta** w **osi** obszarze **modelu** w **Legendy** obszaru i **vin** w **wartość** obszaru.  
    ![Połączone samochodów - kolumnowy grupowany](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Połączone samochodów - renderowania](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

Rozmieszczanie wszystkich wizualizacji na tej stronie, jak pokazano na rysunku.  
    ![Połączone samochodów - wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

Raport w czasie rzeczywistym "Pojazdów w operacji" hello została pomyślnie skonfigurowana. Można kontynuować toocreate hello dalej raportu w czasie rzeczywistym lub zatrzymać w tym miejscu i skonfigurować hello pulpitu nawigacyjnego. 

### <a name="2-vehicles-requiring-maintenance"></a>2. Pojazdów wymagających konserwacji
Kliknij przycisk ![Dodaj](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nowy raport, zmień jego nazwę zbyt**"Pojazdów wymagających obsługi"**

![Połączone samochodów - pojazdów wymagających konserwacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

Wybierz **vin** pól i zmień typ wizualizacji zbyt**karty**.  
    ![Połączone samochodów — karta Vin wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

Mamy pole o nazwie "MaintenanceLabel" w zestawie danych hello. To pole może mieć wartość "0" lub "1"." Ta wartość jest ustawiana przez hello Azure Machine Learning model udostępniane w ramach rozwiązania i zintegrowane z hello ścieżki w czasie rzeczywistym. Witaj, wartość "1" oznacza, że vehicle wymaga konserwacji. 

tooadd **poziomu strony** filtr przedstawiający pojazdów danych, które wymagają obsługi: 

1. Przeciągnij hello **"MaintenanceLabel"** pole do **filtrów stron poziomu**.  
   ![Połączone samochodów — filtry poziomu strony](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. Kliknij przycisk **podstawowe filtrowanie** w dolnej części filtru poziomu strony MaintenanceLabel menu.  
   ![Połączone samochodów — podstawowe filtrowanie](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. Ustaw dla niego wartość filtru zbyt**"1"**    
   ![Połączone samochodów — wartość filtru](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.  

Wybierz **wykres kolumnowy grupowany** z wizualizacji  
![Połączone samochodów — karta Vind wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Połączone samochodów - kolumnowy grupowany](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

Przeciągnij pole **modelu** do **osi** obszarze **Vin** za**wartość** obszaru. Następnie Sortuj wizualizacji przez **liczba vin**.  Zmień wykres **tytuł** zbyt**"Pojazdów wymagających obsługi przez model"**  

Przeciągnij **vin** pól do **nasycenie kolorów** w **pola** ![pola](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) sekcji **wizualizacji**kartę  
![Połączone samochodów - nasycenie kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

Zmień **kolory danych** w wizualizacji z **Format** sekcji  
Zmień kolor Minimum: **F2C812**  
Zmień kolor wartości maksymalnej do: **FF6300**  
![Połączone samochodów — zmiany kolorów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Połączone samochodów — nowe kolory wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.  

Wybierz **klastrowanych kolumnowy** z wizualizacji, przeciągnij **vin** pole do **wartość** obszaru, przeciągnij **miasta** pole do **Osi** obszaru. Wykres sortowania przez **"Liczba vin"**. Zmień wykres **tytuł** zbyt**"Pojazdów wymagających obsługi przez Miasto"**   
![Połączone samochodów - pojazdów wymagających obsługi przez miasta](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.  

Wybierz **karty wielowierszowych** wizualizacji z wizualizacji, przeciągnij **modelu** i **vin** do hello **pola** obszaru.  
![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Zmienianie rozmieszczenia wszystkie hello wizualizacji, raport końcowy hello wygląda następująco:  
![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

Raport w czasie rzeczywistym "Pojazdów wymagających obsługi" hello została pomyślnie skonfigurowana. Można kontynuować toocreate hello dalej raportu w czasie rzeczywistym lub zatrzymać w tym miejscu i skonfigurować hello pulpitu nawigacyjnego. 

### <a name="3-vehicles-health-statistics"></a>3. Statystyki kondycji pojazdów
Kliknij przycisk ![Dodaj](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nowy raport, zmień jego nazwę zbyt**"Statystyki kondycji pojazdów"**  

Wybierz **miernika** wizualizacji z wizualizacji, a następnie przeciągnij hello **szybkości** pole do **wartości, wartość minimalna, wartość maksymalna** obszarów.  
![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

Zmienić domyślne hello agregacji **szybkości** w **wartość obszaru** zbyt**średni** 

Zmienić domyślne hello agregacji **szybkości** w **obszar minimalny** zbyt**minimalna**

Zmienić domyślne hello agregacji **szybkości** w **maksymalny obszar** zbyt**maksymalna**

![Połączone samochodów — karta wielowierszowych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Zmień nazwę hello **tytuł miernika** zbyt**"Średnia szybkość"** 

![Połączone samochodów - miernika](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.  

Podobnie dodać **miernika** dla **średni wydobycie ropy naftowej aparat**, **średni paliwa**, i **aparat średnia temperatura**.  

Zmień hello domyślnej agregacji pól w każdym miernika zgodnie powyżej kroki opisane w **"Średnia szybkość"** miernika.

![Połączone samochodów - mierników](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.

Wybierz **liniowy i kolumnowy grupowany** z wizualizacji, przeciągnij **miasta** pole do **udostępnionych osi**, przeciągnij **szybkości**, **pól tirepressure i engineoil** do **wartości w kolumnie** obszaru, zmień ich typ agregacji zbyt**średni**. 

Przeciągnij hello **engineTemperature** pole do **wartości wiersza** obszaru, Zmień typ agregacji hello zbyt**średni**. 

![Połączone samochodów - pola wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

Zmień wykres hello **tytuł** za**"Średnia szybkość, opona wykorzystania, aparat wydobycie ropy naftowej i temperatury aparat"**.  

![Połączone samochodów - pola wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.

Wybierz **właściwości** wizualizacji z wizualizacji, przeciągnij hello **modelu** pole do hello **grupy** obszarów i pól hello przeciągania  **MaintenanceProbability** do hello **wartości** obszaru.

Zmień wykres hello **tytuł** za**"Modele pojazdów wymagających obsługi"**.

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.

Wybierz **100% skumulowany wykres słupkowy** z wizualizacji, przeciągnij hello **miasta** pole do hello **osi** obszaru i przeciągnij hello **MaintenanceProbability**, **RecallProbability** pola na powitania **wartość** obszaru.

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

Kliknij przycisk **Format**, wybierz pozycję **kolory danych**i ustaw hello **MaintenanceProbability** toohello wartości koloru **"F2C80F"**.

Zmień hello **tytuł** z hello wykresu za**"Prawdopodobieństwo z Vehicle konserwacji & Wycofaj przez Miasto"**.

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

Kliknij przycisk hello pusty obszar tooadd nowej wizualizacji.

Wybierz **wykres warstwowy** z wizualizacji z wizualizacji, przeciągnij hello **modelu** pole do hello **osi** obszaru i przeciągnij hello **engineOil, tirepressure, szybkość i MaintenanceProbability** pola na powitania **wartości** obszaru. Zmień ich typ agregacji zbyt**"Średni"**. 

![Połączone samochodów — Zmień typ agregacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Zmień tytuł hello wykresu hello zbyt**"Średni aparat wydobycie ropy naftowej, opona prawdopodobieństwo wykorzystania, szybkość i konserwacja przez model"**.

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Kliknij hello pusty obszar tooadd nowej wizualizacji:

1. Wybierz **wykres punktowy** wizualizacji z wizualizacji.
2. Przeciągnij hello **modelu** pole do hello **szczegóły** i **legendy** obszaru.
3. Przeciągnij hello **paliwa** pole do hello **osi x** obszaru, zmień agregacji hello zbyt**średni**.
4. Przeciągnij **engineTemparature** do **osi y obszaru**, zmień agregacji hello zbyt**średni**
5. Przeciągnij hello **vin** pole do hello **rozmiar** obszaru.

![Połączone samochodów — Dodawanie nowej wizualizacji](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

Zmień wykres hello **tytuł** za**"Średnie paliwa, aparat temperatury przez Model"**.

![Połączone samochodów — Zmień tytuł wykresu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

raport końcowy Hello będzie wyglądać jak pokazano poniżej.

![Połączony raport końcowy samochodów](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>Wizualizacje numeru PIN z pulpitu nawigacyjnego hello raporty toohello w czasie rzeczywistym
Utwórz pusty pulpit nawigacyjny, klikając hello plus ikona tooDashboards dalej. Można określić nazwę "Pulpitu nawigacyjnego Analytics Vehicle Telemetrii"

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

Wizualizacja PIN hello z hello powyżej toohello raporty w pulpicie nawigacyjnym. 

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

pulpit nawigacyjny Hello powinna wyglądać następująco po wszystkich hello, które są tworzone trzy raporty i hello odpowiadającego wizualizacje przypiętych toohello pulpitu nawigacyjnego. Jeśli nie utworzono wszystkich raportów hello, pulpit nawigacyjny może wyglądać inaczej. 

![Połączone samochodów pulpitu nawigacyjnego](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

Gratulacje! Pomyślnie utworzono hello w czasie rzeczywistym pulpitu nawigacyjnego. Kontynuując tooexecute CarEventGenerator.exe i RealtimeDashboardApp.exe, powinny pojawić się aktualizacje na żywo na powitania pulpitu nawigacyjnego. Powinien upłynąć hello toocomplete too15 około 10 minut z następujące kroki.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Konfiguracja pulpitu nawigacyjnego przetwarzania wsadowego usługi Power BI
> [!NOTE]
> Trwa około dwie godziny (od hello pomyślnego wdrożenia hello) dla partii tooend zakończenia hello przetwarzania potoku toofinish wykonywania, a przetworzyć wygenerowanych danych, przez które roku. Dlatego poczekaj hello przetwarzania toofinish przed kontynuowaniem hello następne kroki. 
> 
> 

**Pobierz plik projektanta usługi Power BI hello**

* Wstępnie skonfigurowane pliku projektanta usługi Power BI wchodzi w skład wdrożenia hello instrukcje działania ręczne
* Poszukaj 2. Instalator usługi Power BI partii przetwarzania w pulpicie nawigacyjnym możesz pobrać hello szablonu usługi Power BI dla pulpitu nawigacyjnego przetwarzania wsadowego nosi nazwę **ConnectedCarsPbiReport.pbix**.
* Zapisz lokalnie

**Konfigurowanie raportów usługi Power BI**

* Otwórz hello pliku projektanta "**ConnectedCarsPbiReport.pbix**" przy użyciu Power BI Desktop. Jeśli nie już zainstalujesz hello Power BI Desktop z [instalacji Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331). 
* Kliknij przycisk hello **edytowanie zapytań**.

![Edytuj zapytanie usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Kliknij dwukrotnie hello **źródła**.

![Źródło usługi Power BI zbioru](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Zaktualizuj parametry połączenia serwera z hello Azure SQL server, które uzyskano udostępnione jako część wdrożenia hello.  Szukaj w instrukcjach operacji ręcznego hello w obszarze 

    4. Usługa Azure SQL Database
    
    * Serwer: somethingsrv.database.windows.net
    * Baza danych: connectedcar
    * Nazwa użytkownika: nazwa użytkownika
    * Hasło: Hasło programu SQL server można zarządzać z portalu Azure

* Pozostaw **bazy danych** jako *connectedcar*.

![Ustaw bazę danych usługi Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* Kliknij przycisk **OK**.
* Zobaczysz **poświadczenia systemu Windows** kartę domyślnie zaznaczone, zmień ją za**bazy danych poświadczeń** , klikając **bazy danych** kartę w prawym rogu.
* Podaj hello **Username** i **hasło** Twojej bazy danych SQL Azure, która została określona podczas jego wdrażania instalacji.

![Podaj poświadczenia bazy danych](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* Kliknij przycisk **połączenia**
* Powtórz hello powyżej kroki dla każdego hello trzy pozostałe zapytań w okienku po prawej stronie, a następnie zaktualizuj szczegóły połączenia źródła danych hello.
* Kliknij przycisk **Zamknij i załadować**. Power BI Desktop pliku z zestawów danych są tooSQL połączonych tabel bazy danych Azure.
* **Zamknij** pliku Power BI Desktop.

![Zamknij usługę Power BI desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* Kliknij przycisk **zapisać** przycisk toosave hello zmiany. 

Wszystkie raporty hello odpowiadającego ścieżka przetwarzania wsadowego toohello w rozwiązaniu hello został skonfigurowany. 

## <a name="upload-toopowerbicom"></a>Przekaż zbyt*witrynie powerbi.com*
1. Przejdź portalu sieci web usługi Power BI toohello http://powerbi.com i logowania.
2. Kliknij przycisk **pobieranie danych**  
3. Przekaż hello Power BI Desktop pliku.  
4. tooupload, kliknij przycisk **Pobierz dane -> pliki -> pliku lokalnego**  
5. Przejdź toohello **"**ConnectedCarsPbiReport.pbix**"**  
6. Po przekazaniu pliku hello można nawigować tooyour wstecz obszar roboczy usługi Power BI.  

Zestaw danych, raportów i pustego pulpitu nawigacyjnego zostanie utworzona automatycznie.  

Numer PIN wykresy nowego pulpitu nawigacyjnego tooa o nazwie **pulpitu nawigacyjnego Analytics Telemetrii Vehicle** w **usługi Power BI**. Kliknij pozycję puste pulpit nawigacyjny hello utworzone powyżej, a następnie przejdź toohello **raporty** kliknij sekcję hello nowo przekazać raportu.  

![Vehicle Telemetrii Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**Uwaga hello raport ma sześć stron:**  
Strona 1: Gęstość Vehicle  
Strona 2: Kondycja vehicle w czasie rzeczywistym  
Strona 3: Agresywnie zmiennych pojazdów   
4 strony: Pojazdów odwołane  
5 strony: Efektywne zmiennych pojazdów paliwa  
6 strony: Logo firmy Contoso  

![Połączone samochodów Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**Z 3 stron**, przypiąć hello następujące czynności:  

1. Liczba VIN  
   ![Połączone samochodów Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. Agresywnie zmiennych pojazdów przez model — wykresu wykresu kaskadowego  
   ![Vehicle Telemetrii - Pin wykresy 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**Od 5 strony**, przypiąć hello następujące czynności: 

1. Liczba vin    
   ![Vehicle Telemetrii - Pin wykresy 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. Paliwa pojazdów wydajne przez model: kolumnowy grupowany  
   ![Vehicle Telemetrii - Pin wykresy 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**Z 4 strony**, przypiąć hello następujące czynności:  

1. Liczba vin  
   ![Vehicle Telemetrii - Pin wykresy 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. Odwołane pojazdów miejscowość, model: właściwości  
   ![Vehicle Telemetrii - Pin wykresy 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**Od 6 do strony**, przypiąć hello następujące czynności:  

1. Logo firmy Contoso silniki  
   ![Vehicle Telemetrii - Pin wykresy 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Organizowanie hello pulpitu nawigacyjnego**  

1. Przejdź do pulpitu nawigacyjnego toohello
2. Umieść kursor nad każdym wykresu i zmień jego nazwę oparte na powitania nazewnictwa w hello pełny pulpit nawigacyjny obraz poniżej. Przenieś również wykresy hello wokół toolook, takich jak pulpit nawigacyjny hello poniżej.  
   ![Vehicle Telemetrii - organizowanie pulpitu nawigacyjnego 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetrii Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. Jeśli utworzono wszystkich raportów hello, jak wspomniano w tym dokumencie hello końcowego zakończonych pulpitu nawigacyjnego powinien wyglądać powitania po rysunku. 

![Vehicle Telemetrii - organizowanie pulpitu nawigacyjnego 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

Gratulacje! Pomyślnie utworzono hello raporty i hello toogain pulpitu nawigacyjnego w czasie rzeczywistym, predykcyjnej i zwyczaje rozeznanie partii vehicle kondycji i zwiększa.  
