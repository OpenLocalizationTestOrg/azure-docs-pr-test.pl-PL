---
title: "Symulowane urządzenie & Azure IoT bramy - Lekcja 1: Konfigurowanie NUC | Dokumentacja firmy Microsoft"
description: "Ustawienie toowork Intel NUC jako bramy IoT między czujników i informacji z czujnika toocollect Centrum IoT Azure i wysyłać je tooIoT koncentratora."
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
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="2bcdd-104">Konfigurowanie Intel NUC jako brama IoT</span><span class="sxs-lookup"><span data-stu-id="2bcdd-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="2bcdd-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="2bcdd-105">What you will do</span></span>

- <span data-ttu-id="2bcdd-106">Ustawienie Intel NUC jako bramę IoT.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="2bcdd-107">Zainstaluj pakiet Azure IoT krawędzi hello na Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="2bcdd-108">Uruchom przykładową aplikację "hello_world" na funkcjonalność bramy hello tooverify Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="2bcdd-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2bcdd-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2bcdd-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="2bcdd-110">What you will learn</span></span>

<span data-ttu-id="2bcdd-111">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="2bcdd-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="2bcdd-112">Jak tooconnect Intel NUC z urządzenia peryferyjne.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="2bcdd-113">Jak pakietów hello wymagane tooinstall i aktualizacji przy użyciu Intel NUC hello inteligentne Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="2bcdd-114">Jak toorun hello "hello_world" Przykładowe funkcjonalność bramy hello tooverify aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2bcdd-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="2bcdd-115">What you need</span></span>

- <span data-ttu-id="2bcdd-116">Intel NUC Kit DE3815TYKE z hello pakiet oprogramowania bramy IoT firmy Intel (Linux rzeki knie * 7.0.0.13) preinstalowany.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="2bcdd-117">Kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-117">An Ethernet cable.</span></span>
- <span data-ttu-id="2bcdd-118">Klawiatury.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-118">A keyboard.</span></span>
- <span data-ttu-id="2bcdd-119">Kabel HDMI lub VGA.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="2bcdd-120">Monitor portu HDMI lub VGA.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-120">A monitor with an HDMI or VGA port.</span></span>

