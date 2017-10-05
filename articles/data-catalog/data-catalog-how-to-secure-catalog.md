---
title: "Jak zabezpieczyć dostęp do usługi Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak zabezpieczyć dane katalogu i jego zasobów danych."
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
ms.openlocfilehash: 9664a7bc8493b08c8e0797ac6f1b212079829833
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-secure-access-to-data-catalog-and-data-assets"></a><span data-ttu-id="d36db-103">Jak zabezpieczyć dostęp do katalogu danych i zasobów danych</span><span class="sxs-lookup"><span data-stu-id="d36db-103">How to secure access to data catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d36db-104">Ta funkcja jest dostępna tylko w wersji standard usługi Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="d36db-104">This feature is available only in the standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="d36db-105">Wykaz danych Azure służy do określania, kto ma dostęp do katalogu danych i jakie operacje (rejestrowanie, dodawanie adnotacji, przejąć na własność) mogą dotyczyć metadanych w katalogu.</span><span class="sxs-lookup"><span data-stu-id="d36db-105">Azure Data Catalog allows you to specify who can access the data catalog and what operations (register, annotate, take ownership) they can perform on metadata in the catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="d36db-106">Katalogu użytkowników i uprawnień</span><span class="sxs-lookup"><span data-stu-id="d36db-106">Catalog users and permissions</span></span>
<span data-ttu-id="d36db-107">Aby podać użytkownik lub Grupa dostępu do wykazu danych i ustawić uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="d36db-107">To give a user or a group the access to a data catalog and set permissions:</span></span>

