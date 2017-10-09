---
title: "aaaBack zapasowej obciążeń programu DPM tooAzure klasyczny portal | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toobacking zapasową serwerów DPM przy użyciu usługi Kopia zapasowa Azure hello"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: System Center Data Protection Manager, programu data protection manager, kopii zapasowych programu dpm
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Przygotowywanie tooback się tooAzure obciążenia za pomocą programu DPM
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Serwer kopii zapasowej systemu Azure (klasyczne)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (klasyczne)](backup-azure-dpm-introduction-classic.md)
>
>

Ten artykuł zawiera wprowadzenie toousing kopia zapasowa Microsoft Azure tooprotect System Center Data Protection Manager (DPM) serwerów i obciążeń. Przeczytaj go, będzie zrozumieć:

* Jak działa kopii zapasowej serwera Azure DPM
* Witaj wymagania wstępne tooachieve smooth środowisko tworzenia kopii zapasowej
* Witaj typowych błędów napotkanych i w jaki sposób toodeal z nimi
* Obsługiwane scenariusze

System Center DPM tworzy kopie zapasowe danych plików i aplikacji. TooDPM kopię zapasową danych można przechowywane na taśmie na dysku, lub kopię zapasową tooAzure w usłudze Kopia zapasowa Microsoft Azure. Program DPM współdziała z usługi Kopia zapasowa Azure w następujący sposób:

* **Program DPM wdrożony jako fizycznego serwera lub lokalnej maszyny wirtualnej** — Jeśli program DPM wdrożony jako serwera fizycznego lub lokalnej maszyny wirtualnej funkcji Hyper-V można utworzyć kopię zapasową danych tooan kopia zapasowa Azure dodatkowo magazyn toodisk i kopii zapasowej na taśmie.
* **Program DPM wdrożony jako maszyna wirtualna platformy Azure** — z programu System Center 2012 R2 z aktualizacją Update 3 programu DPM można wdrożyć jako maszynę wirtualną platformy Azure. Jeśli program DPM wdrożony jako maszyna wirtualna platformy Azure, które można tworzyć kopie zapasowe danych tooAzure dysków dołączonych do maszyny wirtualnej platformy Azure programu DPM toohello lub dzięki tworzeniu kopii zapasowej tooan magazynu usługi Kopia zapasowa Azure można odciążyć magazyn danych hello.

## <a name="why-backup-your-dpm-servers"></a>Dlaczego warto utworzyć kopię zapasową serwerów DPM?
korzyści biznesowe Hello przy użyciu usługi Kopia zapasowa Azure do wykonywania kopii zapasowych serwerów programu DPM obejmują:

* Lokalnego wdrożenia programu DPM kopia zapasowa Azure służy jako alternatywne termin toolong tootape wdrożenia.
* Dla wdrożeń programu DPM na platformie Azure kopia zapasowa Azure umożliwia toooffload magazynu z hello dysku platformy Azure, umożliwiając tooscale się starsze dane są przechowywane w usłudze Kopia zapasowa Azure i nowych danych na dysku.

## <a name="how-does-dpm-server-backup-work"></a>Jak działa kopii zapasowej serwera DPM
tooback maszyny wirtualnej, najpierw migawek w momencie hello danych jest wymagana. Hello kopia zapasowa Azure Usługa inicjuje hello zadanie tworzenia kopii zapasowej na powitania zaplanowana godzina, a wyzwalacze hello tootake zapasowy numer wewnętrzny migawki. współrzędne zapasowy numer wewnętrzny Hello z hello gościa VSS usługi tooachieve spójności i wywołuje hello interfejsu API migawki obiektu blob z hello usługi Azure Storage, po przekroczeniu spójności. Jest to wykonywane tooget migawki spójne hello dyski maszyny wirtualnej hello, bez konieczności tooshut go w dół.

Po podjęciu hello migawki, hello dane są przesyłane przy magazynu kopii zapasowych hello kopia zapasowa Azure usługa toohello. Usługa Hello odpowiada on za identyfikacji i transferowanie tylko bloki hello, które zostały zmienione od ostatniej kopii zapasowej hello wprowadzania efektywne hello kopii zapasowych magazynu i sieci. Po ukończeniu transferu danych hello hello migawka zostanie usunięta i utworzenia punktu odzyskiwania. Tego punktu odzyskiwania można wyświetlić w hello klasycznego portalu Azure.

> [!NOTE]
> Dla maszyn wirtualnych systemu Linux tylko plików kopii zapasowej spójnej jest możliwe.
>
>

## <a name="prerequisites"></a>Wymagania wstępne
Przygotuj tooback kopia zapasowa Azure zapasowej danych programu DPM w następujący sposób:

