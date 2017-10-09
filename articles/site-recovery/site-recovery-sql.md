---
title: "aaaReplicate aplikacji za pomocą programu SQL Server i usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooreplicate SQL Server przy użyciu usługi Azure Site Recovery dla funkcji po awarii programu SQL Server."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>Ochrona programu SQL Server przy użyciu odzyskiwanie po awarii programu SQL Server i usługi Azure Site Recovery

W tym artykule opisano, jak hello tooprotect programu SQL Server zaplecza aplikacji przy użyciu kombinacji ciągłość prowadzenia działalności biznesowej programu SQL Server i technologii (BCDR) odzyskiwania po awarii, a [usługi Azure Site Recovery](site-recovery-overview.md).

Przed rozpoczęciem upewnij się, że rozumiesz możliwości odzyskiwania po awarii programu SQL Server, łącznie z klastra trybu failover, zawsze włączonych grup dostępności funkcji dublowania baz danych i wysyłania dziennika.


## <a name="sql-server-deployments"></a>Wdrożenie programu SQL Server

Wiele obciążeń Użyj programu SQL Server jako podstawę i można zintegrować z aplikacji, takich jak SharePoint, Dynamics i SAP, tooimplement usług danych.  SQL Server może być wdrożony na kilka sposobów:

* **Autonomicznego serwera SQL**: SQL Server i wszystkie bazy danych znajdują się na pojedynczym komputerze (fizycznej lub wirtualnej). Podczas wirtualizacji, klaster hosta jest używana do lokalnego wysokiej dostępności. Wysoka dostępność poziomie gościa nie jest zaimplementowana.
* **Tryb Failover Clustering wystąpienia programu SQL Server (zawsze na FCI)**: co najmniej dwa węzły z uruchomionym programem SQL Server instancji z udostępnionych dysków są skonfigurowane w klastrze pracy awaryjnej systemu Windows. Jeśli węzeł jest wyłączony, hello klastra może przełączyć tooanother wystąpienia programu SQL Server. Ta konfiguracja jest najczęściej używanymi tooimplement wysokiej dostępności w lokacji głównej. To wdrożenie nie chroni przed uszkodzenie lub awaria hello warstwy magazynu udostępnionego. Udostępniony dysk może być zaimplementowany przy użyciu udostępnionego dysku vhdx, fiber channel lub iSCSI.
* **SQL zawsze włączonych grup dostępności**: co najmniej dwa węzły są konfigurowane w udostępnionym klastra nic z baz danych serwera SQL skonfigurowany w grupie dostępności, Replikacja synchroniczna i automatycznej pracy awaryjnej.

 W tym artykule wykorzystuje powitania po natywnego technologii odzyskiwania po awarii SQL do przywrócenia lokacji zdalnej tooa baz danych:

* SQL zawsze włączonych grup dostępności, tooprovide odzyskiwania po awarii dla programu SQL Server 2012 lub 2014 Enterprise Edition.
* Funkcja dublowania bazy danych SQL w trybie wysokiego bezpieczeństwa, SQL Server Standard edition (dowolna wersja) lub SQL Server 2008 R2.

## <a name="site-recovery-support"></a>Obsługa odzyskiwania lokacji

### <a name="supported-scenarios"></a>Obsługiwane scenariusze
Usługa Site Recovery może chronić programu SQL Server, zgodnie z opisem w tabeli hello.

**Scenariusz** | **tooa lokacji dodatkowej** | **tooAzure**
--- | --- | ---
**Funkcja Hyper-V** | Tak | Tak
**VMware** | Tak | Tak
**Serwer fizyczny** | Tak | Tak

### <a name="supported-sql-server-versions"></a>Obsługiwane wersje programu SQL Server
Te wersje programu SQL Server są obsługiwane dla hello obsługiwane scenariusze:

* SQL Server 2016 Enterprise i Standard
* SQL Server 2014 Enterprise i Standard
* SQL Server 2012 Enterprise i Standard
* SQL Server 2008 R2 Enterprise i Standard

### <a name="supported-sql-server-integration"></a>Obsługiwaną integracji programu SQL Server

Usługa Site Recovery można zintegrować z natywnego technologiami BCDR serwera SQL podsumowane w tabeli hello, tooprovide rozwiązanie odzyskiwania po awarii.

