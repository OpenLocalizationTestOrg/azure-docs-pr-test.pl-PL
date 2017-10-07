---
title: koszty aaaManage skutecznie dla programu SQL Server na maszynach wirtualnych Azure | Dokumentacja firmy Microsoft
description: "Zawiera najlepsze rozwiązania dotyczące wybierania hello prawo maszyny wirtualnej SQL Server model cenowy."
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Wskazówek dotyczących ceny dla maszyn wirtualnych Azure, programu SQL Server

Ten temat zawiera wskazówek dotyczących ceny dla maszyn wirtualnych programu SQL Server na platformie Azure. Dostępnych jest kilka opcji, które mają wpływ na koszty i jest ważne toopick hello prawego obrazu, który równoważy koszt z wymaganiami biznesowymi.

## <a name="free-licensed-sql-server-editions"></a>Zwolnij licencjonowane wersje programu SQL Server

Toodevelop należy przetestować, lub kompilacji Weryfikacja koncepcji, a następnie użyj hello wolne licencją **programu SQL Server Developer edition**. Ta wersja zawiera wszystko, co w programie SQL Server Enterprise edition, w związku z tym można używać go toobuild niezależnie od aplikacji ma. Po prostu nie można toorun w środowisku produkcyjnym. Maszyna wirtualna serwera SQL Server Developer tylko obciąży dla hello koszt hello maszyny Wirtualnej, nie licencjonowania programu SQL Server.

Jeśli chcesz, aby toorun lekkie obciążenia w środowisku produkcyjnym (< 4 rdzenie < 1 GB pamięci RAM, < 10 GB/bazy danych), następnie użyć hello wolne licencją **programu SQL Server Express edition**. Maszynę wirtualną SQL Express tylko obciąży dla hello koszt hello maszyny Wirtualnej, nie licencjonowania programu SQL.

Dla tych programowanie i testowanie obciążeń produkcyjnych lekkie można także zapisać pieniądze, wybierając mniejszego rozmiaru maszyny Wirtualnej, odpowiadający tych obciążeń. Witaj DS1v2 może być dobrym rozwiązaniem w przypadku tych obciążeń.

toocreate programu SQL Server 2016 Azure maszynę Wirtualną za pomocą jednego z tych obrazów, zobacz hello następującego łącza:

