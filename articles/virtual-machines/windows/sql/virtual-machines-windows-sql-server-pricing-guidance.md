---
title: "Efektywne zarządzanie kosztami dla programu SQL Server na maszynach wirtualnych Azure | Dokumentacja firmy Microsoft"
description: "Zawiera najlepsze rozwiązania dotyczące wybierania model cenowy prawo maszyny wirtualnej programu SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 10/17/2017
ms.author: jroth
ms.openlocfilehash: fa1611944d266001a54c4d78205c942a5226d97b
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Wskazówek dotyczących ceny dla maszyn wirtualnych Azure, programu SQL Server

Ten artykuł zawiera wskazówek dotyczących ceny dla maszyn wirtualnych programu SQL Server na platformie Azure. Dostępnych jest kilka opcji, które mają wpływ na koszty i ważne jest, aby wybrać prawego obrazu, który równoważy koszt z wymaganiami biznesowymi.

## <a name="free-licensed-sql-server-editions"></a>Zwolnij licencjonowane wersje programu SQL Server

Testowanie, lub kompilacji Weryfikacja koncepcji, następnie należy użyć wolne licencją **programu SQL Server Developer edition**. Ta wersja zawiera wszystko, co w programie SQL Server Enterprise edition, w związku z tym go używać do tworzenia aplikacji, niezależnie od ma. Tylko nie mogą być uruchamiane w środowisku produkcyjnym. Maszyna wirtualna programu SQL Server Developer tylko opłaty kosztów maszyny Wirtualnej, a nie dla licencjonowania programu SQL Server.

Jeśli chcesz uruchomić lekkie obciążenia w środowisku produkcyjnym (< 4 rdzenie < 1 GB pamięci RAM, < 10 GB/bazy danych), następnie użyć wolne licencją **programu SQL Server Express edition**. Maszynę wirtualną SQL Express jedynie opłatami za kosztów maszyny Wirtualnej, nie licencjonowania programu SQL.

Dla tych programowanie i testowanie obciążeń produkcyjnych lekkie można także zapisać pieniądze, wybierając mniejszego rozmiaru maszyny Wirtualnej, odpowiadający tych obciążeń. DS1v2 może być dobrym rozwiązaniem w przypadku tych obciążeń.

Aby utworzyć Maszynę wirtualną Azure 2017 serwera SQL z jednym z tych obrazów, zobacz następujące linki:

| Platforma | Za darmo licencjonowane obrazów |
|---|---|
| Windows Server 2016 | [SQL Server 2017 Developer Azure VM](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017DeveloperonWindowsServer2016)<br/>[SQL Server 2017 Express maszyna wirtualna platformy Azure](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017ExpressonWindowsServer2016) |
| Red Hat Enterprise Linux | [SQL Server 2017 Developer Azure VM](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017DeveloperonRedHatEnterpriseLinux74)<br/>[SQL Server 2017 Express maszyna wirtualna platformy Azure](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017ExpressonRedHatEnterpriseLinux74) |
| SUSE Linux Enterprise Server | [SQL Server 2017 Developer Azure VM](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017DeveloperonSLES12SP2)<br/>[SQL Server 2017 Express maszyna wirtualna platformy Azure](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017ExpressonSLES12SP2) |
| Ubuntu | [SQL Server 2017 Developer Azure VM](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017DeveloperonUbuntuServer1604LTS)<br/>[SQL Server 2017 Express maszyna wirtualna platformy Azure](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017ExpressonUbuntuServer1604LTS) |

## <a name="paid-sql-server-editions"></a>Płatną wersjach programu SQL Server

Jeśli obciążenie z systemem innym niż lightweight produkcji, użyj jednej z następujących wersji programu SQL Server:

| Wersja programu SQL Server | Obciążenie |
|-----|-----|
| Sieć Web | Mała witryn sieci web |
| Standardowa | Mała liczba godzin w przypadku obciążeń średnia |
| Enterprise | Obciążeń dużych lub krytycznym|

Dostępne są dwie opcje w celu opłacenia licencjonowania programu SQL Server dla następujących wersji: *płatności za użycie* lub *użycie własnej licencji (BYOL)*.

### <a name="pay-per-usage"></a>Należy zwrócić na użycie

