---
title: "aaaSQL Server na maszynach wirtualnych Azure — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania dotyczące programem SQL Server na maszynach wirtualnych Azure."
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Często zadawane pytania dotyczące programu SQL Server w usłudze Azure Virtual Machines
W tym temacie przedstawiono odpowiedzi toosome z hello często zadawane pytania na temat uruchamiania [programu SQL Server na maszynach wirtualnych Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Często zadawane pytania

1. **Jak utworzyć maszynę wirtualną platformy Azure z programem SQL Server?**

    Witaj najlepszym rozwiązaniem jest toocreate maszynę wirtualną, która obejmuje program SQL Server. Samouczek dotyczący rejestracji na platformie Azure i tworzenia maszyny Wirtualnej SQL z hello portalu, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server w portalu Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Można wybrać obraz maszyny wirtualnej, który używa licencjonowania programu SQL Server o płatności na minutę, lub można użyć obrazu, który pozwala toobring licencję programu SQL Server. Istnieje również opcja hello ręcznego instalowania programu SQL Server na maszynie Wirtualnej i ponowne użycie licencji usługi lokalnej. Jeśli użycie własnej licencji, musisz mieć [przenośność licencji za pośrednictwem programu Software Assurance na platformie Azure](https://azure.microsoft.com/pricing/license-mobility/). Aby uzyskać więcej informacji, zobacz [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Wskazówki dotyczące cen maszyn wirtualnych platformy Azure z programem SQL Server).

1. **Co to jest hello różnica między maszynami wirtualnymi SQL i hello usługi baza danych SQL?**

    Koncepcyjnie programem SQL Server na maszynie wirtualnej platformy Azure nie, która różni się z programem SQL Server w zdalnym centrum danych. Z kolei [bazy danych SQL](../../../sql-database/sql-database-technical-overview.md) oferuje bazy danych jako usługa. Z bazy danych SQL nie masz dostępu toohello maszyny, które obsługi baz danych. Porównanie pełnej, zobacz [wybierz chmurę programu SQL Server option: Azure SQL Database (PaaS) lub SQL Server na maszynach wirtualnych Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Jak przeprowadzić migrację Mój toohello bazy danych programu SQL Server lokalne chmury?**

    Najpierw należy utworzyć maszyny wirtualnej platformy Azure z wystąpieniem programu SQL Server. Następnie przeprowadzenie migracji wystąpienia toothat lokalnych baz danych. Aby strategii migracji danych, zobacz [migracji tooSQL bazy danych serwera SQL Server w maszynie Wirtualnej platformy Azure](virtual-machines-windows-migrate-sql.md).

1. **Czy mogę zainstalować drugie wystąpienie programu SQL Server na powitania tej samej maszyny Wirtualnej? Czy można zmieniać zainstalowane funkcje hello domyślnego wystąpienia?**

    Tak. Witaj nośnik instalacyjny programu SQL Server znajduje się w folderze na powitania **C** dysku. Uruchom **Setup.exe** z tej lokalizacji tooadd nowe wystąpienia programu SQL Server lub toochange inne zainstalowane funkcje programu SQL Server na maszynie hello. Należy pamiętać, że niektóre funkcje, takie jak automatyczna usługa Backup, automatyczne stosowanie poprawek i integracji magazynu kluczy Azure wykonywać operacje tylko względem hello domyślnego wystąpienia.

1. **Czy można odinstalować hello domyślnego wystąpienia programu SQL Server**

    Tak. Istnieją pewne zagadnienia. Jak już wspomniano w poprzedniej hello odpowiedzi, funkcje, które opierają się na powitania [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md) wykonywać operacje tylko na powitania domyślnego wystąpienia. Po odinstalowaniu hello domyślnego wystąpienia rozszerzenia hello nadal toolook dla niego i może generować błędy dziennika zdarzeń. Te błędy są z następujących dwóch źródeł hello: **zarządzania poświadczeń programu Microsoft SQL Server** i **programu Microsoft SQL Server IaaS Agent**. Błędy hello może być podobne toohello następujące:
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    W razie wystąpienia domyślnego hello toouninstall należy również odinstalować hello [rozszerzenia agenta programu SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md) również.

1. **Jak uaktualnić tooa nowej wersji/wydania programu hello programu SQL Server w maszynie Wirtualnej platformy Azure?**

    Obecnie nie są bez uaktualnienia w miejscu programu SQL Server w maszynie Wirtualnej platformy Azure. Tworzenie nowej maszyny wirtualnej platformy Azure z wersji wersji programu SQL Server hello żądanego, a następnie przeprowadzić migrację bazy danych toohello nowego serwera przy użyciu standardu [techniki migracji danych](virtual-machines-windows-migrate-sql.md).

1. **Jak zainstalować mój licencjonowanej kopii programu SQL Server na maszynie Wirtualnej platformy Azure?**

    Istnieją dwa sposoby toodo to. Można je hello udostępnić [obrazy maszyny wirtualnej, które obsługuje licencji](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Inną opcją jest toocopy hello programu SQL Server instalacji nośnika tooa maszyny Wirtualnej systemu Windows Server, a następnie zainstaluj program SQL Server na powitania maszyny Wirtualnej. Licencjonowania powodów, musisz mieć [przenośność licencji za pośrednictwem programu Software Assurance na platformie Azure](https://azure.microsoft.com/pricing/license-mobility/). Aby uzyskać więcej informacji, zobacz [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Wskazówki dotyczące cen maszyn wirtualnych platformy Azure z programem SQL Server).

1. **Czy można zmienić toouse maszyny Wirtualnej własnej licencji programu SQL Server, jeśli został utworzony z jednego z obrazów z galerii hello?**

    Nie. Nie można przełączyć z płatności na minutę licencjonowania toousing własnej licencji. Tworzenie nowej maszyny wirtualnej platformy Azure przy użyciu jednej z hello [obrazy BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), a następnie przeprowadzić migrację bazy danych toohello nowego serwera przy użyciu standardu [techniki migracji danych](virtual-machines-windows-migrate-sql.md).

1. **Wystąpienia klastra trybu Failover (FCI) programu SQL Server są obsługiwane na maszynach wirtualnych Azure?**

   Tak. Możesz [utworzyć klaster trybu Failover systemu Windows w systemie Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) używanie bezpośrednie miejsca do magazynowania (S2D) hello magazynu klastra. Można również użyć rozwiązań innych firm klastra lub magazyn zgodnie z opisem w [wysokiej dostępności i odzyskiwania po awarii dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **Toolicense toopay programu SQL Server na maszynie Wirtualnej platformy Azure są dostępne Jeśli jest on używany tylko dla stanu wstrzymania i pracy awaryjnej?**

    Nie masz toopay toolicense jednego programu SQL Server uczestniczących w programie jako replika pomocnicza pasywnym we wdrożeniu wysokiej dostępności, jeśli masz Software Assurance i używać przenośność licencji, zgodnie z opisem w [często zadawane pytania dotyczące licencjonowania maszyny wirtualnej](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Jak są aktualizacje i dodatków service pack stosowane na maszynie Wirtualnej serwera SQL?**

    Maszyn wirtualnych zapewnia kontrolę nad hello komputer hosta, w tym, kiedy i jak należy zastosować aktualizacje. Dla systemu operacyjnego hello, możesz ręcznie zastosować aktualizacje systemu windows lub można włączyć usługi harmonogramu o nazwie [automatyczne stosowanie poprawek](virtual-machines-windows-sql-automated-patching.md). Usługa Automatyczne stosowanie poprawek instaluje wszelkie aktualizacje, które są oznaczone jako ważne, w tym aktualizacje programu SQL Server w tej kategorii. Inne tooSQL opcjonalne aktualizacje, które należy zainstalować ręcznie.

1. **Jest to możliwe tooset się konfiguracje nie są wyświetlane w galerii maszyn wirtualnych hello (na przykład Windows 2008 R2 i SQL Server 2012)**

    Nie. Dla maszyny wirtualnej galerii obrazów, które obejmują program SQL Server należy wybrać jeden z obrazów dostarczanych hello.

1. **Jak zainstalować narzędzia danych serwera SQL na maszynie Wirtualnej platformy Azure?**

     Pobierz i zainstaluj hello narzędzi danych SQL z [Microsoft SQL Server Data Tools - Business Intelligence dla programu Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Zasoby

Omówienie programu SQL Server na maszynach wirtualnych platformy Azure, Obejrzyj klip wideo hello [maszyny Wirtualnej platformy Azure jest najlepszą platformą hello SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). Można także uzyskać dobrą wprowadzenie w temacie hello [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).

Inne zasoby obejmują:

* [Aprowizowanie maszyny wirtualnej programu SQL Server w hello portalu Azure](virtual-machines-windows-portal-sql-server-provision.md)
* [Migrowanie tooSQL bazy danych serwera na maszynie Wirtualnej platformy Azure](virtual-machines-windows-migrate-sql.md)
* [Wysoka dostępność i odzyskiwanie po awarii dla programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-high-availability-dr.md)
* [Najlepsze rozwiązania w zakresie wydajności dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-performance.md)
* [Wzorce aplikacji i strategii rozwoju dla programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 