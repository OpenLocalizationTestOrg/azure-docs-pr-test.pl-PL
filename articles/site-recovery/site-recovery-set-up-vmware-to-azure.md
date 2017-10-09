---
title: "Konfigurowanie środowiska źródłowego hello (VMware tooAzure) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooset się z toostart środowiska lokalnego replikowanie wirtualnych VMware maszyny tooAzure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Konfigurowanie środowiska źródłowego hello (VMware tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure fizycznych](./site-recovery-set-up-physical-to-azure.md)

W tym artykule opisano, jak tooset się z toostart środowiska lokalnego replikowanie wirtualnych maszyn uruchomiona na VMware tooAzure.

## <a name="prerequisites"></a>Wymagania wstępne

Hello artykule przyjęto założenie, że utworzono już:
- W magazynie usług odzyskiwania w hello [portalu Azure](http://portal.azure.com "portalu Azure").
- Dedykowane konto w oprogramowaniu VMware vCenter sieci używanej do [automatyczne odnajdowanie](./site-recovery-vmware-to-azure.md).
- Maszynę wirtualną, na którym serwerze tooinstall hello konfiguracji.

## <a name="configuration-server-minimum-requirements"></a>Minimalne wymagania dotyczące konfiguracji serwera
oprogramowanie serwera konfiguracji Hello powinny zostać wdrożone na maszynie wirtualnej VMware wysokiej dostępności. Witaj w poniższej tabeli wymieniono hello minimalne wymagania dotyczące sprzętu, oprogramowania i wymagania sieciowe dotyczące serwera konfiguracji.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Serwery proxy oparty na protokole HTTPS nie są obsługiwane przez serwer konfiguracji hello.

## <a name="choose-your-protection-goals"></a>Wybranie celów ochrony

1. W hello portalu Azure, przejdź do pozycji toohello **usług odzyskiwania** magazyn bloku i wybierz magazyn.
2. Menu hello zasobów magazynu hello Przejdź zbyt**wprowadzenie** > **usługi Site Recovery** > **krok 1: Przygotowanie infrastruktury**  >  **Cel ochrony**.

    ![Wybieranie celów](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. W **cel ochrony**, wybierz pozycję **tooAzure**i wybierz polecenie **tak, z programem VMware vSphere Hypervisor**. Następnie kliknij przycisk **OK**.

    ![Wybieranie celów](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello
Konfigurowanie środowiska źródłowego hello obejmuje dwa działania głównego:

- Zainstaluj i Zarejestruj serwer konfiguracji z usługą Site Recovery.
- Odnajdywanie maszyn wirtualnych lokalnie łącząc usługi Site Recovery tooyour lokalnymi VMware vCenter lub vSphere EXSi hostów.

### <a name="step-1-install-and-register-a-configuration-server"></a>Krok 1: Zainstaluj i Zarejestruj serwer konfiguracji

1. Kliknij przycisk **krok 1: Przygotowanie infrastruktury** > **źródła**. W **Przygotuj źródło**, jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji** tooadd jeden.

    ![Konfiguracja źródła](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. Na powitania **Dodaj serwer** bloku, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.
4. Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.
5. Pobierz klucz rejestracji magazynu hello. Po uruchomieniu Instalatora Unified muszą się hello klucza rejestracji. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

    ![Konfiguracja źródła](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. Na komputerze hello używasz jako hello konfiguracji serwera, uruchom **Unified instalacja usługi Azure Site Recovery** tooinstall hello konfiguracji serwera, powitania serwera przetwarzania i główny hello docelowego serwera.

#### <a name="run-azure-site-recovery-unified-setup"></a>Uruchom usługi Azure Site Recovery Unified Instalatora

> [!TIP]
> Rejestracja serwera konfiguracji kończy się niepowodzeniem, jeśli hello godziną zegara systemowego różni się od czasu lokalnego przez ponad pięć minut. Synchronizowanie zegara systemowego z [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) przed rozpoczęciem powitalne instalacji.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Serwer konfiguracji Hello można zainstalować za pomocą wiersza polecenia. Aby uzyskać więcej informacji, zobacz [serwera konfiguracji hello instalowanie przy użyciu narzędzia wiersza polecenia](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Dodaj konto VMware hello automatycznego wykrywania

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>Krok 2: Dodaj vCenter
tooallow usługi Azure Site Recovery toodiscover maszyn wirtualnych działających w środowisku lokalnym, potrzebujesz tooconnect Twojego programu VMware vCenter Server lub hostach ESXi vSphere z usługą Site Recovery.

Wybierz **+ vCenter** toostart łączenie programu VMware vCenter server lub VMware vSphere ESXi hosta.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Typowe problemy
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Następne kroki
[Konfigurowanie środowiska docelowego](./site-recovery-prepare-target-vmware-to-azure.md) na platformie Azure.