- [SQL Server 2016 Developer Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [SQL Server 2016 Express maszyna wirtualna platformy Azure](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Płatną wersjach programu SQL Server

Jeśli masz obciążeń produkcyjnych z systemem innym niż lightweight, użyj jednej z hello następujące wersje programu SQL Server:

| Wersja programu SQL Server | Obciążenie |
|-----|-----|
| Sieć Web | Mała witryn sieci web |
| Standardowa | Toomedium małych obciążeń |
| Enterprise | Obciążeń dużych lub krytycznym|

Masz dwie opcje toopay licencjonowania programu SQL Server dla następujących wersji: *płatności za użycie* lub *użycie własnej licencji*.

### <a name="pay-per-usage"></a>Należy zwrócić na użycie

**Płatniczych hello licencji programu SQL Server na użycie** oznacza, że hello na minutę koszt hello maszyny Wirtualnej Azure zawiera koszt hello hello licencji programu SQL Server. Witaj ceny hello różnych wersjach programu SQL Server (sieci Web, Standard i Enterprise) można zobaczyć w hello [maszyny Wirtualnej Azure cennikiem](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Witaj koszt jest hello takie same dla wszystkich wersji programu SQL Server (too2016 2008 R2). Jak ogólnie rzecz biorąc, licencjonowanie hello z programem SQL Server na minutę naliczana jest opłata licencyjna zależy od hello liczba rdzeni maszyny Wirtualnej.

Płatności hello programu SQL Server licencjonowania na użycie jest zalecane w przypadku:

- Tymczasowe lub okresowe obciążeń. Na przykład aplikacja, która wymaga toosupport zdarzenia z kilku miesięcy, co rok lub analizy biznesowe od poniedziałku.
- Obciążeń z istnienia nieznany lub skali. Na przykład aplikacja, co może nie być wymagane w ciągu kilku miesięcy lub co może wymagać więcej lub mniej moc obliczeniową, w zależności od zapotrzebowania.

toocreate programu SQL Server 2016 Azure maszynę Wirtualną za pomocą jednego z tych obrazów płatności za użycie Zobacz hello następującego łącza:

- [SQL Server 2016 sieci Web Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [SQL Server 2016 standardowa maszyna wirtualna platformy Azure](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Po utworzeniu maszyny wirtualnej programu SQL Server w portalu Azure hello hello szacowany miesięczny koszt wyświetlany na powitania **wybierz rozmiar** bloku nie obejmuje koszty licencjonowania programu SQL Server. Jest to koszt hello hello samej maszyny Wirtualnej.
>
> ![Wybierz bloku rozmiar maszyny Wirtualnej](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Hello wolne licencjonowanych Express i deweloperów wersji programu SQL Server jest to całkowita szacowany koszt hello. Ale dla sieci Web, Standard i Enterprise, Znajdź hello dodatkowych kosztów licencjonowania programu SQL na powitania [cennik maszyn wirtualnych Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Na stronie dotyczącej cen hello wybierz sieci docelowej wersji programu SQL Server.

### <a name="bring-your-own-license-byol"></a>Model dostarczania własnej licencji (BYOL)

**Przywracanie licencję programu SQL Server za pośrednictwem przenośność licencji**, nazywana także tooas **BYOL**, środków z Software Assurance w maszynie Wirtualnej platformy Azure przy użyciu istniejącego programu SQL Server z licencją zbiorczą. Maszyna wirtualna programu SQL Server przy użyciu BYOL tylko obciąży koszt hello uruchomionych hello maszyny Wirtualnej, nie licencjonowania programu SQL Server, biorąc pod uwagę, że ma już nabytych licencji i Software Assurance za pośrednictwem programu licencjonowania zbiorowego.

Dostarczają własne SQL licencjonowania za pośrednictwem przenośność licencji jest zalecane w przypadku:

- Ciągłe obciążeń. Na przykład aplikacja, która wymaga operacje biznesowe toosupport 24 x 7.
- Obciążeń przy użyciu znanych okres istnienia i skali. Na przykład aplikacji, które będzie wymagane hello cały rok i popytu zostały prognozowanych.

toouse BYOL z maszyną Wirtualną programu SQL Server musi mieć licencję na program SQL Server Standard lub Enterprise i [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), która jest wymagana przez niektóre [licencjonowania zbiorowego](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programy i opcjonalne zakup z innymi osobami.  Hello cennik poziomy realizowane za pośrednictwem programów licencjonowania zbiorczego zależy od typu hello umowy oraz hello ilość i lub zobowiązań tooSQL serwera. Ale jako zasadą, przywracanie własnej licencji w przypadku obciążeń produkcyjnych ciągłego ma hello następujące korzyści:

| BYOL korzyści | Opis |
|-----|-----|
| **Oszczędności** | Przywracanie licencję programu SQL Server jest tańsze niż płatności za użycie, jeśli Obciążenie Uruchamiaj stale SQL Server Standard lub Enterprise dla *więcej niż 10 miesięcy*. |
| **Długoterminowe oszczędności** | Na ogół jest *30% rocznie tańsze* toobuy lub odnowić licencji programu SQL Server hello pierwszy 3 lata. Ponadto po 3 lata, nie ma potrzeby toorenew hello licencji, po prostu płatności dla Software Assurance. W tym momencie jest *200% tańsze*. |
| **Bezpłatne pasywnym repliki pomocniczej** | Inną zaletą dostarczają własnej licencji jest hello [wolne Licencjonowanie jedna replika pomocnicza pasywnym](https://azure.microsoft.com/pricing/licensing-faq/) dla programu SQL Server na potrzeby wysokiej dostępności. Wytnij to w połowie hello licencjonowania koszt wdrożenia programu SQL Server o wysokiej dostępności (np. przy użyciu zawsze włączonych grup dostępności). pomocniczy pasywnym hello toorun prawa Hello są realizowane za pośrednictwem hello awaryjnej serwerów Software Assurance korzyści. |

toocreate SQL Server 2016 Azure maszynę Wirtualną za pomocą jednego z tych obrazów Przełącz your właścicielem licencji Zobacz hello maszyn wirtualnych i jest poprzedzony prefiksem "{BYOL}":

- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [SQL Server 2016 standardowa maszyna wirtualna platformy Azure](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Prosimy o kontakt w ciągu 10 dni liczbę licencji programu SQL Server będzie używany na platformie Azure. Witaj łącza toohello poprzedniego obrazy mają instrukcje na temat toodo to.

## <a name="avoid-unecessary-costs"></a>Uniknąć kosztów niepotrzebne

Jeśli korzystasz z dowolnych zadań, które nie są uruchamiane w sposób ciągły, należy wziąć pod uwagę zamykanie maszyny wirtualnej hello okresach nieaktywne hello. Płaci się wyłącznie za użyte zasoby.

Na przykład jeśli próbujesz po prostu limit programu SQL Server na maszynie Wirtualnej platformy Azure, nie byłaby wskazana opłat tooincur przypadkowo pozostawienie systemem tygodni. Jednym z nich jest toouse hello [funkcji automatycznego zamykania](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Autoshutdown maszyny Wirtualnej SQL](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

Automatyczne zamknięcie jest częścią większy zestaw podobne funkcje oferowane przez [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Dla innych przepływów pracy, należy wziąć pod uwagę automatycznie zamykanie i ponowne uruchamianie maszyn wirtualnych platformy Azure z rozwiązaniem do obsługi skryptów, takich jak [usługi Automatyzacja Azure](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> Zamykanie i cofanie przydziału maszyny Wirtualnej jest hello tylko sposób tooavoid opłat. Po prostu zatrzymanie lub przy użyciu tooshut Opcje zasilania w dół hello maszyny Wirtualnej nadal użycie zostaną naliczone opłaty powiązane.

## <a name="next-steps"></a>Następne kroki

Ogólne Azure cennik wskazówki, zobacz [uniknąć kosztów nieoczekiwany rozliczenia Azure i kosztów zarządzania](../../../billing/billing-getting-started.md).

Dla hello najnowsze maszyn wirtualnych o cenach, tym program SQL Server, zobacz hello [maszyny Wirtualnej Azure cennikiem](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Przejrzyj inne tematy maszyny wirtualnej programu SQL Server na [programu SQL Server na omówienia maszyn wirtualnych Azure](virtual-machines-windows-sql-server-iaas-overview.md).
