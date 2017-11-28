---
title: "tooadd aaaHow środowiska Azure czas serii Insights tooyour źródła zdarzeń Centrum IoT | Dokumentacja firmy Microsoft"
description: "W tym samouczku opisano sposób tooadd zdarzenie źródła, to znaczy połączenia tooan środowiska czasu serii Insights tooyour Centrum IoT"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a><span data-ttu-id="c0b31-103">Jak tooadd źródłem zdarzenia Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-103">How tooadd an IoT Hub event source</span></span>

<span data-ttu-id="c0b31-104">W tym samouczku opisano, jak toouse hello Azure tooadd portalu źródło zdarzenia, które odczytuje ze środowiska czasu serii Insights tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-104">This tutorial covers how toouse hello Azure portal tooadd an event source that reads from an IoT Hub tooyour Time Series Insights environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0b31-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c0b31-105">Prerequisites</span></span>

<span data-ttu-id="c0b31-106">Utworzono Centrum IoT i pisania tooit zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c0b31-106">You have created an IoT Hub and are writing events tooit.</span></span> <span data-ttu-id="c0b31-107">Aby uzyskać więcej informacji o centra IoT, zobacz <https://azure.microsoft.com/services/iot-hub/></span><span class="sxs-lookup"><span data-stu-id="c0b31-107">For more information on IoT Hubs, see <https://azure.microsoft.com/services/iot-hub/></span></span>

> <span data-ttu-id="c0b31-108">[Grupy konsumentów] Źródło zdarzenia każdego Insights serii czasu musi toohave własnej dedykowanej grupy klientów, które nie są współużytkowane z innym klientom.</span><span class="sxs-lookup"><span data-stu-id="c0b31-108">[Consumer Groups] Each Time Series Insights event source needs toohave its own dedicated consumer group that is not shared with any other consumers.</span></span> <span data-ttu-id="c0b31-109">Jeśli korzystać z wielu czytników zdarzeń z hello tej samej grupy konsumentów, wszystkie czytniki są prawdopodobnie toosee błędów.</span><span class="sxs-lookup"><span data-stu-id="c0b31-109">If multiple readers consume events from hello same consumer group, all readers are likely toosee failures.</span></span> <span data-ttu-id="c0b31-110">Aby uzyskać więcej informacji, zobacz hello [Centrum IoT — przewodnik dewelopera](../iot-hub/iot-hub-devguide.md).</span><span class="sxs-lookup"><span data-stu-id="c0b31-110">For details, see hello [IoT Hub developer guide](../iot-hub/iot-hub-devguide.md).</span></span>

## <a name="choose-an-import-option"></a><span data-ttu-id="c0b31-111">Wybierz opcję importu</span><span class="sxs-lookup"><span data-stu-id="c0b31-111">Choose an Import option</span></span>

<span data-ttu-id="c0b31-112">Ustawienia Hello hello źródło zdarzenia można wprowadzić ręcznie lub Centrum IoT można wybierać z hello centra IoT, które są dostępne tooyou.</span><span class="sxs-lookup"><span data-stu-id="c0b31-112">hello settings for hello event source can be entered manually or an IoT hub can be selected from hello IoT hubs that are available tooyou.</span></span>
<span data-ttu-id="c0b31-113">W hello **opcję importu** selektora, wybierz jedną z hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="c0b31-113">In hello **Import Option** selector, choose one of hello following options:</span></span>

* <span data-ttu-id="c0b31-114">Podaj ustawienia Centrum IoT ręcznie</span><span class="sxs-lookup"><span data-stu-id="c0b31-114">Provide IoT Hub settings manually</span></span>
* <span data-ttu-id="c0b31-115">Użyj Centrum IoT z dostępnych subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c0b31-115">Use IoT Hub from available subscriptions</span></span>

### <a name="select-an-available-iot-hub"></a><span data-ttu-id="c0b31-116">Wybierz dostępny Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-116">Select an available IoT Hub</span></span>