![Zestaw bramy](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="2bcdd-122">Intel NUC Uzyskuj dostęp do urządzeń peryferyjnych hello</span><span class="sxs-lookup"><span data-stu-id="2bcdd-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="2bcdd-123">Obraz powitania poniżej przedstawiono przykładowy NUC firmy Intel, który jest połączony z różnych urządzeń peryferyjnych:</span><span class="sxs-lookup"><span data-stu-id="2bcdd-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="2bcdd-124">Klawiatura tooa połączonych.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="2bcdd-125">Połączone monitor toohello kabel VGA lub kabla HDMI.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="2bcdd-126">Połączone tooa ich z przewodową siecią przez kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="2bcdd-127">Zasilacz toohello połączonych za pomocą kabla zasilania.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-127">Connected toohello power supply with a power cable.</span></span>

![Tooperipherals NUC Intel połączone](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="2bcdd-129">Połącz system Intel NUC toohello z komputera hosta za pośrednictwem protokołu Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="2bcdd-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="2bcdd-130">W tym miejscu należy klawiatury i monitora tooget hello adres IP urządzenia NUC.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="2bcdd-131">Jeśli znasz już hello IP adresu, możesz pominąć toostep 3 w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="2bcdd-132">Włącz NUC firmy Intel, naciskając przycisk zasilania hello i dziennika w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="2bcdd-133">Hello domyślna nazwa użytkownika i hasło są `root`.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="2bcdd-134">Uzyskaj adres IP hello NUC uruchamiając hello `ifconfig` polecenia.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="2bcdd-135">Ten krok jest wykonywana na powitania NUC urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="2bcdd-136">Oto przykład danych wyjściowych polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-136">Here is an example of hello command output.</span></span>

   ![dane wyjściowe ifconfig przedstawiający NUC IP](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="2bcdd-138">W tym przykładzie hello wartość, która wykonuje `inet addr:` jest adresem IP hello potrzebne, planując tooconnect zdalnie z tooIntel komputera hosta NUC.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="2bcdd-139">Użyj jednej z hello poniższych klientów SSH z tooIntel tooconnect NUC z hosta maszyny.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="2bcdd-140">[PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="2bcdd-141">Witaj w kompilacji SSH klient Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="2bcdd-142">Jest bardziej wydajny i produktywności toooperate na Intel NUC z komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="2bcdd-143">Potrzebujesz adresu IP hello hello, nazwę użytkownika i hasło tooconnect hello NUC przy użyciu klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="2bcdd-144">Oto klienta SSH Użyj przykład hello na macOS.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="2bcdd-145">![Klient SSH systemem macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="2bcdd-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="2bcdd-146">Zainstaluj pakiet Azure IoT krawędzi hello</span><span class="sxs-lookup"><span data-stu-id="2bcdd-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="2bcdd-147">Pakiet Azure IoT krawędzi Hello zawiera hello wstępnie skompilowanych plików binarnych hello zestawu SDK i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="2bcdd-148">Te pliki binarne są Azure IoT krawędzi, hello Azure IoT SDK i narzędzia odpowiednie hello.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="2bcdd-149">Pakiet HELLO zawiera również "hello_world" przykładowej aplikacji, która jest funkcjonalność bramy hello toovalidate używane.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="2bcdd-150">Krawędź IoT jest hello główną część hello bramy.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="2bcdd-151">Witaj tooinstall pakiet, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2bcdd-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="2bcdd-152">Dodaj hello IoT chmury repozytorium, uruchamiając następujące polecenia w oknie terminalu hello:</span><span class="sxs-lookup"><span data-stu-id="2bcdd-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="2bcdd-153">Witaj `rpm` polecenie importuje hello klucza obr. / min.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="2bcdd-154">Witaj `smart channel` polecenie dodaje hello rpm kanału toohello inteligentne Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="2bcdd-155">Przed rozpoczęciem powitalne `smart update` polecenia, zobacz dane wyjściowe podobne poniżej.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![obr. / min i dane wyjściowe polecenia inteligentne kanału](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="2bcdd-157">Instalacja pakietu hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2bcdd-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="2bcdd-158">`packagegroup-cloud-azure`jest nazwą hello hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="2bcdd-159">Witaj `smart install` polecenia jest używane tooinstall hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="2bcdd-160">Po zainstalowaniu pakietu hello Intel NUC jest oczekiwany toowork jako brama.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="2bcdd-161">Uruchom hello Azure IoT krawędzi "hello_world" przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="2bcdd-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="2bcdd-162">Przejdź do zbyt`azureiotgatewaysdk/samples` i uruchom hello próbki "hello_world" przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="2bcdd-163">Ta przykładowa aplikacja tworzy bramę z hello `hello_world.json` pliku i używa podstawowych składników hello Azure IoT krawędzi architektura toolog pliku tooa wiadomość hello world hello co 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="2bcdd-164">Hello próbki "hello_world" przykładową aplikację można uruchomić, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2bcdd-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="2bcdd-165">Witaj przykładowej aplikacji daje następujące hello wyniki, jeśli hello funkcjonalność bramy działa prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="2bcdd-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![dane wyjściowe aplikacji](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="2bcdd-167">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2bcdd-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="2bcdd-168">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="2bcdd-168">Summary</span></span>

<span data-ttu-id="2bcdd-169">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="2bcdd-169">Congratulations!</span></span> <span data-ttu-id="2bcdd-170">Po zakończeniu konfigurowania Intel NUC jako brama.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="2bcdd-171">Teraz wszystko jest gotowe toomove na toohello dalej tooset lekcji komputera hosta utworzyć Centrum Azure IoT i zarejestrować urządzenia logicznego centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="2bcdd-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bcdd-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2bcdd-172">Next steps</span></span>
[<span data-ttu-id="2bcdd-173">Przygotuj komputer hosta, a następnie Centrum Azure IoT</span><span class="sxs-lookup"><span data-stu-id="2bcdd-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
