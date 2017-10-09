---
title: "Konto usługi partia zadań w portalu Azure hello aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate partii zadań Azure konto hello Azure toorun portalu dużych obciążeń równoległe w chmurze hello"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="952e0-103">Tworzenie konta usługi partia zadań z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="952e0-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="952e0-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="952e0-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="952e0-105">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="952e0-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="952e0-106">Dowiedz się, jak konto partii zadań Azure toocreate hello [portalu Azure][azure_portal]i wybierz polecenie Właściwości hello konta, które pasują do danego scenariusza obliczeń.</span><span class="sxs-lookup"><span data-stu-id="952e0-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="952e0-107">Dowiedz się, gdy toofind konta ważne właściwości, takie jak klucze dostępu i adres URL konta.</span><span class="sxs-lookup"><span data-stu-id="952e0-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="952e0-108">Dalsze informacje dotyczące konta usługi partia zadań i scenariusze, można znaleźć hello [funkcji — omówienie](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="952e0-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="952e0-109">Tworzenie konta usługi Batch</span><span class="sxs-lookup"><span data-stu-id="952e0-109">Create a Batch account</span></span>

<span data-ttu-id="952e0-110">Użyj hello toocreate portalu konta usługi partia zadań w jednym z dwóch hello *puli tryby alokacji*: **partii usługi** tryb lub nowszej hello **subskrypcji użytkownika** tryb, który wymaga więcej Konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="952e0-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="952e0-111">Aby uzyskać informacje dotyczące tych dwóch trybów, zobacz hello [funkcji — omówienie](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="952e0-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="952e0-112">Dla funkcji trybu subskrypcji użytkownika hello, zobacz też hello [wpis w blogu](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="952e0-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="952e0-113">Tryb usługi Batch</span><span class="sxs-lookup"><span data-stu-id="952e0-113">Batch service mode</span></span>



1. <span data-ttu-id="952e0-114">Zaloguj się toohello [portalu Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="952e0-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="952e0-115">Kliknij kolejno opcje **Nowy** > **Obliczenia** > **Usługa Batch**.</span><span class="sxs-lookup"><span data-stu-id="952e0-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Partia hello Marketplace][marketplace_portal]
3. <span data-ttu-id="952e0-117">Witaj **nowe konto wsadowe** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="952e0-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="952e0-118">Patrz opisy hello poniżej poszczególnych elementów bloku.</span><span class="sxs-lookup"><span data-stu-id="952e0-118">See hello descriptions below of each blade element.</span></span>

    ![Tworzenie konta usługi Batch][account_portal]

    <span data-ttu-id="952e0-120">a.</span><span class="sxs-lookup"><span data-stu-id="952e0-120">a.</span></span> <span data-ttu-id="952e0-121">**Nazwa konta**: Nazwa konta wsadowego hello wybierzesz muszą być unikatowe w hello region platformy Azure, gdzie jest utworzone konto hello (zobacz **lokalizacji** poniżej).</span><span class="sxs-lookup"><span data-stu-id="952e0-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="952e0-122">Witaj, nazwa konta może zawierać tylko małe litery lub cyfry i musi składać się z 3 do 24 znaków.</span><span class="sxs-lookup"><span data-stu-id="952e0-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="952e0-123">b.</span><span class="sxs-lookup"><span data-stu-id="952e0-123">b.</span></span> <span data-ttu-id="952e0-124">**Subskrypcja**: hello subskrypcji, w których hello toocreate konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="952e0-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="952e0-125">Jeśli masz tylko jedną subskrypcję, jest ona wybrana domyślnie.</span><span class="sxs-lookup"><span data-stu-id="952e0-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="952e0-126">c.</span><span class="sxs-lookup"><span data-stu-id="952e0-126">c.</span></span> <span data-ttu-id="952e0-127">**Tryb alokacji puli**: wybierz **Usługa Batch**.</span><span class="sxs-lookup"><span data-stu-id="952e0-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="952e0-128">c.</span><span class="sxs-lookup"><span data-stu-id="952e0-128">c.</span></span> <span data-ttu-id="952e0-129">**Grupa zasobów**: wybierz istniejącą grupę zasobów dla nowego konta usługi Batch. Opcjonalnie można utworzyć nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="952e0-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="952e0-130">d.</span><span class="sxs-lookup"><span data-stu-id="952e0-130">d.</span></span> <span data-ttu-id="952e0-131">**Lokalizacja**: hello region platformy Azure, w których hello toocreate konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="952e0-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="952e0-132">Tylko regiony hello obsługiwane przez subskrypcji i grupy zasobów są wyświetlane jako opcje.</span><span class="sxs-lookup"><span data-stu-id="952e0-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="952e0-133">e.</span><span class="sxs-lookup"><span data-stu-id="952e0-133">e.</span></span> <span data-ttu-id="952e0-134">**Konto magazynu** (opcjonalne): konto usługi Azure Storage ogólnego przeznaczenia skojarzone z kontem usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="952e0-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="952e0-135">Jest to zalecane w przypadku większości kont usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="952e0-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="952e0-136">Więcej szczegółów można znaleźć w sekcji [Połączone konto usługi Azure Storage](#linked-azure-storage-account) w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="952e0-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="952e0-137">Kliknij przycisk **Utwórz** toocreate hello konta.</span><span class="sxs-lookup"><span data-stu-id="952e0-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="952e0-138">Hello portal wskazuje, że wdrożenie jest w toku.</span><span class="sxs-lookup"><span data-stu-id="952e0-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="952e0-139">Po zakończeniu w obszarze **Powiadomienia** pojawia się powiadomienie **Wdrożenie zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="952e0-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="952e0-140">Tryb subskrypcji użytkownika</span><span class="sxs-lookup"><span data-stu-id="952e0-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="952e0-141">Zezwalaj na tooaccess partii zadań Azure hello subskrypcji (jednorazowa operacja)</span><span class="sxs-lookup"><span data-stu-id="952e0-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="952e0-142">Podczas tworzenia konta usługi partia zadań pierwszy w trybie użytkownika subskrypcji, należy wykonać następujące kroki tooregister hello subskrypcji z partii.</span><span class="sxs-lookup"><span data-stu-id="952e0-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="952e0-143">(Jeśli wcześniej została to, Pomiń toohello następnej sekcji).</span><span class="sxs-lookup"><span data-stu-id="952e0-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="952e0-144">Zaloguj się toohello [portalu Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="952e0-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="952e0-145">Kliknij przycisk **więcej usług** > **subskrypcje**i kliknij subskrypcję hello ma toouse hello konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="952e0-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="952e0-146">W hello **subskrypcji** bloku, kliknij przycisk **(IAM) kontroli dostępu** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="952e0-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Kontrola dostępu do subskrypcji][subscription_access]

4. <span data-ttu-id="952e0-148">Na powitania **dodać uprawnienia** bloku, wybierz hello **współautora** roli, wyszukaj hello interfejsu API partii.</span><span class="sxs-lookup"><span data-stu-id="952e0-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="952e0-149">Wyszukiwania dla każdego z tych parametrów do momentu znalezienia hello interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="952e0-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="952e0-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="952e0-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="952e0-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="952e0-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="952e0-152">W przypadku nowszych dzierżaw usługi Azure AD może być używana ta nazwa.</span><span class="sxs-lookup"><span data-stu-id="952e0-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="952e0-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** jest identyfikator hello hello interfejsu API partii.</span><span class="sxs-lookup"><span data-stu-id="952e0-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="952e0-154">Po znalezieniu hello interfejsu API partii, zaznacz go i kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="952e0-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Dodawanie uprawnień usługi Batch][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="952e0-156">Tworzenie magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="952e0-156">Create a key vault</span></span>
<span data-ttu-id="952e0-157">W trybie użytkownika subskrypcji usługi Azure key vault jest wymagana należący toothe tej samej grupie zasobów co toobe konta wsadowego hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="952e0-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="952e0-158">Upewnij się, że grupa zasobów hello znajduje się w regionie, w przypadku partii [dostępne](https://azure.microsoft.com/regions/services/) , które obsługuje subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="952e0-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="952e0-159">W hello [portalu Azure][azure_portal], kliknij przycisk **nowy** > **bezpieczeństwo i Obsługa tożsamości** > **magazyn kluczy** .</span><span class="sxs-lookup"><span data-stu-id="952e0-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="952e0-160">W hello **utworzyć magazyn kluczy** bloku, wprowadź nazwę dla magazynu kluczy hello i Utwórz grupę zasobów w regionie powitania dla Twojego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="952e0-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="952e0-161">Pozostaw hello pozostałe ustawienia na wartości domyślne, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="952e0-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="952e0-162">Tworzenie konta usługi Batch</span><span class="sxs-lookup"><span data-stu-id="952e0-162">Create a Batch account</span></span>

1. <span data-ttu-id="952e0-163">W hello [portalu Azure][azure_portal], kliknij przycisk **nowy** > **obliczeniowe** > **usługa partia zadań**.</span><span class="sxs-lookup"><span data-stu-id="952e0-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Partia hello Marketplace][marketplace_portal]
3. <span data-ttu-id="952e0-165">Witaj **nowe konto wsadowe** bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="952e0-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="952e0-166">Patrz opisy hello poniżej poszczególnych elementów bloku.</span><span class="sxs-lookup"><span data-stu-id="952e0-166">See hello descriptions below of each blade element.</span></span>

    ![Tworzenie konta usługi Batch][account_portal_byos]

    <span data-ttu-id="952e0-168">a.</span><span class="sxs-lookup"><span data-stu-id="952e0-168">a.</span></span> <span data-ttu-id="952e0-169">**Nazwa konta**: Nazwa konta wsadowego hello wybierzesz muszą być unikatowe w hello region platformy Azure, gdzie jest utworzone konto hello (zobacz **lokalizacji** poniżej).</span><span class="sxs-lookup"><span data-stu-id="952e0-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="952e0-170">Witaj, nazwa konta może zawierać tylko małe litery lub cyfry i musi składać się z 3 do 24 znaków.</span><span class="sxs-lookup"><span data-stu-id="952e0-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="952e0-171">b.</span><span class="sxs-lookup"><span data-stu-id="952e0-171">b.</span></span> <span data-ttu-id="952e0-172">**Subskrypcja**: Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello, który został zarejestrowany z hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="952e0-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="952e0-173">c.</span><span class="sxs-lookup"><span data-stu-id="952e0-173">c.</span></span> <span data-ttu-id="952e0-174">**Tryb alokacji puli**: wybierz pozycję **Subskrypcja użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="952e0-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="952e0-175">d.</span><span class="sxs-lookup"><span data-stu-id="952e0-175">d.</span></span> <span data-ttu-id="952e0-176">**Magazyn kluczy**: hello wybierz magazyn kluczy został utworzony dla konta wsadowego w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="952e0-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="952e0-177">Opcjonalnie utwórz nowy magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="952e0-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="952e0-178">Po wybraniu hello magazynu, wybierz hello wyboru toogrant partii zadań Azure dostępu toohello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="952e0-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="952e0-179">c.</span><span class="sxs-lookup"><span data-stu-id="952e0-179">c.</span></span> <span data-ttu-id="952e0-180">**Grupa zasobów**: hello wybierz grupę zasobów, w którym został utworzony magazyn kluczy hello.</span><span class="sxs-lookup"><span data-stu-id="952e0-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="952e0-181">d.</span><span class="sxs-lookup"><span data-stu-id="952e0-181">d.</span></span> <span data-ttu-id="952e0-182">**Lokalizacja**: hello region platformy Azure, w której utworzono hello magazynu kluczy dla konta wsadowego hello.</span><span class="sxs-lookup"><span data-stu-id="952e0-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="952e0-183">e.</span><span class="sxs-lookup"><span data-stu-id="952e0-183">e.</span></span> <span data-ttu-id="952e0-184">**Konto magazynu** (opcjonalne): konto usługi Azure Storage ogólnego przeznaczenia skojarzone z kontem usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="952e0-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="952e0-185">Jest to zalecane w przypadku większości kont usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="952e0-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="952e0-186">Więcej szczegółów zamieszczono w sekcji [Połączone konto usługi Azure Storage](#linked-azure-storage-account) poniżej.</span><span class="sxs-lookup"><span data-stu-id="952e0-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="952e0-187">Kliknij przycisk **Utwórz** toocreate hello konta.</span><span class="sxs-lookup"><span data-stu-id="952e0-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="952e0-188">Hello portal wskazuje, że wdrożenie jest w toku.</span><span class="sxs-lookup"><span data-stu-id="952e0-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="952e0-189">Po zakończeniu w obszarze **Powiadomienia** pojawia się powiadomienie **Wdrożenie zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="952e0-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="952e0-190">Wyświetlanie właściwości konta usługi Batch</span><span class="sxs-lookup"><span data-stu-id="952e0-190">View Batch account properties</span></span>
<span data-ttu-id="952e0-191">Po utworzeniu konta hello, możesz otworzyć hello **bloku konta usługi partia zadań** tooaccess jego ustawienia i właściwości.</span><span class="sxs-lookup"><span data-stu-id="952e0-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="952e0-192">Za pomocą menu po lewej stronie powitania w bloku konta usługi partia zadań hello są dostępne wszystkie ustawienia konta i właściwości.</span><span class="sxs-lookup"><span data-stu-id="952e0-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Blok konta usługi Batch w witrynie Azure Portal][account_blade]

* <span data-ttu-id="952e0-194">**Adres URL konta wsadowego**: podczas opracowywania aplikacji przy użyciu hello [API partii](batch-apis-tools.md#azure-accounts-for-batch-development), będziesz potrzebować tooaccess adres URL konta wsadowego zasobów.</span><span class="sxs-lookup"><span data-stu-id="952e0-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="952e0-195">Adres URL konta usługi partia zadań ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="952e0-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![Adres URL konta usługi Batch w portalu][account_url]

* <span data-ttu-id="952e0-197">**Klucze dostępu** (tryb usługi partii): tooauthenticate tooyour dostępu do konta usługi partia zadań z aplikacji, musisz mieć klucz dostępu konta.</span><span class="sxs-lookup"><span data-stu-id="952e0-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="952e0-198">(To ustawienie nie jest dostępne w trybie subskrypcji użytkownika, w którym używasz uwierzytelniania usługi Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="952e0-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="952e0-199">tooview lub regenerate kluczy dostępu do konta partii zadań, wprowadź `keys` w menu po lewej stronie powitania **wyszukiwania** w bloku konta usługi partia zadań hello, a następnie wybierz **klucze**.</span><span class="sxs-lookup"><span data-stu-id="952e0-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Klucze konta usługi Batch w witrynie Azure Portal][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="952e0-201">Połączone konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="952e0-201">Linked Azure Storage account</span></span>

<span data-ttu-id="952e0-202">Opcjonalnie możesz połączyć ogólnego przeznaczenia tooyour konta usługi Azure Storage konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="952e0-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="952e0-203">Witaj [pakietów aplikacji](batch-application-packages.md) funkcji partii używa magazynu obiektów Blob platformy Azure, podobnie jak hello [.NET konwencje pliku wsadowego](batch-task-output.md) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="952e0-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="952e0-204">Te funkcje opcjonalne ułatwiają wdrażanie aplikacji hello uruchamianych zadań wsadowych i trwałych danych hello, które oferują.</span><span class="sxs-lookup"><span data-stu-id="952e0-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="952e0-205">Zaleca się utworzenie nowego konta usługi Storage do wyłącznego użytku przez konto usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="952e0-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Tworzenie konta magazynu ogólnego przeznaczenia][storage_account]

> [!NOTE]
> <span data-ttu-id="952e0-207">Partia zadań Azure aktualnie obsługuje tylko hello ogólnego przeznaczenia typu konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="952e0-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="952e0-208">Ten typ konta opisano w kroku 5 [Tworzenie konta magazynu] (../storage/common/storage-create-storage-account.md#create-a-storage-account) w artykule [Informacje o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="952e0-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="952e0-209">Należy zachować ostrożność, gdy trwa ponowne generowanie kluczy dostępu hello połączonego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="952e0-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="952e0-210">Generuj tylko jeden klucz konta magazynu, a następnie kliknij przycisk **klucze synchronizacji** na powitania połączone bloku konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="952e0-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="952e0-211">Zaczekaj 5 minut tooallow hello klucze toopropagate toohello obliczeniowe węzłów w Twojej puli, a następnie ponownie wygenerować i zsynchronizować hello innego klucza, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="952e0-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="952e0-212">Jeśli ponownie wygenerować jednocześnie klawisze hello sam czas węzłów obliczeniowych nie będą mogli toosynchronize albo klucza i utracą konta magazynu toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="952e0-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="952e0-213">![Ponowne generowanie kluczy konta magazynu][4]</span><span class="sxs-lookup"><span data-stu-id="952e0-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="952e0-214">Limity przydziału i limity usługi Batch</span><span class="sxs-lookup"><span data-stu-id="952e0-214">Batch service quotas and limits</span></span>
<span data-ttu-id="952e0-215">Należy pamiętać, że jako z subskrypcją platformy Azure i Azure innych usług, niektóre [przydziały i limity](batch-quota-limit.md) zastosować tooBatch kont.</span><span class="sxs-lookup"><span data-stu-id="952e0-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="952e0-216">Bieżący przydziałów dla konta usługi partia zadań wyświetlane w portalu hello na koncie hello **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="952e0-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Limity przydziału konta usługi Batch w witrynie Azure Portal][quotas]



<span data-ttu-id="952e0-218">Ponadto wiele te przydziały można zwiększyć po prostu z żądania pomocy technicznej produktu wolnego przesłane w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="952e0-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="952e0-219">Zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md) szczegółowe informacje dotyczące żądania zwiększanie przydziału.</span><span class="sxs-lookup"><span data-stu-id="952e0-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="952e0-220">Inne opcje zarządzania kontem usługi Batch</span><span class="sxs-lookup"><span data-stu-id="952e0-220">Other Batch account management options</span></span>
<span data-ttu-id="952e0-221">Ponadto toousing hello portalu Azure, można również tworzyć i zarządzanie kontami partii hello następujący:</span><span class="sxs-lookup"><span data-stu-id="952e0-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="952e0-222">Polecenia cmdlet programu PowerShell usługi Batch</span><span class="sxs-lookup"><span data-stu-id="952e0-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="952e0-223">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="952e0-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="952e0-224">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="952e0-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="952e0-225">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="952e0-225">Next steps</span></span>
* <span data-ttu-id="952e0-226">Zobacz hello [Przegląd funkcji partii](batch-api-basics.md) toolearn więcej informacji na temat partii pojęcia dotyczące usługi i funkcje.</span><span class="sxs-lookup"><span data-stu-id="952e0-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="952e0-227">Hello artykule omówiono hello głównej partii zasobów takich jak pule, węzły obliczeniowe, zadań i zadań i zapoznać się z omówieniem hello funkcje usługi, które umożliwiają wykonanie obciążenie obliczeniowe na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="952e0-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="952e0-228">Dowiedz się podstawy hello opracowanie aplikacji z obsługą usługi partia zadań przy użyciu hello [biblioteki klienta .NET partii](batch-dotnet-get-started.md) lub [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="952e0-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="952e0-229">Te artykuły wprowadzające informacje pomocne przy działającą aplikację, która używa hello partii usługi tooexecute obciążenia na wielu węzłach obliczeniowych oraz oferuje, za pomocą usługi Azure Storage dla obciążenia pliku tymczasowego i pobierania.</span><span class="sxs-lookup"><span data-stu-id="952e0-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Ponowne generowanie kluczy konta magazynu"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
