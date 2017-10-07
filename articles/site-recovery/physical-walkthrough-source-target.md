---
title: "aaaSet hello źródła i celu tooAzure replikacji serwerze fizycznym z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie tooset kroki hello źródłowa i docelowa ustawień replikacji magazynu tooAzure serwery fizyczne z hello usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>Krok 7: Konfigurowanie hello źródłowa i docelowa dla tooAzure replikacji serwera fizycznego

W tym artykule opisano sposób tooconfigure źródłowa i docelowa ustawień podczas replikowania lokalnie tooAzure serwerów fizycznych za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Konfigurowanie serwera konfiguracji hello, zarejestruj go w magazynie hello i Odkryj maszyny.

1. Kliknij przycisk **lokacji odzyskiwania** > **krok 1: Przygotowanie infrastruktury** > **źródła**.
2. Jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji**.
3. W **Dodaj serwer**, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.
4. Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.
5. Pobierz klucz rejestracji magazynu hello. Należy to po uruchomieniu Instalatora Unified. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

   ![Konfiguracja źródła](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Zarejestruj serwer konfiguracji hello w magazynie hello

Następujące hello przed start, a następnie uruchom serwer konfiguracji hello tooinstall Unified instalacji, powitania serwera przetwarzania i hello główny serwer docelowy. Witaj wideo Opisuje konfigurowanie składników hello replikacji tooAzure maszyny Wirtualnej VMware. Jednak hello sam proces jest prawidłowa dla replikacji tooAzure serwera fizycznego.

- Upewnij się, że hello zegar systemowy jest zsynchronizowany z na powitania serwera konfiguracji maszyny Wirtualnej, [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Powinna być zgodna. Jeśli jest 15 minut przed lub za, Instalator może zakończyć się niepowodzeniem.
- Uruchom Instalatora jako Administrator lokalny na komputerze z serwerem konfiguracji hello.
- Upewnij się, że włączono protokołu TLS 1.0 na powitania maszyny Wirtualnej.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> można również zainstalować serwer konfiguracji Hello [z wiersza polecenia hello](http://aka.ms/installconfigsrv).




## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello

Aby skonfigurować środowisko docelowe hello, upewnij się, że masz konto magazynu Azure i konfigurowanie sieci wirtualnej.

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**, i wybierz hello ma toouse subskrypcji platformy Azure.
2. Określ, czy docelowy modelu wdrażania jest oparte na Menedżera zasobów albo klasycznego.
3. Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.

   ![docelowy](./media/physical-walkthrough-source-target/gs-target.png)

4. Jeśli nie utworzono konta magazynu lub sieci, kliknij przycisk **+ konto magazynu** lub **+ sieć**, toocreate wbudowanego konta lub sieci Menedżera zasobów.

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 8: Konfigurowanie zasad replikacji](physical-walkthrough-replication.md)
