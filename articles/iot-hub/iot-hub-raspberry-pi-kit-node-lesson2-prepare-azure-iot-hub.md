---
featureFlags: usabilla
title: "Nawiązać Pi malina (węzeł) Azure IoT — Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Utwórz grupę zasobów, tworzenia Centrum Azure IoT i zarejestrować Pi w rejestrze tożsamości Centrum IoT przy użyciu wiersza polecenia platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Połącz chmury pi malinowe pi chmury,"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 774f9356d7a11b2c61905ada75bed92d44e5fc0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="5f871-104">Utworzenie Centrum IoT i zarejestruj malina Pi 3</span><span class="sxs-lookup"><span data-stu-id="5f871-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5f871-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="5f871-105">What you will do</span></span>
* <span data-ttu-id="5f871-106">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="5f871-106">Create a resource group.</span></span>
* <span data-ttu-id="5f871-107">Utworzenie Centrum Azure IoT w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="5f871-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="5f871-108">Dodaj malina Pi 3 do Centrum Azure IoT przy użyciu interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="5f871-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="5f871-109">Korzystając z wiersza polecenia platformy Azure można dodać Pi do Centrum IoT, Usługa generuje klucz pi do uwierzytelniania w usłudze.</span><span class="sxs-lookup"><span data-stu-id="5f871-109">When you use Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="5f871-110">Jeśli masz problemy z poszukiwanie rozwiązania na [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5f871-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5f871-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="5f871-111">What you will learn</span></span>
<span data-ttu-id="5f871-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="5f871-112">In this article, you will learn:</span></span>
* <span data-ttu-id="5f871-113">Sposób użycia interfejsu wiersza polecenia Azure do tworzenia Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="5f871-113">How to use Azure CLI to create an IoT hub</span></span>
* <span data-ttu-id="5f871-114">Jak utworzyć tożsamość urządzenia pi w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="5f871-114">How to create a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5f871-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="5f871-115">What you need</span></span>
* <span data-ttu-id="5f871-116">Konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5f871-116">An Azure account</span></span>
* <span data-ttu-id="5f871-117">Mac lub komputerze z systemem Windows z wiersza polecenia platformy Azure zainstalowany</span><span class="sxs-lookup"><span data-stu-id="5f871-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="5f871-118">Utworzenie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="5f871-118">Create your IoT hub</span></span>
<span data-ttu-id="5f871-119">Centrum IoT Azure pomaga połączyć, monitorować i zarządzać nimi miliony zasoby IoT.</span><span class="sxs-lookup"><span data-stu-id="5f871-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="5f871-120">Aby utworzyć Centrum IoT, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f871-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="5f871-121">Zaloguj się do konta platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5f871-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="5f871-122">Wszystkie dostępne subskrypcje są wyświetlane po pomyślnym zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="5f871-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="5f871-123">Wartość domyślna subskrypcja, którego chcesz używać, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5f871-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="5f871-124">`subscription ID or name`można znaleźć w danych wyjściowych `az login` lub `az account list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="5f871-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="5f871-125">Zarejestruj dostawcę, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="5f871-125">Register the provider by running the following command.</span></span> <span data-ttu-id="5f871-126">Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5f871-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="5f871-127">Przed wdrożeniem zasobów platformy Azure, dostawcy oferujący należy zarejestrować dostawcę.</span><span class="sxs-lookup"><span data-stu-id="5f871-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="5f871-128">Utwórz grupę zasobów o nazwie iot próbkami regionu zachodnie stany USA, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5f871-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="5f871-129">`westus`jest to lokalizacja, tworzenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="5f871-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="5f871-130">Jeśli chcesz użyć innej lokalizacji, możesz uruchomić `az account list-locations -o table` do wyświetlenia wszystkich lokalizacji platformy Azure obsługuje.</span><span class="sxs-lookup"><span data-stu-id="5f871-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="5f871-131">Utwórz Centrum IoT w grupie zasobów przykładowej iot, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5f871-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="5f871-132">Domyślnie narzędzie tworzy Centrum IoT w warstwy cenowej bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="5f871-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="5f871-133">Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="5f871-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="5f871-134">Nazwa centrum IoT musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="5f871-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="5f871-135">Można utworzyć tylko jedną F1 wersji Centrum IoT Azure w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5f871-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="5f871-136">Zarejestruj Pi w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="5f871-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="5f871-137">Poszczególne urządzenia, która wysyła komunikaty do Centrum IoT i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="5f871-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="5f871-138">Azure CLI użyje do rejestracji programu Pi i utwórz samopodpisany certyfikat X.509 do uwierzytelniania urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5f871-138">You will use Azure CLI to register your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="5f871-139">Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5f871-139">Run the following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="5f871-140">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5f871-140">Summary</span></span>
<span data-ttu-id="5f871-141">Utworzeniu Centrum IoT i zarejestrowane Pi za pomocą tożsamości urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5f871-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="5f871-142">Możesz dowiedzieć się, jak wysyłać wiadomości z Pi do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5f871-142">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f871-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f871-143">Next steps</span></span>
[<span data-ttu-id="5f871-144">Tworzenie aplikacji funkcji platformy Azure i konto magazynu Azure do przetwarzania i przechowywania wiadomości Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="5f871-144">Create an Azure function app and an Azure storage account to process and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

