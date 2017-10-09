---
title: "Connect Raspberry pi (C) tooAzure IoT — Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Utwórz grupę zasobów, tworzenia Centrum Azure IoT i zarejestrować Pi w Centrum Azure IoT hello za pomocą hello wiersza polecenia platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Połącz chmury pi malinowe pi chmury,"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 473658c5a8e1e0d4cfced0efafbad2640a1e0696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="d6106-104">Utworzenie Centrum IoT i zarejestruj malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="d6106-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d6106-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="d6106-105">What you will do</span></span>
* <span data-ttu-id="d6106-106">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="d6106-106">Create a resource group.</span></span>
* <span data-ttu-id="d6106-107">Utworzenie Centrum Azure IoT w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="d6106-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="d6106-108">Dodaj Centrum Azure IoT toohello malina Pi 3 za pomocą hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="d6106-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="d6106-109">Korzystając z Centrum IoT tooyour tooadd Pi hello wiersza polecenia platformy Azure, usługa hello generuje klucz dla tooauthenticate Pi z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="d6106-109">When you use hello Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="d6106-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d6106-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d6106-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="d6106-111">What you will learn</span></span>
<span data-ttu-id="d6106-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="d6106-112">In this article, you will learn:</span></span>
* <span data-ttu-id="d6106-113">Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="d6106-113">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="d6106-114">Jak toocreate tożsamość urządzenia pi w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d6106-114">How toocreate a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d6106-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="d6106-115">What you need</span></span>
* <span data-ttu-id="d6106-116">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d6106-116">An Azure account</span></span>
* <span data-ttu-id="d6106-117">Mac lub komputerze z systemem Windows z hello Azure CLI jest zainstalowany</span><span class="sxs-lookup"><span data-stu-id="d6106-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="d6106-118">Utworzenie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="d6106-118">Create your IoT hub</span></span>
<span data-ttu-id="d6106-119">Centrum IoT Azure pomaga połączyć, monitorować i zarządzać nimi miliony zasoby IoT.</span><span class="sxs-lookup"><span data-stu-id="d6106-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="d6106-120">toocreate Centrum IoT, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d6106-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="d6106-121">Zaloguj się tooyour konto platformy Azure, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d6106-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="d6106-122">Wszystkie dostępne subskrypcje są wyświetlane po pomyślnym zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="d6106-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="d6106-123">Ustaw hello Domyślna subskrypcja ma toouse, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d6106-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="d6106-124">`subscription ID or name`można znaleźć w danych wyjściowych hello hello `az login` lub hello `az account list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d6106-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="d6106-125">Zarejestruj dostawcę hello, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="d6106-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="d6106-126">Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6106-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="d6106-127">Należy zarejestrować dostawcę hello przed wdrożeniem hello zasobów platformy Azure, która hello oferty dostawcy.</span><span class="sxs-lookup"><span data-stu-id="d6106-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="d6106-128">Utwórz grupę zasobów o nazwie na próbki iot, hello regionu zachodnie stany USA, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d6106-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="d6106-129">`westus`to miejsce hello Tworzenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d6106-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="d6106-130">Jeśli chcesz toouse w innej lokalizacji, możesz uruchomić `az account list-locations -o table` toosee wszystkie hello Azure obsługuje lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d6106-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="d6106-131">Utwórz Centrum IoT w grupie zasobów przykładowej iot hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="d6106-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="d6106-132">Domyślnie narzędzie hello tworzy Centrum IoT w hello warstwa cenowa bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="d6106-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="d6106-133">Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="d6106-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="d6106-134">Hello nazwę Centrum IoT musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="d6106-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="d6106-135">Można utworzyć tylko jedną F1 wersji Centrum IoT Azure w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6106-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="d6106-136">Zarejestruj Pi w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="d6106-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="d6106-137">Poszczególne urządzenia, która Centrum IoT tooyour komunikatów wysyła i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="d6106-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="d6106-138">Zarejestruj Pi w Centrum przez uruchomione następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d6106-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="d6106-139">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d6106-139">Summary</span></span>
<span data-ttu-id="d6106-140">Utworzeniu Centrum IoT i zarejestrowane Pi za pomocą tożsamości urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="d6106-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="d6106-141">Wszystko jest gotowe toolearn jak toosend komunikaty z Centrum IoT tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="d6106-141">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6106-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6106-142">Next steps</span></span>
<span data-ttu-id="d6106-143">[Tworzenie aplikacji funkcji platformy Azure i usługi Azure Storage konta tooprocess i Magazyn Centrum IoT wiadomości](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="d6106-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

