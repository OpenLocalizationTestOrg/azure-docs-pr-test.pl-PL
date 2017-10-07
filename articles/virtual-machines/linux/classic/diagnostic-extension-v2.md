---
title: "aaaMonitoring Maszynę wirtualną z rozszerzenia maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello wydajności hello toomonitor Linux rozszerzenia diagnostycznych i danych diagnostycznych maszyny wirtualnej systemu Linux na platformie Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Użyj hello rozszerzenia diagnostycznych Linux toomonitor hello wydajności i danych diagnostycznych maszyny wirtualnej systemu Linux

W tym dokumencie opisano wersji 2.3 hello rozszerzenia diagnostyczne systemu Linux.

> [!IMPORTANT]
> Ta wersja jest przestarzały i może być nieopublikowane dowolnym momencie po 30 czerwca 2018. Zastąpiono wersji 3.0 lub nowszej. Aby uzyskać więcej informacji, zobacz hello [dokumentacji dla wersji 3.0 hello rozszerzenia diagnostycznych Linux](../diagnostic-extension.md).

## <a name="introduction"></a>Wprowadzenie

(**Uwaga**: hello rozszerzenia diagnostyczne systemu Linux jest open-powierzając jej ich konserwację na [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) gdzie hello najnowsze informacje dotyczące rozszerzeń hello pierwszej publikacji. Może być toocheck hello [GitHub strony](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) pierwszej.)

Hello rozszerzenia diagnostycznych Linux pomaga użytkownika monitora hello maszyn wirtualnych systemu Linux, które działają w systemie Microsoft Azure. Ma hello następujące możliwości:

* Zbiera i przekazuje informacje o wydajności systemu hello z tabeli magazynu hello maszyny Wirtualnej systemu Linux toohello użytkownika, w tym informacji diagnostycznych i syslog.
* Umożliwia użytkownikom toocustomize hello danych metryki, które zostaną zebrane i przekazane.
* Umożliwia użytkownikom tooupload określony dziennik pliki tooa magazynu wyznaczonego tabeli.

W bieżącej wersji hello 2.3 hello dane obejmują:

