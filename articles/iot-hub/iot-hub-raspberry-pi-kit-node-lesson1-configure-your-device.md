---
title: "Połącz Pi malina (węzeł) tooAzure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie malina Pi 3 do pierwszego użycia i zainstaluj hello Raspbian systemu operacyjnego, bezpłatna systemu operacyjnego, który jest zoptymalizowana pod kątem hello Pi malina sprzętu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "raspbian instalacji, pobierania raspbian sposób łączenia raspbian Instalatora malinowe pi instalacji raspbian malinowe pi instalacji systemu operacyjnego, malinowe pi sd karty instalacji malinowe pi tooinstall raspbian połączyć tooraspberry pi malinowe pi łączność"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 43f7c2cf-f1a5-4dd5-93f0-7e546c6dc91e
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 504a4d2a3f29717f955530812442cce2a78a6448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="61bf8-104">Konfigurowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="61bf8-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="61bf8-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="61bf8-105">What you will do</span></span>
<span data-ttu-id="61bf8-106">Konfigurowanie Pi do pierwszego użycia i zainstaluj system operacyjny Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="61bf8-106">Configure Pi for first-time use and install hello Raspbian operating system.</span></span> <span data-ttu-id="61bf8-107">Raspbian jest bezpłatna systemu operacyjnego, który jest zoptymalizowana pod kątem hello Pi malina sprzętu.</span><span class="sxs-lookup"><span data-stu-id="61bf8-107">Raspbian is a free operating system that is optimized for hello Raspberry Pi hardware.</span></span> <span data-ttu-id="61bf8-108">Jeśli masz problemy można wyszukiwać rozwiązań na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="61bf8-108">If you have any problems, you can seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="61bf8-109">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="61bf8-109">What you will learn</span></span>
<span data-ttu-id="61bf8-110">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="61bf8-110">In this article, you will learn:</span></span>

* <span data-ttu-id="61bf8-111">Jak tooinstall Raspbian na Pi.</span><span class="sxs-lookup"><span data-stu-id="61bf8-111">How tooinstall Raspbian on Pi.</span></span>
* <span data-ttu-id="61bf8-112">Jak toopower się Pi przy użyciu kabla USB.</span><span class="sxs-lookup"><span data-stu-id="61bf8-112">How toopower up Pi by using a USB cable.</span></span>
* <span data-ttu-id="61bf8-113">Jak tooconnect Pi toohello sieci za pomocą kabla Ethernet lub sieci bezprzewodowej.</span><span class="sxs-lookup"><span data-stu-id="61bf8-113">How tooconnect Pi toohello network by using an Ethernet cable or wireless network.</span></span>
* <span data-ttu-id="61bf8-114">Jak breadboard tooadd toohello LED i podłącz go tooPi.</span><span class="sxs-lookup"><span data-stu-id="61bf8-114">How tooadd an LED toohello breadboard and connect it tooPi.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="61bf8-115">Dane będą potrzebne</span><span class="sxs-lookup"><span data-stu-id="61bf8-115">What you will need</span></span>
<span data-ttu-id="61bf8-116">toocomplete tej operacji, należy po części z Twojej malina Pi 3 Starter Kit hello:</span><span class="sxs-lookup"><span data-stu-id="61bf8-116">toocomplete this operation, you need hello following parts from your Raspberry Pi 3 Starter Kit:</span></span>

* <span data-ttu-id="61bf8-117">Witaj tablicy malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="61bf8-117">hello Raspberry Pi 3 board</span></span>
* <span data-ttu-id="61bf8-118">Karta microSD 16 GB Hello</span><span class="sxs-lookup"><span data-stu-id="61bf8-118">hello 16-GB microSD card</span></span>
* <span data-ttu-id="61bf8-119">Hello 5 volt 2-amp zasilacz za hello stopy 6 micro kabla USB</span><span class="sxs-lookup"><span data-stu-id="61bf8-119">hello 5-volt 2-amp power supply with hello 6-foot micro USB cable</span></span>
* <span data-ttu-id="61bf8-120">Witaj breadboard</span><span class="sxs-lookup"><span data-stu-id="61bf8-120">hello breadboard</span></span>
* <span data-ttu-id="61bf8-121">Przewodów łącznika</span><span class="sxs-lookup"><span data-stu-id="61bf8-121">Connector wires</span></span>
* <span data-ttu-id="61bf8-122">Ohm — 560 opornikiem</span><span class="sxs-lookup"><span data-stu-id="61bf8-122">A 560-ohm resistor</span></span>
* <span data-ttu-id="61bf8-123">Rozproszona LED 10 mm</span><span class="sxs-lookup"><span data-stu-id="61bf8-123">A diffused 10-mm LED</span></span>
* <span data-ttu-id="61bf8-124">Witaj kabla Ethernet</span><span class="sxs-lookup"><span data-stu-id="61bf8-124">hello Ethernet cable</span></span>

