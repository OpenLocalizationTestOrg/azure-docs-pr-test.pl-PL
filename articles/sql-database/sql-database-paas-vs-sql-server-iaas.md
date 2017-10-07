---
title: vs bazy danych aaaSQL (PaaS). Program SQL Server w chmurze hello na maszynach wirtualnych (IaaS) | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej opcji programu SQL Server chmurze jest odpowiednia do używanej aplikacji: Azure SQL Database (PaaS) lub SQL Server w chmurze hello na maszynach wirtualnych platformy Azure."
services: sql-database, virtual-machines
keywords: Chmury programu SQL Server, SQL Server w chmurze hello, PaaS w bazie danych programu SQL Server, DBaaS w chmurze
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>Wybieranie opcji programu SQL Server w chmurze: usługa Azure SQL Database (PaaS) lub program SQL Server na maszynach wirtualnych Azure (IaaS)
Platforma Azure ma dwie opcje do obsługi obciążeń programu SQL Server na platformie Microsoft Azure:

* [Baza danych SQL Azure](https://azure.microsoft.com/services/sql-database/): chmury toohello natywnej bazy danych A SQL, znanej także jako platforma jako usługa (PaaS) lub bazy danych jako usługa (DBaaS), która jest zoptymalizowana pod kątem tworzenia aplikacji oprogramowania jako usługa (SaaS). Zapewnia zgodność z większością funkcji programu SQL Server. Aby uzyskać więcej informacji o usłudze PaaS, zobacz [Co to jest PaaS](https://azure.microsoft.com/overview/what-is-paas/).
* [SQL Server na maszynach wirtualnych Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/): SQL Server zainstalowany i hostowany w chmurze hello na systemu Windows Server maszynach wirtualnych (VM) na platformie Azure, znany również jako infrastruktura jako usługa (IaaS).
  Program SQL Server w usłudze Azure Virtual Machines został zoptymalizowany pod kątem migrowania istniejących aplikacji programu SQL Server. Witaj wszystkich wersji i wydań programu SQL Server są dostępne. Zapewnia ona 100% zgodności z programem SQL Server, dzięki czemu możesz toohost dowolną liczbę baz danych jako wymagane i wykonywanie transakcji między bazami danych. Zapewnia on pełną kontrolę w programie SQL Server i systemie Windows.

Dowiedz się, jak każdej opcji dopasowuje się do platformy danych firmy Microsoft hello i uzyskać pomoc pasującego hello odpowiedniej opcji tooyour wymagań biznesowych. Czy priorytetem jest oszczędność, czy ograniczenie administracji do minimum wszystkich innych urządzeń, w tym artykule mogą pomóc zdecydować, które rozwiązanie pozwoli względem wymagań biznesowych hello się, że Ci najbardziej zależy.

## <a name="microsofts-data-platform"></a>Platforma danych firmy Microsoft
Jednym z pierwszego toounderstand rzeczy hello podczas każdej dyskusji dotyczącej Azure w zestawieniu z lokalnych baz danych programu SQL Server jest czy można używać ich wszystkich. Platforma danych firmy Microsoft korzysta z technologii programu SQL Server i udostępnia ją na fizycznych komputerach lokalnych, w prywatnych środowiskach chmury, prywatnych środowiskach chmury udostępnianych przez inne firmy i w chmurze publicznej. SQL Server na maszynach wirtualnych Azure pozwala potrzeb biznesowych unikatowych i różnych toomeet przy użyciu kombinacji lokalnych i hostowanych w chmurze wdrożenia, gdy przy użyciu hello tego samego zestawu produktów serwerowych, narzędzi do tworzenia i doświadczenia w tych środowiska.

   ![Opcje programu SQL Server w chmurze: program SQL server na IaaS lub SaaS SQL bazy danych w chmurze hello.](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Jak pokazano na diagramie hello, każdy rozwiązanie można scharakteryzować hello poziomu administracji, nad hello infrastruktury (na osi hello X) oraz hello stopnia opłacalności wynikającej z konsolidacji poziomu bazy danych i automatyzacji (na osi hello Y).

Podczas projektowania aplikacji, cztery podstawowe opcje są dostępne dla hostingu hello programu SQL Server część aplikacji hello:

* program SQL Server na niezwirtualizowanych komputerach fizycznych,
* program SQL Server na lokalnych komputerach zwirtualizowanych (w chmurze prywatnej),
* program SQL Server na maszynie wirtualnej platformy Azure (w chmurze publicznej firmy Microsoft),
* usługa Azure SQL Database (w chmurze publicznej firmy Microsoft).

W następujące sekcje hello, możesz dowiedzieć się o programie SQL Server w hello firmy Microsoft w chmurze publicznej: usługi Azure SQL Database i programu SQL Server na maszynach wirtualnych Azure. Ponadto przeanalizujemy typowe czynniki motywujące związane z działalnością biznesową, aby ustalić, która opcja jest najlepsza dla aplikacji.

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>Bliższe spojrzenie na usługę Azure SQL Database i program SQL Server na maszynach wirtualnych platformy Azure
**Baza danych SQL Azure** jest relacyjnej bazy danych jako — usługa (DBaaS) hostowanych w hello chmury Azure, która należy do kategorii branżowych hello *oprogramowania — jako — usługa (SaaS)* i *platforma jako usługa (PaaS)* . [Baza danych SQL](sql-database-technical-overview.md) działa na ustandaryzowanym sprzęcie i oprogramowaniu, które stanowi własność firmy Microsoft, jest przez nią hostowane i konserwowane. W usłudze SQL Database można programować bezpośrednio na powitania usługi przy użyciu wbudowanych funkcji i funkcjonalności. Podczas korzystania z bazy danych SQL, płatność z tooscale opcje górę lub w poziomie dla większe możliwości, dzięki czemu.

**SQL Server na maszynach wirtualnych Azure (VM)** należy do kategorii branżowych hello *infrastruktury jako — usługa (IaaS)* i pozwala toorun programu SQL Server w maszynie wirtualnej w chmurze hello. Podobne tooSQL bazy danych jest oparty na ze standardami sprzęcie, będące własnością, obsługiwane i obsługiwanego przez firmę Microsoft. Program SQL Server na maszynie wirtualnej umożliwia płatność zgodnie z rzeczywistym użyciem za licencję programu SQL Server dołączoną do obrazu programu SQL Server lub łatwe użycie istniejącej licencji. Można również łatwo skalę, w górę lub w dół i wstrzymanie/wznowienie hello maszyny Wirtualnej zgodnie z potrzebami.

Ogólnie rzecz biorąc, te dwie opcje są zoptymalizowane do różnych celów:

* **Baza danych SQL Azure** jest zoptymalizowany tooreduce ogólne koszty toohello minimalna inicjowania obsługi i zarządzania nimi wielu baz danych. Obniża bieżące koszty administracyjne, ponieważ nie masz toomanage wszystkie maszyny wirtualne, systemu operacyjnego ani oprogramowaniem bazy danych. Nie masz toomanage uaktualnień, wysokiej dostępności lub [kopii zapasowych](sql-database-automated-backups.md). Ogólnie rzecz biorąc, usługi Azure SQL Database może znacząco zwiększyć hello liczba baz danych zarządzanych przez pojedynczy IT lub tworzenia zasobu.
* **Program SQL Server uruchomiony na maszynach wirtualnych Azure** jest zoptymalizowana pod kątem Migrowanie istniejących aplikacji tooAzure lub rozszerzanie istniejących, lokalnych aplikacji toohello chmury we wdrożeniach hybrydowych. Ponadto można używać programu SQL Server w toodevelop maszyny wirtualnej i przetestować tradycyjne aplikacje programu SQL Server. Program SQL Server na maszynach wirtualnych platformy Azure masz hello pełne prawa administracyjne przez dedykowane wystąpienie programu SQL Server i maszyny Wirtualnej opartej na chmurze. Gdy organizacja już ma maszyn wirtualnych hello toomaintain dostępne zasoby IT jest doskonałym rozwiązaniem. Te funkcje umożliwiają toobuild tooaddress doskonale dopasowanego systemu, dotyczące wydajności i dostępności wymagań aplikacji.

Witaj w poniższej tabeli przedstawiono podsumowanie hello głównych cech usługi SQL Database i programu SQL Server na maszynach wirtualnych platformy Azure:

| **Najlepsze dla:** | **Azure SQL Database** | **SQL Server na maszynie wirtualnej platformy Azure** |
| --- | --- | --- |
|  |Nowe aplikacje zaprojektowane dla chmury, które mają ograniczenia czasowe w zakresie projektowania i marketingu. |Istniejące aplikacje, które wymagają szybkiej migracji toohello chmury przy minimalnych zmianach. Szybkie projektowania i testowania scenariuszy nie należy toobuy lokalnymi nieprodukcyjnych programu SQL Server sprzętu. |
|  | Zespoły, które wymagają wbudowanej wysokiej dostępności, odzyskiwania po awarii i uaktualniania hello bazy danych. |Zespoły, które mogą konfigurować wysoką dostępność, odzyskiwanie po awarii i poprawki dla programu SQL Server oraz zarządzać nimi. Niektóre dostępne funkcje automatyczne znacznie to upraszczają. | |
|  | Zespoły, które nie ma toomanage hello system operacyjny i ustawienia konfiguracji. |Potrzebne jest dostosowane środowisko z pełnymi prawami administracyjnymi. | |
|  | Baz danych w górę too4 TB lub większych baz danych, które mogą być [poziomo czy pionowo podzielona na partycje](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) przy użyciu wzorca skalowalnego w poziomie. |Wystąpień programu SQL Server z zapasowej too64 TB pamięci masowej. wystąpienie Hello może obsługiwać dowolną liczbę baz danych, zgodnie z potrzebami. | |
|  | [Tworzenie aplikacji typu oprogramowanie jako usługa (SaaS)](sql-database-design-patterns-multi-tenancy-saas-applications.md). |Migrowanie i tworzenie aplikacji dla przedsiębiorstw i aplikacji hybrydowych. | |
|  | | |
| **Zasoby:** |Nie ma tooemploy IT zasoby dotyczące konfiguracji i zarządzania hello podstawowej infrastruktury, ale mają toofocus na warstwie aplikacji hello. |Masz niektóre zasoby informatyczne do konfiguracji i zarządzania. Niektóre dostępne funkcje automatyczne znacznie to upraszczają. |
| **Całkowity koszt posiadania:** |Eliminuje koszty sprzętu i ogranicza koszty administracyjne. |Eliminuje koszty sprzętu. |
| **Ciągłość działalności biznesowej:** |W dodanie toobuilt w odporność na uszkodzenia infrastruktury możliwościach bazy danych SQL Azure udostępnia funkcje, takie jak [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md), [w momencie przywracania](sql-database-recovery-using-backups.md#point-in-time-restore), [przywracaniem geograficznym](sql-database-recovery-using-backups.md#geo-restore), i [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) tooincrease ciągłość działania. Więcej informacji znajduje się w temacie [Omówienie ciągłości działalności biznesowej usługi SQL Database](sql-database-business-continuity.md). |Program SQL Server na maszynach wirtualnych platformy Azure umożliwia skonfigurowanie rozwiązania wysokiej dostępności i odzyskiwania po awarii w zależności od określonych potrzeb bazy danych. Można mieć zatem system w znacznym stopniu zoptymalizowany dla aplikacji. Jeśli wystąpi taka potrzeba, tryb failover można przetestować i uruchomić samodzielnie. Więcej informacji znajduje się w temacie [Wysoka dostępność i odzyskiwanie po awarii dla programu SQL Server w usłudze Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md). |
| **Chmura hybrydowa:** |Aplikacja lokalna może uzyskiwać dostęp do danych w usłudze Azure SQL Database. |Program SQL Server na maszynach wirtualnych platformy Azure możesz może obejmować aplikacje, które działają częściowo w chmurze hello i częściowo lokalnie. Na przykład można rozszerzyć z sieci lokalnej i w chmurze toohello domeny usługi Active Directory za pośrednictwem [sieci wirtualnej Azure](../virtual-network/virtual-networks-overview.md). Ponadto można przechowywać lokalne pliki danych w usłudze Azure Storage przy użyciu [plików danych programu SQL Server na platformie Azure](http://msdn.microsoft.com/library/dn385720.aspx). Aby uzyskać więcej informacji, zobacz [tooSQL wprowadzenie chmura hybrydowa 2014 serwera](http://msdn.microsoft.com/library/dn606154.aspx). |
|  | Obsługuje [Replikacja transakcyjna programu SQL Server](https://msdn.microsoft.com/library/mt589530.aspx) jako dane tooreplicate subskrybenta. |W pełni obsługuje [Replikacja transakcyjna programu SQL Server](https://msdn.microsoft.com/library/mt589530.aspx), [zawsze włączonych grup dostępności](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md), usługi integracji i wysyłania dziennika tooreplicate danych. Ponadto w pełni obsługiwane są tradycyjne kopie zapasowe programu SQL Server. | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>Względy biznesowe przemawiające za wyborem usługi Azure SQL Database lub programu SQL Server na maszynach wirtualnych Azure
### <a name="cost"></a>Koszty
Czy jesteś uruchamiania, który jest start-up dla pieniężnych lub zespołu w firmowego, który działa w warunkach ścisłej budżecie, ograniczone fundusze jest często podstawowym czynnikiem hello podczas podejmowania decyzji o sposobie toohost baz danych. W tej sekcji opisano hello rozliczeń i licencjonowania podstawy na platformie Azure z zakresie toothese dwie opcje relacyjnej bazy danych: baza danych SQL i programu SQL Server na maszynach wirtualnych Azure. Również informacje o obliczanie hello całkowity koszt aplikacji.

#### <a name="billing-and-licensing-basics"></a>Podstawowe informacje dotyczące rozliczeń i licencjonowania
**Baza danych SQL** są sprzedanych toocustomers jako usługa, nie za pomocą licencji.  [Program SQL Server w usłudze Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) jest sprzedawany z dołączoną licencją płatną według stawki minutowej. Możesz również użyć istniejącej licencji, jeśli ją masz.  

Obecnie **bazy danych SQL** jest dostępna w kilku warstwach usług, z których wszystkie są rozliczane godzinowo według stałej stawki ustalanej oparte na powitania warstwę i poziom wydajności usługi możesz wybrać. Rozliczany jest również internetowy ruch wychodzący po zwykłych [stawkach transferu danych](https://azure.microsoft.com/pricing/details/data-transfers/). Witaj Basic, Standard i Premium i usługi Premium RS warstw są zaprojektowane toodeliver przewidywalną wydajność wielu toomatch poziomy wydajności aplikacji szczytowe wymagania. Można zmienić warstwy usług i toomatch poziomy wydajności, wymagane przez zróżnicowane przepływność aplikacji. Jeśli bazy danych ma wysoką transakcyjne toosupport woluminu i musi wielu użytkowników równocześnie, zalecamy warstwę Premium hello. Aby hello najnowsze informacje dotyczące bieżącego hello obsługiwane warstwy usług, zobacz [warstwach usług bazy danych SQL Azure](sql-database-service-tiers.md). Można również utworzyć [pule elastyczne](sql-database-elastic-pool.md) tooshare wydajności zasobów między wystąpień bazy danych.

Z **bazy danych SQL**, hello oprogramowanie bazy danych jest automatycznie skonfigurowane, poprawiono i uaktualniane przez firmę Microsoft, co obniża koszty administracyjne. Ponadto [wbudowana funkcja tworzenia kopii zapasowych](sql-database-automated-backups.md) pozwala osiągnąć znaczne oszczędności kosztów, zwłaszcza w przypadku dużej liczby baz danych.

Z **programu SQL Server na maszynach wirtualnych Azure**, można użyć dowolnego hello dostarczane przez platformę obrazów programu SQL Server (co obejmuje licencję) lub przenieść licencję programu SQL Server. Witaj wszystkie obsługiwane wersje programu SQL Server (2008 R2, 2012, 2014, 2016) i dostępne są wersje (Developer Express, sieci Web, Standard, Enterprise). Ponadto są dostępne wersje Bring Your-właścicielem-licencji (BYOL) hello obrazów. Korzystając z hello Azure dostępne obrazy, hello koszty operacyjne zależą hello rozmiar maszyny Wirtualnej i hello wydanie programu SQL Server możesz wybrać. Niezależnie od rozmiaru maszyny Wirtualnej lub wersji programu SQL Server należy zwrócić na minutę naliczana jest opłata licencyjna programu SQL Server i Windows Server oraz hello kosztu usługi Azure Storage dla dysków maszyny Wirtualnej hello. Opcja rozliczania co minutę Hello umożliwia toouse programu SQL Server tak długo jak bez kupowanie dodanie licencji programu SQL Server. W przypadku przeniesienia własne tooAzure licencji programu SQL Server, są naliczane systemu Windows Server i tylko kosztów magazynowania. Więcej informacji na temat przenoszenia własnej licencji można znaleźć w temacie [Przenośność licencji za pośrednictwem programu Software Assurance w systemie Azure](https://azure.microsoft.com/pricing/license-mobility/).

#### <a name="calculating-hello-total-application-cost"></a>Obliczanie hello całkowity koszt aplikacji
Podczas uruchamiania przy użyciu platformy w chmurze, hello koszt obsługi aplikacji obejmuje programowanie hello koszty administracyjne, a także koszty usługi platforma chmury publicznej hello.

Oto szczegółowe obliczenie kosztów obsługi aplikacji uruchomionej w usłudze SQL Database i programu SQL Server na maszynach wirtualnych Azure hello:

**W przypadku korzystania z usługi Azure SQL Database:**

*Całkowity koszt aplikacji = znacznie ograniczone koszty administracyjne + koszty rozwoju oprogramowania + koszty usługi SQL Database*

**W przypadku korzystania z programu SQL Server na maszynach wirtualnych platformy Azure:**

*Całkowity koszt aplikacji = ograniczone do minimum koszty tworzenia oprogramowania + koszty administracyjne + koszty licencjonowania programu SQL Server i systemu Windows Server + koszty usługi Azure Storage*

Aby uzyskać więcej informacji o cenach zobacz następujące zasoby hello:

* [Cennik usługi SQL Database](https://azure.microsoft.com/pricing/details/sql-database/)
* [Maszyny wirtualne — cennik](https://azure.microsoft.com/pricing/details/virtual-machines/) ([SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) i [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows))
* [Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> W programie SQL Server istnieje niewielki podzbiór funkcji, które nie są używane w usłudze SQL Database lub nie są w niej dostępne. Więcej informacji znajduje się w tematach [SQL Database Features](sql-database-features.md) (Funkcje usługi SQL Database) i [SQL Database Transact-SQL information](sql-database-transact-sql-information.md) (Informacje o programie Transact-SQL w usłudze SQL Database). Jeśli przenosisz istniejącej chmurze toohello rozwiązania programu SQL Server, zobacz [Migrowanie tooAzure bazy danych programu SQL Server, bazy danych SQL](sql-database-cloud-migrate.md). Podczas migracji istniejącej lokalnej programu SQL Server aplikacji tooSQL bazy danych, należy rozważyć aktualizowanie hello aplikacji tootake korzystać z funkcji hello, które oferują usługi w chmurze. Na przykład można rozważyć przy użyciu [Azure Web App Service](https://azure.microsoft.com/services/app-service/web/) lub [usługi w chmurze Azure](https://azure.microsoft.com/services/cloud-services/) toohost Twojego tooincrease warstwy aplikacji koszt korzyści.
> 
> 

### <a name="administration"></a>Administracja
Dla wielu firm usługa tooa tootransition hello decyzji w chmurze jest znacznie o przeniesieniu złożoności w zakresie administracji, ponieważ jest kosztów. Z **bazy danych SQL**, Microsoft zarządza hello podstawowy sprzęt. Microsoft automatycznie replikuje wszystkie dane tooprovide wysokiej dostępności, konfiguruje i uaktualnia oprogramowanie bazy danych hello zarządza równoważenia obciążenia i jest przezroczysty tryb failover w przypadku awarii serwera. Można kontynuować tooadminister bazy danych, ale nie są już potrzebne aparatu bazy danych hello toomanage, system operacyjny serwera lub sprzętu.  Przykładowe elementy nadal tooadminister uwzględnić baz danych i logowania, indeksu i dostrajania zapytania, inspekcji i zabezpieczeń.

Z **programu SQL Server na maszynach wirtualnych Azure**, mają pełną kontrolę nad hello systemu operacyjnego i konfiguracji wystąpienia programu SQL Server. Z maszyny Wirtualnej, jest tooyou toodecide podczas tooupdate/upgrade hello oprogramowania operacyjnego systemu i bazy danych i tooinstall żadnego dodatkowego oprogramowania, takie jak oprogramowanie antywirusowe. Niektóre funkcje automatycznych są dostarczane toodramatically uprościć stosowania poprawek, tworzenia kopii zapasowej i wysokiej dostępności. Ponadto można kontrolować rozmiar hello hello maszyny Wirtualnej, hello liczbę dysków oraz ich konfiguracje magazynu. Azure umożliwia toochange hello rozmiaru maszyny Wirtualnej zgodnie z potrzebami. Więcej informacji można znaleźć w temacie [Virtual Machine and Cloud Service Sizes for Azure](../virtual-machines/windows/sizes.md) (Rozmiary maszyn wirtualnych i usług w chmurze na platformie Azure). 

### <a name="service-level-agreement-sla"></a>Umowa dotycząca poziomu usług (SLA)
Dla wielu działów IT wypełnienie zobowiązań wynikających z umowy dotyczącej poziomu usług (SLA) ma najwyższy priorytet. W tej sekcji opisano umowy SLA stosuje opcji obsługi bazy danych tooeach.

W przypadku warstw usług Podstawowej, Standardowej, Premium i Premium RS usługi **SQL Database** firma Microsoft gwarantuje dostępność na poziomie 99,99%. Aby hello najnowsze informacje, zobacz [umową dotyczącą poziomu usług](https://azure.microsoft.com/support/legal/sla/sql-database/). Witaj najnowsze informacje dotyczące warstw usługi SQL Database i hello obsługiwanych planów ciągłości działalności biznesowej, zobacz [warstwy usług](sql-database-service-tiers.md).

Aby uzyskać **programu SQL Server uruchomionego na maszynach wirtualnych Azure**, Microsoft zapewnia dostępność na poziomie 99,95%, że obejmuje tylko hello maszyny wirtualnej. Umowa SLA nie obejmuje procesów hello (takich jak SQL Server) uruchomionych na powitania maszyny Wirtualnej i wymaga obsługi przynajmniej dwóch wystąpień maszyny Wirtualnej w zestawie dostępności. Dla hello najnowsze informacje znajdują się w temacie hello [umowy SLA dla maszyny Wirtualnej](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Baza danych wysokiej dostępności (HA) w maszynach wirtualnych, należy skonfigurować jedną z opcji wysokiej dostępności hello obsługiwane w programie SQL Server, takich jak [zawsze włączonych grup dostępności](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx). Przy użyciu opcji obsługiwanych wysokiej dostępności nie są dostępne dodatkowe umowy dotyczącej poziomu usług, ale pozwala tooachieve > dostępności 99,99% bazy danych.

### <a name="market"></a>Czas toomarket
**Baza danych SQL** jest hello odpowiednie rozwiązanie dla aplikacje zaprojektowane dla chmury, gdy wydajność deweloperów i szybkie czas na rynek są ważne. Z funkcjonalności przypominającej model DBA programowe jest doskonała dla architektów i deweloperów chmury ponieważ zmniejsza potrzebę hello Zarządzanie hello system operacyjny i bazy danych. Na przykład można użyć hello [interfejsu API REST](http://msdn.microsoft.com/library/azure/dn505719.aspx) i [poleceń cmdlet programu PowerShell](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate i zarządzanie nimi operacji administracyjnych dla tysięcy baz danych. Funkcje, takie jak [pule elastyczne](sql-database-elastic-pool.md) pozwalają toofocus na warstwie aplikacji hello i szybciej dostarczania rynku toohello Twojego rozwiązania.

**Program SQL Server uruchomiony na maszynach wirtualnych Azure** jest idealne, jeśli istniejące lub nowe aplikacje wymagają dużych baz danych, powiązanych baz danych, lub dostęp tooall funkcji programu SQL Server lub Windows. Możliwe jest również odpowiedni, jeśli chcesz istniejących toomigrate tooAzure aplikacji i baz danych jako lokalnymi — jest. Ponieważ nie trzeba toochange hello prezentacji, aplikacji i warstwach danych, zapiszesz czas i pieniądze oszczędzasz istniejącego rozwiązania. Zamiast tego możesz skoncentrować się na temat migracji tooAzure rozwiązań i przeprowadzeniu optymalizacji wydajności, które mogą być wymagane przez hello platformy Azure. Więcej informacje zawiera artykuł [Performance Best Practices for SQL Server on Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md) (Najlepsze praktyki dotyczące wydajności dla programu SQL Server w usłudze Azure Virtual Machines).

## <a name="summary"></a>Podsumowanie
W tym artykule omówiono usługę SQL Database i program SQL Server w usłudze Azure Virtual Machines oraz względy biznesowe, które mogą mieć wpływ na wybór jednego z tych rozwiązań. Witaj poniżej znajduje się podsumowanie sugestii tooconsider możesz:

Wybierz usługę **Azure SQL Database**, jeśli:

* Jesteś tworzenie nowych chmurowych aplikacji zapewniają tootake zaletą hello koszt wydajności i oszczędności optymalizacji usługi w chmurze. Takie podejście zapewnia korzyści hello usługi w chmurze w pełni zarządzana, pomaga w dolnym początkowy czas na rynek i zapewniają długoterminową optymalizację kosztów.
* Ma toohave Microsoft wykonywała zwyczajowe operacje zarządzania na bazach danych i wymaga dostępności silniejszych umowy SLA dla baz danych.

Wybierz rozwiązanie **SQL Server na maszynach wirtualnych Azure**, jeśli:

* Masz istniejące aplikacje lokalne mają toomigrate, lub rozszerzyć toohello chmury, lub jeśli użytkownik chce aplikacje przedsiębiorstwa toobuild większych niż 4 TB. Rozwiązanie zapewnia korzyści hello 100% SQL zgodności, pojemność dużej bazy danych, pełną kontrolę nad programu SQL Server i systemu Windows i bezpieczne lokalnych tunelowania tooon. To podejście minimalizuje koszty tworzenia i modyfikowania istniejących aplikacji.
* Masz istniejące zasoby IT i możesz ostatecznie samodzielnie zarządzać poprawkami, kopiami zapasowymi i wysoką dostępnością bazy danych. Należy zauważyć, że niektóre funkcje automatyczne umożliwiają znaczne uproszczenie tych operacji. 

## <a name="next-steps"></a>Następne kroki
* Zobacz [pierwszą bazę danych SQL Azure](sql-database-get-started-portal.md) tooget korzystania z bazy danych SQL.
* Zobacz [Cennik usługi SQL Database](https://azure.microsoft.com/pricing/details/sql-database/).
* Zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server na platformie Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md) tooget wprowadzenie do programu SQL Server na maszynach wirtualnych platformy Azure.