<span data-ttu-id="c0b31-117">Hello poniższej tabeli opisano poszczególne opcje hello kartę nowe źródło zdarzeń z jego opisem podczas wybierania dostępne Centrum IoT jako źródło zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="c0b31-117">hello following table explains each option in hello New Event Source tab with its description when selecting an available IoT Hub as an event source:</span></span>

| <span data-ttu-id="c0b31-118">NAZWA WŁAŚCIWOŚCI</span><span class="sxs-lookup"><span data-stu-id="c0b31-118">PROPERTY NAME</span></span> | <span data-ttu-id="c0b31-119">OPIS</span><span class="sxs-lookup"><span data-stu-id="c0b31-119">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="c0b31-120">Nazwa źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c0b31-120">Event source name</span></span> | <span data-ttu-id="c0b31-121">Nazwa Hello źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c0b31-121">hello name of your event source.</span></span> <span data-ttu-id="c0b31-122">Ta nazwa musi być unikatowa w danym środowisku Insights serii czasu.</span><span class="sxs-lookup"><span data-stu-id="c0b31-122">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="c0b31-123">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="c0b31-123">Source</span></span> | <span data-ttu-id="c0b31-124">Wybierz **Centrum IoT** toocreate źródłem zdarzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-124">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="c0b31-125">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c0b31-125">Subscription Id</span></span> | <span data-ttu-id="c0b31-126">Wybierz subskrypcję hello, w której utworzono to Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-126">Select hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="c0b31-127">Nazwa centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-127">IoT hub name</span></span> | <span data-ttu-id="c0b31-128">Wybierz nazwę hello hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-128">Select hello name of hello IoT Hub.</span></span>
| <span data-ttu-id="c0b31-129">Nazwa zasad Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-129">IoT hub policy name</span></span> | <span data-ttu-id="c0b31-130">Wybierz zasad dostępu hello udostępnionych, które znajdują się na powitania kartę Ustawienia Centrum IoT. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia ustawić i klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0b31-130">Select hello shared access policy, which can be found on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="c0b31-131">Hello udostępnionych zasady dostępu dla źródła zdarzeń *musi* ma **usługa połączyć** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="c0b31-131">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="c0b31-132">Grupy odbiorców Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-132">IoT hub consumer group</span></span> | <span data-ttu-id="c0b31-133">Witaj grupy odbiorców zdarzeń tooread z hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-133">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="c0b31-134">Jest zdecydowanie zalecane toouse dedykowanej grupy klientów dla źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c0b31-134">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

### <a name="provide-iot-hub-settings-manually"></a><span data-ttu-id="c0b31-135">Podaj ustawienia Centrum IoT ręcznie</span><span class="sxs-lookup"><span data-stu-id="c0b31-135">Provide IoT Hub settings manually</span></span>

<span data-ttu-id="c0b31-136">Witaj poniższej tabeli opisano każdej właściwości w karcie nowe źródło zdarzeń hello z jego opisem podczas wprowadzania ustawień ręcznie:</span><span class="sxs-lookup"><span data-stu-id="c0b31-136">hello following table explains each property in hello New Event Source tab with its description when entering settings manually:</span></span>