1. <span data-ttu-id="d36db-108">Na [strony głównej wykazu danych](http://www.azuredatacatalog.com), kliknij przycisk **ustawienia** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="d36db-108">On the [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on the toolbar.</span></span>

    ![Data catalog — ustawienia](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="d36db-110">Na stronie ustawień, rozwiń węzeł **użytkownicy wykazu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d36db-110">In the settings page, expand the **Catalog Users** section.</span></span>
    <span data-ttu-id="d36db-111">![W katalogu użytkowników — Dodaj](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="d36db-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="d36db-112">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d36db-112">Click **Add**.</span></span>
4. <span data-ttu-id="d36db-113">Wprowadź w pełni kwalifikowaną **nazwy użytkownika** lub nazwa **grupy zabezpieczeń** w usłudze Azure Active Directory (AAD) skojarzone z katalogiem.</span><span class="sxs-lookup"><span data-stu-id="d36db-113">Enter the fully qualified **user name** or name of the **security group** in the Azure Active Directory (AAD) associated with the catalog.</span></span> <span data-ttu-id="d36db-114">Użyj przecinka (",") jako separatora, dodając więcej niż jednego użytkownika lub grupę.</span><span class="sxs-lookup"><span data-stu-id="d36db-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="d36db-115">![Użytkownicy wykazu - użytkowników lub grup](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="d36db-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="d36db-116">Naciśnij klawisz **ENTER** lub **kartę** poza pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d36db-116">Press **ENTER** or **TAB** out of the text box.</span></span> 
6.  <span data-ttu-id="d36db-117">Upewnij się, że wszystkie uprawnienia (**Adnotuj**, **zarejestrować**, i **Przejmij na własność**) są domyślnie przypisane do tych użytkowników lub grup.</span><span class="sxs-lookup"><span data-stu-id="d36db-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned to these users or groups by default.</span></span> <span data-ttu-id="d36db-118">Oznacza to, że użytkownik lub grupa może [zarejestrować zasobów danych]( data-catalog-how-to-register.md), [adnotacji zasobów danych]( data-catalog-how-to-annotate.md), i [przejąć na własność zasobów danych]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="d36db-118">That is, the user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="d36db-119">![Użytkownicy wykazu - domyślnych uprawnień](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="d36db-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="d36db-120">Aby dać użytkownikowi lub grupie dostęp tylko do odczytu do katalogu, wyczyść **adnotacji** opcji dla tego użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="d36db-120">To give a user or group only the read access to the catalog, clear the **annotate** option for that user or group.</span></span> <span data-ttu-id="d36db-121">Można to zrobić, użytkownik lub grupa nie adnotacji zasobów danych w katalogu, ale mogą je wyświetlać.</span><span class="sxs-lookup"><span data-stu-id="d36db-121">When you do so, the user or group cannot annotate data assets in the catalog but they can view them.</span></span> 
8.  <span data-ttu-id="d36db-122">Aby uniemożliwić użytkownikowi lub grupie zasobów danych rejestrowania, wyczyść **zarejestrować** opcji dla tego użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="d36db-122">To deny a user or group from registering data assets, clear the **register** option for that user or group.</span></span>
9.  <span data-ttu-id="d36db-123">Aby zablokować użytkownika z przejmowania własności zasobów danych, wyczyść **przejąć na własność** opcji dla tego użytkownika lub grupy.</span><span class="sxs-lookup"><span data-stu-id="d36db-123">To deny a user from taking ownership of a data asset, clear the **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="d36db-124">Aby usunąć użytkownika/grupy użytkowników z katalogu, kliknij przycisk **x**  /grupy użytkowników w dolnej części listy.</span><span class="sxs-lookup"><span data-stu-id="d36db-124">To delete a user/group from catalog users, click **x** for the user/group at the bottom of the list.</span></span> 
    <span data-ttu-id="d36db-125">![Użytkownicy w katalogu — Usuń użytkownika](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="d36db-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d36db-126">Firma Microsoft zaleca, aby dodać grupy zabezpieczeń, aby bezpośrednio katalogu użytkowników, zamiast dodawania użytkowników i przypisać uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d36db-126">We recommend that you add security groups to catalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="d36db-127">Następnie należy dodać użytkowników do grup zabezpieczeń, które odpowiada ich ról oraz ich wymagany dostęp do katalogu.</span><span class="sxs-lookup"><span data-stu-id="d36db-127">Then, add users to the security groups that match their roles and their required access to the catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="d36db-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d36db-128">Special considerations</span></span>

- <span data-ttu-id="d36db-129">Uprawnienia przypisane do grupy zabezpieczeń są dodatku.</span><span class="sxs-lookup"><span data-stu-id="d36db-129">The permissions assigned to security groups are additive.</span></span> <span data-ttu-id="d36db-130">Użytkownik jest w dwóch grupach.</span><span class="sxs-lookup"><span data-stu-id="d36db-130">Say, a user is in two groups.</span></span> <span data-ttu-id="d36db-131">Jedna grupa ma adnotacji uprawnienia i nie mają adnotacje do innej grupy uprawnień.</span><span class="sxs-lookup"><span data-stu-id="d36db-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="d36db-132">Następnie użytkownik ma adnotacji uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d36db-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="d36db-133">Uprawnienia jawnie przypisane do użytkownika musi zostać zastąpiona uprawnienia przypisane do grup, do których należy użytkownik.</span><span class="sxs-lookup"><span data-stu-id="d36db-133">The permissions assigned explicitly to a user override the permissions assigned to groups to which the user belongs.</span></span> <span data-ttu-id="d36db-134">W poprzednim przykładzie powiedzieć jawnie dodawania użytkownika do katalogu użytkowników i czy nie przypisuj uprawnienia funkcji dodawania adnotacji.</span><span class="sxs-lookup"><span data-stu-id="d36db-134">In the previous example, say, you explicitly added the user to catalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="d36db-135">Użytkownik nie adnotacji zasobów danych, nawet jeśli użytkownik jest członkiem grupy, która ma adnotacji uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="d36db-135">The user cannot annotate data assets even though the user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d36db-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d36db-136">Next steps</span></span>
- [<span data-ttu-id="d36db-137">Rozpoczynanie pracy z usługą Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="d36db-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

