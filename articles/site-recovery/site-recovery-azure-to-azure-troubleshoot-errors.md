---
title: "aaaAzure usługi Site Recovery Rozwiązywanie problemów z błędów i problemów z replikacją Azure do platformy Azure | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z błędów i problemów podczas replikowania maszyn wirtualnych platformy Azure dla odzyskiwania po awarii"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Rozwiązywanie problemów z replikacją maszyn wirtualnych Azure do platformy Azure

W tym artykule opisano hello typowych problemów w usłudze Azure Site Recovery podczas replikacji i odzyskiwania maszyn wirtualnych platformy Azure z jednego regionu tooanother oraz wyjaśniono, jak tootroubleshoot je. Aby uzyskać więcej informacji o obsługiwanych konfiguracjach, zobacz hello [macierz obsługi replikowania maszyn wirtualnych platformy Azure](site-recovery-support-matrix-azure-to-azure.md).

## <a name="azure-resource-quota-issues-error-code-150097"></a>Problemy przydziału zasobów platformy Azure (kod błędu 150097)
Subskrypcji powinna być włączona toocreate maszynach wirtualnych platformy Azure w region docelowy hello planowanie toouse jako obszar odzyskiwania po awarii. Ponadto subskrypcji powinny mieć wystarczające włączone przydziały toocreate maszyn wirtualnych o określonym rozmiarze. Domyślnie usługi Site Recovery pobrania hello sam rozmiar hello docelowego maszyny Wirtualnej, ponieważ hello źródłowej maszyny Wirtualnej. Jeśli rozmiar pasującego hello jest niedostępna, hello najbliższy rozmiar możliwe jest pobierany automatycznie. Jeśli rozmiar pasującego obsługującego źródła konfiguracji maszyny Wirtualnej nie jest, zostanie wyświetlony ten komunikat o błędzie:

