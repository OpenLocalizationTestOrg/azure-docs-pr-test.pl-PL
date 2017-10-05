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
ms.openlocfilehash: 685a479583f5f11f57bef22dc5881285bb1f70d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="e5d10-103">Utworzenie Centrum Azure IoT i rejestrowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="e5d10-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e5d10-104">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="e5d10-104">What you will do</span></span>

- <span data-ttu-id="e5d10-105">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="e5d10-105">Create a resource group</span></span>
- <span data-ttu-id="e5d10-106">Utworzenie pierwszego Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e5d10-106">Create your first IoT hub</span></span>
- <span data-ttu-id="e5d10-107">Zarejestruj urządzenie w Centrum IoT przy użyciu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d10-107">Register your device in your IoT hub by using the Azure CLI.</span></span> 

<span data-ttu-id="e5d10-108">Podczas rejestrowania urządzenia w Centrum IoT, usługa Azure IoT Hub generuje klucz dla urządzenia w celu używania do uwierzytelniania w usłudze.</span><span class="sxs-lookup"><span data-stu-id="e5d10-108">When you register your device in your IoT hub, the Azure IoT Hub service generates a key for your device to use to authenticate with the service.</span></span> 

<span data-ttu-id="e5d10-109">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e5d10-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e5d10-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="e5d10-110">What you will learn</span></span>

<span data-ttu-id="e5d10-111">W tej lekcji dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="e5d10-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="e5d10-112">Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e5d10-112">How to use the Azure CLI to create an IoT hub.</span></span>
- <span data-ttu-id="e5d10-113">Jak zarejestrować urządzenie w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e5d10-113">How to register a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e5d10-114">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="e5d10-114">What you need</span></span>

- <span data-ttu-id="e5d10-115">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d10-115">An active Azure subscription.</span></span> <span data-ttu-id="e5d10-116">Jeśli nie masz konta platformy Azure, możesz utworzyć [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="e5d10-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="e5d10-117">Powinny mieć zainstalowane interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d10-117">You should have the Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="e5d10-118">Tworzenie centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e5d10-118">Create an IoT hub</span></span>

<span data-ttu-id="e5d10-119">Aby utworzyć Centrum IoT, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e5d10-119">To create an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="e5d10-120">Zaloguj się do konta platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e5d10-120">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="e5d10-121">Zostaną wyświetlone wszystkie subskrypcje dostępne po pomyślnym zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="e5d10-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="e5d10-122">Ustaw domyślny subskrypcji Azure, która ma być używany, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e5d10-122">Set the default Azure subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="e5d10-123">`subscription ID or name`można znaleźć w danych wyjściowych `az login` lub `az account list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5d10-123">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="e5d10-124">Zarejestruj dostawcę, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="e5d10-124">Register the provider by running the following command.</span></span> <span data-ttu-id="e5d10-125">Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5d10-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="e5d10-126">Przed wdrożeniem zasobów platformy Azure, dostawcy oferujący należy zarejestrować dostawcę.</span><span class="sxs-lookup"><span data-stu-id="e5d10-126">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="e5d10-127">Utwórz grupę zasobów o nazwie `iot-gateway` regionu zachodnie stany USA, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e5d10-127">Create a resource group named `iot-gateway` in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="e5d10-128">`westus`jest to lokalizacja, tworzenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e5d10-128">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="e5d10-129">Jeśli chcesz użyć innej lokalizacji, możesz uruchomić `az account list-locations -o table` do wyświetlenia wszystkich lokalizacji platformy Azure obsługuje.</span><span class="sxs-lookup"><span data-stu-id="e5d10-129">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="e5d10-130">Tworzenie Centrum IoT w `iot-gateway` grupy zasobów, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e5d10-130">Create an IoT hub in the `iot-gateway` resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="e5d10-131">Domyślnie narzędzie tworzy Centrum IoT w warstwy cenowej bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="e5d10-131">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="e5d10-132">Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="e5d10-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="e5d10-133">Nazwa centrum IoT musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="e5d10-133">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="e5d10-134">Można utworzyć tylko jedną F1 wersji Centrum Iot Azure w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d10-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="e5d10-135">Zarejestruj urządzenie w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e5d10-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="e5d10-136">Poszczególne urządzenia, która wysyła komunikaty do Centrum IoT i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="e5d10-136">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="e5d10-137">Zarejestruj urządzenie w Centrum IoT przez uruchomione następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e5d10-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="e5d10-138">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e5d10-138">Summary</span></span>

<span data-ttu-id="e5d10-139">Utworzeniu Centrum IoT i zarejestrowane urządzenia logicznego za pomocą tożsamości urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e5d10-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="e5d10-140">Możesz dowiedzieć się, jak skonfigurować i uruchomić bramy przykładowej aplikacji do wysyłania danych z urządzenia fizycznego do Centrum IoT w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e5d10-140">You're ready to learn how to configure and run a gateway sample application to send data from your physical device to your IoT hub in the cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5d10-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5d10-141">Next steps</span></span>
[<span data-ttu-id="e5d10-142">Konfigurowanie i uruchamianie cz przykładową aplikację</span><span class="sxs-lookup"><span data-stu-id="e5d10-142">Configure and run a BLE sample app</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)