---
title: "aaaMigrate maszyn wirtualnych z usług AWS tooAzure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toomigrate wirtualnych maszyn uruchomiona w tooAzure Amazon Web Services (AWS) przy użyciu usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Migrowanie maszyn wirtualnych w tooAzure Amazon Web Services (AWS) z usługą Azure Site Recovery

W tym artykule opisano, jak toomigrate systemu Windows usług AWS wystąpienia hello maszynom wirtualnym tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Migracja jest skutecznie trybu failover z usług AWS tooAzure. Nie tooAWS maszyny powrotu po awarii, i nie ma żadnych trwającej replikacji. W tym artykule opisano kroki hello dotyczące migracji w hello portalu Azure i są oparte na powitania instrukcje dotyczące [replikowanie tooAzure maszyny fizycznej](site-recovery-vmware-to-azure.md).

Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Obsługiwane systemy operacyjne

Usługa Site Recovery może być używane toomigrate EC2 wystąpień z dowolnym z następujących systemów operacyjnych hello:

- Systemu Windows (tylko w 64 bity)
    - Windows Server 2008 R2 z dodatkiem SP1 + (Citrix PV sterowników lub usług AWS PV tylko sterowniki. **Instancje systemem RedHat PV sterowniki nie są obsługiwane**) systemu Windows Server 2012 systemu Windows Server 2012 R2
- Linux (64-bitowy tylko)
    - Red Hat Enterprise Linux 6.7 (tylko w przypadku wystąpienia HVM zwirtualizowanych)

## <a name="prerequisites"></a>Wymagania wstępne

Oto, co jest potrzebne dla tego wdrożenia:

* **Serwer konfiguracji**: Amazon EC2 uruchomionych maszyn wirtualnych systemu Windows Server 2012 R2 jest wdrożona jako powitania serwera konfiguracji. Domyślnie program hello innych składników usługi Azure Site Recovery (serwer przetwarzania i główny serwer docelowy) są instalowane podczas wdrażania hello konfiguracji serwera. W tym artykule opisano kroki hello dotyczące migracji w hello portalu Azure i są oparte na powitania instrukcje dotyczące [Dowiedz się więcej](site-recovery-components.md)

* **Wystąpienia EC2**: hello Amazon EC2 wystąpień maszyn wirtualnych, które mają toomigrate.

## <a name="deployment-steps"></a>Kroki wdrażania

1. Utwórz magazyn usługi Recovery Services.
2. Grupy zabezpieczeń dla swoich wystąpień EC2 Hello powinien mieć skonfigurowanych reguł tooallow komunikacji między hello EC2 wystąpienia mają toomigrate i hello wystąpienia, na którym planujesz toodeploy powitania serwera konfiguracji.

3. Na powitania tego samego Amazon wirtualnego chmury prywatnej jako swoich wystąpień EC2 wdrażanie serwera konfiguracji automatycznego odzyskiwania systemu. Zobacz hello VMware / fizycznych tooAzure wymagania wstępne wymagania dotyczące wdrażania serwera konfiguracji.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Gdy serwer konfiguracji jest wdrożony w usług AWS i zarejestrowany w magazynie usług odzyskiwania, powinny być widoczne hello konfiguracji serwera i serwera przetwarzania w obszarze infrastruktura usługi Site Recovery w sposób przedstawiony poniżej:

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Po wdrożeniu serwera konfiguracji hello (może zająć się too15 minustes dla niego tooappear), zweryfikuj, że może komunikować się z maszynami wirtualnymi hello, które mają toomigrate.

6. [Konfigurowanie ustawień replikacji](site-recovery-setup-replication-settings-vmware.md).

7. Włącz replikację: Włącz replikację hello ma toomigrate maszyn wirtualnych. Może odnajdywać hello EC2 wystąpień przy użyciu prywatnych adresów IP hello, których można uzyskać z konsoli EC2 hello.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Po chronionych hello EC2 wystąpień i zakończeniu tooAzure replikacji hello [testować tryb failover](site-recovery-test-failover-to-azure.md) toovalidate wydajności aplikacji na platformie Azure.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Uruchom tryb Failover z usług AWS tooAzure dla każdej maszyny Wirtualnej. Opcjonalnie możesz utworzyć plan odzyskiwania i uruchamiania trybu Failover, toomigrate wiele maszyn wirtualnych z usług AWS tooAzure. [Dowiedz się więcej](site-recovery-create-recovery-plans.md) o planach odzyskiwania.

10. W przypadku migracji nie ma potrzeby toocommit trybu failover. Zamiast tego należy wybrać opcję przeprowadzenia migracji powitania dla każdego komputera ma toomigrate. Hello akcji przeprowadzenia migracji zakończy proces migracji hello spowoduje usunięcie replikacji dla maszyny hello i zatrzymuje usługi Site Recovery rozliczeń hello maszyny.

    ![Migrate (Migracja)](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Następne kroki

- [Przygotowanie replikacji tooenable zmigrowane maszyny](site-recovery-azure-to-azure-after-migration.md) tooanother region na potrzeby odzyskiwania po awarii.
- Zacznij chronić obciążenia, [replikując maszyny wirtualne platformy Azure.](site-recovery-azure-to-azure.md)
