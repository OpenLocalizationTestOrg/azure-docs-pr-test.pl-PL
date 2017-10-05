---
title: "Connect Arduino (C) do Azure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie sieci Wi-Fi Adafruit piór M0 dla pierwszego użycia."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino ustawienie nawiązać arduino komputerów, arduino Instalatora, arduino tablicy"
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
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="fa2fd-104">Konfigurowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="fa2fd-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fa2fd-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="fa2fd-105">What you will do</span></span>
<span data-ttu-id="fa2fd-106">Skonfiguruj tablicy Adafruit piór M0 sieci Wi-Fi Arduino dla pierwszego użycia przez łączenie tablicy, jego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="fa2fd-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="fa2fd-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fa2fd-108">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="fa2fd-108">What you need</span></span>
<span data-ttu-id="fa2fd-109">Aby wykonać tę operację, potrzebne następujące części dla Twojego startowy Adafruit piór M0 sieci Wi-Fi:</span><span class="sxs-lookup"><span data-stu-id="fa2fd-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="fa2fd-110">Tablica Adafruit piór M0 sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="fa2fd-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="fa2fd-111">B Micro do kabla USB A typu</span><span class="sxs-lookup"><span data-stu-id="fa2fd-111">A Micro B to Type A USB cable</span></span>

![zestaw][kit]

<span data-ttu-id="fa2fd-113">Wymagane są również:</span><span class="sxs-lookup"><span data-stu-id="fa2fd-113">You also need:</span></span>

* <span data-ttu-id="fa2fd-114">Komputer z systemem Windows, Mac lub Linux.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="fa2fd-115">Połączenia bezprzewodowego dla tablicy Arduino do nawiązania połączenia.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="fa2fd-116">Połączenia internetowego na pobieranie narzędzia do konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fa2fd-117">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="fa2fd-117">What you will learn</span></span>
<span data-ttu-id="fa2fd-118">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="fa2fd-118">In this article, you will learn:</span></span>

* <span data-ttu-id="fa2fd-119">Jak utworzyć tablicy Arduino i włączenie go dla następujących — lekcje.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="fa2fd-120">Jak dodawać uprawnienia portu szeregowego na Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="fa2fd-121">Łączenie się z komputerem tablicy Arduino</span><span class="sxs-lookup"><span data-stu-id="fa2fd-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="fa2fd-122">Podłącz kabel USB micro do górnej micro portu USB.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Górny micro portu USB][top-micro-usb-port]

2. <span data-ttu-id="fa2fd-124">Podłącz drugi koniec kabla USB do komputera.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-124">Plug the other end of USB cable into your computer.</span></span>

   ![Komputer USB][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="fa2fd-126">Dodaj uprawnienia portu szeregowego na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="fa2fd-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="fa2fd-127">Jeśli używasz systemu Windows lub macOS można pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="fa2fd-128">Ubuntu należy następujące kroki, aby upewnij się, że użytkownik normalne linux ma uprawnienia do działania na port USB Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="fa2fd-129">Teraz jako zwykłego użytkownika z terminalu:</span><span class="sxs-lookup"><span data-stu-id="fa2fd-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="fa2fd-130">Otrzymasz wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="fa2fd-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="fa2fd-131">"0" może być inny numer, lub może być zwrócony wiele wpisów.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="fa2fd-132">W pierwszym przypadku danych potrzebne jest `uucp`, w ciągu sekundy jest `dialout`, który jest właścicielem grupy pliku.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="fa2fd-133">Dodaj użytkownika do grupy:</span><span class="sxs-lookup"><span data-stu-id="fa2fd-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="fa2fd-134">Gdzie `group-name` danych znaleziono w pierwszym kroku i `username` to nazwa użytkownika systemu linux.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="fa2fd-135">Konieczne będzie rejestrować Wyloguj się i zaloguj ponownie ta zmiana została uwzględniona i ukończyć instalację.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="fa2fd-136">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="fa2fd-136">Summary</span></span>
<span data-ttu-id="fa2fd-137">W tym artykule kiedy znasz już sposobu konfigurowania Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="fa2fd-138">Następne zadanie jest Zainstaluj niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia na tablicy Arduino przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa2fd-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Sprzęt jest gotowy][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="fa2fd-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa2fd-140">Next steps</span></span>
<span data-ttu-id="fa2fd-141">[Pobierz narzędzia][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="fa2fd-141">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md