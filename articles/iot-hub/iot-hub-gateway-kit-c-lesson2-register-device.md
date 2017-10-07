---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Centrum Azure iot, internet rzeczy chmury azure iot Centrum tworzenia urządzenia, analizy czasowej Sensor tag, cz analizy czasowej"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 2c18f5ae-e39a-48ae-a9fe-04bb595740a0
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5d2322268aa18f52f60c2833778323773ac4eec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="c7b5a-103">Utworzenie Centrum Azure IoT i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="c7b5a-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c7b5a-104">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="c7b5a-104">What you will do</span></span>

- <span data-ttu-id="c7b5a-105">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="c7b5a-105">Create a resource group</span></span>
- <span data-ttu-id="c7b5a-106">Utworzenie pierwszego Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c7b5a-106">Create your first IoT hub</span></span>
- <span data-ttu-id="c7b5a-107">Zarejestruj urządzenie w Centrum IoT przy użyciu hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="c7b5a-108">Po zarejestrowaniu urządzenia w Centrum IoT hello usługi Centrum IoT Azure generuje klucz dla tooauthenticate toouse Twojego urządzenia z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="c7b5a-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c7b5a-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c7b5a-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="c7b5a-110">What you will learn</span></span>

<span data-ttu-id="c7b5a-111">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="c7b5a-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="c7b5a-112">Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="c7b5a-113">Jak tooregister urządzenie w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c7b5a-114">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="c7b5a-114">What you need</span></span>

- <span data-ttu-id="c7b5a-115">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-115">An active Azure subscription.</span></span> <span data-ttu-id="c7b5a-116">Jeśli nie masz konta platformy Azure, możesz utworzyć [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="c7b5a-117">Powinien mieć hello zainstalowana wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c7b5a-118">Tworzenie centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c7b5a-118">Create an IoT hub</span></span>

<span data-ttu-id="c7b5a-119">toocreate Centrum IoT, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c7b5a-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="c7b5a-120">Zaloguj się tooyour konto platformy Azure, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c7b5a-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="c7b5a-121">Zostaną wyświetlone wszystkie subskrypcje dostępne po pomyślnym zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="c7b5a-122">Ustaw domyślny hello subskrypcji platformy Azure, które mają toouse, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c7b5a-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="c7b5a-123">`subscription ID or name`można znaleźć w danych wyjściowych hello hello `az login` lub hello `az account list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="c7b5a-124">Zarejestruj dostawcę hello, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="c7b5a-125">Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="c7b5a-126">Należy zarejestrować dostawcę hello przed wdrożeniem hello zasobów platformy Azure, która hello oferty dostawcy.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="c7b5a-127">Utwórz grupę zasobów o nazwie `iot-gateway` hello regionu zachodnie stany USA, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c7b5a-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="c7b5a-128">`westus`to miejsce hello Tworzenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="c7b5a-129">Jeśli chcesz toouse w innej lokalizacji, możesz uruchomić `az account list-locations -o table` toosee wszystkie hello Azure obsługuje lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="c7b5a-130">Tworzenie Centrum IoT w hello `iot-gateway` grupy zasobów, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c7b5a-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="c7b5a-131">Domyślnie narzędzie hello tworzy Centrum IoT w hello warstwa cenowa bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="c7b5a-132">Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="c7b5a-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="c7b5a-133">Hello nazwę Centrum IoT musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="c7b5a-134">Można utworzyć tylko jedną F1 wersji Centrum Iot Azure w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="c7b5a-135">Zarejestruj urządzenie w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c7b5a-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="c7b5a-136">Poszczególne urządzenia, która Centrum IoT tooyour komunikatów wysyła i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="c7b5a-137">Zarejestruj urządzenie w Centrum IoT przez uruchomione następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c7b5a-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="c7b5a-138">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c7b5a-138">Summary</span></span>

<span data-ttu-id="c7b5a-139">Utworzeniu Centrum IoT i zarejestrowane urządzenia logicznego za pomocą tożsamości urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="c7b5a-140">Wszystko jest gotowe toolearn jak tooconfigure i uruchamiania bramy przykładowych aplikacji toosend danych z urządzenia fizycznego Centrum IoT tooyour w hello chmury.</span><span class="sxs-lookup"><span data-stu-id="c7b5a-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7b5a-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c7b5a-141">Next steps</span></span>
[<span data-ttu-id="c7b5a-142">Konfigurowanie i uruchamianie cz przykładową aplikację</span><span class="sxs-lookup"><span data-stu-id="c7b5a-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)