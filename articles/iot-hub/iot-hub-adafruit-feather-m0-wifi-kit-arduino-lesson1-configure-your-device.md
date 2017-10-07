---
title: "Connect Arduino (C) tooAzure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie sieci Wi-Fi Adafruit piór M0 dla pierwszego użycia."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino Konfigurowanie, Połącz arduino toopc, arduino Instalatora, arduino tablicy"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="bf0b1-104">Konfigurowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="bf0b1-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="bf0b1-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="bf0b1-105">What you will do</span></span>
<span data-ttu-id="bf0b1-106">Skonfiguruj tablicy Adafruit piór M0 sieci Wi-Fi Arduino dla pierwszego użycia przez łączenie tablicy hello, jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="bf0b1-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bf0b1-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bf0b1-108">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="bf0b1-108">What you need</span></span>
<span data-ttu-id="bf0b1-109">toocomplete tej operacji, należy hello następujące części dla Twojego startowy Adafruit piór M0 sieci Wi-Fi:</span><span class="sxs-lookup"><span data-stu-id="bf0b1-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="bf0b1-110">Witaj tablicy Adafruit piór M0 sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="bf0b1-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="bf0b1-111">TooType Micro B kabla A USB</span><span class="sxs-lookup"><span data-stu-id="bf0b1-111">A Micro B tooType A USB cable</span></span>

![zestaw][kit]

<span data-ttu-id="bf0b1-113">Wymagane są również:</span><span class="sxs-lookup"><span data-stu-id="bf0b1-113">You also need:</span></span>

* <span data-ttu-id="bf0b1-114">Komputer z systemem Windows, Mac lub Linux.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="bf0b1-115">Połączenia bezprzewodowego dla Twojego tooconnect tablicy Arduino do.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="bf0b1-116">Internet połączenia toodownload narzędzie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bf0b1-117">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="bf0b1-117">What you will learn</span></span>
<span data-ttu-id="bf0b1-118">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="bf0b1-118">In this article, you will learn:</span></span>

* <span data-ttu-id="bf0b1-119">Jak tooassemble Arduino tablicy, a power go dla następującego hello lekcje.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="bf0b1-120">Jak tooadd uprawnienia Ubuntu portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="bf0b1-121">Połącz komputer tooyour Arduino tablicy</span><span class="sxs-lookup"><span data-stu-id="bf0b1-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="bf0b1-122">Podłącz kabel USB micro hello do portu USB micro najwyższego hello.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Górny micro portu USB][top-micro-usb-port]

2. <span data-ttu-id="bf0b1-124">Plug hello drugiej, kabel USB do komputera.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-124">Plug hello other end of USB cable into your computer.</span></span>

   ![Komputer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="bf0b1-126">Dodaj uprawnienia portu szeregowego na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="bf0b1-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="bf0b1-127">Jeśli używasz systemu Windows lub macOS można pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="bf0b1-128">Ubuntu należy hello następujące kroki toomake się, że hello normalne linux użytkownik ma toooperate uprawnienia hello na port USB hello Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="bf0b1-129">Teraz jako zwykłego użytkownika z terminalu:</span><span class="sxs-lookup"><span data-stu-id="bf0b1-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="bf0b1-130">Otrzymasz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="bf0b1-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="bf0b1-131">Witaj, "0" może być inną liczbę lub może być zwrócony wiele wpisów.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="bf0b1-132">W hello potrzebujemy pierwsze dane przypadków hello jest `uucp`, hello drugi jest `dialout`, który jest właścicielem grupy hello hello pliku.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="bf0b1-133">Dodaj grupę toohello toohello użytkowników:</span><span class="sxs-lookup"><span data-stu-id="bf0b1-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="bf0b1-134">Gdzie `group-name` dane hello w pierwszym krokiem hello i `username` to nazwa użytkownika systemu linux.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="bf0b1-135">Konieczne będzie toolog Wyloguj się i zaloguj ponownie dla tego efektu tootake zmiany i hello ukończenia instalacji.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="bf0b1-136">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="bf0b1-136">Summary</span></span>
<span data-ttu-id="bf0b1-137">W tym artykule, kiedy znasz już jak tooconfigure Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="bf0b1-138">następne zadanie Hello jest tooinstall hello niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia na tablicy Arduino przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf0b1-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Sprzęt jest gotowy][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="bf0b1-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bf0b1-140">Next steps</span></span>
<span data-ttu-id="bf0b1-141">[Pobierz narzędzia hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="bf0b1-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md