---
title: "Kopia zapasowa Azure: spójnych z aplikacją kopii zapasowych maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft"
description: "Użyj skryptów tooguarantee kopie zapasowe spójnych z aplikacją tooAzure, maszyn wirtualnych systemu Linux. skrypty Hello są stosowane tylko tooLinux VMs we wdrożeniu usługi Resource Manager; skrypty Hello nie stosuj tooWindows maszyn wirtualnych lub wdrożenia Menedżera usług. Ten artykuł przedstawia hello kroki konfigurowania skryptów hello, w tym Rozwiązywanie problemów."
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: "kopii zapasowej całej aplikacji. spójnych z aplikacją kopii zapasowej maszyny Wirtualnej platformy Azure; Kopii zapasowej maszyny Wirtualnej systemu Linux. Kopia zapasowa Azure"
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Spójnych z aplikacją kopii zapasowej maszyn wirtualnych systemu Linux platformy Azure (wersja zapoznawcza)

Ten artykuł zawiera informacje o hello skryptu wstępne systemu Linux i skrypt po framework i jak mogą być używane tootake spójnych z aplikacją kopii zapasowych maszyn wirtualnych systemu Linux platformy Azure.

> [!Note]
> framework skryptów przed i po skryptu Hello jest obsługiwana tylko dla maszyn wirtualnych wdrożonych przez Menedżera zasobów Azure systemu Linux. Skrypty w celu zachowania spójności aplikacji nie są obsługiwane dla maszyn wirtualnych wdrożonych programu Service Manager lub maszyn wirtualnych systemu Windows.
>

## <a name="how-hello-framework-works"></a>Jak działa hello framework

Witaj framework zapewnia toorun opcji niestandardowych skryptów przed i po skrypty podczas tworzenia migawki maszyny Wirtualnej. Wstępne skrypty są uruchamiane tuż przed zająć hello migawki maszyny Wirtualnej, a po skrypty są uruchamiane natychmiast po hello migawki maszyny Wirtualnej. Dzięki temu podczas tworzenia migawki maszyny Wirtualnej hello toocontrol elastyczność aplikacji i środowiska.

W tym scenariuszu jest ważne tooensure spójnych z aplikacją kopii zapasowej maszyny Wirtualnej. Skrypt przed Hello można wywołać hello tooquiesce interfejsów API natywnych aplikacji systemu IOs i opróżnienia dysku toohello zawartości w pamięci. Dzięki temu, że migawka hello jest spójne z aplikacjami (oznacza to, że aplikacja hello pojawia się podczas rozruchu maszyny Wirtualnej hello wykonywane po przywróceniu). Skrypt po może być używane toothaw hello systemu IOs. Robi to przy użyciu interfejsów API natywnych aplikacji, dzięki czemu aplikacja hello można wznowić wykonywania normalnych operacji post-VM migawki.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>Kroki tooconfigure skryptów przed i po skryptu

1. Zaloguj się w hello głównego użytkownika toohello maszyny Wirtualnej systemu Linux, który ma tooback się.

2. Pobierz **VMSnapshotScriptPluginConfig.json** z [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig), a następnie skopiować go toohello **azure/etc/** folderu na wszystkich maszynach wirtualnych hello zamierza tooback się. Utwórz hello **/etc/azure** katalogu, jeśli nie istnieje już.

3. Skopiuj hello skryptów przed i po skrypt aplikacji na powitania wszystkich maszyn wirtualnych, które planujesz tooback w górę. Możesz skopiować lokalizacji tooany skrypty hello na powitania maszyny Wirtualnej. Należy się tooupdate hello pełną ścieżkę hello plików skryptów w hello **VMSnapshotScriptPluginConfig.json** pliku.

