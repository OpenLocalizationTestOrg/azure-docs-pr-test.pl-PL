---
title: "aaaSet hello źródłowego i docelowego dla lokacji dodatkowej tooa replikacji funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooset Konfigurowanie hello źródłowego i docelowego podczas replikowania maszyn wirtualnych funkcji Hyper-V toosecondary VMM lokacji z usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>Krok 6: Konfigurowanie hello replikacji źródłowa i docelowa


Po utworzeniu usługi odzyskiwania magazynu dla funkcji Hyper-V replikacji tooa lokacja dodatkowa programu VMM z [usługi Azure Site Recovery](site-recovery-overview.md), użyj tego artykułu tooset hello źródła i docelowe lokalizacje replikacji. 

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

Zainstalować hello dostawcy usługi Azure Site Recovery na serwerach VMM i Odnajdź i Zarejestruj serwer w magazynie hello.

1. Kliknij przycisk **krok 1: Przygotowanie infrastruktury** > **źródła**.

    ![Konfiguracja źródła](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. W **Przygotuj źródło**, kliknij przycisk **+ VMM** tooadd serwera programu VMM.

    ![Konfiguracja źródła](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. W **Dodaj serwer**, sprawdź, czy **serwera programu System Center VMM** pojawia się w **typ serwera** , że serwer VMM hello spełnia hello [wymagania wstępne](#prerequisites).
4. Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery hello.
5. Pobierz klucz rejestracji hello. Będzie on potrzebny po uruchomieniu Instalatora. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

    ![Konfiguracja źródła](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Zainstaluj hello dostawcy usługi Azure Site Recovery na serwerze VMM hello. Nie ma potrzeby tooexplicitly należy już nic instalować na serwerach hostów funkcji Hyper-V.


## <a name="install-hello-azure-site-recovery-provider"></a>Zainstaluj hello dostawcy usługi Azure Site Recovery

1. Uruchom plik Instalatora dostawcy hello na każdym serwerze programu VMM. Jeśli program VMM jest wdrożony w klastrze, wykonaj powitania po pierwszym instalowanym hello:
    -  Zainstaluj dostawcę hello na aktywnym węźle i Zakończ hello instalacji tooregister hello serwer VMM w magazynie hello.
    - Następnie należy zainstalować hello dostawcy na powitania innych węzłów. Węzły klastra należy uruchomić hello tę samą wersję programu hello dostawcy.
2. Instalator uruchamia kilka wymagań wstępnych i żądania usługi VMM hello toostop uprawnienia. Witaj usługi programu VMM zostanie automatycznie uruchomiona po zakończeniu instalacji. Po zainstalowaniu na klastrze programu VMM, możesz roli klastra hello toostop zostanie wyświetlony monit o.
3. W **Microsoft Update**, można włączyć toospecify czy aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.
4. W **instalacji**, Zaakceptuj lub zmodyfikuj hello domyślna lokalizacja instalacji, a następnie kliknij przycisk **zainstalować**.

    ![Lokalizacja instalacji](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. Po zakończeniu instalacji kliknij przycisk **zarejestrować** tooregister powitania serwera w magazynie hello.

    ![Lokalizacja instalacji](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. W **nazwę magazynu**, sprawdź nazwę hello hello magazynu, w którym hello serwer zostanie zarejestrowany. Kliknij przycisk *Dalej*.

    ![Rejestracja serwera](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. W **połączenia internetowego**, określ, jak dostawca hello uruchomiony na serwerze VMM hello łączy tooAzure.

    ![Ustawienia internetowe](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - Można określić, tego dostawcy hello należy łączyć bezpośrednio toohello internet, lub za pośrednictwem serwera proxy.
   - Określ ustawienia serwera proxy, jeśli to konieczne.
   - Jeśli używasz serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) jest tworzony automatycznie przy użyciu hello określonych poświadczeń serwera proxy. Konfiguracja serwera proxy hello, dzięki czemu to konto mogło być pomyślnie uwierzytelnione. Witaj ustawienia konta Uruchom jako można modyfikować w konsoli programu VMM hello > **ustawienia** > **zabezpieczeń** > **konta Uruchom jako**. Uruchom ponownie zmiany tooupdate usługi VMM hello.
8. W **klucz rejestracji**, zaznacz klucz hello pobrany z usługi Azure Site Recovery, a następnie skopiować toohello serwera VMM.
9. ustawienie szyfrowania Hello jest używana tylko w przypadku replikacji maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM. Jeśli replikujesz tooa lokacji dodatkowej nie jest używane.
10. W **nazwy serwera**, określ serwer VMM hello tooidentify przyjazną nazwę w magazynie hello. W konfiguracji klastra Określ nazwę roli klastra VMM hello.
11. W **Synchronizuj metadane chmury**, wybierz, czy dla wszystkich chmur na powitania serwera VMM w magazynie hello toosynchronize metadanych. Ta akcja wymaga tylko toohappen raz na każdym serwerze. Jeśli nie chcesz toosynchronize wszystkich chmur, można zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie WE hello właściwości chmury w konsoli programu VMM hello.
12. Kliknij przycisk **dalej** toocomplete hello procesu. Po rejestracji metadane z serwera VMM hello są pobierane przez usługę Azure Site Recovery. Serwer Hello jest wyświetlany na powitania **serwery VMM** kartę na powitania **serwerów** strony w magazynie hello.

    ![Serwer](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Po hello serwer jest dostępny w konsoli usługi Site Recovery hello w **źródła** > **Przygotuj źródło** wybierz serwer VMM hello i wybierz hello chmury, w których hello funkcji Hyper-V znajduje się host. Następnie kliknij przycisk **OK**.

Dostawca hello można także zainstalować z wiersza polecenia hello:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello

Wybierz hello docelowym serwerze VMM i w chmurze:

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**i wybierz hello docelowym serwerze VMM ma toouse.
2. Pojawi się na serwerze hello chmury, które są synchronizowane z usługą Site Recovery. Wybierz chmurę docelową hello.

   ![docelowy](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Następne kroki

Przejdź za[kroku 7: Konfigurowanie mapowania sieci](vmm-to-vmm-walkthrough-network-mapping.md).
