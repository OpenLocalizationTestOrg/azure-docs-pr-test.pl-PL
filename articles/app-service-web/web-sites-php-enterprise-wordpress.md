---
title: Klasa aaaEnterprise WordPress na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toohost WordPress przedsiębiorstw lokacji w usłudze Azure App Service"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Klasy korporacyjnej WordPress na platformie Azure
Usługa aplikacji Azure oferuje skalowalne, bezpieczne i łatwe w użyciu środowisko dla krytycznym, dużych [WordPress] [ wordpress] witryny. Microsoft sama działa witrynach przedsiębiorstw, takich jak hello [Office] [ officeblog] i [Bing] [ bingblog] blogów. W tym artykule opisano sposób toouse hello funkcji aplikacji sieci Web programu Microsoft Azure App Service tooestablish i obsługa klasy korporacyjnej, oparte na chmurze witryny WordPress, który może obsługiwać dużą odwiedzin.

## <a name="architecture-and-planning"></a>Planowanie i architektura
Podstawowa instalacja WordPress ma tylko dwóch wymagań:

* **Baza danych MySQL**: to wymaganie jest dostępna za pośrednictwem [ClearDB w portalu Azure Marketplace hello][cdbnstore]. Alternatywnie, można zarządzać własne MySQL instalacja na maszynach wirtualnych platformy Azure przy użyciu [Windows] [ mysqlwindows] lub [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB udostępnia kilka konfiguracji MySQL. W każdej konfiguracji została różnych parametrów. Zobacz hello [magazynu Azure] [ cdbnstore] informacji o oferty, które znajdują się za pomocą magazynu Azure hello lub bezpośrednio, jak pokazano na powitania [ClearDB witryny sieci Web](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 lub większą**: obecnie udostępnia usługi Azure App Service [wersji PHP 5.4, 5.5 i 5.6][phpwebsite].

  > [!NOTE]
  > Firma Microsoft zaleca tego należy zawsze wykonywania hello najnowszej wersji programu PHP, co wymaga hello najnowszych poprawek zabezpieczeń.
  >
  >

### <a name="basic-deployment"></a>Podstawy wdrażania
Jeśli używasz tylko hello podstawowych wymagań można utworzyć podstawowego rozwiązania w obrębie regionu platformy Azure.

![Aplikacja sieci web platformy Azure i baza danych MySQL hostowanej w pojedynczym regionie Azure][basic-diagram]

Mimo że temu będzie można utworzyć wiele wystąpień aplikacji sieci Web tooscale lokacji hello limit aplikacji, wszystko jest obsługiwana w centrach danych hello w określonym regionie geograficznym. Wydłużają czas odpowiedzi podczas korzystają z witryny hello mogą pojawić się gości z poza tym regionie. Jeśli hello centrów danych, w tym regionie przestaną działać, dlatego nie aplikacji.

### <a name="multi-region-deployment"></a>W przypadku wdrożenia
Za pomocą usługi Azure [Traffic Manager][trafficmanager], można skalować witryny WordPress w różnych regionach geograficznych i podaj hello tego samego adresu URL dla wszystkich odwiedzających. Wszystkich odwiedzających są dostępne w Menedżerze ruchu i są następnie region tooa routingiem, na podstawie hello konfiguracji równoważenia obciążenia.

![Aplikacja sieci web platformy Azure hostowanej w wielu regionach, przy użyciu tooMySQL tooroute router CDBR wysokiej dostępności w regionach][multi-region-diagram]

W każdym regionie witryny WordPress hello nadal będzie można skalować w wielu wystąpieniach aplikacji sieci Web, ale ta skalowanie jest tooa określonego regionu. Regiony dużym natężeniu ruchu i regiony mniejszym natężeniu ruchu może być skalowana w inny sposób.

tooreplicate i tras ruchu toomultiple baz danych MySQL, można użyć [ClearDB routery wysokiej dostępności (CDBRs)] [ cleardbscale] (wyświetlane po lewej stronie) lub [MySQL klastra operatora klasy Edition (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>W przypadku wdrożenia z nośników magazynowania i buforowanie
Jeśli witryna hello akceptuje przekazywania lub plików multimedialnych hostów, użyj magazynu obiektów Blob platformy Azure. Buforowanie, należy wziąć pod uwagę [pamięci podręcznej Redis][rediscache], [chmury Memcache](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), lub jeden z innych buforowania oferty w hello hello [Magazynu azure](http://azure.microsoft.com/gallery/store/).

![Aplikacja sieci web platformy Azure hostowanej w wielu regionach, przy użyciu routera CDBR wysoką dostępność dla programu MySQL zarządzane pamięci podręcznej, magazynu obiektów Blob i Content Delivery Network][performance-diagram]

Magazyn obiektów blob jest rozproszona geograficznie w regionach domyślnie, dzięki czemu nie trzeba tooworry o replikacji plików we wszystkich lokacjach. Można również włączyć hello Azure [Content Delivery Network] [ cdn] dla magazynu obiektów Blob, który dystrybuuje węzłów tooend pliki, które są bliższe odwiedzających tooyour.

### <a name="planning"></a>Planowanie
#### <a name="additional-requirements"></a>Wymagania dodatkowe
| toodo to... | Użyj polecenia... |
| --- | --- |
| **Przekazywanie lub przechowywania dużych plików** |[Wtyczki WordPress dla przy użyciu magazynu obiektów Blob][storageplugin] |
| **Wyślij wiadomość e-mail** |[SendGrid] [ storesendgrid] i hello [wtyczki WordPress dla przy użyciu SendGrid][sendgridplugin] |
| **Niestandardowa nazwa domeny** |[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service][customdomain] |
| **PROTOKÓŁ HTTPS** |[Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service][httpscustomdomain] |
| **Sprawdzanie poprawności produkcji wstępnej** |[Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych][staging] <p>Po przeniesieniu aplikacji sieci web z tymczasowej tooproduction również przenieść hello WordPress konfiguracji. Upewnij się, czy wszystkie ustawienia są toohello zaktualizowane wymagania dotyczące aplikacji produkcyjnych, przed przeniesieniem tooproduction aplikacji hello przemieszczane.</p> |
| **Monitorowanie i rozwiązywanie problemów** |[Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service] [ log] i [monitorowanie aplikacji sieci Web w usłudze Azure App Service][monitor] |
| **Wdrażanie witryny** |[Wdrażanie aplikacji sieci web w usłudze Azure App Service][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Dostępność i odzyskiwanie po awarii
| toodo to... | Użyj polecenia... |
| --- | --- |
| **Lokacje Równoważenie obciążenia** lub **geograficznie-dystrybucji lokacji** |[Kierować ruchem z usługi Azure Traffic Manager][trafficmanager] |
| **Tworzenie kopii zapasowej i przywracanie** |[Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service] [ backup] i [Przywracanie aplikacji sieci web w usłudze Azure App Service][restore] |

#### <a name="performance"></a>Wydajność
Wydajność w chmurze hello jest osiągana, przede wszystkim dzięki buforowaniu oraz skalowalnych w poziomie. Jednak należy rozważyć hello pamięci, przepustowości i inne atrybuty hosting aplikacji sieci Web.

| toodo to... | Użyj polecenia... |
| --- | --- |
| **Zrozumieć możliwości wystąpienia usługi aplikacji** |[Informacje o cenach, łącznie z możliwości warstwy usług aplikacji][websitepricing] |
| **Zasoby pamięci podręcznej** |[Pamięć podręczna redis][rediscache], [chmury Memcache](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), lub jeden z innych buforowania oferty w hello hello [magazynu Azure](/gallery/store/) |
| **Skalowanie aplikacji** |[Skalowanie aplikacji sieci web w usłudze Azure App Service] [ websitescale] i [ClearDB wysokiej dostępności routingu][cleardbscale]. Jeśli możesz wybrać toohost i zarządzać instalacji MySQL, należy rozważyć [CGE klastra MySQL] [ cge] dla skalowalnego w poziomie. |

#### <a name="migration"></a>Migracja
Istnieją dwie metody toomigrate istniejącej witryny WordPress tooAzure usługi aplikacji:

* **[Eksportuj WordPress][export]**: Ta metoda eksportuje zawartości hello wpis w blogu. Następnie można zaimportować hello zawartości tooa nowej witryny WordPress w usłudze Azure App Service przy użyciu hello [wtyczki WordPress importera][import].

  > [!NOTE]
  > Podczas tego procesu pozwala migrować zawartość, nie są migrowane się jakieś wtyczki, kompozycje lub inne dostosowania. Te składniki należy zainstalować ponownie ręcznie.
  >
  >
* **Ręcznej migracji**: [kopię zapasową witryny] [ wordpressbackup] i [bazy danych][wordpressdbbackup], a następnie przywróć ją ręcznie tooa aplikacji sieci web na platformie Azure Usługi aplikacji i skojarzona baza danych MySQL. Ta metoda jest przydatne toomigrate wysoce dostosowane witryny, ponieważ takie rozwiązanie pomaga uniknąć konieczność powtarzania hello ręcznego instalowania wtyczek, kompozycje i inne dostosowania.

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku
### <a name="create-a-wordpress-site"></a>Utwórz witrynę WordPress
1. Użyj hello [portalu Azure Marketplace] [ cdbnstore] toocreate bazę danych MySQL rozmiaru hello, który został zidentyfikowany w hello [architektury i planowania](#planning) sekcji w regionie hello lub regionów gdy zostanie hosta witryny.
2. Wykonaj kroki hello w [tworzenie aplikacji sieci web WordPress w usłudze Azure App Service] [ createwordpress] toocreate aplikacji sieci web WordPress. Podczas tworzenia aplikacji sieci web hello wybrać **Użyj istniejącej bazy danych MySQL**, a następnie wybierz hello bazy danych, który został utworzony w kroku 1.

W przypadku migracji z istniejącej witryny WordPress, zobacz [migracji istniejącej tooAzure witryny WordPress](#Migrate-an-existing-WordPress-site-to-Azure) po utworzeniu nowej aplikacji sieci web.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Migrowanie istniejących tooAzure witryny WordPress
Jak wspomniano w hello [architektury i planowania](#planning) sekcji, istnieją dwa sposoby toomigrate witrynę WordPress:

* **Używać funkcji eksportowania i importowania** dla witryn, nie mają dużo dostosowywania lub gdzie chcesz toomove hello zawartości.
* **Użyj kopii zapasowej i przywracania** dla witryn, które mają wiele możliwości dostosowania miejscu toomove wszystko.

Użyj jednej z hello następujące sekcje toomigrate witryny.

#### <a name="hello-export-and-import-method"></a>Witaj eksportowania i importowania — metoda
1. Użyj [wyeksportować WordPress] [ export] tooexport istniejącą witrynę.
2. Tworzenie aplikacji sieci web za pomocą kroków hello w hello [Utwórz witrynę WordPress](#Create-a-new-WordPress-site) sekcji.
3. Zaloguj się w witrynie WordPress tooyour na powitania [portalu Azure][mgmtportal], a następnie kliknij przycisk **wtyczek** > **Dodaj nowy**. Wyszukiwanie i instalowanie hello **importera WordPress** wtyczki.
4. Po zainstalowaniu hello wtyczki importera WordPress kliknij **narzędzia** > **importu**, a następnie kliknij przycisk **WordPress** toouse hello wtyczki WordPress importera.
5. Na powitania **WordPress importu** kliknij przycisk **wybierz plik**. Znajdź plik WXR hello, który został wyeksportowany z istniejącej witryny WordPress, a następnie kliknij przycisk **przekazywania pliku, a następnie zaimportuj**.
6. Kliknij przycisk **przesłać**. Zostanie wyświetlony monit, że hello importowanie zakończyło się pomyślnie.
7. Po wykonaniu wszystkich tych kroków należy ponownie uruchomić witryny z jego **usługi aplikacji** bloku w hello [portalu Azure][mgmtportal].

Po zaimportowaniu hello lokacji, może być konieczne hello tooperform następujące ustawienia tooenable kroki, które nie znajdują się w pliku importu hello.

| W przypadku używania to... | W tym celu... |
| --- | --- |
| **Stałych** |Z poziomu pulpitu nawigacyjnego WordPress hello hello nowej lokacji, kliknij przycisk **ustawienia** > **stałych**, a następnie zaktualizuj hello stałych struktury. |
| **łącza obrazu/media** |tooupdate łączy toohello nowej lokalizacji, należy użyć hello [wtyczkę aktualizacji adresów URL niebieskie Mietlica][velvet], wyszukaj i Zamień narzędzie lub ręcznie zaktualizować łącza hello w bazie danych. |
| **Motywy** |Przejdź za**wygląd** > **motyw**, a następnie zaktualizuj motyw witryny hello zgodnie z potrzebami. |
| **Menu** |Kompozycję obsługuje menu, strony głównej tooyour łącza mogą nadal zawierać hello podkatalogu starego osadzonych w tych obiektach. Przejdź za**wygląd** > **menu**, a następnie zaktualizuj je. |

#### <a name="hello-backup-and-restore-method"></a>Witaj kopii zapasowej i przywracania — metoda
1. Utwórz kopię zapasową programu WordPress istniejących lokacji przy użyciu informacji hello na [kopii zapasowych WordPress][wordpressbackup].
2. Utwórz kopię zapasową istniejącej bazy danych przy użyciu informacji hello na [wykonywanie kopii zapasowej bazy danych][wordpressdbbackup].
3. Utwórz bazę danych i przywracanie kopii zapasowej hello.

   1. Kup nową bazę danych z hello [portalu Azure Marketplace][cdbnstore], lub skonfigurować bazę danych MySQL na [Windows] [ mysqlwindows] lub [systemu Linux ] [ mysqllinux] maszyny wirtualnej.
   2. Używanie klienta MySQL, takich jak [MySQL Workbench] [ workbench] toohello tooconnect nowe bazy danych, a następnie zaimportuj WordPress bazy danych.
   3. Aktualizacja hello bazy danych toochange hello domeny wpisów tooyour nowej usłudze Azure App Service domeny, na przykład mywordpress.azurewebsites.net. Użyj hello [wyszukiwania i zamieniania WordPress baz danych skryptu] [ searchandreplace] toosafely należy zastąpić wszystkie wystąpienia.
4. Tworzenie aplikacji sieci web w portalu Azure hello i opublikować hello WordPress w kopii zapasowej.

   1. toocreate aplikacji sieci web z bazą danych, w hello [portalu Azure][mgmtportal], kliknij przycisk **nowy** > **sieci Web i mobilność**  >  **Witrynę azure Marketplace** > **Web Apps** > **aplikacja sieci Web i SQL** (lub **aplikacja sieci Web i MySQL**) > **Utworzyć**. Skonfiguruj wszystkie wymagane hello toocreate ustawienia pustą aplikację sieci web.
   2. Kopia zapasowa WordPress, zlokalizuj hello **wp config.php** pliku i otwórz go w edytorze. Zastąp następujące wpisy hello informacje dla nowej bazy danych MySQL hello:

      * **DB_NAME**: nazwa użytkownika hello hello bazy danych.
      * **DB_USER**: hello użytkownika nazwę używaną tooaccess hello bazy danych.
      * **DB_PASSWORD**: hello hasło użytkownika.

        Po zmianie tych pozycji Zapisz i zamknij hello **wp config.php** pliku.
   3. Użyj hello [wdrażanie aplikacji sieci web w usłudze Azure App Service] [ deploy] informacji tooenable hello metody wdrażania mają toouse, a następnie wdrożyć tooyour kopii zapasowej aplikacji sieci web WordPress w usłudze Azure App Service.
5. Po wdrożeniu witryny WordPress hello (jako aplikacji sieci web usługi App Service) należy tooaccess stanie hello nowej lokacji za pomocą hello *. adres URL azurewebsite.net hello witryny.

### <a name="configure-your-site"></a>Konfigurowanie lokacji
Po witryny WordPress hello została utworzona lub migracji, użyj następujących informacji o wydajności tooimprove hello lub włączyć dodatkowe funkcje.

| toodo to... | Użyj polecenia... |
| --- | --- |
| **Ustaw tryb planu usługi aplikacji, rozmiar i Włączanie skalowania** |[Skalowanie aplikacji sieci web w usłudze Azure App Service][websitescale]. |
| **Włącz połączenia trwałe bazy danych** |Domyślnie program WordPress nie korzysta z połączenia trwałe bazy danych, co może spowodować Twojej bazy danych toobecome toohello połączenia ograniczany po wielu połączeń. tooenable połączeń trwałych, zainstaluj hello [wtyczki karty połączeń trwałych](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Poprawianie wydajności** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Wyłącz hello ARR cookie</a>, które może poprawić wydajność w przypadku uruchomienia WordPress na wiele wystąpień aplikacji sieci Web.</p></li><li><p>Włącz buforowanie. Można użyć <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">pamięci podręcznej Redis</a> (Podgląd) z hello <a href="https://wordpress.org/plugins/redis-object-cache/">wtyczki WordPress obiektu pamięci podręcznej Redis</a>, lub można użyć jednej z hello innych buforowania ofert z hello <a href="/gallery/store/">magazynu Azure</a>.</p></li><li><p>[Wprowadź WordPress szybsze z Wincache](https://wordpress.org/plugins/w3-total-cache/). Wincache jest domyślnie włączone dla aplikacji sieci web. Podczas korzystania ze sobą WinCache i dynamiczne pamięci podręcznej, wyłącz WinCache w pamięci podręcznej plików, ale pozostawić hello użytkownika i włączone pamięci podręcznej sesji. tooturn poza pamięci podręcznej plików, która znajduje się w pliku .ini na poziomie systemu, ustaw hello następujące wartości:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Skalowanie aplikacji sieci web w usłudze Azure App Service] [ websitescale] i użyj <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB wysokiej dostępności routingu</a> lub <a href="http://www.mysql.com/products/cluster/">CGE klastra MySQL</a>.</p></li></ul> |
| **Użyj magazynu obiektów blob** |<ol><li><p>[Tworzenie konta magazynu Azure](../storage/common/storage-create-storage-account.md).</p></li><li><p>Dowiedz się, jak za[hello użycia sieci dystrybucji zawartości](../cdn/cdn-create-new-endpoint.md) toogeo-dystrybucji danych przechowywanych w obiektach blob.</p></li><li><p>Instalowanie i konfigurowanie hello <a href="https://wordpress.org/plugins/windows-azure-storage/">magazyn Azure dla wtyczki WordPress</a>.</p><p>Aby uzyskać szczegółowe ustawienia oraz informacje o konfiguracji dla wtyczki hello, zobacz hello <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">Podręcznik użytkownika</a>.</p> </li></ol> |
| **Włącz poczty e-mail** |Włącz <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> przy użyciu hello magazynu Azure. Zainstaluj hello <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">wtyczki SendGrid</a> platformy WordPress. |
| **Konfigurowanie niestandardowej nazwy domeny** |[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service][customdomain]. |
| **Włącz protokół HTTPS dla niestandardowej nazwy domeny** |[Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service][httpscustomdomain]. |
| **Obciążenia Saldo lub geograficznie-dystrybucji lokacji** |[Kierować ruchem z usługi Azure Traffic Manager][trafficmanager]. Jeśli używasz niestandardowej domeny, zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service] [ customdomain] informacje na temat toouse Menedżera ruchu z niestandardowych nazw domen. |
| **Włącz automatyczne kopie zapasowe** |[Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service][backup]. |
| **Włączanie rejestrowania diagnostyki** |[Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service][log]. |

## <a name="next-steps"></a>Następne kroki
* [Optymalizacja WordPress](http://codex.wordpress.org/WordPress_Optimization)
* [Konwertuj toomultisite WordPress w usłudze Azure App Service](web-sites-php-convert-wordpress-multisite.md)
* [Kreator Azure uaktualnienia ClearDB](http://www.cleardb.com/store/azure/upgrade)
* [Hosting WordPress w podfolderze aplikacji sieci web w usłudze Azure App Service](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Krok po kroku: Tworzenie witryny WordPress korzysta z platformy Azure](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Host istniejących bloga WordPress na platformie Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Włączanie automatycznego stałych w WordPress](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Jak toomigrate i uruchom bloga WordPress w usłudze Azure App Service](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [W jaki sposób toorun WordPress w usłudze Azure App Service dla w warstwie bezpłatna](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress na platformie Azure w ciągu 2 minut lub mniej](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Przenoszenie tooAzure blogu WordPress — część 1: Tworzenie bloga WordPress na platformie Azure](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Przenoszenie tooAzure blogu WordPress — część 2: transfer zawartości](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Przenoszenie tooAzure blogu WordPress — część 3: Konfigurowanie domeny niestandardowej](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Przenoszenie tooAzure blogu WordPress — część 4: Pretty stałych i ponowne zapisywanie adresów URL reguły](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Przenoszenie tooAzure blogu WordPress — część 5: przejście z głównego toohello podfolderu](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Jak tooset się WordPress sieci web aplikacji w konta platformy Azure](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Propping się WordPress na platformie Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Porady dotyczące WordPress na platformie Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Wymagane są bez kart kredytowych i bez zobowiązań.
>
>

## <a name="whats-changed"></a>Co zostało zmienione
Przewodnik toohello zmian z tooApp witryn sieci Web Service, zobacz [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
