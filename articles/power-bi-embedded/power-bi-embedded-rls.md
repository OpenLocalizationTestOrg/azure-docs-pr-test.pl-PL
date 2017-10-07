---
title: zabezpieczenia na poziomie aaaRow z Power BI Embedded
description: "Szczegółowe informacje dotyczące zabezpieczeń na poziomie wiersza z Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Zabezpieczenia na poziomie wierszy w usłudze Power BI Embedded

Zabezpieczeń na poziomie wiersza (kontrola dostępu) może być danych tooparticular dostępu użytkownika toorestrict używanych w obrębie raportu lub zestawu danych, co pozwala na wielu różnych użytkowników toouse hello jednym raporcie podczas oglądanie wszystkie inne dane. Usługa Power BI Embedded obsługuje teraz skonfigurowane odświeżania zestawów danych.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

W kolejności tootake zaletą zabezpieczenia na poziomie wiersza jest ważne, że rozumiesz trzy główne pojęcia; Użytkownicy, role i zasady. Spójrzmy bliższe spojrzenie na każdym:

**Użytkownicy** — te są użytkownicy końcowi rzeczywiste hello wyświetlania raportów. W usłudze Power BI Embedded użytkownicy są identyfikowani na podstawie hello właściwości nazwy użytkownika w tokenie aplikacji.

**Role** — użytkownicy należą tooroles. Rola to kontener dla reguły i może być nazwana "Menedżer sprzedaży" lub "Przedstawiciel". W usłudze Power BI Embedded użytkownicy są identyfikowani przez właściwość role hello w tokenie aplikacji.

**Reguły** — role mają zasady, a zasady te są hello rzeczywiste filtry, które będą stosowane toobe toohello danych. Może to być tak proste, jak "kraju = USA" lub coś bardziej dynamiczne.

### <a name="example"></a>Przykład