* Wszystkie dzienniki Linux Rsyslog, w tym system, zabezpieczenia i dzienniki aplikacji.
* Wszystkie dane systemu, które jest określone w [lokacji rozwiązania Cross platformy w programie System Center hello](https://scx.codeplex.com/wikipage?title=xplatproviders).
* Pliki dziennika zdefiniowane przez użytkownika.

To rozszerzenie działa zarówno z klasycznym hello i modeli wdrażania Menedżera zasobów.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Bieżąca wersja rozszerzenia hello i amortyzacja stare wersje

Najnowsza wersja rozszerzenia hello Hello jest **2.3**, i **wszystkie starsze wersje (2.0, 2.1 i 2.2) zostanie zastąpiona i nieopublikowane końca roku (2017)**. Jeśli zainstalowano hello rozszerzenia Diagnostyka systemu Linux wraz z uaktualnieniem automatyczne wersja pomocnicza wyłączone, jest zalecane Odinstaluj hello rozszerzenie, a następnie zainstaluj go ponownie z uaktualnieniem automatyczne wersja pomocnicza włączone. W klasycznym (ASM) maszyn wirtualnych można to osiągnąć, określając "2.*" jako wersja hello instalowania rozszerzenia hello za pośrednictwem interfejsu wiersza polecenia XPLAT platformy Azure lub programu Powershell. Na maszynach ARM można to osiągnąć poprzez włączenie ""autoUpgradeMinorVersion": true" w szablonie wdrożenia maszyny Wirtualnej hello. Ponadto żadnej nowej instalacji rozszerzenia hello powinien mieć wersja pomocnicza automatycznie hello uaktualnienia opcja jest włączona.

## <a name="enable-hello-extension"></a>Włącz rozszerzenie hello

To rozszerzenie można włączyć za pomocą hello [portalu Azure](https://portal.azure.com/#), programu Azure PowerShell lub skryptów wiersza polecenia platformy Azure.

tooview i skonfiguruj hello system oraz dane wydajności bezpośrednio z hello portalu Azure, wykonaj [następujące czynności na powitania Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

Ten artykuł skupia się na temat tooenable i skonfigurować rozszerzenia hello przy użyciu poleceń wiersza polecenia platformy Azure. Dzięki temu tooread i widok danych hello bezpośrednio z tabeli magazynu hello.

Należy pamiętać, że hello metody konfiguracji, które zostały opisane w tym miejscu nie będzie działać dla hello portalu Azure. tooview i skonfigurować hello wydajność systemu i dane bezpośrednio z hello portalu Azure, musi być włączona rozszerzenia hello za pośrednictwem portalu hello.

## <a name="prerequisites"></a>Wymagania wstępne

* **Agenta systemu Linux platformy Azure w wersji 2.0.6 lub nowszym**.

  Należy pamiętać, że większość obrazów Galeria Linux maszyny Wirtualnej Azure obejmuje wersji 2.0.6 lub nowszej. Można uruchomić **agenta WAAgent-wersja** tooconfirm wersję zainstalowanego na powitania maszyny Wirtualnej. Jeśli hello maszyny Wirtualnej jest uruchomiony w wersji starszej niż 2.0.6, można wykonać [tych instrukcji w serwisie GitHub](https://github.com/Azure/WALinuxAgent "instrukcje") tooupdate go.
* **Interfejs wiersza polecenia platformy Azure**. Postępuj zgodnie z [tym instrukcje dotyczące instalowania interfejsu wiersza polecenia](../../../cli-install-nodejs.md) tooset hello środowiska wiersza polecenia platformy Azure na tym komputerze. Po zainstalowaniu interfejsu wiersza polecenia Azure, można użyć hello **azure** polecenie z interfejsu wiersza polecenia (Bash, Terminal lub wiersza polecenia) tooaccess hello Azure CLI poleceniach. Na przykład:

  * Uruchom **zestaw rozszerzenie azure maszyny wirtualnej — Pomoc** uzyskać szczegółową pomoc.
  * Uruchom **logowanie w usłudze azure** toosign w tooAzure.
  * Uruchom **listy maszyna wirtualna platformy azure** toolist hello wszystkich maszyn wirtualnych, które masz na platformie Azure.
* Dane hello toostore konta magazynu. Konieczne będzie nazwa konta magazynu, które zostało utworzone wcześniej i dostępu do klucza tooupload hello tooyour pamięci masowej.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Użyj hello Azure CLI polecenia tooenable hello rozszerzenia diagnostyczne systemu Linux

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Scenariusz 1. Włącz rozszerzenie hello hello domyślny zestaw danych

W wersji 2.3 lub nowszej zawierają hello domyślnych danych, które będą zbierane:

* Wszystkie informacje Rsyslog (w tym system, zabezpieczenia i dzienniki aplikacji).  
* Podstawowy zestaw danych systemowych podstawy. Należy pamiętać, że hello pełny zestaw danych jest opisane na powitania [lokacji rozwiązania Cross platformy w programie System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Jeśli chcesz, aby tooenable dodatkowe dane, wykonaj czynności hello w scenariuszach 2 i 3.

Krok 1. Utwórz plik o nazwie PrivateConfig.json z hello następującej zawartości:

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

Krok 2. Uruchom  **vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2 ustawić rozszerzenia maszyny wirtualnej platformy azure.* — PrivateConfig.json prywatnego config-path**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Scenariusz 2. Dostosowanie metryk monitora wydajności hello

W tej sekcji opisano, jak toocustomize hello wydajności i tabelę danych diagnostycznych.

Krok 1. Utwórz plik o nazwie PrivateConfig.json z zawartością hello, który został opisany w scenariuszu 1. Utwórz również plik o nazwie PublicConfig.json. Umożliwia określenie hello danych ma toocollect.

Dla wszystkich obsługiwanych dostawców i zmienne odwołania hello [lokacji rozwiązania Cross platformy w programie System Center](https://scx.codeplex.com/wikipage?title=xplatproviders). Możesz mieć wiele zapytań i przechowywać je w wielu tabel, dodając więcej skryptu toohello zapytania.

Domyślnie zbierane są zawsze hello Rsyslog danych.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


Krok 2. Uruchom  **vm_name LinuxDiagnostic Microsoft.OSTCExtensions "2 ustawić rozszerzenia maszyny wirtualnej platformy azure.*"--prywatnego config-path PrivateConfig.json — PublicConfig.json publicznego config-path**.

### <a name="scenario-3-upload-your-own-log-files"></a>Scenariusz 3. Przekazanie plików dzienników

W tej sekcji opisano, jak toocollect i przekazywania dziennika określone pliki tooyour konta magazynu. Należy toospecify zarówno hello ścieżki tooyour dziennika plików i hello nazwy tabeli hello miejscu toostore dziennika. Można utworzyć wiele plików dziennika, dodając wielu skryptu toohello wpisów tabeli/plików.

Krok 1. Utwórz plik o nazwie PrivateConfig.json z zawartością hello, który został opisany w scenariuszu 1. Następnie utwórz plik o nazwie PublicConfig.json z powitania po zawartości:

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

Krok 2. Uruchom polecenie `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.

Należy pamiętać, że to ustawienie na powitania rozszerzenie wersji wcześniejszych too2.3, wszystkie dzienniki zapisane zbyt`/var/log/mysql.err` mogą być zduplikowane zbyt`/var/log/syslog` (lub `/var/log/messages` w zależności od hello Linux distro) oraz. Jeśli chcesz tooavoid duplikat rejestrowania, można wykluczyć rejestrowanie `local6` zakładzie dzienniki w konfiguracji rsyslog. Zależy od hello Linux distro, ale w systemie Ubuntu 14.04 toomodify pliku hello jest `/etc/rsyslog.d/50-default.conf` można zastąpić wiersza hello `*.*;auth,authpriv.none -/var/log/syslog` zbyt`*.*;auth,authpriv,local6.none -/var/log/syslog`. Tego problemu w najnowszej wersji poprawki hello 2.3 (2.3.9007), więc jeśli masz rozszerzenia hello wersji 2.3, ten problem nie powinno się zdarzyć. Jeśli nadal nie nawet po ponownym uruchomieniu maszyny Wirtualnej, skontaktuj się z nami i pomóc nam Rozwiązywanie problemów z powodu hello poprawka jest zainstalowana najnowsza wersja nie automatycznie.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Scenariusz 4. Zatrzymaj rozszerzenia hello ze zbierania żadnych dzienników

W tej sekcji opisano, jak rozszerzenie hello toostop ze zbierania dzienników. Należy pamiętać, że proces agenta monitorowania hello będzie nadal uruchomione i działają prawidłowo, nawet w przypadku tego procesu ponownej konfiguracji. Jeśli chcesz całkowicie monitorowania procesu agenta hello toostop, możesz to zrobić przez wyłączenie hello rozszerzenia. rozszerzenie hello toodisable polecenia Hello jest `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

Krok 1. Utwórz plik o nazwie PrivateConfig.json z zawartością hello, który został opisany w scenariuszu 1. Utwórz plik o nazwie PublicConfig.json z powitania po zawartości:

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


Krok 2. Uruchom  **vm_name LinuxDiagnostic Microsoft.OSTCExtensions "2 ustawić rozszerzenia maszyny wirtualnej platformy azure.*"--prywatnego config-path PrivateConfig.json — PublicConfig.json publicznego config-path**.

## <a name="review-your-data"></a>Przejrzyj dane

Witaj wydajności i danych diagnostycznych są przechowywane w tabeli magazynu Azure. Przegląd [jak toouse Azure Table Storage w języku Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn jak tooaccess hello danych w magazynie hello tabeli za pomocą skryptów wiersza polecenia platformy Azure.

Ponadto można użyć następujących danych hello tooaccess narzędzi interfejsu użytkownika:

1. Eksplorator serwera programu Visual Studio. Przejdź tooyour konta magazynu. Po uruchomieniu hello maszyny Wirtualnej dla około pięciu minut, zobaczysz hello cztery domyślne tabele: "LinuxCpu", "LinuxDisk", "LinuxMemory" i "Linuxsyslog". Kliknij dwukrotnie hello tabeli nazw tooview hello danych.
1. [Eksplorator usługi Azure Storage](https://azurestorageexplorer.codeplex.com/ "Eksploratora usługi Azure Storage").

![Obraz](./media/diagnostic-extension/no1.png)

Jeśli włączono fileCfg lub perfCfg (zgodnie z opisem w scenariuszach 2 i 3), można użyć danych innych niż domyślne tooview Eksploratora serwera w usłudze Visual Studio i Eksploratora usługi Storage platformy Azure.

## <a name="known-issues"></a>Znane problemy

* Witaj Rsyslog informacji i określonych przez klienta plików dziennika można uzyskać tylko za pomocą skryptów.
