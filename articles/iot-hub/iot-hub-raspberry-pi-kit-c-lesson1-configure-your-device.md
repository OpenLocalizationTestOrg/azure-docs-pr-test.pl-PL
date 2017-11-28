---
title: "Connect Raspberry pi (C) do Azure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Skonfiguruj malina Pi 3 dla pierwszego użycia i zainstalować system operacyjny Raspbian wolnego systemu operacyjnego, który jest zoptymalizowana pod kątem sprzętu malina Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "raspbian instalacji, pobierania raspbian sposób instalowania raspbian, ustawienia raspbian, malinowe pi instalacji raspbian, os instalacji malinowe pi, zainstaluj karty sd malinowe pi, malina pi łączenia, nawiązać łączności pi malinowe pi malinowe"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2a380f78d67db47a0dcab5b90843404921510528
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="07825-104">Konfigurowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="07825-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="07825-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="07825-105">What you will do</span></span>
<span data-ttu-id="07825-106">Konfigurowanie Pi do pierwszego użycia i zainstaluj system operacyjny Raspbian.</span><span class="sxs-lookup"><span data-stu-id="07825-106">Configure Pi for first-time use and install the Raspbian operating system.</span></span> <span data-ttu-id="07825-107">Raspbian jest bezpłatna systemu operacyjnego, który jest zoptymalizowana pod kątem sprzętu malina Pi.</span><span class="sxs-lookup"><span data-stu-id="07825-107">Raspbian is a free operating system that is optimized for the Raspberry Pi hardware.</span></span> <span data-ttu-id="07825-108">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="07825-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="07825-109">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="07825-109">What you will learn</span></span>
<span data-ttu-id="07825-110">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="07825-110">In this article, you will learn:</span></span>

* <span data-ttu-id="07825-111">Jak zainstalować Raspbian na Pi.</span><span class="sxs-lookup"><span data-stu-id="07825-111">How to install Raspbian on Pi.</span></span>
* <span data-ttu-id="07825-112">Jak zasilanie Pi przy użyciu kabla USB.</span><span class="sxs-lookup"><span data-stu-id="07825-112">How to power up Pi by using a USB cable.</span></span>
* <span data-ttu-id="07825-113">Jak nawiązać Pi sieci za pomocą kabla Ethernet lub sieci bezprzewodowej.</span><span class="sxs-lookup"><span data-stu-id="07825-113">How to connect Pi to the network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="07825-114">Jak dodać diodę LED do breadboard i podłącz go do Pi.</span><span class="sxs-lookup"><span data-stu-id="07825-114">How to add an LED to the breadboard and connect it to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="07825-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="07825-115">What you need</span></span>
<span data-ttu-id="07825-116">Aby wykonać tę operację, potrzebne następujące części z Twojej malina Pi 3 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="07825-116">To complete this operation, you need the following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="07825-117">Tablica malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="07825-117">The Raspberry Pi 3 board</span></span>
* <span data-ttu-id="07825-118">Karta microSD 16 GB</span><span class="sxs-lookup"><span data-stu-id="07825-118">The 16-GB microSD card</span></span>
* <span data-ttu-id="07825-119">5 volt 2-amp zasilacz z stopy 6 micro kabla USB</span><span class="sxs-lookup"><span data-stu-id="07825-119">The 5-volt 2-amp power supply with the 6-foot micro USB cable</span></span>
* <span data-ttu-id="07825-120">Breadboard</span><span class="sxs-lookup"><span data-stu-id="07825-120">The breadboard</span></span>
* <span data-ttu-id="07825-121">Przewodów łącznika</span><span class="sxs-lookup"><span data-stu-id="07825-121">Connector wires</span></span>
* <span data-ttu-id="07825-122">Ohm — 560 opornikiem</span><span class="sxs-lookup"><span data-stu-id="07825-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="07825-123">Rozproszona LED 10 mm</span><span class="sxs-lookup"><span data-stu-id="07825-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="07825-124">Kabla Ethernet</span><span class="sxs-lookup"><span data-stu-id="07825-124">The Ethernet cable</span></span>

