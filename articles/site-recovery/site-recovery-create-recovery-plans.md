---
title: "aaaCreate plany odzyskiwania dla trybu failover i odzyskiwania w usłudze Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toocreate i dostosowywać plany odzyskiwania w usłudze Azure Site Recovery, toofail za pośrednictwem i odzyskiwania maszyn wirtualnych i serwerów fizycznych"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>Tworzenie planów odzyskiwania


Ten artykuł zawiera informacje na temat tworzenia i dostosowywania planów odzyskiwania w [usługi Azure Site Recovery](site-recovery-overview.md).

Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

 Utwórz hello toodo planów odzyskiwania po:

* Definiowanie grup komputerów, które w tryb failover ze sobą, a następnie uruchom ze sobą.
* Model zależności między komputerami, grupując je do odzyskiwania Zaplanuj grupy. Na przykład toofail za pośrednictwem i wyświetlić określonej aplikacji, wszystkie maszyny wirtualne powitania dla tej aplikacji na powitania grupy tej samej grupie planu odzyskiwania.
* Uruchom tryb failover. Można uruchomić testu, planowane, ani nieplanowane przełączenie awaryjne, w ramach planu odzyskiwania.


## <a name="create-a-recovery-plan"></a>Tworzenie planu odzyskiwania

1. Kliknij przycisk **planów odzyskiwania** > **utworzenie planu odzyskiwania**.
   Określ nazwę hello planu odzyskiwania, a źródłowa i docelowa. Lokalizacja źródła Hello musi mieć maszyn wirtualnych, które są włączone dla trybu failover i odzyskiwania.

    - Replikacja tooVMM VMM, wybierz **typ źródła** > **VMM**i hello źródłowych i docelowych serwerów programu VMM. Kliknij przycisk **funkcji Hyper-V** toosee chmury, które są chronione.
    - VMM tooAzure, wybierz **typ źródła** > **VMM**.  Witaj wybierz źródłowy serwer VMM i **Azure** jako cel hello.
    - Dla funkcji Hyper-V tooAzure replikacji (bez VMM), wybierz **typ źródła** > **lokacji funkcji Hyper-V**. Wybierz hello lokacji jako źródło hello i **Azure** jako cel hello.
    - Dla maszyny Wirtualnej VMware lub fizycznego lokalnego serwera tooAzure, wybierz serwer konfiguracji jako źródło hello i **Azure** jako cel hello.
    - Azure tooAzure plan odzyskiwania wybierz region platformy Azure jako źródło hello i dodatkowej region platformy Azure jako cel hello. Witaj dodatkowej regiony platformy Azure są tylko maszyny wirtualne toowhich są chronione.
2. W **wybierz maszyny wirtualne**, wybierz maszyny wirtualne hello (lub grupa replikacji) mają tooadd toohello domyślnej grupy (Grupa 1) w planie odzyskiwania hello.

## <a name="customize-and-extend-recovery-plans"></a>Dostosowywanie i rozszerzanie planów odzyskiwania

Można dostosować i rozszerzyć planów odzyskiwania:

- **Dodaj nowe grupy**— Dodawanie grup (up tooseven) planu odzyskiwania dodatkowe toohello grupy domyślnej, a następnie dodaj więcej maszyny lub replikacji grupy toothose odzyskiwania planu grupy. Grupy są numerowane kolejno hello je dodać. Maszyny wirtualnej lub grupy replikacji tylko mogą zostać włączone w grupie planu odzyskiwania jednego.
- **Dodaj akcję ręczną**— można dodać ręczne akcje, które są uruchamiane przed lub po grupie planu odzyskiwania. Po uruchomieniu planu odzyskiwania hello przestaje w momencie hello jaką dodaje hello akcji ręcznej. Okno dialogowe monituje toospecify zakończenie akcji ręcznej hello.
- **Dodawanie skryptu**— można dodać skryptów uruchamianych przed lub po grupie planu odzyskiwania. Po dodaniu skrypt dodaje nowy zestaw działań hello grupy. Na przykład, zostanie utworzony zestaw kroków wstępne 1 grupy o nazwie hello: Grupa 1: wstępne czynności. Wszystkie kroki przed będzie wyświetlane w tym zestawie. Skrypt można dodać na powitania lokacji głównej, jeśli serwer VMM wdrożone.
- **Dodaj elementy runbook Azure**— można rozszerzyć plany odzyskiwania z elementów runbook platformy Azure. Na przykład tooautomate zadań lub toocreate pojedynczy krok odzyskiwania. [Dowiedz się więcej](site-recovery-runbook-automation.md).

## <a name="add-scripts"></a>Dodawanie skryptów

Można użyć skryptów środowiska PowerShell w planów odzyskiwania.

 - Upewnij się, że skrypty używać bloków try-catch, tak aby bezpiecznie obsługi wyjątków hello.
    - W przypadku wyjątku w skrypcie hello przestaje działać i zadań hello pokazuje nie powiodło się.
    - Jeśli wystąpi błąd, pozostała część hello skrypt nie działa.
    - Jeśli błąd wystąpi po uruchomieniu nieplanowanego trybu failover, nadal hello planu odzyskiwania.
    - Jeśli wystąpi błąd podczas uruchamiania planowanego trybu failover, zatrzymuje hello planu odzyskiwania. Należy toofix hello skryptu, sprawdź, czy działa zgodnie z oczekiwaniami, a następnie uruchom ponownie planu odzyskiwania hello.
