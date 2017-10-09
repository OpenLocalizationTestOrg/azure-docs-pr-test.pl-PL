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
# <a name="step-10-install-hello-mobility-service"></a>Krok 10: Zainstaluj usługę mobilności hello


W tym artykule opisano sposób tooconfigure źródłowa i docelowa ustawień podczas replikowania lokalnie tooAzure maszyny wirtualne VMware, za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Hello usługi mobilności przechwytywania zapisów danych na maszynie i przekazuje je toohello serwera przetwarzania. Na każdym komputerze można zainstalować, które mają tooreplicate tooAzure.

Zainstaluj ręcznie usługę mobilności hello, przy użyciu instalacji wypychanej z serwera przetwarzania hello Site Recovery po włączeniu replikacji lub za pomocą narzędzia System Center Configuration Manager. Jeśli używasz instalacji wypychanej hello usługa jest zainstalowana na powitania maszyny Wirtualnej, po włączeniu replikacji.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="install-manually"></a>Instalowanie ręczne

1. Sprawdź hello [wymagania wstępne](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) dla instalacji ręcznej.
2. Postępuj zgodnie z [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) dotyczące ręcznej instalacji przy użyciu portalu hello.
3. Jeśli wolisz tooinstall z wiersza polecenia hello wykonaj [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).

## <a name="install-from-hello-process-server"></a>Zainstaluj z serwera przetwarzania hello

Jeśli chcesz instalacji usługi mobilności hello toopush z serwera przetwarzania powitania po włączeniu replikacji dla maszyny Wirtualnej, należy konta, które mogą być używane przez hello procesu serwera tooaccess hello maszyny Wirtualnej. Konto Hello jest używana tylko dla instalacji wypychanej hello.

1. Powinien mieć [utworzone konto](vmware-walkthrough-prepare-vmware.md) które mogą być używane dla instalacji wypychanej. Następnie możesz określić hello konta, które chcesz toouse podczas konfigurowania ustawień źródła podczas wdrażania usługi Site Recovery.
2. Następnie postępuj zgodnie z [tych instrukcji](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Jeśli chcesz, aby usługa mobilności hello toopush na maszynach wirtualnych z systemem Windows lub Linux.

## <a name="other-methods"></a>Inne metody

Dowiedz się więcej o [Instalowanie usługi mobilności hello przy użyciu programu Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), lub za pomocą [Konfiguracja DSC automatyzacji Azure](site-recovery-automate-mobility-service-install.md).

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 11: Włączanie replikacji](vmware-walkthrough-enable-replication.md)
