---
title: "aaaHow toosecure dostępu tooAzure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toosecure usługi data catalog i jej zasobów danych."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="51600-103">Jak toosecure uzyskują dostęp do zasobów katalogu i danych toodata</span><span class="sxs-lookup"><span data-stu-id="51600-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="51600-104">Ta funkcja jest dostępna tylko w wersji standard hello usługi Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="51600-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="51600-105">Wykaz danych Azure umożliwia toospecify, kto ma dostęp do wykazu danych hello i jakie operacje (rejestrowanie, dodawanie adnotacji, przejąć na własność) mogą dotyczyć metadanych w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="51600-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="51600-106">Katalogu użytkowników i uprawnień</span><span class="sxs-lookup"><span data-stu-id="51600-106">Catalog users and permissions</span></span>
<span data-ttu-id="51600-107">toogive przez użytkownika lub hello grupy dostępu usługi data catalog tooa i ustawić uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="51600-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="51600-108">Na powitania [strony głównej wykazu danych](http://www.azuredatacatalog.com), kliknij przycisk **ustawienia** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="51600-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![Data catalog — ustawienia](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="51600-110">Na stronie ustawień hello, rozwiń węzeł hello **użytkownicy wykazu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="51600-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="51600-111">![W katalogu użytkowników — Dodaj](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="51600-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="51600-112">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="51600-112">Click **Add**.</span></span>
4. <span data-ttu-id="51600-113">Wprowadź w pełni kwalifikowana hello **nazwy użytkownika** lub nazwa hello **grupy zabezpieczeń** w hello Azure Active Directory (AAD) skojarzone z hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="51600-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="51600-114">Użyj przecinka (",") jako separatora, dodając więcej niż jednego użytkownika lub grupę.</span><span class="sxs-lookup"><span data-stu-id="51600-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="51600-115">![Użytkownicy wykazu - użytkowników lub grup](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="51600-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="51600-116">Naciśnij klawisz **ENTER** lub **kartę** poza hello pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="51600-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="51600-117">Upewnij się, że wszystkie uprawnienia (**Adnotuj**, **zarejestrować**, i **Przejmij na własność**) domyślnie przypisane toothese użytkowników lub grup.</span><span class="sxs-lookup"><span data-stu-id="51600-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="51600-118">Oznacza to, że hello użytkownik lub grupa może [zarejestrować zasobów danych]( data-catalog-how-to-register.md), [adnotacji zasobów danych]( data-catalog-how-to-annotate.md), i [przejąć na własność zasobów danych]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="51600-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="51600-119">![Użytkownicy wykazu - domyślnych uprawnień](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="51600-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="51600-120">toogive użytkownikowi lub grupie tylko hello katalogu toohello dostęp, wyczyść hello **adnotacji** opcji dla tego użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="51600-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="51600-121">Po wykonaniu tej hello użytkownika lub grupy nie można adnotować zasobów danych w katalogu hello, ale mogą je wyświetlać.</span><span class="sxs-lookup"><span data-stu-id="51600-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="51600-122">toodeny użytkownika lub grupy z rejestrowania zasobów danych, wyczyść hello **zarejestrować** opcji dla tego użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="51600-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="51600-123">toodeny użytkownika z przejmowania własności zasobów danych, wyczyść hello **przejąć na własność** opcji dla tego użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="51600-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="51600-124">toodelete użytkownika/grupy użytkowników z katalogu, kliknij przycisk **x** hello użytkownika/grupy u dołu hello hello listy.</span><span class="sxs-lookup"><span data-stu-id="51600-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="51600-125">![Użytkownicy w katalogu — Usuń użytkownika](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="51600-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="51600-126">Zalecamy bezpośrednio dodać użytkowników toocatalog grup zabezpieczeń, zamiast dodawania użytkowników, a następnie przypisz uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="51600-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="51600-127">Następnie należy dodać grupy zabezpieczeń toohello użytkowników odpowiadających im role i ich katalogu toohello wymaganego dostępu.</span><span class="sxs-lookup"><span data-stu-id="51600-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="51600-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="51600-128">Special considerations</span></span>

- <span data-ttu-id="51600-129">grupy toosecurity przypisane uprawnienia Hello są dodatku.</span><span class="sxs-lookup"><span data-stu-id="51600-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="51600-130">Użytkownik jest w dwóch grupach.</span><span class="sxs-lookup"><span data-stu-id="51600-130">Say, a user is in two groups.</span></span> <span data-ttu-id="51600-131">Jedna grupa ma adnotacji uprawnienia i nie mają adnotacje do innej grupy uprawnień.</span><span class="sxs-lookup"><span data-stu-id="51600-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="51600-132">Następnie użytkownik ma adnotacji uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="51600-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="51600-133">jawnie hello zastąpienie użytkownika tooa przypisane uprawnienia toogroups toowhich hello użytkownika należy przypisać uprawnienia Hello.</span><span class="sxs-lookup"><span data-stu-id="51600-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="51600-134">W poprzednim przykładzie hello powiedzieć jawnie dodać hello użytkownika toocatalog użytkowników i nie należy przypisywać uprawnienia adnotacji.</span><span class="sxs-lookup"><span data-stu-id="51600-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="51600-135">Użytkownik Hello nie adnotacji zasobów danych, mimo że hello użytkownik jest członkiem grupy, która ma adnotacji uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="51600-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51600-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51600-136">Next steps</span></span>
- [<span data-ttu-id="51600-137">Rozpoczynanie pracy z usługą Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="51600-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

