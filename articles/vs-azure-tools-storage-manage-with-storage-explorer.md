---
title: "aaaGet wprowadzenie do Eksploratora usługi Storage (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Zarządzanie zasobami usługi Azure Storage za pomocą programu Storage Explorer (wersja zapoznawcza)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="d4a60-103">Wprowadzenie do programu Storage Explorer (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d4a60-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="d4a60-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d4a60-104">Overview</span></span>
<span data-ttu-id="d4a60-105">Eksplorator usługi Azure Storage (wersja zapoznawcza) jest aplikacją autonomiczną, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="d4a60-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="d4a60-106">W tym artykule dowiesz się hello różnych sposobów łączenia tooand Zarządzanie kontami magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Microsoft Azure Storage Explorer (wersja zapoznawcza)][15]

## <a name="prerequisites"></a><span data-ttu-id="d4a60-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d4a60-108">Prerequisites</span></span>
* [<span data-ttu-id="d4a60-109">Pobieranie i instalowanie programu Storage Explorer (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d4a60-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="d4a60-110">Połącz z usługą lub kontem magazynu tooa</span><span class="sxs-lookup"><span data-stu-id="d4a60-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="d4a60-111">Eksplorator usługi Storage (wersja zapoznawcza) oferuje kilka możliwości tooconnect toostorage kont.</span><span class="sxs-lookup"><span data-stu-id="d4a60-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="d4a60-112">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="d4a60-112">For example, you can:</span></span>
* <span data-ttu-id="d4a60-113">Łączenie kont toostorage skojarzonych z subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="d4a60-114">Podłącz toostorage konta i usługi, które są udostępniane z innych subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="d4a60-115">Połącz tooand Zarządzanie magazynem lokalnym przy użyciu hello emulatora magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="d4a60-116">Ponadto można pracować z kontami magazynu na globalnej i krajowej platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="d4a60-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="d4a60-117">[Połącz tooan subskrypcji platformy Azure](#connect-to-an-azure-subscription): Zarządzanie zasobami magazynu, które należą tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="d4a60-118">[Praca z magazynu lokalnego programowanie](#work-with-local-development-storage): Zarządzanie magazynem lokalnym przy użyciu hello emulatora magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="d4a60-119">[Dołącz magazynu tooexternal](#attach-or-detach-an-external-storage-account): Zarządzanie zasobami magazynu, które należą tooanother subskrypcji platformy Azure lub które są w obszarze national chmury Azure przy użyciu nazwy konta magazynu hello, klucz i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d4a60-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="d4a60-120">[Dołączanie konta magazynu przy użyciu sygnatury dostępu Współdzielonego](#attach-storage-account-using-sas): Zarządzanie zasobami magazynu, które należą tooanother subskrypcji platformy Azure przy użyciu sygnatury dostępu współdzielonego (SAS).</span><span class="sxs-lookup"><span data-stu-id="d4a60-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="d4a60-121">[Dołączanie usługi przy użyciu sygnatury dostępu Współdzielonego](#attach-service-using-sas): Zarządzanie określoną usługą magazynu (kontenera obiektów blob, kolejki lub tabeli) należącą tooanother subskrypcji platformy Azure przy użyciu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="d4a60-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="d4a60-122">Połącz tooan subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d4a60-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="d4a60-123">Jeśli nie masz konta platformy Azure, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d4a60-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="d4a60-124">W programie Storage Explorer (wersja zapoznawcza) wybierz pozycję **Ustawienia konta platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Ustawienia konta platformy Azure][0]

2. <span data-ttu-id="d4a60-126">w okienku po lewej stronie powitania Wyświetla wszystkie konta Microsoft hello, który użytkownik został zarejestrowany w usłudze.</span><span class="sxs-lookup"><span data-stu-id="d4a60-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="d4a60-127">Konto tooanother tooconnect, wybierz opcję **Dodaj konto**, a następnie wykonaj toosign instrukcje hello za pomocą konta Microsoft, który jest skojarzony z co najmniej jedną aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="d4a60-128">Łączenie toonational Azure (na przykład platformy Azure w Niemczech, Azure dla instytucji rządowych i Chińskiej wersji platformy Azure za pomocą logowania) nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="d4a60-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="d4a60-129">Zobacz hello "Dołączanie lub odłączanie konta magazynu zewnętrznego" sekcji opisano sposób kontami magazynu Azure toonational tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d4a60-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="d4a60-130">Po pomyślnym zalogowaniu się przy użyciu konta Microsoft, lewo hello okienko jest wypełniana hello subskrypcji platformy Azure skojarzonych z tym kontem.</span><span class="sxs-lookup"><span data-stu-id="d4a60-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="d4a60-131">Wybierz hello subskrypcji platformy Azure, które mają toowork z, a następnie wybierz **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="d4a60-132">(Wybieranie **wszystkie subskrypcje** przełącza wyświetlaniem wszystkich lub żadnej hello wymienionych subskrypcji platformy Azure.)</span><span class="sxs-lookup"><span data-stu-id="d4a60-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![Wybieranie subskrypcji platformy Azure][3]  
    <span data-ttu-id="d4a60-134">w okienku po lewej stronie powitania Wyświetla hello konta magazynu skojarzone z hello wybrane subskrypcje platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![Wybrane subskrypcje platformy Azure][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="d4a60-136">Połączyć subskrypcję Azure stosu tooan</span><span class="sxs-lookup"><span data-stu-id="d4a60-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="d4a60-137">Uzyskać informacje dotyczące łączenia subskrypcji Azure stosu tooan, zobacz [tooan połączenia Eksploratora usługi Storage subskrypcji Azure stosu](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="d4a60-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="d4a60-138">Praca z lokalnym magazynem projektowym</span><span class="sxs-lookup"><span data-stu-id="d4a60-138">Work with local development storage</span></span>
<span data-ttu-id="d4a60-139">Z Eksploratora usługi Storage (wersja zapoznawcza) można pracować z magazynu lokalnego przy użyciu hello emulatora magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="d4a60-140">To rozwiązanie umożliwia pisanie kodu oraz testów magazynu bez konieczności posiadania konta magazynu wdrożonego na platformie Azure, ponieważ hello konta magazynu jest emulowane przez Emulator usługi Azure Storage hello.</span><span class="sxs-lookup"><span data-stu-id="d4a60-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="d4a60-141">Witaj emulatora magazynu Azure jest obecnie obsługiwane tylko dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d4a60-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="d4a60-142">W okienku po lewej stronie powitania z Eksploratora usługi Storage (wersja zapoznawcza), rozwiń węzeł hello **(lokalny i dołączonego)** > **kont magazynu** > **(Programowanie)** węzła.</span><span class="sxs-lookup"><span data-stu-id="d4a60-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Węzeł projektowania lokalnego][21]

2. <span data-ttu-id="d4a60-144">Jeśli hello emulatora magazynu Azure nie został jeszcze zainstalowany, to zostanie wyświetlony monit o toodo tak za pośrednictwem paska informacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d4a60-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="d4a60-145">Jeśli zostanie wyświetlony pasek informacyjny hello, wybierz **pobierania hello najnowszej wersji**, a następnie zainstaluj hello emulator.</span><span class="sxs-lookup"><span data-stu-id="d4a60-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![Monit o pobranie emulatora usługi Azure Storage][22]

3. <span data-ttu-id="d4a60-147">Po zainstalowaniu emulatora hello można tworzyć i pracować z lokalnych obiektów blob, kolejek i tabel.</span><span class="sxs-lookup"><span data-stu-id="d4a60-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="d4a60-148">toolearn jak typ toowork z każdego konta magazynu, zobacz jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="d4a60-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="d4a60-149">Zarządzanie zasobami usługi Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="d4a60-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="d4a60-150">Zarządzanie zasobami magazynu udziału plików platformy Azure: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="d4a60-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="d4a60-151">Zarządzanie zasobami usługi Azure Queue Storage: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="d4a60-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="d4a60-152">Zarządzanie zasobami usługi Azure Table Storage: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="d4a60-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="d4a60-153">Dołączanie lub odłączanie konta magazynu zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="d4a60-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="d4a60-154">Z Eksploratora usługi Storage (wersja zapoznawcza) można dołączyć tooexternal kont magazynu, dzięki czemu można łatwo udostępniać konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d4a60-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="d4a60-155">W tej sekcji opisano sposób tooattach too(and detach from) kont magazynu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="d4a60-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="d4a60-156">Uzyskiwanie poświadczeń konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="d4a60-156">Get hello storage account credentials</span></span>
<span data-ttu-id="d4a60-157">tooshare konta magazynu zewnętrznego, hello właściciela tego konta musi najpierw uzyskać poświadczenia hello (nazwa konta i klucz) dla konta hello, a następnie udostępnić te informacje osobie hello, którzy chcą tooattach toothat (zewnętrznego) konta.</span><span class="sxs-lookup"><span data-stu-id="d4a60-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="d4a60-158">Można uzyskać poświadczeń konta magazynu hello za pośrednictwem portalu Azure hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="d4a60-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="d4a60-159">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d4a60-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d4a60-160">Wybierz pozycję **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-160">Select **Browse**.</span></span>

3. <span data-ttu-id="d4a60-161">Wybierz pozycję **Konta usługi Storage**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="d4a60-162">Na powitania **kont magazynu** bloku, wybierz hello żądanego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d4a60-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="d4a60-163">Na powitania **ustawienia** bloku hello wybranego konta magazynu, wybierz **klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![Opcja Klucze dostępu][5]

6. <span data-ttu-id="d4a60-165">Na powitania **klucze dostępu** bloku, hello kopiowania **nazwy konta magazynu** i **klucz1** wartości do użycia podczas dołączania konta magazynu toohello.</span><span class="sxs-lookup"><span data-stu-id="d4a60-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![Klawisze dostępu][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="d4a60-167">Dołączanie konta magazynu zewnętrznego tooan</span><span class="sxs-lookup"><span data-stu-id="d4a60-167">Attach tooan external storage account</span></span>
<span data-ttu-id="d4a60-168">konta magazynu zewnętrznego tooan tooattach, należy nazwę hello konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="d4a60-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="d4a60-169">sekcja "Poświadczeń konta magazynu hello Get" Hello wyjaśniono, jak te wartości z tooobtain hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="d4a60-170">Jednak w portalu hello klucz konta hello jest nazywany **klucz1**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="d4a60-171">Dlatego w przypadku, gdy Eksploratora usługi Storage (wersja zapoznawcza) wprowadza się klucza konta, możesz wprowadzić hello **klucz1** wartości.</span><span class="sxs-lookup"><span data-stu-id="d4a60-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="d4a60-172">W Eksploratorze usługi Storage (wersja zapoznawcza), wybierz **łączą magazyn tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opcja magazynu tooAzure połączenia][23]

2. <span data-ttu-id="d4a60-174">W hello **połączyć tooAzure magazynu** okna dialogowego należy określić klucz konta hello (hello **klucz1** wartość z zakresu od hello portalu Azure), a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4a60-175">Możesz wprowadzić parametry połączenia magazynu hello z konta magazynu Azure national.</span><span class="sxs-lookup"><span data-stu-id="d4a60-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="d4a60-176">Na przykład tooconnect tooAzure Niemcy kont magazynu, wprowadź następujące toohello podobne parametry połączenia:</span><span class="sxs-lookup"><span data-stu-id="d4a60-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="d4a60-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="d4a60-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="d4a60-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="d4a60-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="d4a60-179">AccountKey=<klucz_konta_magazynu></span><span class="sxs-lookup"><span data-stu-id="d4a60-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="d4a60-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="d4a60-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="d4a60-181">Można pobrać ciągu połączenia hello z hello Azure portalu w hello sam sposób, jak opisano w hello sekcji "Uzyskiwanie poświadczeń konta magazynu hello".</span><span class="sxs-lookup"><span data-stu-id="d4a60-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![Okno dialogowe magazynu tooAzure łączenie][24]

3. <span data-ttu-id="d4a60-183">W hello **Dołącz zewnętrzną usługę Storage** okno dialogowe, w hello **nazwa konta** , wprowadź nazwę konta magazynu hello, określ odpowiednie ustawienia, a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Okno dialogowe Dołączanie zewnętrznej usługi Storage][8]

4. <span data-ttu-id="d4a60-185">W hello **podsumowanie połączenia** okna dialogowego Sprawdź hello informacji.</span><span class="sxs-lookup"><span data-stu-id="d4a60-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="d4a60-186">Toochange cokolwiek, zaznacz **ponownie** i wprowadzić ustawienia hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d4a60-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="d4a60-187">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-187">Select **Connect**.</span></span>

6. <span data-ttu-id="d4a60-188">Po pomyślnym połączeniu konta magazynu zewnętrznego hello jest wyświetlana z **(zewnętrzne)** dołączana nazwa konta magazynu toohello.</span><span class="sxs-lookup"><span data-stu-id="d4a60-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![Wynik łączenia tooan konta magazynu zewnętrznego][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="d4a60-190">Odłączanie konta magazynu zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="d4a60-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="d4a60-191">Kliknij prawym przyciskiem myszy konto magazynu zewnętrznego hello mają toodetach, a następnie wybierz **Detach**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![Opcja odłączenia magazynu][10]

2. <span data-ttu-id="d4a60-193">Komunikat potwierdzający hello, wybierz **tak** tooconfirm hello odłączenie konta magazynu zewnętrznego hello.</span><span class="sxs-lookup"><span data-stu-id="d4a60-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="d4a60-194">Dołączanie konta magazynu przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="d4a60-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="d4a60-195">[SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) umożliwia Witaj, Administratorze subskrypcji platformy Azure przyznać konta magazynu tymczasowego dostępu tooa bez konieczności tooprovide poświadczenia subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a60-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="d4a60-196">tooillustrate w tym scenariuszu, załóżmy, że ten Użytkownik_a jest administratorem subskrypcji platformy Azure i Użytkownik_a chce tooaccess Użytkownik_b tooallow konta magazynu przez ograniczony czas z określonymi uprawnieniami:</span><span class="sxs-lookup"><span data-stu-id="d4a60-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="d4a60-197">Użytkownik_a generuje sygnatury dostępu Współdzielonego (składającą się z hello parametry połączenia dla konta magazynu hello) na określoną godzinę okresu i hello potrzebne uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d4a60-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="d4a60-198">Użytkownik_a udziałów hello sygnatury dostępu Współdzielonego osobie hello (w naszym przykładzie Użytkownik_b), którzy chcą konta magazynu toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="d4a60-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="d4a60-199">Użytkownik_b korzysta z konta toohello tooattach Eksploratora usługi Storage (wersja zapoznawcza), który należy tooUserA za pomocą hello dostarczony sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="d4a60-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="d4a60-200">Uzyskiwanie sygnatury dostępu Współdzielonego hello konta, które chcesz tooshare</span><span class="sxs-lookup"><span data-stu-id="d4a60-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="d4a60-201">W Eksploratorze usługi Storage (wersja zapoznawcza), kliknij prawym przyciskiem myszy konto magazynu hello chcesz udostępnić, a następnie wybierz **Uzyskaj sygnaturę dostępu współdzielonego**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Opcja menu kontekstowego Uzyskaj sygnaturę dostępu współdzielonego][13]

