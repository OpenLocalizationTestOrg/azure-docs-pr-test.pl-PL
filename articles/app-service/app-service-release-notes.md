---
title: Informacje o wersji zestawu SDK dla platformy .NET 2.5.1 aaaAzure
description: Informacje o wersji zestawu Azure SDK dla platformy .NET 2.5.1
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>Informacje o wersji zestawu Azure SDK dla platformy .NET 2.5.1
Ten dokument zawiera informacje o wersji hello hello Azure SDK dla wersji .NET 2.5.1. 

## <a name="azure-sdk-for-net-251-release-notes"></a>Informacje o wersji zestawu Azure SDK dla platformy .NET 2.5.1
Witaj poniżej przedstawiono nowe funkcje i aktualizacje w hello Azure SDK dla platformy .NET 2.5.1.

* Nowe features\scenarios powiązane zbyt**rozszerzeń narzędzi sieci Web**. 
  
  * Witryn sieci Web Azure została zmieniona tooAzure usługi aplikacji. Aby uzyskać więcej informacji, zobacz [istniejących usług Azure i usłudze Azure App Service](../app-service-web/app-service-changes-existing-services.md).
  * Dodano obsługę aplikacje interfejsu API (wersja zapoznawcza) Azure, dzięki czemu klienci mogą publikowanie projektów programu ASP.NET, jak aplikacje interfejsu API, a następnie użyj hello Dodaj > gestu klienta aplikacji interfejsu API platformy Azure w C# projekty toogenerate kodu na podstawie struktury hello hello wdrożonych aplikacji interfejsu API. 
  * Zamiast węzła usługi aplikacji Azure hello, zawierającą Obsługa zasobów na podstawie grupy grupowanie Azure API Apps, Mobile Apps i aplikacje sieci Web została zastąpiona Hello węzła witryn sieci Web w Eksploratorze serwera.
  * Pomoc techniczna platformy Azure Mobile Apps (wersja zapoznawcza) został dodany, aby klienci mogą tworzyć nowe projekty Mobile Apps, Dodaj kontrolery Mobile Apps, publikowanie projektów hello i zdalne debugowanie aplikacji.
  * Dodaj > gestu klienta aplikacji interfejsu API Azure obsługuje teraz lokalne pliki JSON programu Swagger, więc deweloperzy interfejsu API sieci Web można używać NuGets innych firm, takich jak Swashbuckle toogenerate Swagger lub tworzyć go ręcznie. W ten sposób klient deweloperzy mogą używać tooconsume funkcji generowania kodu hello dowolnego punktu końcowego struktury Swagger w projektów C#. 
  * Aplikacja sieci Web i aplikacji interfejsu API publikowania okien dialogowych zostały rozszerzone toosupport hello Azure Portal pojęcia grupowanie zasobów i wyboru/tworzenia grup zasobów platformy Azure i plany usługi App Service są reprezentowane w hello nowej aplikacji sieci Web i aplikacji interfejsu API inicjowania obsługi administracyjnej okna dialogowego. 
  * Węzły w Eksploratorze serwera aplikacji interfejsu API platformy Azure zapewniają toohello łącza, które aplikacje interfejsu API głębokie łącze w hello portalu Azure, a także inne funkcje, takie jak dzienników przesyłania strumieniowego i debugowanie zdalne.
    
    Znane problemy i bieżących ograniczeń w .NET SDK usługi Azure 2.5.1 [to](app-service-release-notes.md#known_issues_2_5_1) poniższej sekcji.
* Nowe features\scenarios powiązane zbyt**narzędzi HDInsight Tools** w programie Visual Studio są włączone w tej wersji. 
  
  * Lokalna Weryfikacja skryptów hive. Kliknij przycisk skrypt weryfikacji hello hello narzędzi toosee, jeśli występują błędy skryptu. 
  * Ulepszone debugowanie zadań Hive. Można teraz debugowania zadań Hive, uzyskując dostęp do dzienników Yarn w programie Visual Studio. Jeśli aplikacja ma problemy z wydajnością, analizowania dzienników YARN będzie dostarczające przydatnych informacji...
  * (W publicznej wersji zapoznawczej) IntelliSense i autouzupełniania — słowo kluczowe obsługę Hive. toohelp Tworzenie gałęzi skryptów, narzędzi HDInsight Tools for Visual Studio dodane autouzupełniania — słowo kluczowe i obsługę funkcji IntelliSense dla gałęzi.
  * Obsługa platformy STORM. Można teraz używać narzędzi HDInsight Tools dla Visual Studio toodevelop Storm topologies/elementach Spout/elementów Bolt w języku C#. Następnie można przesłać hello opracowany klaster Storm tooa topologii i wyświetlić stan spout/bolt/topologii hello. Można użyć dzienniki systemu i klienta dzienniki tootroubleshoot Twojego Storm topologies/elementów Bolt/elementach Spout. Umożliwia także istniejące zasoby JAVA w Storm w usłudze HDInsight.
    
    Aby uzyskać więcej informacji, zobacz [rozpocząć korzystanie z narzędzi Hadoop w HDInsight dla programu Visual Studio](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a id="known_issues_2_5_1"></a>Zestaw Azure SDK dla platformy .NET 2.5.1 znane problemy i ograniczenia
* Aplikacje interfejsu API platformy Azure jest widoczny jako cel wdrożenia dla aplikacji mobilnych. Aplikacje sieci Web powinna być hello tylko miejsce docelowe Mobile Apps do późniejszych wersji. 
* Inicjowanie obsługi aplikacji interfejsu API platformy Azure może spowodować Powodzenie, ale okresowo niepowodzenie tooupdate hello postęp w oknie działanie usługi Azure App Service hello. Obejście jest stan toocheck hello API Azure nowych aplikacji w hello portalu Azure. 
* Plik > Nowy Projekt > Aplikacja interfejsu API > środowisko F5 powoduje błąd HTTP, ponieważ nie istnieje żadne default/index.html. Obejście jest toomanually przeglądania toohello/api/wartości adresu URL. 
* Sporadycznie ikony Eksploratora serwera są wyświetlane spłaszczony. Ponowne uruchomienie programu VS rozwiązuje ten problem. 
* Jeśli w aplikacji sieci Web lub aplikacji interfejsu API inicjowania obsługi administracyjnej (np. Przekroczono limit przydziału błędy lub zduplikowaną nazwę bramy aplikacji interfejsu API Azure), jest zgłaszany wyjątek, błędy hello Pokaż nieprzetworzone tekst JSON. 
* Problemy sporadyczne tworzenia projektu, gdy zaznaczone jest pole w czasie tworzenia projektu usługi Application Insights.
* Czasami hello wygenerowany kod klienta aplikacji interfejsu API Azure brakuje przestrzeni nazw, muszą one mieć toobe ręcznie włączone (lub automatycznie importowane przy użyciu programu Visual Studio wskaźników) dla toocompile kodu. 
* Projekty aplikacji mobilnej powinien być tooweb opublikowanej aplikacji, ale należy wybrać utworzony jako aplikacja mobilna, w portalu Azure hello, ponieważ projekt aplikacji mobilnej wymaga bazy danych lokacji. 
* Witaj strony początkowej dla aplikacji mobilnych używa hello termin "usługi mobilnej" zamiast "aplikacje mobilne" 
* Tworzenie projektu aplikacji mobilnej może trwać tooa toocreate minuty. 
* W aplikacji interfejsu API inicjowania obsługi administracyjnej (w niektórych przypadkach) wystąpił błąd wróci od hello Azure API odbicia czy hello uprawnienia nie można poprawnie, ustawić podczas hello aplikacji interfejsu API został prawidłowo zainicjowany i jest gotowy do użycia. Można ręcznie ustawić uprawnień przy użyciu hello portalu Azure.
* Usługa Application Insights nie jest obsługiwana na szablony aplikacji interfejsu API i aplikacji mobilnej.
* Projekty aplikacji interfejsu API nie można używać w połączeniu z projektami usługi w chmurze.
* Szablony projektu aplikacji interfejsu API są dostępne tylko w języku C#.
* Użycie aplikacji interfejsu API za pomocą menu kontekstowe "Dodawanie Azure klienta interfejsu API aplikacji" hello jest obsługiwana tylko w języku C#.

