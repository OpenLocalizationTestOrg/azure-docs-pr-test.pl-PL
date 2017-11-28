---
title: "Zarządzaj kontem bazy danych rozwiązania Cosmos Azure za pośrednictwem portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Zarządzanie kontem bazy danych Azure rozwiązania Cosmos w portalu Azure. Przewodnik na wyświetlanie, kopiowanie, usuwanie i dostęp do kont za pomocą portalu Azure."
keywords: Portal Azure documentdb, azure, platformy Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="7dd1a-105">Jak zarządzać konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="7dd1a-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="7dd1a-106">Dowiedz się, jak ustawić globalne spójności, pracy z kluczy oraz usunąć konto bazy danych Azure rozwiązania Cosmos w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="7dd1a-107"><a id="consistency"></a>Zarządzanie ustawieniami spójności bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="7dd1a-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="7dd1a-108">Wybranie poziomu spójności prawo zależy od semantykę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="7dd1a-109">Należy zapoznać się z poziomu spójności dostępne w usłudze Azure DB rozwiązania Cosmos odczytując [za pomocą poziomów spójności w celu zwiększenia dostępności i wydajności w usłudze Azure DB rozwiązania Cosmos][consistency].</span><span class="sxs-lookup"><span data-stu-id="7dd1a-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="7dd1a-110">Azure DB rozwiązania Cosmos zapewnia spójność, dostępności i wydajności gwarancji, na każdym poziomie spójności niedostępna dla Twojego konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="7dd1a-111">Konfigurowanie konta bazy danych z poziomu spójności silne wymaga danych zamkniętej do jednego regionu Azure i globalny nie jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="7dd1a-112">Z drugiej strony, poziomy swobodna spójności — spójność powiązanej nieaktualności, session lub Włącz ostatecznego można skojarzyć dowolną liczbę regiony platformy Azure przy użyciu konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="7dd1a-113">Następujące prostych krokach pokazano, jak wybrać domyślny poziom spójności dla konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="7dd1a-114">Aby określić domyślna spójność konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="7dd1a-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="7dd1a-115">W [portalu Azure](https://portal.azure.com/), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7dd1a-116">W bloku konta kliknij **domyślna spójność**.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="7dd1a-117">W **domyślna spójność** bloku, wybierz nowy poziom spójności i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="7dd1a-118">![Domyślna spójność sesji][5]</span><span class="sxs-lookup"><span data-stu-id="7dd1a-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="7dd1a-119"><a id="keys"></a>Wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu</span><span class="sxs-lookup"><span data-stu-id="7dd1a-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="7dd1a-120">Podczas tworzenia konta bazy danych Azure rozwiązania Cosmos usługi generuje dwa klucze dostępu do głównego, które mogą być używane do uwierzytelniania podczas uzyskiwania dostępu do konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="7dd1a-121">Zapewniając dwa klucze dostępu do bazy danych rozwiązania Cosmos Azure umożliwia ponowne generowanie kluczy nie przeszkód do swojego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="7dd1a-122">W [portalu Azure](https://portal.azure.com/), dostępu **klucze** bloku z menu zasobów na **konta bazy danych Azure rozwiązania Cosmos** bloku, aby wyświetlić, kopiowanie i ponowne generowanie kluczy dostępu, które są używane do dostęp do tego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Azure Portal zrzut ekranu bloku klucze](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="7dd1a-124">**Klucze** bloku obejmuje również parametry połączenia podstawowych i pomocniczych, które mogą służyć do łączenia się z kontem z [narzędzia migracji danych](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="7dd1a-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="7dd1a-125">Tylko do odczytu klucze są również dostępne w tym bloku.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="7dd1a-126">Odczyty i zapytań tworzy podczas operacji tylko do odczytu, usuwanie, i nie są zastępowane.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="7dd1a-127">Kopiowanie klucza dostępu w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7dd1a-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="7dd1a-128">Na **klucze** bloku, kliknij przycisk **kopiowania** przycisku z prawej strony klucz, który chcesz skopiować.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![Wyświetlanie i kopiowanie kluczy dostępu w portalu Azure, w bloku klucze](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="7dd1a-130">Ponowne generowanie kluczy dostępu</span><span class="sxs-lookup"><span data-stu-id="7dd1a-130">Regenerate access keys</span></span>
<span data-ttu-id="7dd1a-131">Należy zmienić klucze dostępu do konta bazy danych Azure rozwiązania Cosmos okresowo, aby zabezpieczyć połączenia.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="7dd1a-132">Dwa klucze dostępu są przypisywane do utrzymania połączeń przy użyciu jednego klucza dostępu, jednocześnie ponownie generując drugi klucz dostępu konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="7dd1a-133">Trwa ponowne generowanie kluczy dostępu ma wpływ na wszystkie aplikacje, które są zależne od bieżącego klucza.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="7dd1a-134">Wszyscy klienci, którzy używają klucza dostępu do uzyskania dostępu do konta bazy danych Azure rozwiązania Cosmos trzeba zaktualizować do użycia nowego klucza.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="7dd1a-135">Jeśli masz aplikacje lub usługi w chmurze przy użyciu konta bazy danych Azure rozwiązania Cosmos utracisz połączenia ponownego generowania kluczy, chyba że wdrożysz klucze.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="7dd1a-136">Poniższe kroki wchodzą w skład proces stopniowych kluczy.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="7dd1a-137">Zaktualizuj klucz dostępu w kodzie aplikacji, aby odwołać pomocniczy klucz dostępu konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7dd1a-138">Ponownie wygenerować podstawowy klucz dostępu dla konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="7dd1a-139">W [Azure Portal](https://portal.azure.com/), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="7dd1a-140">W **konto bazy danych Azure rozwiązania Cosmos** bloku, kliknij przycisk **klucze**.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="7dd1a-141">Na **klucze** bloku, kliknij przycisk regenerate, a następnie kliknij przycisk **Ok** aby potwierdzić wygenerowanie nowego klucza.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="7dd1a-142">![Ponowne generowanie kluczy dostępu](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="7dd1a-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="7dd1a-143">Po upewnieniu się, że nowy klucz jest dostępny do użycia (około 5 minut od ponownego wygenerowania), należy zaktualizować klucz dostępu w kodzie aplikacji, aby odwołać nowego podstawowego klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="7dd1a-144">Wygeneruj ponownie pomocniczy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-144">Regenerate the secondary access key.</span></span>
   
    ![Ponowne generowanie kluczy dostępu](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="7dd1a-146">Może upłynąć kilka minut przed wygenerowanym klucza może służyć do uzyskania dostępu do konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="7dd1a-147">Pobierz ciąg połączenia</span><span class="sxs-lookup"><span data-stu-id="7dd1a-147">Get the  connection string</span></span>
<span data-ttu-id="7dd1a-148">Aby pobrać parametrów połączenia, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7dd1a-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="7dd1a-149">W [portalu Azure](https://portal.azure.com), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7dd1a-150">W menu zasobów kliknij **klucze**.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="7dd1a-151">Kliknij przycisk **kopiowania** znajdujący się obok **parametry połączenia podstawowej** lub **parametry połączenia pomocniczej** pole.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="7dd1a-152">Jeśli używane są parametry połączenia w [narzędzia migracji bazy danych DB rozwiązania Cosmos Azure](import-data.md), Dodaj nazwę bazy danych do końca ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="7dd1a-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="7dd1a-154"><a id="delete"></a>Usuń konto bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="7dd1a-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="7dd1a-155">Aby usunąć konta bazy danych Azure rozwiązania Cosmos z portalu Azure, nie jest już używany, kliknij prawym przyciskiem myszy nazwę konta, a następnie kliknij przycisk **usunąć konto**.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![Jak usunąć konto bazy danych Azure rozwiązania Cosmos w portalu Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="7dd1a-157">W [portalu Azure](https://portal.azure.com/), uzyskać dostęp do konta bazy danych Azure rozwiązania Cosmos do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="7dd1a-158">Na **konta bazy danych Azure rozwiązania Cosmos** bloku, kliknij prawym przyciskiem myszy konto, a następnie kliknij przycisk **usunąć konto**.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="7dd1a-159">W bloku wynikowy potwierdzenie wpisz nazwę konta Azure DB rozwiązania Cosmos aby upewnić się, że chcesz usunąć to konto.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="7dd1a-160">Kliknij przycisk **usunąć** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7dd1a-160">Click the **Delete** button.</span></span>

![Jak usunąć konto bazy danych Azure rozwiązania Cosmos w portalu Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="7dd1a-162"><a id="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7dd1a-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="7dd1a-163">Dowiedz się, jak [Rozpoczynanie pracy z Twoim kontem platformy Azure DB rozwiązania Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="7dd1a-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