2. <span data-ttu-id="d4a60-203">W hello **sygnatura dostępu współdzielonego** oknie dialogowym Określ przedział czasu hello i uprawnienia, które hello konta, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="d4a60-204">![Okno dialogowe uzyskiwania sygnatury dostępu współdzielonego][14]</span><span class="sxs-lookup"><span data-stu-id="d4a60-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="d4a60-205">Witaj **sygnatura dostępu współdzielonego** otwiera okno dialogowe i wyświetla hello sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="d4a60-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="d4a60-206">Dalej toohello **ciąg połączenia**, wybierz pozycję **kopiowania** toocopy go Schowka toohello, a następnie wybierz **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="d4a60-207">Dołączanie toohello udostępnionego konta przy użyciu hello SAS</span><span class="sxs-lookup"><span data-stu-id="d4a60-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="d4a60-208">W Eksploratorze usługi Storage (wersja zapoznawcza), wybierz **łączą magazyn tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opcja magazynu tooAzure połączenia][23]

2. <span data-ttu-id="d4a60-210">W hello **połączyć tooAzure magazynu** okno dialogowe, określ ciąg połączenia hello, a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![Okno dialogowe magazynu tooAzure łączenie][24]

3. <span data-ttu-id="d4a60-212">W hello **podsumowanie połączenia** okna dialogowego Sprawdź hello informacji.</span><span class="sxs-lookup"><span data-stu-id="d4a60-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="d4a60-213">Wybierz zmiany toomake **ponownie**i wprowadź ustawienia hello.</span><span class="sxs-lookup"><span data-stu-id="d4a60-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="d4a60-214">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-214">Select **Connect**.</span></span>

