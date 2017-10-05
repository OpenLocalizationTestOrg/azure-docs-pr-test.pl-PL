---
title: "Urządzeń Sensor tag & Azure IoT bramy - Lekcja 1: Konfigurowanie Intel NUC | Dokumentacja firmy Microsoft"
description: "Skonfigurować Intel NUC do pracy jako bramy IoT między czujników i Centrum IoT Azure do zbierania informacji z czujnika i wysyłania go do Centrum IoT."
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
ms.openlocfilehash: 1a3a92ab8d08c6ed6f047208217c46022027157e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="a7a0a-104">Konfigurowanie Intel NUC jako brama IoT</span><span class="sxs-lookup"><span data-stu-id="a7a0a-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="a7a0a-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="a7a0a-105">What you will do</span></span>

- <span data-ttu-id="a7a0a-106">Ustawienie Intel NUC jako bramę IoT.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="a7a0a-107">Zainstaluj pakiet Azure IoT Edge na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-107">Install the Azure IoT Edge package on the Intel NUC.</span></span>
- <span data-ttu-id="a7a0a-108">Uruchom przykładową aplikację "hello_world" na NUC firmy Intel, aby sprawdzić funkcjonalność bramy.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-108">Run a "hello_world" sample application on the Intel NUC to verify the gateway functionality.</span></span>

  > <span data-ttu-id="a7a0a-109">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a7a0a-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a7a0a-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="a7a0a-110">What you will learn</span></span>

<span data-ttu-id="a7a0a-111">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="a7a0a-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="a7a0a-112">Jak nawiązać połączenia z urządzeń peryferyjnych Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="a7a0a-113">Sposób instalacji i aktualizacji wymaganych pakietów na NUC Intel pomocą inteligentne Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="a7a0a-114">Jak uruchomić "hello_world" przykładowej aplikacji, aby sprawdzić funkcjonalność bramy.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a7a0a-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="a7a0a-115">What you need</span></span>

