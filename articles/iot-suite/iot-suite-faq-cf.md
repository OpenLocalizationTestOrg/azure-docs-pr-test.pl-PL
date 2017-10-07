---
title: "aaaAzure pakiet IoT połączone fabryki — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dla fabryki połączonych pakiet IoT"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Często zadawane pytania dla fabryki połączonych pakiet IoT wstępnie skonfigurowane rozwiązanie

Zobacz też, hello ogólne [— często zadawane pytania](iot-suite-faq.md) pakietu IoT.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>Gdzie mogę znaleźć kodu źródłowego hello hello wstępnie skonfigurowane rozwiązanie?

Kod źródłowy Hello są przechowywane w hello następujące repozytorium GitHub:

* [Fabryka połączonych wstępnie skonfigurowane rozwiązanie](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>Co to jest OPC UA?

OPC Ujednolicona architektura (UA), wydane w ramach 2008, jest niezależne od platformy, zorientowane na usługę współdziałanie standardowa. OPC UA jest używany przez różnych systemów przemysłowych i urządzeń, takich jak czujniki branży komputerów i układy logiczne. OPC UA integruje funkcjonalność hello specyfikacji OPC klasycznego hello jeden rozszerzalne środowisko z wbudowanych zabezpieczeń. Jest to standardowy, który jest wymuszany przez hello OPC Foundation. Witaj [OPC Foundation](http://opcfoundation.org/) jest organizacją nie dla zysków z więcej niż 440 elementów członkowskich. Celem Hello organizacji hello jest toouse OPC specyfikacje toofacilitate wielu dostawców, obejmującego wiele platform, bezpieczny i niezawodny współdziałanie za pomocą:

* Infrastruktura
* Specyfikacje
* Technologia
* Procesy

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>Dlaczego warto wybrać się Microsoft UA OPC dla hello połączony fabryki wstępnie skonfigurowane rozwiązanie?

Microsoft postanowiono OPC UA, ponieważ jest to platforma otwarty, niezastrzeżonych, standard niezależne, branży i sprawdzone. Jest wymagane dla rozwiązań architektura odwołanie Industrie 4.0 (RAMI4.0) zapewniające współdziałanie szeroką gamę wytwarzania i urządzeń. Microsoft widzi żądanie z naszych rozwiązań toobuild Industrie 4.0 klientów. Obsługa OPC UA pomaga niższe hello bariery dla klientów tooachieve swoje cele i zapewnia natychmiastowe toothem wartość.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>Jak dodać publicznego symulację toohello adres IP maszyny Wirtualnej?

Masz dwie opcje tooadd hello adres IP:

* Użyj skryptu programu PowerShell hello `Simulation/Factory/Add-SimulationPublicIp.ps1` w hello [repozytorium](https://github.com/Azure/azure-iot-connected-factory). Podaj nazwę wdrożenia jako parametr. Dla wdrożenia lokalnego, należy użyć `<your username>ConnFactoryLocal`. skrypt Hello Wyświetla adres IP hello hello maszyny Wirtualnej.

* W portalu Azure hello zlokalizuj grupy zasobów hello wdrożenia. Z wyjątkiem wdrożenia lokalnego grupa zasobów hello ma nazwę hello, określone jako rozwiązanie lub wdrożenia. W przypadku wdrożenia lokalnego przy użyciu skryptu kompilacji hello hello Nazwa grupy zasobów hello jest `<your username>ConnFactoryLocal`. Teraz Dodaj nową **publicznego adresu IP** zasób toohello grupa zasobów.

> [!NOTE]
> W obu przypadkach upewnij się, zainstaluj najnowsze poprawki hello wykonując instrukcje hello na powitania [Ubuntu witryny sieci Web](https://wiki.ubuntu.com/Security/Upgrades). Zachowaj instalacji hello zapasowej toodate dla tak długo, jak długo maszyny Wirtualnej jest dostępna za pośrednictwem publicznego adresu IP.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>Jak usunąć hello publicznego adresu IP adres toohello symulacji maszyny Wirtualnej?

Masz dwie opcje tooremove hello adres IP:

* Użyj skryptu programu PowerShell hello Simulation/Factory/Remove-SimulationPublicIp.ps1 hello [repozytorium](https://github.com/Azure/azure-iot-connected-factory). Podaj nazwę wdrożenia jako parametr. Dla wdrożenia lokalnego, należy użyć `<your username>ConnFactoryLocal`. skrypt Hello Wyświetla adres IP hello hello maszyny Wirtualnej.

* W portalu Azure hello zlokalizuj grupy zasobów hello wdrożenia. Z wyjątkiem wdrożenia lokalnego grupa zasobów hello ma nazwę hello, określone jako rozwiązanie lub wdrożenia. W przypadku wdrożenia lokalnego przy użyciu skryptu kompilacji hello hello Nazwa grupy zasobów hello jest `<your username>ConnFactoryLocal`. Teraz usunąć hello **publicznego adresu IP** zasobów z hello grupy zasobów.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>Jak tworzyć w symulacji toohello maszyny Wirtualnej

Rejestrowanie w symulacji toohello maszyny Wirtualnej jest obsługiwana tylko jeśli wdrożono rozwiązanie przy użyciu skryptu środowiska PowerShell hello `build.ps1` w hello [repozytorium](https://github.com/Azure/azure-iot-connected-factory).

Jeśli wdrożono rozwiązanie hello z www.azureiotsuite.com, nie można zalogować toohello maszyny Wirtualnej. Nie można zalogować się, ponieważ hasło hello jest generowany losowo i nie można zresetować go.

1. Dodaj publiczny toohello adres IP maszyny Wirtualnej. Zobacz [jak dodać publicznego symulację toohello adres IP maszyny Wirtualnej?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Utwórz tooyour sesji SSH maszyny Wirtualnej za pomocą adresu IP hello hello maszyny Wirtualnej.
1. jest Hello username toouse: `docker`.
1. toouse hasło Hello zależy od wersji hello używanych toodeploy:
    * Dla rozwiązań wdrożenie za pomocą skryptu build.ps1 hello przed 1 czerwca 2017 hasło hello jest: `Passw0rd`.
    * Rozwiązania w zakresie wdrażania przy użyciu skryptu build.ps1 powitania po 1 czerwca 2017 hello hasła można znaleźć w hello `<name of your deployment>.config.user` pliku. Witaj hasło jest zapisywane w hello **VmAdminPassword** ustawienie. Witaj hasła jest generowany losowo w czasie wdrażania chyba że zostanie określony za pomocą hello `build.ps1` skryptu parametru`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>Jak zatrzymać i uruchomić wszystkie procesy docker w symulacji hello maszyny Wirtualnej?

1. Zaloguj się w symulacji toohello maszyny Wirtualnej. Zobacz [jak zarejestrować się w symulacji toohello maszyny Wirtualnej?](#how-do-i-sign-in-to-the-simulation-vm)
1. Uruchom kontenery, które są aktywne, toocheck: `docker ps`.
1. Uruchom wszystkie kontenery symulacji, toostop: `./stopsimulation`.
1. toostart wszystkich kontenerów symulacji:
    * Eksportuj powłoki zmienna o nazwie hello **IOTHUB_CONNECTIONSTRING**. Należy użyć wartości hello hello **IotHubOwnerConnectionString** ustawienie w hello `<name of your deployment>.config.user` pliku. Na przykład:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Uruchom polecenie `./startsimulation`.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>Jak zaktualizować symulacji hello w hello maszyny Wirtualnej?

Jeśli zostały wprowadzone żadne zmiany symulacji toohello, możesz użyć skryptu programu PowerShell hello `build.ps1` w hello [repozytorium](https://github.com/Azure/azure-iot-connected-factory) przy użyciu hello `updatedimulation` polecenia. Ten skrypt tworzy wszystkie składniki symulacji hello, zatrzymuje symulacji hello w hello maszyny Wirtualnej, przekazuje, instaluje i można je uruchomić.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>Jak sprawdzić hello parametry połączenia używane przez Moje rozwiązanie Centrum IoT hello?

Jeśli wdrożono rozwiązanie z hello `build.ps1` skryptu w hello [repozytorium](https://github.com/Azure/azure-iot-connected-factory), ciąg połączenia hello jest wartość hello **IotHubOwnerConnectionString** w hello `<name of your deployment>.config.user` pliku.

Można również znaleźć hello ciągu połączenia za pomocą hello portalu Azure. W Centrum IoT zasobów w grupie zasobów hello wdrożenia hello Znajdź ustawień parametrów połączenia hello.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>Które urządzenia IoT Hub hello Użyj symulacji fabryka połączenia?

Witaj symulacji samodzielnie rejestruje hello następujące urządzenia:

* proxy.Beijing.corp.contoso
* proxy.capetown.corp.contoso
* proxy.Mumbai.corp.contoso
* proxy.munich0.corp.contoso
* proxy.Rio.corp.contoso
* proxy.Seattle.corp.contoso
* Publisher.Beijing.corp.contoso
* Publisher.capetown.corp.contoso
* Publisher.Mumbai.corp.contoso
* Publisher.munich0.corp.contoso
* Publisher.Rio.corp.contoso
* Publisher.Seattle.corp.contoso

Przy użyciu hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) lub [explorer Centrum iothub](https://github.com/azure/iothub-explorer) narzędzia, możesz sprawdzić, które urządzenia są zarejestrowane w usłudze Centrum IoT hello jest przy użyciu rozwiązania. toouse tych narzędzi, i potrzebne hello parametry połączenia dla Centrum IoT hello w danym wdrożeniu.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>Jak uzyskać danych dziennika z hello symulacji składników

Wszystkie składniki w symulacji hello rejestrowanie informacji w plikach toolog. Te pliki znajdują się w hello maszyny Wirtualnej w folderze hello `home/docker/Logs`. Dzienniki hello tooretrieve, możesz użyć skryptu programu PowerShell hello `Simulation/Factory/Get-SimulationLogs.ps1` w hello [repozytorium](https://github.com/Azure/azure-iot-connected-factory).

Ten skrypt wymaga toosign w toohello maszyny Wirtualnej. Mogą być potrzebne tooprovide poświadczeń logowania hello. Zobacz [jak zarejestrować się w symulacji toohello maszyny Wirtualnej?](#how-do-i-sign-in-to-the-simulation-vm) toofind hello poświadczeń.

skrypt Hello dodaje i usuwa publiczny toohello adres IP maszyny Wirtualnej, jeśli jeszcze nie ma jeden i usuwa go. skrypt Hello umieszcza wszystkie pliki dziennika w archiwum i pobiera hello archiwum tooyour Programowanie w stacji roboczej.

Możesz też zalogować toohello maszyny Wirtualnej za pośrednictwem SSH i sprawdzić hello pliki dziennika w czasie wykonywania.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>Jak sprawdzić, czy symulacji hello wysyła toohello danych w chmurze?

Z hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) lub hello [explorer Centrum iothub](https://github.com/azure/iothub-explorer) narzędzia, możesz sprawdzić hello danych wysłanych tooIoT Centrum z określonymi urządzeniami. toouse tych narzędzi, potrzeby parametrów połączenia hello tooknow Centrum IoT hello w danym wdrożeniu. Zobacz [jak sprawdzić hello parametry połączenia używane przez Moje rozwiązanie Centrum IoT hello?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Sprawdź hello dane wysyłane przez jednego z urządzeń wydawcy hello:

* Publisher.Beijing.corp.contoso
* Publisher.capetown.corp.contoso
* Publisher.Mumbai.corp.contoso
* Publisher.munich0.corp.contoso
* Publisher.Rio.corp.contoso
* Publisher.Seattle.corp.contoso

Jeśli zostanie wyświetlone żadne dane wysyłane tooIoT koncentratora, oznacza to, że wystąpił problem z hello symulacji. Pierwszym krokiem analizy powinien analizowanie plików dziennika hello hello symulacji składników. Zobacz [jak można uzyskać danych dziennika z hello symulacji składniki?](#how-can-i-get-log-data-from-the-simulation-components) Następnie spróbuj toostop i uruchomić symulacji hello i w razie nie ma jeszcze żadnych danych wysyłane, zaktualizować symulacji hello całkowicie. Zobacz [jak zaktualizować symulacji hello w hello maszyny Wirtualnej?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Następne kroki

Możesz też przeglądać niektóre hello inne funkcje i możliwości rozwiązań pakiet IoT wstępnie hello:

* [Omówienie rozwiązania konserwacji predykcyjnej wstępnie](iot-suite-predictive-overview.md)
* [Fabryka połączonych wstępnie Omówienie rozwiązania](iot-suite-connected-factory-overview.md)
* [Zabezpieczenia IoT z hello tła w](securing-iot-ground-up.md)