**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia**
--- | --- | ---
150097<br></br>**Komunikat**: nie można włączyć replikacji dla maszyny wirtualnej hello VmName. | -Subskrypcja identyfikator nie może być włączona toocreate żadnej maszyny wirtualnej w lokalizacji region docelowy hello.</br></br>— Identyfikator subskrypcji nie może być włączone lub nie ma wystarczających przydziału toocreate określonych rozmiarów maszyn wirtualnych w lokalizacji region docelowy hello.</br></br>— Dla rozmiaru maszyny Wirtualnej odpowiedniego elementu docelowego odpowiadający źródła hello liczba kart interfejsu Sieciowego maszyny Wirtualnej (2) nie zostanie odnaleziony hello subskrypcji o identyfikatorze w lokalizacji region docelowy hello.| Skontaktuj się z [Azure pomocy dotyczącej rozliczeń](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable tworzenia maszyny Wirtualnej dla hello wymagane rozmiarów maszyn wirtualnych w miejscu docelowym powitania dla Twojej subskrypcji. Po włączeniu hello ponownych prób nie można wykonać operacji.

### <a name="fix-hello-problem"></a>Rozwiąż hello problem
Możesz skontaktować się [Azure pomocy dotyczącej rozliczeń](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable Twojego toocreate subskrypcji maszyn wirtualnych z wymaganym rozmiarze w miejscu docelowym hello.

Jeśli lokalizacja docelowa hello ma ograniczenie pojemności, wyłącz replikację i Włącz tooa innej lokalizacji, gdzie subskrypcji ma wystarczające toocreate limitu przydziału maszyn wirtualnych o rozmiarach hello wymagane.

## <a name="trusted-root-certificates-error-code-151066"></a>Zaufane certyfikaty główne (kod błędu 151066)

Jeśli wszystkie hello najnowsze zaufanych certyfikatów głównych nie są dostępne na powitania maszyny Wirtualnej, zadanie "Włącz replikację" może zakończyć się niepowodzeniem. Wywołania z hello maszyny Wirtualnej bez hello certyfikatów, hello uwierzytelniania i autoryzacji usługi Site Recovery zakończyć się niepowodzeniem. zostanie wyświetlony komunikat o błędzie Hello zadania usługi Site Recovery "Włącz replikację" hello nie powiodło się:

**Kod błędu:** | **Możliwa przyczyna** | **Zalecenia**
--- | --- | ---
151066<br></br>**Komunikat**: Konfiguracja usługi Site Recovery nie powiodła się. | Witaj wymagane zaufanych certyfikatów głównych używany do autoryzacji i uwierzytelniania nie są dostępne na powitania maszyny. | — Dla maszyny Wirtualnej, system operacyjny Windows hello upewnij się, że hello zaufane certyfikaty główne są obecne na komputerze hello. Aby uzyskać informacje, zobacz [Konfigurowanie zaufanych certyfikatów głównych i certyfikatów niedozwolonych](https://technet.microsoft.com/library/dn265983.aspx).<br></br>— Dla maszyny Wirtualnej, systemem operacyjnym Linux hello wykonaj hello wskazówki dotyczące zaufanych certyfikatów głównych opublikowanych przez dystrybutora wersji systemu operacyjnego Linux hello.

### <a name="fix-hello-problem"></a>Rozwiąż hello problem
**Windows**

Zainstaluj wszystkie hello najnowsze aktualizacje systemu Windows na powitania maszyny Wirtualnej tak, aby wszystkie certyfikaty główne hello zaufane znajdują się na komputerze hello. Jeśli pracujesz w środowisku bez połączenia, procedura hello standardowe Windows update w certyfikatach hello tooget organizacji. Jeśli hello wymagane certyfikaty nie są dostępne na powitania maszyny Wirtualnej, hello toohello wywołania usługi Site Recovery nie ze względów bezpieczeństwa.

Wykonaj typowe zarządzania aktualizacjami systemu Windows hello lub certyfikat proces zarządzania aktualizacjami w Twojej organizacji tooget, wszystkie najnowsze certyfikaty główne hello i odwołania certyfikatu hello zaktualizowane listy na powitania maszyn wirtualnych.

tooverify, który hello problem zostanie rozwiązany, przejdź toologin.microsoftonline.com z przeglądarki w maszynie Wirtualnej.

**Linux**

Wykonaj wskazówki hello Linux dystrybutora tooget hello najnowsze zaufanych certyfikatów głównych oraz hello ostatnią listę odwołania certyfikatów na powitania maszyny Wirtualnej.

Ponieważ SuSE Linux używa łączy symbolicznych toomaintain listę certyfikatów, wykonaj następujące kroki:

1.  Zaloguj się jako użytkownik root.

2.  Uruchom następujące polecenie:

      ``# cd /etc/ssl/certs``

3.  toosee Jeśli certyfikat hello Symantec głównego urzędu certyfikacji jest obecna, uruchom następujące polecenie:

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Jeśli plik hello nie zostanie odnaleziony, uruchom następujące polecenia:

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  toocreate łącza symbolicznego z b204d74a.0 -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem, uruchom to polecenie:

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  Sprawdź toosee, jeśli hello następujące dane wyjściowe tego polecenia. Jeśli nie masz toocreate łącza symbolicznego:

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. Jeśli 653b494a.0 łącza symbolicznego nie jest obecny, użyj tego polecenia toocreate łącza symbolicznego:

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Łączność wychodząca dla zakresów adresów URL odzyskiwania lokacji lub adres IP (kod błędu 151037 lub 151072)

Dla toowork replikacji usługi Site Recovery toospecific łączność wychodząca, który zakresów adresów URL lub adres IP jest wymagana od hello maszyny Wirtualnej. Jeśli maszyna wirtualna znajduje się za zaporą lub używać sieci łączność wychodząca reguły toocontrol zabezpieczeń grupy (NSG), może pojawić się jeden z tych komunikatów o błędzie:

**Kody błędów** | **Możliwe przyczyny** | **Zalecenia**
--- | --- | ---
151037<br></br>**Komunikat**: nie powiodło się tooregister maszyny wirtualnej platformy Azure z usługą Site Recovery. | -Używasz NSG toocontrol wychodzący dostęp na powitania maszyny Wirtualnej i hello wymagane IP zakresów nie są białej dla ruchu wychodzącego dostępu.</br></br>-Używasz narzędzia zapór i hello wymagane zakresy IP/adresy URL nie są białej.</br>| — Jeśli używasz zapory serwera proxy toocontrol wychodzącego łączność na powitania maszyny Wirtualnej, upewnij się, że hello wymagań wstępnych adresy URL lub zakresy IP centrum danych są białej. Aby uzyskać informacje, zobacz [zapory wskazówki dotyczące serwera proxy](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>— Jeśli używasz łączności sieciowej wychodzących toocontrol reguły NSG na powitania maszyny Wirtualnej, upewnij się, że zakresy IP centrum danych wymagań wstępnych hello są białej. Aby uzyskać informacje, zobacz [wskazówki dotyczące grupy zabezpieczeń sieci](https://aka.ms/a2a-nsg-guidance).
151072<br></br>**Komunikat**: Konfiguracja usługi Site Recovery nie powiodła się. | Połączenie nie może być punktów końcowych usługi odzyskiwania tooSite ustalonych. | — Jeśli używasz zapory serwera proxy toocontrol wychodzącego łączność na powitania maszyny Wirtualnej, upewnij się, że hello wymagań wstępnych adresy URL lub zakresy IP centrum danych są białej. Aby uzyskać informacje, zobacz [zapory wskazówki dotyczące serwera proxy](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>— Jeśli używasz łączności sieciowej wychodzących toocontrol reguły NSG na powitania maszyny Wirtualnej, upewnij się, że zakresy IP centrum danych wymagań wstępnych hello są białej. Aby uzyskać informacje, zobacz [wskazówki dotyczące grupy zabezpieczeń sieci](https://aka.ms/a2a-nsg-guidance).

### <a name="fix-hello-problem"></a>Rozwiąż hello problem
toowhitelist [hello wymagane adresy URL](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) lub hello [wymagane zakresy IP](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), wykonaj kroki hello hello [sieci wytycznych](site-recovery-azure-to-azure-networking-guidance.md).

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Nie znaleziono hello maszyny (kod błędu 150039) dysku

Nowy dysk dołączony toohello, który musi zostać zainicjowany maszyny Wirtualnej.

**Kod błędu:** | **Możliwe przyczyny** | **Zalecenia**
--- | --- | ---
150039<br></br>**Komunikat**: dysk danych platformy Azure (DiskName) (DiskURI) numer jednostki logicznej (LUN) (LUNValue) nie jest zmapowane tooa odpowiedniego dysku raportowany przez w hello maszynę Wirtualną, która ma hello tę samą wartość jednostki LUN. | -Nowy dysk danych zostało dołączone toohello maszyny Wirtualnej, ale nie został on zainicjowany.</br></br>-hello dysk danych wewnątrz hello maszyny Wirtualnej nie zgłasza poprawnie hello wartość jednostki LUN na które hello dysk był dołączony toohello maszyny Wirtualnej.| Upewnij się, że dyski danych hello są inicjowane, a następnie ponów operację hello.</br></br>W systemie Windows: [Attach i zainicjować nowego dysku](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</br></br>Dla systemu Linux: [inicjowania dysku danych w systemie Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

### <a name="fix-hello-problem"></a>Rozwiąż hello problem
Upewnij się, że dyski danych hello został zainicjowany, a następnie ponów operację hello:

- W systemie Windows: [Attach i zainicjować nowego dysku](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).
- Dla systemu Linux: [inicjowania dysku danych w systemie Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

Jeśli hello problem będzie się powtarzać, skontaktuj się z pomocy technicznej.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>Toosee hello maszyny Wirtualnej platformy Azure dla wyboru "Włącz replikacji"

Maszyna wirtualna platformy Azure do wyboru w może nie być wyświetlana [włączyć replikację: krok 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines). Ten problem może być ukończenia konfiguracji usługi Site Recovery toostale na powitania maszyny Wirtualnej platformy Azure. Witaj przestarzałą konfigurację może pozostać na maszynie Wirtualnej platformy Azure hello w następujących przypadkach:

- Możesz włączyć replikację dla maszyny Wirtualnej Azure hello przy użyciu usługi Site Recovery, a następnie usuwany magazynu usługi Site Recovery hello bez jawnie wyłączenie replikacji na powitania maszyny Wirtualnej.
- Możesz włączyć replikację dla maszyny Wirtualnej Azure hello przy użyciu usługi Site Recovery, a następnie usuwany hello grupę zasobów zawierającą magazyn usługi Site Recovery hello bez jawnie wyłączenie replikacji na powitania maszyny Wirtualnej.

### <a name="fix-hello-problem"></a>Rozwiąż hello problem

Można użyć [Usuń stare skryptu konfiguracji ASR](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) i usuwanie starych konfiguracji usługi Site Recovery hello na powitania maszyny Wirtualnej platformy Azure. Powinny pojawić się hello maszyny Wirtualnej w ramach [włączyć replikację: krok 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) po usunięciu hello przestarzałą konfigurację.


## <a name="next-steps"></a>Następne kroki
[Replikowanie maszyn wirtualnych platformy Azure](site-recovery-replicate-azure-to-azure.md)