4. Upewnij się, hello następujących uprawnień dla tych plików:

   - **VMSnapshotScriptPluginConfig.json**: uprawnienie "600." Na przykład tylko użytkownika "root" powinien mieć plik toothis uprawnienia "Odczyt" i "write" i żaden użytkownik nie ma uprawnienia "execute".

   - **Plik skryptu przed**: uprawnienie "700."  Na przykład tylko "root" użytkownik powinien mieć "do odczytu", "write" i "execute" pliku toothis uprawnienia.
  
   - **Skrypt po** uprawnienia "700." Na przykład tylko "root" użytkownik powinien mieć "do odczytu", "write" i "execute" pliku toothis uprawnienia.

   > [!Important]
   > Witaj framework zapewnia użytkownikom dużo energii. Jest ważne, czy jest bezpieczne i że tylko użytkownika "root" zawiera pliki JSON i skrypt toocritical dostępu.
   > Jeśli nie są spełnione wymagania poprzedniej hello, hello skrypt nie działa. Powoduje to kopia zapasowa spójna awaria/systemu plików.
   >

5. Skonfiguruj **VMSnapshotScriptPluginConfig.json** zgodnie z opisem w tym miejscu:
    - **pluginName**: pozostaw to pole jest lub skryptów mogą nie działać zgodnie z oczekiwaniami.

    - **preScriptLocation**: Podaj pełną ścieżkę hello skryptu przed hello na powitania to jest toobe będzie kopii zapasowej maszyny Wirtualnej.

    - **postScriptLocation**: Podaj pełną ścieżkę hello skryptu po hello na powitania to jest toobe będzie kopii zapasowej maszyny Wirtualnej.

    - **preScriptParams**: Podaj hello następujące parametry opcjonalne wymagające toobe przekazany toohello wstępne skryptu. Wszystkie parametry powinna być w cudzysłowie, a powinien być oddzielonych przecinkami, jeśli istnieje wiele parametrów.

    - **postScriptParams**: Podaj hello opcjonalnymi parametrami, które wymagają toobe przekazany toohello skryptu po. Wszystkie parametry powinna być w cudzysłowie, a powinien być oddzielonych przecinkami, jeśli istnieje wiele parametrów.

    - **preScriptNoOfRetries**: ustawić hello liczbę skryptu przed hello należy wykonać ponownie razie błędu przed zakończeniem. Zero oznacza, że tylko jedna próba i nie ponownych prób w przypadku awarii.

    - **postScriptNoOfRetries**: ustawić hello liczbę hello skryptu po powinno być ponowione w razie błędu przed zakończeniem. Zero oznacza, że tylko jedna próba i nie ponownych prób w przypadku awarii.
    
    - **LimitCzasuWSekundach**: Określ poszczególnych limitów czasu dla hello skryptów przed i po skryptu hello.

    - **continueBackupOnFailure**: Ustaw tę wartość za**true** jeśli mają kopia zapasowa Azure toofall tooa wstecz spójne/awarii spójne kopia zapasowa systemu plików w przypadku skryptu przed lub po wykonaniu script kończy się niepowodzeniem. Ustawienie zbyt**false** hello kopii zapasowych w przypadku błędu skryptu (z wyjątkiem przypadków, gdy masz jednego dysku maszyny Wirtualnej wypada ponownie toocrash spójnych kopii zapasowej niezależnie od tego ustawienia) kończy się niepowodzeniem.

    - **fsFreezeEnabled**: Określ, czy Linux fsfreeze powinna być wywoływana podczas tworzenia migawki maszyny Wirtualnej hello tooensure spójności systemu plików. Zaleca się pozostawienie to ustawienie, ustaw zbyt**true** chyba, że aplikacja ma zależności wyłączenie fsfreeze.