![Elementy w zestawie początkowy](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

<span data-ttu-id="61bf8-126">Wymagane są również:</span><span class="sxs-lookup"><span data-stu-id="61bf8-126">You also need:</span></span>

* <span data-ttu-id="61bf8-127">Połączenie przewodowe i bezprzewodowe dla tooconnect Pi do.</span><span class="sxs-lookup"><span data-stu-id="61bf8-127">A wired or wireless connection for Pi tooconnect to.</span></span>
* <span data-ttu-id="61bf8-128">USB SD karty sieciowej lub miniSD karty tooburn hello obraz systemu operacyjnego na karcie microSD hello.</span><span class="sxs-lookup"><span data-stu-id="61bf8-128">A USB-SD adapter or miniSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="61bf8-129">Komputer z systemem Windows, Mac lub Linux.</span><span class="sxs-lookup"><span data-stu-id="61bf8-129">A computer running Windows, Mac, or Linux.</span></span> <span data-ttu-id="61bf8-130">komputer Hello jest używany tooinstall Raspbian na karcie microSD hello.</span><span class="sxs-lookup"><span data-stu-id="61bf8-130">hello computer is used tooinstall Raspbian on hello microSD card.</span></span>
* <span data-ttu-id="61bf8-131">Toodownload połączenia internetowego hello niezbędne narzędzia i oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="61bf8-131">An Internet connection toodownload hello necessary tools and software.</span></span>

## <a name="install-raspbian-on-hello-microsd-card"></a><span data-ttu-id="61bf8-132">Zainstaluj na karcie microSD hello Raspbian</span><span class="sxs-lookup"><span data-stu-id="61bf8-132">Install Raspbian on hello microSD card</span></span>
<span data-ttu-id="61bf8-133">Przygotuj karty microSD hello instalacji hello Raspbian obrazu.</span><span class="sxs-lookup"><span data-stu-id="61bf8-133">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="61bf8-134">Pobierz Raspbian.</span><span class="sxs-lookup"><span data-stu-id="61bf8-134">Download Raspbian.</span></span>
   1. <span data-ttu-id="61bf8-135">[Pobierz](https://www.raspberrypi.org/downloads/raspbian/) pliku zip hello Joasia Raspbian z pikseli.</span><span class="sxs-lookup"><span data-stu-id="61bf8-135">[Download](https://www.raspberrypi.org/downloads/raspbian/) hello .zip file for Raspbian Jessie with Pixel.</span></span>
   2. <span data-ttu-id="61bf8-136">Wyodrębnij hello Raspbian obrazu tooa folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="61bf8-136">Extract hello Raspbian image tooa folder on your computer.</span></span>
2. <span data-ttu-id="61bf8-137">Instalowanie karty microSD toohello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="61bf8-137">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="61bf8-138">[Pobierz](https://www.etcher.io) i zainstaluj narzędzie palnika karty Etcher SD hello.</span><span class="sxs-lookup"><span data-stu-id="61bf8-138">[Download](https://www.etcher.io) and install hello Etcher SD card burner utility.</span></span>
   2. <span data-ttu-id="61bf8-139">Uruchom Etcher i wybierz hello Raspbian obrazu, który został wyodrębniony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="61bf8-139">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   3. <span data-ttu-id="61bf8-140">Wybierz dysk karty microSD hello.</span><span class="sxs-lookup"><span data-stu-id="61bf8-140">Select hello microSD card drive.</span></span>
      <span data-ttu-id="61bf8-141">Należy pamiętać, że Etcher może już wybrane hello poprawnego dysku.</span><span class="sxs-lookup"><span data-stu-id="61bf8-141">Note that Etcher may have already selected hello correct drive.</span></span>
   4. <span data-ttu-id="61bf8-142">Kliknij przycisk **Flash** karta microSD toohello Raspbian tooinstall.</span><span class="sxs-lookup"><span data-stu-id="61bf8-142">Click **Flash** tooinstall Raspbian toohello microSD card.</span></span>
   5. <span data-ttu-id="61bf8-143">Karta microSD hello należy usunąć z komputera po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="61bf8-143">Remove hello microSD card from your computer when installation is complete.</span></span>
      <span data-ttu-id="61bf8-144">Jest karta microSD hello bezpieczne tooremove bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karta microSD powitania po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="61bf8-144">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   6. <span data-ttu-id="61bf8-145">Włóż kartę microSD hello do Pi.</span><span class="sxs-lookup"><span data-stu-id="61bf8-145">Insert hello microSD card into Pi.</span></span>

![Włóż kartę hello SD.](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a><span data-ttu-id="61bf8-147">Włącz Pi</span><span class="sxs-lookup"><span data-stu-id="61bf8-147">Turn on Pi</span></span>
<span data-ttu-id="61bf8-148">Włącz Pi przy użyciu kabla USB micro hello i hello zasilania.</span><span class="sxs-lookup"><span data-stu-id="61bf8-148">Turn on Pi by using hello micro USB cable and hello power supply.</span></span>

![Włącz](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> <span data-ttu-id="61bf8-150">Jest ważne toouse hello zasilacz w zestawie hello, który jest co najmniej 2A toomake się, że Twoje malina poprawnie ma za mało toowork zasilania.</span><span class="sxs-lookup"><span data-stu-id="61bf8-150">It is important toouse hello power supply in hello kit that is at least 2A toomake sure that your Raspberry has enough power toowork correctly.</span></span>

## <a name="enable-ssh"></a><span data-ttu-id="61bf8-151">Włącz SSH</span><span class="sxs-lookup"><span data-stu-id="61bf8-151">Enable SSH</span></span>
<span data-ttu-id="61bf8-152">Począwszy od wersji listopada 2016 hello Raspbian ma serwer SSH hello domyślnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="61bf8-152">As of hello November 2016 release, Raspbian has hello SSH server disabled by default.</span></span> <span data-ttu-id="61bf8-153">Należy tooenable go ręcznie.</span><span class="sxs-lookup"><span data-stu-id="61bf8-153">You need tooenable it manually.</span></span> <span data-ttu-id="61bf8-154">Może się odwoływać toohello [oficjalnego instrukcje](https://www.raspberrypi.org/documentation/remote-access/ssh/) lub połączyć z monitorem i przejść za**Preferencje -> Konfiguracja Pi malina** tooenable SSH.</span><span class="sxs-lookup"><span data-stu-id="61bf8-154">You can refer toohello [official instructions](https://www.raspberrypi.org/documentation/remote-access/ssh/) or connect a monitor and go too**Preferences -> Raspberry Pi Configuration** tooenable SSH.</span></span>

## <a name="connect-raspberry-pi-3-toohello-network"></a><span data-ttu-id="61bf8-155">Łączenie z siecią toohello malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="61bf8-155">Connect Raspberry Pi 3 toohello network</span></span>
<span data-ttu-id="61bf8-156">Możesz połączyć tooa Pi przewodowej sieci lub tooa sieci bezprzewodowej.</span><span class="sxs-lookup"><span data-stu-id="61bf8-156">You can connect Pi tooa wired network or tooa wireless network.</span></span> <span data-ttu-id="61bf8-157">Upewnij się, że Pi jest połączonych toohello sam sieci jako komputera.</span><span class="sxs-lookup"><span data-stu-id="61bf8-157">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="61bf8-158">Na przykład możesz połączyć toohello Pi, które same przełącznika, że komputer jest podłączony do.</span><span class="sxs-lookup"><span data-stu-id="61bf8-158">For example, you can connect Pi toohello same switch that your computer is connected to.</span></span>

### <a name="connect-tooa-wired-network"></a><span data-ttu-id="61bf8-159">Łączenie ich z przewodową siecią tooa</span><span class="sxs-lookup"><span data-stu-id="61bf8-159">Connect tooa wired network</span></span>
<span data-ttu-id="61bf8-160">Użyj tooconnect kabla Ethernet hello tooyour Pi ich z przewodową siecią.</span><span class="sxs-lookup"><span data-stu-id="61bf8-160">Use hello Ethernet cable tooconnect Pi tooyour wired network.</span></span> <span data-ttu-id="61bf8-161">Witaj dwie LED Pi włączyć Jeśli hello połączenie zostanie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="61bf8-161">hello two LEDs on Pi turn on if hello connection is established.</span></span>

![Połącz za pomocą kabla Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a><span data-ttu-id="61bf8-163">Łączenie z siecią bezprzewodową tooa</span><span class="sxs-lookup"><span data-stu-id="61bf8-163">Connect tooa wireless network</span></span>
<span data-ttu-id="61bf8-164">Wykonaj hello [instrukcje](https://www.raspberrypi.org/learning/software-guide/wifi/) z hello Foundation Pi malina tooconnect Pi tooyour bezprzewodowej sieci.</span><span class="sxs-lookup"><span data-stu-id="61bf8-164">Follow hello [instructions](https://www.raspberrypi.org/learning/software-guide/wifi/) from hello Raspberry Pi Foundation tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="61bf8-165">Instrukcje te wymagają toofirst połączyć z monitorem i tooPi klawiatury.</span><span class="sxs-lookup"><span data-stu-id="61bf8-165">These instructions require you toofirst connect a monitor and a keyboard tooPi.</span></span>

## <a name="connect-hello-led-toopi"></a><span data-ttu-id="61bf8-166">Połącz tooPi hello LED</span><span class="sxs-lookup"><span data-stu-id="61bf8-166">Connect hello LED tooPi</span></span>
<span data-ttu-id="61bf8-167">toocomplete tego zadania, użyj hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello przewodów łącznika hello LED i hello rezystor.</span><span class="sxs-lookup"><span data-stu-id="61bf8-167">toocomplete this task, use hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), hello connector wires, hello LED, and hello resistor.</span></span> <span data-ttu-id="61bf8-168">Podłącz je toohello [ogólnego przeznaczenia wejścia/wyjścia](https://www.raspberrypi.org/documentation/usage/gpio/) portów (interfejs GPIO) pi.</span><span class="sxs-lookup"><span data-stu-id="61bf8-168">Connect them toohello [general-purpose input/output](https://www.raspberrypi.org/documentation/usage/gpio/) (GPIO) ports of Pi.</span></span>

![Breadboard LED i rezystor](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. <span data-ttu-id="61bf8-170">Połącz hello krótszą etap hello LED zbyt**GND interfejs GPIO (numer Pin 6)**.</span><span class="sxs-lookup"><span data-stu-id="61bf8-170">Connect hello shorter leg of hello LED too**GPIO GND (Pin 6)**.</span></span>
2. <span data-ttu-id="61bf8-171">Połącz hello dłużej etap hello etap tooone LED rezystor hello.</span><span class="sxs-lookup"><span data-stu-id="61bf8-171">Connect hello longer leg of hello LED tooone leg of hello resistor.</span></span>
3. <span data-ttu-id="61bf8-172">Połącz hello innych etap rezystor hello zbyt**interfejs GPIO 4 (numer Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="61bf8-172">Connect hello other leg of hello resistor too**GPIO 4 (Pin 7)**.</span></span>

<span data-ttu-id="61bf8-173">Należy pamiętać, że bieguna hello LED ważne.</span><span class="sxs-lookup"><span data-stu-id="61bf8-173">Note that hello LED polarity is important.</span></span> <span data-ttu-id="61bf8-174">To ustawienie bieguna jest często nazywana Active niski.</span><span class="sxs-lookup"><span data-stu-id="61bf8-174">This polarity setting is commonly known as Active Low.</span></span>

![Szablon](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

<span data-ttu-id="61bf8-176">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="61bf8-176">Congratulations!</span></span> <span data-ttu-id="61bf8-177">Pomyślnie skonfigurowano Pi.</span><span class="sxs-lookup"><span data-stu-id="61bf8-177">You've successfully configured Pi.</span></span>

## <a name="summary"></a><span data-ttu-id="61bf8-178">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="61bf8-178">Summary</span></span>
<span data-ttu-id="61bf8-179">W tym artykule, kiedy znasz już jak tooconfigure Pi przez zainstalowanie Raspbian, łączącego Pi tooa sieci i łączenie tooPi LED.</span><span class="sxs-lookup"><span data-stu-id="61bf8-179">In this article, you’ve learned how tooconfigure Pi by installing Raspbian, connecting Pi tooa network, and connecting an LED tooPi.</span></span> <span data-ttu-id="61bf8-180">Należy pamiętać, że powitalne LED jeszcze nie podświetlony.</span><span class="sxs-lookup"><span data-stu-id="61bf8-180">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="61bf8-181">następne zadanie Hello jest tooinstall hello niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia aplikacji przykładowej na Pi.</span><span class="sxs-lookup"><span data-stu-id="61bf8-181">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Pi.</span></span>

![Sprzęt jest gotowy](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a><span data-ttu-id="61bf8-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="61bf8-183">Next steps</span></span>
[<span data-ttu-id="61bf8-184">Pobierz narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="61bf8-184">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-node-lesson1-get-the-tools-win32.md)

