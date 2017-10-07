---
title: "Connect Intel Edison (C) tooAzure IoT — Lekcja 2: rejestrowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Utwórz grupę zasobów, tworzenia Centrum Azure IoT i zarejestrować Edison w Centrum Azure IoT hello za pomocą hello wiersza polecenia platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 80bfc3cd-a1fc-4775-8994-d8033381dd3d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9635e916425883d65793d0ed46843ab49b3f35ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="14df3-103">Utworzenie Centrum IoT i zarejestruj Intel Edison</span><span class="sxs-lookup"><span data-stu-id="14df3-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="14df3-104">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="14df3-104">What you will do</span></span>
* <span data-ttu-id="14df3-105">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="14df3-105">Create a resource group.</span></span>
* <span data-ttu-id="14df3-106">Utworzenie Centrum Azure IoT w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="14df3-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="14df3-107">Dodaj Centrum Azure IoT toohello Intel Edison przy użyciu hello interfejsu wiersza polecenia platformy Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="14df3-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="14df3-108">Gdy używasz hello Azure CLI tooadd Centrum IoT tooyour Edison usługi hello generuje klucz dla tooauthenticate Edison z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="14df3-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="14df3-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="14df3-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="14df3-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="14df3-110">What you will learn</span></span>
<span data-ttu-id="14df3-111">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="14df3-111">In this article, you will learn:</span></span>
* <span data-ttu-id="14df3-112">Jak toouse hello toocreate interfejsu wiersza polecenia Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="14df3-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="14df3-113">Jak toocreate tożsamość urządzenia dla Edison w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="14df3-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="14df3-114">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="14df3-114">What you need</span></span>
* <span data-ttu-id="14df3-115">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14df3-115">An Azure account.</span></span> <span data-ttu-id="14df3-116">Jeśli nie masz konta platformy Azure, Utwórz [bezpłatnego konta wersji próbnej Azure](http://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="14df3-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="14df3-117">Powinien mieć hello zainstalowana wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14df3-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="14df3-118">Utworzenie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="14df3-118">Create your IoT hub</span></span>
<span data-ttu-id="14df3-119">Centrum IoT Azure pomaga połączyć, monitorować i zarządzać nimi miliony zasoby IoT.</span><span class="sxs-lookup"><span data-stu-id="14df3-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="14df3-120">toocreate Centrum IoT, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="14df3-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="14df3-121">Zaloguj się tooyour konto platformy Azure, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="14df3-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="14df3-122">Wszystkie dostępne subskrypcje są wyświetlane po pomyślnym zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="14df3-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="14df3-123">Ustaw hello Domyślna subskrypcja ma toouse, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="14df3-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="14df3-124">`subscription ID or name`można znaleźć w danych wyjściowych hello hello `az login` lub hello `az account list` polecenia.</span><span class="sxs-lookup"><span data-stu-id="14df3-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="14df3-125">Zarejestruj dostawcę hello, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="14df3-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="14df3-126">Dostawcy zasobów są usługi, które zapewniają zasobów dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="14df3-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="14df3-127">Należy zarejestrować dostawcę hello przed wdrożeniem hello zasobów platformy Azure, która hello oferty dostawcy.</span><span class="sxs-lookup"><span data-stu-id="14df3-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="14df3-128">Utwórz grupę zasobów o nazwie na próbki iot, hello regionu zachodnie stany USA, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="14df3-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="14df3-129">`westus`to miejsce hello Tworzenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="14df3-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="14df3-130">Jeśli chcesz toouse w innej lokalizacji, możesz uruchomić `az account list-locations -o table` toosee wszystkie hello Azure obsługuje lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="14df3-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="14df3-131">Utwórz Centrum IoT w grupie zasobów przykładowej iot hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="14df3-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="14df3-132">Domyślnie narzędzie hello tworzy Centrum IoT w hello warstwa cenowa bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="14df3-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="14df3-133">Aby uzyskać więcej informacji, zobacz [cennik Centrum IoT Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="14df3-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="14df3-134">Hello nazwę Centrum IoT musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="14df3-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="14df3-135">Można utworzyć tylko jedną F1 wersji Centrum IoT Azure w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14df3-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="14df3-136">Zarejestruj Edison w Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="14df3-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="14df3-137">Poszczególne urządzenia, która Centrum IoT tooyour komunikatów wysyła i odbiera komunikaty z Centrum IoT musi być zarejestrowany unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="14df3-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="14df3-138">Zarejestruj Edison w Centrum IoT przez uruchomione następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="14df3-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="14df3-139">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="14df3-139">Summary</span></span>
<span data-ttu-id="14df3-140">Utworzeniu Centrum IoT i zarejestrowane Edison za pomocą tożsamości urządzenia w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="14df3-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="14df3-141">Wszystko jest gotowe toolearn jak toosend komunikaty z Centrum IoT tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="14df3-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14df3-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="14df3-142">Next steps</span></span>
<span data-ttu-id="14df3-143">[Tworzenie aplikacji funkcji platformy Azure i usługi Azure Storage konta tooprocess i Magazyn Centrum IoT wiadomości][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="14df3-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md