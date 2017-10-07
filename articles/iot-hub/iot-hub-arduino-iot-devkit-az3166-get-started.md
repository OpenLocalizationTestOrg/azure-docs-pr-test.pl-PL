---
title: "aaaIoT zestaw deweloperski toocloud — Połącz AZ3166 zestaw deweloperski IoT tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz toosend danych toohello chmury Azure platforma AZ3166 zestaw deweloperski IoT tooAzure Centrum IoT na jej w tym samouczku."
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
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a>Połącz tooAzure AZ3166 zestaw deweloperski IoT Centrum IoT w chmurze hello

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

Witaj [zestaw deweloperski IoT MXChip](https://microsoft.github.io/azure-iot-developer-kit/) mogą być używane toodevelop i prototypu rozwiązań Internetu rzeczy (IoT) na wykorzystaniu usług Microsoft Azure. Obejmuje on Arduino tablicy zgodny z zaawansowanych urządzeń peryferyjnych i czujników, pakiet tablicy open source i rosnącym [katalogu projektów](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).

## <a name="what-you-do"></a>Co zrobić
Połącz [zestaw deweloperski](https://microsoft.github.io/azure-iot-developer-kit/) Centrum Azure IoT tooan utworzyć zbieranie hello temperatury i wilgotności dane z czujników, a następnie wysłać hello danych tooIoT koncentratora.

Nie masz jeszcze zestaw deweloperski? Uzyskać nowy [tutaj](https://aka.ms/iot-devkit-purchase).

## <a name="what-you-learn"></a>Omawiane zagadnienia

* Jak tooconnect dostępu tooWireless zestaw deweloperski IoT punktu i przygotowywanie środowiska projektowego.
* Jak toocreate Centrum IoT i zarejestrować urządzenie zestaw deweloperski IoT MXChip.
* Jak toocollect dane czujników, uruchamiając na zestaw deweloperski IoT MXChip przykładowej aplikacji.
* Jak toosend hello Centrum IoT tooyour danych czujnika.

## <a name="what-you-need"></a>Co jest potrzebne

* Zestaw deweloperski IoT MXChip tablicy za pomocą kabla USB micro. [Pobierz teraz](https://aka.ms/iot-devkit-purchase)
* Komputer z systemem Windows 10 lub macOS 10.10 +
* Aktywną subskrypcją platformy Azure
  * Aktywuj [bezpłatne 30-dniowej wersji próbnej konto Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html)

## <a name="prepare-your-hardware"></a>Przygotowanie sprzętu

Podłączanie hello sprzętu tooyour komputera.

### <a name="hardware-you-need"></a>Sprzęt niezbędny

* Zestaw deweloperski tablicy
* Micro kabla USB

![Pobieranie uruchomiona — sprzęt](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a>Podłącz komputer tooyour zestaw deweloperski

1. Połączenie USB zakończenia tooyour PC
2. Połączenie Micro USB zakończenia toohello zestaw deweloperski
3. zielony Hello LED dalej toopower potwierdza połączenia

![pobieranie rozpoczęto — połączenia](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a>Konfigurowanie sieci Wi-Fi

Projektami IoT jest zależne od łączności z Internetem. Użyj hello następujące instrukcje tooconfigure hello zestaw deweloperski tooconnect tooWiFi.

### <a name="enter-ap-mode"></a>Tryb region

Przytrzymaj naciśnięty przycisk B, a następnie wypychania i zwolnij przycisk reset hello, a następnie przycisk B. Twoje zestaw deweloperski przejdzie trybu region konfigurowania sieci Wi-Fi. ekran Hello spowoduje wyświetlenie hello usługi ustawić Identifier(SSID) z hello zestaw deweloperski, a także adres IP portalu hello konfiguracji:

![wprowadzenie — uruchomiona — sieci Wi-Fi region](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a>Połącz region tooDevKit

Teraz Użyj innej sieci Wi-Fi włączone urządzenia (komputera lub telefonu komórkowego) tooconnect toohello SSID zestaw deweloperski (wyróżnione na zrzucie ekranu hello powyżej), pozostaw puste hasło hello.

![pobieranie pracy — identyfikator ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a>Konfigurowanie sieci Wi-Fi dla zestaw deweloperski

Otwórz hello adres IP wyświetlany na ekranie zestaw deweloperski hello na komputerze lub przeglądarki telefonu komórkowego, wybierz sieć Wi-Fi hello interesujące tooconnect zestaw deweloperski hello do, a następnie wpisz hasło hello. Kliknij przycisk **Connect** toocomplete:

![pobieranie rozpoczęto — sieci Wi-Fi portalu](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

Po pomyślnym hello połączenia, hello zestaw deweloperski zostanie ponownie uruchomiony w ciągu kilku sekund. Jeśli zakończyło się pomyślnie, zostanie wyświetlony hello sieci Wi-Fi nazwy i adresu IP na ekranie powitania:

![pobieranie rozpoczęto — sieci Wi-Fi ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
adres IP Hello wyświetlane w fotografii hello może nie odpowiadać IP rzeczywistego hello przypisane i wyświetlany na ekranie zestaw deweloperski hello. Jest to normalne jako wykorzystanie sieci Wi-Fi DHCP toodynamically przypisywanie adresów IP.

Po skonfigurowaniu sieci Wi-Fi, poświadczenia zostaną utrwalone hello urządzenia dla tego połączenia, nawet wtedy, gdy odłączony. Na przykład, jeśli skonfigurowany hello zestaw deweloperski dla sieci Wi-Fi w domu, a następnie trwało hello zestaw deweloperski toohello office, konieczne będzie tryb tooreconfigure region (poczynając od kroku **Wprowadź tryb region**) hello tooconnect office tooyour zestaw deweloperski sieci Wi-Fi. 

## <a name="start-using-devkit"></a>Uruchom przy użyciu zestaw deweloperski

Hello domyślnej aplikacji uruchomionej na zestaw deweloperski sprawdzi hello najnowsza wersja oprogramowania układowego hello i wyświetli niektóre dane diagnostyki czujników za Ciebie.

### <a name="upgrade-toohello-latest-firmware"></a>Uaktualnij toohello najnowszego oprogramowania układowego

Zostanie wyświetlony monit na ekranie powitania zarówno hello wersja bieżących i najnowszego oprogramowania układowego, jeśli jest konieczne uaktualnienie. Postępuj zgodnie z [uaktualnienie oprogramowania układowego](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) przewodnik tooupgrade go.

![wprowadzenie — uruchomiona-oprogramowania układowego](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
To jest jednorazowe wysiłku, po rozpoczęciu tworzenia na powitania zestaw deweloperski i przekazać aplikację, mają najnowszego oprogramowania układowego hello pochodzą z aplikacji.

### <a name="test-various-sensors"></a>Testowanie różnych czujników

Naciśnij przycisk B tootest czujników, Kontynuuj naciskanie i zwalnianie toocycle przycisk hello B za pośrednictwem każdej czujnika.

![wprowadzenie — uruchomiona czujników](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a>Przygotuj Środowisko deweloperskie

Teraz nadszedł czas tooset się środowisko projektowe hello: narzędzia i pakiety toobuild ogłuszania aplikacji IoT. Można wybrać systemu Windows lub wersji macOS zgodnie z tooyour systemu operacyjnego.


### <a name="windows"></a>Windows

Firma Microsoft zachęca możesz toouse hello instalacji pakietu tooprepare hello Środowisko deweloperskie. Jeśli wystąpią problemy, można wykonać hello [ręczne](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget go wykonać.

#### <a name="download-latest-package"></a>Pobierz najnowszy pakiet

Witaj `.zip` należy pobrać plik zawiera wszystkie niezbędne narzędzia i wymagane przez zestaw deweloperski programowanie pakietów.

> [!div class="button"]
[Pobieranie](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> Witaj `.zip` plik zawiera hello następujące narzędzia i pakietów. Jeśli masz już pewne składniki zainstalowane, hello skrypt wykrywania i Pomiń nich.
> * Node.js i Yarn: program obsługi dla skryptu instalacyjnego hello i automatycznych zadań
> * [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -wieloplatformowych środowiska wiersza polecenia do zarządzania zasobami Azure hello MSI zawiera zależnej Python i pip.
> * [Visual Studio Code](https://code.visualstudio.com/): Edytor niewielki kod dla rozwoju zestaw deweloperski
> * [Rozszerzenia programu Visual Studio Code Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): włącza Arduino Programowanie w kodzie VS
> * [Arduino IDE](https://www.arduino.cc/en/Main/Software): hello rozszerzenie Arduino zależy od tego narzędzia
> * Pakiet tablicy zestaw deweloperski: Narzędzie łańcuchy, biblioteki i projektów dla hello zestaw deweloperski
> * Narzędzie ST łącza: Niezbędne narzędzia i sterowniki

#### <a name="run-installation-script"></a>Uruchom skrypt instalacji

W Eksploratorze plików systemu Windows, Znajdź hello `.zip` i wyodrębnij go, Znajdź `install.cmd`, kliknij prawym przyciskiem myszy i wybierz **"Uruchom jako administrator"** toostart.

![wprowadzenie — uruchomiona — Uruchom — administrator](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

Podczas instalacji zostanie wyświetlony postęp hello każdego narzędzia lub pakietu.

![pobieranie rozpoczęto Zainstaluj](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a>Potwierdź tooinstall sterowniki

Hello kodzie VS rozszerzenia Arduino polega na powitania Arduino IDE. Jeśli jest to hello instalujesz hello Arduino IDE po raz pierwszy, będzie tooinstall zostanie wyświetlony monit o odpowiednich sterowników:

![pobieranie rozpoczęto sterowników](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

Powinien upłynąć instalacji toofinish około 10 minut w zależności od szybkości Internet. Po zakończeniu instalacji hello Visual Studio Code i Arduino IDE skróty powinny być widoczne na pulpicie.

> [!NOTE] 
Czasami podczas uruchamiania kodu programu VS, pojawi się monit z powodu błędu, który nie może znaleźć Arduino IDE lub pakietu pokrewne tablicy. toosolve Arduino IDE jego kod VS zamknięcia uruchom raz i kodzie VS należy zlokalizować ścieżki Arduino IDE poprawnie.


### <a name="macos-preview"></a>System macOS (wersja zapoznawcza)

Wykonaj środowisko projektowe tooprepare te kroki na macOS.

#### <a name="install-azure-cli-20"></a>Instalowanie interfejsu wiersza polecenia platformy Azure 2.0

Wykonaj hello [oficjalnym przewodniku](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall 2.0 interfejsu wiersza polecenia platformy Azure:

Zainstaluj 2.0 interfejsu wiersza polecenia platformy Azure z jednym `curl` polecenia:

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

I ponownie uruchom polecenia powłoki dla efektu tootake zmiany:

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a>Zainstaluj Arduino IDE

Hello rozszerzenia programu Visual Studio Code Arduino polega na powitania Arduino IDE. Pobierz i zainstaluj hello [Arduino IDE dla macOS](https://www.arduino.cc/en/Main/Software).

#### <a name="install-visual-studio-code"></a>Zainstaluj kod programu Visual Studio

Pobierz i zainstaluj [Visual Studio Code dla macOS](https://code.visualstudio.com/). Są to narzędzie do projektowania głównej hello do tworzenia aplikacji IoT zestaw deweloperski.

####  <a name="download-latest-package"></a>Pobierz najnowszy pakiet

1. Zainstaluj środowisko Node.js. Można użyć Menedżera pakietów macOS popularnych [Homebrew](https://brew.sh/) lub [wstępnie skompilowany Instalator](https://nodejs.org/en/download/) tooinstall go.

2. Pobierz `.zip` plik zawierający skrypty zadań niezbędnych zestaw deweloperski w kodzie VS.

   > [!div class="button"]
   [Pobieranie](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   Zlokalizuj hello `.zip` i wyodrębnij go. Następnie uruchom **Terminal** hello uruchom następujące polecenia tooconfigure i aplikacji:

   Przenieść folder użytkownika macOS tooyour wyodrębnionego folderu:
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   Zainstaluj `npm` pakiety:
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a>Zainstaluj rozszerzenie kodzie VS dla Arduino

Visual Studio Code pozwala tooinstall Marketplace rozszerzenia bezpośrednio w narzędziu hello, po prostu kliknij ikonę rozszerzenia hello w okienku po lewej stronie menu hello i wyszukiwać `Arduino` tooinstall:

![Instalacja rozszerzenia](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a>Zainstaluj zestaw deweloperski pakiet tablicy

Konieczne będzie tablicy zestaw deweloperski hello tooadd przy użyciu hello Menedżera tablicy w Visual Studio Code.

1. Użyj `Cmd+Shift+P` tooinvoke polecenia palety i typ **Arduino** następnie znajdź i zaznacz pozycję **Arduino: Menedżer tablicy**.

2. Kliknij przycisk **dodatkowych adresów URL** na powitania prawym dolnym rogu.
   ![Instalacja dodatkowych-adresów URL](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. W hello `settings.json` plików, Dodaj wiersz na dole hello `USER SETTINGS` okienko i Zapisz.
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![json instalacji — ustawienia](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. Teraz hello Menedżera tablicy Wyszukaj "az3166" i zainstaluj najnowszą wersję hello.
   ![az3166 instalacji](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

Masz teraz wszystkie niezbędne narzędzia hello i pakiety zainstalowane dla macOS.


## <a name="open-project-folder"></a>Otwórz projekt folderu

### <a name="launch-vs-code"></a>Uruchom program VS Code

Upewnij się, że nie jest połączona z zestaw deweloperski. Najpierw uruchom kodzie VS i podłącz komputer tooyour zestaw deweloperski hello. Kod VS będzie automatycznie ją znaleźć i wyskakujące strona wprowadzenia:

![Mini solution vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
Czasami podczas uruchamiania kodu programu VS, pojawi się monit z powodu błędu, który nie może znaleźć Arduino IDE lub pakietu pokrewne tablicy. toosolve Arduino IDE jego kod VS zamknięcia, uruchom ponownie i kodzie VS należy zlokalizować ścieżki Arduino IDE poprawnie.

### <a name="open-arduino-examples-folder"></a>Otwórz folder Arduino przykłady

Przełącz zbyt**"Przykłady Arduino"** karcie kolejno zbyt`Examples for MXCHIP AZ3166 > AzureIoT` i wybierz polecenie `GetStarted`.

![Mini solution — przykłady](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

W przypadku tooclose hello okienku tooreload go, użyj `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke polecenia palety i typ **Arduino** toofind i wybierz **Arduino: przykłady**.

## <a name="provision-azure-services"></a>Udostępnianie usług platformy Azure

W oknie rozwiązania hello Uruchom zadania za pomocą `Ctrl+P` (macOS: `Cmd+P`), wpisując "task chmury przepisu":

W hello kodzie VS terminali interakcyjne wiersza polecenia poprowadzi Cię przez hello inicjowania obsługi administracyjnej wymaganych usług Azure:

![Mini-solution-chmury provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a>Tworzenie i przekazywanie Arduino szkicu

### <a name="install-required-library"></a>Zainstalować wymaganej biblioteki

1. Naciśnij klawisz `F1` lub `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke polecenia palety i typ **Arduino** następnie znajdź i zaznacz pozycję **Arduino: Library Manager**.

2. Wyszukaj `ArduinoJson` biblioteki i kliknij przycisk **instalacji**

### <a name="build-and-upload-hello-device-code"></a>Tworzenie i przekazywanie hello urządzenia kodu

Użyj `Ctrl+P` (macOS: `Cmd+P`) toorun "zadań urządzenia — przekazywanie". Witaj terminali wyświetli monit o możesz tooenter trybu konfiguracji. toodo tak, naciśnij i przytrzymaj przycisk A, a następnie przycisk reset hello wypychania i wersji. ekran Hello wyświetli "Konfiguracja". Jest to ciąg połączenia hello tooset pobiera z kroku "świadczenia chmury zadania".

Następnie zostanie ona rozpoczęta Weryfikowanie i przekazywanie szkicu Arduino hello:

![Mini-solution urządzenia wysyłania](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

Hello zestaw deweloperski spowoduje ponowny rozruch i uruchamianie hello kodu.

## <a name="test-hello-project"></a>Projekt testowy hello

W kodzie VS kliknij hello zasilania plug ikonę na pasku tooopen hello Serial Monitor stanu hello.

Witaj Przykładowa aplikacja działa prawidłowo po wyświetleniu hello następujące wyniki:

* Witaj Serial monitorów hello tych samych informacji dotyczących zawartości hello na powitania zrzucie ekranu pokazano poniżej.
* Witaj LED na zestaw deweloperski IoT MXChip jest migający.

![Ostateczne dane wyjściowe w kodzie VS](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>Problemy i opinie

Można znaleźć [— często zadawane pytania](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) w przypadku wystąpienia problemów lub dotrzeć toous z kanałów hello poniżej.

## <a name="next-steps"></a>Następne kroki

Pomyślnie nawiązano tooyour zestaw deweloperski IoT MXChip Centrum IoT i wysłane hello przechwycone Centrum IoT tooyour danych czujnika.

toocontinue wprowadzenie do korzystania z Centrum IoT i tooexplore innych scenariuszach IoT, zobacz:

- [Zarządzanie przesyłaniem komunikatów między chmurą a urządzeniem za pomocą narzędzia iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [Zapisz komunikaty Centrum IoT tooAzure magazynu danych](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [Użyj usługi Power BI toovisualize czujnika w czasie rzeczywistym danych z Centrum IoT Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [Korzystanie z Centrum IoT Azure danych czujnika w czasie rzeczywistym toovisualize aplikacji sieci Web Azure](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [Prognoza pogody przy użyciu danych czujnika hello z Centrum IoT w usłudze Azure Machine Learning](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [Zarządzanie urządzeniami za pomocą narzędzia iothub-explorer](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [Zdalne monitorowanie i powiadomienia w usłudze Logic Apps](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)