5. <span data-ttu-id="d4a60-215">Po dołączeniu go hello konto magazynu zostanie wyświetlony z **(SAS)** dołączany toohello nazwę konta, który został dostarczony.</span><span class="sxs-lookup"><span data-stu-id="d4a60-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![Wynik konto podłączone tooan przy użyciu sygnatury dostępu Współdzielonego][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="d4a60-217">Dołączanie usługi przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="d4a60-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="d4a60-218">sekcja "Dołącz konto magazynu przy użyciu sygnatury dostępu Współdzielonego" Hello wyjaśniono, jak administrator subskrypcji Azure mogą udzielać dostępu konta magazynu tymczasowego dostępu tooa generowania i udostępniając sygnatury dostępu Współdzielonego dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="d4a60-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="d4a60-219">Podobnie można wygenerować sygnaturę dostępu współdzielonego dla określonej usługi (kontenera obiektów blob, kolejki lub tabeli) w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d4a60-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="d4a60-220">Generowanie sygnatury dostępu Współdzielonego dla usługi hello, które mają tooshare</span><span class="sxs-lookup"><span data-stu-id="d4a60-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="d4a60-221">W tym kontekście usługa może być kontenerem, kolejką lub tabelą obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="d4a60-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="d4a60-222">Witaj toogenerate sygnatury dostępu Współdzielonego dla wymienionych usług, zobacz:</span><span class="sxs-lookup"><span data-stu-id="d4a60-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="d4a60-223">Pobierz hello SAS dla kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="d4a60-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="d4a60-224">Pobierz hello sygnatury dostępu Współdzielonego dla udziału plików: *wkrótce*</span><span class="sxs-lookup"><span data-stu-id="d4a60-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="d4a60-225">Pobierz hello sygnatury dostępu Współdzielonego dla kolejki: *wkrótce*</span><span class="sxs-lookup"><span data-stu-id="d4a60-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="d4a60-226">Pobierz hello sygnatury dostępu Współdzielonego dla tabeli: *wkrótce*</span><span class="sxs-lookup"><span data-stu-id="d4a60-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="d4a60-227">Dołączanie usługi przy użyciu hello sygnatury dostępu Współdzielonego konta toohello udostępnionych</span><span class="sxs-lookup"><span data-stu-id="d4a60-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="d4a60-228">W Eksploratorze usługi Storage (wersja zapoznawcza), wybierz **łączą magazyn tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Opcja magazynu tooAzure połączenia][23]

