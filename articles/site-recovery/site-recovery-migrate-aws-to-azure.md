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
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="f040a-103">Migrowanie maszyn wirtualnych w tooAzure Amazon Web Services (AWS) z usługą Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f040a-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="f040a-104">W tym artykule opisano, jak toomigrate systemu Windows usług AWS wystąpienia hello maszynom wirtualnym tooAzure [usługi Azure Site Recovery](site-recovery-overview.md) usługi.</span><span class="sxs-lookup"><span data-stu-id="f040a-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="f040a-105">Migracja jest skutecznie trybu failover z usług AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f040a-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="f040a-106">Nie tooAWS maszyny powrotu po awarii, i nie ma żadnych trwającej replikacji.</span><span class="sxs-lookup"><span data-stu-id="f040a-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="f040a-107">W tym artykule opisano kroki hello dotyczące migracji w hello portalu Azure i są oparte na powitania instrukcje dotyczące [replikowanie tooAzure maszyny fizycznej](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f040a-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="f040a-108">Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="f040a-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="f040a-109">Obsługiwane systemy operacyjne</span><span class="sxs-lookup"><span data-stu-id="f040a-109">Supported operating systems</span></span>

<span data-ttu-id="f040a-110">Usługa Site Recovery może być używane toomigrate EC2 wystąpień z dowolnym z następujących systemów operacyjnych hello:</span><span class="sxs-lookup"><span data-stu-id="f040a-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="f040a-111">Systemu Windows (tylko w 64 bity)</span><span class="sxs-lookup"><span data-stu-id="f040a-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="f040a-112">Windows Server 2008 R2 z dodatkiem SP1 + (Citrix PV sterowników lub usług AWS PV tylko sterowniki.</span><span class="sxs-lookup"><span data-stu-id="f040a-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="f040a-113">**Instancje systemem RedHat PV sterowniki nie są obsługiwane**) systemu Windows Server 2012 systemu Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f040a-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="f040a-114">Linux (64-bitowy tylko)</span><span class="sxs-lookup"><span data-stu-id="f040a-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="f040a-115">Red Hat Enterprise Linux 6.7 (tylko w przypadku wystąpienia HVM zwirtualizowanych)</span><span class="sxs-lookup"><span data-stu-id="f040a-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f040a-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f040a-116">Prerequisites</span></span>

<span data-ttu-id="f040a-117">Oto, co jest potrzebne dla tego wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="f040a-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="f040a-118">**Serwer konfiguracji**: Amazon EC2 uruchomionych maszyn wirtualnych systemu Windows Server 2012 R2 jest wdrożona jako powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f040a-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="f040a-119">Domyślnie program hello innych składników usługi Azure Site Recovery (serwer przetwarzania i główny serwer docelowy) są instalowane podczas wdrażania hello konfiguracji serwera.</span><span class="sxs-lookup"><span data-stu-id="f040a-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="f040a-120">W tym artykule opisano kroki hello dotyczące migracji w hello portalu Azure i są oparte na powitania instrukcje dotyczące [Dowiedz się więcej](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="f040a-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="f040a-121">**Wystąpienia EC2**: hello Amazon EC2 wystąpień maszyn wirtualnych, które mają toomigrate.</span><span class="sxs-lookup"><span data-stu-id="f040a-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="f040a-122">Kroki wdrażania</span><span class="sxs-lookup"><span data-stu-id="f040a-122">Deployment steps</span></span>

1. <span data-ttu-id="f040a-123">Utwórz magazyn usługi Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f040a-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="f040a-124">Grupy zabezpieczeń dla swoich wystąpień EC2 Hello powinien mieć skonfigurowanych reguł tooallow komunikacji między hello EC2 wystąpienia mają toomigrate i hello wystąpienia, na którym planujesz toodeploy powitania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f040a-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="f040a-125">Na powitania tego samego Amazon wirtualnego chmury prywatnej jako swoich wystąpień EC2 wdrażanie serwera konfiguracji automatycznego odzyskiwania systemu.</span><span class="sxs-lookup"><span data-stu-id="f040a-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="f040a-126">Zobacz hello VMware / fizycznych tooAzure wymagania wstępne wymagania dotyczące wdrażania serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f040a-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="f040a-128">Gdy serwer konfiguracji jest wdrożony w usług AWS i zarejestrowany w magazynie usług odzyskiwania, powinny być widoczne hello konfiguracji serwera i serwera przetwarzania w obszarze infrastruktura usługi Site Recovery w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="f040a-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="f040a-130">Po wdrożeniu serwera konfiguracji hello (może zająć się too15 minustes dla niego tooappear), zweryfikuj, że może komunikować się z maszynami wirtualnymi hello, które mają toomigrate.</span><span class="sxs-lookup"><span data-stu-id="f040a-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="f040a-131">[Konfigurowanie ustawień replikacji](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="f040a-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="f040a-132">Włącz replikację: Włącz replikację hello ma toomigrate maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f040a-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="f040a-133">Może odnajdywać hello EC2 wystąpień przy użyciu prywatnych adresów IP hello, których można uzyskać z konsoli EC2 hello.</span><span class="sxs-lookup"><span data-stu-id="f040a-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="f040a-135">Po chronionych hello EC2 wystąpień i zakończeniu tooAzure replikacji hello [testować tryb failover](site-recovery-test-failover-to-azure.md) toovalidate wydajności aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f040a-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="f040a-137">Uruchom tryb Failover z usług AWS tooAzure dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f040a-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="f040a-138">Opcjonalnie możesz utworzyć plan odzyskiwania i uruchamiania trybu Failover, toomigrate wiele maszyn wirtualnych z usług AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f040a-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="f040a-139">[Dowiedz się więcej](site-recovery-create-recovery-plans.md) o planach odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="f040a-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="f040a-140">W przypadku migracji nie ma potrzeby toocommit trybu failover.</span><span class="sxs-lookup"><span data-stu-id="f040a-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="f040a-141">Zamiast tego należy wybrać opcję przeprowadzenia migracji powitania dla każdego komputera ma toomigrate.</span><span class="sxs-lookup"><span data-stu-id="f040a-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="f040a-142">Hello akcji przeprowadzenia migracji zakończy proces migracji hello spowoduje usunięcie replikacji dla maszyny hello i zatrzymuje usługi Site Recovery rozliczeń hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="f040a-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Migrate (Migracja)](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="f040a-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f040a-144">Next steps</span></span>

- <span data-ttu-id="f040a-145">[Przygotowanie replikacji tooenable zmigrowane maszyny](site-recovery-azure-to-azure-after-migration.md) tooanother region na potrzeby odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="f040a-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="f040a-146">Zacznij chronić obciążenia, [replikując maszyny wirtualne platformy Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="f040a-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
