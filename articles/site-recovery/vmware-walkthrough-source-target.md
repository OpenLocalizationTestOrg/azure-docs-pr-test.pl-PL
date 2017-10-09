---
title: "aaaSet hello źródła i celu tooAzure replikacji VMware z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie tooset kroki hello źródłowa i docelowa ustawień replikacji maszyn wirtualnych VMware tooAzure magazynu z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>Krok 8: Konfigurowanie hello źródłowa i docelowa dla tooAzure replikacji VMware

W tym artykule opisano sposób tooconfigure źródłowa i docelowa ustawień podczas replikowania lokalnie tooAzure maszyny wirtualne VMware, za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Konfigurowanie serwera konfiguracji hello, zarejestruj go w magazynie hello i odnajdywanie maszyn wirtualnych.

1. Kliknij przycisk **lokacji odzyskiwania** > **krok 1: Przygotowanie infrastruktury** > **źródła**.
2. Jeśli nie masz serwera konfiguracji, kliknij przycisk **+ serwer konfiguracji**.
3. W **Dodaj serwer**, sprawdź, czy **serwera konfiguracji** pojawia się w **typ serwera**.
4. Pobierz plik instalacyjny instalacja Unified usługi Site Recovery hello.
5. Pobierz klucz rejestracji magazynu hello. Należy to po uruchomieniu Instalatora Unified. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

   ![Konfiguracja źródła](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Zarejestruj serwer konfiguracji hello w magazynie hello

Następujące hello przed start, a następnie uruchom serwer konfiguracji hello tooinstall Unified instalacji, powitania serwera przetwarzania i hello główny serwer docelowy.
    - Uzyskać szybkie omówienie wideo

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Upewnij się, że hello zegar systemowy jest zsynchronizowany z na powitania serwera konfiguracji maszyny Wirtualnej, [serwer czasu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Powinna być zgodna. Jeśli jest 15 minut przed lub za, Instalator może zakończyć się niepowodzeniem.
    - Uruchom instalację jako Administrator lokalny na serwerze konfiguracji hello maszyny Wirtualnej.
    - Upewnij się, że włączono protokołu TLS 1.0 na powitania maszyny Wirtualnej.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> można również zainstalować serwer konfiguracji Hello [z wiersza polecenia hello](http://aka.ms/installconfigsrv).



## <a name="connect-toovmware-servers"></a>Połącz serwery tooVMware

tooallow usługi Azure Site Recovery toodiscover maszyn wirtualnych działających w środowisku lokalnym, potrzebujesz tooconnect Twojego programu VMware vCenter Server lub hostach ESXi vSphere z usługą Site Recovery. Przed rozpoczęciem należy zwrócić uwagę hello poniżej:

- Po dodaniu serwera vCenter hello lub tooSite hostami vSphere odzyskiwania przy użyciu konta bez uprawnień administratora na serwerze hello hello konto na potrzeby następujące uprawnienia:
    - Centrum danych, Magazyn danych, Folder, hosta, sieci, zasobów, wirtualnej maszyny, vSphere rozproszonego przełącznika.
    - Serwer vCenter Hello musi mieć uprawnienia widoków magazynu.
- Po dodaniu tooSite serwerów VMware odzyskiwania może zająć 15 minut lub dłużej, aby je tooappear w portalu hello.

### <a name="add-hello-account-for-automatic-discovery"></a>Dodaj konto hello automatycznego wykrywania

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>Konfigurowanie połączenia

Połącz tooservers w następujący sposób:

1. Wybierz **+ vCenter** toostart łączenie programu VMware vCenter server lub VMware vSphere ESXi hosta.
2. W **dodać vCenter**, określ przyjazną nazwę dla serwera hosta lub vCenter vSphere hello, a następnie określ hello adres IP lub nazwę FQDN serwera hello.
3. Pozostaw hello portu 443, chyba że VMware serwery są skonfigurowane toolisten na innym porcie żądań. Wybierz konto hello tooconnect toohello VMware vCenter lub vSphere ESXi serwera. Kliknij przycisk **OK**.
4. Usługa Site Recovery łączy serwery tooVMware przy użyciu hello określone ustawienia i odnajduje maszyn wirtualnych.

> [!NOTE]
> W przypadku dodawania serwera lub hosta przy użyciu konta, który nie ma uprawnień administratora na serwerze vCenter lub hosta hello, upewnij się, że konto hello ma te uprawnienia: centrum danych, Magazyn danych, Folder, hosta, sieci, zasobów, w przypadku maszyny wirtualnej i vSphere rozproszonego przełącznika. Ponadto hello programu VMware vCenter server musi widoków magazynu hello włączone uprawnienia.


## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello

Aby skonfigurować środowisko docelowe hello, upewnij się, że masz konto magazynu Azure i konfigurowanie sieci wirtualnej.

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**, i wybierz hello ma toouse subskrypcji platformy Azure.
2. Określ, czy docelowy modelu wdrażania jest oparte na Menedżera zasobów albo klasycznego.
3. Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.

   ![docelowy](./media/vmware-walkthrough-source-target/gs-target.png)
4. Jeśli nie utworzono konta magazynu lub sieci, kliknij przycisk **+ konto magazynu** lub **+ sieć**, toocreate wbudowanego konta lub sieci Menedżera zasobów.

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 9: Konfigurowanie zasad replikacji](vmware-walkthrough-replication.md)
