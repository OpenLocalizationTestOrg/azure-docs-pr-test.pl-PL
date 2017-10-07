---
title: aaaUse hello toocreate portalu Azure IoT Hub | Dokumentacja firmy Microsoft
description: "Jak toocreate, zarządzania i usuwania centra Azure IoT za pośrednictwem hello portalu Azure. Zawiera informacje na temat warstw cenowych, skalowania, zabezpieczeń i konfiguracji do obsługi komunikatów."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="bf896-104">Tworzenie Centrum IoT przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bf896-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="bf896-105">W tym artykule opisano:</span><span class="sxs-lookup"><span data-stu-id="bf896-105">This article describes:</span></span>

* <span data-ttu-id="bf896-106">Jak toofind hello usługi Centrum IoT w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bf896-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="bf896-107">Jak toocreate i zarządzanie nimi centra IoT.</span><span class="sxs-lookup"><span data-stu-id="bf896-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="bf896-108">Gdzie toofind hello usługi Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="bf896-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="bf896-109">Hello usługi Centrum IoT można znaleźć w następującej lokalizacji w portalu hello hello:</span><span class="sxs-lookup"><span data-stu-id="bf896-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="bf896-110">Wybierz **+ nowy**, a następnie wybierz **Internetu rzeczy**.</span><span class="sxs-lookup"><span data-stu-id="bf896-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="bf896-111">Hello Marketplace, wybierz **Internetu rzeczy**.</span><span class="sxs-lookup"><span data-stu-id="bf896-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="bf896-112">Tworzenie centrum IoT</span><span class="sxs-lookup"><span data-stu-id="bf896-112">Create an IoT hub</span></span>

<span data-ttu-id="bf896-113">Można utworzyć Centrum IoT przy użyciu hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="bf896-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="bf896-114">Witaj **+ nowy** opcji Otwiera blok hello pokazano powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="bf896-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="bf896-115">Witaj kroki tworzenia Centrum IoT hello za pomocą tej metody i za pośrednictwem portalu marketplace hello są identyczne.</span><span class="sxs-lookup"><span data-stu-id="bf896-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="bf896-116">Hello Marketplace, wybierz **Utwórz** bloku hello tooopen pokazano powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="bf896-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="bf896-117">Witaj poniższych sekcjach opisano hello kilka kroków toocreate Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="bf896-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="bf896-118">Wybierz nazwę hello hello Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="bf896-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="bf896-119">toocreate Centrum IoT można nazwać hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="bf896-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="bf896-120">Ta nazwa musi być unikatowa w wszystkie centra IoT.</span><span class="sxs-lookup"><span data-stu-id="bf896-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="bf896-121">Wybierz warstwę cenową hello</span><span class="sxs-lookup"><span data-stu-id="bf896-121">Choose hello pricing tier</span></span>

<span data-ttu-id="bf896-122">Możesz wybrać spośród czterech warstw: **wolne**, **Standard 1** i **standardowy 2**, i **standardowa S3**.</span><span class="sxs-lookup"><span data-stu-id="bf896-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="bf896-123">Warstwa bezpłatna Hello umożliwia tylko 500 toobe urządzenia połączone z Centrum IoT toohello oraz too8, 000 wiadomości na dzień.</span><span class="sxs-lookup"><span data-stu-id="bf896-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="bf896-124">**Standardowa S1**: Użyj hello S1 edition dla rozwiązania IoT z dużą liczbą urządzeń, że wygenerowany dla każdego niewielkich ilości danych.</span><span class="sxs-lookup"><span data-stu-id="bf896-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="bf896-125">Umożliwia każdej jednostki edition hello S1 się too400, 000 wiadomości na dzień dla wszystkich połączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="bf896-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="bf896-126">**Standardowa S2**: Użyj hello S2 edition dla rozwiązania IoT, w których urządzenie wygenerować dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="bf896-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="bf896-127">Każdej jednostki hello S2 edition umożliwia się too6 milionów wiadomości na dzień między wszystkich połączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="bf896-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="bf896-128">**Standardowa S3**: Użyj hello S3 edition dla rozwiązania IoT, które generują dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="bf896-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="bf896-129">Każdej jednostki hello S3 edition umożliwia się too300 milionów wiadomości na dzień między wszystkich połączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="bf896-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="bf896-130">Centrum IoT umożliwia tylko koncentratorze wolne dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf896-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="bf896-131">Jednostki Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="bf896-131">IoT hub units</span></span>