- <span data-ttu-id="a7a0a-116">Intel NUC Kit DE3815TYKE z pakietem oprogramowania bramy IoT firmy Intel (Linux rzeki knie * 7.0.0.13) preinstalowany.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="a7a0a-117">[Kliknij tutaj, aby kupić Grove IoT komercyjnych bramy zestaw](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="a7a0a-117">[Click here to purchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="a7a0a-118">Kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-118">An Ethernet cable.</span></span>
- <span data-ttu-id="a7a0a-119">Klawiatury.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-119">A keyboard.</span></span>
- <span data-ttu-id="a7a0a-120">Kabel HDMI lub VGA.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="a7a0a-121">Monitor portu HDMI lub VGA.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="a7a0a-122">Opcjonalnie: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="a7a0a-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Zestaw bramy](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="a7a0a-124">Połącz z urządzeniami peryferyjnymi Intel NUC</span><span class="sxs-lookup"><span data-stu-id="a7a0a-124">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="a7a0a-125">Na poniższym obrazie przedstawiono przykładowy NUC firmy Intel, który jest połączony z różnych urządzeń peryferyjnych:</span><span class="sxs-lookup"><span data-stu-id="a7a0a-125">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="a7a0a-126">Podłączona do klawiatury.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-126">Connected to a keyboard.</span></span>
2. <span data-ttu-id="a7a0a-127">Połączona z monitorem za pomocą kabla VGA lub kabla HDMI.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-127">Connected to a monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="a7a0a-128">Podłączony do sieci przewodowej za pomocą kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-128">Connected to a wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="a7a0a-129">Podłączone do źródła zasilania, za pomocą kabla zasilania.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-129">Connected to a power supply with a power cable.</span></span>

![Połączone dla urządzeń peryferyjnych NUC Intel](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="a7a0a-131">Połączyć się z systemem Intel NUC z komputera hosta za pośrednictwem protokołu Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="a7a0a-131">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="a7a0a-132">Konieczne będzie, klawiatury i monitora, aby uzyskać adres IP urządzenia Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-132">You will need a keyboard and a monitor to get the IP address of your Intel NUC device.</span></span> <span data-ttu-id="a7a0a-133">Jeśli znasz już adres IP, możesz przejść od razu do kroku 3 w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-133">If you already know the IP address, you can skip ahead to step 3 in this section.</span></span>

1. <span data-ttu-id="a7a0a-134">Włącz NUC firmy Intel, naciskając przycisk zasilania, a następnie zaloguj.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-134">Turn on the Intel NUC by pressing the power button and then log in.</span></span>

   <span data-ttu-id="a7a0a-135">Domyślna nazwa użytkownika i hasło są `root`.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-135">The default user name and password are both `root`.</span></span>

       > Hit the enter key on your keyboard if you see either of the following errors when you boot: 'A TPM error (7) occurred attempting to read a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="a7a0a-136">Uzyskaj adres IP NUC firmy Intel, uruchamiając `ifconfig` polecenia na urządzeniu Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-136">Get the IP address of the Intel NUC by running the `ifconfig` command on the Intel NUC device.</span></span>

   <span data-ttu-id="a7a0a-137">Oto przykład danych wyjściowych polecenia.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-137">Here is an example of the command output.</span></span>

   ![dane wyjściowe ifconfig przedstawiający Intel NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="a7a0a-139">W tym przykładzie wartość następujący `inet addr:` to adres IP, do którego należy, gdy nawiązać Intel NUC z komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-139">In this example, the value that follows `inet addr:` is the IP address that you need when connect to the Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="a7a0a-140">Do nawiązania połączenia NUC firmy Intel, użyj jednej z następujących klientów SSH z komputera hosta.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-140">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span></span>

    - <span data-ttu-id="a7a0a-141">[PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="a7a0a-142">Wbudowane SSH klient Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-142">The built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="a7a0a-143">Jest bardziej wydajny i produktywności działanie NUC Intel z komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-143">It is more efficient and productive to operate an Intel NUC from a host computer.</span></span> <span data-ttu-id="a7a0a-144">Będziesz potrzebować Intel NUC adres IP, nazwę użytkownika i hasło, aby połączyć przy użyciu klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-144">You'll need the Intel NUC's IP address, user name and password to connect to it via an SSH client.</span></span> <span data-ttu-id="a7a0a-145">Oto przykład, które używa klienta SSH w macOS.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="a7a0a-146">![Klient SSH systemem macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="a7a0a-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="a7a0a-147">Zainstaluj pakiet Azure IoT krawędzi</span><span class="sxs-lookup"><span data-stu-id="a7a0a-147">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="a7a0a-148">Pakiet Azure IoT krawędzi zawiera wstępnie skompilowanych plików binarnych krawędzi IoT i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-148">The Azure IoT Edge package contains the pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="a7a0a-149">Te pliki binarne są Azure IoT krawędzi, zestaw SDK usługi Azure IoT i odpowiednie narzędzia.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-149">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="a7a0a-150">Pakiet zawiera również "hello_world" przykładowej aplikacji jest używany do sprawdzania poprawności funkcje bramy.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-150">The package also contains a "hello_world" sample application is used to validate the gateway functionality.</span></span> <span data-ttu-id="a7a0a-151">Krawędź IoT jest główną część bramy.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-151">IoT Edge is the core part of the gateway.</span></span> 

<span data-ttu-id="a7a0a-152">Wykonaj następujące kroki, aby zainstalować pakiet.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-152">Follow these steps to install the package.</span></span>

1. <span data-ttu-id="a7a0a-153">Dodaj repozytorium chmury IoT, uruchamiając następujące polecenia w oknie terminala:</span><span class="sxs-lookup"><span data-stu-id="a7a0a-153">Add the IoT Cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="a7a0a-154">Wprowadź "y", gdy monit o "Zawierać ten kanał?"</span><span class="sxs-lookup"><span data-stu-id="a7a0a-154">Enter 'y', when it prompts you to 'Include this channel?'</span></span>
   
   <span data-ttu-id="a7a0a-155">Jeśli zostanie wyświetlony `import read failed(-1)` błędu, aby rozwiązać ten problem należy użyć następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="a7a0a-155">If you receive an `import read failed(-1)` error, use the following commands to resolve the issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="a7a0a-156">`rpm` Polecenie importuje klucz obr. / min.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-156">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="a7a0a-157">`smart channel` Polecenie dodaje kanału obr. / min na inteligentne Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-157">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="a7a0a-158">Przed uruchomieniem `smart update` polecenia, zostanie wyświetlony wyjścia, takich jak poniżej.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-158">Before you run the `smart update` command, you will see an output like below.</span></span>

   ![obr. / min i dane wyjściowe polecenia inteligentne kanału](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="a7a0a-160">Wykonanie polecenia update inteligentnych:</span><span class="sxs-lookup"><span data-stu-id="a7a0a-160">Execute the smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="a7a0a-161">Zainstaluj pakiet Azure IoT bramy, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a7a0a-161">Install the Azure IoT Gateway package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="a7a0a-162">`packagegroup-cloud-azure`to nazwa pakietu.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-162">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="a7a0a-163">`smart install` Polecenie służy do zainstalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-163">The `smart install` command is used to install the package.</span></span>

    > <span data-ttu-id="a7a0a-164">Jeśli zostanie wyświetlony ten błąd, uruchom następujące polecenie: "klucz publiczny nie jest dostępna"</span><span class="sxs-lookup"><span data-stu-id="a7a0a-164">Run the following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="a7a0a-165">Ponowny rozruch NUC firmy Intel, jeśli zostanie wyświetlony ten błąd: "nie zawiera util-linux deweloperów"</span><span class="sxs-lookup"><span data-stu-id="a7a0a-165">Reboot the Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="a7a0a-166">Po zainstalowaniu pakietu Intel NUC jest gotowy do działania jako brama.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-166">After the package is installed, Intel NUC is ready to function as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="a7a0a-167">Uruchom przykładową aplikację "hello_world" krawędzi IoT Azure</span><span class="sxs-lookup"><span data-stu-id="a7a0a-167">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="a7a0a-168">Następujące przykładowej aplikacji tworzy bramę z `hello_world.json` pliku i używa podstawowych składników architektury Azure IoT Edge, aby wiadomość hello world w pliku dziennika (log.txt) co 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-168">The following sample application creates a gateway from a `hello_world.json` file and uses the fundamental components of Azure IoT Edge architecture to log a hello world message to a file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="a7a0a-169">Przykład Witaj świecie można uruchomić, wykonując następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="a7a0a-169">You can run the Hello World sample by executing the following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="a7a0a-170">Zezwalaj aplikacji Hello World Uruchom kilka minut, a następnie naciśnij klawisz Enter, aby ją zatrzymać.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-170">Let the Hello World application run for a few minutes and then hit the Enter key to stop it.</span></span>
<span data-ttu-id="a7a0a-171">![dane wyjściowe aplikacji](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="a7a0a-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="a7a0a-172">Możesz zignorować wszelkie błędy "handle(NULL) nieprawidłowy argument", które są wyświetlane po naciśnięciu przycisku Enter.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="a7a0a-173">Możesz sprawdzić, czy brama zostało wykonane pomyślnie, otwierając plik log.txt, która jest teraz w folderze hello_world ![log.txt widok katalogu](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="a7a0a-173">You can verify that the gateway ran successfully by opening the log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="a7a0a-174">Otwórz log.txt za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a7a0a-174">Open log.txt using the following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="a7a0a-175">Zostanie wtedy wyświetlone zawartość log.txt, który zostanie zapisany formatu JSON, wiadomości rejestrowanie, które zostały napisane co 5 sekund, przez moduł Hello World bramy.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-175">You will then see the contents of log.txt, which will be a JSON formatted output of the logging messages that were written every 5 seconds by the gateway Hello World module.</span></span>
<span data-ttu-id="a7a0a-176">![Widok katalogu log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="a7a0a-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="a7a0a-177">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a7a0a-177">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="a7a0a-178">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a7a0a-178">Summary</span></span>

<span data-ttu-id="a7a0a-179">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="a7a0a-179">Congratulations!</span></span> <span data-ttu-id="a7a0a-180">Po zakończeniu konfigurowania Intel NUC jako brama.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="a7a0a-181">Teraz możesz przejść do następnej lekcji, aby skonfigurować komputer hosta, tworzenia Centrum IoT Azure i zarejestrować urządzenie logiczne Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="a7a0a-181">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7a0a-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a7a0a-182">Next steps</span></span>
[<span data-ttu-id="a7a0a-183">Użyj bramy IoT połączenia z urządzeniem z Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="a7a0a-183">Use an IoT gateway to connect a device to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