1. **Utwórz magazyn kopii zapasowych**. Jeśli nie utworzono magazyn kopii zapasowych w ramach subskrypcji, zobacz hello Azure portalu wersja tego artykułu - [przygotowanie tooback się tooAzure obciążenia za pomocą programu DPM](backup-azure-dpm-introduction.md).

  > [!IMPORTANT]
  > Uruchamianie 2017 marca, można dłużej korzystać magazyny kopii zapasowych w klasycznym portalu toocreate hello.
  > Teraz można uaktualnić Twoje Magazyny usług tooRecovery magazynów kopii zapasowych. Aby uzyskać więcej informacji, zobacz artykuł hello [uaktualnienia tooa magazynu kopii zapasowej, Magazyn usług odzyskiwania i](backup-azure-upgrade-backup-to-recovery-services.md). Firma Microsoft zachęca tooupgrade Magazyny usług tooRecovery magazyny kopii zapasowych.<br/> Po 15 października 2017 nie można użyć magazyny kopii zapasowych toocreate środowiska PowerShell. **Do 1 listopada 2017 r.**:
  >- Wszystkie pozostałe magazyny kopii zapasowych zostanie automatycznie uaktualniony tooRecovery Magazyny usług.
  >- Użytkownik nie będzie możliwe tooaccess danych kopii zapasowych w portalu klasycznym hello. Zamiast tego użyj hello Azure tooaccess portalu tej kopii zapasowej w Magazyny usług odzyskiwania.
  >

2. **Pobierz poświadczenia magazynu** — w usłudze Kopia zapasowa Azure certyfikat zarządzania hello Przekaż utworzony magazyn toohello.
3. **Zainstaluj hello Agent usługi Kopia zapasowa Azure i Zarejestruj serwer hello** — z usługi Kopia zapasowa Azure, zainstaluj agenta hello na każdym serwerze DPM i Zarejestruj serwer DPM hello w magazynie kopii zapasowych hello.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>Wymagania (i ograniczenia)
* Program DPM może działać jako serwer fizyczny lub maszyny wirtualnej funkcji Hyper-V zainstalowanych w programie System Center 2012 SP1 lub System Center 2012 R2. Mogą również działać jako maszyna wirtualna platformy Azure z programu System Center 2012 R2 z co najmniej programu DPM 2012 R2 Update Rollup 3 lub maszyny wirtualnej systemu Windows w środowisku programu VMWare na nim uruchomione w programie System Center 2012 R2 z pakietem zbiorczym aktualizacji 5.
* Jeśli używasz programu DPM z programu System Center 2012 z dodatkiem SP1, należy zainstalować pakiet zbiorczy aktualizacji 2 dla programu System Center Data Protection Manager z dodatkiem SP1. Jest to wymagane, aby można było zainstalować hello Azure Backup Agent.
* Serwer programu DPM Hello powinien mieć programu Windows PowerShell i .net Framework 4.5 zainstalowane.
* Program DPM można utworzyć kopię zapasową większości obciążeń tooAzure kopii zapasowej. Pełną listę, co ma obsługiwane Zobacz hello kopia zapasowa Azure obsługuje poniższe elementy.
* Nie można odzyskać danych przechowywanych w usłudze Kopia zapasowa Azure z opcją "Kopiuj tootape" hello.
* Konieczne będzie konto platformy Azure z włączoną funkcją kopia zapasowa Azure hello. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Przeczytaj informacje o [cennikiem usługi Kopia zapasowa Azure](https://azure.microsoft.com/pricing/details/backup/).
* Za pomocą usługi Kopia zapasowa Azure wymaga hello Azure Backup Agent toobe zainstalowanych na serwerach hello, który ma tooback w górę. Każdy serwer musi mieć co najmniej 10% hello rozmiar danych hello, która jest tworzona kopia zapasowa, dostępne jako wolnego miejsca w magazynie lokalnym. Na przykład tworzenie kopii zapasowej 100 GB danych wymaga co najmniej 10 GB wolnego miejsca w lokalizacji pliki tymczasowe hello. Gdy hello minimalna wynosi 10%, 15% wolnego miejsca toobe lokalizacji pamięci podręcznej hello jest zalecane.
* Dane będą przechowywane w hello magazynu magazynu Azure. Nie ma limit nie toohello ilość danych, które można tworzyć kopie zapasowe tooan magazynu usługi Kopia zapasowa Azure, ale rozmiar hello źródła danych (na przykład maszyny wirtualnej lub bazy danych) nie powinna przekraczać 54,400 GB.

Kopia zapasowa tooAzure obsługuje następujące typy plików:

* Zaszyfrowane (tylko pełne kopie zapasowe)
* Skompresowane (obsługą przyrostowych kopii zapasowych)
* Rozrzedzone (obsługą przyrostowych kopii zapasowych)
* Skompresowane i rozrzedzone (traktowane jako rozrzedzone)

I te nie są obsługiwane:

* Serwery w systemach plików z uwzględnieniem wielkości liter nie są obsługiwane.
* Twarde linki (pomijane)
* (Pomijane) punkty ponownej analizy
* Zaszyfrowane i skompresowane (pomijane)
* Zaszyfrowane i rozrzedzone (pomijane)
* Skompresowany strumień
* Rozrzedzony strumień

> [!NOTE]
> Od w System Center 2012 DPM z dodatkiem SP1 lub nowszym, można tworzyć kopie zapasowe dużych obciążeń chronionych przez tooAzure programu DPM za pomocą usługi Microsoft Azure Backup.
>
>
