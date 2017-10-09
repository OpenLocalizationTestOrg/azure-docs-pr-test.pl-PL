---
title: aaaOverview programu SQL Server na maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sposobu toorun pełnej wersji programu SQL Server na maszynach wirtualnych Azure. Pobierz obrazów maszyn wirtualnych programu SQL Server tooall linki bezpośrednie i powiązanej zawartości."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Omówienie programu SQL Server w usłudze Azure Virtual Machines
W tym temacie opisano opcje uruchamiania programu SQL Server na maszynach wirtualnych platformy Azure (VM), wraz z [łączy obrazy tooportal](#option-1-create-a-sql-vm-with-per-minute-licensing) i omówienie [typowych zadań](#manage-your-sql-vm).

> [!NOTE]
> Jeśli znasz już program SQL Server, a jedynie chcesz toosee toodeploy maszyny Wirtualnej programu SQL Server, zobacz temat [Aprowizowanie maszyny wirtualnej programu SQL Server w portalu Azure hello](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## <a name="overview"></a>Omówienie
Jeśli jesteś administratorem bazy danych lub deweloperem, maszynach wirtualnych platformy Azure zapewniają toomove sposób użytkownika lokalnego programu SQL Server obciążeń i aplikacji toohello chmury. Hello poniższego klipu wideo zawiera omówienie techniczne maszynach wirtualnych Azure serwera SQL.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

Hello wideo omawia hello w następujących obszarach:

| Time | Obszar |
| --- | --- |
| 00:21 |Co to są maszyny wirtualne platformy Azure? |
| 01:45 |Bezpieczeństwo |
| 02:50 |Łączność |
| 03:30 |Wydajność i niezawodność magazynu |
| 05:20 |Rozmiary maszyn wirtualnych |
| 05:54 |Wysoka dostępność i umowy SLA |
| 07:30 |Pomoc techniczna w zakresie konfiguracji |
| 08:00 |Monitorowanie |
| 08:32 |Pokaz: tworzenie maszyny wirtualnej programu SQL Server 2016 |

> [!NOTE]
> Witaj wideo koncentruje się na SQL Server 2016, ale platforma Azure udostępnia obrazów maszyn wirtualnych dla wielu wersji programu SQL Server, w tym 2012, 2014 i 2016. 
> 
> 

## <a name="scenarios"></a>Scenariusze
Istnieje wiele przyczyn, które można wybrać toohost danych na platformie Azure. Jeśli aplikacja jest przenoszona tooAzure, poprawia wydajność tooalso przenoszenia hello danych. Są jednak także inne korzyści. Automatycznie uzyskujesz dostęp toomultiple centrach danych globalnych obecność i odzyskiwanie po awarii. dane Hello jest również wysoce zabezpieczonych i trwałe.

Program SQL Server uruchomiony na maszynach wirtualnych platformy Azure stanowi jedną z opcji przechowywania danych relacyjnych w systemie Azure. Dla kilku scenariuszy jest to właściwy wybór. Na przykład można hello tooconfigure maszyny Wirtualnej Azure podobnie jako możliwych tooan na lokalnej maszynie programu SQL Server. Można też toorun dodatkowe aplikacje i usługi na powitania tego samego serwera bazy danych. Istnieją dwa główne zasoby, które mogą pomóc w przemyśleniu większej liczby scenariuszy i zagadnień:

* [SQL Server na maszynach wirtualnych Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/) zawiera omówienie hello najważniejsze scenariusze dotyczące korzystania z programu SQL Server na maszynach wirtualnych platformy Azure. 
* Artykuł [Wybieranie opcji programu SQL Server w chmurze: usługa Azure SQL Database (PaaS) lub program SQL Server na maszynach wirtualnych Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md) zawiera szczegółowe porównanie usługi SQL Database oraz programu SQL Server uruchomionego na maszynie wirtualnej.

## <a name="create-a-new-sql-vm"></a>Tworzenie nowej maszyny wirtualnej SQL
Witaj poniższe sekcje zawierają toohello linki bezpośrednie portalu Azure dla obrazów Galeria maszyny wirtualnej programu SQL Server hello. W zależności od hello obraz można albo płatności dla koszty licencjonowania programu SQL Server na podstawie na minutę lub przenoszenia własnej licencji (BYOL).

Znajdź wskazówki krok po kroku dotyczące tworzenia nowej maszyny Wirtualnej SQL w samouczku hello [Aprowizowanie maszyny wirtualnej programu SQL Server w portalu Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Sprawdź również hello [wydajności najlepsze rozwiązania dotyczące maszyn wirtualnych programu SQL Server](virtual-machines-windows-sql-performance.md), co wyjaśnia, jak maszyny odpowiednie hello tooselect rozmiarze i inne funkcje są dostępne podczas inicjowania obsługi.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>Opcja 1. Tworzenie maszyny wirtualnej SQL z licencją płatną według stawki minutowej
Witaj Poniższa tabela zawiera macierz hello najnowsze obrazów programu SQL Server w galerii maszyn wirtualnych hello. Kliknij w dowolnym toobegin łącza tworzenia nowej maszyny Wirtualnej SQL z określonej wersji, wersji i systemu operacyjnego. 

> [!TIP]
> Witaj toounderstand maszyny Wirtualnej i SQL cenach dla tych obrazów, zobacz [cennik wskazówki dotyczące maszyn wirtualnych programu SQL Server Azure](virtual-machines-windows-sql-server-pricing-guidance.md).

| Wersja | System operacyjny | Wersja |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

Ponadto listy toothis, inne kombinacje wersji programu SQL Server i systemów operacyjnych są dostępne. Znajdź inne obrazy za pomocą wyszukiwania marketplace hello portalu Azure. 

## <a id="BYOL"></a>Opcja 2. Tworzenie maszyny wirtualnej SQL przy użyciu istniejącej licencji
Możesz również skorzystać z modelu dostarczania własnej licencji (Bring Your Own License, BYOL). W tym scenariuszu płacisz tylko za hello maszyny Wirtualnej bez żadnych dodatkowych kosztów licencjonowania programu SQL Server. toouse własnej licencji, użyj hello macierzy wersji programu SQL Server, wersji i systemów operacyjnych. W portalu hello te nazwy obrazów są poprzedzane prefiksem **{BYOL}**.

> [!TIP]
> Użycie własnej licencji może w dłuższym okresie przynieść oszczędności w przypadku ciągłych obciążeń produkcyjnych. Aby uzyskać więcej informacji, zobacz [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Wskazówki dotyczące cen maszyn wirtualnych platformy Azure z programem SQL Server).

| Wersja | System operacyjny | Wersja |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard BYOL](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Ponadto listy toothis, inne kombinacje wersji programu SQL Server i systemów operacyjnych są dostępne. Znajdź inne obrazy za pomocą wyszukiwania marketplace hello portalu Azure (Wyszukaj "SQL Server {BYOL}").

> [!IMPORTANT]
> obrazy BYOL wirtualna toouse, musisz mieć umowę Enterprise z [przenośność licencji za pośrednictwem programu Software Assurance na platformie Azure](https://azure.microsoft.com/pricing/license-mobility/). Należy również prawidłowej licencji dla hello wersji/wydania programu SQL Server ma toouse. Należy [Podaj hello niezbędne BYOL informacji tooMicrosoft](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) w **10** dni od aprowizacji maszyny Wirtualnej. 

> [!NOTE]
> Nie jest możliwe toochange hello licencjonowania własnej licencji modelu toouse maszyny Wirtualnej programu SQL Server płatności na minutę. W takim przypadku należy utworzyć nową maszynę Wirtualną BYOL i migracji toohello Twojej bazy danych nowej maszyny Wirtualnej. 

## <a name="manage-your-sql-vm"></a>Zarządzanie maszyną wirtualną z programem SQL
Po aprowizacji maszyny wirtualnej z programem SQL Server możesz wykonać kilka opcjonalnych zadań związanych z zarządzaniem. Pod wieloma względami możesz konfigurować program SQL Server i zarządzać nim dokładnie tak, jak w przypadku lokalnej instalacji programu SQL Server. Jednak niektóre zadania są określone tooAzure. Witaj poniższych sekcjach omówiono niektóre z tych obszarów i łączy toomore informacje.

### <a name="connect-toohello-vm"></a>Połącz toohello maszyny Wirtualnej
Jednym z najprostszych czynności administracyjne hello jest tooconnect tooyour maszyny Wirtualnej programu SQL Server za pomocą narzędzi, takich jak SQL Server Management Studio (SSMS). Aby uzyskać instrukcje dotyczące tooconnect tooyour nowy serwer SQL maszyny Wirtualnej, zobacz temat [połączyć tooa maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Migrowanie danych
Jeśli masz istniejącą bazę danych, należy toomove tego toohello nowo udostępnione maszyny Wirtualnej SQL. Aby uzyskać listę opcji migracji i wskazówki, zobacz [Migrowanie tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](virtual-machines-windows-migrate-sql.md).

### <a name="configure-high-availability"></a>Konfigurowanie wysokiej dostępności
Jeśli potrzebujesz wysokiej dostępności, rozważ skonfigurowanie grup dostępności programu SQL Server. Obejmuje to wiele maszyn wirtualnych Azure w sieci wirtualnej. Witaj portalu Azure ma szablon, który przeprowadzi konfigurację za Ciebie. Aby uzyskać więcej informacji, zobacz [Configure an AlwaysOn availability group in Azure Resource Manager virtual machines](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Konfigurowanie zawsze włączonej grupy dostępności na maszynach wirtualnych korzystających z usługi Azure Resource Manager). Jeśli toomanually należy skonfigurować grupę dostępności i skojarzony odbiornik, zobacz [Konfigurowanie zawsze włączonych grup dostępności w maszynie Wirtualnej platformy Azure](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Inne zagadnienia dotyczące wysokiej dostępności można znaleźć w temacie [High Availability and Disaster Recovery for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md) (Wysoka dostępność i odzyskiwanie po awarii dla programu SQL Server w usłudze Azure Virtual Machines).

### <a name="back-up-your-data"></a>Tworzenie kopii zapasowej danych
Maszyny wirtualne platformy Azure mogą wykorzystać [automatyczna usługa Backup](virtual-machines-windows-sql-automated-backup.md), który regularnie tworzy kopie zapasowe bazy danych magazynu tooblob. Tej techniki można również używać ręcznie. Aby uzyskać więcej informacji, zobacz [Use Azure Storage for SQL Server Backup and Restore](virtual-machines-windows-use-storage-sql-server-backup-restore.md) (Używanie usługi Azure Storage do tworzenia kopii zapasowych programu SQL Server i ich przywracania). Omówienie wszystkich opcji tworzenia i przywracania kopii zapasowych znajduje się w temacie [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md) (Tworzenie i przywracanie kopii zapasowych programu SQL Server w usłudze Azure Virtual Machines).

### <a name="automate-updates"></a>Automatyzowanie aktualizacji
Maszyny wirtualne platformy Azure można używać [automatyczne stosowanie poprawek](virtual-machines-windows-sql-automated-patching.md) tooschedule automatycznie aktualizuje okno obsługi instalacji ważne systemu windows i program SQL Server.

### <a name="customer-experience-improvement-program-ceip"></a>Program poprawy jakości obsługi klienta
Witaj Program poprawy jakości obsługi klienta (CEIP) jest domyślnie włączona. Tym okresowo wysyła raporty tooMicrosoft toohelp poprawy programu SQL Server. Nie zadania zarządzania wymagane z programu CEIP, chyba że chcesz toodisable go po zainicjowaniu obsługi administracyjnej. Można dostosować lub wyłączyć hello CEIP łącząc toohello maszyny Wirtualnej przy użyciu pulpitu zdalnego. Następnie uruchom hello **programu SQL Server Error and Usage Reporting** narzędzia. Postępuj zgodnie z hello instrukcje toodisable raportowania. 

Aby uzyskać więcej informacji, zobacz hello CEIP części hello [zaakceptuj postanowienia licencyjne](https://msdn.microsoft.com/library/ms143343.aspx) tematu. 

## <a name="next-steps"></a>Następne kroki

Odpowiedzi na pytania o cenach, zobacz [cennik wskazówki dotyczące maszyn wirtualnych programu SQL Server Azure](virtual-machines-windows-sql-server-pricing-guidance.md) i hello [Azure cennikiem](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Wybierz sieci docelowej wersji programu SQL Server w hello **systemu operacyjnego/oprogramowania** listy. Następnie wyświetlić cen hello inaczej rozmiarze maszyn wirtualnych.

Masz więcej pytań? Najpierw Zobacz hello [programu SQL Server na maszynach wirtualnych Azure — często zadawane pytania](virtual-machines-windows-sql-server-iaas-faq.md). Ale także dodać Twoje pytania lub komentarze toohello dołu żadnych toointeract tematy maszyny Wirtualnej SQL z firmy Microsoft i hello społeczności.
