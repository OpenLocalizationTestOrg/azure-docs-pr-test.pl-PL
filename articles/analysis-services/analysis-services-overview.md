---
title: "usług Azure Analysis Services jest aaaWhat | Dokumentacja firmy Microsoft"
description: "Pobierz hello szerszej usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>Co to są usługi Azure Analysis Services?
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services zawiera modelowania w chmurze hello danych korporacyjnej. Jest to w pełni zarządzane rozwiązanie „platforma jako usługa” (PaaS), zintegrowane z usługami platformy danych Azure. 

Usługi Analysis Services umożliwiają mieszanie i łączenie danych z wielu źródeł, definiowanie metryk oraz zabezpieczanie danych w jednym zaufanym modelu danych semantycznych. model danych Hello umożliwia łatwiejsze i szybsze dla Twojego toobrowse użytkowników olbrzymich ilości danych z aplikacji klienta, takich jak usługi Power BI, Excel, usługi Reporting Services, aplikacje innych firm i niestandardowych.

![Źródła danych](./media/analysis-services-overview/aas-overview-data-sources.png)

Zapoznaj się z [ten film](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) toolearn sposobu wpasowania Microsoft Azure Analysis Services na ogólne możliwości analizy Biznesowej i jak można korzystać z pobierania modeli danych w chmurze hello.

## <a name="built-on-sql-server-analysis-services"></a>Powstałe na bazie usług SQL Server Analysis Services
Usługi Azure Analysis Services są zgodne z wieloma wspaniałymi funkcjami, które już istnieją w usługach SQL Server Analysis Services Enterprise Edition. Azure Analysis Services obsługuje modeli tabelarycznych przy hello 1200 i 1400 [poziomy zgodności](analysis-services-compat-level.md). Obsługiwane są partycje, zabezpieczenia na poziomie wierszy, relacje dwukierunkowe i przekształcenia. Tryby W pamięci i DirectQuery oznaczają błyskawiczne przetwarzanie zapytań względem ogromnych, złożonych zestawów danych.

