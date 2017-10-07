---
title: "Konfigurowanie środowiska źródłowego hello (tooAzure serwerów fizycznych) | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooset się toostart środowiska użytkownika lokalnego, replikowania serwerów fizycznych z systemem Windows lub Linux na platformie Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Konfigurowanie środowiska źródłowego hello (tooAzure serwera fizycznego)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure fizycznych](./site-recovery-set-up-physical-to-azure.md)

W tym artykule opisano sposób tooset się toostart środowiska użytkownika lokalnego, replikowania serwerów fizycznych z systemem Windows lub Linux na platformie Azure.

## <a name="prerequisites"></a>Wymagania wstępne

Hello artykule przyjęto założenie, że masz już:
1. Magazyn usług odzyskiwania w hello [portalu Azure](http://portal.azure.com "portalu Azure").
3. Komputer fizyczny, na którym serwerze tooinstall hello konfiguracji.

### <a name="configuration-server-minimum-requirements"></a>Minimalne wymagania dotyczące konfiguracji serwera
Witaj w poniższej tabeli wymieniono hello minimalne wymagania dotyczące sprzętu, oprogramowania i wymagania sieciowe dotyczące serwera konfiguracji.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Serwery proxy oparty na protokole HTTPS nie są obsługiwane przez serwer konfiguracji hello.

## <a name="choose-your-protection-goals"></a>Wybranie celów ochrony

1. W hello portalu Azure, przejdź do pozycji toohello **usług odzyskiwania** magazyny bloku, a następnie wybierz magazyn.
2. W hello **zasobów** kliknij menu magazynu hello **wprowadzenie** > **usługi Site Recovery** > **krok 1: przygotowanie Infrastruktura** > **cel ochrony**.

    ![Wybieranie celów](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. W **cel ochrony**, wybierz pozycję **tooAzure** i **nie zwirtualizowanych/inne**, a następnie kliknij przycisk **OK**.

    ![Wybieranie celów](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

1. W **Przygotuj źródło**, jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji** tooadd jeden.

  ![Konfiguracja źródła](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. W hello **Dodaj serwer** bloku, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.
4. Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.
5. Pobierz klucz rejestracji magazynu hello. Po uruchomieniu Instalatora Unified muszą się hello klucza rejestracji. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

    ![Konfiguracja źródła](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. Na komputerze hello używasz jako hello konfiguracji serwera, uruchom **Unified instalacja usługi Azure Site Recovery** tooinstall hello konfiguracji serwera, powitania serwera przetwarzania i główny hello docelowego serwera.

#### <a name="run-azure-site-recovery-unified-setup"></a>Uruchom usługi Azure Site Recovery Unified Instalatora

> [!TIP]
> Rejestracja serwera konfiguracji kończy się niepowodzeniem, jeśli czas hello na zegara systemowego jest więcej niż pięć minut wylogowuje na czas lokalny. Synchronizowanie zegara systemowego z [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) przed rozpoczęciem powitalne instalacji.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Serwer konfiguracji Hello można zainstalować za pomocą wiersza polecenia. Aby uzyskać więcej informacji, zobacz [Instalowanie serwera konfiguracji za pomocą narzędzia wiersza polecenia](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Typowe problemy

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Następne kroki

Następny krok polega na [Konfigurowanie środowiska docelowego](./site-recovery-prepare-target-physical-to-azure.md) na platformie Azure.