**Funkcja** | **Szczegóły** | **SQL Server** |
--- | --- | ---
**Konfigurowanie zawsze włączonej grupy dostępności** | Uruchamianie wielu wystąpień autonomicznych programu SQL Server w klastrze trybu failover, który ma wiele węzłów.<br/><br/>Bazy danych można grupować w grupy trybu failover, które mogą zostać skopiowane (dublowany) w wystąpieniach programu SQL Server, aby niezbędne jest brak udostępnionego magazynu.<br/><br/>Zapewnia odzyskiwanie po awarii między lokacją główną i co najmniej jednej lokacji dodatkowej. Dwa węzły można skonfigurować w udostępnionej nic skonfigurowany klaster z baz danych programu SQL Server w grupie dostępności Replikacja synchroniczna i automatycznej pracy awaryjnej. | SQL Server 2014 & 2012 w wersji Enterprise
**(Zawsze na FCI dla) klastra trybu failover** | SQL Server korzysta z systemu Windows klastra trybu failover dla wysokiej dostępności lokalnego obciążeń programu SQL Server.<br/><br/>Węzły uruchomione wystąpienia programu SQL Server z udostępnionych dysków są skonfigurowane w klastrze pracy awaryjnej. Jeśli wystąpienie jest wyłączony za pośrednictwem toodifferent, co nie powiedzie się hello klastra.<br/><br/>Witaj klastra nie chroni przed awarią lub awarie w magazynie udostępnionym. Witaj udostępnionego dysku może być zaimplementowany z interfejsu iSCSI, fiber channel, lub udostępnionego Vhdx. | SQL Server Enterprise Edition<br/><br/>SQL Server Standard edition (tylko dla węzłów ograniczona tootwo)
**(Tryb wysokiego bezpieczeństwa) dublowania bazy danych** | Zapewnia ochronę jednej kopii bazy danych tooa jednej dodatkowej. Dostępne w obu wysokiego bezpieczeństwa (synchroniczne) i wysokiej wydajności replikacji (asynchronicznej) trybów. Nie wymaga klastra pracy awaryjnej. | SQL Server 2008 R2<br/><br/>SQL Server Enterprise wszystkie wersje
**Autonomiczny program SQL Server** | Hello programu SQL Server i bazy danych znajdują się na jednym serwerze (fizycznych lub wirtualnych). Klaster hostów jest używana wysokiej dostępności, gdy serwer hello jest wirtualnego. Nie wysokiej dostępności poziomie gościa. | Enterprise lub Standard edition

## <a name="deployment-recommendations"></a>Zalecenia dotyczące wdrożenia

Ta tabela zawiera podsumowanie Nasze zalecenia dotyczące integracji z usługą Site Recovery technologiami BCDR serwera SQL.

| **Wersja** | **Wersja** | **Wdrożenie** | **Lokalnego tooon — wersja Premium** | **TooAzure lokalnego** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 lub 2012 |Enterprise |Wystąpienie klastra pracy awaryjnej |Zawsze włączone grupy dostępności |Zawsze włączone grupy dostępności |
|| Enterprise |Zawsze włączone grupy dostępności wysokiej dostępności |Zawsze włączone grupy dostępności |Zawsze włączone grupy dostępności | |
|| Standardowa |Wystąpienia klastra trybu failover (FCI) |Replikacja z lokacji odzyskiwania dublowaniem lokalnego |Replikacja z lokacji odzyskiwania dublowaniem lokalnego | |
|| Enterprise lub Standard |Autonomiczna |Replikacja odzyskiwania lokacji |Replikacja odzyskiwania lokacji | |
| SQL Server 2008 R2 lub 2008 |Enterprise lub Standard |Wystąpienia klastra trybu failover (FCI) |Replikacja z lokacji odzyskiwania dublowaniem lokalnego |Replikacja z lokacji odzyskiwania dublowaniem lokalnego |
|| Enterprise lub Standard |Autonomiczna |Replikacja odzyskiwania lokacji |Replikacja odzyskiwania lokacji | |
| SQL Server (dowolna wersja) |Enterprise lub Standard |Wystąpienie klastra pracy awaryjnej — aplikacji usługi DTC |Replikacja odzyskiwania lokacji |Nieobsługiwane |

## <a name="deployment-prerequisites"></a>Wymagania wstępne dotyczące wdrożenia

