---
title: aaaTroubleshoot problemy aktywacji maszyny wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Udostępnia hello Rozwiązywanie problemów z kroki rozwiązywania problemów aktywacji maszyny wirtualnej systemu Windows na platformie Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Rozwiązywanie problemów aktywacji maszyny wirtualnej systemu Windows Azure

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Jeśli masz problemy podczas aktywacji maszyny wirtualnej systemu Windows Azure (VM), która jest tworzona na podstawie obrazu niestandardowego, można użyć hello informacji dostępnych w problem hello tootroubleshoot tego dokumentu. 

## <a name="symptom"></a>Objaw

Podczas próby tooactivate maszyny Wirtualnej systemu Windows Azure, komunikat o błędzie podobny do wiadomość hello następujące przykładowe:

**Błąd: hello 0xC004F074 LicensingService oprogramowania zgłosił, że nie można aktywować komputera hello. Można się skontaktować z nie ManagementService kluczami (KMS). Zobacz dziennik zdarzeń aplikacji hello, aby uzyskać dodatkowe informacje.**

## <a name="cause"></a>Przyczyna
Ogólnie rzecz biorąc problemy dotyczące aktywacji maszyny Wirtualnej Azure wystąpić, jeśli hello maszyny Wirtualnej systemu Windows nie jest skonfigurowany przy użyciu hello odpowiedni klucz instalacji klienta usługi KMS lub hello maszyny Wirtualnej systemu Windows ma toohello problem łączności usługi Azure KMS (kms.core.windows.net, port 1668). 

## <a name="solution"></a>Rozwiązanie

>[!NOTE]
>Jeśli używasz sieci VPN lokacja lokacja i wymuszone tunelowanie, zobacz [Azure Użyj niestandardowych kieruje tooenable aktywacji usługi KMS przy użyciu tunelowania wymuszonego](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx). 
>
>Jeśli używasz usługi ExpressRoute i konieczne jest opublikowane trasy domyślnej, zobacz [maszyny Wirtualnej platformy Azure może się nie powieść tooactivate za pośrednictwem usługi ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>Krok 1 Konfiguruj hello odpowiedni klucz klienta usługi KMS instalacji (dla systemu Windows Server 2016 i Windows Server 2012 R2)

W przypadku hello maszynę Wirtualną, która jest tworzona na podstawie niestandardowego obrazu systemu Windows Server 2016 lub Windows Server 2012 R2 należy skonfigurować hello odpowiedni klucz klienta usługi KMS instalacji dla hello maszyny Wirtualnej.

Ten krok nie obejmuje tooWindows 2012 lub Windows 2008 R2. Używa hello funkcji automatyzacji Aktywacja maszyny wirtualnej (AVMA), która jest obsługiwana tylko przez system Windows Server 2016 i Windows Server 2012 R2.

1. Uruchom **slmgr.vbs/DLV** w wierszu polecenia z podwyższonym poziomem uprawnień. Sprawdź hello opis wartość w danych wyjściowych hello, a następnie określ, czy został utworzony z detaliczne (kanał sprzedaży DETALICZNEJ) lub z nośnika licencji zbiorczej (VOLUME_KMSCLIENT):
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Jeśli **slmgr.vbs/DLV** przedstawia kanał sprzedaży DETALICZNEJ, uruchom następujące polecenia tooset hello hello [klucz instalacji klienta usługi KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) hello wersji systemu Windows Server używana i wymusić tooretry aktywacji: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Na przykład dla systemu Windows Server 2016 centrum danych, możesz uruchomić hello następujące polecenie:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>Krok 2 Sprawdź hello łączność między hello maszyny Wirtualnej i usługa Azure KMS

1. Pobierać i wyodrębniać hello [narzędzia Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) narzędzie tooa lokalny folder w hello maszynę Wirtualną, która nie jest aktywowany. 

2. Przejdź tooStart, wyszukiwanie w programie Windows PowerShell, kliknij prawym przyciskiem myszy środowiska Windows PowerShell i wybierz polecenie Uruchom jako administrator.

3. Upewnij się, że hello, że maszyna wirtualna jest skonfigurowana toouse hello właściwym serwerem usługi KMS Azure. toodo to uruchom następujące polecenie:
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    polecenie Hello powinna zwracać: Nazwa komputera usługi zarządzania kluczami pomyślnie ustawiono tookms.core.windows.net:1688.

4. Sprawdź przy użyciu narzędzia Psping, że serwer usługi KMS toohello łączności. Przełącz toohello folder, w którym wyodrębniono hello Pstools.zip pobierania, a następnie uruchom następujące hello:
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  Upewnij się, że jest wyświetlany w hello sekundy do ostatniego wiersza danych wyjściowych hello,: Wysłane = 4, odebrane = 4, utracone = 0 (0% straty).

  Jeśli utracone jest większa niż 0 (zero), hello maszyny Wirtualnej nie ma serwer usługi KMS toohello łączności. W takiej sytuacji jeśli hello maszyna wirtualna jest w sieci wirtualnej i ma niestandardowy serwer DNS określona, należy się upewnić, że serwer DNS jest kms.core.windows.net tooresolve stanie. Możesz też zmienić hello tooone serwera DNS, który jest rozpoznawany kms.core.windows.net.

  Należy zauważyć, że po usunięciu wszystkich serwerów DNS z sieci wirtualnej maszyn wirtualnych użyć wewnętrznego usługa DNS platformy Azure. Ta usługa może zostać rozwiązany kms.core.windows.net.
  
Sprawdź także zaporą gościa hello nie został skonfigurowany w taki sposób, który może blokować próby aktywacji.

5. Po zweryfikowaniu tookms.core.windows.net połączenie powiodło się uruchamianie hello następujące polecenia w tym wierszu środowiska Windows PowerShell z podwyższonym poziomem uprawnień. To polecenie podejmuje aktywacji wiele razy.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

Pomyślnej aktywacji zwraca informacje podobne następujących hello:

**Aktywowanie Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678)... Produkt aktywowany pomyślnie.**

## <a name="faq"></a>Często zadawane pytania 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>Utworzony hello systemu Windows Server 2016 z portalu Azure Marketplace. Należy tooconfigure klucz usługi KMS do aktywacji systemu Windows Server 2016 hello? 
 
Nie. Obraz powitania w portalu Azure Marketplace ma hello odpowiedni klucz klienta usługi KMS instalacji już skonfigurowane. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>Pracy aktywacji systemu Windows hello sam sposób niezależnie od Jeśli hello maszyna wirtualna używa Azure hybrydowego Użyj korzyści (HUB) lub nie? 
 
Tak. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>Co się stanie, jeśli okres aktywacji systemu Windows? 
 
Gdy upłynął okres prolongaty hello i systemu Windows nadal nie włączono, Windows Server 2008 R2 i nowszych wersjach systemu Windows zostanie wyświetlone dodatkowe powiadomienia dotyczące aktywacji. tapety pulpitu Hello pozostanie czarne i usługi Windows Update zainstaluje zabezpieczeń i tylko aktualizacje krytyczne, ale nie opcjonalne aktualizacje. Zobacz powiadomień hello sekcji u dołu hello hello [warunki licencyjne](http://technet.microsoft.com/en-us/library/ff793403.aspx) strony.   

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
