---
title: "aaaSecure aplikacji w usłudze Azure App Service"
description: "Dowiedz się, jak toosecure aplikacji sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service."
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
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Zabezpieczanie aplikacji w usłudze Azure App Service
Ten artykuł ułatwia rozpoczęcie pracy dotyczące zabezpieczania aplikację sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service. 

Zabezpieczenia w usłudze Azure App Service ma dwa poziomy: 

* **Zabezpieczenia infrastruktury i platformy** -zaufania hello Azure toohave usług można niezbędne elementy tooactually Uruchom bezpiecznie w chmurze hello.
* **Zabezpieczenia aplikacji** — należy samej aplikacji hello toodesign bezpieczne. W tym sposób integracji z usługą Azure Active Directory, jak zarządzać certyfikatami i jak należy upewnić się, że możesz bezpiecznie porozmawiać toodifferent usług. 

#### <a name="infrastructure-and-platform-security"></a>Zabezpieczenia infrastruktury i platform
Ponieważ maszyny wirtualne Azure hello, magazynu, połączeń sieciowych, platformy sieci web, zarządzania i funkcje integracji i wiele innych przechowuje usługi aplikacji jest aktywnie zabezpieczone i wzmocnione zabezpieczenia i przechodzi przez intensywnie zgodności oraz sprawdza się, że na toomake stałego które:

* Aplikacji usługi aplikacji są odizolowane od obu hello Internet i z hello zasobów Azure dla innych klientów.
* Komunikacja klucze tajne (np. parametry połączenia) między aplikację usługi aplikacji i innych zasobów platformy Azure (np. Baza danych SQL) w grupie zasobów w obrębie platformy Azure i nie krzyżowe żadnych granic sieci. Hasła są zawsze szyfrowane.
* Cała komunikacja między aplikacji usługi aplikacji i zasobów zewnętrznych, takich jak zarządzanie w programie PowerShell, interfejsu wiersza polecenia Azure SDK, interfejsów API REST i połączeń hybrydowych było możliwe, były prawidłowo zaszyfrowane.
* 24-godzinnym threat management chroni zasoby usługi aplikacji przed złośliwym oprogramowaniem, distributed denial of service (DDoS), man-in--middle (MITM) i innymi zagrożeniami. 