Modele tabelaryczne oferują szybkie tworzenie rozwiązań i są wysoce dostosowywalne. Dla deweloperów modeli tabelarycznych obejmują hello tabelaryczny Model obiektów (niestandardowy) toodescribe modelu obiektów. TOMASZ jest widoczna w formacie JSON za pośrednictwem hello [tabelaryczny Model skryptów języka (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) i hello AMO języka definicji danych za pośrednictwem hello [Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) przestrzeni nazw.

## <a name="better-with-azure"></a>Lepiej korzystać z platformy Azure
Azure Analysis Services integruje się z wielu usług Azure, umożliwiając toobuild zaawansowane opcje rozwiązań analitycznych. Integracja z [usługi Azure Active Directory](../active-directory/active-directory-whatis.md) zapewnia bezpieczny dostęp opartej na rolach tooyour najważniejszych danych. Integracja z [fabryki danych Azure](../data-factory/data-factory-introduction.md) potoki, umieszczając w niej działania, który ładuje dane do modelu hello. Istnieje możliwość prostego organizowania modeli za pomocą usług [Azure Automation](../automation/automation-intro.md) i [Azure Functions](../azure-functions/functions-overview.md) oraz niestandardowego kodu.

## <a name="get-up-and-running-quickly"></a>Szybkie rozpoczęcie pracy
W witrynie Azure Portal [serwer można utworzyć](analysis-services-create-server.md) w ciągu kilku minut. [Szablony](../azure-resource-manager/resource-manager-create-first-template.md) usługi Azure Resource Manager i program PowerShell pozwalają natomiast aprowizować serwery za pomocą szablonu deklaratywnego. Pojedynczy szablon pozwala wdrożyć wiele usług wraz z innymi składnikami platformy Azure, takimi jak konta magazynu i usługa Azure Functions. 

Gdy już serwer zostanie utworzony, można utworzyć model tabelaryczny bezpośrednio w witrynie Azure Portal. Z nowego hello (wersja zapoznawcza) [projektanta funkcję Web](analysis-services-create-model-portal.md), można połączyć tooan usługi Azure SQL Database, źródła danych magazynu danych SQL Azure, lub importowanie pliku pbix Power BI Desktop. Relacje między tabelami są tworzone automatycznie, a następnie można utworzyć miary lub edytować plik model.bim hello w formacie json prawo z przeglądarki.

## <a name="scale-tooyour-needs"></a>Skala tooyour potrzeb
Usługi Azure Analysis Services są dostępne w warstwach Deweloper, Podstawowa i Standardowa. W każdej warstwie koszty planu różnią się zgodnie z rozmiar tooprocessing zasilania, QPUs i pamięci. Plan w ramach warstwy wybiera się podczas tworzenia serwera. Plany można zmienić w w dół w ramach hello same warstwy lub uaktualnienia tooa wyższego poziomu, ale nie można obniżyć z wyższego poziomu niższe tooa warstwy.

Serwer można skalować w górę, skalować w dół lub wstrzymywać. Użyj hello portalu Azure lub mają pełną kontrolę na bieżąco za pomocą programu PowerShell. Płaci się wyłącznie za użyte zasoby. toolearn więcej informacji na temat różnych planów hello i warstwy i użyj hello Kalkulator toodetermine hello prawo planu cenowego, zobacz [cennik usługi Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="keep-your-data-close"></a>Przechowywanie danych w zasięgu ręki
Serwery usług Analysis Services Azure mogą być tworzone w następujących hello [regiony platformy Azure](https://azure.microsoft.com/regions/):

| Ameryki | Europa | Azja i Pacyfik |
|----------|--------|--------------|
|  Brazylia Południowa<br> Kanada Środkowa<br> Wschodnie stany USA 2<br> Środkowo-północne stany USA<br> Środkowo-południowe stany USA<br> Środkowo-zachodnie stany USA<br> Zachodnie stany USA | Europa Północna<br> Południowe Zjednoczone Królestwo<br> Europa Zachodnia |   Australia Południowo-Wschodnia<br> Japonia Wschodnia<br> Azja Południowo-Wschodnia<br> Indie Zachodnie  |

Nowe regiony są dodawane cały czas hello, więc tej listy mogą być niekompletne. Lokalizację wybiera się przy tworzeniu serwera za pomocą witryny Azure Portal lub szablonów usługi Azure Resource Manager. Witaj tooget najlepszych wydajności, wybierz lokalizację najbliżej największy bazy użytkowników. Zagwarantuj [wysoką dostępność](analysis-services-bcdr.md), wdrażając swoje modele na serwerach nadmiarowych w wielu regionach.

## <a name="migrate-your-existing-tabular-models"></a>Migrowanie istniejących modeli tabelarycznych
Jeśli masz już istniejącą lokalnymi rozwiązaniami modelu usług SQL Server Analysis Services, należy przeprowadzić migrację usług Analysis Services tooAzure bez znaczących zmian. toomigrate, można użyć narzędzia SSDT toodeploy serwera tooyour modelu. Możesz też w programie SSMS użyć funkcji tworzenia i przywracania kopii zapasowych albo języka TMSL.

Jeśli masz lokalnych źródeł danych, należy tooinstall i skonfigurować [bramy danych lokalnych](analysis-services-gateway.md). Jeśli masz ról i członkowie roli już skonfigurowany migracji ról, ale masz tooreadd członków roli przy użyciu narzędzia SSMS lub programu PowerShell.

## <a name="connect-toopopular-data-sources"></a>Połącz toopopular źródła danych
Azure Analysis Services obsługuje [łączenie źródeł toodata](analysis-services-datasource.md) lokalne w Twojej organizacji i w chmurze hello. Połącz dane z lokalnych źródeł danych i źródeł danych w chmurze, aby uzyskać rozwiązanie hybrydowe. 

Nowe modele tabelaryczne 1400 funkcja hello nowoczesnych Pobierz dane programu SSDT, opierając się na powitania M formuły zapytania. Z Pobierz dane mają więcej transformacji danych i funkcji zestawu połączonych danych i hello możliwości toocreate i edytować własnych zaawansowanych zapytań formuły języka M. Na przykład dzięki modelom tabelarycznym 1400 można tworzyć modele w oparciu o pliki danych w usłudze Azure Blob Storage.

## <a name="use-hello-tools-you-already-know"></a>Narzędzia hello znanych

![Narzędzia programistyczne BI](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>Narzędzia SQL Server Data Tools (SSDT) dla Visual Studio
Tworzenie i wdrażanie modeli z hello wolnego [programu SQL Server Data Tools (SSDT) dla programu Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx). Narzędzia SSDT obejmują szablony projektów usług Analysis Services, które pozwalają szybko rozpocząć pracę. Program SSDT teraz obejmuje hello nowoczesnych pobieranie danych źródła danych zapytań i mashup funkcjonalności dla modeli tabelarycznych 1400. Jeśli znasz pobieranie danych w programie Power BI Desktop i Excel 2016, już wiesz, jak łatwo jest toocreate wysoce dostosowane kwerend źródła danych.

#### <a name="sql-server-management-studio"></a>Sql Server Management Studio
Zarządzaj serwerami i bazami danych modeli przy użyciu [programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Połącz serwery tooyour w chmurze hello. Uruchamianie skryptów TMSL bezpośrednio z okna zapytania XMLA hello i automatyzowania zadań za pomocą skryptów TMSL. Nowe funkcje i możliwości pojawiają się bardzo szybko — program SSMS jest aktualizowany co miesiąc.

#### <a name="powershell"></a>PowerShell
Zadania zarządzania serwerem zasobów takich jak tworzenie serwerów, wstrzymywania lub wznawiania operacji serwera lub zmiana hello poziomu usług (warstwy), użyj polecenia cmdlet usługi Azure Resource Manager (AzureRM). Innych zadań związanych z zarządzaniem baz danych, takich jak dodawanie lub usuwanie członków roli przetwarzania lub uruchamiania skryptów TMSL za pomocą poleceń cmdlet w hello SqlServer module. Zarówno AzureRM i SQLServer moduły są dostępne w hello [galerii programu PowerShell](https://www.powershellgallery.com/).


## <a name="your-data-is-secure"></a>Twoje dane są bezpieczne
![Wizualizacja danych](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>Uwierzytelnianie
Uwierzytelnianie użytkownika dla usług Azure Analysis Services jest obsługiwane przez [usługi Azure Active Directory (AAD)](../active-directory/active-directory-whatis.md). Podczas próby toolog w bazie danych z usług Azure Analysis Services tooan, użyj użytkowników tożsamość konta organizacji z bazy danych programu access toohello próbujesz tooaccess. Te tożsamości użytkowników muszą być elementami członkowskimi domyślne hello Azure Active Directory dla subskrypcji hello, gdzie znajduje się serwer usług Azure Analysis Services hello. toolearn więcej, zobacz [uprawnienia do uwierzytelniania i użytkownik](analysis-services-manage-users.md).

#### <a name="data-security"></a>Bezpieczeństwo danych
Azure Analysis Services używa magazynu toopersist magazynu obiektów Blob platformy Azure i metadanych dla baz danych usług Analysis Services. Pliki danych w ramach obiektu Blob są szyfrowane za pomocą szyfrowania po stronie serwera (SSE) Azure Blob. W trybie zapytania bezpośredniego przechowywane są tylko metadane. rzeczywiste dane Hello jest dostępny ze źródła danych hello podczas przeszukiwania.

#### <a name="on-premises-data-sources"></a>Lokalne źródła danych
Bezpieczny dostęp toodata przechowywanych lokalnie w organizacji jest to osiągane przez zainstalowanie i skonfigurowanie [bramy danych lokalnych](analysis-services-gateway.md). Bram zapewnienia toodata dostępu zapytania bezpośredniego i tryby w pamięci. Zapytanie modelu usług Azure Analysis Services łączy tooan lokalnego źródła danych, zostanie utworzona wraz z hello zaszyfrowane poświadczenia dla źródła danych lokalne powitania. Witaj usługi bramy w chmurze analizuje zapytania hello i wypchnięcia tooan żądania hello Azure Service Bus. Brama lokalna Hello sonduje hello Azure Service Bus dla żądań oczekujących. następnie bramy Hello pobiera hello zapytania, odszyfrowuje hello poświadczeń i łączy toohello źródła danych do wykonania. wyniki Hello są następnie wysyłane z hello źródła danych, Utwórz kopię toohello bramy i następnie w toohello Azure Analysis Services bazy danych.

Azure Analysis Services podlega hello [warunki dotyczące usług Online firmy Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) i hello [Microsoft Online Services Privacy Statement](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).
toolearn więcej informacji na temat zabezpieczeń platformy Azure, zobacz hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/Security/AzureSecurity).

## <a name="supports-hello-latest-client-tools"></a>Obsługuje hello najnowsze narzędzia klienta
![Wizualizacja danych](./media/analysis-services-overview/aas-overview-clients.png)

Nowoczesne narzędzia do eksploracji i wizualizacji danych, takie jak Power BI, Excel czy narzędzia innych firm, udostępniają użytkownikom wysoce interakcyjny i rozbudowany wizualnie wgląd w dane modelu.

Klienci używają MSOLAP, AMO lub ADOMD [bibliotek klienckich](analysis-services-data-providers.md) serwerów usług tooAnalysis tooconnect. Aplikacje klienckie firmy Microsoft, takie jak Power BI Desktop i Excel, instalują wszystkie trzy biblioteki klienta. Ale należy pamiętać, w zależności od wersji hello lub częstotliwość aktualizacji bibliotek klienta nie może być najnowsze wersje hello wymagane przez usług Azure Analysis Services. Witaj dotyczy toocustom aplikacji lub innych interfejsów, takich jak AsCmd, TOMASZ, ADOMD.NET. Te aplikacje zwykle wymagają ręcznej instalacji hello biblioteki jako część pakietu.


## <a name="get-help"></a>Uzyskiwanie pomocy

#### <a name="documentation"></a>Dokumentacja
Azure Analysis Services jest proste tooset się i toomanage. Wszystkie informacje hello należy toocreate i zarządzania usługami serwera w tym miejscu można znaleźć. Podczas tworzenia serwera tooyour toodeploy modelu danych, jej ma znacznie hello sam podobnie jak w przypadku tworzenia modelu danych, wdrażanie tooan na serwerze lokalnym. W witrynie [usług Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services) jest dostępna szeroka gama artykułów dotyczących koncepcji, procedur, szkoleń i samouczków.

#### <a name="videos"></a>Filmy wideo
Zapoznaj się z pomocnymi wideo, odwiedzając dział [usług Azure Analysis Services w witrynie Channel 9](https://channel9.msdn.com/series/Azure-Analysis-Services).

#### <a name="blogs"></a>Blogi
Wszystko zmienia się tak szybko. Możesz zawsze uzyskać najnowsze informacje o hello na powitania [blogu zespołu usług Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/) i [Azure blog](https://azure.microsoft.com/blog/).

#### <a name="community"></a>Społeczność
Społeczność użytkowników usług Analysis Services jest bardzo aktywna. Dołącz do konwersacji hello [forum usług Azure Analysis Services](https://aka.ms/azureanalysisservicesforum).

## <a name="feedback"></a>Opinia
Masz sugestie lub propozycje nowych funkcji? Należy się tooleave komentarze na [Azure Analysis Services opinii](https://aka.ms/azureanalysisservicesfeedback).

Masz sugestie dotyczące dokumentacji hello? Można dodawać komentarze przy użyciu Livefyre u dołu hello każdego artykułu.

## <a name="next-steps"></a>Następne kroki
Teraz, aby dowiedzieć się więcej na temat usług Azure Analysis Services, nadszedł czas tooget uruchomiona. Dowiedz się, jak za[utworzyć serwer](analysis-services-create-server.md) na platformie Azure. Gdy serwer jest gotowy, kroków hello [samouczek Adventure Works](tutorials/aas-adventure-works-tutorial.md) toolearn jak toocreate funkcjonalnej modelu tabelarycznego i wdróż je tooyour serwera.