![Elementy w zestawie początkowy](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="07825-126">Wymagane są również:</span><span class="sxs-lookup"><span data-stu-id="07825-126">You also need:</span></span>

* <span data-ttu-id="07825-127">Połączenia przewodowe i bezprzewodowe pi nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="07825-127">A wired or wireless connection for Pi to connect to.</span></span>
* <span data-ttu-id="07825-128">USB-karty sieciowej lub mini SD na kartach SD Nagraj obraz systemu operacyjnego na karcie microSD.</span><span class="sxs-lookup"><span data-stu-id="07825-128">A USB-SD adapter or mini-SD card to burn the OS image onto the microSD card.</span></span>
* <span data-ttu-id="07825-129">Komputer z systemem Windows, Mac lub Linux.</span><span class="sxs-lookup"><span data-stu-id="07825-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="07825-130">Komputer jest używany do zainstalowania na karcie microSD Raspbian.</span><span class="sxs-lookup"><span data-stu-id="07825-130">The computer is used to install Raspbian on the microSD card.</span></span>
* <span data-ttu-id="07825-131">Połączenie internetowe, aby pobrać niezbędne narzędzia i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="07825-131">An Internet connection to download the necessary tools and software.</span></span>

## <a name="install-raspbian-on-the-microsd-card"></a><span data-ttu-id="07825-132">Zainstaluj na karcie MicroSD Raspbian</span><span class="sxs-lookup"><span data-stu-id="07825-132">Install Raspbian on the MicroSD card</span></span>
<span data-ttu-id="07825-133">Przygotuj karty microSD instalacji obrazu Raspbian.</span><span class="sxs-lookup"><span data-stu-id="07825-133">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="07825-134">Pobierz Raspbian.</span><span class="sxs-lookup"><span data-stu-id="07825-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="07825-135">[Pobierz](https://www.raspberrypi.org/downloads/raspbian/) pliku zip o Joasia Raspbian z pikseli.</span><span class="sxs-lookup"><span data-stu-id="07825-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) the .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="07825-136">Wyodrębnij obrazu Raspbian do folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="07825-136">Extract the Raspbian image to a folder on your computer.</span></span>
2. <span data-ttu-id="07825-137">Zainstaluj Raspbian karty microSD.</span><span class="sxs-lookup"><span data-stu-id="07825-137">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="07825-138">[Pobierz](https://www.etcher.io) i zainstaluj narzędzie palnika karty Etcher SD.</span><span class="sxs-lookup"><span data-stu-id="07825-138">[Download](https://www.etcher.io) and install the Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="07825-139">Uruchom Etcher i wybierz obraz Raspbian, który został wyodrębniony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="07825-139">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="07825-140">Wybierz dysk karty microSD.</span><span class="sxs-lookup"><span data-stu-id="07825-140">Select the microSD card drive.</span></span>
      <span data-ttu-id="07825-141">Należy pamiętać, że Etcher może już wybrane poprawnego dysku.</span><span class="sxs-lookup"><span data-stu-id="07825-141">Note that Etcher may have already selected the correct drive.</span></span>
   4. <span data-ttu-id="07825-142">Kliknij przycisk **Flash** instalowanie Raspbian karty microSD.</span><span class="sxs-lookup"><span data-stu-id="07825-142">Click **Flash** to install Raspbian to the microSD card.</span></span>
   5. <span data-ttu-id="07825-143">Karta microSD należy usunąć z komputera po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="07825-143">Remove the microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="07825-144">Jest bezpiecznie usunąć karta microSD bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karty microSD po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="07825-144">It is safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   6. <span data-ttu-id="07825-145">Włóż kartę microSD do Twojej Pi.</span><span class="sxs-lookup"><span data-stu-id="07825-145">Insert the microSD card into your Pi.</span></span>

![Włóż kartę SD.](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="07825-147">Włącz Pi</span><span class="sxs-lookup"><span data-stu-id="07825-147">Turn on Pi</span></span>
<span data-ttu-id="07825-148">Włącz Pi przy użyciu micro kabla USB i zasilania.</span><span class="sxs-lookup"><span data-stu-id="07825-148">Turn on Pi by using the micro USB cable and the power supply.</span></span>

![Włącz](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="07825-150">Ważne jest, aby używać źródła zasilania w zestawie, który jest co najmniej 2A, aby upewnić się, że Twoje malina ma wystarczająco dużo mocy działała prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="07825-150">It is important to use the power supply in the kit that is at least 2A to make sure that your Raspberry has enough power to work correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="07825-151">Włącz SSH</span><span class="sxs-lookup"><span data-stu-id="07825-151">Enable SSH</span></span>
<span data-ttu-id="07825-152">Począwszy od wersji listopada 2016 Raspbian zawiera serwer SSH, domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="07825-152">As of the November 2016 release, Raspbian has the SSH server disabled by default.</span></span> <span data-ttu-id="07825-153">Musisz włączyć ją ręcznie.</span><span class="sxs-lookup"><span data-stu-id="07825-153">You need to enable it manually.</span></span> <span data-ttu-id="07825-154">Można odwołać się do [oficjalnego instrukcje](https://www.raspberrypi.org/documentation/remote-access/ssh/) lub połączyć z monitorem i przejdź do **Preferencje -> Konfiguracja Pi malina** umożliwiające SSH.</span><span class="sxs-lookup"><span data-stu-id="07825-154">You can refer to the [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go to **Preferences -> Raspberry Pi Configuration** to enable SSH.</span></span>

## <a name="connect-raspberry-pi-3-to-the-network"></a><span data-ttu-id="07825-155">Połączenie z siecią 3 Pi malina</span><span class="sxs-lookup"><span data-stu-id="07825-155">Connect Raspberry Pi 3 to the network</span></span>
<span data-ttu-id="07825-156">Pi można podłączyć do sieci przewodowej lub bezprzewodowej sieci.</span><span class="sxs-lookup"><span data-stu-id="07825-156">You can connect Pi to a wired network or to a wireless network.</span></span> <span data-ttu-id="07825-157">Upewnij się, że Pi jest podłączony do sieci z komputera.</span><span class="sxs-lookup"><span data-stu-id="07825-157">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="07825-158">Na przykład można połączyć Pi do tego samego przełącznika, że komputer jest połączony.</span><span class="sxs-lookup"><span data-stu-id="07825-158">For example, you can connect Pi to the same switch that your computer is connected to.</span></span>

### <a name="connect-to-a-wired-network"></a><span data-ttu-id="07825-159">Podłącz do sieci przewodowej</span><span class="sxs-lookup"><span data-stu-id="07825-159">Connect to a wired network</span></span>
<span data-ttu-id="07825-160">Podłącz Pi do sieci przewodowej za pomocą kabla Ethernet.</span><span class="sxs-lookup"><span data-stu-id="07825-160">Use the Ethernet cable to connect Pi to your wired network.</span></span> <span data-ttu-id="07825-161">Dwa LED na Pi włączyć, jeśli połączenie zostanie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="07825-161">The two LEDs on Pi turn on if the connection is established.</span></span>

![Połącz za pomocą kabla Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-to-a-wireless-network"></a><span data-ttu-id="07825-163">Połącz się z siecią bezprzewodową</span><span class="sxs-lookup"><span data-stu-id="07825-163">Connect to a wireless network</span></span>
<span data-ttu-id="07825-164">Postępuj zgodnie z [instrukcje](https://www.raspberrypi.org/learning/software-guide/wifi/) z malina Foundation Pi do Pi nawiązania połączenia z siecią bezprzewodową.</span><span class="sxs-lookup"><span data-stu-id="07825-164">Follow the [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from the Raspberry Pi Foundation to connect Pi to your wireless network.</span></span> <span data-ttu-id="07825-165">Te instrukcje trzeba najpierw połączyć monitora i klawiatury do Pi.</span><span class="sxs-lookup"><span data-stu-id="07825-165">These instructions require you to first connect a monitor and a keyboard to Pi.</span></span>

## <a name="connect-the-led-to-pi"></a><span data-ttu-id="07825-166">Nawiązać LED Pi</span><span class="sxs-lookup"><span data-stu-id="07825-166">Connect the LED to Pi</span></span>
<span data-ttu-id="07825-167">Aby wykonać to zadanie, należy użyć [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), przewodów łącznika, LED i opornik.</span><span class="sxs-lookup"><span data-stu-id="07825-167">To complete this task, use the [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), the connector wires, the LED, and the resistor.</span></span> <span data-ttu-id="07825-168">Podłącz je do [ogólnego przeznaczenia wejścia/wyjścia](https://www.raspberrypi.org/documentation/usage/gpio/) portów (interfejs GPIO) pi.</span><span class="sxs-lookup"><span data-stu-id="07825-168">Connect them to the [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Breadboard LED i rezystor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="07825-170">Połącz krótszą etap LED do **GND interfejs GPIO (numer Pin 6)**.</span><span class="sxs-lookup"><span data-stu-id="07825-170">Connect the shorter leg of the LED to **GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="07825-171">Etap dłużej LED nawiązać połączenia z jednym etap opornik.</span><span class="sxs-lookup"><span data-stu-id="07825-171">Connect the longer leg of the LED to one leg of the resistor.</span></span>
3. <span data-ttu-id="07825-172">Połącz innych etap opornik do **interfejs GPIO 4 (numer Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="07825-172">Connect the other leg of the resistor to **GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="07825-173">Należy pamiętać, że bieguna LED ważne.</span><span class="sxs-lookup"><span data-stu-id="07825-173">Note that the LED polarity is important.</span></span> <span data-ttu-id="07825-174">To ustawienie bieguna jest często nazywana Active niski.</span><span class="sxs-lookup"><span data-stu-id="07825-174">This polarity setting is commonly known as Active Low.</span></span>

![Szablon](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="07825-176">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="07825-176">Congratulations!</span></span> <span data-ttu-id="07825-177">Pomyślnie skonfigurowano Pi.</span><span class="sxs-lookup"><span data-stu-id="07825-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="07825-178">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="07825-178">Summary</span></span>
<span data-ttu-id="07825-179">W tym artykule kiedy znasz już sposobu konfigurowania Pi przez zainstalowanie Raspbian, Pi nawiązywania połączenia z siecią i nawiązywanie LED Pi.</span><span class="sxs-lookup"><span data-stu-id="07825-179">In this article, you’ve learned how to configure Pi by installing Raspbian, connecting Pi to a network, and connecting an LED to Pi.</span></span> <span data-ttu-id="07825-180">Należy pamiętać, że jeszcze nie podświetlony LED.</span><span class="sxs-lookup"><span data-stu-id="07825-180">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="07825-181">Następne zadanie jest Zainstaluj niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia aplikacji przykładowej na Pi.</span><span class="sxs-lookup"><span data-stu-id="07825-181">The next task is to install the necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Sprzęt jest gotowy](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="07825-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07825-183">Next steps</span></span>
[<span data-ttu-id="07825-184">Pobierz narzędzia</span><span class="sxs-lookup"><span data-stu-id="07825-184">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

