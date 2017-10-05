---
title: Klasy korporacyjnej WordPress na platformie Azure | Dokumentacja firmy Microsoft
description: "Informacje o sposobie obsługi przedsiębiorstw witryny WordPress w usłudze Azure App Service"
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
ms.openlocfilehash: 21281955458a2632d96a91d884cab13803f4d296
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Klasy korporacyjnej WordPress na platformie Azure
Usługa aplikacji Azure oferuje skalowalne, bezpieczne i łatwe w użyciu środowisko dla krytycznym, dużych [WordPress] [ wordpress] witryny. Microsoft sama działa takich jak lokacje klasy korporacyjnej [Office] [ officeblog] i [Bing] [ bingblog] blogów. W tym artykule przedstawiono sposób korzystania z funkcji aplikacji sieci Web programu Microsoft Azure App Service i obsługa klasy korporacyjnej, oparte na chmurze witryny WordPress, który może obsługiwać dużą odwiedzin.

## <a name="architecture-and-planning"></a>Planowanie i architektura
Podstawowa instalacja WordPress ma tylko dwóch wymagań:

* **Baza danych MySQL**: to wymaganie jest dostępna za pośrednictwem [ClearDB w portalu Azure Marketplace][cdbnstore]. Alternatywnie, można zarządzać własne MySQL instalacja na maszynach wirtualnych platformy Azure przy użyciu [Windows] [ mysqlwindows] lub [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB udostępnia kilka konfiguracji MySQL. W każdej konfiguracji została różnych parametrów. Zobacz [magazynu Azure] [ cdbnstore] informacji o oferty, które znajdują się za pomocą magazynu Azure lub bezpośrednio, jak pokazano na [ClearDB witryny sieci Web](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 lub większą**: obecnie udostępnia usługi Azure App Service [wersji PHP 5.4, 5.5 i 5.6][phpwebsite].

  > [!NOTE]
  > Firma Microsoft zaleca zawsze uruchamiaj najnowszej wersji programu PHP, co wymaga najnowszych poprawek zabezpieczeń.
  >
  >

### <a name="basic-deployment"></a>Podstawy wdrażania
Jeśli używasz podstawowych wymagań, można utworzyć podstawowego rozwiązania w obrębie regionu platformy Azure.

![Aplikacja sieci web platformy Azure i baza danych MySQL hostowanej w pojedynczym regionie Azure][basic-diagram]

Mimo że temu będzie można utworzyć wiele wystąpień aplikacji sieci Web witryny do skalowania aplikacji, wszystko jest obsługiwana w centrach danych w określonym regionie geograficznym. Osoby odwiedzające z poza tym regionie może pojawić się wydłużają czas odpowiedzi podczas korzystają z witryny. W przypadku centrów danych w tym regionie wyłączenia, co powoduje aplikacji.

### <a name="multi-region-deployment"></a>W przypadku wdrożenia
Za pomocą usługi Azure [Traffic Manager][trafficmanager], można skalować witryny WordPress w różnych regionach geograficznych i podaj ten sam adres URL dla wszystkich odwiedzających. Wszystkich odwiedzających są dostępne w Menedżerze ruchu, a następnie są kierowane do regionu, która jest oparta na konfiguracji równoważenia obciążenia.

![Aplikacja sieci web platformy Azure hostowanej w wielu regionach, przy użyciu routera CDBR wysokiej dostępności do kierowania do MySQL w regionach][multi-region-diagram]

W każdym regionie witryny WordPress nadal będzie można skalować w wielu wystąpieniach aplikacji sieci Web, ale ta skalowanie jest specyficzne dla regionu. Regiony dużym natężeniu ruchu i regiony mniejszym natężeniu ruchu może być skalowana w inny sposób.

Aby replikować i kierować ruchem do wielu baz danych MySQL, można użyć [ClearDB routery wysokiej dostępności (CDBRs)] [ cleardbscale] (wyświetlane po lewej stronie) lub [MySQL klastra operatora klasy Edition (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>W przypadku wdrożenia z nośników magazynowania i buforowanie
Jeśli lokacji akceptuje przekazywania lub plików multimedialnych hostów, użyj magazynu obiektów Blob platformy Azure. Buforowanie, należy wziąć pod uwagę [pamięci podręcznej Redis][rediscache], [chmury Memcache](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), lub jeden z buforowania oferty w [ Magazyn Azure](http://azure.microsoft.com/gallery/store/).

![Aplikacja sieci web platformy Azure hostowanej w wielu regionach, przy użyciu routera CDBR wysoką dostępność dla programu MySQL zarządzane pamięci podręcznej, magazynu obiektów Blob i Content Delivery Network][performance-diagram]

Magazyn obiektów blob jest rozproszona geograficznie w regionach domyślnie, tak aby nie trzeba martwić się o replikacji plików we wszystkich lokacjach. Można również włączyć Azure [Content Delivery Network] [ cdn] dla magazynu obiektów Blob, który dystrybuuje pliki, aby zakończyć węzły, które są bliższe odwiedzających.

### <a name="planning"></a>Planowanie
#### <a name="additional-requirements"></a>Wymagania dodatkowe
| Aby wykonać tę czynność... | Użyj polecenia... |
| --- | --- |
| **Przekazywanie lub przechowywania dużych plików** |[Wtyczki WordPress dla przy użyciu magazynu obiektów Blob][storageplugin] |
| **Wyślij wiadomość e-mail** |[SendGrid] [ storesendgrid] i [wtyczki WordPress dla przy użyciu SendGrid][sendgridplugin] |
| **Niestandardowa nazwa domeny** |[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service][customdomain] |
| **PROTOKÓŁ HTTPS** |[Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service][httpscustomdomain] |
| **Sprawdzanie poprawności produkcji wstępnej** |[Konfigurowanie środowisk dla aplikacji sieci web w usłudze Azure App Service przejściowych][staging] <p>Podczas przenoszenia aplikacji sieci web z obszaru przemieszczania do środowiska produkcyjnego, można również przenosić konfiguracji WordPress. Upewnij się, że wszystkie ustawienia są aktualizowane w celu wymagania dotyczące aplikacji produkcyjnych przed przeniesieniem przygotowanych aplikacji do środowiska produkcyjnego.</p> |
| **Monitorowanie i rozwiązywanie problemów** |[Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service] [ log] i [monitorowanie aplikacji sieci Web w usłudze Azure App Service][monitor] |
| **Wdrażanie witryny** |[Wdrażanie aplikacji sieci web w usłudze Azure App Service][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Dostępność i odzyskiwanie po awarii
| Aby wykonać tę czynność... | Użyj polecenia... |
| --- | --- |
| **Lokacje Równoważenie obciążenia** lub **geograficznie-dystrybucji lokacji** |[Kierować ruchem z usługi Azure Traffic Manager][trafficmanager] |
| **Tworzenie kopii zapasowej i przywracanie** |[Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service] [ backup] i [Przywracanie aplikacji sieci web w usłudze Azure App Service][restore] |

#### <a name="performance"></a>Wydajność
Wydajność w chmurze jest osiągana, przede wszystkim dzięki buforowaniu oraz skalowalnych w poziomie. Jednak należy rozważyć pamięć, przepustowości i inne atrybuty hosting aplikacji sieci Web.

| Aby wykonać tę czynność... | Użyj polecenia... |
| --- | --- |
| **Zrozumieć możliwości wystąpienia usługi aplikacji** |[Informacje o cenach, łącznie z możliwości warstwy usług aplikacji][websitepricing] |
| **Zasoby pamięci podręcznej** |[Pamięci podręcznej redis][rediscache], [chmury Memcache](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), lub jeden z buforowania oferty w [magazynu Azure](/gallery/store/) |
| **Skalowanie aplikacji** |[Skalowanie aplikacji sieci web w usłudze Azure App Service] [ websitescale] i [ClearDB wysokiej dostępności routingu][cleardbscale]. Jeśli wybierzesz do zarządzania własnych instalacji MySQL, należy rozważyć [CGE klastra MySQL] [ cge] dla skalowalnego w poziomie. |

#### <a name="migration"></a>Migracja
Istnieją dwie metody, aby przeprowadzić migrację istniejącej witryny WordPress w usłudze Azure App Service:

* **[Eksportuj WordPress][export]**: Ta metoda eksportuje zawartość blogu. Następnie można zaimportować zawartość do nowej witryny WordPress w usłudze Azure App Service przy użyciu [wtyczki WordPress importera][import].

  > [!NOTE]
  > Podczas tego procesu pozwala migrować zawartość, nie są migrowane się jakieś wtyczki, kompozycje lub inne dostosowania. Te składniki należy zainstalować ponownie ręcznie.
  >
  >
* **Ręcznej migracji**: [kopię zapasową witryny] [ wordpressbackup] i [bazy danych][wordpressdbbackup], a następnie ręcznie przywrócić go do aplikacji sieci web na platformie Azure Usługi aplikacji i skojarzona baza danych MySQL. Ta metoda jest przydatna do migracji lokacji wysoce dostosowane, ponieważ pozwala ona na uniknięcie konieczność ręcznej instalacji wtyczek, kompozycje i inne dostosowania powtarzania.

## <a name="step-by-step-instructions"></a>Instrukcje krok po kroku
### <a name="create-a-wordpress-site"></a>Utwórz witrynę WordPress
1. Użyj [portalu Azure Marketplace] [ cdbnstore] do tworzenia bazy danych MySQL o rozmiarze, który został zidentyfikowany w [architektury i planowania](#planning) sekcji w regionie lub regionach, gdzie będą hostowanie witryny.
2. Postępuj zgodnie z instrukcjami [tworzenie aplikacji sieci web WordPress w usłudze Azure App Service] [ createwordpress] do utworzenia aplikacji sieci web WordPress. Podczas tworzenia aplikacji sieci web wybierz **Użyj istniejącej bazy danych MySQL**, a następnie wybierz bazę danych, który został utworzony w kroku 1.

W przypadku migracji z istniejącej witryny WordPress, zobacz [migracji istniejącej witryny WordPress na platformie Azure](#Migrate-an-existing-WordPress-site-to-Azure) po utworzeniu nowej aplikacji sieci web.

### <a name="migrate-an-existing-wordpress-site-to-azure"></a>Migracji istniejącej witryny WordPress na platformie Azure
Jak wspomniano w [architektury i planowania](#planning) sekcji, można dokonać migracji witryny WordPress na dwa sposoby:

* **Używać funkcji eksportowania i importowania** dla witryn, które nie mają dużo dostosowywania lub gdy chcesz przenieść zawartość.
* **Użyj kopii zapasowej i przywracania** dla witryn, które mają wiele możliwości dostosowania gdzie chcesz przenieść wszystkie elementy.

Użyj jednej z następujących sekcji się dokonanie migracji lokacji.

#### <a name="the-export-and-import-method"></a>Eksportowanie i importowanie — metoda
1. Użyj [wyeksportować WordPress] [ export] do wyeksportowania istniejącej lokacji.
2. Tworzenie aplikacji sieci web za pomocą kroków w [Utwórz witrynę WordPress](#Create-a-new-WordPress-site) sekcji.
3. Zaloguj się do witryny WordPress [portalu Azure][mgmtportal], a następnie kliknij przycisk **wtyczek** > **Dodaj nowy**. Wyszukiwanie i instalowanie **importera WordPress** wtyczki.
4. Po zainstalowaniu dodatku importera WordPress kliknij **narzędzia** > **importu**, a następnie kliknij przycisk **WordPress** do użycia wtyczki WordPress importera.
5. Na **WordPress importu** kliknij przycisk **wybierz plik**. Znajdź plik WXR, który został wyeksportowany z istniejącej witryny WordPress, a następnie kliknij przycisk **przekazywania pliku, a następnie zaimportuj**.
6. Kliknij przycisk **przesłać**. Zostanie wyświetlony monit, że importowanie zakończyło się pomyślnie.
7. Po wykonaniu wszystkich tych kroków należy ponownie uruchomić witryny z jego **usługi aplikacji** bloku w [portalu Azure][mgmtportal].

Po zaimportowaniu lokacji, może być konieczne wykonaj następujące kroki, aby włączyć ustawienia, które nie znajdują się w pliku importu.

| W przypadku używania to... | W tym celu... |
| --- | --- |
| **Stałych** |Na pulpicie nawigacyjnym WordPress nowej lokacji, kliknij **ustawienia** > **stałych**, a następnie zaktualizuj struktury stałych. |
| **łącza obrazu/media** |Aby zaktualizować łącza do nowej lokalizacji, należy użyć [wtyczkę aktualizacji adresów URL niebieskie Mietlica][velvet], wyszukaj i Zamień narzędzie lub ręcznie zaktualizować linki w bazie danych. |
| **Motywy** |Przejdź do **wygląd** > **motyw**, a następnie zaktualizuj motyw witryny, zgodnie z potrzebami. |
| **Menu** |Jeśli kompozycję obsługuje menu, linki do strony głównej nadal obowiązują podkatalogu starego osadzonych w tych obiektach. Przejdź do **wygląd** > **menu**, a następnie zaktualizuj je. |

#### <a name="the-backup-and-restore-method"></a>Metoda tworzenia kopii zapasowych i przywracania
1. Utwórz kopię zapasową programu WordPress istniejących lokacji, korzystając z informacji w [kopii zapasowych WordPress][wordpressbackup].
2. Utwórz kopię zapasową istniejącej bazy danych, korzystając z informacji w [wykonywanie kopii zapasowej bazy danych][wordpressdbbackup].
3. Utwórz bazę danych i przywracanie kopii zapasowej.

   1. Kup nową bazę danych z [portalu Azure Marketplace][cdbnstore], lub skonfigurować bazę danych MySQL na [Windows] [ mysqlwindows] lub [Linux] [ mysqllinux] maszyny wirtualnej.
   2. Używanie klienta MySQL, takich jak [MySQL Workbench] [ workbench] do połączenia z bazą danych i zaimportuj WordPress bazy danych.
   3. Aktualizowanie bazy danych, aby zmienić wpisy domeny do nowej domeny usługi Azure App Service, na przykład mywordpress.azurewebsites.net. Użyj [wyszukiwania i zamieniania WordPress baz danych skryptu] [ searchandreplace] można bezpiecznie zmienić wszystkie wystąpienia.
4. Tworzenie aplikacji sieci web w portalu Azure i publikowanie WordPress kopii zapasowej.

   1. Aby utworzyć aplikację sieci web, który ma w bazie danych [portalu Azure][mgmtportal], kliknij przycisk **nowy** > **sieci Web i mobilność**  >  **Witrynę azure Marketplace** > **Web Apps** > **aplikacja sieci Web i SQL** (lub **aplikacja sieci Web i MySQL**) > **Utworzyć**. Skonfiguruj wszystkie wymagane ustawienia, aby utworzyć pustą aplikację sieci web.
   2. Kopia zapasowa WordPress, zlokalizuj **wp config.php** pliku i otwórz go w edytorze. Informacje dotyczące nowej bazy danych MySQL Zastąp następujące wpisy:

      * **DB_NAME**: nazwa użytkownika bazy danych.
      * **DB_USER**: nazwa użytkownika używana do dostępu do bazy danych.
      * **DB_PASSWORD**: hasło użytkownika.

        Po zmianie tych pozycji Zapisz i Zamknij **wp config.php** pliku.
   3. Użyj [wdrażanie aplikacji sieci web w usłudze Azure App Service] [ deploy] informacje umożliwiające metody wdrażania, której chcesz użyć, a następnie wdrożyć kopii zapasowej WordPress do aplikacji sieci web w usłudze Azure App Service.
5. Po wdrożeniu witryny WordPress powinno być możliwe dostęp do nowej lokacji (jako aplikacji sieci web usługi App Service) przy użyciu *. azurewebsite.net adres URL witryny.

### <a name="configure-your-site"></a>Konfigurowanie lokacji
Po została utworzona lub migracji witryny WordPress, skorzystaj z poniższych informacji, aby poprawić wydajność lub włączyć dodatkowe funkcje.

| Aby wykonać tę czynność... | Użyj polecenia... |
| --- | --- |
| **Ustaw tryb planu usługi aplikacji, rozmiar i Włączanie skalowania** |[Skalowanie aplikacji sieci web w usłudze Azure App Service][websitescale]. |
| **Włącz połączenia trwałe bazy danych** |Domyślnie program WordPress nie korzysta z połączenia trwałe bazy danych, które może spowodować, że połączenie z bazą danych do ograniczany stanie po wielu połączeń. Aby umożliwić połączenia trwałe, zainstaluj [wtyczki karty połączeń trwałych](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Poprawianie wydajności** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Wyłącz ARR cookie</a>, które może poprawić wydajność w przypadku uruchomienia WordPress na wiele wystąpień aplikacji sieci Web.</p></li><li><p>Włącz buforowanie. Można użyć <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">pamięci podręcznej Redis</a> (Podgląd) z <a href="https://wordpress.org/plugins/redis-object-cache/">wtyczki WordPress obiektu pamięci podręcznej Redis</a>, lub można użyć jednej z buforowania ofert z <a href="/gallery/store/">magazynu Azure</a>.</p></li><li><p>[Wprowadź WordPress szybsze z Wincache](https://wordpress.org/plugins/w3-total-cache/). Wincache jest domyślnie włączone dla aplikacji sieci web. Podczas korzystania ze sobą WinCache i dynamiczne pamięci podręcznej, wyłącz WinCache w pamięci podręcznej plików, ale pozostawić użytkownika i włączone pamięci podręcznej sesji. Aby wyłączyć pamięć podręczną plików w pliku .ini na poziomie systemu, należy ustawić następującą wartość:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Skalowanie aplikacji sieci web w usłudze Azure App Service] [ websitescale] i użyj <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB wysokiej dostępności routingu</a> lub <a href="http://www.mysql.com/products/cluster/">CGE klastra MySQL</a>.</p></li></ul> |
| **Użyj magazynu obiektów blob** |<ol><li><p>[Tworzenie konta magazynu Azure](../storage/common/storage-create-storage-account.md).</p></li><li><p>Dowiedz się, jak [używają sieci dystrybucji zawartości](../cdn/cdn-create-new-endpoint.md) do geograficznie-dystrybucji danych przechowywanych w obiektach blob.</p></li><li><p>Instalowanie i konfigurowanie <a href="https://wordpress.org/plugins/windows-azure-storage/">magazyn Azure dla wtyczki WordPress</a>.</p><p>Aby uzyskać szczegółowe ustawienia oraz informacje o konfiguracji dla wtyczki, zobacz <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">Podręcznik użytkownika</a>.</p> </li></ol> |
| **Włącz poczty e-mail** |Włącz <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> przy użyciu magazynu Azure. Zainstaluj <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">wtyczki SendGrid</a> platformy WordPress. |
| **Konfigurowanie niestandardowej nazwy domeny** |[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service][customdomain]. |
| **Włącz protokół HTTPS dla niestandardowej nazwy domeny** |[Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service][httpscustomdomain]. |
| **Obciążenia Saldo lub geograficznie-dystrybucji lokacji** |[Kierować ruchem z usługi Azure Traffic Manager][trafficmanager]. Jeśli używasz niestandardowej domeny, zobacz [Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service] [ customdomain] informacji o sposobie użycia Menedżera ruchu z niestandardowych nazw domen. |
| **Włącz automatyczne kopie zapasowe** |[Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service][backup]. |
| **Włączanie rejestrowania diagnostyki** |[Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service][log]. |

## <a name="next-steps"></a>Następne kroki
* [Optymalizacja WordPress](http://codex.wordpress.org/WordPress_Optimization)
* [Konwertuj WordPress na wielu lokacjach w usłudze Azure App Service](web-sites-php-convert-wordpress-multisite.md)
* [Kreator Azure uaktualnienia ClearDB](http://www.cleardb.com/store/azure/upgrade)
* [Hosting WordPress w podfolderze aplikacji sieci web w usłudze Azure App Service](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Krok po kroku: Tworzenie witryny WordPress korzysta z platformy Azure](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Host istniejących bloga WordPress na platformie Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Włączanie automatycznego stałych w WordPress](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Jak migrować i uruchomić bloga WordPress w usłudze Azure App Service](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Jak uruchomić WordPress w usłudze Azure App Service za darmo](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress na platformie Azure w ciągu 2 minut lub mniej](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Przenoszenie bloga WordPress na platformie Azure — część 1: Tworzenie bloga WordPress na platformie Azure](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Przenoszenie bloga WordPress na platformie Azure — część 2: transfer zawartości](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Przenoszenie bloga WordPress na platformie Azure — część 3: Konfigurowanie domeny niestandardowej](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Przenoszenie bloga WordPress na platformie Azure — część 4: Pretty stałych i ponowne zapisywanie adresów URL reguły](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Przenoszenie bloga WordPress na platformie Azure — część 5: przejście z podfolderu do katalogu głównego](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Jak skonfigurować aplikację sieci web WordPress w konta platformy Azure](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Propping się WordPress na platformie Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Porady dotyczące WordPress na platformie Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Jeśli chcesz rozpocząć pracę z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do [Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Wymagane są bez kart kredytowych i bez zobowiązań.
>
>

## <a name="whats-changed"></a>Co zostało zmienione
Przewodnik dotyczący zmiany z witryn sieci Web w usłudze App Service, zobacz [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

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
