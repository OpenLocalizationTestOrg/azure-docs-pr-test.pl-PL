---
title: Lista kont magazynu Azure
description: "Zarządzanie ustawieniami konta magazynu przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse"
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
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="08ea1-103">Lista kont magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="08ea1-103">Azure Storage Account List</span></span>
<span data-ttu-id="08ea1-104">Konta magazynu platformy Azure umożliwiają lokalizacji pobierania do użycia dla JDK, serwera aplikacji i składników dowolnego, a także na potrzeby przechowywania stanu, korzystając z buforowania.</span><span class="sxs-lookup"><span data-stu-id="08ea1-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="08ea1-105">Eclipse przechowuje listę kont magazynu znane, które są dostępne dla projektów w obszarze roboczym Eclipse.</span><span class="sxs-lookup"><span data-stu-id="08ea1-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="08ea1-106">Aby otworzyć **kont magazynu** okno dialogowe, które jest używane do zarządzania tym listy w programie Eclipse kliknij **okna**, kliknij przycisk **preferencje**, rozwiń węzeł **Azure**, a następnie kliknij przycisk **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="08ea1-107">Poniżej przedstawiono **kont magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="08ea1-108">Można również otworzyć to okno dialogowe z **kont** łącza w oknach dialogowych, korzystających z konta magazynu, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="08ea1-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="08ea1-109">**JDK** karcie **konfiguracji serwera** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="08ea1-110">**Serwera** karcie **konfiguracji serwera** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="08ea1-111">**Dodaj składnik** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="08ea1-112">**Buforowanie** okna dialogowego właściwości.</span><span class="sxs-lookup"><span data-stu-id="08ea1-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="08ea1-113">Aby zaimportować kont magazynu używany plik ustawień publikowania</span><span class="sxs-lookup"><span data-stu-id="08ea1-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="08ea1-114">W ramach **kont magazynu** okna dialogowego, kliknij przycisk **Import z pliku ustawień publikowania**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="08ea1-115">(Pomiń ten krok, jeśli został już zapisany plik ustawień publikowania na komputer lokalny). W **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Pobierz plik ustawień publikowania**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="08ea1-116">Jeśli użytkownik nie jest jeszcze zalogowany do konta platformy Azure, pojawi się zalogować.</span><span class="sxs-lookup"><span data-stu-id="08ea1-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="08ea1-117">Następnie zostanie wyświetlony monit, aby zapisać Azure pliku ustawień publikowania.</span><span class="sxs-lookup"><span data-stu-id="08ea1-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="08ea1-118">(Możesz zignorować wynikowy instrukcje wyświetlane na stronach logowania — one znajdują się w portalu Azure i są przeznaczone dla użytkowników programu Visual Studio) Zapisz go na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="08ea1-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="08ea1-119">Nadal **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Przeglądaj** przycisku, wybierz plik ustawień publikowania, który został wcześniej zapisany w lokalnie, a następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="08ea1-120">Kliknij przycisk **OK** zamknąć **importu informacji o subskrypcji** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="08ea1-121">Aby utworzyć nowe konto magazynu</span><span class="sxs-lookup"><span data-stu-id="08ea1-121">To create a new storage account</span></span>
1. <span data-ttu-id="08ea1-122">W ramach **kont magazynu** okna dialogowego, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="08ea1-123">W ramach **Dodawanie konta magazynu** okna dialogowego, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="08ea1-124">W ramach **nowe konto magazynu** okna dialogowego, określ wartości dla następujących:</span><span class="sxs-lookup"><span data-stu-id="08ea1-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="08ea1-125">Nazwa konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="08ea1-125">Storage account name.</span></span>

   * <span data-ttu-id="08ea1-126">Lokalizacja konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="08ea1-126">Location of the storage account.</span></span>

   * <span data-ttu-id="08ea1-127">Opis konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="08ea1-127">Description of the storage account.</span></span>

   * <span data-ttu-id="08ea1-128">Subskrypcja, do której należy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="08ea1-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="08ea1-129">Kliknij przycisk **OK** zamknąć **nowe konto magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="08ea1-130">Może upłynąć kilka minut dla konta magazynu do utworzenia.</span><span class="sxs-lookup"><span data-stu-id="08ea1-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="08ea1-131">Po utworzeniu, kliknij przycisk **OK** zamknąć **Dodawanie konta magazynu** okno dialogowe i nowe konto magazynu zostanie dodany do listy kont dostępny magazyn.</span><span class="sxs-lookup"><span data-stu-id="08ea1-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="08ea1-132">Aby dodać istniejące konto magazynu do listy</span><span class="sxs-lookup"><span data-stu-id="08ea1-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="08ea1-133">Jeśli nie masz już konto magazynu Azure, utworzyć, wykonując czynności opisane w **do utworzenia nowej sekcji konta magazynu** powyżej.</span><span class="sxs-lookup"><span data-stu-id="08ea1-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="08ea1-134">(Można również utworzyć nowe konto magazynu w [portalu zarządzania Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="08ea1-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="08ea1-135">W ramach **kont magazynu** okna dialogowego, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="08ea1-136">W ramach **Dodawanie konta magazynu** okna dialogowego, wprowadź wartości w polach **nazwa** i **klucz dostępu**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="08ea1-137">Konto nazwy i klucza dostępu musi być dla istniejącego konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="08ea1-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="08ea1-138">Użyj **magazynu** sekcji [portalu zarządzania Azure] [ Azure Management Portal] wyświetlanie Twoich nazwy konta magazynu i klucze.</span><span class="sxs-lookup"><span data-stu-id="08ea1-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="08ea1-139">Twoje **Dodawanie konta magazynu** okno dialogowe będzie wyglądać podobnie do następującego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="08ea1-140">Kliknij przycisk **OK** zamknąć **Dodawanie konta magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="08ea1-141">Aby zmodyfikować konto magazynu, aby użyć klucza dostępu</span><span class="sxs-lookup"><span data-stu-id="08ea1-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="08ea1-142">W ramach **kont magazynu** okno dialogowe, kliknij przycisk Magazyn konta chcesz edytować, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="08ea1-143">W ramach **Edytuj klucz dostępu do konta magazynu** okna dialogowego, zmodyfikuj **klucz dostępu** wartość.</span><span class="sxs-lookup"><span data-stu-id="08ea1-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="08ea1-144">Kliknij przycisk **OK** zamknąć **Edytuj klucz dostępu do konta magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ea1-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="08ea1-145">Aby usunąć konto magazynu z listy w programie Eclipse</span><span class="sxs-lookup"><span data-stu-id="08ea1-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="08ea1-146">W ramach **kont magazynu** okno dialogowe, kliknij przycisk Magazyn konta chcesz edytować, a następnie kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="08ea1-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="08ea1-147">Kliknij przycisk **OK** po wyświetleniu monitu, aby usunąć konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="08ea1-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="08ea1-148">Usuwanie konta magazynu za pośrednictwem **kont magazynu** okna dialogowego tylko usunięcie go z listy kont magazynu, widocznego w środowisku Eclipse.</span><span class="sxs-lookup"><span data-stu-id="08ea1-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="08ea1-149">Nie powoduje usunięcia konta magazynu z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="08ea1-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="08ea1-150">Ponadto konto magazynu może ponownie wyświetlone na liście po Eclipse ponowne ładowanie szczegółów subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="08ea1-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="08ea1-151">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="08ea1-151">See Also</span></span>
<span data-ttu-id="08ea1-152">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="08ea1-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="08ea1-153">[Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="08ea1-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="08ea1-154">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="08ea1-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="08ea1-155">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="08ea1-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
