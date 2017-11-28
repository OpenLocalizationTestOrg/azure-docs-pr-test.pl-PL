---
title: "Urządzeń Sensor tag & Azure IoT bramy - Lekcja 1: Konfigurowanie Intel NUC | Dokumentacja firmy Microsoft"
description: "Ustawienie toowork Intel NUC jako bramy IoT między czujników i informacji z czujnika toocollect Centrum IoT Azure i wysyłać je tooIoT koncentratora."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iot bramy intel nuc nuc komputera, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="d6516-104">Konfigurowanie Intel NUC jako brama IoT</span><span class="sxs-lookup"><span data-stu-id="d6516-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="d6516-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="d6516-105">What you will do</span></span>

- <span data-ttu-id="d6516-106">Ustawienie Intel NUC jako bramę IoT.</span><span class="sxs-lookup"><span data-stu-id="d6516-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="d6516-107">Zainstaluj pakiet Azure IoT krawędzi hello na powitania Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="d6516-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="d6516-108">Uruchom przykładową aplikację "hello_world" na powitania funkcjonalność bramy hello tooverify Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="d6516-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="d6516-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d6516-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d6516-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="d6516-110">What you will learn</span></span>

<span data-ttu-id="d6516-111">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="d6516-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="d6516-112">Jak tooconnect Intel NUC z urządzenia peryferyjne.</span><span class="sxs-lookup"><span data-stu-id="d6516-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="d6516-113">Jak pakietów hello wymagane tooinstall i aktualizacji przy użyciu Intel NUC hello inteligentne Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="d6516-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="d6516-114">Jak toorun hello "hello_world" Przykładowe funkcjonalność bramy hello tooverify aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6516-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d6516-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="d6516-115">What you need</span></span>

- <span data-ttu-id="d6516-116">Intel NUC Kit DE3815TYKE z hello pakiet oprogramowania bramy IoT firmy Intel (Linux rzeki knie * 7.0.0.13) preinstalowany.</span><span class="sxs-lookup"><span data-stu-id="d6516-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="d6516-117">[Kliknij tutaj toopurchase Grove IoT komercyjnych bramy zestawu](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="d6516-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="d6516-118">Kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="d6516-118">An Ethernet cable.</span></span>
- <span data-ttu-id="d6516-119">Klawiatury.</span><span class="sxs-lookup"><span data-stu-id="d6516-119">A keyboard.</span></span>
- <span data-ttu-id="d6516-120">Kabel HDMI lub VGA.</span><span class="sxs-lookup"><span data-stu-id="d6516-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="d6516-121">Monitor portu HDMI lub VGA.</span><span class="sxs-lookup"><span data-stu-id="d6516-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="d6516-122">Opcjonalnie: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="d6516-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Zestaw bramy](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="d6516-124">Intel NUC Uzyskuj dostęp do urządzeń peryferyjnych hello</span><span class="sxs-lookup"><span data-stu-id="d6516-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="d6516-125">Obraz powitania poniżej przedstawiono przykładowy NUC firmy Intel, który jest połączony z różnych urządzeń peryferyjnych:</span><span class="sxs-lookup"><span data-stu-id="d6516-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="d6516-126">Klawiatura tooa połączonych.</span><span class="sxs-lookup"><span data-stu-id="d6516-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="d6516-127">Połączone tooa monitor za pomocą kabla VGA lub kabla HDMI.</span><span class="sxs-lookup"><span data-stu-id="d6516-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="d6516-128">Połączone tooa przewodowej sieci za pomocą kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="d6516-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="d6516-129">Zasilacz tooa połączonych za pomocą kabla zasilania.</span><span class="sxs-lookup"><span data-stu-id="d6516-129">Connected tooa power supply with a power cable.</span></span>