| <span data-ttu-id="c0b31-137">NAZWA WŁAŚCIWOŚCI</span><span class="sxs-lookup"><span data-stu-id="c0b31-137">PROPERTY NAME</span></span> | <span data-ttu-id="c0b31-138">OPIS</span><span class="sxs-lookup"><span data-stu-id="c0b31-138">DESCRIPTION</span></span> |
| --- | --- |
| <span data-ttu-id="c0b31-139">Nazwa źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c0b31-139">Event source name</span></span> | <span data-ttu-id="c0b31-140">Nazwa Hello źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c0b31-140">hello name of your event source.</span></span> <span data-ttu-id="c0b31-141">Ta nazwa musi być unikatowa w danym środowisku Insights serii czasu.</span><span class="sxs-lookup"><span data-stu-id="c0b31-141">This name must be unique within your Time Series Insights environment.</span></span>
| <span data-ttu-id="c0b31-142">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="c0b31-142">Source</span></span> | <span data-ttu-id="c0b31-143">Wybierz **Centrum IoT** toocreate źródłem zdarzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-143">Choose **IoT Hub** toocreate an IoT Hub event source.</span></span>
| <span data-ttu-id="c0b31-144">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c0b31-144">Subscription Id</span></span> | <span data-ttu-id="c0b31-145">Subskrypcja Hello, w której utworzono to Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-145">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="c0b31-146">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="c0b31-146">Resource group</span></span> | <span data-ttu-id="c0b31-147">Subskrypcja Hello, w której utworzono to Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-147">hello subscription in which this IoT hub was created.</span></span>
| <span data-ttu-id="c0b31-148">Nazwa centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-148">IoT hub name</span></span> | <span data-ttu-id="c0b31-149">Nazwa Hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-149">hello name of your IoT Hub.</span></span> <span data-ttu-id="c0b31-150">Podczas tworzenia Centrum IoT należy też nadać mu nazwę</span><span class="sxs-lookup"><span data-stu-id="c0b31-150">When you created your IoT hub, you also gave it a specific name</span></span>
| <span data-ttu-id="c0b31-151">Nazwa zasad Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-151">IoT hub policy name</span></span> | <span data-ttu-id="c0b31-152">zasad dostępu Hello udostępnionych, które mogą być tworzone na powitania kartę Ustawienia Centrum IoT. Wszystkie zasady dostępu współdzielonego ma nazwę uprawnienia ustawić i klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="c0b31-152">hello shared access policy, which can be created on hello IoT Hub settings tab. Each shared access policy has a name, permissions that you set, and access keys.</span></span> <span data-ttu-id="c0b31-153">Hello udostępnionych zasady dostępu dla źródła zdarzeń *musi* ma **usługa połączyć** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="c0b31-153">hello shared access policy for your event source *must* have **service connect** permissions.</span></span>
| <span data-ttu-id="c0b31-154">Klucz zasad Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-154">IoT hub policy key</span></span> | <span data-ttu-id="c0b31-155">klucz dostęp współdzielony Hello używany tooauthenticate dostępu toohello — przestrzeń nazw magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="c0b31-155">hello Shared Access key used tooauthenticate access toohello Service Bus namespace.</span></span> <span data-ttu-id="c0b31-156">Typ hello klucz podstawowy lub pomocniczy tutaj.</span><span class="sxs-lookup"><span data-stu-id="c0b31-156">Type hello primary or secondary key here.</span></span>
| <span data-ttu-id="c0b31-157">Grupy odbiorców Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="c0b31-157">IoT hub consumer group</span></span> | <span data-ttu-id="c0b31-158">Witaj grupy odbiorców zdarzeń tooread z hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="c0b31-158">hello Consumer Group tooread events from hello IoT Hub.</span></span> <span data-ttu-id="c0b31-159">Jest zdecydowanie zalecane toouse dedykowanej grupy klientów dla źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="c0b31-159">It is highly recommended toouse a dedicated consumer group for your event source.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0b31-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c0b31-160">Next steps</span></span>

1. <span data-ttu-id="c0b31-161">Dodaj środowisku tooyour zasad dostępu do danych [danych Definiowanie zasad dostępu](time-series-insights-data-access.md)</span><span class="sxs-lookup"><span data-stu-id="c0b31-161">Add a data access policy tooyour environment [Define data access policies](time-series-insights-data-access.md)</span></span>
1. <span data-ttu-id="c0b31-162">Dostęp do środowiska w hello [portalu Insights serii czasu](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="c0b31-162">Access your environment in hello [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