* Lokalnego wdrożenia serwera SQL, zainstalowana obsługiwana wersja programu SQL Server. Zazwyczaj należy również usługi Active Directory dla programu SQL server.
* wymagania Hello hello scenariusz ma toodeploy. Dowiedz się więcej o wymaganiach dotyczących pomocy technicznej dla [tooAzure replikacji](site-recovery-support-matrix-to-azure.md) i [lokalnymi](site-recovery-support-matrix.md), i [wymagania wstępne dotyczące wdrażania](site-recovery-prereq.md).
* tooset zapasowej odzyskiwania na platformie Azure, uruchom hello [oceny gotowości maszyny wirtualnej Azure](http://www.microsoft.com/download/details.aspx?id=40898) narzędzia na maszynach wirtualnych programu SQL Server toomake się, że są one zgodne z platformy Azure i usługi Site Recovery.

## <a name="set-up-active-directory"></a>Konfigurowanie usługi Active Directory

Usługi Active Directory, w lokacji dodatkowej odzyskiwania hello, dla programu SQL Server toorun prawidłowo skonfigurowany.

* **Małe przedsiębiorstwa**— z mniejszą liczbą aplikacji i jednego kontrolera domeny do lokacji lokalnej hello, jeśli chcesz toofail za pośrednictwem hello całej lokacji, zalecane jest użycie usługi Site Recovery replikacji tooreplicate hello kontrolerem domeny toohello dodatkowego centrum danych lub tooAzure.
* **Średnia toolarge enterprise**— Jeśli masz wiele aplikacji w lesie usługi Active Directory i chcesz toofail przez aplikację lub obciążenia, zaleca się Konfigurowanie dodatkowego kontrolera domeny w hello dodatkowego centrum danych lub w Azure. Jeśli używasz zawsze na dostępność grupy toorecover tooa lokacji zdalnej, zaleca się Konfigurowanie innego dodatkowego kontrolera domeny w lokacji dodatkowej hello lub na platformie Azure, toouse dla wystąpienia programu SQL Server hello odzyskane.

Witaj instrukcje w tym artykule zakładają, że kontroler domeny jest dostępny w lokalizacji dodatkowej hello. [Dowiedz się więcej](site-recovery-active-directory.md) o ochronie usługi Active Directory z usługą Site Recovery.


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>Integrowanie z programu SQL Server AlwaysOn dla tooAzure replikacji

Oto co należy toodo:

1. Importuj skryptów do konta usługi Automatyzacja Azure. Zawiera toofailover skrypty hello grupy dostępności SQL w [maszyny wirtualnej usługi Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) i [maszynę wirtualną w klasycznym](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1).

    [![Wdrażanie tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. Dodaj ASR-SQL-FailoverAG jako akcją przed pierwszą grupą hello hello planu odzyskiwania.

1. Wykonaj instrukcje hello dostępne w hello skryptu toocreate nazwa hello tooprovide zmiennej automatyzacji hello grup dostępności.

### <a name="steps-toodo-a-test-failover"></a>Kroki toodo test trybu failover

Program SQL AlwaysOn nie obsługuje natywnie testowy tryb failover. Dlatego zaleca się następujące hello:

1. Konfigurowanie [kopia zapasowa Azure](../backup/backup-azure-vms.md) na maszynie wirtualnej hello hostującego replikę grupy dostępności hello na platformie Azure.

1. Aby mogło nastąpić wyzwolenie testowy tryb failover planu odzyskiwania hello, odzyskać hello maszyny wirtualnej z kopii zapasowej hello w poprzednim kroku hello.

    ![Przywracanie z kopii zapasowej systemu Azure ](./media/site-recovery-sql/restore-from-backup.png)

1. [Wymuszenie kworum](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) hello maszyny wirtualnej przywróconej z kopii zapasowej.

1. Zaktualizuj IP hello odbiornika tooan IP dostępne w hello testowej sieci trybu failover.

    ![Zaktualizuj odbiornik IP](./media/site-recovery-sql/update-listener-ip.png)

1. Przełącz odbiornika w trybie online.

    ![Przełącz do trybu Online odbiornika](./media/site-recovery-sql/bring-listener-online.png)

1. Tworzenie modułu równoważenia obciążenia z jeden adres IP utworzone na podstawie frontonu IP puli odpowiedniego tooeach odbiornika grupy dostępności i maszyny wirtualnej SQL hello dodane w puli zaplecza hello.

     ![Tworzenie usługi równoważenia obciążenia - puli adresów IP frontonu ](./media/site-recovery-sql/create-load-balancer1.png)

    ![Tworzenie usługi równoważenia obciążenia - puli wewnętrznej bazy danych ](./media/site-recovery-sql/create-load-balancer2.png)

1. Wykonaj test trybu failover planu odzyskiwania hello.

### <a name="steps-toodo-a-failover"></a>Kroki toodo trybu failover

Po dodaniu hello skryptu w planie odzyskiwania hello i planu odzyskiwania zweryfikowanych hello wykonując test trybu failover, możesz to zrobić trybu failover planu odzyskiwania hello.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>Integracja z programu SQL Server AlwaysOn dla lokacji dodatkowej lokalnymi tooa replikacji

Hello programu SQL Server używa grup dostępności dla wysokiej dostępności (lub FCI), zaleca się przy użyciu grup dostępności w również hello odzyskiwania lokacji. Należy pamiętać, że ma to zastosowanie tooapps, który nie używaj transakcji rozproszonej.

1. [Skonfuguruj](https://msdn.microsoft.com/library/hh213078.aspx) do grupy dostępności.
1. Tworzenie sieci wirtualnej w lokacji dodatkowej hello.
1. Konfigurowanie połączenia sieci VPN lokacja lokacja między hello sieci wirtualnej i lokacji głównej hello.
1. Utwórz maszynę wirtualną na powitania odzyskiwania lokacji i SQL Server należy zainstalować na nim.
1. Rozszerzanie hello istniejących zawsze na dostępność grupy toohello nową maszynę Wirtualną programu SQL Server. Konfigurowania tego wystąpienia programu SQL Server jako kopia repliki asynchronicznego.
1. Utwórz odbiornik grupy dostępności, lub zaktualizuj hello istniejący odbiornik tooinclude hello asynchroniczne maszyny wirtualnej repliki.
1. Upewnij się, że w farmie aplikacji hello jest skonfigurowany odbiornik hello. Jeśli Instalator przy użyciu nazwy serwera bazy danych hello, aktualizować toouse hello odbiornika, więc nie trzeba tooreconfigure go po hello w tryb failover.

W przypadku aplikacji korzystających z transakcji rozproszonych, zaleca się wdrażania usługi Site Recovery z [replikacji do lokacji serwera VMware/fizyczne](site-recovery-vmware-to-vmware.md).

### <a name="recovery-plan-considerations"></a>Zagadnienia dotyczące planu odzyskiwania
1. Ten przykładowy skrypt toohello biblioteki VMM, należy dodać w lokacjach głównych i dodatkowych hello.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. Po utworzeniu planu odzyskiwania dla aplikacji hello Dodaj sprzed akcji tooGroup 1 inicjowanych przez skrypty krok, wywołująca hello skryptu toofail za pośrednictwem grup dostępności.

## <a name="protect-a-standalone-sql-server"></a>Ochrona autonomicznego serwera SQL

W tym scenariuszu zaleca się, że używasz usługi Site Recovery replikacji tooprotect hello programu SQL Server maszyny. Hello kolejnych kroków zależy, czy serwer SQL jest maszyny Wirtualnej lub serwerze fizycznym i czy ma tooreplicate tooAzure lub dodatkowej lokacji lokalnymi. Dowiedz się więcej o [scenariuszy odzyskiwania lokacji](site-recovery-overview.md).

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>Ochrona klastra programu SQL Server (standard edition/Windows Server 2008 R2)

W przypadku klastra z programem SQL Server Standard edition lub SQL Server 2008 R2, firma Microsoft zaleca się, że używasz usługi Site Recovery tooprotect replikacji programu SQL Server.

### <a name="on-premises-tooon-premises"></a>Lokalne tooon lokalnej

* Jeśli aplikacja hello korzysta z transakcji rozproszonych zalecamy wdrożeniem [odzyskiwania lokacji za pomocą replikacji SAN](site-recovery-vmm-san.md) w środowisku funkcji Hyper-V lub [tooVMware serwera VMware/fizyczne](site-recovery-vmware-to-vmware.md) w środowisku VMware.
* Dla aplikacji z systemem innym niż DTC należy użyć hello powyżej podejście toorecover hello klastra jako serwer autonomiczny, dzięki wykorzystaniu lokalnego wysokiego bezpieczeństwa dublowania bazy danych.

### <a name="on-premises-tooazure"></a>TooAzure lokalnej

Usługa Site Recovery nie zapewnia gościa Obsługa klastrów podczas replikowania tooAzure. Dla wersji Standard programu SQL Server również nie zapewnia rozwiązanie odzyskiwania po awarii niskich kosztach. W tym scenariuszu zalecamy chronić hello lokalnego programu SQL Server klastra tooa autonomiczny programu SQL Server i odzyskać ją na platformie Azure.

1. Skonfiguruj dodatkowe autonomiczne wystąpienie programu SQL Server na powitania lokacji lokalnej.
1. Skonfiguruj hello wystąpienia tooserve jako dublowania dla hello baz danych można mają tooprotect. Konfigurowanie funkcji dublowania w trybie wysokiego bezpieczeństwa.
1. Konfigurowanie usługi Site Recovery w witrynie lokalne powitania dla ([funkcji Hyper-V](site-recovery-hyper-v-site-to-azure.md) lub [VMware maszyny wirtualne/serwery fizyczne)](site-recovery-vmware-to-azure-classic.md).
1. Użyj usługi Site Recovery replikacji tooreplicate hello nowego programu SQL Server wystąpienia tooAzure. Ponieważ jest kopii duplikatu wysokiego bezpieczeństwa, zostanie on zsynchronizowany z klastra głównego hello, ale będzie replikowany tooAzure przy użyciu replikacji usługi Site Recovery.


![Klaster w warstwie Standardowa](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>Zagadnienia dotyczące powrotu po awarii

W przypadku klastrów programu SQL Server Standard powrotu po awarii po nieplanowany tryb failover wymaga kopii zapasowej serwera SQL i przywracania z hello dublowany wystąpienia toohello oryginalnego klastra, z reestablishment hello duplikatu.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej](site-recovery-components.md) o architekturze usługi Site Recovery.