6. framework skryptu Hello jest teraz skonfigurowany. Jeśli hello kopii zapasowej maszyny Wirtualnej jest już skonfigurowana, następnej kopii zapasowej hello wywołuje hello skryptów i wyzwala spójnych z aplikacją kopii zapasowej. Jeśli nie skonfigurowano kopii zapasowej maszyny Wirtualnej hello, skonfiguruj ją za pomocą [kopię zapasową Magazyny usług tooRecovery maszyn wirtualnych platformy Azure.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Upewnij się, Dodaj odpowiednie rejestrowania podczas zapisywania w skrypcie przed i po skryptu i przejrzyj wszelkie problemy skryptu toofix dzienniki Twojego skryptu. Jeśli nadal występują problemy z uruchamianiem skryptów, zapoznaj się toohello w poniższej tabeli, aby uzyskać więcej informacji.

| Błąd | Komunikat o błędzie | Zalecane działanie |
| ------------------------ | -------------- | ------------------ |
| Wstępnie ScriptExecutionFailed |Hello skryptu przed zwróciło błąd, aby kopia zapasowa może nie być spójnych z aplikacją. | Sprawdź dzienniki awarii hello opis problemu hello toofix skryptu.|  
|   Post ScriptExecutionFailed |    skrypt po Hello zwrócił błąd, który może mieć wpływ na stan aplikacji. |  Sprawdź dzienniki awarii hello opis problemu hello toofix skryptu i sprawdź stan aplikacji hello. |
| Wstępnie ScriptNotFound |  Hello wstępne skryptu nie została znaleziona w lokalizacji hello, która została określona w hello **VMSnapshotScriptPluginConfig.json** pliku konfiguracji. | Upewnij się, że to wstępne skryptu musi być obecny przy hello ścieżki określonej w hello config tooensure spójnych z aplikacją wykonywanie kopii zapasowej plików.|
| Post ScriptNotFound | Witaj po skryptu nie można znaleźć lokalizacji hello jest określona w hello **VMSnapshotScriptPluginConfig.json** pliku konfiguracji. | Upewnij się, że to po skryptu musi być obecny przy hello ścieżki określonej w hello config tooensure spójnych z aplikacją wykonywanie kopii zapasowej plików.|
| IncorrectPluginhostFile | Witaj **Pluginhost** pliku, który zawiera hello VmSnapshotLinux rozszerzenia, jest uszkodzony, dlatego nie można uruchomić skryptu przed i po skryptu i hello kopii zapasowej nie będzie spójnych z aplikacją.   | Odinstaluj hello **VmSnapshotLinux** rozszerzenia, a zostaną automatycznie zainstalowane ponownie z hello następnej kopii zapasowej toofix hello problem. |
| IncorrectJSONConfigFile | Witaj **VMSnapshotScriptPluginConfig.json** plik jest nieprawidłowy, dlatego przed skryptu i nie można uruchomić skrypt po hello kopii zapasowej nie będzie spójnych z aplikacją. | Pobierz kopię hello z [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) i skonfiguruj go ponownie. |
| InsufficientPermissionforPre skryptu | Uruchamianie skryptów, użytkownika "root" powinny być hello właściciela pliku hello i hello plik powinien mieć uprawnienia "700" (to znaczy powinny mieć tylko "właściciela" "do odczytu", "write" i "uprawnienia do wykonywania"). | Upewnij się, użytkownik "root" hello "właściciela" hello pliku skryptu, a czy tylko "właściciela" ma "", "write" i "execute" uprawnienia odczytu. |
| InsufficientPermissionforPost skryptu | Uruchamianie skryptów, użytkownika głównego powinny być hello właściciela pliku hello i hello plik powinien mieć uprawnienia "700" (to znaczy powinny mieć tylko "właściciela" "do odczytu", "write" i "uprawnienia do wykonywania"). | Upewnij się, użytkownik "root" hello "właściciela" hello pliku skryptu, a czy tylko "właściciela" ma "", "write" i "execute" uprawnienia odczytu. |
| Wstępnie ScriptTimeout | Witaj wykonanie skryptu spójnych z aplikacją wstępne kopii zapasowej hello przekroczyła limit czasu. | Sprawdź hello skryptu i zwiększyć limit czasu hello w hello **VMSnapshotScriptPluginConfig.json** pliku znajdującego się na **/etc/azure**. |
| Post ScriptTimeout | wykonanie Hello hello spójnych z aplikacją skryptu po kopii zapasowej został przekroczony. | Sprawdź hello skryptu i zwiększyć limit czasu hello w hello **VMSnapshotScriptPluginConfig.json** pliku znajdującego się na **/etc/azure**. |

## <a name="next-steps"></a>Następne kroki
[Skonfiguruj Magazyn usług odzyskiwania tooa kopii zapasowej maszyny Wirtualnej](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