Witaj pozostałej części tego artykułu udostępnimy przykładem tworzenia zabezpieczenia na poziomie wiersza i wykorzystywanie który w osadzonych aplikacji. Przedstawiony przykład używa hello [Retail Analysis próbki](http://go.microsoft.com/fwlink/?LinkID=780547) plików PBIX.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

Naszej próbki Retail Analysis przedstawia sprzedaż dla wszystkich magazynów hello w łańcuchu określonego sprzedaży detalicznej. Bez zabezpieczenia na poziomie wiersza niezależnie od tego, które regionalnego Menedżera loguje i widoków hello raport, będzie zobaczy hello tych samych danych. Kierownictwo wykrył, że Menedżer każdy region powinien zobaczyć tylko sprzedaży hello hello magazynów, którymi zarządzają i toodo to, możemy użyć zabezpieczenia na poziomie wiersza.

Kontrola dostępu jest tworzone w programie Power BI Desktop. Po otwarciu hello zestawu danych i raportów, możemy przełącznika toodiagram widoku toosee hello schematu:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

Oto kilka rzeczy toonotice tego schematu:

* Wszystkie miary, takich jak **Total Sales**, są przechowywane w hello **sprzedaży** tabeli faktów.
* Istnieją cztery tabele wymiarów powiązane dodatkowe: **elementu**, **czasu**, **magazynu**, i **regionalnego**.
* strzałki Hello wierszach relacji hello wskazują jaki sposób filtry mogą przepływać z tooanother jedna tabela. Na przykład, jeśli filtr jest umieszczona na **czasu [Date]**, w bieżącym schemacie hello go tylko filtruje wartości w hello **sprzedaży** tabeli. Nie inne tabele może niekorzystnie wpływać filtru wszystkie strzałki hello na powitania relacji wierszy toohello punktu sprzedaży tabeli i nie optymalizacji.
* Witaj **regionalnego** tabela wskazuje będącego dla każdego regionalnego Menedżera hello:
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

Na podstawie tego schematu, jeśli Trwa stosowanie toohello filtru **Menedżera regionalnego** kolumny w hello regionalnego tabeli, a jeśli z filtrem zgodne użytkownika hello wyświetlanie raportu hello, że filtr zostanie również filtrować dół hello **magazynu**i **sprzedaży** tooonly tabel Pokaż dane dla tego konkretnego regionalnego menedżera.

Oto jak:

1. Na karcie modelowania powitania kliknij **Zarządzanie rolami**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Utwórz nową rolę o nazwie **Menedżera**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. W hello **regionalnego** tabeli wprowadź następujące wyrażenie DAX hello: **[regionalnego Manager] = USERNAME()**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. toomake się, że reguły hello pracuje na powitania **modelowania** , kliknij pozycję **widoku w postaci ról**, a następnie wprowadź następujące hello:  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   Witaj raporty będą teraz wyświetlane dane tak, jakby użytkownik był zalogowany jako **Andrew Ma**.

Stosowanie filtru hello, w tym miejscu opisano sposób hello spowoduje odfiltrowanie dół wszystkie rekordy z hello **regionalnego**, **magazynu**, i **sprzedaży** tabel. Jednak ze względu na kierunek filtru hello na powitania relacje między **sprzedaży** i **czasu**, **sprzedaży** i **elementu**i **Elementu** i **czasu** tabele nie będą filtrowane w dół.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Może to być ok tego wymagania, jednak nie chcemy, menedżerów toosee elementy, dla których nie ma żadnej sprzedaży, firma Microsoft może włączyć dwukierunkowego filtrowania krzyżowego hello relacja i przepływu hello filtru zabezpieczeń w obu kierunkach. Można to zrobić, edytując hello relacji między **sprzedaży** i **elementu**, podobnie do następującej:

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

Teraz, filtry również mogą przepływać z hello sprzedaży tabeli toohello **elementu** tabeli:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Jeśli używasz trybu zapytania bezpośredniego dla danych, konieczne będzie tooenable dwukierunkowego między filtrowania zaznaczając te dwie opcje:

1. **Plik** -> **opcji i ustawień** -> **funkcje w wersji zapoznawczej** -> **Włącz filtrowanie krzyżowe w obu kierunkach dla zapytania bezpośredniego**.
2. **Plik** -> **opcji i ustawień** -> **DirectQuery** -> **Zezwalaj na nieograniczoną miar w trybie zapytania bezpośredniego**.

więcej informacji na temat dwukierunkowego filtrowania krzyżowego, pobierania hello toolearn [dwukierunkowego filtrowania krzyżowego w SQL Server Analysis Services 2016 i Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) oficjalny dokument.

To opakowuje pracy hello wszystkich wymagające toobe zrobić w programie Power BI Desktop, ale ma jednego więcej element pracy musi wykonać toobe toomake zasady hello zabezpieczenia na poziomie wiersza zdefiniowanego w usłudze Power BI Embedded pracy. Użytkownicy uwierzytelniania i autoryzacji przez aplikację i tokenów aplikacji są używane toogrant tego użytkownika dostępu tooa określonego Power BI Embedded raportu. Usługa Power BI Embedded nie ma żadnych określone informacje, na który jest użytkownika. Toowork zabezpieczenia na poziomie wiersza wymagany będzie toopass niektórych dodatkowy kontekst jako część token aplikacji:

* **Nazwa użytkownika** (opcjonalnie) — używane zabezpieczenia na poziomie wiersza jest ciągiem, który może służyć toohelp identyfikowania hello użytkownika, stosując zasady zabezpieczenia na poziomie wiersza. Zobacz wiersz zabezpieczeń na poziomie przy użyciu usługi Power BI Embedded
* **role** — ciąg zawierający tooselect ról hello podczas stosowania zasad zabezpieczeń na poziomie wiersza. Jeśli przekazywanie więcej niż jednej roli, powinien zostać przekazany jako tablicy ciągów.

Utwórz hello token przy użyciu hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) metody. Jeśli właściwość username hello jest obecny, należy także podać co najmniej jedną wartość w rolach.

Na przykład można zmienić hello EmbedSample. Wiersz DashboardController 55 może być aktualizowane z

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

na

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

token pełnej aplikacji Hello będzie wyglądać mniej więcej tak:

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

Teraz z wszystkich elementów hello razem, podczas logowania użytkownika do naszej aplikacji tooview tego raportu, aby tylko były stanie toosee hello danych, że mogą one toosee, zgodnie z definicją w naszym zabezpieczeń na poziomie wiersza.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>Zobacz też

[Zabezpieczenia na poziomie wiersza (kontrola dostępu) z zasilania](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Program Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)

