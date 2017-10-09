---
title: "Witaj aaaInstall usługę mobilności dla serwera fizycznego tooAzure replikacji | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooinstall hello agent usługi mobilności na serwerach fizycznych replikowanie tooAzure z usługą Azure Site Recovery hello."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="1b7ed-103">Krok 9: Instalowanie usługi mobilności hello</span><span class="sxs-lookup"><span data-stu-id="1b7ed-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="1b7ed-104">W tym artykule opisano sposób tooinstall hello składnika usługi Mobility podczas replikowania lokalnych tooAzure serwerach fizycznych systemu Windows i Linux, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="1b7ed-105">Hello usługi mobilności przechwytywania zapisów danych na maszynie i przekazuje je toohello serwera przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="1b7ed-106">Na każdym serwerze, można zainstalować, które mają tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="1b7ed-107">Można ręcznie zainstalować usługi mobilności hello, lub za pomocą instalacji wypychanej hello Site Recovery przetworzyć serwera po włączeniu replikacji lub za pomocą narzędzi takich jak System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="1b7ed-108">Jeśli używasz instalacji wypychanej usługa hello jest zainstalowana na serwerze powitania po włączeniu replikacji.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="1b7ed-109">Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1b7ed-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="1b7ed-110">Instalowanie ręczne</span><span class="sxs-lookup"><span data-stu-id="1b7ed-110">Install manually</span></span>

1. <span data-ttu-id="1b7ed-111">Sprawdź hello [wymagania wstępne](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) dla instalacji ręcznej.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="1b7ed-112">Postępuj zgodnie z [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) dotyczące ręcznej instalacji przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="1b7ed-113">Jeśli wolisz tooinstall z wiersza polecenia hello wykonaj [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="1b7ed-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="1b7ed-114">Zainstaluj z serwera przetwarzania hello</span><span class="sxs-lookup"><span data-stu-id="1b7ed-114">Install from hello process server</span></span>

<span data-ttu-id="1b7ed-115">Jeśli chcesz hello toopush instalacji usługi mobilności z serwera przetwarzania powitania po włączeniu replikacji dla maszyny, należy konta, które mogą być używane przez hello procesu serwera tooaccess hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="1b7ed-116">Konto Hello jest używana tylko dla instalacji wypychanej hello.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="1b7ed-117">Jeśli nie utworzono konta, to zrobić przy użyciu poniższych wskazówek:</span><span class="sxs-lookup"><span data-stu-id="1b7ed-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="1b7ed-118">Korzystając z domeny lub lokalnego konta</span><span class="sxs-lookup"><span data-stu-id="1b7ed-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="1b7ed-119">W systemie Windows Jeśli nie używasz konta domeny, należy toodisable kontroli dostępu użytkownika zdalnego na komputerze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="1b7ed-120">toodo, hello rejestrowania w obszarze **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, Dodaj wpis DWORD hello **LocalAccountTokenFilterPolicy**, o wartości 1.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="1b7ed-121">Wpis rejestru hello tooadd dla systemu Windows z interfejsu wiersza polecenia, wpisz:</span><span class="sxs-lookup"><span data-stu-id="1b7ed-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="1b7ed-122">Dla systemu Linux hello konto powinno być głównym urzędem certyfikacji na serwerze Linux źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="1b7ed-123">Następnie postępuj zgodnie z [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Jeśli chcesz, aby usługa mobilności hello toopush na maszynach wirtualnych z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="1b7ed-124">Inne metody instalacji</span><span class="sxs-lookup"><span data-stu-id="1b7ed-124">Other installation methods</span></span>

- <span data-ttu-id="1b7ed-125">[Dowiedz się więcej o](site-recovery-install-mobility-service-using-sccm.md) Instalowanie usługi mobilności hello przy użyciu programu Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="1b7ed-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="1b7ed-126">[Dowiedz się więcej o](site-recovery-automate-mobility-service-install.md) instalacji z usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="1b7ed-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b7ed-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b7ed-127">Next steps</span></span>

<span data-ttu-id="1b7ed-128">Przejdź do zbyt[kroku 10: Włączanie replikacji](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="1b7ed-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