**Płatności licencji programu SQL Server na użycie** oznacza, że koszt na minutę maszyny Wirtualnej Azure zawiera koszt licencji programu SQL Server. Cennik o różnych wersjach programu SQL Server (sieci Web, Standard i Enterprise) można zobaczyć w [maszyny Wirtualnej Azure cennikiem](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Koszt jest taka sama dla wszystkich wersji programu SQL Server (2012 z dodatkiem SP3 2017). Podobnie jak w przypadku licencjonowania programu SQL Server ogólnie rzecz biorąc, kosztów licencjonowania na minutę zależy od liczby rdzeni maszyny Wirtualnej.

Płatności programu SQL Server licencjonowania na użycie jest zalecane w przypadku:

- Tymczasowe lub okresowe obciążeń. Na przykład aplikacja, która musi obsługiwać zdarzenia z kilku miesięcy, co rok lub analizy biznesowej od poniedziałku.
- Obciążeń z istnienia nieznany lub skali. Na przykład aplikacja, co może nie być wymagane w ciągu kilku miesięcy lub co może wymagać więcej lub mniej moc obliczeniową, w zależności od zapotrzebowania.

Aby utworzyć Maszynę wirtualną Azure 2017 serwera SQL z jednym z tych obrazów płatności za użycie, zobacz następujące linki:

| Platforma | Licencjonowane obrazów |
|---|---|
| Windows Server 2016 | [SQL Server 2017 sieci Web Azure VM](https://portal.azure.com/#create/Microsoft.SQLServer2017WebonWindowsServer2016)<br/>[SQL Server 2017 standardowa maszyna wirtualna platformy Azure](https://portal.azure.com/#create/Microsoft.SQLServer2017StandardonWindowsServer2016)<br/>[SQL Server 2017 Enterprise Azure VM](https://portal.azure.com/#create/Microsoft.SQLServer2017EnterpriseWindowsServer2016) |
| Red Hat Enterprise Linux | [SQL Server 2017 sieci Web Azure VM](https://portal.azure.com/#create/Microsoft.SQLServer2017WebonRedHatEnterpriseLinux74)<br/>[SQL Server 2017 standardowa maszyna wirtualna platformy Azure](https://portal.azure.com/#create/Microsoft.SQLServer2017StandardonRedHatEnterpriseLinux74)<br/>[SQL Server 2017 Enterprise Azure VM](https://portal.azure.com/#create/Microsoft.SQLServer2017EnterpriseonRedHatEnterpriseLinux74) |
| SUSE Linux Enterprise Server | [SQL Server 2017 sieci Web Azure VM](https://portal.azure.com/#create/Microsoft.SQLServer2017WebonSLES12SP2)<br/>[SQL Server 2017 standardowa maszyna wirtualna platformy Azure](https://portal.azure.com/#create/Microsoft.SQLServer2017StandardonSLES12SP2)<br/>[SQL Server 2017 Enterprise Azure VM](https://portal.azure.com/#create/Microsoft.SQLServer2017EnterpriseonSLES12SP2) |
| Ubuntu | [SQL Server 2017 sieci Web Azure VM](https://portal.azure.com/#create/Microsoft.SQLServer2017WebonUbuntuServer1604LTS)<br/>[SQL Server 2017 standardowa maszyna wirtualna platformy Azure](https://portal.azure.com/#create/Microsoft.SQLServer2017StandardonUbuntuServer1604LTS)<br/>[SQL Server 2017 Enterprise Azure VM](https://portal.azure.com/#create/Microsoft.SQLServer2017EnterpriseonUbuntuServer1604LTS) |

> [!IMPORTANT]
> Podczas tworzenia maszyny wirtualnej programu SQL Server w portalu, **wybierz rozmiar** okna pokazuje szacowany koszt. Należy pamiętać, że ta szacowana tylko kosztów obliczeń do uruchamiania maszyny Wirtualnej wraz z oknami koszty licencjonowania dla maszyn wirtualnych systemu Windows. Nie ma dodatkowych licencjonowania koszty sieci Web, wersje Standard i Enterprise programu SQL Server. On również nie ma żadnych dodatkowych kosztów licencjonowania dla systemów operacyjnych Linux innych firm dla maszyn wirtualnych systemu Linux. Aby uzyskać najbardziej dokładnego oszacowania cenową, wybierz system operacyjny i wersji programu SQL Server na stronie dotyczącej cen [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) i [Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).
>
> ![Wybierz bloku rozmiar maszyny Wirtualnej](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)

### <a name="bring-your-own-license-byol"></a>Model dostarczania własnej licencji (BYOL)

**Przywracanie licencję programu SQL Server za pośrednictwem przenośność licencji**, nazywany również **BYOL**, środków z Software Assurance w maszynie Wirtualnej platformy Azure przy użyciu istniejącego programu SQL Server z licencją zbiorczą. Maszyna wirtualna SQL Server przy użyciu BYOL opłat tylko kosztów uruchamiania maszyny Wirtualnej, a nie dla licencjonowania programu SQL Server, biorąc pod uwagę, że ma już nabytych licencji i Software Assurance za pośrednictwem programu licencjonowania zbiorowego.

> [!NOTE]
> Obrazy BYOL są obecnie dostępne tylko dla maszyn wirtualnych systemu Windows. Można jednak ręcznie zainstalować program SQL Server na maszynie Wirtualnej systemu Linux — tylko do. Zapoznaj się z instrukcjami w [Linux SQL maszyny Wirtualnej — często zadawane pytania](../../linux/sql/sql-server-linux-faq.md).

Dostarczają własne SQL licencjonowania za pośrednictwem przenośność licencji jest zalecane w przypadku:

- Ciągłe obciążeń. Na przykład aplikacja, która musi obsługiwać operacje biznesowe 24 x 7.
- Obciążeń przy użyciu znanych okres istnienia i skali. Na przykład aplikację, która jest wymagana dla całego roku i popytu zostały prognozowanych.

Aby używać BYOL z maszyny Wirtualnej programu SQL Server, musi mieć licencję na program SQL Server Standard lub Enterprise i [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), która jest wymagana przez niektóre [licencjonowania zbiorowego](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programy i opcjonalne zakup z innymi osobami.  Poziom cenową realizowane za pośrednictwem programów licencjonowania zbiorczego zależy od typu umowy oraz ilość i lub zobowiązań do programu SQL Server. Jednak jako zasadą, przywracanie własnej licencji w przypadku obciążeń produkcyjnych ciągłego ma następujące zalety:

| BYOL korzyści | Opis |
|-----|-----|
| **Oszczędności** | Przywracanie licencję programu SQL Server jest tańsze niż płatności za użycie, jeśli obciążenie działa w sposób ciągły SQL Server Standard lub Enterprise dla *więcej niż 10 miesięcy*. |
| **Długoterminowe oszczędności** | Na ogół jest *30% rocznie tańsze* lub odnowić licencji programu SQL Server przez pierwsze 3 lata. Ponadto po 3 lata, nie trzeba już odnowić licencji, po prostu opłacać Software Assurance. W tym momencie jest *200% tańsze*. |
| **Bezpłatne pasywnym repliki pomocniczej** | Inną zaletą dostarczają własnej licencji jest [wolne Licencjonowanie jedna replika pomocnicza pasywnym](https://azure.microsoft.com/pricing/licensing-faq/) dla programu SQL Server na potrzeby wysokiej dostępności. Wytnij to w połowie licencjonowania koszt wdrożenia programu SQL Server o wysokiej dostępności (na przykład przy użyciu zawsze włączonych grup dostępności). Prawa do uruchamiania pomocniczej pasywnym są udostępniane za pośrednictwem korzyści awaryjnej serwerów Software Assurance. |

Aby utworzyć maszyny Wirtualnej Azure SQL Server 2016 z jednym z tych obrazów Przełącz your właścicielem licencji, zobacz maszyn wirtualnych i jest poprzedzony prefiksem "{BYOL}":

- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [SQL Server 2016 standardowa maszyna wirtualna platformy Azure](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!IMPORTANT]
> Trafić w ciągu 10 dni liczbę licencji programu SQL Server będzie używany na platformie Azure. Łącza do poprzedniego obrazy mają instrukcje jak to zrobić.

> [!NOTE]
> Nie można zmienić modelu licencjonowania maszyny wirtualnej z programem SQL Server opłacanej za minuty użycia na własną licencję. W takim przypadku należy utworzyć nową maszynę wirtualną w modelu BYOL i zmigrować bazy danych do tej nowej maszyny wirtualnej. 

## <a name="avoid-unnecessary-costs"></a>Unikaj niepotrzebnych kosztów

Aby uniknąć niepotrzebnych kosztów, wybierz rozmiar maszyny wirtualnej optymalne i rozważ sporadyczne zamknięcia nieciągły obciążeń.

### <a id="machinesize"></a>Poprawnie rozmiaru maszyny Wirtualnej

Liczba rdzeni bezpośrednio dotyczy koszty licencjonowania programu SQL Server. Wybierz rozmiar maszyny Wirtualnej, który odpowiada Twoim potrzebom oczekiwany dla Procesora, pamięci, magazynu i przepustowości we/wy. Aby uzyskać pełną listę opcji rozmiaru maszyny, zobacz [rozmiarów maszyn wirtualnych systemu Windows](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) i [rozmiarów maszyn wirtualnych systemu Linux](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Istnieją nowe rozmiary maszyny, które działają prawidłowo w przypadku niektórych typów obciążeń programu SQL Server. Rozmiary maszyn Obsługa wysokiego poziomu pamięci, magazynu i przepustowości we/wy, ale mają niższe liczby rdzeni zwirtualizowanych. Rozważmy na przykład następująco:

| Rozmiar maszyny wirtualnej | Vcpu | Memory (Pamięć) | Maksymalna liczba dysków | Maksymalna przepustowość we/wy | Koszty licencjonowania programu SQL | Łączne koszty (obliczeń + licencjonowania) |
|---|---|---|---|---|---|---|
| **Standard_DS14v2** | 16 | 112 GB | 32 | 51,200 IOPS lub 768 MB/s | | |
| **Standard_DS14 4v2** | 4 | 112 GB | 32 | 51,200 IOPS lub 768 MB/s | 75% niższa | 57% niższa |

> [!IMPORTANT]
> To jest przykład punktu w czasie. Najnowsze specyfikacji, można znaleźć maszyny artykuły rozmiary i Azure cennikiem dla [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) i [Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

W poprzednim przykładzie, można stwierdzić, że specyfikacje **Standard_DS14v2** i **Standard_DS14 4v2** są identyczne z wyjątkiem Vcpu. Sufiks **-4v2** na końcu **Standard_DS14 4v2** rozmiaru maszyny wskazuje liczbę aktywnych Vcpu. Ponieważ koszty licencjonowania programu SQL Server są powiązane z liczby rdzeni, to znacznie ograniczyć koszty maszyny Wirtualnej w scenariuszach, w którym nie są wymagane dodatkowe Vcpu. Jest to przykład i istnieje wiele rozmiarów maszyn z ograniczeniami Vcpu, które są oznaczone symbolem tego wzorca sufiks. Aby uzyskać więcej informacji, zobacz w blogu [o nowe rozmiary maszyny Wirtualnej Azure więcej pracy ekonomicznego bazy danych](https://azure.microsoft.com/blog/announcing-new-azure-vm-sizes-for-more-cost-effective-database-workloads/).

### <a name="shut-down-your-vm-when-possible"></a>Zamknij maszyny Wirtualnej, jeśli to możliwe

Jeśli korzystasz z dowolnych zadań, które nie są uruchamiane w sposób ciągły, należy wziąć pod uwagę zamykanie maszyny wirtualnej w okresach nieaktywne. Płaci się wyłącznie za użyte zasoby.

Na przykład jeśli próbujesz po prostu limit programu SQL Server na maszynie Wirtualnej platformy Azure, czy chcesz naliczenie opłat przypadkowo pozostawienie systemem tygodni. Jeden rozwiązaniem jest użycie [funkcji automatycznego zamykania](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Autoshutdown maszyny Wirtualnej SQL](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

Automatyczne zamknięcie jest częścią większy zestaw podobne funkcje oferowane przez [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Dla innych przepływów pracy, należy wziąć pod uwagę automatycznie zamykanie i ponowne uruchamianie maszyn wirtualnych platformy Azure z rozwiązaniem do obsługi skryptów, takich jak [usługi Automatyzacja Azure](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> Zamykanie i cofanie przydziału maszyny Wirtualnej jest jedynym sposobem uniknięcia naliczania opłat. Po prostu zatrzymanie lub zamykania maszyny Wirtualnej za pomocą apletu Opcje zasilania nadal użycie zostaną naliczone opłaty powiązane.

## <a name="next-steps"></a>Następne kroki

Ogólne Azure cennik wskazówki, zobacz [uniknąć kosztów nieoczekiwany rozliczenia Azure i kosztów zarządzania](../../../billing/billing-getting-started.md).

Dla maszyn wirtualnych najnowsze cennika, w tym program SQL Server, zobacz [maszyny Wirtualnej Azure cennikiem](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Dowiedz się więcej o maszynach wirtualnych programu SQL Server dla obu [maszyn wirtualnych systemu Windows Server SQL](virtual-machines-windows-sql-server-iaas-overview.md) i [maszyn wirtualnych systemu Linux serwera SQL](../../linux/sql/sql-server-linux-virtual-machines-overview.md).
