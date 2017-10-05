---
title: "Symulowane urządzenie & Azure IoT bramy - Lekcja 1: Konfigurowanie NUC | Dokumentacja firmy Microsoft"
description: "Skonfigurować Intel NUC do pracy jako bramy IoT między czujników i Centrum IoT Azure do zbierania informacji z czujnika i wysyłania go do Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: iot bramy intel nuc nuc komputera, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="4dbc5-104">Konfigurowanie Intel NUC jako brama IoT</span><span class="sxs-lookup"><span data-stu-id="4dbc5-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4dbc5-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="4dbc5-105">What you will do</span></span>

- <span data-ttu-id="4dbc5-106">Ustawienie Intel NUC jako bramę IoT.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="4dbc5-107">Zainstaluj pakiet Azure IoT Edge na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="4dbc5-108">Uruchom przykładową aplikację "hello_world" na NUC firmy Intel, aby sprawdzić funkcjonalność bramy.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="4dbc5-109">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4dbc5-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4dbc5-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="4dbc5-110">What you will learn</span></span>

<span data-ttu-id="4dbc5-111">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="4dbc5-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="4dbc5-112">Jak nawiązać połączenia z urządzeń peryferyjnych Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="4dbc5-113">Sposób instalacji i aktualizacji wymaganych pakietów na NUC Intel pomocą inteligentne Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="4dbc5-114">Jak uruchomić "hello_world" przykładowej aplikacji, aby sprawdzić funkcjonalność bramy.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4dbc5-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="4dbc5-115">What you need</span></span>

- <span data-ttu-id="4dbc5-116">Intel NUC Kit DE3815TYKE z pakietem oprogramowania bramy IoT firmy Intel (Linux rzeki knie * 7.0.0.13) preinstalowany.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="4dbc5-117">Kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-117">An Ethernet cable.</span></span>
- <span data-ttu-id="4dbc5-118">Klawiatury.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-118">A keyboard.</span></span>
- <span data-ttu-id="4dbc5-119">Kabel HDMI lub VGA.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="4dbc5-120">Monitor portu HDMI lub VGA.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-120">A monitor with an HDMI or VGA port.</span></span>