<span data-ttu-id="bf896-132">Hello liczbę wiadomości dozwolonych dla jednej jednostki dziennie zależy od warstwy cenowej Twoje Centrum.</span><span class="sxs-lookup"><span data-stu-id="bf896-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="bf896-133">Na przykład jeśli chcesz, aby hello wejściowych toosupport Centrum IoT 700 000 komunikatów, wybierz dwie jednostki warstwy S1.</span><span class="sxs-lookup"><span data-stu-id="bf896-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="bf896-134">Partycje toocloud urządzenia i grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="bf896-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="bf896-135">Możesz zmienić hello liczba partycji dla Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="bf896-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="bf896-136">Witaj domyślny numer partycji jest 4, z listy rozwijanej hello można wybrać inny numer.</span><span class="sxs-lookup"><span data-stu-id="bf896-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="bf896-137">Nie trzeba tooexplicitly utworzyć pustej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bf896-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="bf896-138">Podczas tworzenia zasobu, można wybrać albo toocreate nowy lub użyć istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="bf896-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="bf896-139">Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="bf896-139">Choose subscription</span></span>

<span data-ttu-id="bf896-140">Centrum IoT Azure automatycznie hello list konta użytkownika hello subskrypcji platformy Azure jest połączony.</span><span class="sxs-lookup"><span data-stu-id="bf896-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="bf896-141">Można wybrać hello Centrum IoT hello tooassociate subskrypcji platformy Azure do.</span><span class="sxs-lookup"><span data-stu-id="bf896-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="bf896-142">Wybierz lokalizację hello</span><span class="sxs-lookup"><span data-stu-id="bf896-142">Choose hello location</span></span>

<span data-ttu-id="bf896-143">Opcja lokalizacji Hello zawiera listę regionów hello, w którym Centrum IoT jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="bf896-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="bf896-144">Tworzenie Centrum IoT hello</span><span class="sxs-lookup"><span data-stu-id="bf896-144">Create hello IoT hub</span></span>

<span data-ttu-id="bf896-145">Po zakończeniu wszystkich poprzednich kroków, można utworzyć hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="bf896-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="bf896-146">Kliknij przycisk **Utwórz** toostart hello toocreate procesu zaplecza i wdrażanie hello Centrum IoT z opcjami hello została wybrana opcja.</span><span class="sxs-lookup"><span data-stu-id="bf896-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="bf896-147">Jako zajmuje trochę czasu toorun wdrożenia zaplecza hello na serwerach odpowiednią lokalizację hello może potrwać kilka minut toocreate hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="bf896-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="bf896-148">Zmień ustawienia hello hello Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="bf896-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="bf896-149">Ustawienia hello istniejących Centrum IoT można zmienić po jego utworzeniu z hello blok Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="bf896-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="bf896-150">**Zasady dostępu do udostępnionych**: te zasady definiują hello uprawnienia do urządzeń i usług tooIoT tooconnect koncentratora.</span><span class="sxs-lookup"><span data-stu-id="bf896-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="bf896-151">Te zasady można uzyskać, klikając **zasady dostępu współużytkowanego** w obszarze **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="bf896-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="bf896-152">W tym bloku należy modyfikowania istniejących zasad lub Dodaj nowe zasady.</span><span class="sxs-lookup"><span data-stu-id="bf896-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="bf896-153">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="bf896-153">Create a policy</span></span>

