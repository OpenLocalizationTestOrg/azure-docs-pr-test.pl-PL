---
title: "aaaData przypadek użycia fabryki — zalecenia produktu"
description: "Więcej informacji na temat przypadek użycia implementowane przy użyciu fabryki danych Azure wraz z innymi usługami."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>Przypadek użycia — rekomendacje produktów
Fabryka danych Azure to jedna z wielu usług używanych hello tooimplement pakietu Cortana Intelligence Suite akceleratorów rozwiązania.  Zobacz [pakietu Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics) strony w celu uzyskania szczegółów dotyczących tego zestawu. W tym dokumencie opisano typowe przypadek użycia, które Azure użytkownicy mają już rozwiązany i implementowane przy użyciu fabryki danych Azure i innych usług składowych Cortana Intelligence.

## <a name="scenario"></a>Scenariusz
Sklepach internetowych często mają tooentice ich produkty toopurchase klientów z uwzględnieniem ich z produktami, które są najprawdopodobniej toobe planuje się i dlatego najprawdopodobniej toobuy. tooaccomplish, sklepach internetowych należy toocustomize ich użytkownika w trybie online za pomocą produktu spersonalizowane zalecenia dla tego określonego użytkownika. Zalecenia te spersonalizowane to toobe wprowadzone oparte na bieżących i historycznych zakupów zachowania danych, informacje o produkcie, nowo wdrożonych marki i produktu i segmentacji danych klientów.  Ponadto może zapewnić zalecenia produktu użytkownika hello oparte na analizie ogólną zachowanie użycia wszystkim użytkownikom ich łączyć.

Celem tych sprzedawców Hello jest toooptimize dla użytkownika kliknij do sprzedaży konwersji i, tym wyższy przychód ze sprzedaży.  Ta konwersja one osiągnąć dostarcza kontekstowe, na podstawie zachowania produktu zalecenia na podstawie zainteresowań klienta i akcji. Dla tego przypadku użycia używamy sklepach internetowych na przykład firm, które mają toooptimize dla klientów. Jednak te zasady zastosować tooany firma chce tooengage klientom wokół jego towarów i usług i udoskonalenie ich klientom kupowania wraz z zaleceniami spersonalizowane produktu.

## <a name="challenges"></a>Wyzwania
Istnieje wiele wyzwań napotykane przez sprzedawców online podczas próby tooimplement tego typu przypadek użycia. 

Po pierwsze, dane o różnych rozmiarach i kształty musi pozyskanych z wielu źródeł danych, zarówno lokalnie i w chmurze hello. Te dane obejmują dane produktów, dane zachowanie klienta historycznych i dane użytkowników, jak hello użytkownik będzie przeglądać hello online detalicznej lokacji. 

Drugi, spersonalizowane produktu zalecenia należy rozsądnie i dokładnie obliczyć i przewidzieć. Ponadto sklepach internetowych tooproduct marki i zachowanie i przeglądarki danych klienta, również muszą tooinclude opinii klientów na ostatnich toofactor zakupy w ustalaniu hello hello zaleceniach produktu hello użytkownika. 

Trzecie zaleceń hello musi być natychmiast dostarczanego toohello użytkownika tooprovide łatwego przeglądania i zakupu środowisko i zalecenia hello najnowszego i odpowiednie. 

Na koniec sprzedawców muszą toomeasure hello skuteczności ich podejścia śledząc ogólnej sprzedaży w górę i sprzedaży sukcesów sprzedaży kliknij do konwersji, a dostosować zalecenia przyszłych tootheir.

