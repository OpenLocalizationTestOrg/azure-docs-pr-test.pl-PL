---
title: "aaaCapture danych z usługi Event Hubs do usługi Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Data Lake Store toocapture danych z usługi Event Hubs"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="397e1-103">Użyj usługi Azure Data Lake Store toocapture danych z usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="397e1-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="397e1-104">Dowiedz się, jak toouse Azure Data Lake Store toocapture danych odebranych przez usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="397e1-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="397e1-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="397e1-105">Prerequisites</span></span>

* <span data-ttu-id="397e1-106">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="397e1-106">**An Azure subscription**.</span></span> <span data-ttu-id="397e1-107">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="397e1-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="397e1-108">**Konto usługi Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="397e1-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="397e1-109">Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="397e1-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="397e1-110">**Centra zdarzeń w przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="397e1-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="397e1-111">Aby uzyskać instrukcje, zobacz [tworzenie przestrzeni nazw usługi Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="397e1-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="397e1-112">Upewnij się, że konto usługi Data Lake Store hello i przestrzeni nazw usługi Event Hubs hello znajdują się w hello tej samej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="397e1-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="397e1-113">Przypisz uprawnienia tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="397e1-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="397e1-114">W tej sekcji należy utworzyć folder w ramach konta hello miejscu toocapture hello dane z usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="397e1-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="397e1-115">Można także przypisać uprawnienia koncentratory tooEvent tak, aby ją zapisać danych do konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="397e1-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="397e1-116">Otwieranie konta usługi Data Lake Store hello gdzie toocapture dane z usługi Event Hubs, a następnie kliknij polecenie **Eksploratora danych**.</span><span class="sxs-lookup"><span data-stu-id="397e1-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="397e1-117">![Eksplorator danych Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Eksploratora danych usługi Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="397e1-118">Kliknij przycisk **nowy Folder** , a następnie wprowadź nazwę folderu, w którym ma toocapture hello danych.</span><span class="sxs-lookup"><span data-stu-id="397e1-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="397e1-119">![Utwórz nowy folder w usłudze Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Utwórz nowy folder w usłudze Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="397e1-120">Przypisz uprawnienia w katalogu głównym hello hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="397e1-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="397e1-121">a.</span><span class="sxs-lookup"><span data-stu-id="397e1-121">a.</span></span> <span data-ttu-id="397e1-122">Kliknij przycisk **Eksploratora danych**wybierz katalog główny hello hello konta usługi Data Lake Store, a następnie kliknij przycisk **dostępu**.</span><span class="sxs-lookup"><span data-stu-id="397e1-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="397e1-123">![Przypisywanie uprawnień do katalogu głównego usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "przypisać uprawnienia dla elementu głównego usługi Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="397e1-124">b.</span><span class="sxs-lookup"><span data-stu-id="397e1-124">b.</span></span> <span data-ttu-id="397e1-125">W obszarze **dostępu**, kliknij przycisk **Dodaj**, kliknij przycisk **Wybieranie użytkownika lub grupy**, a następnie wyszukaj `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="397e1-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="397e1-126">![Przypisywanie uprawnień do katalogu głównego usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "przypisać uprawnienia dla elementu głównego usługi Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="397e1-127">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="397e1-127">Click **Select**.</span></span>

    <span data-ttu-id="397e1-128">c.</span><span class="sxs-lookup"><span data-stu-id="397e1-128">c.</span></span> <span data-ttu-id="397e1-129">W obszarze **przypisywanie uprawnień**, kliknij przycisk **wybierz uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="397e1-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="397e1-130">Ustaw **uprawnienia** za**Execute**.</span><span class="sxs-lookup"><span data-stu-id="397e1-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="397e1-131">Ustaw **dodać do** za**ten folder i wszystkie obiekty podrzędne**.</span><span class="sxs-lookup"><span data-stu-id="397e1-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="397e1-132">Ustaw **dodać jako** za**wpisu uprawnienia dostępu i wpis uprawnienia domyślne**.</span><span class="sxs-lookup"><span data-stu-id="397e1-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="397e1-133">![Przypisywanie uprawnień do katalogu głównego usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "przypisać uprawnienia dla elementu głównego usługi Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="397e1-134">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="397e1-134">Click **OK**.</span></span>

4. <span data-ttu-id="397e1-135">Przypisanie uprawnień dla folderu hello w ramach konta usługi Data Lake Store, w którym ma toocapture danych.</span><span class="sxs-lookup"><span data-stu-id="397e1-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="397e1-136">a.</span><span class="sxs-lookup"><span data-stu-id="397e1-136">a.</span></span> <span data-ttu-id="397e1-137">Kliknij przycisk **Eksploratora danych**, wybierz hello folder hello konta usługi Data Lake Store, a następnie kliknij przycisk **dostępu**.</span><span class="sxs-lookup"><span data-stu-id="397e1-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="397e1-138">![Przypisanie uprawnień dla folderu usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "przypisanie uprawnień dla folderu usługi Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="397e1-139">b.</span><span class="sxs-lookup"><span data-stu-id="397e1-139">b.</span></span> <span data-ttu-id="397e1-140">W obszarze **dostępu**, kliknij przycisk **Dodaj**, kliknij przycisk **Wybieranie użytkownika lub grupy**, a następnie wyszukaj `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="397e1-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="397e1-141">![Przypisanie uprawnień dla folderu usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "przypisanie uprawnień dla folderu usługi Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="397e1-142">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="397e1-142">Click **Select**.</span></span>

    <span data-ttu-id="397e1-143">c.</span><span class="sxs-lookup"><span data-stu-id="397e1-143">c.</span></span> <span data-ttu-id="397e1-144">W obszarze **przypisywanie uprawnień**, kliknij przycisk **wybierz uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="397e1-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="397e1-145">Ustaw **uprawnienia** za**Odczyt, zapis,** i **Execute**.</span><span class="sxs-lookup"><span data-stu-id="397e1-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="397e1-146">Ustaw **dodać do** za**ten folder i wszystkie obiekty podrzędne**.</span><span class="sxs-lookup"><span data-stu-id="397e1-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="397e1-147">Wreszcie, ustaw **dodać jako** za**wpisu uprawnienia dostępu i wpis uprawnienia domyślne**.</span><span class="sxs-lookup"><span data-stu-id="397e1-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="397e1-148">![Przypisanie uprawnień dla folderu usługi Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "przypisanie uprawnień dla folderu usługi Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="397e1-149">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="397e1-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="397e1-150">Konfigurowanie usługi Event Hubs toocapture tooData usługi data Lake Store</span><span class="sxs-lookup"><span data-stu-id="397e1-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="397e1-151">W tej sekcji utworzysz Centrum zdarzeń w przestrzeni nazw usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="397e1-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="397e1-152">Możesz również skonfigurować hello Centrum zdarzeń toocapture danych tooan konta usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="397e1-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="397e1-153">W tej sekcji założono, że utworzono już przestrzeń nazw usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="397e1-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="397e1-154">Z hello **omówienie** kliknij okienko hello przestrzeni nazw usługi Event Hubs, **+ Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="397e1-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="397e1-155">![Tworzenie Centrum zdarzeń](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "tworzenia Centrum zdarzeń")</span><span class="sxs-lookup"><span data-stu-id="397e1-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="397e1-156">Podaj poniżej hello wartości tooconfigure usługi Event Hubs toocapture danych tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="397e1-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="397e1-157">![Tworzenie Centrum zdarzeń](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "tworzenia Centrum zdarzeń")</span><span class="sxs-lookup"><span data-stu-id="397e1-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="397e1-158">a.</span><span class="sxs-lookup"><span data-stu-id="397e1-158">a.</span></span> <span data-ttu-id="397e1-159">Podaj nazwę hello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="397e1-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="397e1-160">b.</span><span class="sxs-lookup"><span data-stu-id="397e1-160">b.</span></span> <span data-ttu-id="397e1-161">W tym samouczku, ustaw **liczba partycji** i **przechowywania wiadomości** toohello wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="397e1-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="397e1-162">c.</span><span class="sxs-lookup"><span data-stu-id="397e1-162">c.</span></span> <span data-ttu-id="397e1-163">Ustaw **przechwytywania** za**na**.</span><span class="sxs-lookup"><span data-stu-id="397e1-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="397e1-164">Zestaw hello **przedział czasu** (częstotliwość toocapture) i **rozmiar okna** (toocapture rozmiar danych).</span><span class="sxs-lookup"><span data-stu-id="397e1-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="397e1-165">d.</span><span class="sxs-lookup"><span data-stu-id="397e1-165">d.</span></span> <span data-ttu-id="397e1-166">Dla **przechwytywania dostawcy**, wybierz pozycję **Azure Data Lake Store** i hello wybierz hello utworzoną wcześniej usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="397e1-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="397e1-167">Dla **Data Lake ścieżka**, wprowadź nazwę hello hello folderu utworzonego w hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="397e1-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="397e1-168">Wystarczy tooprovide hello ścieżki względnej toohello folderu.</span><span class="sxs-lookup"><span data-stu-id="397e1-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="397e1-169">e.</span><span class="sxs-lookup"><span data-stu-id="397e1-169">e.</span></span> <span data-ttu-id="397e1-170">Pozostaw hello **formatów nazwy pliku przechwytywania próbki** toohello wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="397e1-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="397e1-171">Ta opcja reguluje hello struktury folderów, który jest tworzony w folderze przechwytywania hello.</span><span class="sxs-lookup"><span data-stu-id="397e1-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="397e1-172">f.</span><span class="sxs-lookup"><span data-stu-id="397e1-172">f.</span></span> <span data-ttu-id="397e1-173">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="397e1-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="397e1-174">Instalator hello testu</span><span class="sxs-lookup"><span data-stu-id="397e1-174">Test hello setup</span></span>

<span data-ttu-id="397e1-175">Teraz możesz przetestować rozwiązania hello wysyłając toohello danych Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="397e1-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="397e1-176">Postępuj zgodnie z instrukcjami hello w [wysyłać zdarzenia tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="397e1-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="397e1-177">Po uruchomieniu wysyłanie danych hello, zostaną wyświetlone hello dane zostaną uwzględnione w usłudze Data Lake Store za pomocą struktury folderów hello określona.</span><span class="sxs-lookup"><span data-stu-id="397e1-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="397e1-178">Na przykład zostanie wyświetlony strukturę folderów, jak pokazano w hello następującego zrzutu ekranu w usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="397e1-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="397e1-179">![Przykładowe dane EventHub w usłudze Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "EventHub przykładowych danych w usłudze Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="397e1-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="397e1-180">Nawet jeśli nie masz wiadomości przychodzących do usługi Event Hubs, usługa Event Hubs zapisuje pustych plików z tylko nagłówki hello do hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="397e1-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="397e1-181">Witaj pliki są zapisywane na powitania sam podanemu podczas tworzenia usługi Event Hubs hello interwał czasu.</span><span class="sxs-lookup"><span data-stu-id="397e1-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="397e1-182">Analizowanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="397e1-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="397e1-183">Po hello danych w usłudze Data Lake Store można uruchamiać zadania analityczne dane hello tooprocess i wykonywać.</span><span class="sxs-lookup"><span data-stu-id="397e1-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="397e1-184">Zobacz [USQL Avro przykład](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) na temat toodo to przy użyciu usługi Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="397e1-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="397e1-185">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="397e1-185">See also</span></span>
* [<span data-ttu-id="397e1-186">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="397e1-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="397e1-187">Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="397e1-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
