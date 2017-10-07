---
title: aaaBackup i przywracania dla programu SQL Server | Dokumentacja firmy Microsoft
description: "Zawiera opis zagadnień kopia zapasowa i przywracanie baz danych SQL Server uruchomiony na maszynach wirtualnych platformy Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Tworzenie i przywracanie kopii zapasowych programu SQL Server na maszynach wirtualnych platformy Azure
## <a name="overview"></a>Omówienie
Magazyn Azure przechowuje kopie 3 każdej maszyny Wirtualnej Azure dysku tooguarantee ochrony przed utratą danych lub uszkodzenie danych fizycznych. W związku z tym w przeciwieństwie do lokalnego, tooworry o tych nie jest konieczne. Jednak nadal należy utworzyć kopię zapasową tooprotect baz danych programu SQL Server przed błędy aplikacji lub użytkownika (np. Wstawianie nieodpowiedniego lub usuwaniem tabel) i jest w stanie toorestore tooa punktu w czasie.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Dla programu SQL Server uruchomiony na maszynach wirtualnych Azure można używać natywnego wykonywania kopii zapasowych i przywracania techniki przy użyciu dołączonych dysków dla docelowego hello hello plików kopii zapasowej. Istnieje jednak Ogranicz liczbę toohello dysków, możesz dołączyć tooan maszyny wirtualnej Azure, oparte na powitania [rozmiar maszyny wirtualnej hello](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Istnieje również koszty hello tooconsider zarządzania dyskami.

Począwszy od programu SQL Server 2014, musisz kopii zapasowej i przywracania tooMicrosoft magazynu obiektów Blob platformy Azure. SQL Server 2016 udostępnia również rozszerzeń dla tej opcji. Ponadto plików bazy danych przechowywanych w magazynie obiektów Blob Microsoft Azure, programu SQL Server 2016 udostępnia opcję dla niemal natychmiastowe tworzenie kopii zapasowych i szybkiego przywracania przy użyciu migawek Azure. W tym artykule omówiono te opcje i dodatkowe informacje można znaleźć w folderze [programu SQL Server z kopii zapasowej i przywracania usługi magazynu obiektów Blob platformy Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Omówienie hello opcje tworzenia kopii zapasowych bardzo dużych baz danych, zobacz [Terabajtowe programu SQL Server bazy danych kopii zapasowej strategii dla maszyn wirtualnych Azure](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

Poniższe rozdziały zawierają Hello obejmują informacje o określonych toohello różnych wersji programu SQL Server w maszynie wirtualnej platformy Azure obsługiwane.

## <a name="sql-server-virtual-machines"></a>Maszyny wirtualne serwera SQL
Kiedy wystąpienia programu SQL Server jest uruchomiona na maszynie wirtualnej platformy Azure, plików bazy danych już znajdują się na dysku z danymi na platformie Azure. Te dyski na żywo w magazynie obiektów Blob Azure. Dlatego hello przyczyn tworzenia kopii zapasowych z bazy danych i hello podejście może nieco potrwać zmiany. Należy wziąć pod uwagę następujące hello. 

* Ochrona tooprovide kopii zapasowych bazy danych tooperform awariami sprzętu lub nośnik nie są już potrzebne, ponieważ Microsoft Azure umożliwia ochronę jako część hello usługi Microsoft Azure.
* Nadal potrzebujesz tooperform bazy danych kopii zapasowych tooprovide ochrony przed błędy użytkownika lub archiwizacji, powodów przepisami lub celów administracyjnych.
* Plik kopii zapasowej hello można przechowywać bezpośrednio na platformie Azure. Aby uzyskać więcej informacji zobacz następujące sekcje zawierają wskazówki dotyczące hello różne wersje programu SQL Server hello.

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016 obsługuje [kopia zapasowa i przywracanie z obiektami blob Azure](https://msdn.microsoft.com/library/jj919148.aspx) znaleziono funkcji w programie SQL Server 2014. Ale zawiera także hello następujące ulepszenia:

| Rozszerzenie 2016 | Szczegóły |
| --- | --- |
| **Rozkładanie** |Podczas tworzenia kopii zapasowej tooMicrosoft magazynu obiektów blob platformy Azure, programu SQL Server 2016 obsługuje wykonywanie kopii zapasowych toomultiple tooenable obiektów blob, tworzenie kopii zapasowej dużych baz danych w górę tooa maksymalnie 12,8 TB. |
| **Kopia zapasowa migawki** |Za pomocą hello Azure migawek kopii zapasowej migawki pliku programu SQL Server zapewnia niemal natychmiastowe tworzenie kopii zapasowych i szybkiego przywracania plików bazy danych przechowywane przy użyciu usługi magazynu obiektów Blob platformy Azure hello. Ta funkcja umożliwia możesz toosimplify zasad tworzenia kopii zapasowych i przywracania. Kopia zapasowa migawki pliku obsługuje również punktu w czasie przywracania. Aby uzyskać więcej informacji, zobacz [kopii zapasowych migawki plików bazy danych na platformie Azure](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx). |
| **Zarządzane Planowanie tworzenia kopii zapasowej** |TooAzure zarządzanej kopii zapasowej serwera SQL obsługuje teraz niestandardowe harmonogramy. Aby uzyskać więcej informacji, zobacz [tooMicrosoft zarządzanej kopii zapasowej serwera SQL Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Samouczek hello możliwości programu SQL Server 2016 przy użyciu magazynu obiektów Blob platformy Azure, zobacz [samouczek: w przypadku baz danych programu SQL Server 2016 przy użyciu usługi magazynu obiektów Blob platformy Azure Microsoft hello](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 obejmuje hello następujące ulepszenia:

1. **Kopia zapasowa i przywracanie tooAzure**:
   
   * *Kopia zapasowa programu SQL Server tooURL* ma teraz obsługę programu SQL Server Management Studio. tooback opcja Hello się tooAzure jest teraz dostępna, korzystając z zadania tworzenia kopii zapasowej lub przywracania lub kreatora w programie SQL Server Management Studio. Aby uzyskać więcej informacji, zobacz [tooURL kopii zapasowej programu SQL Server](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *SQL Server zarządzanych kopii zapasowej tooAzure* ma nową funkcję, która umożliwia automatyczne zarządzanie kopii zapasowej. Jest to szczególnie przydatne w przypadku automatyzacji tworzenia kopii zapasowej zarządzania dla wystąpień programu SQL Server 2014 uruchomione na maszynie platformy Azure. Aby uzyskać więcej informacji, zobacz [tooMicrosoft zarządzanej kopii zapasowej serwera SQL Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Automatyczna usługa Backup* udostępnia dodatkowe automatyzacji tooautomatically Włącz *tooAzure zarządzanej kopii zapasowej serwera SQL* na wszystkich istniejących i nowych baz danych dla maszyny Wirtualnej programu SQL Server na platformie Azure. Aby uzyskać więcej informacji, zobacz [Automated Backup for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md) (Automatyczne tworzenie kopii zapasowych dla programu SQL Server w usłudze Azure Virtual Machines).
   * Przegląd wszystkich opcji hello tooAzure kopii zapasowej programu SQL Server 2014, zobacz [programu SQL Server z kopii zapasowej i przywracania usługi magazynu obiektów Blob platformy Microsoft Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Szyfrowanie**: SQL Server 2014 obsługuje szyfrowanie danych podczas tworzenia kopii zapasowej. Obsługuje wiele algorytmów szyfrowania i hello za pomocą osf certyfikatu lub klucza asymetrycznego. Aby uzyskać więcej informacji, zobacz [szyfrowania kopii zapasowych](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
Aby uzyskać szczegółowe informacje o kopii zapasowej serwera SQL i przywracania danych w programie SQL Server 2012, zobacz [kopii zapasowej i przywracanie z serwera bazy danych SQL (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx).

Począwszy od programu SQL Server 2012 z dodatkiem SP1 Cumulative Update 2, można tworzyć kopie zapasowe przywracania tooand z hello usługi Magazyn obiektów Blob Azure. To rozszerzenie może być używane tooback zapasową baz danych programu SQL Server na serwerze SQL Server uruchomiony na maszynie wirtualnej platformy Azure lub lokalnego wystąpienia. Aby uzyskać więcej informacji, zobacz [programu SQL Server z kopii zapasowej i przywracania usługi magazynu obiektów Blob Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Zalety używania usługi Magazyn obiektów Blob platformy Azure hello hello innymi hello możliwości toobypass hello 16 dysków limit dołączonych dysków, łatwość zarządzania, dostępność bezpośredniego hello hello pliku kopii zapasowej tooanother wystąpienia programu SQL Server działających na platformie Azure Maszyna wirtualna, lub lokalne wystąpienie na potrzeby odzyskiwania migracji lub po awarii. Aby uzyskać pełną listę toousing świadczenia usługi magazynu obiektów blob platformy Azure do przechowywania kopii zapasowych programu SQL Server, zobacz hello *korzyści* sekcji [programu SQL Server z kopii zapasowej i przywracania usługi magazynu obiektów Blob Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Aby uzyskać zalecenia dotyczące najlepszych rozwiązań i informacje dotyczące rozwiązywania problemów, zobacz [kopii zapasowej i przywracanie najlepszych rozwiązań (usługi magazynu obiektów Blob Azure)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx).

## <a name="sql-server-2008"></a>SQL Server 2008
Dla programu SQL Server z kopii zapasowej i przywracania danych w programie SQL Server 2008 R2, zobacz [wykonywanie kopii zapasowej i przywracanie baz danych programu SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

Dla kopii zapasowej serwera SQL i przywracania danych w programie SQL Server 2008, zobacz [wykonywanie kopii zapasowej i przywracanie baz danych programu SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Następne kroki
Jeśli planujesz wdrożenia programu SQL Server w maszynie Wirtualnej platformy Azure, inicjowania obsługi administracyjnej wskazówki można znaleźć w hello samouczka: [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure za pomocą Menedżera zasobów Azure](virtual-machines-windows-portal-sql-server-provision.md).

Mimo że wykonywanie kopii zapasowych i przywracania może być używane toomigrate danych, jest potencjalnie łatwiejsze danych migracji ścieżki tooSQL serwera na maszynie Wirtualnej platformy Azure. Pełne omówienie opcji migracji i zalecenia, zobacz [Migrowanie tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](virtual-machines-windows-migrate-sql.md).

Przejrzyj inne [zasobów uruchamiania programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

