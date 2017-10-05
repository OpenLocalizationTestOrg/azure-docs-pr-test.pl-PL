---
title: "Zestaw deweloperski IoT do chmury - nawiązać Centrum IoT Azure IoT zestaw deweloperski AZ3166 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować i AZ3166 zestaw deweloperski IoT nawiązać połączenia z Centrum IoT Azure go do przesyłania danych do platformy w chmurze platformy Azure, w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: 122fac584ac5b954ef7b33a3121bee2c502ebc63
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-iot-devkit-az3166-to-azure-iot-hub-in-the-cloud"></a>AZ3166 zestaw deweloperski IoT nawiązać połączenia z Centrum IoT Azure w chmurze

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

[Zestaw deweloperski IoT MXChip](https://microsoft.github.io/azure-iot-developer-kit/) służy do opracowywania i rozwiązań Internetu rzeczy (IoT) prototypu na wykorzystaniu usług Microsoft Azure. Obejmuje on Arduino tablicy zgodny z zaawansowanych urządzeń peryferyjnych i czujników, pakiet tablicy open source i rosnącym [katalogu projektów](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).

## <a name="what-you-do"></a>Co zrobić
Połącz [zestaw deweloperski](https://microsoft.github.io/azure-iot-developer-kit/) w Centrum Azure IoT utworzony zbierania danych temperatury i wilgotności, z czujników i wysyłania danych do Centrum IoT.

Nie masz jeszcze zestaw deweloperski? Uzyskać nowy [tutaj](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>Omawiane zagadnienia

* Jak zestaw deweloperski IoT nawiązać połączenia z punktem dostępu bezprzewodowego i przygotowywanie środowiska projektowego.
* Jak utworzyć Centrum IoT i zarejestrować urządzenie zestaw deweloperski IoT MXChip.
* Jak zbierać dane czujników, uruchamiając na zestaw deweloperski IoT MXChip przykładowej aplikacji.
* Jak wysyłać dane czujników do Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

* Zestaw deweloperski IoT MXChip tablicy za pomocą kabla USB micro. [Pobierz teraz](https://aka.ms/iot-devkit-purchase)
* Komputer z systemem Windows 10 lub macOS 10.10 +
* Aktywną subskrypcją platformy Azure
  * Aktywuj [bezpłatne 30-dniowej wersji próbnej konto Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>Przygotowanie sprzętu

Podłączanie sprzętu do komputera.

### <a name="hardware-you-need"></a>Sprzęt niezbędny

* Zestaw deweloperski tablicy
* Micro kabla USB

![Pobieranie uruchomiona — sprzęt](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-to-your-computer"></a>Łączenie się z komputerem zestaw deweloperski

1. Połącz koniec USB do komputera
2. Połącz koniec Micro USB do zestaw deweloperski
3. Zielona LED obok zasilania potwierdza połączenia

![pobieranie rozpoczęto — połączenia](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>Konfigurowanie sieci Wi-Fi

Projektami IoT jest zależne od łączności z Internetem. Użyj poniższych instrukcji, aby skonfigurować zestaw deweloperski, aby nawiązać połączenie sieci Wi-Fi.

### <a name="enter-ap-mode"></a>Tryb region

Przytrzymaj naciśnięty przycisk B, wypychania i zwolnij przycisk reset, a następnie zwolnij przycisk B. Twoje zestaw deweloperski przejdzie trybu region konfigurowania sieci Wi-Fi. Na ekranie będą wyświetlani Identifier(SSID) ustawić usługi zestaw deweloperski, a także adres IP portalu w konfiguracji:

![wprowadzenie — uruchomiona — sieci Wi-Fi region](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-to-devkit-ap"></a>Nawiązać zestaw deweloperski region

Teraz Użyj innego urządzenia włączone sieci Wi-Fi (komputera lub telefonu komórkowego), aby nawiązać połączenie SSID zestaw deweloperski (wyróżnione na zrzucie ekranu powyżej), pozostaw puste hasło.

![pobieranie pracy — identyfikator ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>Konfigurowanie sieci Wi-Fi dla zestaw deweloperski

Otwórz adres IP wyświetlany na ekranie zestaw deweloperski w przeglądarce PC lub telefonu komórkowego, wybierz sieć Wi-Fi, ma zestaw deweloperski, aby nawiązać połączenie, a następnie wpisz hasło. Kliknij przycisk **Connect** do ukończenia:

![pobieranie rozpoczęto — sieci Wi-Fi portalu](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Po pomyślnym połączenia, zestaw deweloperski zostanie ponownie uruchomiony w ciągu kilku sekund. Jeśli zakończyło się pomyślnie, na ekranie zostanie wyświetlony sieci Wi-Fi nazwy i adresu IP:

![pobieranie rozpoczęto — sieci Wi-Fi ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
Adres IP wyświetlany w zdjęcia może nie odpowiadać rzeczywista IP przypisany i wyświetlane na ekranie zestaw deweloperski. Jest to normalne, jak dynamiczne przypisywanie adresów IP sieci Wi-Fi korzysta z protokołu DHCP.

Po skonfigurowaniu sieci Wi-Fi, poświadczenia zostaną utrwalone na urządzeniu dla tego połączenia, nawet jeśli odłączony. Na przykład jeśli skonfigurowany zestaw deweloperski dla sieci Wi-Fi w domu, a następnie trwało zestaw deweloperski urzędowi, należy ponownie skonfigurować tryb region (poczynając od kroku **Wprowadź tryb region**) do nawiązania połączenia z biurem sieci Wi-Fi zestaw deweloperski. 

## <a name="start-using-devkit"></a>Uruchom przy użyciu zestaw deweloperski

Domyślna aplikacja uruchomiona na zestaw deweloperski sprawdzi najnowszej wersji oprogramowania układowego i wyświetli niektóre dane diagnostyki czujników za Ciebie.

### <a name="upgrade-to-the-latest-firmware"></a>Uaktualnij do najnowszego oprogramowania układowego

Zostanie wyświetlony monit na ekranie wymagane zarówno bieżąca, najnowsza wersja oprogramowania układowego w przypadku uaktualnienia. Postępuj zgodnie z [uaktualnienie oprogramowania układowego](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) przewodnik ją uaktualnić.

![wprowadzenie — uruchomiona-oprogramowania układowego](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
To jest jednorazowe wysiłku, po rozpoczęciu tworzenia na zestaw deweloperski i przekazać aplikację, mają najnowszego oprogramowania układowego pochodzą z aplikacji.

### <a name="test-various-sensors"></a>Testowanie różnych czujników

Naciśnij przycisk B do testowania czujników, nadal naciśnięcie klawisza i zwolnieniem przycisku B, aby przechodzić kolejno przez każdy czujnika.

![wprowadzenie — uruchomiona czujników](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Przygotuj Środowisko deweloperskie

Teraz nadszedł czas, aby skonfigurować środowisko projektowe: narzędzia i pakietów do tworzenia niezwykłych aplikacji IoT. Można wybrać systemu Windows lub wersji macOS zgodnie z systemu operacyjnego.


### <a name="windows"></a>Windows

Firma Microsoft zachęca do użycia pakietu instalacyjnego, aby przygotować Środowisko deweloperskie. Jeśli wystąpią problemy, można wykonać [ręczne](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) do wykonywania pracy.

#### <a name="download-latest-package"></a>Pobierz najnowszy pakiet

`.zip` Należy pobrać plik zawiera wszystkie niezbędne narzędzia i wymagane przez zestaw deweloperski programowanie pakietów.

> [!div class="button"]
[Pobieranie](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> `.zip` Plik zawiera następujące narzędzia i pakietów. Jeśli masz już pewne składniki zainstalowane, skrypt wykryje i Pomiń nich.
> * Node.js i Yarn: program obsługi dla skryptu Instalatora i automatycznych zadań
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -środowiska wiersza polecenia i platform do zarządzania zasobami platformy Azure, MSI zawiera zależnej Python i pip.
> * [Visual Studio Code](https://code.visualstudio.com/): Edytor niewielki kod dla rozwoju zestaw deweloperski
> * [Rozszerzenia programu Visual Studio Code Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): włącza Arduino Programowanie w kodzie VS
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): rozszerzenie Arduino zależy od tego narzędzia
> * Pakiet tablicy zestaw deweloperski: Narzędzie łańcuchy, biblioteki i projektów dla zestaw deweloperski
> * Narzędzie ST łącza: Niezbędne narzędzia i sterowniki

#### <a name="run-installation-script"></a>Uruchom skrypt instalacji

W Eksploratorze plików systemu Windows, Znajdź `.zip` i wyodrębnij go, Znajdź `install.cmd`, kliknij prawym przyciskiem myszy i wybierz **"Uruchom jako administrator"** można uruchomić.

![wprowadzenie — uruchomiona — Uruchom — administrator](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Podczas instalacji będzie wyświetlany jest postęp każdego narzędzia lub pakietu.

![pobieranie rozpoczęto Zainstaluj](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-to-install-drivers"></a>Upewnij się, aby zainstalować sterowniki

Kod VS rozszerzenia Arduino zależy od Arduino IDE. Jeśli instalujesz Arduino IDE po raz pierwszy, wyświetli się monit o zainstalowanie odpowiednich sterowników:

![pobieranie rozpoczęto sterowników](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Zakończenie instalacji, w zależności od szybkości Internet powinno zająć około 10 minut. Po zakończeniu instalacji programu Visual Studio Code i Arduino IDE skróty powinny być widoczne na pulpicie.

> [!NOTE] 
Czasami podczas uruchamiania kodu programu VS, pojawi się monit z powodu błędu, który nie może znaleźć Arduino IDE lub pakietu pokrewne tablicy. Aby go rozwiązać, zamknij kodzie VS, uruchom raz Arduino IDE i kodzie VS należy zlokalizować Arduino IDE ścieżkę poprawnie.


### <a name="macos-preview"></a>System macOS (wersja zapoznawcza)

Wykonaj następujące kroki, aby przygotować środowisko projektowe na macOS.

#### <a name="install-azure-cli-20"></a>Instalowanie interfejsu wiersza polecenia platformy Azure 2.0

Postępuj zgodnie z [oficjalnym przewodniku](https://docs.microsoft.com//cli/azure/install-azure-cli) instalowania 2.0 interfejsu wiersza polecenia platformy Azure:

Zainstaluj 2.0 interfejsu wiersza polecenia platformy Azure z jednym `curl` polecenia:

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

I ponownie uruchom z powłoki poleceń, aby zmiany zaczęły obowiązywać:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Zainstaluj Arduino IDE

Rozszerzenia programu Visual Studio Code Arduino zależy od Arduino IDE. Pobierz i zainstaluj [Arduino IDE dla macOS](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio

Pobierz i zainstaluj [Visual Studio Code dla macOS](https://code.visualstudio.com/). Są to narzędzie tworzenia podstawowego do tworzenia aplikacji IoT zestaw deweloperski.

####  <a name="download-latest-package"></a>Pobierz najnowszy pakiet

1. Zainstaluj środowisko Node.js. Można użyć Menedżera pakietów macOS popularnych [Homebrew](https://brew.sh/) lub [wstępnie skompilowany Instalator](https://nodejs.org/en/download/) go zainstalować.

2. Pobierz `.zip` plik zawierający skrypty zadań niezbędnych zestaw deweloperski w kodzie VS.

   > [!div class="button"]
   [Pobieranie](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Zlokalizuj `.zip` i wyodrębnij go. Następnie uruchom **Terminal** aplikacji i uruchom następujące polecenia, aby skonfigurować:

   Przenieś wyodrębnionego folderu do folderu macOS użytkownika:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Zainstaluj `npm` pakiety:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>Zainstaluj rozszerzenie kodzie VS dla Arduino

Visual Studio Code umożliwia instalowanie rozszerzeń Marketplace bezpośrednio w narzędziu, wystarczy kliknąć ikonę rozszerzenia w okienku po lewej stronie menu i wyszukiwać `Arduino` do zainstalowania:

![Instalacja rozszerzenia](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>Zainstaluj zestaw deweloperski pakiet tablicy

Należy dodać zestaw deweloperski tablicy za pomocą Menedżera tablicy w Visual Studio Code.

1. Użyj `Cmd+Shift+P` do wywołania palety polecenia i wpisz **Arduino** następnie znajdź i zaznacz pozycję **Arduino: Menedżer tablicy**.

2. Kliknij przycisk **dodatkowych adresów URL** w prawym dolnym rogu.
   ![Instalacja dodatkowych-adresów URL](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. W `settings.json` plików, dodawanie wiersza w dolnej części `USER SETTINGS` okienko i Zapisz.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![json instalacji — ustawienia](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Teraz w Menedżerze tablicy wyszukiwanie "az3166" i zainstaluj najnowszą wersję.
   ![az3166 instalacji](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

Masz teraz wszystkie niezbędne narzędzia i pakiety zainstalowane dla macOS.


## <a name="open-project-folder"></a>Otwórz projekt folderu

### <a name="launch-vs-code"></a>Uruchom program VS Code

Upewnij się, że nie jest połączona z zestaw deweloperski. Najpierw uruchom kodzie VS i łączenie się z komputerem zestaw deweloperski. Kod VS będzie automatycznie ją znaleźć i wyskakujące strona wprowadzenia:

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
Czasami podczas uruchamiania kodu programu VS, pojawi się monit z powodu błędu, który nie może znaleźć Arduino IDE lub pakietu pokrewne tablicy. Aby go rozwiązać, zamknij kodzie VS, uruchom ponownie Arduino IDE i kodzie VS należy zlokalizować Arduino IDE ścieżkę poprawnie.

### <a name="open-arduino-examples-folder"></a>Otwórz folder Arduino przykłady

Przełącz się do **"Przykłady Arduino"** karcie, przejdź do `Examples for MXCHIP AZ3166 > AzureIoT` i wybierz polecenie `GetStarted`.

![Mini solution — przykłady](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

W przypadku zamknąć okienko, aby załadować ponownie, należy użyć `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) do wywołania palety polecenia i wpisz **Arduino** Aby znaleźć i wybrać **Arduino: przykłady**.

## <a name="provision-azure-services"></a>Udostępnianie usług platformy Azure

W oknie rozwiązania, uruchom zadanie za pośrednictwem `Ctrl+P` (macOS: `Cmd+P`), wpisując "task chmury przepisu":

W kodzie VS terminali interakcyjne wiersza polecenia poprowadzi Cię przez Inicjowanie obsługi administracyjnej wymaganych usług Azure:

![Mini-solution-chmury provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Tworzenie i przekazywanie Arduino szkicu

### <a name="install-required-library"></a>Zainstalować wymaganej biblioteki

1. Naciśnij klawisz `F1` lub `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) do wywołania palety polecenia i wpisz **Arduino** następnie znajdź i zaznacz pozycję **Arduino: Library Manager**.

2. Wyszukaj `ArduinoJson` biblioteki i kliknij przycisk **instalacji**

### <a name="build-and-upload-the-device-code"></a>Tworzenie i przekazywanie kodu urządzenia

Użyj `Ctrl+P` (macOS: `Cmd+P`) do uruchamiania "zadań przekazywania urządzenie". Terminal wyświetli monit o wprowadzenie trybu konfiguracji. Aby to zrobić, przytrzymaj naciśnięty przycisk A, a następnie wypychania, a następnie zwolnij przycisk resetowania. Na ekranie będą wyświetlani "Konfiguracja". Jest to można ustawić parametry połączenia, które pobiera z kroku "zadań chmurze provision".

Następnie zostanie ona rozpoczęta Weryfikowanie i przekazywanie szkicu Arduino:

![Mini-solution urządzenia wysyłania](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Zestaw deweloperski spowoduje ponowny rozruch i uruchamianie kodu.

## <a name="test-the-project"></a>Projekt testowy

W kodzie VS kliknij ikonę plug zasilania na pasku stanu, aby otworzyć Serial Monitor.

Przykładowa aplikacja działa prawidłowo, gdy pojawi się następujące wyniki:

* Serial Monitor wyświetla te same informacje jak zawartość na poniższym zrzucie ekranu.
* LED na zestaw deweloperski IoT MXChip jest migający.

![Ostateczne dane wyjściowe w kodzie VS](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Problemy i opinie

Można znaleźć [— często zadawane pytania](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) w przypadku wystąpienia problemów lub dotrzeć do nas z kanałów poniżej.

## <a name="next-steps"></a>Następne kroki

Pomyślnie połączony zestaw deweloperski IoT MXChip Centrum IoT i wysyłane dane czujników przechwyconych do Centrum IoT.

Aby kontynuować wprowadzenie do usługi IoT Hub i zapoznać się z innymi scenariuszami IoT, zobacz:

- [Zarządzanie przesyłaniem komunikatów między chmurą a urządzeniem za pomocą narzędzia iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [Zapisywanie komunikatów usługi IoT Hub w magazynie danych platformy Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Użyj usługi Power BI do wizualizacji danych czujnika w czasie rzeczywistym z Centrum IoT Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Korzystanie z aplikacji sieci Web platformy Azure do wizualizacji danych czujnika w czasie rzeczywistym z Centrum IoT Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Pogody prognozy przy użyciu danych czujnika z Centrum IoT w usłudze Azure Machine Learning](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [Zarządzanie urządzeniami za pomocą narzędzia iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Zdalne monitorowanie i powiadomienia w usłudze Logic Apps](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)