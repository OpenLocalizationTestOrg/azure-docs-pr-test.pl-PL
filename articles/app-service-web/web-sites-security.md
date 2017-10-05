---
title: "Zabezpieczanie aplikacji w usłudze Azure App Service"
description: "Dowiedz się, jak zabezpieczyć aplikacji sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: b70d74441f3d6d9793ae516b3f04e36e786a9a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Zabezpieczanie aplikacji w usłudze Azure App Service
Ten artykuł ułatwia rozpoczęcie pracy dotyczące zabezpieczania aplikację sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service. 

Zabezpieczenia w usłudze Azure App Service ma dwa poziomy: 

* **Zabezpieczenia infrastruktury i platformy** -zaufania Azure do usługi, należy uruchomić faktycznie rzeczy bezpiecznie w chmurze.
* **Zabezpieczenia aplikacji** -trzeba bezpiecznie projektować samej aplikacji. W tym sposób integracji z usługą Azure Active Directory, jak zarządzać certyfikatami i jak należy upewnić się, że możesz bezpiecznie porozmawiać do różnych usług. 

#### <a name="infrastructure-and-platform-security"></a>Zabezpieczenia infrastruktury i platform
Ponieważ usługa aplikacji przechowuje maszynach wirtualnych platformy Azure, magazynu, połączeń sieciowych, platformy sieci web, zarządzania i funkcje integracji i wiele innych jest aktywnie zabezpieczone i wzmocnione zabezpieczenia i przechodzi przez intensywnie zgodności oraz sprawdza w sposób ciągły, aby upewnić się, które:

* Usługi aplikacji — aplikacje odizolowanych z obu Internetu i z innych klientów zasobów platformy Azure.
* Komunikacja klucze tajne (np. parametry połączenia) między aplikację usługi aplikacji i innych zasobów platformy Azure (np. Baza danych SQL) w grupie zasobów w obrębie platformy Azure i nie krzyżowe żadnych granic sieci. Hasła są zawsze szyfrowane.
* Cała komunikacja między aplikacji usługi aplikacji i zasobów zewnętrznych, takich jak zarządzanie w programie PowerShell, interfejsu wiersza polecenia Azure SDK, interfejsów API REST i połączeń hybrydowych było możliwe, były prawidłowo zaszyfrowane.
* 24-godzinnym threat management chroni zasoby usługi aplikacji przed złośliwym oprogramowaniem, distributed denial of service (DDoS), man-in--middle (MITM) i innymi zagrożeniami. 

