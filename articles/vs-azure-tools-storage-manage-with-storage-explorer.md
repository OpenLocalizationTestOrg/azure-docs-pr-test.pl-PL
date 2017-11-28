---
title: Wprowadzenie do programu Storage Explorer (wersja zapoznawcza) | Microsoft Docs
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
ms.openlocfilehash: 1794a86a4185d587cf184a1f61a5720e2ab65e92
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="8fcb2-103">Wprowadzenie do programu Storage Explorer (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="8fcb2-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="8fcb2-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8fcb2-104">Overview</span></span>
<span data-ttu-id="8fcb2-105">Microsoft Azure Storage Explorer (wersja zapoznawcza) jest aplikacją autonomiczną, która umożliwia łatwą pracę z danymi w usłudze Azure Storage w systemach Windows, macOS i Linux.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="8fcb2-106">Ten artykuł zawiera informacje dotyczące różnych sposobów łączenia się z kontami magazynu Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span></span>

![Microsoft Azure Storage Explorer (wersja zapoznawcza)][15]

## <a name="prerequisites"></a><span data-ttu-id="8fcb2-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8fcb2-108">Prerequisites</span></span>
* [<span data-ttu-id="8fcb2-109">Pobieranie i instalowanie programu Storage Explorer (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="8fcb2-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a><span data-ttu-id="8fcb2-110">Łączenie się z usługą lub kontem magazynu</span><span class="sxs-lookup"><span data-stu-id="8fcb2-110">Connect to a storage account or service</span></span>
<span data-ttu-id="8fcb2-111">Program Storage Explorer (wersja zapoznawcza) oferuje kilka sposobów łączenia się z kontem magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-111">Storage Explorer (Preview) provides several ways to connect to storage accounts.</span></span> <span data-ttu-id="8fcb2-112">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="8fcb2-112">For example, you can:</span></span>
* <span data-ttu-id="8fcb2-113">Łączyć się z kontami magazynu skojarzonymi z subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-113">Connect to storage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="8fcb2-114">Łączyć się z usługami i kontami magazynu udostępnianymi z innych subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-114">Connect to storage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="8fcb2-115">Łączyć się z magazynem lokalnym i zarządzać nim przy użyciu emulatora usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-115">Connect to and manage local storage by using the Azure Storage Emulator.</span></span> 

<span data-ttu-id="8fcb2-116">Ponadto można pracować z kontami magazynu na globalnej i krajowej platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="8fcb2-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="8fcb2-117">[Łączenie się z subskrypcją platformy Azure](#connect-to-an-azure-subscription): zarządzanie zasobami magazynu należącymi do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-117">[Connect to an Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong to your Azure subscription.</span></span>
* <span data-ttu-id="8fcb2-118">[Praca z lokalnym magazynem programistycznym](#work-with-local-development-storage): zarządzanie magazynem lokalnym przy użyciu emulatora usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using the Azure Storage Emulator.</span></span>
* <span data-ttu-id="8fcb2-119">[Dołączanie do magazynu zewnętrznego](#attach-or-detach-an-external-storage-account): zarządzanie zasobami magazynu należącymi do innej subskrypcji platformy Azure lub w innych chmurach krajowej platformy Azure przy użyciu nazwy, klucza i punktów końcowych konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-119">[Attach to external storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="8fcb2-120">[Dołączanie konta magazynu przy użyciu sygnatury dostępu współdzielonego](#attach-storage-account-using-sas): zarządzanie zasobami magazynu należącymi do innej subskrypcji platformy Azure przy użyciu sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="8fcb2-121">[Dołączanie usługi przy użyciu sygnatury dostępu współdzielonego](#attach-service-using-sas): zarządzanie określoną usługą magazynu (kontenerem obiektów blob, kolejką lub tabelą) należącą do innej subskrypcji platformy Azure przy użyciu sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs to another Azure subscription by using an SAS.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="8fcb2-122">Łączenie się z subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8fcb2-122">Connect to an Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="8fcb2-123">Jeśli nie masz konta platformy Azure, możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8fcb2-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="8fcb2-124">W programie Storage Explorer (wersja zapoznawcza) wybierz pozycję **Ustawienia konta platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Ustawienia konta platformy Azure][0]

2. <span data-ttu-id="8fcb2-126">W lewym okienku są wyświetlane wszystkie konta Microsoft, na których się zalogowano.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-126">The left pane displays all the Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="8fcb2-127">Aby połączyć się z innym kontem, wybierz pozycję **Dodaj konto** i postępuj zgodnie z instrukcjami w celu zalogowania się przy użyciu konta Microsoft skojarzonego z co najmniej jedną aktywną subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-127">To connect to another account, select **Add an account**, and then follow the instructions to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8fcb2-128">Łączenie z krajową wersją platformy Azure (taką jak niemiecka wersja platformy Azure, chińska wersja platformy Azure i platforma Azure dla instytucji rządowych za pośrednictwem logowania) nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-128">Connecting to national Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="8fcb2-129">Zobacz sekcję „Dołączanie lub odłączanie konta magazynu zewnętrznego”, aby zapoznać się z opisem nawiązywania połączenia z kontami magazynu na krajowej platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-129">See the "Attach or detach an external storage account" section for how to connect to national Azure storage accounts.</span></span>

3. <span data-ttu-id="8fcb2-130">Po pomyślnym zalogowaniu się przy użyciu konta Microsoft w okienku po lewej stronie zostaną wyświetlone wszystkie subskrypcje platformy Azure skojarzone z tym kontem.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-130">After you successfully sign in with a Microsoft account, the left pane is populated with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="8fcb2-131">Wybierz subskrypcje platformy Azure, z którymi chcesz pracować, a następnie wybierz przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-131">Select the Azure subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="8fcb2-132">(Zaznaczenie pola **Wszystkie subskrypcje** powoduje przełączenie między wyświetlaniem wszystkich lub żadnej z wymienionych subskrypcji platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="8fcb2-132">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span></span>

    ![Wybieranie subskrypcji platformy Azure][3]  
    <span data-ttu-id="8fcb2-134">W okienku po lewej stronie są wyświetlane wszystkie konta magazynu skojarzone z wybranymi subskrypcjami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-134">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>

    ![Wybrane subskrypcje platformy Azure][4]

## <a name="connect-to-an-azure-stack-subscription"></a><span data-ttu-id="8fcb2-136">Łączenie z subskrypcją usługi Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8fcb2-136">Connect to an Azure Stack subscription</span></span>

<span data-ttu-id="8fcb2-137">Aby uzyskać informacje dotyczące łączenia z subskrypcją usługi Azure Stack, zobacz [Connect Storage Explorer to an Azure Stack subscription (Łączenie programu Storage Explorer z subskrypcją usługi Azure Stack)](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="8fcb2-137">For information about connecting to an Azure Stack subscription, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="8fcb2-138">Praca z lokalnym magazynem projektowym</span><span class="sxs-lookup"><span data-stu-id="8fcb2-138">Work with local development storage</span></span>
<span data-ttu-id="8fcb2-139">Program Storage Explorer (wersja zapoznawcza) pozwala pracować z magazynem lokalnym przy użyciu emulatora usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-139">With Storage Explorer (Preview), you can work against local storage by using the Azure Storage Emulator.</span></span> <span data-ttu-id="8fcb2-140">Takie podejście umożliwia pisanie kodu dla magazynu i testowanie go bez konieczności posiadania konta magazynu wdrożonego na platformie Azure, ponieważ konto magazynu jest emulowane przez emulator usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because the storage account is being emulated by the Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="8fcb2-141">Emulator usługi Azure Storage jest obecnie obsługiwany tylko dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-141">The Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="8fcb2-142">W lewym okienku programu Storage Explorer (wersja zapoznawcza) rozwiń węzeł **(Lokalne i dołączone)** > **Konta usługi Storage** > **(Projektowanie)**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-142">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Węzeł projektowania lokalnego][21]

2. <span data-ttu-id="8fcb2-144">Jeśli emulator usługi Azure Storage nie został jeszcze zainstalowany, na pasku informacyjnym zostanie wyświetlony monit o jego zainstalowanie.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-144">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span></span> <span data-ttu-id="8fcb2-145">Po wyświetleniu paska informacyjnego wybierz polecenie **Pobierz najnowszą wersję** i zainstaluj emulator.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-145">If the infobar is displayed, select **Download the latest version**, and then install the emulator.</span></span>

    ![Monit o pobranie emulatora usługi Azure Storage][22]

3. <span data-ttu-id="8fcb2-147">Po zainstalowaniu emulatora będziesz mieć możliwość tworzenia lokalnych obiektów blob, kolejek i tabel oraz pracy z nimi.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-147">After the emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="8fcb2-148">Aby dowiedzieć się, w jaki sposób pracować z poszczególnymi typami kont magazynu, zobacz jeden z poniższych artykułów:</span><span class="sxs-lookup"><span data-stu-id="8fcb2-148">To learn how to work with each storage account type, see one of the following:</span></span>

    * [<span data-ttu-id="8fcb2-149">Zarządzanie zasobami usługi Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="8fcb2-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="8fcb2-150">Zarządzanie zasobami magazynu udziału plików platformy Azure: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="8fcb2-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="8fcb2-151">Zarządzanie zasobami usługi Azure Queue Storage: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="8fcb2-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="8fcb2-152">Zarządzanie zasobami usługi Azure Table Storage: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="8fcb2-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="8fcb2-153">Dołączanie lub odłączanie konta magazynu zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="8fcb2-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="8fcb2-154">Program Storage Explorer (wersja zapoznawcza) umożliwia dołączanie kont magazynu zewnętrznego, dzięki czemu można łatwo udostępniać konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-154">With Storage Explorer (Preview), you can attach to external storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="8fcb2-155">W tej sekcji opisano sposób dołączania (i odłączania) kont magazynu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-155">This section explains how to attach to (and detach from) external storage accounts.</span></span>

### <a name="get-the-storage-account-credentials"></a><span data-ttu-id="8fcb2-156">Uzyskiwanie poświadczeń konta magazynu</span><span class="sxs-lookup"><span data-stu-id="8fcb2-156">Get the storage account credentials</span></span>
<span data-ttu-id="8fcb2-157">Aby udostępnić konto magazynu zewnętrznego, właściciel tego konta musi najpierw uzyskać poświadczenia (nazwę konta i klucz) dla konta, a następnie udostępnić te informacje osobie, która chce dołączyć do tego (zewnętrznego) konta.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-157">To share an external storage account, the owner of that account must first get the credentials (account name and key) for the account and then share that information with the person who wants to attach to that (external) account.</span></span> <span data-ttu-id="8fcb2-158">Poświadczenia konta magazynu można uzyskać za pośrednictwem witryny Azure Portal, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8fcb2-158">You can obtain the storage account credentials via the Azure portal by doing the following:</span></span>

1. <span data-ttu-id="8fcb2-159">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fcb2-159">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8fcb2-160">Wybierz pozycję **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-160">Select **Browse**.</span></span>

3. <span data-ttu-id="8fcb2-161">Wybierz pozycję **Konta usługi Storage**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="8fcb2-162">W bloku **Konta usługi Storage** wybierz odpowiednie konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-162">On the **Storage Accounts** blade, select the desired storage account.</span></span>

5. <span data-ttu-id="8fcb2-163">W bloku **Ustawienia** dla wybranego konta magazynu wybierz pozycję **Klucze dostępu**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-163">On the **Settings** blade for the selected storage account, select **Access keys**.</span></span>

    ![Opcja Klucze dostępu][5]

6. <span data-ttu-id="8fcb2-165">W bloku **Klucze dostępu** skopiuj wartość **Nazwa konta usługi Storage** i **klucz 1**, aby użyć ich podczas dołączania do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-165">On the **Access keys** blade, copy the **Storage account name** and **key1** values for use when attaching to the storage account.</span></span>

    ![Klawisze dostępu][6]

### <a name="attach-to-an-external-storage-account"></a><span data-ttu-id="8fcb2-167">Dołączanie konta magazynu zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="8fcb2-167">Attach to an external storage account</span></span>
<span data-ttu-id="8fcb2-168">Aby dołączyć konto magazynu zewnętrznego, potrzebna jest nazwa konta i klucz.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-168">To attach to an external storage account, you need the account's name and key.</span></span> <span data-ttu-id="8fcb2-169">W sekcji „Uzyskiwanie poświadczeń konta magazynu” wyjaśniono sposób uzyskiwania tych wartości z witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-169">The "Get the storage account credentials" section explains how to obtain these values from the Azure portal.</span></span> <span data-ttu-id="8fcb2-170">Należy pamiętać, że w witrynie Azure Portal klucz konta ma nazwę **klucz 1**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-170">However, in the portal, the account key is called **key1**.</span></span> <span data-ttu-id="8fcb2-171">Dlatego w przypadku, gdy program Storage Explorer (wersja zapoznawcza) wymaga podania klucza konta, należy wprowadzić wartość **klucz 1**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-171">So where Storage Explorer (Preview) asks for an account key, you enter the **key1** value.</span></span>

1. <span data-ttu-id="8fcb2-172">W programie Storage Explorer (wersja zapoznawcza) wybierz pozycję **Połącz z usługą Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-172">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opcja Połącz z usługą Azure Storage][23]

2. <span data-ttu-id="8fcb2-174">W oknie dialogowym **Łączenie z usługą Azure Storage** określ klucz konta (wartość **klucz 1** z witryny Azure Portal), a następnie wybierz przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-174">In the **Connect to Azure Storage** dialog box, specify the account key (the **key1** value from the Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8fcb2-175">Możesz wprowadzić parametry połączenia z usługą Storage z poziomu konta magazynu na krajowej platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-175">You can enter the storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="8fcb2-176">Na przykład aby połączyć się z kontami magazynu niemieckiej wersji platformy Azure, należy wprowadzić parametry połączenia podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="8fcb2-176">For example, to connect to Azure Germany storage accounts, enter connection strings similar to the following:</span></span> 
    >
    >* <span data-ttu-id="8fcb2-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="8fcb2-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="8fcb2-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="8fcb2-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="8fcb2-179">AccountKey=<klucz_konta_magazynu></span><span class="sxs-lookup"><span data-stu-id="8fcb2-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="8fcb2-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="8fcb2-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="8fcb2-181">Parametry połączenia można uzyskać z witryny Azure Portal w taki sam sposób, jak opisany w sekcji „Uzyskiwanie poświadczeń konta magazynu”.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-181">You can get the connection string from the Azure portal in the same way as described in the "Get the storage account credentials" section.</span></span>

    ![Okno dialogowe Łączenie z usługą Azure Storage][24]

3. <span data-ttu-id="8fcb2-183">W oknie dialogowym **Dołączanie zewnętrznej usługi Storage** w polu **Nazwa konta** wprowadź nazwę konta magazynu, określ inne żądane ustawienia, a następnie wybierz przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-183">In the **Attach External Storage** dialog box, in the **Account name** box, enter the storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Okno dialogowe Dołączanie zewnętrznej usługi Storage][8]

4. <span data-ttu-id="8fcb2-185">Sprawdź informacje wyświetlone w oknie dialogowym **Podsumowanie połączenia**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-185">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="8fcb2-186">Aby wprowadzić zmiany, wybierz przycisk **Wstecz** i ponownie wprowadź odpowiednie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-186">If you want to change anything, select **Back** and reenter the desired settings.</span></span> 

5. <span data-ttu-id="8fcb2-187">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-187">Select **Connect**.</span></span>

6. <span data-ttu-id="8fcb2-188">Po pomyślnym nawiązaniu połączenia konto magazynu zewnętrznego będzie wyświetlane z tekstem **(Zewnętrzne)** dodanym na końcu nazwy konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-188">After it is successfully connected, the external storage account is displayed with **(External)** appended to the storage account name.</span></span>

    ![Wynik połączenia z kontem magazynu zewnętrznego][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="8fcb2-190">Odłączanie konta magazynu zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="8fcb2-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="8fcb2-191">Kliknij prawym przyciskiem myszy konto magazynu zewnętrznego, które chcesz odłączyć, a następnie wybierz polecenie **Odłącz**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-191">Right-click the external storage account that you want to detach, and then select **Detach**.</span></span>

    ![Opcja odłączenia magazynu][10]

2. <span data-ttu-id="8fcb2-193">W oknie komunikatu z potwierdzeniem wybierz przycisk **Tak**, aby potwierdzić odłączenie konta magazynu zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-193">In the confirmation message, select **Yes** to confirm the detachment from the external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="8fcb2-194">Dołączanie konta magazynu przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="8fcb2-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="8fcb2-195">[Sygnatura dostępu współdzielonego](storage/common/storage-dotnet-shared-access-signature-part-1.md) zapewnia administratorowi subskrypcji platformy Azure możliwość tymczasowego przyznania dostępu do konta magazynu bez konieczności podawania poświadczeń subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets the admin of an Azure subscription grant temporary access to a storage account without having to provide Azure subscription credentials.</span></span>

<span data-ttu-id="8fcb2-196">Aby zilustrować ten scenariusz, załóżmy, że Użytkownik_A jest administratorem subskrypcji platformy Azure i Użytkownik_A chce zezwolić Użytkownikowi_B na dostęp do konta magazynu przez ograniczony czas z określonymi uprawnieniami:</span><span class="sxs-lookup"><span data-stu-id="8fcb2-196">To illustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="8fcb2-197">Użytkownik_A generuje sygnaturę dostępu współdzielonego (składającą się z parametrów połączenia dla konta magazynu) dla określonego przedziału czasu i z odpowiednimi uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-197">UserA generates an SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span></span>

2. <span data-ttu-id="8fcb2-198">Użytkownik_A udostępnia sygnaturę dostępu współdzielonego osobie, która chce uzyskać dostęp do konta magazynu — w naszym przykładzie jest to Użytkownik_B.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-198">UserA shares the SAS with the person (UserB, in our example) who wants access to the storage account.</span></span>  

3. <span data-ttu-id="8fcb2-199">Użytkownik_B korzysta z programu Storage Explorer (wersja zapoznawcza), aby dołączyć do konta należącego do Użytkownika_A przy użyciu dostarczonej sygnatury dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-199">UserB uses Storage Explorer (Preview) to attach to the account that belongs to UserA by using the supplied SAS.</span></span>

### <a name="get-an-sas-for-the-account-you-want-to-share"></a><span data-ttu-id="8fcb2-200">Uzyskiwanie sygnatury dostępu współdzielonego dla konta, które chcesz udostępnić</span><span class="sxs-lookup"><span data-stu-id="8fcb2-200">Get an SAS for the account you want to share</span></span>
1. <span data-ttu-id="8fcb2-201">W programie Storage Explorer (wersja zapoznawcza) kliknij prawym przyciskiem myszy konto magazynu, które chcesz udostępnić, a następnie wybierz polecenie **Uzyskaj sygnaturę dostępu współdzielonego**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-201">In Storage Explorer (Preview), right-click the storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Opcja menu kontekstowego Uzyskaj sygnaturę dostępu współdzielonego][13]

2. <span data-ttu-id="8fcb2-203">W oknie dialogowym **Sygnatura dostępu współdzielonego** określ przedział czasu i uprawnienia dla konta, a następnie wybierz przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-203">In the **Shared Access Signature** dialog box, specify the time frame and permissions that you want for the account, and then select **Create**.</span></span>

    <span data-ttu-id="8fcb2-204">![Okno dialogowe uzyskiwania sygnatury dostępu współdzielonego][14]</span><span class="sxs-lookup"><span data-stu-id="8fcb2-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="8fcb2-205">Zostanie otwarte okno dialogowe **Sygnatura dostępu współdzielonego** z wyświetloną sygnaturą dostępu współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-205">The **Shared Access Signature** dialog box opens and displays the SAS.</span></span>

3. <span data-ttu-id="8fcb2-206">Obok pola **Parametry połączenia** wybierz przycisk **Kopiuj**, aby skopiować go do schowka, a następnie wybierz polecenie **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-206">Next to the **Connection String**, select **Copy** to copy it to the clipboard, and then select **Close**.</span></span>

### <a name="attach-to-the-shared-account-by-using-the-sas"></a><span data-ttu-id="8fcb2-207">Dołączanie do udostępnionego konta przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="8fcb2-207">Attach to the shared account by using the SAS</span></span>
1. <span data-ttu-id="8fcb2-208">W programie Storage Explorer (wersja zapoznawcza) wybierz pozycję **Połącz z usługą Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-208">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opcja Połącz z usługą Azure Storage][23]

2. <span data-ttu-id="8fcb2-210">W oknie dialogowym **Łączenie z usługą Azure Storage** określ parametry połączenia, a następnie wybierz przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-210">In the **Connect to Azure Storage** dialog box, specify the connection string, and then select **Next**.</span></span>

    ![Okno dialogowe Łączenie z usługą Azure Storage][24]

3. <span data-ttu-id="8fcb2-212">Sprawdź informacje wyświetlone w oknie dialogowym **Podsumowanie połączenia**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-212">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="8fcb2-213">Aby wprowadzić zmiany, wybierz przycisk **Wstecz**, a następnie wprowadź odpowiednie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-213">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="8fcb2-214">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-214">Select **Connect**.</span></span>

5. <span data-ttu-id="8fcb2-215">Po dołączeniu konto magazynu będzie wyświetlane z tekstem **(SAS)** dodanym na końcu podanej nazwy konta.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-215">After it is attached, the storage account is displayed with **(SAS)** appended to the account name that you supplied.</span></span>

    ![Wynik dołączania do konta przy użyciu sygnatury dostępu współdzielonego][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="8fcb2-217">Dołączanie usługi przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="8fcb2-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="8fcb2-218">W sekcji „Dołączanie konta magazynu przy użyciu sygnatury dostępu współdzielonego” omówiono sposób udzielania tymczasowego dostępu do konta magazynu przez administratora subskrypcji platformy Azure przez wygenerowanie i udostępnienie sygnatury dostępu współdzielonego dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-218">The "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access to a storage account by generating and sharing an SAS for the storage account.</span></span> <span data-ttu-id="8fcb2-219">Podobnie można wygenerować sygnaturę dostępu współdzielonego dla określonej usługi (kontenera obiektów blob, kolejki lub tabeli) w ramach konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-the-service-that-you-want-to-share"></a><span data-ttu-id="8fcb2-220">Generowanie sygnatury dostępu współdzielonego dla usługi, którą chcesz udostępnić</span><span class="sxs-lookup"><span data-stu-id="8fcb2-220">Generate an SAS for the service that you want to share</span></span>
<span data-ttu-id="8fcb2-221">W tym kontekście usługa może być kontenerem, kolejką lub tabelą obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="8fcb2-222">Aby wygenerować sygnaturę dostępu współdzielonego dla wymienionych usług, zobacz:</span><span class="sxs-lookup"><span data-stu-id="8fcb2-222">To generate the SAS for a listed service, see:</span></span>

* [<span data-ttu-id="8fcb2-223">Uzyskiwanie sygnatury dostępu współdzielonego dla kontenera obiektów blob</span><span class="sxs-lookup"><span data-stu-id="8fcb2-223">Get the SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="8fcb2-224">Uzyskiwanie sygnatury dostępu współdzielonego dla udziału plików: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="8fcb2-224">Get the SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="8fcb2-225">Uzyskiwanie sygnatury dostępu współdzielonego dla kolejki: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="8fcb2-225">Get the SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="8fcb2-226">Uzyskiwanie sygnatury dostępu współdzielonego dla tabeli: *dostępne wkrótce*</span><span class="sxs-lookup"><span data-stu-id="8fcb2-226">Get the SAS for a table: *Coming soon*</span></span>

### <a name="attach-to-the-shared-account-service-by-using-the-sas"></a><span data-ttu-id="8fcb2-227">Dołączanie do usługi udostępnionego konta przy użyciu sygnatury dostępu współdzielonego</span><span class="sxs-lookup"><span data-stu-id="8fcb2-227">Attach to the shared account service by using the SAS</span></span>
1. <span data-ttu-id="8fcb2-228">W programie Storage Explorer (wersja zapoznawcza) wybierz pozycję **Połącz z usługą Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-228">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opcja Połącz z usługą Azure Storage][23]

2. <span data-ttu-id="8fcb2-230">W oknie dialogowym **Łączenie z usługą Azure Storage** określ identyfikator URI sygnatury dostępu współdzielonego, a następnie wybierz przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-230">In the **Connect to Azure Storage** dialog box, specify the SAS URI, and then select **Next**.</span></span>

    ![Okno dialogowe Łączenie z usługą Azure Storage][24]

3. <span data-ttu-id="8fcb2-232">Sprawdź informacje wyświetlone w oknie dialogowym **Podsumowanie połączenia**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-232">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="8fcb2-233">Aby wprowadzić zmiany, wybierz przycisk **Wstecz**, a następnie wprowadź odpowiednie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-233">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="8fcb2-234">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-234">Select **Connect**.</span></span>

5. <span data-ttu-id="8fcb2-235">Po dołączeniu nowo dołączona usługa jest wyświetlana w węźle **(Sygnatura dostępu współdzielonego usługi)**.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-235">After it is attached, the newly attached service is displayed under the **(Service SAS)** node.</span></span>

    ![Wynik dołączenia do usługi udostępnionej przy użyciu sygnatury dostępu współdzielonego][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="8fcb2-237">Wyszukiwanie kont magazynu</span><span class="sxs-lookup"><span data-stu-id="8fcb2-237">Search for storage accounts</span></span>
<span data-ttu-id="8fcb2-238">Jeśli masz długą listę kont magazynu, możesz szybko odnaleźć określone konto magazynu przy użyciu pola wyszukiwania w górnej części okienka po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-238">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span></span>

<span data-ttu-id="8fcb2-239">Podczas pisania w polu wyszukiwania w okienku po lewej stronie są wyświetlane tylko konta magazynu pasujące do podanej wartości wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="8fcb2-239">As you type in the search box, the left pane displays the storage accounts that match the search value you've entered up to that point.</span></span> <span data-ttu-id="8fcb2-240">Na poniższym zrzucie ekranu przedstawiono przykład, gdzie wyszukano wszystkie konta magazynu, których nazwa zawiera tekst **tarcher**:</span><span class="sxs-lookup"><span data-stu-id="8fcb2-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in the following screenshot:</span></span>

![Wyszukiwanie kont magazynu][11]

## <a name="next-steps"></a><span data-ttu-id="8fcb2-242">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8fcb2-242">Next steps</span></span>
* [<span data-ttu-id="8fcb2-243">Zarządzanie zasobami usługi Azure Blob Storage przy użyciu programu Storage Explorer (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="8fcb2-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

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
