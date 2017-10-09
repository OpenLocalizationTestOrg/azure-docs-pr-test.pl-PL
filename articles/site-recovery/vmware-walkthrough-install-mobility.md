---
title: "Witaj aaaInstall usługę mobilności dla replikacji tooAzure VMware | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooinstall hello agent usługi mobilności VMware tooAzure replikacji przy użyciu usługi Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="88b91-103">Krok 10: Zainstaluj usługę mobilności hello</span><span class="sxs-lookup"><span data-stu-id="88b91-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="88b91-104">W tym artykule opisano sposób tooconfigure źródłowa i docelowa ustawień podczas replikowania lokalnie tooAzure maszyny wirtualne VMware, za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="88b91-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="88b91-105">Hello usługi mobilności przechwytywania zapisów danych na maszynie i przekazuje je toohello serwera przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="88b91-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="88b91-106">Na każdym komputerze można zainstalować, które mają tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="88b91-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="88b91-107">Zainstaluj ręcznie usługę mobilności hello, przy użyciu instalacji wypychanej z serwera przetwarzania hello Site Recovery po włączeniu replikacji lub za pomocą narzędzia System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="88b91-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="88b91-108">Jeśli używasz instalacji wypychanej hello usługa jest zainstalowana na powitania maszyny Wirtualnej, po włączeniu replikacji.</span><span class="sxs-lookup"><span data-stu-id="88b91-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="88b91-109">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="88b91-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="88b91-110">Instalowanie ręczne</span><span class="sxs-lookup"><span data-stu-id="88b91-110">Install manually</span></span>

1. <span data-ttu-id="88b91-111">Sprawdź hello [wymagania wstępne](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) dla instalacji ręcznej.</span><span class="sxs-lookup"><span data-stu-id="88b91-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="88b91-112">Postępuj zgodnie z [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) dotyczące ręcznej instalacji przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="88b91-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="88b91-113">Jeśli wolisz tooinstall z wiersza polecenia hello wykonaj [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="88b91-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="88b91-114">Zainstaluj z serwera przetwarzania hello</span><span class="sxs-lookup"><span data-stu-id="88b91-114">Install from hello process server</span></span>

<span data-ttu-id="88b91-115">Jeśli chcesz instalacji usługi mobilności hello toopush z serwera przetwarzania powitania po włączeniu replikacji dla maszyny Wirtualnej, należy konta, które mogą być używane przez hello procesu serwera tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="88b91-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="88b91-116">Konto Hello jest używana tylko dla instalacji wypychanej hello.</span><span class="sxs-lookup"><span data-stu-id="88b91-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="88b91-117">Powinien mieć [utworzone konto](vmware-walkthrough-prepare-vmware.md) które mogą być używane dla instalacji wypychanej.</span><span class="sxs-lookup"><span data-stu-id="88b91-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="88b91-118">Następnie możesz określić hello konta, które chcesz toouse podczas konfigurowania ustawień źródła podczas wdrażania usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="88b91-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="88b91-119">Następnie postępuj zgodnie z [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Jeśli chcesz, aby usługa mobilności hello toopush na maszynach wirtualnych z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="88b91-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="88b91-120">Inne metody</span><span class="sxs-lookup"><span data-stu-id="88b91-120">Other methods</span></span>

<span data-ttu-id="88b91-121">Dowiedz się więcej o [Instalowanie usługi mobilności hello przy użyciu programu Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), lub za pomocą [Konfiguracja DSC automatyzacji Azure](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="88b91-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="88b91-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88b91-122">Next steps</span></span>

<span data-ttu-id="88b91-123">Przejdź do zbyt[krok 11: Włączanie replikacji](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="88b91-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
