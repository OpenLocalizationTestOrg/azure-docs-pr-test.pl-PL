---
title: aaaMigrate tooSQL bazy danych serwera SQL Server na maszynie Wirtualnej | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sposobu toomigrate użytkownika lokalnego bazy danych tooSQL serwera w maszynie wirtualnej platformy Azure."
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>Migrowanie tooSQL bazy danych serwera SQL Server w maszynie Wirtualnej platformy Azure

Istnieje kilka metod toomigrate tooSQL bazy danych użytkowników programu SQL Server lokalnego serwera w maszynie Wirtualnej platformy Azure. W tym artykule krótko będzie omówienia różnych metod i zaleca hello najlepszej metody dla różnych scenariuszy.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Jakie są metody głównej migracji hello?
dostępne są następujące metody głównej migracji Hello:

* Wykonaj kopię zapasową lokalnych przy użyciu kompresji i ręcznie Kopiuj plik kopii zapasowej hello na powitania maszyny wirtualnej platformy Azure
* Wykonywania tooURL kopii zapasowej i przywracania do maszyny wirtualnej platformy Azure z adresu URL hello hello
* Odłączyć, a następnie skopiuj hello danych i dziennika pliki tooAzure magazynu obiektów blob i następnie dołącz tooSQL serwera w maszynie Wirtualnej platformy Azure z adresu URL
* Konwertowanie fizycznej lokalnego komputera wirtualnego dysku twardego tooHyper-V, Przekaż tooAzure magazynu obiektów Blob, a następnie wdrożenie jako nowej maszyny Wirtualnej za pomocą przekazać wirtualnego dysku twardego
* Wyślij dysk twardy za pomocą usługi Import/Eksport systemu Windows
* Jeśli masz wdrożenie AlwaysOn lokalnie, należy użyć hello [Kreatora dodawania repliki Azure](../classic/sql-onprem-availability.md) toocreate repliki w Azure, a następnie trybu failover, wskazując wystąpienie bazy danych platformy Azure toohello użytkowników
* Użyj programu SQL Server [replikacji transakcyjnej](https://msdn.microsoft.com/library/ms151176.aspx) wystąpienia jako subskrybent tooconfigure hello Azure SQL Server, a następnie wyłącz replikacji wskazujące wystąpienie bazy danych platformy Azure toohello użytkowników

> [!TIP]
> Umożliwia także tych samym techniki toomove baz danych między maszynami wirtualnymi serwera SQL na platformie Azure. Na przykład jest nie tooupgrade sposób obsługiwane galerii obrazu maszyny Wirtualnej programu SQL Server z jednego tooanother wersji/wydania. W takim przypadku należy utworzyć nową maszynę Wirtualną programu SQL Server z hello nowej wersji/wydania i następnie użyj jednej z metod migracji hello w tym artykule toomove baz danych. 

## <a name="choosing-your-migration-method"></a>Wybieranie metody migracji
Dla danych optymalną wydajność transferu migracja hello pliki bazy danych do hello Azure maszyny Wirtualnej przy użyciu skompresowany plik kopii zapasowej.

toominimize czas przestoju w trakcie procesu migracji bazy danych hello, użyć opcji zawsze włączone hello lub hello opcji replikacji transakcyjnej.

Jeśli nie jest możliwe toouse hello powyżej metod, ręcznej migracji bazy danych. Za pomocą tej metody, będzie zwykle zaczyna się od kopii zapasowej bazy danych, a następnie kopii zapasowej bazy danych hello na platformie Azure i następnie wykonaj operację przywracania bazy danych. Można również skopiować pliki bazy danych hello, samodzielnie na platformie Azure, a następnie dołącz je. Istnieje kilka metod, które można wykonać ten ręczny proces migracji bazy danych do maszyny Wirtualnej platformy Azure.

> [!NOTE]
> Po uaktualnieniu tooSQL Server 2014 lub SQL Server 2016 ze starszych wersji programu SQL Server, należy rozważyć, czy zmiany są potrzebne. Zaleca się zajęcie się wszystkie zależności w funkcji nie są obsługiwane przez hello nowej wersji programu SQL Server w ramach migracji projektu. Aby uzyskać więcej informacji na powitania obsługiwane wersje i scenariuszy, zobacz [uaktualnienia tooSQL serwera](https://msdn.microsoft.com/library/bb677622.aspx).

Hello w poniższej tabeli wymieniono każdej z metod migracji głównej hello i omówiono, gdy użycie hello każdej metody jest najbardziej odpowiednia.

| Metoda | Wersja bazy danych źródła | Docelowej wersji bazy danych | Ograniczenia rozmiaru kopii zapasowej bazy danych źródła | Uwagi |
| --- | --- | --- | --- | --- |
| [Wykonaj kopię zapasową lokalnych przy użyciu kompresji i ręcznie Kopiuj plik kopii zapasowej hello na powitania maszyny wirtualnej platformy Azure](#backup-and-restore) |SQL Server 2005 lub nowszy |SQL Server 2005 lub nowszy |[Limit magazynu maszyny Wirtualnej platformy Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Jest to bardzo proste i dobrze przetestowane technika przenoszenia baz danych na komputerach. |
| [Wykonywania tooURL kopii zapasowej i przywracania do maszyny wirtualnej platformy Azure z adresu URL hello hello](#backup-to-url-and-restore) |SQL Server 2012 z dodatkiem SP1 CU2 lub nowszej |SQL Server 2012 z dodatkiem SP1 CU2 lub nowszej |< 12,8 TB dla programu SQL Server 2016, w przeciwnym razie < 1 TB | Ta metoda jest po prostu inną sposób toomove hello pliku kopii zapasowej toohello maszyny Wirtualnej za pomocą usługi Azure storage. |
| [Odłączyć, a następnie skopiuj hello danych i dziennika pliki tooAzure magazynu obiektów blob i następnie dołącz tooSQL serwera na maszynie wirtualnej platformy Azure z adresu URL](#detach-and-attach-from-url) |SQL Server 2005 lub nowszy |SQL Server 2014 lub nowszy |[Limit magazynu maszyny Wirtualnej platformy Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Ta metoda ma zbyt[przechowywania tych plików przy użyciu usługi magazynu obiektów Blob platformy Azure hello](https://msdn.microsoft.com/library/dn385720.aspx) i dołącz je tooSQL serwera w maszynie Wirtualnej platformy Azure, szczególnie w przypadku bardzo dużych baz danych |
| [Konwertuj na lokalne maszyny wirtualne dyski twarde tooHyper-V, Przekaż tooAzure magazynu obiektów Blob, a następnie wdrożyć maszynę wirtualną przy użyciu przekazywanego wirtualnego dysku twardego](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 lub nowszy |SQL Server 2005 lub nowszy |[Limit magazynu maszyny Wirtualnej platformy Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Używany, gdy [dostarczają licencję programu SQL Server](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), podczas migracji bazy danych, które zostanie uruchomione na starszej wersji programu SQL Server lub podczas migrowania systemu i baz danych użytkowników jednocześnie w ramach migracji bazy danych jest zależny od innych hello bazy danych użytkownika i/lub systemowych bazach danych. |
| [Wyślij dysk twardy za pomocą usługi Import/Eksport systemu Windows](#ship-hard-drive) |SQL Server 2005 lub nowszy |SQL Server 2005 lub nowszy |[Limit magazynu maszyny Wirtualnej platformy Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Użyj hello [usługi Import/Eksport Windows](../../../storage/common/storage-import-export-service.md) gdy Metoda ręcznego kopiowania jest zbyt wolno, takie jak w przypadku bardzo dużych baz danych |
| [Użyj hello Kreatora dodawania repliki Azure](../classic/sql-onprem-availability.md) |SQL Server 2012 lub nowszy |SQL Server 2012 lub nowszy |[Limit magazynu maszyny Wirtualnej platformy Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Minimalizuje przestojów, używania wdrożenie lokalnymi (AlwaysOn) |
| [Użyj Replikacja transakcyjna programu SQL Server](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 lub nowszy |SQL Server 2005 lub nowszy |[Limit magazynu maszyny Wirtualnej platformy Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Opcja używana podczas należy przestoju toominimize i nie ma lokalnego wdrożenia (AlwaysOn) |

## <a name="backup-and-restore"></a>Tworzenie kopii zapasowej i przywracanie
Utwórz kopię zapasową bazy danych za pomocą kompresji skopiuj hello toohello kopii zapasowej maszyny Wirtualnej, a następnie przywróć hello bazy danych. Jeśli w pliku kopii zapasowej jest większy niż 1 TB, musi paskowych ponieważ hello maksymalny rozmiar dysku maszyny Wirtualnej wynosi 1 TB. Użyj hello następujące ogólne kroki toomigrate bazy danych użytkownika za pomocą tej metody ręczne:

1. Wykonaj lokalizacji lokalnej kopii zapasowej tooan pełnej bazy danych.
2. Utwórz lub Przekaż hello wersji programu SQL Server na potrzeby maszyny wirtualnej.
3. Konfiguracja połączenia, w zależności od wymagań. Zobacz [połączyć tooa maszyny wirtualnej programu SQL Server na platformie Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).
4. Skopiuj tooyour Twoje pliki kopii zapasowej maszyny Wirtualnej za pomocą zdalnego pulpitu, Eksploratora Windows i hello polecenia kopiowania w wierszu polecenia.

## <a name="backup-toourl-and-restore"></a>TooURL kopii zapasowej i przywracania
Zamiast tworzenia kopii zapasowej pliku lokalnego tooa, możesz użyć hello [tooURL kopii zapasowej](https://msdn.microsoft.com/library/dn435916.aspx) , a następnie Przywróć z adresu URL toohello maszyny Wirtualnej. Z programem SQL Server 2016 rozłożone zestawy kopii zapasowych są obsługiwane, są zalecane w przypadku wydajności i wymagane limity rozmiaru hello tooexceed dla obiekt blob. W przypadku bardzo dużych baz danych hello Użyj hello [usługi Import/Eksport Windows](../../../storage/common/storage-import-export-service.md) jest zalecane.

## <a name="detach-and-attach-from-url"></a>Odłącz i Dołącz z adresu URL
Odłącz plików dziennika i bazy danych, a następnie przesyła je za[magazynu obiektów Blob Azure](https://msdn.microsoft.com/library/dn385720.aspx). Następnie dołącz hello bazy danych z adresu URL hello na maszynie Wirtualnej platformy Azure. Użyj, jeśli chcesz hello fizyczna baza danych plików tooreside w magazynie obiektów Blob. Może to być przydatne w przypadku bardzo dużych baz danych. Użyj hello następujące ogólne kroki toomigrate bazy danych użytkownika za pomocą tej metody ręczne:

1. Odłączyć hello pliki bazy danych z hello lokalnego wystąpienia bazy danych.
2. Skopiuj pliki bazy danych hello odłączyć do magazynu obiektów blob platformy Azure przy użyciu hello [wiersza polecenia azcopy](../../../storage/common/storage-use-azcopy.md).
3. Dołącz pliki bazy danych hello z wystąpienia programu SQL Server toohello hello Azure adres URL w hello maszyny Wirtualnej platformy Azure.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>Konwertuj tooVM i przekazać tooURL i wdrożyć jako nową maszynę Wirtualną
Użyj tego toomigrate — metoda wszystkie bazy danych systemu i użytkownika w maszynie wirtualnej tooAzure wystąpienia lokalnego programu SQL Server. Użyj hello następujące ogólne kroki toomigrate całego wystąpienia programu SQL Server za pomocą tej metody ręcznego:

1. Konwertowanie fizycznej lub wirtualnej maszyny wirtualne dyski twarde tooHyper-V przy użyciu [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. Przekaż tooAzure pliki VHD magazynu przy użyciu hello [polecenia cmdlet Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Wdrażanie nowej maszyny wirtualnej za pomocą hello przekazać wirtualnego dysku twardego.

> [!NOTE]
> toomigrate całej aplikacji, należy rozważyć użycie [usługi Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Wyślij dysk twardy
Użyj hello [usługi Import/Eksport Windows metody](../../../storage/common/storage-import-export-service.md) tootransfer dużych ilości tooAzure danych pliku magazynu obiektów Blob w sytuacjach, gdy przekazywania przez sieć hello jest zbyt duży i nie jest możliwe. Z tą usługą wysyła jeden lub więcej dyski twarde zawierające ten tooan danych Azure centrach danych, w którym dane zostaną przekazane tooyour konta magazynu.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat uruchamiania programu SQL Server na maszynach wirtualnych platformy Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).

Aby uzyskać instrukcje dotyczące tworzenia maszyny wirtualnej Azure SQL Server z przechwyconego obrazu, zobacz [porady i sztuczki w klonowania maszyn wirtualnych Azure SQL z przechwyconych obrazów](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) na blogu CSS programu SQL Server inżynierów hello.

