---
title: "aaaAzure bazy danych SQL — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Odpowiedzi toocommon pytania klientów poproś o baz danych w chmurze i baza danych SQL Azure, system zarządzania relacyjnymi bazami danych firmy Microsoft (RDBMS) oraz bazy danych jako usługa w chmurze hello."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 1da12abc-0646-43ba-b564-e3b049a6487f
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 02/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 04c02f96e6e91cf314221134ee0ef6d24217ef45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-faq"></a>SQL Database — często zadawane pytania

## <a name="what-is-hello-current-version-of-sql-database"></a>Co to jest hello bieżąca wersja bazy danych SQL?
Bieżąca wersja Hello bazy danych SQL jest w wersji 12. W wersji V11 została wycofana.

## <a name="what-is-hello-sla-for-sql-database"></a>Co to jest hello umowy SLA dla bazy danych SQL?
Gwarantujemy co najmniej 99,99% hello klientów będzie mieć łączność między ich pojedyncze lub elastyczne Basic, Standard, lub baza danych SQL Premium Microsoft Azure i naszych bramą internetową. Aby uzyskać więcej informacji, zobacz [SLA](http://azure.microsoft.com/support/legal/sla/).

## <a name="how-do-i-reset-hello-password-for-hello-server-admin"></a>Jak zresetować hasła hello Witaj, Administratorze serwera?
W hello [portalu Azure](https://portal.azure.com) kliknij **serwerów SQL**, wybierz z listy hello powitania serwera, a następnie kliknij przycisk **Resetuj hasło**.

## <a name="how-do-i-manage-databases-and-logins"></a>Jak zarządzać baz danych i logowania
Zobacz [Zarządzanie bazami danych i logowaniami](sql-database-manage-logins.md).

## <a name="how-do-i-make-sure-only-authorized-ip-addresses-are-allowed-tooaccess-a-server"></a>Jak utworzyć się tylko autoryzowani adresy IP są dozwolone tooaccess serwer?
Zobacz [porady: Konfigurowanie ustawień zapory w bazie danych SQL](sql-database-configure-firewall-settings.md).

## <a name="how-does-hello-usage-of-sql-database-show-up-on-my-bill"></a>Jak jest użycie hello bazy danych SQL wyświetlany na mojego rachunku?
Opłaty bazy danych SQL na przewidywalną, godzinową szybkość oparte na zarówno hello warstwy usług i wydajności poziomu dla pojedynczych baz danych lub Edtu dla każdej puli elastycznej. Rzeczywistego użycia jest obliczana i proporcjonalnie co godzinę, więc rachunku mogą być wyświetlane ułamków godzinę. Na przykład jeśli baza danych istnieje na 12 godzin w miesiącu, rachunku pokazuje użycie 0,5 dni. Ponadto są dzielone warstwy usług i poziom wydajności i jednostek Edtu na pulę out w hello rachunku toomake go łatwiejsze toosee hello liczbie dni bazy danych używane dla każdej z nich w ciągu jednego miesiąca.

## <a name="what-if-a-single-database-is-active-for-less-than-an-hour-or-uses-a-higher-service-tier-for-less-than-an-hour"></a>Co zrobić, jeśli pojedynczej bazy danych jest aktywna na mniej niż godzinę lub używa wyższego poziomu usług mniej niż godzinę?
Opłaty są naliczane dla każdej godziny, który istnieje baza danych przy użyciu hello najwyższej warstwy usług i wydajności poziom zastosowane podczas tej godziny, niezależnie od użycia i czy hello bazy danych było aktywne przez mniej niż godzinę. Po utworzeniu pojedynczej bazy danych i usunąć go pięciu minut rachunku odzwierciedla opłat godzinę jedną bazę danych. 

Przykłady

* Jeśli tworzenie podstawowej bazy danych, a następnie od razu ją uaktualnić tooStandard S1, naliczane są opłaty według stawki standardowe S1 hello dla hello pierwszej godziny.
* W przypadku uaktualnienia bazy danych z podstawowych tooPremium na 10:00 w dniu i zakończeniu uaktualniania 1:35 o godzinie na powitania dnia naliczane są opłaty szybkością Premium hello, rozpoczynając od godziny 1:00 
* Jeśli starszą wersję bazy danych w warstwie Premium tooBasic o 11:00 wykonuje na 2:15:00, a następnie hello bazy danych jest rozliczana według stawek hello do 3:00 w dniu, po upływie którego jest rozliczana stawkami podstawowe hello.

## <a name="how-does-elastic-pool-usage-show-up-on-my-bill-and-what-happens-when-i-change-edtus-per-pool"></a>Jak jest użycie puli elastycznej wyświetlany na mojego rachunku i co się stanie po zmianie jednostek Edtu na pulę?
Puli elastycznej opłat Pokaż na rachunku jako elastycznej Dtu (Edtu) w przyrostach hello wyświetlany w obszarze jednostek Edtu na pulę na [hello cennikiem](https://azure.microsoft.com/pricing/details/sql-database/). Jest bezpłatna dla bazy danych dla puli elastycznej. Opłaty są naliczane dla każdej godziny puli istnieje w najwyższym eDTU hello niezależnie od użycia i czy pula hello było aktywne przez mniej niż godzinę. 

Przykłady

* Po utworzeniu standardowej puli elastycznej z 200 Edtu o godzinie 11:18 Dodawanie puli toohello pięć baz danych, naliczane są opłaty dla 200 jednostek Edtu dla całego godziny hello, od o godzinie 11 za pomocą hello pozostałej części hello dnia.
* W dniu 2, 5 o godzinie: 05 1 bazy danych rozpocznie korzystanie z 50 jednostek Edtu i przechowuje stałej hello dzień. Bazy danych 2-5 zmieniają się między 0 a Edtu 80. W ciągu dnia hello można dodać pięć innych baz danych używających różnych jednostek Edtu w ciągu dnia hello. Dzień 2 jest pełny dzień rozliczane według 200 eDTU. 
* W dniu 3, 5 o godzinie Możesz dodać inny 15 baz danych. W punkcie toohello dzień hello decyzję dotyczącą tooincrease Edtu puli powitania od 200 too400 8 o godzinie: 05 powoduje zwiększenie użycia bazy danych Opłaty na poziomie eDTU hello 200 były obowiązywać do 20: 00 i zwiększa too400 Edtu dla hello pozostałych czterech godzin. 

## <a name="elastic-pool-billing-and-pricing-information"></a>Informacje o cenach i rozliczeniami puli elastycznej
Elastyczne pule są rozliczane na powitania następujące cechy:

* Pula elastyczna jest on rozliczany po jego utworzeniu, nawet jeśli nie ma baz danych w puli hello.
* Pula elastyczna jest rozliczane co godzinę. Jest to hello samego pomiaru częstotliwości, podobnie jak w przypadku poziomy wydajności pojedynczej bazy danych.
* Jeśli po zmianie rozmiaru tooa nowej puli elastycznej liczbę jednostek Edtu, następnie puli hello nie jest rozliczane zgodnie z toohello nowe liczby jednostek Edtu do momentu ukończenia hello zmiana rozmiaru operacji. Wynika to hello sam wzorca podczas zmieniania poziomu wydajności hello pojedynczych baz danych.
* Cena Hello elastycznej puli jest oparta na powitania liczbę jednostek Edtu puli hello. Cena Hello puli elastycznej jest niezależna od liczby hello i użycie hello elastycznych baz danych w niej.
* Cena jest obliczana przez (liczba jednostek Edtu puli) x (cena jednostki na eDTU).

Witaj jednostki eDTU ceny dla puli elastycznej jest wyższy niż hello jednostki DTU ceny dla pojedynczej bazy danych w hello tej samej warstwie usługi. Szczegóły można znaleźć w [cenniku usługi SQL Database](https://azure.microsoft.com/pricing/details/sql-database/). 

warstwy usług i jednostek Edtu toounderstand hello, zobacz [opcje bazy danych SQL i wydajność](sql-database-service-tiers.md).

## <a name="how-does-hello-use-of-active-geo-replication-in-an-elastic-pool-show-up-on-my-bill"></a>Jak program hello używa z aktywna replikacja geograficzna w będą wyświetlane puli elastycznej na mojego rachunku?
W przeciwieństwie do pojedynczych baz danych przy użyciu [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) z elastycznych baz danych nie ma to bezpośredni wpływ rozliczeń.  Naliczane są tylko opłaty dla jednostek Edtu hello udostępnione dla poszczególnych pul hello (puli głównej i dodatkowej puli)

## <a name="how-does-hello-use-of-hello-auditing-feature-impact-my-bill"></a>Jak program hello używa z hello inspekcji wpływ funkcji mojego rachunku?
Inspekcja jest oparty na powitania usługi baza danych SQL bez dodatkowych kosztów i jest dostępny tooBasic, Standard, Premium i Premium RS baz danych. Jednak toostore hello dzienniki inspekcji, hello inspekcji funkcji używa konta usługi Azure Storage oraz szybkości dla tabel i kolejek w usłudze Azure Storage są stosowane na podstawie rozmiaru hello dziennika inspekcji.

## <a name="how-do-i-find-hello-right-service-tier-and-performance-level-for-single-databases-and-elastic-pools"></a>Jak znaleźć hello usługowy warstwę i poziom wydajności dla pojedynczych baz danych i pul elastycznych?
Istnieje kilka tooyou dostępne narzędzia. 

* Dla lokalnych baz danych, użyj hello [advisor zmiany rozmiaru jednostek dtu w warstwie](http://dtucalculator.azurewebsites.net/) toorecommend hello baz danych i Dtu wymagane i ocena wielu baz danych dla puli elastycznej.
* Jeśli pojedynczej bazy danych będzie korzystać z w puli, inteligentnego aparatu Azure zaleca puli elastycznej, jeśli wzorzec historycznych danych użycia, która go. Zobacz [monitorowanie i zarządzanie nimi pula elastyczna o hello portalu Azure](sql-database-elastic-pool-manage-portal.md). Aby uzyskać szczegółowe informacje dotyczące sposobu toodo hello matematyczne samodzielnie, zobacz [zagadnienia dotyczące cen i wydajności dla elastycznej puli](sql-database-elastic-pool.md)
* toosee czy potrzebujesz toodial pojedynczej bazy danych w górę lub w dół, zobacz [wytyczne dotyczące wydajności dla pojedynczej bazy danych](sql-database-performance-guidance.md).

## <a name="how-often-can-i-change-hello-service-tier-or-performance-level-of-a-single-database"></a>Jak często można zmienić hello usługi warstwy wydajności poziom lub pojedynczej bazy danych?
Można zmienić warstwy usług hello (między Basic, Standard, Premium i Premium RS) lub często mają hello poziom wydajności w ramach warstwy usług (na przykład tooS2 S1). Dla wcześniejszych wersji baz danych można zmienić poziom wydajności ani warstwy usługi hello łącznie cztery razy w okresie 24 godzin.

## <a name="how-often-can-i-adjust-hello-edtus-per-pool"></a>Jak często można dostosować hello Edtu na pulę?
Tyle razy, ile ma.

## <a name="how-long-does-it-take-toochange-hello-service-tier-or-performance-level-of-a-single-database-or-move-a-database-in-and-out-of-an-elastic-pool"></a>Jak długo czy go zająć toochange hello usługi warstwy wydajności poziom lub pojedynczej bazy danych lub przenieść bazę danych i elastycznej puli?
Zmiana hello warstwy usługi bazy danych i przenoszenia i wylogowywanie puli wymaga toobe bazy danych hello skopiowany na platformie hello jako operacji w tle. Zmiana warstwy usług hello może trwać od kilku minut tooseveral godzin w zależności od wielkości hello hello baz danych. W obu przypadkach hello baz danych pozostaną online i dostępne podczas przenoszenia hello. Aby uzyskać więcej informacji na temat zmieniania pojedynczych baz danych, zobacz [warstwy usług hello zmiany bazy danych](sql-database-service-tiers.md). 

## <a name="when-should-i-use-a-single-database-vs-elastic-databases"></a>Kiedy należy używać pojedynczej bazy danych, a elastycznych baz danych?
Ogólnie rzecz biorąc, elastyczne pule są przeznaczone dla typowe [oprogramowanie jako usługa (SaaS) aplikacji wzorzec](sql-database-design-patterns-multi-tenancy-saas-applications.md), gdy istnieje jedną bazę danych na dzierżawcy lub klienta. Zakupów pojedynczych baz danych i wymaga zmiennej hello toomeet i szczytowego popytu dla każdej bazy danych jest często nie koszty. Pule Zarządzanie hello łączną wydajność puli hello i baz danych hello górę i w dół skalować automatycznie. Inteligentnego aparatu platformy Azure zaleca puli baz danych, gdy użycie wzorca gwarantuje on. Aby uzyskać więcej informacji, zobacz [wskazówki dotyczące puli elastycznej](sql-database-elastic-pool.md).

## <a name="what-does-it-mean-toohave-up-too200-of-your-maximum-provisioned-database-storage-for-backup-storage"></a>Co to znaczy toohave % too200 magazynu maksymalną elastycznie bazy danych w magazynie kopii zapasowej?
Magazyn kopii zapasowych jest skojarzone z kopii zapasowych automatycznych bazy danych, które są używane do przechowywania hello [punkt-w — czas-przywracania](sql-database-recovery-using-backups.md#point-in-time-restore) i [geograficzne](sql-database-recovery-using-backups.md#geo-restore). Baza danych SQL Azure Microsoft udostępnia % too200 maksymalną elastycznie bazy danych magazynu kopii zapasowych magazynu bez ponoszenia dodatkowych kosztów. Na przykład jeśli wystąpienie standardowe bazy danych o rozmiarze DB elastycznie 250 GB, są dostarczane z 500 GB magazynu kopii zapasowej bez dodatkowych opłat. Jeśli bazy danych przekroczy hello podane magazynu kopii zapasowej, można wybrać okres przechowywania hello tooreduce kontaktując się z pomocą techniczną platformy Azure lub opłacać hello bardzo magazynu kopii zapasowych rozliczane według stawki standardowej dostęp do odczytu geograficznie magazynu geograficznie nadmiarowego (RA-GRS). Aby uzyskać więcej informacji dotyczących rozliczeń RA-GRS Zobacz szczegóły cennika magazynu.

## <a name="im-moving-from-webbusiness-toohello-new-service-tiers-what-do-i-need-tooknow"></a>Przeprowadzam z sieci Web/firm toohello nowe warstwy usług, czego potrzebuję tooknow?
Azure baz danych SQL w sieci Web i Business teraz zostały wycofane. warstwy Basic, Standard, Premium, Premium RS i elastyczna Hello Zastąp hello wycofanie baz danych w sieci Web i Business. 

## <a name="what-is-an-expected-replication-lag-when-geo-replicating-a-database-between-two-regions-within-hello-same-azure-geography"></a>Co to jest opóźnienie replikacji oczekiwanego podczas replikację geograficzną a bazy danych między dwóch regionach w ramach sam hello Azure geograficzne?
Możemy są obecnie obsługiwane RPO pięciu sekund i opóźnienie replikacji hello jest mniejsza niż kiedy hello geograficznie / pomocniczych znajduje się w hello Azure zalecane sparowanego regionu i na powitania sam warstwę usługi.

## <a name="what-is-an-expected-replication-lag-when-geo-secondary-is-created-in-hello-same-region-as-hello-primary-database"></a>Co to jest opóźnienie replikacji oczekiwanego podczas dodatkowej geograficzna w hello sam region jako hello podstawowej bazy danych?
Na podstawie empiryczne danych, nie istnieje za dużo różnica między wewnątrz regionu i opóźnienie replikacji między region stosowania hello Azure zalecane sparowanego regionu. 

## <a name="if-there-is-a-network-failure-between-two-regions-how-does-hello-retry-logic-work-when-geo-replication-is-set-up"></a>Jeśli występuje awaria sieci między dwóch regionach, jak logika ponowień hello działa po skonfigurowaniu replikacji geograficznej?
W przypadku rozłączenia, wykonanie co 10 sekund toore-nawiązywać połączenia.

## <a name="what-can-i-do-tooguarantee-that-a-critical-change-on-hello-primary-database-is-replicated"></a>Co można zrobić tooguarantee, że krytyczne zmiany na powitania podstawowej bazy danych są replikowane?
Hello geograficznie pomocniczy jest replika asynchronicznych i nie spróbujemy tookeep w pełnej synchronizacji z hello podstawowego. Ale zapewniamy metodę tooforce synchronizacji tooensure hello replikacji zmian krytyczne (na przykład aktualizacji hasła). Wymuszone synchronizacji wpływa na wydajność, ponieważ wątek wywołujący hello blokuje dopóki wszystkie zatwierdzone transakcje są replikowane. Aby uzyskać więcej informacji, zobacz [operacja sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx). 

## <a name="what-tools-are-available-toomonitor-hello-replication-lag-between-hello-primary-database-and-geo-secondary"></a>Jakie narzędzia są dostępne toomonitor opóźnienie replikacji hello między hello podstawowej bazy danych i dodatkowej geograficzna?
Uwidaczniamy hello opóźnienie replikacji w czasie rzeczywistym między hello podstawowej bazy danych i geograficzna / pomocniczych za pośrednictwem DMV. Aby uzyskać więcej informacji, zobacz [sys.dm_geo_replication_link_status](https://msdn.microsoft.com/library/mt575504.aspx).

## <a name="toomove-a-database-tooa-different-server-in-hello-same-subscription"></a>toomove bazy danych tooa innego serwera w hello tej samej subskrypcji
* W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **baz danych SQL**, wybierz z listy hello bazę danych, a następnie kliknij przycisk **kopiowania**. Zobacz [kopiowania bazy danych Azure SQL](sql-database-copy.md) uzyskać więcej szczegółowych informacji.

## <a name="toomove-a-database-between-subscriptions"></a>toomove bazy danych między subskrypcjami
* W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **serwerów SQL** a następnie wybierz serwer hello, który jest hostem bazy danych z listy hello. Kliknij przycisk **Przenieś**, a następnie wybierz hello toomove zasobów i hello toomove subskrypcji do.
