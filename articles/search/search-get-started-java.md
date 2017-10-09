---
title: "aaaGet wprowadzenie do usługi Azure Search w języku Java | Dokumentacja firmy Microsoft"
description: "Jak toobuild chmury hostowanej wyszukiwanie aplikacji na platformie Azure przy użyciu języka Java jako języka programowania."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>Wprowadzenie do usługi Azure Search w języku Java
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Dowiedz się, jak toobuild niestandardowych Java Wyszukaj aplikację, która używa usługi Azure Search jako środowiska wyszukiwania. W tym samouczku używana hello [interfejsu API REST usługi Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello obiekty i operacje używane w tym ćwiczeniu.

toorun tej próbki, musi mieć usługi Azure Search, której możesz zarejestrować się w hello [Azure Portal](https://portal.azure.com). Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) instrukcje krok po kroku.

Możemy użyć następującego oprogramowania toobuild hello i przetestowania przedstawionego przykładu:

* [Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). Należy się wersję EE hello toodownload. Jeden z kroków weryfikacji hello wymaga funkcji, która znajduje się tylko w tej wersji.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>Dane hello — informacje
Ta przykładowa aplikacja korzysta z danych z hello [Stanów Zjednoczonych Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm)zawężonych hello stanu Rhode Island tooreduce hello dataset rozmiaru. Użyjemy tego toobuild danych aplikacji wyszukiwania, która zwraca punkty orientacyjne, takie jak szpitale i szkoły, jak również geologiczne, takie jak strumienie, jeziora i szczyty.

W tej aplikacji hello **SearchServlet.java** budowania i obciążeń hello indeksu przy użyciu [indeksatora](https://msdn.microsoft.com/library/azure/dn798918.aspx) konstrukcja pobierania hello filtrowane danych agencji USGS z publicznej usługi Azure SQL Database. Wstępnie zdefiniowane poświadczenia oraz źródło danych w trybie online toohello informacji połączenia są zawarte w kodzie programu hello. W zakresie dostępu do danych nie jest konieczna dalsza konfiguracja.

> [!NOTE]
> Zastosowaliśmy filtr na toostay tego zestawu danych w obszarze hello 10 000 dokumentów limit hello warstwy cenowej bezpłatna. Jeśli używasz hello warstwy standardowa, ten limit nie ma zastosowania i możesz zmodyfikować ten kod toouse większego zestawu danych. Aby uzyskać szczegółowe informacje o pojemności dla każdej warstwy cenowej, zobacz [Limits and constraints](search-limits-quotas-capacity.md) (Limity i ograniczenia).
> 
> 

## <a name="about-hello-program-files"></a>Informacje o plikach program hello
Witaj Poniższa lista zawiera opis hello plików, które są odpowiednie toothis próbki.

* Search.JSP: Udostępnia interfejs użytkownika hello
* SearchServlet.java: Udostępnia metody (podobnie tooa kontroler na platformie MVC)
* SearchServiceClient.java: obsługuje żądania HTTP
* SearchServiceHelper.java: klasa pomocy, która udostępnia metody statyczne
* Document.Java: Udostępnia model danych hello
* config.Properties: ustawia adres URL usługi wyszukiwania hello i klucza api-key
* Pom.xml: zależność narzędzia Maven

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Znajdź hello nazwę usługi i klucza interfejsu api usługi Azure Search
Wszystkie wywołania interfejsu API REST usługi Azure Search wymagają podania adresu URL usługi hello i klucz interfejsu api. 

1. Zaloguj się toohello [Azure Portal](https://portal.azure.com).
2. Na pasku skok hello, kliknij przycisk **usługi wyszukiwania** toolist wszystkie hello usługi Azure Search aprowizowanych dla subskrypcji.
3. Wybierz usługę hello ma toouse.
4. Na powitania nawigacyjnym usługi zobaczysz Kafelki z istotnymi informacjami, jak również ikonę klucza hello dla uzyskiwania dostępu do kluczy administratora hello.
   
      ![][3]
5. Skopiuj adres URL usługi hello i klucz administratora. Będą Ci potrzebne później, po dodaniu ich toohello **config.properties** pliku.

## <a name="download-hello-sample-files"></a>Pobieranie plików przykładowych hello
1. Przejdź za[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) w witrynie GitHub.
2. Kliknij przycisk **Pobierz ZIP**, Zapisz toodisk pliku zip hello, a następnie Wyodrębnij wszystkie pliki hello zawiera. Rozważ wyodrębnienie hello plików do sieci toomake obszaru roboczego Java łatwiejsze projektu hello toofind później.
3. pliki przykładowe Hello są tylko do odczytu. Kliknij prawym przyciskiem myszy folder właściwości i wyczyść hello atrybut tylko do odczytu.

Wszystkie kolejne modyfikacje plików i instrukcje uruchamiania będą wykonywane względem plików w tym folderze.  

## <a name="import-project"></a>Importowanie projektu
1. W środowisku Eclipse wybierz pozycję **Plik** > **Importuj** > **Ogólne** > **Istniejące projekty do obszaru roboczego**.
   
    ![][4]
2. W **wybierz katalog główny**, Przeglądaj toohello folderu zawierającego pliki przykładowe. Wybierz folder hello, który zawiera hello .project folder. Witaj projektu powinna być widoczna w hello **projekty** listy wybranego elementu.
   
    ![][12]
3. Kliknij przycisk **Zakończ**.
4. Użyj **Eksplorator projektów** tooview i edytuj pliki hello. Jeśli go nie jest jeszcze otwarty, kliknij przycisk **okna** > **Pokaż widok** > **Eksplorator projektów** lub użyj hello skrótów tooopen go.

## <a name="configure-hello-service-url-and-api-key"></a>Skonfiguruj adres URL usługi hello i klucza api-key
1. W **Eksplorator projektów**, kliknij dwukrotnie **config.properties** ustawienia konfiguracji hello tooedit zawierający hello nazwę serwera i klucz api-key.
2. Zobacz kroki toohello wcześniej w tym artykule, w których znaleziono hello adres URL usługi i klucza api-key w hello [Azure Portal](https://portal.azure.com), tooget hello wartości należy wpisać w **config.properties**.
3. W **config.properties**, zastąp "Klucz interfejsu Api" hello interfejsu api-key dla Twojej usługi. Następnie nazwy usługi (hello pierwszy składnik hello http://servicename.search.windows.net adres URL) zastępuje "Nazwa usługi" w hello tego samego pliku.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Konfigurowanie środowisk hello projektu, kompilacji i środowiska wykonawczego
1. W środowisku Eclipse, w obszarze Eksplorator projektów kliknij prawym przyciskiem myszy projekt hello > **właściwości** > **aspekty projektu**.
2. Wybierz pozycje: **Dynamiczny moduł WWW**, **Java** i **JavaScript**.
   
    ![][6]
3. Kliknij przycisk **Zastosuj**.
4. Wybierz pozycję **Okna** > **Preferencje** > **Serwer** > **Środowiska wykonawcze** > **Dodaj...**.
5. Rozwiń pozycję Apache i wybierz wersję hello hello serwer Apache Tomcat, która została wcześniej zainstalowana. W naszym systemie zainstalowano wersję 8.
   
    ![][7]
6. Na następnej stronie powitania określ katalog instalacyjny serwera Tomcat hello. Na komputerze z systemem Windows najprawdopodobniej będzie to katalog C:\Program Files\Apache Software Foundation\Tomcat *wersja*.
7. Kliknij przycisk **Zakończ**.
8. Wybierz pozycję **Okna** > **Preferencje** > **Java** > **Zainstalowane środowiska JRE** > **Dodaj**.
9. W obszarze **Dodawanie środowiska JRE** wybierz opcję **Standardowa maszyna VM**.
10. Kliknij przycisk **Dalej**.
11. W obszarze Katalog główny środowiska JRE sekcji Definicja środowiska JRE kliknij pozycję **Katalog**.
12. Przejdź za**Program Files** > **Java** i wybierz hello JDK została wcześniej zainstalowana. Jest ważne tooselect hello JDK jako hello środowiska JRE.
13. W obszarze zainstalowane środowiska JRE, wybierz hello **JDK**. Twoje ustawienia powinny być podobne toohello następującego zrzutu ekranu.
    
    ![][9]
14. Opcjonalnie wybierz **okna** > **przeglądarki sieci Web** > **programu Internet Explorer** aplikacji hello tooopen w oknie zewnętrznej przeglądarki. Używanie zewnętrznej przeglądarki zapewnia lepsze środowisko aplikacji sieci Web.
    
    ![][8]

Zadania konfiguracji hello zostało zakończone. Następnie możesz części skompilujesz i uruchomisz projekt hello.

## <a name="build-hello-project"></a>Tworzenie projektu hello
1. W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy nazwę projektu hello i wybierz polecenie **Uruchom jako** > **kompilacja Maven...**  tooconfigure hello projektu.
   
    ![][10]
2. W obszarze Edycja konfiguracji, w polu Cele wpisz „czysta instalacja”, a następnie kliknij pozycję **Wykonaj**.

Komunikaty o stanie są okna konsoli toohello danych wyjściowych. BUDOWANIE powiodło wskazujące hello projektu zakończyło się bez błędów powinna zostać wyświetlona.

## <a name="run-hello-app"></a>Uruchamianie aplikacji hello
W tym ostatnim kroku uruchomisz aplikacji hello w środowisko uruchomieniowe serwera lokalnego.

Jeśli nie zostało jeszcze określone środowisko uruchomieniowe serwera w środowisku Eclipse, potrzebujesz toodo ją najpierw.

1. W obszarze Eksplorator projektów rozwiń pozycję **WebContent**.
2. Kliknij prawym przyciskiem myszy pozycję **Search.jsp** >  wybierz polecenie **Wykonaj jako** > **Wykonaj na serwerze**. Wybierz serwer Apache Tomcat hello, a następnie kliknij przycisk **Uruchom**.

> [!TIP]
> Jeśli używasz toostore z systemem innym niż domyślny obszar roboczy projektu, potrzebujesz toomodify **Konfiguracja Uruchom** toopoint toohello projektu lokalizacji tooavoid błędu podczas uruchamiania serwera. W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy pozycję **Search.jsp** >  wybierz polecenie **Wykonaj jako** > **Konfiguracje wykonywania**. Wybierz serwer Apache Tomcat hello. Kliknij pozycję **Argumenty**. Kliknij przycisk **obszaru roboczego** lub **systemu plików** tooset hello folderu zawierającego hello projektu.
> 
> 

Po uruchomieniu aplikacji hello powinna zostać wyświetlona okno przeglądarki zawierające pole wyszukiwania służące do wprowadzania terminów.

Poczekaj około minutę przed kliknięciem przycisku **wyszukiwania** toogive hello usługi Czas toocreate i obciążenia hello indeksu. Jeśli wystąpi błąd 404 protokołu HTTP, wystarczy toowait nieco dłużej przed podjęciem ponownej próby.

## <a name="search-on-usgs-data"></a>Przeszukiwanie danych agencji USGS
zestaw danych agencji USGS Hello zawiera rekordy, które są odpowiednie toohello stanu Rhode Island. Jeśli klikniesz przycisk **wyszukiwania** na pole wyszukiwania puste, zostanie wyświetlony hello 50 pierwszych wpisów, który jest domyślnym hello.

Wprowadzenie terminu zapewni hello wyszukiwarki coś toogo na. Spróbuj wprowadzić nazwę regionalną. "Roger Williams" był pierwszym gubernatorem stanu Rhode Island hello. Liczne parki, budynki i szkoły są nazwane jego imieniem.

![][11]

Możesz też wprowadzić jeden z poniższych terminów:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Następne kroki
To jest pierwszy samouczek usługi Azure Search hello, oparty na języku Java i hello danych agencji USGS. Wraz z upływem czasu będziemy rozszerzać ten samouczek toodemonstrate dodatkowe funkcje wyszukiwania może być toouse w rozwiązaniach niestandardowych.

Jeśli masz już pewną wiedzę w usłudze Azure Search, możesz użyć tego przykładu jako podstawy do dalszych eksperymentów, prawdopodobnie rozbudować hello [stronę wyszukiwania](search-pagination-page-layout.md), lub implementacja [nawigacji aspektowej](search-faceted-navigation.md). Możesz również ulepszyć stronę wyników wyszukiwania hello przez dodanie liczników i łączenie dokumentów w partie, dzięki czemu użytkownicy mogą przeglądania wyników hello.

TooAzure nowego wyszukiwania? Zaleca się podjęcie próby toodevelop innych samouczków zrozumienia można utworzyć. Można znaleźć w naszych [stronę dokumentacji](https://azure.microsoft.com/documentation/services/search/) toofind więcej zasobów. Można również wyświetlić hello łącza w naszym [listy filmów wideo i samouczków](search-video-demo-tutorial-list.md) tooaccess więcej informacji.

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