## <a name="solution-overview"></a>Omówienie rozwiązania
Ten przypadek użycia przykład został rozwiązany i zaimplementowana przez użytkowników rzeczywistym Azure przy użyciu fabryki danych Azure i innych usług składowych Cortana Intelligence, łącznie [HDInsight](https://azure.microsoft.com/services/hdinsight/) i [usługi Power BI](https://powerbi.microsoft.com/).

Witaj detalicznej online używa magazynu obiektów Blob platformy Azure, programu SQL server lokalnej bazy danych SQL Azure i składnicy danych relacyjnych jako ich opcji przechowywania danych w całym hello przepływu pracy.  Hello obiektu blob magazynu zawiera informacje o kliencie, dane zachowanie klienta i danych informacji o produkcie. informacje o produkcie Hello się, że dane obejmują informacje o produkcie marki i katalog produktów przechowywane lokalnie w usłudze SQL data warehouse. 

Wszystkie dane hello są połączone i przekazywane do produktu zalecenie systemu toodeliver spersonalizowanych zalecenia na podstawie zainteresowań klienta i akcji, gdy hello użytkownik będzie przeglądać produktów w katalogu hello na powitania witryny sieci Web. klientom Witaj Zobacz też produktów, które są powiązane toohello produktu, które są patrzeć, na podstawie ogólnej wzorców użycia witryny sieci Web, które nie są powiązane tooany jednego użytkownika.

![diagram przypadków użycia](./media/data-factory-product-reco-usecase/diagram-1.png)

Gigabajtów web nieprzetworzone pliki dziennika są generowane z witryny sieci Web hello online detalicznej codziennie jako częściowo ustrukturyzowanych plików. Witaj web nieprzetworzone pliki dziennika i powitania klienta i katalogu informacje o produkcie jest regularnie pozyskanych w magazynie obiektów Blob platformy Azure za pomocą przenoszenia danych globalnie wdrożone fabryki danych jako usługa. nieprzetworzone pliki dziennika Hello dzień hello są dzielone (przez rok i miesiąc) w magazynie obiektów blob do przechowywania długoterminowego.  [Usługa Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) jest pliki dziennika raw hello toopartition używanych w obiekcie blob hello dzienniki hello pozyskanych magazynu i procesu na dużą skalę skryptów zarówno Hive i Pig. Hello dzienniki sieci web podzielonym na partycje, które dane są następnie hello przetworzonych tooextract potrzebne dane wejściowe dla zalecenie systemu toogenerate hello spersonalizowanych produktu zalecenia uczenia maszynowego.

Witaj zalecenie system używany do uczenia maszynowego hello w tym przykładzie jest uczenia platformy zalecenia na podstawie maszynowego typu open source [Apache Mahout](http://mahout.apache.org/).  Wszelkie [usługi Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) lub niestandardowy model może być zastosowane toohello scenariusza.  Hello Mahout model jest używane toopredict hello podobieństwa między elementami na powitania witryny sieci Web, na podstawie wzorców użycia ogólnej i zalecenia hello spersonalizowanych toogenerate oparte na powitania poszczególnych użytkowników.

Ponadto zestaw wyników hello zaleceń spersonalizowane produktu jest składnicy danych relacyjnych tooa przeniesiony do użytku przez hello detalicznej witryny sieci Web.  zestaw wyników Hello również mogą być używane bezpośrednio z magazynu obiektów blob przez inną aplikację lub przenieść tooadditional magazynów i innych przypadków użycia.

## <a name="benefits"></a>Korzyści
Optymalizacja ich strategii zalecenie produktu i dostosowanie jej cele biznesowe, rozwiązanie hello spełnione promocji hello detalicznej online i marketingu cele. Ponadto zostały toooperationalize stanie i zarządzać hello produktu zalecenia w przepływie pracy w sposób wydajny, niezawodny i ekonomiczne. podejście Hello ułatwić ich tooupdate ich modelu i dostosować jego skuteczność na podstawie miar hello sprzedaży sukcesów kliknij do konwersji. Przy użyciu fabryki danych Azure, zostały tooabandon stanie ich zarządzanie zasobami chmury ręczne czasochłonne i kosztowne i zarządzanie zasobami chmury tooon żądanie przeniesienia. W związku z tym zostały stanie toosave czas, pieniądze i ich zmniejszyć toosolution czasu. Widoki elementy powiązane danych i kondycji usługi operational stał się toovisualize łatwe i rozwiązywanie problemów z hello intuicyjne fabryki danych monitorowania i zarządzania dostępne w portalu Azure hello interfejsu użytkownika. Teraz można zaplanowane i zarządzane, tak aby niezawodnie produkowane i dostarczyć toousers Zakończono danych i danych i przetwarzania zależności są automatycznie zarządzane bez udziału człowieka ich rozwiązania.

Zapewniając to spersonalizowane środowisko zakupów, hello online detalicznej utworzone klienta konkurencyjności, atrakcyjne doświadczenia i bardziej sprzedaży i ogólnej zadowoleni, w związku z tym.

