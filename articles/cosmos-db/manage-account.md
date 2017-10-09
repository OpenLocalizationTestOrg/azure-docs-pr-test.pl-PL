---
title: "konto bazy danych rozwiązania Cosmos Azure za pośrednictwem portalu Azure hello aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage Twojego Azure DB rozwiązania Cosmos konta za pośrednictwem hello portalu Azure. Przewodnik na temat używania hello tooview portalu Azure, kopiowania, usuwania i dostępu do konta."
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
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="22e60-105">Jak toomanage konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="22e60-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="22e60-106">Dowiedz się, jak pracować z kluczami tooset globalne spójności i usunąć konta bazy danych Azure rozwiązania Cosmos w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22e60-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="22e60-107"><a id="consistency"></a>Zarządzanie ustawieniami spójności bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="22e60-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="22e60-108">Wybieranie poziomu spójności prawo hello zależy od semantyki hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22e60-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="22e60-109">Należy zapoznać się z hello poziomy spójności dostępne w usłudze Azure DB rozwiązania Cosmos odczytując [przy użyciu spójności poziomy toomaximize dostępności i wydajności w usłudze Azure DB rozwiązania Cosmos][consistency].</span><span class="sxs-lookup"><span data-stu-id="22e60-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="22e60-110">Azure DB rozwiązania Cosmos zapewnia spójność, dostępności i wydajności gwarancji, na każdym poziomie spójności niedostępna dla Twojego konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="22e60-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="22e60-111">Konfigurowanie konta bazy danych z poziomu spójności silne wymaga danych zamkniętej tooa pojedynczy region platformy Azure i niedostępne globalnie.</span><span class="sxs-lookup"><span data-stu-id="22e60-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="22e60-112">Na drugiej Witaj, hello poziomy swobodna spójności — spójność powiązanej nieaktualności, session lub Włącz ostatecznego tooassociate można dowolną liczbę regiony platformy Azure przy użyciu konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="22e60-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="22e60-113">Hello następujące proste kroki pokazują, jak tooselect hello domyślny poziom spójności dla konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="22e60-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="22e60-114">toospecify hello domyślna spójność konta bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="22e60-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="22e60-115">W hello [portalu Azure](https://portal.azure.com/), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="22e60-116">W bloku konta usługi powitania kliknij **domyślna spójność**.</span><span class="sxs-lookup"><span data-stu-id="22e60-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="22e60-117">W hello **domyślna spójność** bloku, wybierz hello nowy poziom spójności i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="22e60-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="22e60-118">![Domyślna spójność sesji][5]</span><span class="sxs-lookup"><span data-stu-id="22e60-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="22e60-119"><a id="keys"></a>Wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu</span><span class="sxs-lookup"><span data-stu-id="22e60-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="22e60-120">Podczas tworzenia konta bazy danych Azure rozwiązania Cosmos usługi hello generuje dwa klucze dostępu do głównego, które mogą być używane do uwierzytelniania podczas uzyskiwania dostępu do hello konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="22e60-121">Zapewniając dwa klucze dostępu do bazy danych Azure rozwiązania Cosmos umożliwia tooregenerate hello klucze z nie przeszkód tooyour konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="22e60-122">W hello [portalu Azure](https://portal.azure.com/), hello dostępu **klucze** bloku z menu zasobów hello na powitania **konta bazy danych Azure rozwiązania Cosmos** tooview bloku, kopiowania i regenerate hello kluczy dostępu są używane tooaccess konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Azure Portal zrzut ekranu bloku klucze](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="22e60-124">Witaj **klucze** blok zawiera również podstawowe i parametry połączenia pomocniczej, które mogą być używane tooconnect tooyour konta z hello [narzędzia migracji danych](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="22e60-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="22e60-125">Tylko do odczytu klucze są również dostępne w tym bloku.</span><span class="sxs-lookup"><span data-stu-id="22e60-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="22e60-126">Odczyty i zapytań tworzy podczas operacji tylko do odczytu, usuwanie, i nie są zastępowane.</span><span class="sxs-lookup"><span data-stu-id="22e60-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="22e60-127">Skopiuj klucz dostępu w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="22e60-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="22e60-128">Na powitania **klucze** bloku, kliknij hello **kopiowania** toohello przycisk rogu hello klucz ma toocopy.</span><span class="sxs-lookup"><span data-stu-id="22e60-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![Wyświetlanie i kopiowanie kluczy dostępu w portalu Azure, bloku klucze hello](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="22e60-130">Ponowne generowanie kluczy dostępu</span><span class="sxs-lookup"><span data-stu-id="22e60-130">Regenerate access keys</span></span>
<span data-ttu-id="22e60-131">Należy zmienić hello dostępu do kluczy tooyour bazy danych Azure rozwiązania Cosmos konta okresowo toohelp zabezpieczania połączeń.</span><span class="sxs-lookup"><span data-stu-id="22e60-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="22e60-132">Dwa klucze dostępu są przypisane tooenable możesz toomaintain połączeń toohello konta bazy danych Azure rozwiązania Cosmos przy użyciu jednego klucza dostępu, jednocześnie ponownie generując hello drugi klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="22e60-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="22e60-133">Trwa ponowne generowanie kluczy dostępu ma wpływ na wszystkie aplikacje, które są zależne od hello bieżącego klucza.</span><span class="sxs-lookup"><span data-stu-id="22e60-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="22e60-134">Wszystkich klientów, którzy używają hello dostępu do klucza tooaccess hello Azure DB rozwiązania Cosmos konta musi być zaktualizowany toouse hello nowego klucza.</span><span class="sxs-lookup"><span data-stu-id="22e60-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="22e60-135">Jeśli masz aplikacje lub usługi w chmurze przy użyciu konta bazy danych Azure rozwiązania Cosmos hello utracisz połączenia hello ponownego generowania kluczy, chyba że wdrożysz klucze.</span><span class="sxs-lookup"><span data-stu-id="22e60-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="22e60-136">Hello poniższe kroki wchodzą w skład procesu hello objętego stopniowych klucze.</span><span class="sxs-lookup"><span data-stu-id="22e60-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="22e60-137">Zaktualizuj klucz dostępu hello w Twojej aplikacji kod tooreference hello pomocniczy klucz dostępu z hello konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="22e60-138">Wygeneruj ponownie hello podstawowy klucz dostępu dla konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="22e60-139">W hello [Azure Portal](https://portal.azure.com/), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="22e60-140">W hello **konto bazy danych Azure rozwiązania Cosmos** bloku, kliknij przycisk **klucze**.</span><span class="sxs-lookup"><span data-stu-id="22e60-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="22e60-141">Na powitania **klucze** bloku, kliknij przycisk regenerate hello, a następnie kliknij przycisk **Ok** tooconfirm, które mają toogenerate nowy klucz.</span><span class="sxs-lookup"><span data-stu-id="22e60-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="22e60-142">![Ponowne generowanie kluczy dostępu](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="22e60-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="22e60-143">Po upewnieniu się, się, że ten nowy klucz hello jest dostępny do użytku (około 5 minut od ponownego wygenerowania), zaktualizować klucza dostępu hello w Twojej aplikacji kod tooreference hello nowego podstawowego klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="22e60-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="22e60-144">Wygeneruj ponownie hello pomocniczy klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="22e60-144">Regenerate hello secondary access key.</span></span>
   
    ![Ponowne generowanie kluczy dostępu](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="22e60-146">Może upłynąć kilka minut, zanim nowo wygenerowany klucz może być używane tooaccess konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="22e60-147">Pobierz ciąg połączenia hello</span><span class="sxs-lookup"><span data-stu-id="22e60-147">Get hello  connection string</span></span>
<span data-ttu-id="22e60-148">tooretrieve połączenie string, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="22e60-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="22e60-149">W hello [portalu Azure](https://portal.azure.com), dostęp do tego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="22e60-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="22e60-150">W menu zasobów hello, kliknij przycisk **klucze**.</span><span class="sxs-lookup"><span data-stu-id="22e60-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="22e60-151">Kliknij hello **kopiowania** przycisku Dalej toohello **parametry połączenia podstawowej** lub **parametry połączenia pomocniczej** pole.</span><span class="sxs-lookup"><span data-stu-id="22e60-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="22e60-152">Jeśli używane są parametry połączenia hello w hello [narzędzia migracji bazy danych DB rozwiązania Cosmos Azure](import-data.md), Dołącz hello bazy danych nazwa toohello koniec hello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="22e60-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="22e60-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="22e60-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="22e60-154"><a id="delete"></a>Usuń konto bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="22e60-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="22e60-155">tooremove bazy danych Azure rozwiązania Cosmos konta z hello Portal Azure nie jest już używany, kliknij prawym przyciskiem myszy nazwę konta hello i kliknij przycisk **usunąć konto**.</span><span class="sxs-lookup"><span data-stu-id="22e60-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![Jak konto toodelete bazy danych Azure rozwiązania Cosmos hello portalu Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="22e60-157">W hello [portalu Azure](https://portal.azure.com/), uzyskać dostęp do konta bazy danych Azure rozwiązania Cosmos hello mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="22e60-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="22e60-158">Na powitania **konta bazy danych Azure rozwiązania Cosmos** bloku, kliknij prawym przyciskiem myszy konto hello, a następnie kliknij przycisk **usunąć konto**.</span><span class="sxs-lookup"><span data-stu-id="22e60-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="22e60-159">Na powitania wynikowy bloku potwierdzenie wpisz hello Azure DB rozwiązania Cosmos konta, które mają konta hello toodelete nazwa tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="22e60-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="22e60-160">Kliknij przycisk hello **usunąć** przycisku.</span><span class="sxs-lookup"><span data-stu-id="22e60-160">Click hello **Delete** button.</span></span>

![Jak konto toodelete bazy danych Azure rozwiązania Cosmos hello portalu Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="22e60-162"><a id="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22e60-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="22e60-163">Dowiedz się, jak za[Rozpoczynanie pracy z Twoim kontem platformy Azure DB rozwiązania Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="22e60-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