* <span data-ttu-id="bf896-154">Kliknij przycisk **Dodaj** tooopen bloku.</span><span class="sxs-lookup"><span data-stu-id="bf896-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="bf896-155">Tutaj można wprowadzić hello nową nazwę zasady i uprawnienia hello mają tooassociate z tymi zasadami, jak pokazano poniżej hello rysunek:</span><span class="sxs-lookup"><span data-stu-id="bf896-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="bf896-156">Istnieje kilka uprawnienia, które mogą być skojarzone z tych zasad udostępnionych.</span><span class="sxs-lookup"><span data-stu-id="bf896-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="bf896-157">Witaj **odczytać rejestru** i **zapisu rejestru** zasady przyznać odczytu i zapisu prawa toohello tożsamości rejestru.</span><span class="sxs-lookup"><span data-stu-id="bf896-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="bf896-158">Wybranie opcji zapisu hello automatycznie wybiera hello odczytu opcji.</span><span class="sxs-lookup"><span data-stu-id="bf896-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="bf896-159">Witaj **połączenia usługi** zasad punktów końcowych usługi tooaccess uprawnienia są daje takie jak **odbierania urządzenia do chmury**.</span><span class="sxs-lookup"><span data-stu-id="bf896-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="bf896-160">Witaj **urządzenie połączyć** zasad przyznaje uprawnienia do wysyłania i odbierania wiadomości za pomocą punktów końcowych powitania po stronie urządzenia IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="bf896-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="bf896-161">Kliknij przycisk **Utwórz** tooadd tym nowo utworzone zasady toohello istniejącej listy.</span><span class="sxs-lookup"><span data-stu-id="bf896-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="bf896-162">Punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="bf896-162">Endpoints</span></span>

<span data-ttu-id="bf896-163">Kliknij przycisk **punkty końcowe** toodisplay listę punktów końcowych dla Centrum IoT hello, która jest modyfikowana.</span><span class="sxs-lookup"><span data-stu-id="bf896-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="bf896-164">Istnieją dwa typy punktów końcowych: punkty końcowe wbudowanych w Centrum IoT hello i dodaj Centrum IoT toohello po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="bf896-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="bf896-165">Wbudowane punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="bf896-165">Built-in endpoints</span></span>

<span data-ttu-id="bf896-166">Istnieją dwa punkty końcowe wbudowanych: **chmury opinii toodevice** i **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="bf896-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="bf896-167">**Chmury opinii toodevice** ustawienia: to ustawienie nie ma dwa subsettings: **chmury tooDevice TTL** (time-to-live) i **czas przechowywania** (w godzinach) dla wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="bf896-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="bf896-168">Podczas pierwszego tworzenia Centrum IoT, oba te ustawienia mają wartość hello jedną godzinę.</span><span class="sxs-lookup"><span data-stu-id="bf896-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="bf896-169">tooadjust te ustawienia za pomocą suwaków hello, lub wpisz hello wartości.</span><span class="sxs-lookup"><span data-stu-id="bf896-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="bf896-170">**Zdarzenia** ustawienia: to ustawienie nie ma kilka subsettings, niektóre z nich są tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="bf896-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="bf896-171">następujące listy Hello opisano te ustawienia:</span><span class="sxs-lookup"><span data-stu-id="bf896-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="bf896-172">**Partycje**: ustawiono wartość domyślną, podczas tworzenia Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="bf896-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="bf896-173">Hello liczby partycji za pomocą tego ustawienia można zmienić.</span><span class="sxs-lookup"><span data-stu-id="bf896-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="bf896-174">**Nazwa zgodnych z Centrum zdarzeń i punktu końcowego**: podczas tworzenia Centrum IoT hello, że może muszą uzyskać dostęp toounder pewnych okolicznościach wewnętrznie tworzenia Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="bf896-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="bf896-175">Nie można przypisać wartości nazwy i punktu końcowego hello zgodnego Centrum zdarzeń, ale można je skopiować, klikając **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="bf896-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="bf896-176">**Czas przechowywania**: domyślnie ustawiony dzień tooone, ale można zmienić za pomocą listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="bf896-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="bf896-177">Ta wartość jest w dniach hello ustawienia urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="bf896-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="bf896-178">**Grupy konsumentów**: wiele komunikatów tooread czytników niezależnie od centrum IoT hello włączyć grupy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="bf896-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="bf896-179">Każdy Centrum IoT tworzona jest domyślna grupa odbiorców.</span><span class="sxs-lookup"><span data-stu-id="bf896-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="bf896-180">Jednak można dodać lub usunąć konsumenta grup tooyour centra IoT za pomocą tego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="bf896-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bf896-181">Domyślna grupa odbiorców Hello nie można edytować ani usunąć.</span><span class="sxs-lookup"><span data-stu-id="bf896-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="bf896-182">Niestandardowe punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="bf896-182">Custom endpoints</span></span>

