---
title: "aaaTesting hello wydajności usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Testowanie wydajności hello usługi w chmurze przy użyciu hello profilera Visual Studio"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>Testowanie wydajności hello usługi w chmurze
## <a name="overview"></a>Omówienie
Należy przetestować wydajność hello usługi w chmurze, w hello następujące sposoby:

* Używane diagnostyki Azure toocollect informacje dotyczące żądania i połączeń i statystyki witryny tooreview, które pokazują, jak usługa hello wykonuje z punktu widzenia klienta. tooget wprowadzenie, zobacz [Konfigurowanie diagnostyki dla usług Azure Cloud Services i maszyn wirtualnych](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Użyj tooget profilera Visual Studio hello dokładnych analiz hello obliczeniową aspektów działania hello usługi. Zgodnie z opisem w tym temacie, można użyć hello profilera toomeasure wydajności, jak działa usługa na platformie Azure. Uzyskać informacji o sposobie toouse hello profilera toomeasure wydajności jako usługa działa lokalnie emulatora obliczeń, zobacz [hello testowanie wydajności Azure chmury usługę lokalnie w Witaj Witaj obliczeniowe przy użyciu emulatora programu Visual Studio profilera ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Wybieranie testowania — metoda
### <a name="use-azure-diagnostics-toocollect"></a>Użyj toocollect diagnostyki Azure:
* Statystyka stron sieci web lub usługi, takie jak żądania i połączenia.
* Statystyka role, takie jak częstotliwość roli zostanie ponownie uruchomiony.
* Ogólne informacje na temat użycia pamięci, takich jak hello wartość procentową czasu hello przyjmuje modułu zbierającego elementy bezużyteczne lub hello pamięci zestaw uruchomionej roli.

### <a name="use-hello-visual-studio-profiler-to"></a>Użyj hello profilera Visual Studio do:
* Ustal, które funkcje zająć hello większość czasu.
* Zmierz czas, jaki zajmuje każdej części programu w praktyce znacznym.
* Umożliwiają porównanie wydajności szczegółowe raporty dotyczące dwóch wersji usługi.
* Przeanalizuj więcej szczegółów niż poziom hello alokacji pamięci poszczególnych alokacji pamięci.
* Analizy współbieżności problemów w kodzie wielowątkowych.

Gdy używasz profilera hello może zbierać dane po uruchomieniu usługi w chmurze lokalnie lub na platformie Azure.

### <a name="collect-profiling-data-locally-to"></a>Zbierz dane profilowania lokalnie do:
* Przetestuj wydajność hello części usługi w chmurze, takich jak wykonanie hello określonego procesu roboczego roli, która nie wymaga realistyczne symulowanym obciążeniem.
* Przetestuj wydajność hello usługi w chmurze w izolacji w warunkach kontrolowanych.
* Test wydajności hello usługi w chmurze przed wdrożyć tooAzure.
* Testowanie wydajności hello usługi w chmurze prywatnie, bez zakłóceń hello istniejące wdrożenia.
* Przetestuj wydajność hello hello usługi bez ponoszenia opłat za działające na platformie Azure.

### <a name="collect-profiling-data-in-azure-to"></a>Zbieranie danych profilowania w Azure, aby:
* Przetestuj wydajność hello usługi w chmurze pod obciążeniem symulowane lub rzeczywistej.
* Metoda hello Instrumentacji zbierania danych profilowania, ponieważ w tym temacie opisano później.
* Testowanie wydajności hello usługi hello w hello tym samym środowisku co podczas hello usługa jest uruchamiana w środowisku produkcyjnym.

Zwykle symulować obciążenia tootest usługi w chmurze w normalnych lub podkreślają warunków.

## <a name="profiling-a-cloud-service-in-azure"></a>Profilowanie usługi w chmurze na platformie Azure
Po opublikowaniu usługi w chmurze w programie Visual Studio można profilu usługi hello i określić hello profilowania ustawienia, które pozwalają hello informacji, które mają. Sesja profilowania jest uruchomiony dla każdego wystąpienia roli. Aby uzyskać więcej informacji na temat toopublish usługi z programu Visual Studio, zobacz temat [publikowania tooan usługi w chmurze Azure w programie Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx).

toounderstand więcej informacji na temat profilowanie wydajności w programie Visual Studio, zobacz [tooPerformance przewodnik dla początkujących profilowania](https://msdn.microsoft.com/library/azure/ms182372.aspx) i [analizowanie wydajności aplikacji przy użyciu narzędzi profilowania](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> Można włączyć funkcji IntelliTrace lub profilowania po opublikowaniu usługi w chmurze. Nie można włączyć jednocześnie.
> 
> 

### <a name="profiler-collection-methods"></a>Metoda zbierania danych profilera
Do profilowania, oparte na problemy z wydajnością, można użyć metody innej kolekcji:

* **Próbkowanie Procesora** — ta metoda służy do zbierania statystyk aplikacji, które są przydatne podczas początkowej analizy problemy dotyczące użycia procesora CPU. Próbkowanie Procesora jest hello sugerowane metody większości dochodzenia wydajności. Brak niski wpływ na aplikacji hello są profilowania podczas zbierania danych próbkowania procesora CPU.
* **Instrumentacja** — ta metoda służy do zbierania danych o chronometrażu, który jest przydatne do ukierunkowanej analizy i analizowania problemów z wydajnością wejścia/wyjścia. Każdy wpis, zakończenia i wywołanie funkcji hello funkcji w module metody Instrumentacji Hello rejestruje podczas przebiegu profilowania. Ta metoda jest przydatne do zbierania czasu szczegółowe informacje o sekcji kodu i zrozumienie wpływu hello wejściowymi i wyjściowymi operacje na wydajność aplikacji. Ta metoda jest wyłączona na komputerze 32-bitowym systemie operacyjnym. Ta opcja jest dostępna tylko po uruchomieniu usługi w chmurze hello na platformie Azure, a nie lokalnie w hello emulatora obliczeń.
* **Alokacja pamięci .NET** — ta metoda służy do zbierania danych alokacji pamięci .NET Framework za pomocą metoda profilowania próbkowania hello. Witaj zebranych danych obejmuje hello liczby i rozmiaru przydzielonych obiektów.
* **Współbieżność** — ta metoda służy do zbierania danych kontencji zasobów i procesów i wątków danych wykonawczych, który jest przydatny podczas analizowania aplikacji wielowątkowych i wieloprocesowa. Metoda współbieżności Hello zbiera dane dla każdego zdarzenia, który wykonanie bloki kodu, na przykład jeśli wątek oczekuje na zablokowany dostęp tooan aplikacji zasobów toobe zwolniony. Ta metoda jest przydatna do analizowania aplikacji wielowątkowych.
* Można również włączyć **profilowanie interakcji między warstwami**, zapewniające dodatkowe informacje dotyczące godziny wykonywania hello ADO.NET synchroniczne odwołuje się funkcji aplikacji wielowarstwowych, które komunikują się z co najmniej jednego bazy danych. Z dowolnej z metod profilowania hello można zebrać danych o interakcji między warstwy. Aby uzyskać więcej informacji na temat profilowanie interakcji między warstwami, zobacz [widok interakcji warstwowych](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Konfigurowanie ustawień profilowania
Witaj następującej ilustracji przedstawiono sposób tooconfigure profilowania ustawień w oknie dialogowym hello publikowanie aplikacji platformy Azure.

![Skonfiguruj ustawienia profilowania](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> Witaj tooenable **włączyć profilowanie** pole wyboru, musisz mieć profilera hello zainstalowane na komputerze lokalnym hello, że używasz toopublish usługi w chmurze. Domyślnie profilera hello jest instalowany podczas instalowania programu Visual Studio.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure profilowania, ustawienia
1. W Eksploratorze rozwiązań Otwórz menu skrótów hello Azure projektu, a następnie wybierz **publikowania**. Aby uzyskać szczegółowe instrukcje na temat toopublish usługi w chmurze, zobacz [publikowanie w chmurze przy użyciu usługi hello Azure narzędzia](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. W hello **publikowanie aplikacji platformy Azure** okno dialogowe, wybierz opcję hello **Zaawansowane ustawienia** kartę.
3. tooenable profilowania, wybierz hello **włączyć profilowanie** pole wyboru.
4. tooconfigure ustawienia profilowania wybierz hello **ustawienia** hiperłącza. zostanie wyświetlone okno dialogowe Ustawienia profilowania Hello.
5. Z hello **której metody profilowania ma toouse** przyciski opcji, należy wybrać typ hello profilowania, że należy.
6. interakcja warstwowa hello toocollect profilowania danych, wybierz opcję hello **Włącz profilowanie interakcji między warstwami** pole wyboru.
7. Ustawienia hello toosave, wybierz hello **OK** przycisku.
   
    Podczas publikowania tej aplikacji, te ustawienia są używane toocreate hello sesji dla każdej roli profilowania.

## <a name="viewing-profiling-reports"></a>Wyświetlanie raportów profilowania
Sesja profilowania jest tworzony dla każdego wystąpienia roli w usłudze w chmurze. tooview Twojego profilowania raporty każdej sesji z programu Visual Studio, można wyświetlić hello okno Eksploratora serwera, a następnie wybierz hello rozwiązań usługi obliczenia Azure węzła tooselect wystąpienia roli. Można wyświetlić hello profilowanie raportu, jak pokazano w hello następującej ilustracji.

![Wyświetlanie raportu profilowania z platformy Azure](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>tooview raporty profilowania
1. tooview powitania serwera okno Eksploratora w programie Visual Studio na powitania menu paska wybierz widoku Eksploratora serwera.
2. Wybierz węzeł rozwiązań usługi obliczenia Azure hello, a następnie wybierz węzeł wdrożenia usługi Azure powitania dla usługi w chmurze hello wybrane tooprofile w momencie publikowania w programie Visual Studio.
3. Profilowanie tooview raportów wystąpienia, wybierz rolę hello w usłudze hello hello Otwórz menu skrótów dla określonego wystąpienia, a następnie wybierz pozycję **Wyświetl raport profilowania**.
   
    Raport Hello, plik Vsp, jest teraz pobierane z usługi Azure, a stan hello hello pobierania zostanie wyświetlony w hello dziennika aktywności platformy Azure. Po zakończeniu pobierania hello hello profilowanie raportu pojawi się na karcie w edytorze hello for Visual Studio o nazwie <Role name>  *<Instance Number>*  <identifier>pliku Vsp. Zostanie wyświetlone podsumowanie danych dla raportu hello.
4. toodisplay różne widoki raportu hello hello bieżący widok listy, wybierz typ hello odpowiedni widok. Aby uzyskać więcej informacji, zobacz [widoku raportu narzędzi profilowania](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Następne kroki
[Debugowanie usług w chmurze](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Tooan publikowania usługi w chmurze Azure w programie Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