![Tooperipherals NUC Intel połączone](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="d6516-131">Połącz system Intel NUC toohello z komputera hosta za pośrednictwem protokołu Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="d6516-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="d6516-132">Konieczne będzie, klawiatury i monitora adresu IP hello tooget urządzenia Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="d6516-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="d6516-133">Jeśli znasz już hello IP adresu, możesz pominąć wyprzedzeniem toostep 3 w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6516-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="d6516-134">Włącz hello Intel NUC, naciskając przycisk zasilania hello, a następnie zaloguj.</span><span class="sxs-lookup"><span data-stu-id="d6516-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="d6516-135">Hello domyślna nazwa użytkownika i hasło są `root`.</span><span class="sxs-lookup"><span data-stu-id="d6516-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="d6516-136">Pobierz adres IP hello hello Intel NUC, uruchamiając hello `ifconfig` na powitania Intel NUC urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d6516-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="d6516-137">Oto przykład danych wyjściowych polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="d6516-137">Here is an example of hello command output.</span></span>

   ![dane wyjściowe ifconfig przedstawiający Intel NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="d6516-139">W tym przykładzie hello wartość, która wykonuje `inet addr:` jest adresem IP hello potrzebne przy połączeniu toohello Intel NUC z komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="d6516-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="d6516-140">Użyj jednej z hello poniższych klientów SSH z tooIntel tooconnect NUC Twojego hosta komputera.</span><span class="sxs-lookup"><span data-stu-id="d6516-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="d6516-141">[PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6516-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="d6516-142">Witaj wbudowanego klienta SSH Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="d6516-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="d6516-143">Jest bardziej wydajny i produktywności toooperate NUC Intel z komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="d6516-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="d6516-144">Będzie konieczne hello Intel NUC adres IP użytkownika tooit tooconnect nazwy i hasła przy użyciu klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="d6516-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="d6516-145">Oto przykład, które używa klienta SSH w macOS.</span><span class="sxs-lookup"><span data-stu-id="d6516-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="d6516-146">![Klient SSH systemem macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="d6516-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="d6516-147">Zainstaluj pakiet Azure IoT krawędzi hello</span><span class="sxs-lookup"><span data-stu-id="d6516-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="d6516-148">Pakiet Azure IoT krawędzi Hello zawiera wstępnie skompilowanych plików binarnych hello krawędzi IoT i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="d6516-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="d6516-149">Te pliki binarne są Azure IoT krawędzi, hello Azure IoT SDK i narzędzia odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="d6516-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="d6516-150">Witaj pakietu zawiera także "hello_world" Przykładowa aplikacja jest funkcjonalność bramy hello toovalidate używane.</span><span class="sxs-lookup"><span data-stu-id="d6516-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="d6516-151">Krawędź IoT jest hello główną część hello bramy.</span><span class="sxs-lookup"><span data-stu-id="d6516-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="d6516-152">Wykonaj te kroki tooinstall hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="d6516-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="d6516-153">Dodaj hello repozytorium chmury IoT, uruchamiając następujące polecenia w oknie terminalu hello:</span><span class="sxs-lookup"><span data-stu-id="d6516-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="d6516-154">Wprowadź "y", gdy monit too'Include ten kanał? "</span><span class="sxs-lookup"><span data-stu-id="d6516-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="d6516-155">Jeśli zostanie wyświetlony `import read failed(-1)` błąd, hello Użyj następującego polecenia tooresolve hello problemu:</span><span class="sxs-lookup"><span data-stu-id="d6516-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="d6516-156">Witaj `rpm` polecenie importuje hello klucza obr. / min.</span><span class="sxs-lookup"><span data-stu-id="d6516-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="d6516-157">Witaj `smart channel` polecenie dodaje hello rpm kanału toohello inteligentne Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="d6516-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="d6516-158">Przed rozpoczęciem powitalne `smart update` polecenia, zostanie wyświetlony wyjścia, takich jak poniżej.</span><span class="sxs-lookup"><span data-stu-id="d6516-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![obr. / min i dane wyjściowe polecenia inteligentne kanału](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="d6516-160">Wykonanie polecenia update inteligentne hello:</span><span class="sxs-lookup"><span data-stu-id="d6516-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="d6516-161">Zainstaluj pakiet Azure IoT bramy hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d6516-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="d6516-162">`packagegroup-cloud-azure`jest nazwą hello hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="d6516-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="d6516-163">Witaj `smart install` polecenia jest używane tooinstall hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="d6516-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="d6516-164">Witaj uruchom następujące polecenie, jeśli zostanie wyświetlony ten błąd: "klucz publiczny nie jest dostępna"</span><span class="sxs-lookup"><span data-stu-id="d6516-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="d6516-165">Ponowny rozruch hello NUC firmy Intel, jeśli zostanie wyświetlony ten błąd: "nie zawiera util-linux deweloperów"</span><span class="sxs-lookup"><span data-stu-id="d6516-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="d6516-166">Po zainstalowaniu pakietu hello Intel NUC jest gotowy toofunction jako brama.</span><span class="sxs-lookup"><span data-stu-id="d6516-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="d6516-167">Uruchom hello Azure IoT krawędzi "hello_world" przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="d6516-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="d6516-168">następujące Przykładowa aplikacja Hello tworzy bramę z `hello_world.json` pliku i używa podstawowych składników hello Azure IoT krawędzi architektura toolog pliku tooa wiadomość hello world (log.txt) co 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="d6516-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="d6516-169">Przykładowa aplikacja hello Hello World można uruchomić, wykonując następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="d6516-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="d6516-170">Zezwala aplikacji Hello World hello Uruchom kilka minut, a następnie naciśnij hello Enter klucza toostop go.</span><span class="sxs-lookup"><span data-stu-id="d6516-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="d6516-171">![dane wyjściowe aplikacji](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="d6516-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="d6516-172">Możesz zignorować wszelkie błędy "handle(NULL) nieprawidłowy argument", które są wyświetlane po naciśnięciu przycisku Enter.</span><span class="sxs-lookup"><span data-stu-id="d6516-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="d6516-173">Możesz sprawdzić, że brama hello zostało wykonane pomyślnie, otwierając plik log.txt hello, która jest teraz w folderze hello_world ![log.txt widok katalogu](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="d6516-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="d6516-174">Otwórz za pomocą następującego polecenia hello log.txt:</span><span class="sxs-lookup"><span data-stu-id="d6516-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="d6516-175">Zostanie wtedy wyświetlone hello zawartość log.txt, który zostanie zapisany formatu JSON, hello rejestrowania komunikatów, które zostały napisane co 5 sekund, przez moduł Hello World bramy hello.</span><span class="sxs-lookup"><span data-stu-id="d6516-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="d6516-176">![Widok katalogu log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="d6516-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="d6516-177">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d6516-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="d6516-178">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d6516-178">Summary</span></span>

<span data-ttu-id="d6516-179">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="d6516-179">Congratulations!</span></span> <span data-ttu-id="d6516-180">Po zakończeniu konfigurowania Intel NUC jako brama.</span><span class="sxs-lookup"><span data-stu-id="d6516-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="d6516-181">Teraz możesz już toomove na toohello dalej tooset lekcji komputera hosta tworzenia Centrum IoT Azure i rejestrowanie urządzenia logicznego centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="d6516-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6516-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6516-182">Next steps</span></span>
[<span data-ttu-id="d6516-183">Użyj IoT bramy tooconnect tooAzure urządzenia IoT Hub</span><span class="sxs-lookup"><span data-stu-id="d6516-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