![Zestaw bramy](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="4dbc5-122">Połącz z urządzeniami peryferyjnymi Intel NUC</span><span class="sxs-lookup"><span data-stu-id="4dbc5-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="4dbc5-123">Na poniższym obrazie przedstawiono przykładowy NUC firmy Intel, który jest połączony z różnych urządzeń peryferyjnych:</span><span class="sxs-lookup"><span data-stu-id="4dbc5-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="4dbc5-124">Podłączona do klawiatury.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="4dbc5-125">Połączenie monitor przez kabel VGA lub kabla HDMI.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="4dbc5-126">Połączone z siecią przewodową za kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="4dbc5-127">Podłączone do źródła zasilania, za pomocą kabla zasilania.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-127">Connected to the power supply with a power cable.</span></span>

![Połączone dla urządzeń peryferyjnych NUC Intel](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="4dbc5-129">Połączyć się z systemem Intel NUC z komputera hosta za pośrednictwem protokołu Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="4dbc5-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="4dbc5-130">W tym miejscu należy klawiatury i monitora, aby uzyskać adres IP urządzenia NUC.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="4dbc5-131">Jeśli już znasz adres IP, należy przejść do kroku 3 w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="4dbc5-132">Włącz NUC firmy Intel, naciskając przycisk zasilania i logowania w systemie.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="4dbc5-133">Domyślna nazwa użytkownika i hasło są `root`.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="4dbc5-134">Uzyskaj adres IP NUC uruchamiając `ifconfig` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="4dbc5-135">Ten krok jest realizowane na urządzeniu NUC.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="4dbc5-136">Oto przykład danych wyjściowych polecenia.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-136">Here is an example of the command output.</span></span>

   ![dane wyjściowe ifconfig przedstawiający NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="4dbc5-138">W tym przykładzie wartość następujący `inet addr:` to adres IP, do którego należy, jeśli planujesz łączyć się zdalnie z komputera-hosta Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="4dbc5-139">Do nawiązania połączenia NUC firmy Intel, użyj jednej z następujących klientów SSH z komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="4dbc5-140">[PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="4dbc5-141">Kompilacji w SSH klient Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="4dbc5-142">Jest bardziej wydajny i produktywności do działania na Intel NUC z komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="4dbc5-143">Potrzebujesz adresu IP, nazwę użytkownika i hasło, aby połączyć NUC przy użyciu klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="4dbc5-144">Oto przykład użycia SSH klient, na macOS.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="4dbc5-145">![Klient SSH systemem macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="4dbc5-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="4dbc5-146">Zainstaluj pakiet Azure IoT krawędzi</span><span class="sxs-lookup"><span data-stu-id="4dbc5-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="4dbc5-147">Pakiet Azure IoT krawędzi zawiera wstępnie skompilowanych plików binarnych zestawu SDK i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="4dbc5-148">Te pliki binarne są Azure IoT krawędzi, zestaw SDK usługi Azure IoT i odpowiednie narzędzia.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="4dbc5-149">Pakiet zawiera również "hello_world" przykładowej aplikacji, która służy do sprawdzania poprawności funkcje bramy.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="4dbc5-150">Krawędź IoT jest główną część bramy.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="4dbc5-151">Aby zainstalować pakiet, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4dbc5-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="4dbc5-152">Dodaj repozytorium chmury IoT, uruchamiając następujące polecenia w oknie terminala:</span><span class="sxs-lookup"><span data-stu-id="4dbc5-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="4dbc5-153">`rpm` Polecenie importuje klucz obr. / min.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="4dbc5-154">`smart channel` Polecenie dodaje kanału obr. / min na inteligentne Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="4dbc5-155">Przed uruchomieniem `smart update` polecenia, zobacz dane wyjściowe podobne poniżej.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![obr. / min i dane wyjściowe polecenia inteligentne kanału](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="4dbc5-157">Zainstaluj pakiet, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4dbc5-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="4dbc5-158">`packagegroup-cloud-azure`to nazwa pakietu.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="4dbc5-159">`smart install` Polecenie służy do zainstalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="4dbc5-160">Po zainstalowaniu pakietu Intel NUC powinien działać jako brama.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="4dbc5-161">Uruchom przykładową aplikację "hello_world" krawędzi IoT Azure</span><span class="sxs-lookup"><span data-stu-id="4dbc5-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="4dbc5-162">Przejdź do `azureiotgatewaysdk/samples` i uruchomić przykładowe "hello_world" przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="4dbc5-163">Ta przykładowa aplikacja tworzy bramę z `hello_world.json` pliku i używa podstawowych składników architektury Azure IoT Edge, aby wiadomość hello world w pliku dziennika co 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="4dbc5-164">Przykładowe "hello_world" przykładową aplikację można uruchomić, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4dbc5-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="4dbc5-165">Przykładowa aplikacja tworzy następujące dane wyjściowe, jeśli funkcję bramy działa prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="4dbc5-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![dane wyjściowe aplikacji](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="4dbc5-167">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4dbc5-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="4dbc5-168">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4dbc5-168">Summary</span></span>

<span data-ttu-id="4dbc5-169">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="4dbc5-169">Congratulations!</span></span> <span data-ttu-id="4dbc5-170">Po zakończeniu konfigurowania Intel NUC jako brama.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="4dbc5-171">Teraz możesz przejść do następnej lekcji, aby skonfigurować komputer hosta, tworzenia Centrum Azure IoT i zarejestrować urządzenia logicznego centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="4dbc5-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dbc5-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4dbc5-172">Next steps</span></span>
[<span data-ttu-id="4dbc5-173">Przygotuj komputer hosta, a następnie Centrum Azure IoT</span><span class="sxs-lookup"><span data-stu-id="4dbc5-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
