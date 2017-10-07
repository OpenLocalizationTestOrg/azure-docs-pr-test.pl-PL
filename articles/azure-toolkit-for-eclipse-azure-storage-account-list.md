---
title: aaaAzure lista kont magazynu
description: "Zarządzanie ustawieniami konta magazynu przy użyciu hello Azure zestawu narzędzi dla programu Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="09d23-103">Lista kont magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="09d23-103">Azure Storage Account List</span></span>
<span data-ttu-id="09d23-104">Włącz konta magazynu platformy Azure Pobierz toobe lokalizacje używane dla JDK, serwera aplikacji i składników dowolnego, a także na potrzeby przechowywania stanu, korzystając z buforowania.</span><span class="sxs-lookup"><span data-stu-id="09d23-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="09d23-105">Eclipse przechowuje listę kont magazynu znane, projekty tooyour dostępne w obszarze roboczym Eclipse.</span><span class="sxs-lookup"><span data-stu-id="09d23-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="09d23-106">Witaj tooopen **kont magazynu** okno dialogowe, które jest używane toomanage, który listy w programie Eclipse kliknij **okna**, kliknij przycisk **preferencje**, rozwiń węzeł **Azure **, a następnie kliknij przycisk **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="09d23-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="09d23-107">Witaj poniżej pokazano hello **kont magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09d23-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="09d23-108">Można również otworzyć to okno dialogowe z **kont** łącza w oknach dialogowych, korzystających z konta magazynu, takich jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="09d23-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="09d23-109">Witaj **JDK** kartę hello **konfiguracji serwera** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09d23-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="09d23-110">Witaj **serwera** kartę hello **konfiguracji serwera** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09d23-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="09d23-111">Witaj **Dodaj składnik** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09d23-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="09d23-112">Witaj **buforowanie** okna dialogowego właściwości.</span><span class="sxs-lookup"><span data-stu-id="09d23-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="09d23-113">Magazyn kont przy użyciu narzędzia tooimport plik ustawień publikowania</span><span class="sxs-lookup"><span data-stu-id="09d23-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="09d23-114">W ramach hello **kont magazynu** okna dialogowego, kliknij przycisk **Import z pliku ustawień publikowania**.</span><span class="sxs-lookup"><span data-stu-id="09d23-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="09d23-115">(Pomiń ten krok, jeśli został już zapisany publikowania ustawienia pliku tooyour komputer lokalny). W hello **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Pobierz plik ustawień publikowania**.</span><span class="sxs-lookup"><span data-stu-id="09d23-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="09d23-116">Jeśli użytkownik nie jest jeszcze zalogowany do konta platformy Azure, będzie zostanie wyświetlony monit o toolog w.</span><span class="sxs-lookup"><span data-stu-id="09d23-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="09d23-117">Następnie zostanie wyświetlony monit pliku ustawień publikowania toosave platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="09d23-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="09d23-118">(Możesz zignorować hello instrukcje wynikowy wyświetlane na stronach logowania hello - one są dostarczane przez hello portalu Azure i są przeznaczone dla użytkowników programu Visual Studio) Zapisz tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="09d23-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="09d23-119">Nadal w hello **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk hello **Przeglądaj** przycisku, wybierz hello lokalnie zapisany wcześniej plik ustawień publikowania, a następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="09d23-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="09d23-120">Kliknij przycisk **OK** tooclose hello **importu informacji o subskrypcji** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09d23-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="09d23-121">toocreate nowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="09d23-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="09d23-122">W ramach hello **kont magazynu** okna dialogowego, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="09d23-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="09d23-123">W ramach hello **Dodawanie konta magazynu** okna dialogowego, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="09d23-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="09d23-124">W ramach hello **nowe konto magazynu** okna dialogowego, określ wartości dla następujących hello:</span><span class="sxs-lookup"><span data-stu-id="09d23-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="09d23-125">Nazwa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="09d23-125">Storage account name.</span></span>

   * <span data-ttu-id="09d23-126">Lokalizacja konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="09d23-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="09d23-127">Opis hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="09d23-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="09d23-128">Konto magazynu hello Hello subskrypcji toowhich należy.</span><span class="sxs-lookup"><span data-stu-id="09d23-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="09d23-129">Kliknij przycisk **OK** tooclose hello **nowe konto magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09d23-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="09d23-130">Może upłynąć kilka minut dla Twojego toobe konta magazynu utworzone.</span><span class="sxs-lookup"><span data-stu-id="09d23-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="09d23-131">Po utworzeniu, kliknij przycisk **OK** tooclose hello **Dodawanie konta magazynu** okno dialogowe i nowe konto magazynu zostanie dodany toohello listę kont magazynu dostępne.</span><span class="sxs-lookup"><span data-stu-id="09d23-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="09d23-132">tooadd istniejącej listy toohello konta magazynu</span><span class="sxs-lookup"><span data-stu-id="09d23-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="09d23-133">Jeśli nie masz już usługi Azure storage account, utwórz ją za następujące kroki hello liście hello **toocreate nowej sekcji konta magazynu** powyżej.</span><span class="sxs-lookup"><span data-stu-id="09d23-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="09d23-134">(Można również utworzyć nowe konto magazynu na powitania [portalu zarządzania Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="09d23-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="09d23-135">W ramach hello **kont magazynu** okna dialogowego, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="09d23-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="09d23-136">W ramach hello **Dodawanie konta magazynu** okna dialogowego, wprowadź wartości w polach **nazwa** i **klucz dostępu**.</span><span class="sxs-lookup"><span data-stu-id="09d23-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="09d23-137">Witaj konta nazwy i klucza dostępu musi być dla istniejącego konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="09d23-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="09d23-138">Użyj hello **magazynu** sekcji hello [portalu zarządzania Azure] [ Azure Management Portal] tooview nazwy konta magazynu i klucze.</span><span class="sxs-lookup"><span data-stu-id="09d23-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="09d23-139">Twoje **Dodawanie konta magazynu** okno dialogowe będzie wyglądać podobnie następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="09d23-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="09d23-140">Kliknij przycisk **OK** tooclose hello **Dodawanie konta magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09d23-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="09d23-141">toomodify toouse konta magazynu klucza dostępu</span><span class="sxs-lookup"><span data-stu-id="09d23-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="09d23-142">W ramach hello **kont magazynu** okna dialogowego, kliknij konto magazynu hello mają tooedit, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="09d23-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="09d23-143">W ramach hello **Edytuj klucz dostępu do konta magazynu** okna dialogowego, zmodyfikuj hello **klucz dostępu** wartość.</span><span class="sxs-lookup"><span data-stu-id="09d23-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="09d23-144">Kliknij przycisk **OK** tooclose hello **Edytuj klucz dostępu do konta magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09d23-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="09d23-145">tooremove konto magazynu z listy hello w środowisku Eclipse</span><span class="sxs-lookup"><span data-stu-id="09d23-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="09d23-146">W ramach hello **kont magazynu** okna dialogowego, kliknij konto magazynu hello mają tooedit, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="09d23-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="09d23-147">Kliknij przycisk **OK** gdy zostanie wyświetlony monit o tooremove hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="09d23-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="09d23-148">Usuwanie konta magazynu hello za pośrednictwem hello **kont magazynu** okna dialogowego tylko spowoduje usunięcie jej z listy hello możliwych do wyświetlenia w programie Eclipse kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="09d23-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="09d23-149">Nie powoduje usunięcia konta magazynu hello z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="09d23-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="09d23-150">Ponadto hello konta magazynu można ponownie wyświetlone na liście po Eclipse ładuje hello Szczegóły subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="09d23-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="09d23-151">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="09d23-151">See Also</span></span>
<span data-ttu-id="09d23-152">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="09d23-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="09d23-153">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="09d23-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="09d23-154">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="09d23-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="09d23-155">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="09d23-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