Aby uzyskać więcej informacji na zabezpieczenia infrastruktury i platformy na platformie Azure, zobacz [Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Zabezpieczenia aplikacji
Gdy platforma Azure jest odpowiedzialny za bezpieczeństwo infrastruktury i platformy, która aplikacja działa na, jest obowiązek secure samej aplikacji. Innymi słowy musisz tworzenie, wdrażanie i zarządzanie kodem aplikacji i zawartości w bezpieczny sposób. W przeciwnym razie z kodu aplikacji lub zawartość nadal można narażony na zagrożenia takich jak:

* Iniekcja kodu SQL
* Przejęcie kontroli sesji
* Wykonywanie skryptów lokacji między
* MITM na poziomie aplikacji
* DDoS na poziomie aplikacji

Pełne omówienie zagadnienia dotyczące zabezpieczeń dla aplikacji sieci web, wykracza poza zakres tego dokumentu. Jako punkt początkowy, aby uzyskać dalsze wskazówki dotyczące zabezpieczania aplikacji, zobacz [Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP)](https://www.owasp.org/index.php/Main_Page), w szczególności [10 pierwszych projektu.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), który wyświetla listę bieżącej pierwszych 10 krytyczne sieci Web aplikacji luk w zabezpieczeniach, zgodnie z ustaleniami OWASP członków.

## <a name="perform-penetration-testing-on-your-app"></a>Wykonaj penetracji testowania w aplikacji
Jedną z najprostszych sposobów wprowadzenie testowanie pod kątem luk w zabezpieczeniach w aplikacji usługi aplikacji jest użycie [integrację z usługa Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) przeprowadzić jednym kliknięciem usterki skanowanie w aplikacji. Możesz wyświetlić wyniki testów w raporcie o łatwe do zrozumienia i Dowiedz się, jak rozwiązać każdy luki w zabezpieczeniach instrukcje krok po kroku.

Jeśli chcesz przeprowadzić własne testy penetracji lub chcesz użyć innego dostawcę lub skanera pakietu, należy wykonać [Azure penetracji testowanie procesu zatwierdzania](https://security-forms.azure.com/penetration-testing/terms) i uzyskiwanie pobieraniu do wykonywania testów żądaną penetracji.

## <a name="https"></a>Zabezpieczenia komunikacji z klientami
Jeśli używasz  **\*. azurewebsites.net** nazwy domeny utworzonej dla aplikację usługi aplikacji można natychmiast jest używany protokół HTTPS, certyfikat SSL jest podane dla wszystkich  **\*. azurewebsites.net** nazw domen. Jeśli Twoja witryna wymaga [niestandardowej nazwy domeny](app-service-web-tutorial-custom-domain.md), możesz przekazać certyfikat SSL do [włączyć protokół HTTPS](app-service-web-tutorial-custom-ssl.md) dla domeny niestandardowej.

Włączanie [HTTPS](https://en.wikipedia.org/wiki/HTTPS) może pomóc atakom MITM na komunikację między aplikacji i jej użytkowników.

## <a name="secure-data-tier"></a>Zabezpieczenia warstwy danych
Usługi aplikacji wysokiej integruje się z bazą danych SQL, tak, aby wszystkie parametry połączenia są szyfrowane po szachownicy i odszyfrowane tylko na maszynie Wirtualnej, która aplikacja jest uruchamiana na *i* tylko po uruchomieniu aplikacji. Ponadto bazy danych SQL Azure zawiera wiele funkcji zabezpieczeń, aby zabezpieczyć dane aplikacji przed zagrożeniami przez, w tym [szyfrowania na rest](https://msdn.microsoft.com/library/dn948096.aspx), [zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt163865.aspx), [ Maskowanie danych dynamicznych](../sql-database/sql-database-dynamic-data-masking-get-started.md), i [wykrywanie zagrożeń](../sql-database/sql-database-threat-detection.md). Jeśli masz dane poufne lub wymagania dotyczące zgodności, zobacz [Zabezpieczanie bazy danych SQL](../sql-database/sql-database-security-overview.md) Aby uzyskać więcej informacji na temat sposobu zabezpieczenia danych.

Jeśli używasz dostawcy bazy danych z innych firm, takich jak ClearDB, należy skonsultować się z dokumentacją dostawcy bezpośrednio na najlepszych rozwiązaniach dotyczących zabezpieczeń.  

## <a name="develop"></a>Bezpieczne opracowywania i wdrażania
### <a name="publishing-profiles-and-publish-settings"></a>Publikowanie profile i ustawienia publikowania
Podczas tworzenia aplikacji, wykonywanie zadań zarządzania, lub automatyzacji zadań za pomocą narzędzi takich jak **programu Visual Studio**, **Web Matrix**, **programu Azure PowerShell** lub  **Interfejs wiersza polecenia platformy Azure (Azure CLI)**, możesz użyć dowolnej *ustawień publikowania* pliku lub *profilu publikowania*. Oba typy plików uwierzytelnienia Cię przy użyciu platformy Azure i powinien być zabezpieczony, aby uniemożliwić nieautoryzowany dostęp.

* A **ustawień publikowania** plik zawiera
  
  * Identyfikator subskrypcji platformy Azure
  * Certyfikat zarządzania, który umożliwia wykonywanie zadań zarządzania dla subskrypcji *bez konieczności podaj nazwę użytkownika lub hasło*.
* A **profilu publikowania** plik zawiera
  
  * Informacje dotyczące publikowania aplikacji

Jeśli narzędzie używa pliku ustawień publikowania lub pliku profilu publikowania, zaimportuj plik zawierający ustawienia publikowania lub profilu do narzędzia, a następnie **usunąć** pliku. Jeśli muszą zachować plik, można udostępniać innym użytkownikom pracy w projekcie, na przykład, zapisz go w bezpiecznym miejscu, takich jak *zaszyfrowanych* katalogu z ograniczonymi uprawnieniami.

Ponadto należy upewnij się, że importowany poświadczenia są zabezpieczone. Na przykład **programu Azure PowerShell** i **interfejsu wiersza polecenia platformy Azure (Azure CLI)** sklepów zaimportowanych informacji w sieci **katalogu macierzystego** ( *~*  w systemach Linux lub OS X i */users/nazwa_użytkownika* w systemach Windows.) Dla dodatkowego bezpieczeństwa możesz **szyfrowania** tych lokalizacji za pomocą szyfrowania narzędzi dostępnych w systemie operacyjnym.

### <a name="configuration-settings-and-connection-strings"></a>Ustawienia konfiguracji i parametry połączenia
Jest typowym rozwiązaniem do przechowywania parametrów połączenia, poświadczenia uwierzytelniania i innych poufnych informacji w plikach konfiguracji. Niestety te pliki mogą być widoczne w witrynie sieci Web lub wyewidencjonowany do publicznego repozytorium, udostępnianie tych informacji. Proste wyszukiwanie na [GitHub](https://github.com), na przykład ujawnić niezliczonych plików konfiguracyjnych z narażonych kluczy tajnych w repozytoriach publicznych.

Najlepszym rozwiązaniem jest przechowywanie tej informacji poza pliki konfiguracji aplikacji. Usługa App Service umożliwia przechowywanie informacji o konfiguracji w ramach środowiska wykonawczego jako **ustawień aplikacji** i **parametry połączenia**. Wartości są widoczne dla aplikacji w czasie wykonywania za pośrednictwem *zmiennych środowiskowych* większości języków programowania. W przypadku aplikacji .NET te wartości są wstrzykiwane do konfiguracji platformy .NET w czasie wykonywania. Oprócz tych sytuacji, te ustawienia konfiguracji będą pozostaną zaszyfrowane, jeśli nie możesz wyświetlić lub skonfigurować je za pomocą [Azure Portal](https://portal.azure.com) lub narzędzi, takich jak programu PowerShell lub wiersza polecenia platformy Azure. 

Zapisywanie informacji o konfiguracji w usłudze App Service umożliwia administratora aplikacji do blokowania poufne informacje w aplikacji produkcyjnej. Deweloperzy mogą używać osobny zestaw ustawień konfiguracji w celu opracowywania aplikacji i ustawienia mogą być automatycznie zastąpione z ustawieniami skonfigurowanymi w usłudze App Service. Nawet deweloperzy muszą znać kluczy tajnych skonfigurowany do aplikacji produkcyjnej. Aby uzyskać więcej informacji na temat konfigurowania ustawień aplikacji i parametry połączenia w usłudze App Service, zobacz [Konfigurowanie aplikacji sieci web](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Usługa aplikacji Azure zapewnia bezpieczny dostęp FTP do systemu plików dla aplikacji za pośrednictwem **FTPS**. Dzięki temu można bezpiecznie uzyskiwać dostęp do kodu aplikacji w aplikacji sieci web, a także diagnostyki dzienników. Zaleca się, że zawsze używać FTPS zamiast FTP. 

Łącze FTPS aplikacji znajdują się następujące kroki:

1. Otwórz [portalu Azure](https://portal.azure.com).
2. Wybierz **Przeglądaj wszystkie**.
3. Z **Przeglądaj** bloku, wybierz opcję **usługi aplikacji**.
4. Z **usługi aplikacji** bloku, wybierz odpowiednią aplikację.
5. W bloku aplikacji, wybierz **wszystkie ustawienia**.
6. Z **ustawienia** bloku, wybierz opcję **właściwości**.
7. Łącza FTP i FTPS znajdują się na **ustawienia** bloku. 

Aby uzyskać więcej informacji o FTPS, zobacz [File Transfer Protocol](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat zabezpieczeń platformy Azure, informacje dotyczące zgłaszania **nadużycia lub naruszenie zabezpieczeń**, lub powiadomienia firmy Microsoft, który będzie wykonywać **testowania penetracji** lokacji, zobacz sekcję zabezpieczeń [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Aby uzyskać więcej informacji na temat **web.config** lub **applicationhost.config** plików w aplikacji usługi App Service, zobacz [opcje konfiguracji w aplikacji sieci web w usłudze Azure App Service odblokowane](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Aby uzyskać informacje dotyczące rejestrowania informacji dla aplikacji usługi aplikacji, które mogą być przydatne w procesie wykrywania ataków, zobacz [włączyć rejestrowanie diagnostyczne](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą wersję początkową aplikacji w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

