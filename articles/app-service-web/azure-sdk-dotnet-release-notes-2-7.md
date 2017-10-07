---
title: Informacje o wersji zestawu SDK for .NET 2.7 i .NET 2.7.1 aaaAzure
description: "Zestaw Azure SDK dla platformy .NET 2.7 i .NET 2.7.1 — informacje o wersji"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>Zestaw Azure SDK dla platformy .NET 2.7 i .NET 2.7.1 — informacje o wersji
## <a name="overview"></a>Omówienie
Ten dokument zawiera informacje o wersji hello hello Azure SDK w wersji .NET 2.7. 

dokument Hello również zawierać informacje o wersji hello hello Azure SDK dla wersji .NET 2.7.1.

2.7 zestawu SDK platformy Azure jest obsługiwana tylko w programie Visual Studio 2015 i Visual Studio 2013. [2.6 zestawu SDK platformy Azure](https://azure.microsoft.com/downloads/) hello ostatnio obsługiwane zestawu SDK dla programu Visual Studio 2012.

Aby uzyskać szczegółowe informacje na temat tej wersji, zobacz [post anonsu Azure SDK 2.7](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) i [zestawu Azure SDK 2.7.1 anonsu post](http://go.microsoft.com/fwlink/?LinkId=623850).

## <a name="azure-sdk-for-net-27"></a>Azure SDK for .NET 2.7
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Zaloguj się ulepszenia dla programu Visual Studio 2015
Azure 2.7 zestawu SDK dla programu Visual Studio 2015 obsługuje nowe funkcje zarządzania tożsamościami hello w programie Visual Studio 2015.  Dotyczy to również obsługi kont dostępu do platformy Azure za pomocą kontroli dostępu opartej na rolach, dostawców rozwiązań w chmurze, DreamSpark i innych typów konto i subskrypcję.

Hello logowania ulepszenia dołączonego 2.7 zestawu SDK platformy Azure są dostępne tylko w programie Visual Studio 2015. Dla programu Visual Studio 2013 są obsługiwane w zestawie Azure SDK 2.7.1.

### <a name="mobile-sdk"></a>Przenośne zestawu SDK
Zaktualizowano **Mobile Apps** tooreflect szablony najnowszych [pakietu NuGet](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) i konfiguracji.

### <a name="service-bus"></a>Service Bus
Ogólne poprawki i ulepszenia. Szczegółowe informacje na temat aktualizacji i funkcji, można znaleźć toohello informacje o wersji programu hello najnowszych [NuGet usługi Service Bus](http://www.nuget.org/packages/WindowsAzure.ServiceBus/).

### <a name="hdinsight-tools"></a>Narzędzia HDInsight Tools
W tym hello wersji wprowadzono następujące aktualizacje. Te aktualizacje są w wersji zapoznawczej. Aby uzyskać więcej informacji, zobacz [ten blog](http://go.microsoft.com/fwlink/?LinkId=619108).

* Wykresy gałęzi do gałęzi w aplikacji Tez zadania
* Pełna obsługa Hive DML IntelliSense
* Obsługa szablonów pig
* Szablony STORM do usług platformy Azure

#### <a name="breaking-changes"></a>Fundamentalne zmiany
* Stary **Storm** projekt musi zostać uaktualniony, korzystając z tej wersji narzędzi hello. Aby uzyskać więcej informacji, zobacz [ten blog](http://go.microsoft.com/fwlink/?LinkId=619108).
* Visual Studio Web Express nie jest już obsługiwana. Aby uzyskać więcej informacji, zobacz [ten blog](http://go.microsoft.com/fwlink/?LinkId=619108).

### <a name="azure-app-service-tools"></a>Narzędzia usługi aplikacji Azure
W tej wersji hello następujące aktualizacje wprowadzono tooWeb rozszerzeń narzędzi. Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) blogu. 

* Obsługa kont DreamSpark dodane
* Zmień pełną tooAzure narzędzia wprowadzone toosupport hello nowych interfejsów API Menedżera zasobów Azure
* Obsługa usługi Azure App Service dodane za[Eksplorator chmury](#cloud_explorer)

#### <a name="known-issues"></a>Znane problemy
Węzły miejsca wdrożenia aplikacji sieci Web nie są wyświetlane w węźle miejsc hello w Eksploratorze serwera i węzłów podrzędnych miejsca wdrożenia aplikacji sieci Web nie są ładowane w obszarze Eksplorator chmury. Ten problem zostało rozwiązane i przygotowane do następnej wersji zestawu SDK hello. 

### <a name="cloud_explorer"></a>Cloud Explorer for Visual Studio 2015
2.7 zestawu SDK platformy Azure obejmuje Eksplorator chmury dla programu Visual Studio 2015, co pozwala tooview zasobów platformy Azure, sprawdzić ich właściwości i akcje developer klucza z poziomu programu Visual Studio. 

Eksplorator chmury obsługuje następujące hello:

* Typ zasobu i grupy zasobów widoków zasobów platformy Azure 
* Wyszukiwanie zasobów według nazwy (dostępne w widoku typu zasobu)
* Obsługa subskrypcji i zasoby, które mają roli na podstawie kontroli dostępu (RBAC) stosowane 
* Zintegrowane panelu akcji, które zawiera akcje fokus developer tooselected określonych zasobów. Na przykład: Dołącz debugera zdalnego dla maszyn wirtualnych utworzonych przy użyciu hello stosu usługi Resource Manager, widok danych diagnostycznych dla maszyn wirtualnych itd.
* Zintegrowane panelu Właściwości, które są wyświetlane właściwości fokus developer zazwyczaj potrzebne podczas tworzenia/testowania 
* Szybkie przełączanie hello konta toouse podczas wyliczania zasobów (Użyj ustawień polecenia na pasku narzędzi) 
* Filtrowanie subskrypcji toouse podczas wyliczania zasobów (Użyj ustawień polecenia na pasku narzędzi) 
* Toohello linków bezpośrednich portalu Azure do zarządzania zasobami i grupy zasobów 

### <a name="azure-resource-manager-tools"></a>Narzędzia Menedżera zasobów Azure
Narzędzia Menedżera zasobów Azure Hello zostały zaktualizowane toowork z kontroli dostępu na podstawie ról (RBAC) i nowe typy subskrypcji.  Dołączone do tych zmian jest hello możliwości toouse nowego konta magazynu, oprócz magazynu tooclassic artefakty toostore podczas wdrażania.  

Jeśli projekt grupy zasobów platformy Azure z poprzedniej wersji zestawu SDK hello jest używany z hello 2.7 zestawu SDK, nowy skrypt wdrożenia jest wymagane toodeploy zamiast klasycznego magazynu przy użyciu nowego konta magazynu.  Zostanie wyświetlony monit przed wprowadzeniem zmian tooyour projektu tooadd hello nowy skrypt.  Witaj starego skryptu zostanie zmieniona i konieczne będzie toomanually wprowadź wszelkie zmiany toohello nowy skrypt.

### <a name="storage-explorer-tools"></a>Narzędzia Eksploratora magazynu
* Obsługa wyświetlania Dołącz obiektów blob. Aby dowiedzieć się więcej w [ten wpis w blogu](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx). 
* Obsługa wyświetlania kont Premium magazynu za pomocą Eksploratora serwera. Eksploratora serwera będą wyświetlane tylko stronicowych obiektów blob dla kont premium magazynu, ponieważ są one typu hello obsługiwane tylko dla kont premium magazynu.

### <a name="azure-data-factory-tools-for-visual-studio"></a>Narzędzia fabryki danych Azure dla programu Visual Studio
Wprowadzenie do **narzędzia fabryki danych Azure** dla programu Visual Studio. Poniżej przedstawiono funkcje hello włączone. Zobacz [ten blog](http://go.microsoft.com/fwlink/?LinkId=617530) Aby uzyskać więcej informacji.

* **Szablon na podstawie tworzenia**: wybierz Użyj — z uwzględnieniem wielkości liter na podstawie szablonów, szablony przepływu danych lub przetwarzania danych szablonów toodeploy rozwiązania integracji danych na całej trasie, a następnie rozpocznij praktyczne szybko z fabryką danych. 
* **Integracja z Eksploratora rozwiązań do tworzenia i wdrażania jednostek fabryki danych**: tworzenie i wdrażanie potoki i powiązanych jednostek jako projektów programu Visual Studio. 
* **Integracja z widoku diagramu do visual interakcji, podczas tworzenia**: wizualnie tworzyć potoki i zestawów danych o pomoc z hello widoku diagramu. 
* **Integracja z Eksploratora serwera do przeglądania i interakcji z obiektami już wdrożonych**: toobrowse Eksploratora serwera na powitania korzystają już wdrożony fabryki danych i odpowiednich jednostek. Zaimportuj fabryki danych wdrożonych lub dowolnej jednostki (potoku, połączonej usługi, zbiory danych) do projektu. 
* **Edytowanie JSON za pomocą intellisense schemat sprawdzania poprawności i rozbudowane**: efektywnego konfigurowania i edycji dokumentów JSON jednostek fabryki danych z zaawansowanych funkcji intellisense i schemat sprawdzania poprawności 
* **Publikowanie środowisko**: publikowanie toodev utworzone potoki, testów lub produkcyjną środowiska przez utworzenie oddzielnych config plików dla każdego środowiska.
* **Obsługa przetwarzania danych na podstawie pig, Hive i .net**: Obsługa Pig i Hive skryptów w projekcie fabryki danych. Obsługa odwołujące się do projektu C# .net zarządzania działania.

## <a name="azure-sdk-for-net-271"></a>Zestaw Azure SDK dla programu .NET 2.7.1
Po sekcji Hello zawiera aktualizacje, które zostały wprowadzone z hello Azure SDK dla wersji .NET 2.7.1.

### <a name="hdinsight-tools"></a>Narzędzia HDInsight Tools
Aby uzyskać szczegółowe informacje na temat aktualizacji narzędzi HDInsight, zobacz [ten blog](http://go.microsoft.com/fwlink/?LinkId=623831).

* Widok operatorów hive zadania (Nowa funkcja)
  
    należy zapoznać się z zapytań Hive lepsze, funkcja Widok operatorów Hive hello toohelp został dodany. toosee wszystkie hello operatory wewnątrz wierzchołka, kliknij dwukrotnie hello wierzchołki wykresu zadania hello. tooview szczegółowe informacje o konkretnym operatorze, umieść kursor nad tego operatora.
* Znacznik błąd gałąź (Nowa funkcja)
  
    tooenable tooview hello błędy gramatyczne natychmiast, hello Hive znacznika błędu funkcji zostało dodane. Ponadto zostały rozszerzone komunikaty o błędach i będą teraz widoczne błędy gramatyczne szczegółowe natychmiast (do tej wersji, trzeba było toosubmit klastra toohello skryptu Hive i zaczekaj chwilę przed pobraniem szczegółowe informacje o Twojej komunikat o błędzie).  
* Wykres topologii STORM (Nowa funkcja)
  
    Wizualizacja jest bardzo ważne, gdy chcesz toosee, jeśli ta topologia działa zgodnie z oczekiwaniami. W tej wersji dodano wizualizacji wykresu Storm. Można zwizualizować hello metryki istotne dla topologii (na przykład kolor oznacza pogody niektórych Bolt "zajęty" lub nie). Możesz również dwukrotnie kliknąć tooview Bolt/Spout hello więcej szczegółów.
* Obsługa klastrów usługi HDInsight, które zostały utworzone w portalu Azure (poprawkę) hello
  
    Można teraz używać programu Visual Studio tooview i przesłać zadania tooall Twojego HDInsight clusters niezależnie od tego, gdzie zostały utworzone hello klastra.
* Więcej obsługę funkcji IntelliSense & metadanych Hive ładowania szybciej (poprawa)
  
    Firma Microsoft ulepszyła hello IntelliSense, dodając więcej wskazówek przyjazny dla użytkownika. Na przykład alias tabeli można teraz również sugerowane w IntelliSense, łatwiej można napisać zapytanie. Ponadto firma Microsoft ulepszyła metadanych Hive hello ładowania, dlatego właśnie potrwa kilka sekund toolist hello baz danych, tabel i kolumn Twoje potrzeby magazynu metadanych Hive.

Aby uzyskać szczegółowe informacje na temat aktualizacji narzędzi HDInsight, zobacz [ten blog](http://go.microsoft.com/fwlink/?LinkId=623831).

### <a name="improvements-in-visual-studio-2013"></a>Ulepszenia w programie Visual Studio 2013
* Zestaw Azure SDK 2.7.1 umożliwia tooaccess programu Visual Studio 2013 konta platformy Azure i subskrypcji za pomocą kontroli dostępu opartej na rolach, dostawców rozwiązań w chmurze i Dreamspark.
* Przy użyciu zestawu Azure SDK 2.7.1 nowe okno narzędzi Eksplorator chmury hello jest obecnie również dostępna w programie Visual Studio 2013.

### <a name="known-issues"></a>Znane problemy
Instalowanie hello Azure SDK w wersji 2.6 lub 2.7.1 dla programu Visual Studio Community 2013 na nie - angielskiej wersji językowej systemu operacyjnego zostanie wyświetlone ostrzeżenie o hello angielski i innej niż angielska zasobów programu Visual Studio może nie pasować do siebie. To ostrzeżenie może zostać bezpiecznie odwołany. Go tylko wówczas, gdy maszyna hello nie zawierał wcześniejszego zainstalowania programu Visual Studio Community 2013 i hello zestawu SDK jest instalowany na nie - angielskiej wersji językowej systemu operacyjnego. Ostrzeżenie Hello jest wyświetlany po pakiet językowy hello stosuje hello RTM zasobów tooVisual Studio, ale przed zastosowaniem aktualizacji 4. Odrzucanie ostrzeżenie hello umożliwi hello language pack toocontinue i pełną wersję hello aktualizacji 4 stosowania pakietu językowego hello zawartości.

LightSwitch — projekty nie są compatibile w tej wersji. Ten problem zostanie rozwiązany z hello SDK następnej wersji.

## <a name="also-see"></a>Zobacz też
[Zestaw Azure SDK 2.7.1 post anonsu](http://go.microsoft.com/fwlink/?LinkId=623850)

[Azure post anonsu 2.7 zestawu SDK](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[Obsługa i wycofania informacje dotyczące hello zestaw Azure SDK for .NET i interfejsów API](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