<span data-ttu-id="bf896-183">Można dodać niestandardowe punkty końcowe Centrum IoT przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="bf896-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="bf896-184">Z hello **punkty końcowe** bloku, kliknij przycisk **Dodaj** na powitania top tooopen hello **dodać punkt końcowy** bloku.</span><span class="sxs-lookup"><span data-stu-id="bf896-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="bf896-185">Wprowadź informacje wymagane hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf896-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="bf896-186">Niestandardowe punktu końcowego zostanie wyświetlony w głównym hello **punkty końcowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="bf896-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="bf896-187">Więcej informacje niestandardowe punkty końcowe w [odwołanie — punkty końcowe Centrum IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="bf896-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="bf896-188">Trasy</span><span class="sxs-lookup"><span data-stu-id="bf896-188">Routes</span></span>

<span data-ttu-id="bf896-189">Kliknij przycisk **tras** toomanage jak Centrum IoT wysyła wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="bf896-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="bf896-190">Centrum IoT tooyour tras można dodać, klikając **Dodaj** u góry hello hello **tras*** bloku wprowadzania informacji hello wymagane, a następnie klikając polecenie **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf896-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="bf896-191">Twoje trasy następnie znajduje się w głównym hello **tras** bloku.</span><span class="sxs-lookup"><span data-stu-id="bf896-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="bf896-192">Można edytować trasę, klikając go na liście hello tras.</span><span class="sxs-lookup"><span data-stu-id="bf896-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="bf896-193">tooenable trasy, kliknij go na liście hello tras i ustaw hello **włączone** Przełącz zbyt**poza**.</span><span class="sxs-lookup"><span data-stu-id="bf896-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="bf896-194">toosave hello zmiany, kliknij przycisk **OK** u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="bf896-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="bf896-195">Ceny i skala</span><span class="sxs-lookup"><span data-stu-id="bf896-195">Pricing and scale</span></span>

<span data-ttu-id="bf896-196">Hello cen istniejących Centrum IoT można zmienić, modyfikując hello **cennik** ustawienia z hello następujące wyjątki:</span><span class="sxs-lookup"><span data-stu-id="bf896-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="bf896-197">W hello bieżąca implementacja Centrum IoT z bezpłatnej wersji nie można zmienić warstwy tooone z hello płatnej jednostki SKU, albo na odwrót.</span><span class="sxs-lookup"><span data-stu-id="bf896-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="bf896-198">Może istnieć tylko jeden Centrum IoT warstwę bezpłatna w hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf896-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="bf896-199">Można przenosić z wyższego poziomu toolower tylko wtedy, gdy hello liczbę komunikatów wysłanych tego dnia przekracza hello przydziału hello dolnej warstwy.</span><span class="sxs-lookup"><span data-stu-id="bf896-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="bf896-200">Na przykład jeśli hello liczbę wiadomości na dzień przekracza 400 000, hello warstwę hello IoT hub można zmienić.</span><span class="sxs-lookup"><span data-stu-id="bf896-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="bf896-201">Jednak w przypadku zmiany warstwy S1 toohello Centrum IoT hello jest ograniczany do danego dnia.</span><span class="sxs-lookup"><span data-stu-id="bf896-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="bf896-202">Usuń hello Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="bf896-202">Delete hello IoT hub</span></span>

<span data-ttu-id="bf896-203">Możesz przeglądać Centrum IoT toohello ma toodelete klikając **Przeglądaj**, i wybierając hello toodelete odpowiedniego koncentratora.</span><span class="sxs-lookup"><span data-stu-id="bf896-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="bf896-204">toodelete hello Centrum IoT, kliknij przycisk hello **usunąć** znajdujący się poniżej nazwę Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="bf896-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf896-205">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bf896-205">Next steps</span></span>

<span data-ttu-id="bf896-206">Wykonaj te toolearn łącza więcej informacji na temat zarządzania Centrum IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="bf896-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="bf896-207">[Zbiorcze zarządzania urządzeniami IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="bf896-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="bf896-208">[Metryki Centrum IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="bf896-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="bf896-209">[Operacje monitorowania][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="bf896-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="bf896-210">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="bf896-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="bf896-211">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="bf896-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="bf896-212">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="bf896-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="bf896-213">[Zabezpieczanie rozwiązania IoT z hello tła w][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="bf896-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