2. <span data-ttu-id="d4a60-230">W hello **połączyć tooAzure magazynu** okno dialogowe, określ hello identyfikatora URI połączenia SAS, a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![Okno dialogowe magazynu tooAzure łączenie][24]

3. <span data-ttu-id="d4a60-232">W hello **podsumowanie połączenia** okna dialogowego Sprawdź hello informacji.</span><span class="sxs-lookup"><span data-stu-id="d4a60-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="d4a60-233">Wybierz zmiany toomake **ponownie**i wprowadź ustawienia hello.</span><span class="sxs-lookup"><span data-stu-id="d4a60-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="d4a60-234">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="d4a60-234">Select **Connect**.</span></span>

5. <span data-ttu-id="d4a60-235">Po dołączeniu go hello nowo dołączona usługa zostanie wyświetlona w obszarze hello **(usługa SAS)** węzła.</span><span class="sxs-lookup"><span data-stu-id="d4a60-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![Wynik dołączanie tooa udostępnione usługi przy użyciu sygnatury dostępu Współdzielonego][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="d4a60-237">Wyszukiwanie kont magazynu</span><span class="sxs-lookup"><span data-stu-id="d4a60-237">Search for storage accounts</span></span>
<span data-ttu-id="d4a60-238">Jeśli masz długą listę kont magazynu, szybko toolocate określone konto magazynu jest pole wyszukiwania hello toouse u góry hello hello w lewym okienku.</span><span class="sxs-lookup"><span data-stu-id="d4a60-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="d4a60-239">Podczas wpisywania w polu wyszukiwania hello hello lewe okienko wyświetla hello magazynu kont, które pasuje do wartości wyszukiwania hello wprowadzono toothat punktu.</span><span class="sxs-lookup"><span data-stu-id="d4a60-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="d4a60-240">Na przykład wyszukiwania dla wszystkie magazyny kont, których nazwa zawiera **tarcher** jest wyświetlany w obszarze powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="d4a60-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![Wyszukiwanie kont magazynu][11]

## <a name="next-steps"></a><span data-ttu-id="d4a60-242">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4a60-242">Next steps</span></span>
* [<span data-ttu-id="d4a60-243">Zarządzanie zasobami usługi Azure Blob Storage przy użyciu programu Storage Explorer (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d4a60-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
