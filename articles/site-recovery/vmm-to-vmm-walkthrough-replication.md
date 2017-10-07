---
title: "aaaSet się zasady replikacji dla lokacji dodatkowej tooa replikacji funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooset politykę dla maszyny Wirtualnej funkcji Hyper-V replikacji tooa VMM dodatkowej lokacji z usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>Krok 8: Konfigurowanie zasad replikacji

Po skonfigurowaniu [mapowania sieci](vmm-to-vmm-walkthrough-network-mapping.md), użyj tego artykułu tooset się zasady replikacji dla funkcji Hyper-V maszyny wirtualnej (VM) replikacji tooa lokacji dodatkowej, przy użyciu [usługi Azure Site Recovery](site-recovery-overview.md).

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Przed rozpoczęciem

- Po utworzeniu zasad replikacji wszystkich hostów przy użyciu zasad hello musi mieć hello sam system operacyjny. Witaj chmury VMM może zawierać hosty funkcji Hyper-V z różnymi wersjami systemu Windows Server, ale w takim przypadku należy wielu skojarzeń zasad replikacji.
- Można wykonywać hello o początkowej replikacji w trybie offline.

## <a name="configure-replication-settings"></a>Konfigurowanie ustawień replikacji

1. Kliknij przycisk toocreate nowe zasady replikacji, **przygotowanie infrastruktury** > **ustawienia replikacji** > **+ Utwórz i skojarz**.

    ![Sieć](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. W obszarze **Utwórz i skojarz zasady** określ nazwę zasad. Witaj źródłowy i docelowy typ powinien być **funkcji Hyper-V**.
3. W **host funkcji Hyper-V w wersji**, wybierz system operacyjny jest uruchomiona na hoście hello.
4. W **typ uwierzytelniania** i **port uwierzytelniania**, określ, jak uwierzytelnianie ruchu między hello podstawowego i serwery hosta funkcji Hyper-V odzyskiwania. Wybierz **certyfikatu** w przypadku braku działającego środowiska protokołu Kerberos. Usługa Azure Site Recovery automatycznie skonfiguruje certyfikatów do uwierzytelniania protokołu HTTPS. Nie trzeba toodo niczego ręcznie. Domyślnie port 8083 i 8084 (dla certyfikatów) będą otwierane w hello zapory systemu Windows na serwerach hostów funkcji Hyper-V hello. Jeśli wybierzesz **Kerberos**, biletu protokołu Kerberos będzie używany do wzajemnego uwierzytelniania hello serwerów hosta. Należy pamiętać, że to ustawienie dotyczy tylko serwerów hosta funkcji Hyper-V z systemem Windows Server 2012 R2.
5. W **częstotliwość kopiowania**, określić, jak często dane różnicowe tooreplicate po replikacji początkowej hello (co 30 sekund, 5 lub 15 minut).
6. W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo będą hello okna przechowywania dla każdego punktu odzyskiwania. Chronione maszyny można odzyskać tooany punktu, w tym oknie.
7. W **częstotliwość migawek spójności aplikacji**, określ, jak często (1 – 12 godzin) punkty odzyskiwania zawierające migawki spójne z aplikacjami są tworzone. Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie. Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki. Włącz migawki spójne z aplikacjami, wpłynie na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych. Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.
8. W **kompresję transferu danych**, określ, czy można kompresować replikowane dane przesyłane.
9. Wybierz **Usuń replikę maszyny Wirtualnej**, powinien zostać usunięty toospecify, który hello maszyny wirtualnej repliki, Jeśli wyłączysz ochrona powitalnych źródłowej maszyny Wirtualnej. Jeśli to ustawienie zostanie włączone po wyłączeniu ochrony dla źródła hello maszyny Wirtualnej zostanie usunięte z konsoli usługi Site Recovery hello, ustawienia usługi Site Recovery dla hello VMM z konsoli programu VMM hello, i repliki hello jest usunięte.
10. W **metodę replikacji początkowej**, jeśli przeprowadzasz replikację za pośrednictwem sieci hello, określ, czy toostart hello replikacji początkowej lub zaplanowania jej. toosave przepustowość sieci, może być tooschedule ją poza najbardziej obciążonymi godzinami. Następnie kliknij przycisk **OK**.

     ![Zasady replikacji](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. Podczas tworzenia nowych zasad jest ona automatycznie skojarzona z hello chmury VMM. W **zasad replikacji**, kliknij przycisk **OK**. Dodatkowe chmury VMM (oraz hello maszyn wirtualnych w nich) można skojarzyć z zasadami replikacji w **replikacji** > nazwa_zasady > **Skojarz chmurę VMM**.

     ![Zasady replikacji](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a>Przygotuj się do początkowej replikacji offline

Możesz to zrobić hello kopii początkowe dane replikacji w trybie offline. Można to przygotować w następujący sposób:

* Na powitania serwera źródłowego można określić lokalizacji, z których hello odbędzie się eksportowania danych. Pełna kontrola przypisać uprawnienia NTFS i udziału toohello usługi VMM w ścieżce eksportu hello. Na serwerze docelowym hello można określić lokalizacji, z której zaimportować hello danych zostanie przeprowadzona. Przypisz hello te same uprawnienia, w tym ścieżki importu.
* Jeśli hello importowania lub eksportowania, ścieżka jest udostępniana, przypisz członkostwo w grupie administratora, użytkownik zaawansowany, Operator drukowania lub Operator serwera na powitania konto usługi VMM na komputerze zdalnym hello na które hello udostępnionych znajduje się.
* Jeśli używasz Uruchom jako konta tooadd hosty, na powitania zaimportować i wyeksportuj ścieżki, przypisz odczytu Odczyt i zapis toohello konta Uruchom jako w programie VMM.
* Witaj importowanie i eksportowanie udziałów nie powinien znajdować się na dowolnym komputerze używany jako serwer hosta funkcji Hyper-V, ponieważ konfiguracja ze sprzężeniem zwrotnym nie jest obsługiwana przez funkcję Hyper-V.
* W usłudze Active Directory na każdym serwerze hosta funkcji Hyper-V, który zawiera maszyny wirtualne tooprotect, włączyć i skonfigurować delegowanie ograniczone tootrust hello komputerami zdalnymi na które hello importowanie i eksportowanie ścieżek znajdują się, w następujący sposób:
  1. Na kontrolerze domeny hello Otwórz **użytkownicy usługi Active Directory i komputery**.
  2. W drzewie konsoli powitania kliknij **DomainName** > **komputerów**.
  3. Nazwa serwera hosta funkcji Hyper-V powitania kliknij prawym przyciskiem myszy > **właściwości**.
  4. Na powitania **delegowania** , kliknij pozycję **Ufaj temu komputerowi w delegowania toospecified tylko usług**.
  5. Kliknij przycisk **Użyj dowolnego protokołu uwierzytelniania**.
  6. Kliknij przycisk **dodać** > **użytkownicy i komputery**.
  7. Nazwa typu hello hello komputerze, który obsługuje ścieżkę eksportu hello > **OK**. Z listy dostępnych usług hello, naciśnij i przytrzymaj klawisz CTRL hello, a następnie kliknij przycisk **cifs** > **OK**. Powtórz hello nazwę komputera hello tej ścieżki importu hello hostów. Powtórz w razie potrzeby dodatkowe serwery hosta funkcji Hyper-V.



## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 9: Włączanie replikacji](vmm-to-vmm-walkthrough-enable-replication.md).