- Witaj polecenia Write-Host nie działa w skryptu planu odzyskiwania i hello skrypt zakończy się niepowodzeniem. dane wyjściowe toocreate, utworzyć skrypt serwera proxy, który z kolei uruchamia skrypt głównego. Upewnij się, że wszystkie dane wyjściowe jest przekazywany w potoku się przy użyciu hello >> polecenia.
  * Upłynął limit czasu skryptu Hello Jeśli nie zwraca w 600 sekund.
  * Jeśli wszystko jest zapisywane tooSTDERR, skrypt hello jest klasyfikowany zgodnie z nie powiodło się. Te informacje są wyświetlane w szczegółach wykonywania skryptu hello.

Jeśli używasz programu VMM w ramach wdrożenia:

* Skrypty w planie odzyskiwania są uruchamiane w kontekście hello hello konto usługi VMM. Upewnij się, że to konto ma uprawnienia do odczytu dla hello udziału zdalnego, na których hello zlokalizowany jest skrypt. Testowanie toorun skryptu hello na powitania poziom uprawnień konta usługi programu VMM.
* Poleceń cmdlet programu VMM są dostarczane w moduł programu Windows PowerShell. Moduł Hello jest zainstalowany, po zainstalowaniu konsoli VMM hello. Może być załadowany do skryptu, za pomocą następującego polecenia w skrypcie hello hello:
   - Import-Module-Name virtualmachinemanager. [Dowiedz się więcej](https://technet.microsoft.com/library/hh875013.aspx).
* Upewnij się, że co najmniej jednego serwera biblioteki w danym wdrożeniu programu VMM. Domyślnie program hello ścieżki udziału bibliotecznego na serwerze VMM znajduje się lokalnie na powitania serwera VMM, nazwą folderu hello MSCVMMLibrary.
    * Jeśli Twoje ścieżki udziału bibliotecznego jest zdalne (lub lokalnym, ale nie są udostępniane MSCVMMLibrary), skonfiguruj udział hello w następujący sposób (przy użyciu \\libserver2.contoso.com\share\ jako przykład):
      * Otwórz hello Edytor rejestru i przejdź zbyt**Recovery\Registration lokacji HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure**.
      * Edytowanie wartości hello **ScriptLibraryPath** i umieszczenie go w formie \\libserver2.contoso.com\share\. Określ hello pełną nazwę FQDN. Podaj lokalizację udziału toohello uprawnienia.
      * Należy przetestować skrypt hello przy użyciu konta użytkownika, który ma hello takie same uprawnienia jak hello VMM konta usługi. Sprawdza, że autonomiczny przetestowany skrypty uruchamiane w hello sam sposób, jak zostaną planów odzyskiwania. Na serwerze VMM hello Ustaw toobypass zasad wykonywania hello w następujący sposób:
        * Otwórz konsolę programu Windows PowerShell 64-bitowych hello korzystając z podwyższonym poziomem uprawnień.
        * Typ: **obejścia Set-executionpolicy**. [Dowiedz się więcej](https://technet.microsoft.com/library/ee176961.aspx).

## <a name="add-a-script-or-manual-action-tooa-plan"></a>Dodaj skrypt lub plan tooa działania ręczne

Po utworzeniu dodawania maszyn wirtualnych lub tooit grup replikacji i utworzono hello plan można dodać grupę planu odzyskiwania domyślną toohello skryptu.

1. Otwórz hello planu odzyskiwania.
2. Kliknij element hello **krok** , a następnie kliknij przycisk **skryptu** lub **Akcja ręczna**.
3. Określ, czy skrypt hello tooadd toowant lub akcji przed lub po hello wybrany element. Użyj hello **Przenieś w górę** i **Przenieś w dół** przyciski pozycji hello toomove hello skryptu w górę lub w dół.
4. Jeśli dodasz skryptu programu VMM, wybierz **pracy awaryjnej tooVMM skryptu**. W **ścieżka skryptu**, typ hello ścieżki względnej toohello udziału. W poniższym przykładzie VMM hello, określ ścieżkę hello: **\RPScripts\RPScript.PS1**.
5. Po dodaniu usługi Automatyzacja Azure Uruchom książki Określ konto usługi Automatyzacja Azure hello, w których hello runbook to skrypt odpowiednich elementów runbook platformy Azure hello zlokalizować i wybierz opcję.
6. Tryb failover planu odzyskiwania hello, czy skrypt hello toomake działa zgodnie z oczekiwaniami.


### <a name="add-a-vmm-script"></a>Skrypt programu VMM

Lokację źródłową programu VMM można utworzyć skrypt na serwerze VMM hello i dołącz ją do planu odzyskiwania.

1. Utwórz nowy folder w udziale biblioteki hello. Na przykład \<nazwa > \MSSCVMMLibrary\RPScripts. Umieść go w źródle hello i VMM serwery docelowe.
2. Utwórz skrypt hello (na przykład RPScript), a następnie sprawdź, czy działa on zgodnie z oczekiwaniami.
3. Umieść skrypt hello w lokalizacji hello \<nazwa > \MSSCVMMLibrary na serwerach VMM hello źródłowych i docelowych.


## <a name="next-steps"></a>Następne kroki

[Dowiedz się więcej](site-recovery-failover.md) dotyczące uruchamiania trybu failover.