Aby uzyskać więcej informacji na zabezpieczenia infrastruktury i platformy na platformie Azure, zobacz [Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Zabezpieczenia aplikacji
Azure jest odpowiedzialny za bezpieczeństwo infrastruktury hello i platformy, która aplikacja działa na, ale jest toosecure Twojego odpowiedzialność samej aplikacji. Innymi słowy, należy toodevelop, wdrażania i zarządzania kod aplikacji i zawartości w bezpieczny sposób. W przeciwnym razie z kodu aplikacji lub zawartości jest narażony toothreats takich jak:

* Iniekcja kodu SQL
* Przejęcie kontroli sesji
* Wykonywanie skryptów lokacji między
* MITM na poziomie aplikacji
* DDoS na poziomie aplikacji

Pełne omówienie zagadnienia dotyczące zabezpieczeń dla aplikacji sieci web wykracza poza zakres tego dokumentu hello. Jako punkt początkowy dla dodatkowych wskazówek dotyczących zabezpieczania aplikacji, zobacz hello [Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP)](https://www.owasp.org/index.php/Main_Page), w szczególności hello [10 pierwszych projektu.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), która list hello bieżącego 10 pierwszych krytyczne sieci web aplikacji luk w zabezpieczeniach, zgodnie z ustaleniami OWASP członków.

## <a name="perform-penetration-testing-on-your-app"></a>Wykonaj penetracji testowania w aplikacji
Jeden hello najprostszy sposób tooget wprowadzenie do badania luk w zabezpieczeniach w aplikacji usługi App Service jest toouse hello [integrację z usługa Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) tooperform luki w zabezpieczeniach jednym kliknięciem skanowanie w aplikacji. Możesz wyświetlić wyniki testów hello w raporcie o łatwe do zrozumienia i Dowiedz się, jak toofix każdego luki w zabezpieczeniach instrukcje krok po kroku.

Jeśli wolisz tooperform własne penetracji testów lub mają toouse inny dostawca lub skanera pakietu, należy wykonać hello [Azure penetracji testowanie procesu zatwierdzania](https://security-forms.azure.com/penetration-testing/terms) i uzyskiwanie penetracji hello potrzeby tooperform pobieraniu testy.

## <a name="https"></a>Zabezpieczenia komunikacji z klientami
Jeśli używasz hello  **\*. azurewebsites.net** nazwy domeny utworzonej dla aplikację usługi aplikacji można natychmiast jest używany protokół HTTPS, certyfikat SSL jest podane dla wszystkich  **\*. azurewebsites.net** nazw domen. Jeśli Twoja witryna wymaga [niestandardowej nazwy domeny](app-service-web-tutorial-custom-domain.md), można przekazać certyfikatu SSL za[włączyć protokół HTTPS](app-service-web-tutorial-custom-ssl.md) hello domeny niestandardowej.

Włączanie [HTTPS](https://en.wikipedia.org/wiki/HTTPS) może pomóc atakom MITM na powitania komunikacji między aplikacji i jej użytkowników.

## <a name="secure-data-tier"></a>Zabezpieczenia warstwy danych
Usługi aplikacji wysokiej integruje się z bazą danych SQL, tak, aby wszystkie parametry połączenia hello są szyfrowane w tablicy hello i odszyfrowane tylko na powitania maszyny Wirtualnej, aplikacja hello działa na *i* tylko hello po uruchomieniu aplikacji. Ponadto bazy danych SQL Azure zawiera wiele toohelp funkcje zabezpieczeń, należy zabezpieczyć dane aplikacji przed zagrożeniami przez, w tym [szyfrowania na rest](https://msdn.microsoft.com/library/dn948096.aspx), [zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt163865.aspx), [ Maskowanie danych dynamicznych](../sql-database/sql-database-dynamic-data-masking-get-started.md), i [wykrywanie zagrożeń](../sql-database/sql-database-threat-detection.md). Jeśli masz dane poufne lub wymagania dotyczące zgodności, zobacz [Zabezpieczanie bazy danych SQL](../sql-database/sql-database-security-overview.md) Aby uzyskać więcej informacji na temat toosecure danych.

Jeśli używasz dostawcy bazy danych z innych firm, takich jak ClearDB, należy skonsultować się z dokumentacją dostawcy hello bezpośrednio na najlepszych rozwiązaniach dotyczących zabezpieczeń.  

## <a name="develop"></a>Bezpieczne opracowywania i wdrażania
### <a name="publishing-profiles-and-publish-settings"></a>Publikowanie profile i ustawienia publikowania
Podczas tworzenia aplikacji, wykonywanie zadań zarządzania, lub automatyzacji zadań za pomocą narzędzi takich jak **programu Visual Studio**, **Web Matrix**, **programu Azure PowerShell** lub hello **Interfejsu wiersza polecenia platformy azure (Azure CLI)**, możesz użyć dowolnej *ustawień publikowania* pliku lub *profilu publikowania*. Zarówno typy uwierzytelniania Azure i powinien być zabezpieczony tooprevent nieautoryzowanego dostępu.

* A **ustawień publikowania** plik zawiera
  
  * Identyfikator subskrypcji platformy Azure
  * Certyfikat zarządzania, która pozwala tooperform zadania zarządzania dla subskrypcji *bez konieczności tooprovide nazwę użytkownika lub hasło*.
* A **profilu publikowania** plik zawiera
  
  * Informacje dotyczące publikowania aplikacji tooyour

Jeśli narzędzie używa pliku ustawień publikowania lub pliku profilu publikowania, zaimportuj plik hello zawierający ustawienia publikowania hello lub profilu do narzędzia hello, a następnie **usunąć** hello pliku. Jeśli należy zachować plik hello, tooshare osobom pracy nad projektem hello na przykład, zapisz go w bezpiecznej lokalizacji takich jak *zaszyfrowanych* katalogu z ograniczonymi uprawnieniami.

Ponadto należy upewnij się, że poświadczenia hello zaimportowane są zabezpieczone. Na przykład **programu Azure PowerShell** i hello **interfejsu wiersza polecenia platformy Azure (Azure CLI)** sklepów zaimportowanych informacji w sieci **katalogu macierzystego** ( *~*  w systemach Linux lub OS X i */users/nazwa_użytkownika* w systemach Windows.) Dla dodatkowego bezpieczeństwa możesz zbyt**szyfrowania** tych lokalizacji za pomocą szyfrowania narzędzi dostępnych w systemie operacyjnym.

### <a name="configuration-settings-and-connection-strings"></a>Ustawienia konfiguracji i parametry połączenia
Jest wspólne parametry połączenia toostore rozwiązaniem, poświadczenia uwierzytelniania i innych poufnych informacji w plikach konfiguracji. Niestety te pliki mogą być widoczne w witrynie sieci Web lub wyewidencjonowany do publicznego repozytorium, udostępnianie tych informacji. Proste wyszukiwanie na [GitHub](https://github.com), na przykład ujawnić niezliczonych plików konfiguracyjnych z narażonych kluczy tajnych w repozytoriach publicznych hello.

Witaj najlepszym rozwiązaniem jest tookeep tych informacji poza pliki konfiguracji aplikacji. Usługa App Service umożliwia przechowywanie informacji o konfiguracji w ramach środowiska uruchomieniowego hello jako **ustawień aplikacji** i **parametry połączenia**. wartości Hello są uwidocznione tooyour aplikacji w czasie wykonywania za pośrednictwem *zmiennych środowiskowych* większości języków programowania. W przypadku aplikacji .NET te wartości są wstrzykiwane do konfiguracji platformy .NET w czasie wykonywania. Oprócz tych sytuacji, te ustawienia konfiguracji będą pozostaną zaszyfrowane, jeśli nie możesz wyświetlić lub skonfigurować je za pomocą hello [Azure Portal](https://portal.azure.com) lub narzędzi, takich jak programu PowerShell lub hello wiersza polecenia platformy Azure. 

Zapisywanie informacji o konfiguracji w usłudze App Service umożliwia toolock administrator aplikacji hello poufnych informacji w przypadku aplikacji produkcyjnej hello. Deweloperzy mogą używać osobny zestaw ustawień konfiguracji w celu opracowywania aplikacji i hello ustawienia mogą być automatycznie zastąpione hello ustawienia skonfigurowane w usłudze App Service. Deweloperzy nie nawet hello muszą kluczy tajnych hello tooknow skonfigurowany dla hello aplikacji produkcyjnej. Aby uzyskać więcej informacji na temat konfigurowania ustawień aplikacji i parametry połączenia w usłudze App Service, zobacz [Konfigurowanie aplikacji sieci web](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Usługa aplikacji Azure udostępnia bezpieczne FTP dostępu toohello systemu plików dla aplikacji za pomocą **FTPS**. Dzięki temu można kodu aplikacji hello dostępu toosecurely na powitania aplikacji sieci web, a także diagnostyki dzienników. Zaleca się, że zawsze używać FTPS zamiast FTP. 

łącze FTPS Hello aplikacji można znaleźć z hello następujące kroki:

1. Otwórz hello [Azure Portal](https://portal.azure.com).
2. Wybierz **Przeglądaj wszystkie**.
3. Z hello **Przeglądaj** bloku, wybierz opcję **usługi aplikacji**.
4. Z hello **usługi aplikacji** bloku, wybierz hello żądanej aplikacji.
5. W bloku aplikacja hello wybierz **wszystkie ustawienia**.
6. Z hello **ustawienia** bloku, wybierz opcję **właściwości**.
7. Witaj FTP i FTPS łącza znajdują się na powitania **ustawienia** bloku. 

Aby uzyskać więcej informacji o FTPS, zobacz [File Transfer Protocol](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o zabezpieczeniach hello hello platformy Azure, informacje dotyczące zgłaszania **nadużycia lub naruszenie zabezpieczeń**, lub tooinform firmy Microsoft, który będzie wykonywać **testowania penetracji** z sieci lokacji, zobacz sekcję zabezpieczeń hello hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Aby uzyskać więcej informacji na temat **web.config** lub **applicationhost.config** plików w aplikacji usługi App Service, zobacz [opcje konfiguracji w aplikacji sieci web w usłudze Azure App Service odblokowane](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Aby uzyskać informacje dotyczące rejestrowania informacji dla aplikacji usługi aplikacji, które mogą być przydatne w procesie wykrywania ataków, zobacz [włączyć rejestrowanie diagnostyczne](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą wersję początkową aplikacji w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

