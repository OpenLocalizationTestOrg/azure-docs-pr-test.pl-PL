---
title: "aaaOverview kontroli dostępu w usłudze Data Lake Store | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu działania kontroli dostępu w usłudze Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="5fa04-103">Kontrola dostępu w usłudze Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5fa04-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="5fa04-104">Azure Data Lake Store implementuje model kontroli dostępu, która pochodzi z systemu plików HDFS, który z kolei jest pochodną model kontroli dostępu POSIX hello.</span><span class="sxs-lookup"><span data-stu-id="5fa04-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="5fa04-105">Ten artykuł zawiera podsumowanie hello podstawy hello model kontroli dostępu dla usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="5fa04-106">toolearn więcej informacji na temat hello model kontroli dostępu do systemu plików HDFS, zobacz [przewodnik uprawnienia systemu plików HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="5fa04-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="5fa04-107">Listy kontroli dostępu do plików i folderów</span><span class="sxs-lookup"><span data-stu-id="5fa04-107">Access control lists on files and folders</span></span>

<span data-ttu-id="5fa04-108">Istnieją dwa typy list kontroli dostępu (ACL) — **Listy ACL dostępu** i **Domyślne listy ACL**.</span><span class="sxs-lookup"><span data-stu-id="5fa04-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="5fa04-109">**Dostęp do listy ACL**: obiekt tooan tych kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="5fa04-110">Pliki i foldery mają listy ACL dostępu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="5fa04-111">**Domyślne listy ACL**: "szablon" listy kontroli dostępu skojarzone z folderem ustalić hello dostępu ACL dla wszystkie elementy podrzędne, które zostały utworzone w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="5fa04-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="5fa04-112">Pliki nie mają domyślnych list ACL.</span><span class="sxs-lookup"><span data-stu-id="5fa04-112">Files do not have Default ACLs.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="5fa04-114">Zarówno listy ACL dostępu, jak i domyślnej listy ACL mają hello tej samej struktury.</span><span class="sxs-lookup"><span data-stu-id="5fa04-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="5fa04-116">Zmiana hello domyślnej listy ACL na element nadrzędny nie ma wpływu na powitania dostępu lub domyślnej listy ACL elementy podrzędne, które już istnieją.</span><span class="sxs-lookup"><span data-stu-id="5fa04-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="5fa04-117">Użytkownicy i tożsamości</span><span class="sxs-lookup"><span data-stu-id="5fa04-117">Users and identities</span></span>

<span data-ttu-id="5fa04-118">Każdy plik i folder ma różne uprawnienia do tych tożsamości:</span><span class="sxs-lookup"><span data-stu-id="5fa04-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="5fa04-119">Witaj, będącej właścicielem, jeśli użytkownik hello pliku</span><span class="sxs-lookup"><span data-stu-id="5fa04-119">hello owning user of hello file</span></span>
* <span data-ttu-id="5fa04-120">Witaj będący właścicielem grupy</span><span class="sxs-lookup"><span data-stu-id="5fa04-120">hello owning group</span></span>
* <span data-ttu-id="5fa04-121">Użytkownicy nazwani</span><span class="sxs-lookup"><span data-stu-id="5fa04-121">Named users</span></span>
* <span data-ttu-id="5fa04-122">Grupy nazwane</span><span class="sxs-lookup"><span data-stu-id="5fa04-122">Named groups</span></span>
* <span data-ttu-id="5fa04-123">Wszyscy pozostali użytkownicy</span><span class="sxs-lookup"><span data-stu-id="5fa04-123">All other users</span></span>

<span data-ttu-id="5fa04-124">Witaj tożsamości użytkowników i grup są tożsamości usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fa04-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="5fa04-125">Chyba że określono inaczej, "użytkownika" w kontekście hello Data Lake Store może oznaczać albo użytkownika usługi Azure AD lub grupy zabezpieczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fa04-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="5fa04-126">Uprawnienia</span><span class="sxs-lookup"><span data-stu-id="5fa04-126">Permissions</span></span>

<span data-ttu-id="5fa04-127">Witaj uprawnień do obiektu systemu plików są **odczytu**, **zapisu**, i **Execute**, i mogą być używane w pliki i foldery, jak pokazano w poniższej tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="5fa04-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="5fa04-128">Plik</span><span class="sxs-lookup"><span data-stu-id="5fa04-128">File</span></span>     |   <span data-ttu-id="5fa04-129">Folder</span><span class="sxs-lookup"><span data-stu-id="5fa04-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="5fa04-130">**Odczyt (R)**</span><span class="sxs-lookup"><span data-stu-id="5fa04-130">**Read (R)**</span></span> | <span data-ttu-id="5fa04-131">Można odczytać zawartości pliku hello</span><span class="sxs-lookup"><span data-stu-id="5fa04-131">Can read hello contents of a file</span></span> | <span data-ttu-id="5fa04-132">Wymaga **odczytu** i **Execute** toolist hello zawartość folderu hello</span><span class="sxs-lookup"><span data-stu-id="5fa04-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="5fa04-133">**Zapis (W)**</span><span class="sxs-lookup"><span data-stu-id="5fa04-133">**Write (W)**</span></span> | <span data-ttu-id="5fa04-134">Można zapisać lub Dołącz plik tooa</span><span class="sxs-lookup"><span data-stu-id="5fa04-134">Can write or append tooa file</span></span> | <span data-ttu-id="5fa04-135">Wymaga **zapisu** i **Execute** toocreate elementy podrzędne w folderze</span><span class="sxs-lookup"><span data-stu-id="5fa04-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="5fa04-136">**Wykonanie (X)**</span><span class="sxs-lookup"><span data-stu-id="5fa04-136">**Execute (X)**</span></span> | <span data-ttu-id="5fa04-137">Nie oznacza niczego w kontekście hello Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5fa04-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="5fa04-138">Elementy podrzędne hello tootraverse wymaganego folderu</span><span class="sxs-lookup"><span data-stu-id="5fa04-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="5fa04-139">Krótkie formy uprawnień</span><span class="sxs-lookup"><span data-stu-id="5fa04-139">Short forms for permissions</span></span>

<span data-ttu-id="5fa04-140">**RWX** jest używane tooindicate **odczytu i zapisu i wykonać**.</span><span class="sxs-lookup"><span data-stu-id="5fa04-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="5fa04-141">Zmniejszoną formularza liczbowych istnieje w którym **odczytu = 4**, **zapisu = 2**, i **Execute = 1**, Suma hello reprezentuje hello uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="5fa04-142">Poniżej przedstawiono kilka przykładów.</span><span class="sxs-lookup"><span data-stu-id="5fa04-142">Following are some examples.</span></span>

| <span data-ttu-id="5fa04-143">Forma liczbowa</span><span class="sxs-lookup"><span data-stu-id="5fa04-143">Numeric form</span></span> | <span data-ttu-id="5fa04-144">Forma krótka</span><span class="sxs-lookup"><span data-stu-id="5fa04-144">Short form</span></span> |      <span data-ttu-id="5fa04-145">Co to oznacza</span><span class="sxs-lookup"><span data-stu-id="5fa04-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="5fa04-146">7</span><span class="sxs-lookup"><span data-stu-id="5fa04-146">7</span></span>            | <span data-ttu-id="5fa04-147">RWX</span><span class="sxs-lookup"><span data-stu-id="5fa04-147">RWX</span></span>        | <span data-ttu-id="5fa04-148">Odczyt (R) + zapis (W) + wykonanie (X)</span><span class="sxs-lookup"><span data-stu-id="5fa04-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="5fa04-149">5</span><span class="sxs-lookup"><span data-stu-id="5fa04-149">5</span></span>            | <span data-ttu-id="5fa04-150">R-X</span><span class="sxs-lookup"><span data-stu-id="5fa04-150">R-X</span></span>        | <span data-ttu-id="5fa04-151">Odczyt (R) + wykonanie (X)</span><span class="sxs-lookup"><span data-stu-id="5fa04-151">Read + Execute</span></span>         |
| <span data-ttu-id="5fa04-152">4</span><span class="sxs-lookup"><span data-stu-id="5fa04-152">4</span></span>            | <span data-ttu-id="5fa04-153">R--</span><span class="sxs-lookup"><span data-stu-id="5fa04-153">R--</span></span>        | <span data-ttu-id="5fa04-154">Odczyt</span><span class="sxs-lookup"><span data-stu-id="5fa04-154">Read</span></span>                   |
| <span data-ttu-id="5fa04-155">0</span><span class="sxs-lookup"><span data-stu-id="5fa04-155">0</span></span>            | ---        | <span data-ttu-id="5fa04-156">Brak uprawnień</span><span class="sxs-lookup"><span data-stu-id="5fa04-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="5fa04-157">Uprawnienia nie są dziedziczone</span><span class="sxs-lookup"><span data-stu-id="5fa04-157">Permissions do not inherit</span></span>

<span data-ttu-id="5fa04-158">W modelu POSIX stylu hello jest używany przez usługi Data Lake Store uprawnienia dla elementu są przechowywane w samym elemencie hello.</span><span class="sxs-lookup"><span data-stu-id="5fa04-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="5fa04-159">Innymi słowy uprawnienia dla elementu nie może być dziedziczona z hello elementów nadrzędnych.</span><span class="sxs-lookup"><span data-stu-id="5fa04-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="5fa04-160">Typowe scenariusze toopermissions pokrewne</span><span class="sxs-lookup"><span data-stu-id="5fa04-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="5fa04-161">Poniżej przedstawiono niektóre typowe scenariusze toohelp, zrozumieć, jakie uprawnienia są wymagane tooperform pewnych operacji na konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="5fa04-162">Wymagane uprawnienia tooread pliku</span><span class="sxs-lookup"><span data-stu-id="5fa04-162">Permissions needed tooread a file</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="5fa04-164">Dla hello toobe pliku do odczytu, hello wywołujący musi **odczytu** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="5fa04-165">Dla wszystkich hello folderach hello struktury folderów zawierających plik hello, hello wywołujący musi **Execute** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="5fa04-166">Plik tooa tooappend potrzebne uprawnienia</span><span class="sxs-lookup"><span data-stu-id="5fa04-166">Permissions needed tooappend tooa file</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="5fa04-168">Dla hello toobe plik dołączany do, hello wywołujący musi **zapisu** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="5fa04-169">Dla wszystkich hello foldery, które zawierają hello pliku, hello wywołujący musi **Execute** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="5fa04-170">Wymagane uprawnienia toodelete pliku</span><span class="sxs-lookup"><span data-stu-id="5fa04-170">Permissions needed toodelete a file</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="5fa04-172">Dla folderu nadrzędnego hello, hello wywołujący musi **zapisu i wykonywania** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="5fa04-173">Dla wszystkich hello innych folderów w ścieżce pliku hello, hello wywołujący musi **Execute** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="5fa04-174">Zapisu uprawnienia pliku hello nie są wymagane toodelete go tak długo, jak hello poprzednie dwa warunki są spełnione.</span><span class="sxs-lookup"><span data-stu-id="5fa04-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="5fa04-175">Wymagane uprawnienia tooenumerate folderu</span><span class="sxs-lookup"><span data-stu-id="5fa04-175">Permissions needed tooenumerate a folder</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="5fa04-177">Dla tooenumerate folderu hello, hello wywołujący musi **Odczyt i wykonywanie** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="5fa04-178">Dla wszystkich hello foldery nadrzędne, hello wywołujący musi **Execute** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="5fa04-179">Wyświetlanie uprawnień w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5fa04-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="5fa04-180">Z hello **Eksploratora danych** bloku hello konta usługi Data Lake Store kliknij **dostępu** toosee hello listy ACL dla pliku lub folderu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="5fa04-181">Kliknij przycisk **dostępu** toosee hello listy ACL dla hello **katalogu** folder hello **mydatastore** konta.</span><span class="sxs-lookup"><span data-stu-id="5fa04-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="5fa04-183">W tym bloku hello pierwsza sekcja zawiera omówienie hello uprawnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5fa04-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="5fa04-184">(Hello zrzucie ekranu, użytkownik hello jest Bob). Po tym, że uprawnienia dostępu hello są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="5fa04-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="5fa04-185">Po wykonaniu tej z hello **dostępu** bloku, kliknij przycisk **widoku uproszczonym** toosee hello prostsze widoku.</span><span class="sxs-lookup"><span data-stu-id="5fa04-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="5fa04-187">Kliknij przycisk **widoku zaawansowanego** toosee hello bardziej zaawansowane widoku, gdy są pokazywane pojęcia hello domyślnej listy ACL, maska i administratora.</span><span class="sxs-lookup"><span data-stu-id="5fa04-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="5fa04-189">Witaj administratora</span><span class="sxs-lookup"><span data-stu-id="5fa04-189">hello super-user</span></span>

<span data-ttu-id="5fa04-190">Nadtypem użytkownik ma hello większości prawa wszystkim użytkownikom hello w hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="5fa04-191">Administrator:</span><span class="sxs-lookup"><span data-stu-id="5fa04-191">A super-user:</span></span>

* <span data-ttu-id="5fa04-192">Zbyt uprawnieniami RWX**wszystkich** plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="5fa04-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="5fa04-193">Można zmienić uprawnienia hello plik lub folder.</span><span class="sxs-lookup"><span data-stu-id="5fa04-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="5fa04-194">Można zmienić hello użytkownik będący właścicielem lub będący właścicielem grupy pliku lub folderu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="5fa04-195">Na platformie Azure konto usługi Data Lake Store ma kilka ról platformy Azure, a w tym:</span><span class="sxs-lookup"><span data-stu-id="5fa04-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="5fa04-196">Właściciele</span><span class="sxs-lookup"><span data-stu-id="5fa04-196">Owners</span></span>
* <span data-ttu-id="5fa04-197">Współautorzy</span><span class="sxs-lookup"><span data-stu-id="5fa04-197">Contributors</span></span>
* <span data-ttu-id="5fa04-198">Czytelnicy</span><span class="sxs-lookup"><span data-stu-id="5fa04-198">Readers</span></span>

<span data-ttu-id="5fa04-199">Wszyscy użytkownicy w hello **właścicieli** rolę dla konta usługi Data Lake Store jest automatycznie administratora dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="5fa04-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="5fa04-200">toolearn więcej, zobacz [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5fa04-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="5fa04-201">Jeśli chcesz toocreate roli niestandardowej roli-— kontrola dostępu oparta na (rolach RBAC), która ma uprawnienia administratora musi hello toohave następujących uprawnień:</span><span class="sxs-lookup"><span data-stu-id="5fa04-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="5fa04-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="5fa04-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="5fa04-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="5fa04-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="5fa04-204">Użytkownik będący właścicielem Hello</span><span class="sxs-lookup"><span data-stu-id="5fa04-204">hello owning user</span></span>

<span data-ttu-id="5fa04-205">Hello użytkownika, który utworzył element hello jest automatycznie hello użytkownik hello element będący właścicielem.</span><span class="sxs-lookup"><span data-stu-id="5fa04-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="5fa04-206">Użytkownik będący właścicielem może:</span><span class="sxs-lookup"><span data-stu-id="5fa04-206">An owning user can:</span></span>

* <span data-ttu-id="5fa04-207">Zmień uprawnienia hello pliku, który jest właścicielem.</span><span class="sxs-lookup"><span data-stu-id="5fa04-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="5fa04-208">Zmiana będącej właścicielem grupy plików, która jest właścicielem tak długo, jak długo użytkownik będący właścicielem hello jest również członkiem grupy docelowej hello hello.</span><span class="sxs-lookup"><span data-stu-id="5fa04-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="5fa04-209">Użytkownik będący właścicielem Hello *nie* zmienić hello będącej właścicielem, jeśli użytkownik innego pliku należące do firmy.</span><span class="sxs-lookup"><span data-stu-id="5fa04-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="5fa04-210">Tylko nadtypem użytkownicy mogą zmieniać hello będącej właścicielem, jeśli użytkownik pliku lub folderu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="5fa04-211">Witaj będący właścicielem grupy</span><span class="sxs-lookup"><span data-stu-id="5fa04-211">hello owning group</span></span>

<span data-ttu-id="5fa04-212">W hello listy ACL POSIX każdy użytkownik, jest skojarzona z "podstawowej grupy".</span><span class="sxs-lookup"><span data-stu-id="5fa04-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="5fa04-213">Na przykład "Alicja" użytkownik może należeć toohello "Finanse" grupy.</span><span class="sxs-lookup"><span data-stu-id="5fa04-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="5fa04-214">Alicja może również należeć toomultiple grupy, ale jedna grupa zawsze jest oznaczony jako swojej grupy podstawowej.</span><span class="sxs-lookup"><span data-stu-id="5fa04-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="5fa04-215">W POSIX gdy Alicja tworzy plik hello grupy tego pliku będącej właścicielem, wartość grupy podstawowej tooher, czyli w tym przypadku "Finanse".</span><span class="sxs-lookup"><span data-stu-id="5fa04-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="5fa04-216">Podczas tworzenia nowego elementu systemu plików usługi Data Lake Store przypisuje toohello wartość grupy będącej właścicielem.</span><span class="sxs-lookup"><span data-stu-id="5fa04-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="5fa04-217">**Przypadek 1**: folder główny hello "/".</span><span class="sxs-lookup"><span data-stu-id="5fa04-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="5fa04-218">Ten folder jest tworzony wraz z kontem usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="5fa04-219">W takim przypadku hello będący właścicielem grupy ustawiono toohello użytkownika, który utworzył konto hello.</span><span class="sxs-lookup"><span data-stu-id="5fa04-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="5fa04-220">**Przypadek 2** (każdego innego litery): podczas tworzenia nowego elementu hello będący właścicielem grupy zostaną skopiowane z hello folderu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="5fa04-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="5fa04-221">Witaj będący właścicielem grupy może zostać zmieniona przez:</span><span class="sxs-lookup"><span data-stu-id="5fa04-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="5fa04-222">każdy administrator;</span><span class="sxs-lookup"><span data-stu-id="5fa04-222">Any super-users.</span></span>
* <span data-ttu-id="5fa04-223">Użytkownik, będący właścicielem, jeśli użytkownik będący właścicielem hello jest również członkiem grupy docelowej hello Hello.</span><span class="sxs-lookup"><span data-stu-id="5fa04-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="5fa04-224">Algorytm kontroli dostępu</span><span class="sxs-lookup"><span data-stu-id="5fa04-224">Access check algorithm</span></span>

<span data-ttu-id="5fa04-225">Witaj następującej ilustracji reprezentuje hello dostępu wyboru algorytmu dla kont usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Algorytm list ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="5fa04-227">Maska Hello i "czynne uprawnienia"</span><span class="sxs-lookup"><span data-stu-id="5fa04-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="5fa04-228">Hello **maski** jest RWX wartość czyli dostęp toolimit używane dla **nazwani użytkownicy**, hello **grupy będącej właścicielem**, i **o nazwie grupy** czasie wykonywanie hello dostępu wyboru algorytmu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="5fa04-229">Poniżej przedstawiono podstawowe pojęcia hello hello maski.</span><span class="sxs-lookup"><span data-stu-id="5fa04-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="5fa04-230">Maska Hello tworzy "czynne uprawnienia."</span><span class="sxs-lookup"><span data-stu-id="5fa04-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="5fa04-231">Oznacza to modyfikuje uprawnienia hello w czasie hello kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="5fa04-232">Maska Hello można edytować bezpośrednio przez właściciela pliku hello i nadtypem użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5fa04-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="5fa04-233">Maska Hello można usunąć uprawnienia toocreate hello czynne uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="5fa04-234">Maska Hello *nie* dodać skuteczne toohello uprawnieniami.</span><span class="sxs-lookup"><span data-stu-id="5fa04-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="5fa04-235">Przyjrzyjmy się kilku przykładom.</span><span class="sxs-lookup"><span data-stu-id="5fa04-235">Let's look at some examples.</span></span> <span data-ttu-id="5fa04-236">W hello poniższy przykład, maska hello ustawiono zbyt**RWX**, co oznacza, że maska hello nie powoduje usunięcia żadnych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="5fa04-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="5fa04-237">Hello czynnych uprawnień hello o nazwie użytkownika, grupy będącej właścicielem, a o nazwie grupy nie zostały zmienione podczas sprawdzania dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="5fa04-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="5fa04-239">W hello poniższy przykład, maska hello ustawiono zbyt**R X**.</span><span class="sxs-lookup"><span data-stu-id="5fa04-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="5fa04-240">Oznacza to, że **wyłącza uprawnienia zapisu hello** dla **o nazwie użytkownika**, **grupy będącej właścicielem**, i **o nazwie grupy** w czasie hello dostępu Sprawdź.</span><span class="sxs-lookup"><span data-stu-id="5fa04-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="5fa04-242">Odwołanie w tym miejscu jest gdzie hello maska dla pliku lub folderu będzie wyświetlana w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa04-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="5fa04-244">Dla nowego konta usługi Data Lake Store, maskę hello hello dostępu i domyślne listy ACL hello głównego folderu ("/"), domyślnie przyjmowana tooRWX.</span><span class="sxs-lookup"><span data-stu-id="5fa04-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="5fa04-245">Uprawnienia do nowych plików i folderów</span><span class="sxs-lookup"><span data-stu-id="5fa04-245">Permissions on new files and folders</span></span>

<span data-ttu-id="5fa04-246">Gdy nowy plik lub folder utworzony na podstawie istniejącego folderu, określa hello domyślnej listy kontroli dostępu folderu nadrzędnego hello:</span><span class="sxs-lookup"><span data-stu-id="5fa04-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="5fa04-247">domyślną listę ACL i listę ACL dostępu folderu podrzędnego;</span><span class="sxs-lookup"><span data-stu-id="5fa04-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="5fa04-248">listę ACL dostępu pliku podrzędnego (pliki nie mają domyślnej listy ACL);</span><span class="sxs-lookup"><span data-stu-id="5fa04-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="5fa04-249">Witaj dostępu ACL podrzędnego pliku lub folderu</span><span class="sxs-lookup"><span data-stu-id="5fa04-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="5fa04-250">Po utworzeniu podrzędnego pliku lub folderu nadrzędnego hello domyślne ACL jest kopiowana jako hello dostępu ACL hello podrzędnego pliku lub folderu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="5fa04-251">Ponadto jeśli **innych** użytkownik ma uprawnienia RWX nadrzędnego hello domyślnej listy kontroli dostępu, zostanie ono usunięte z elementu podrzędnego hello dostępu ACL.</span><span class="sxs-lookup"><span data-stu-id="5fa04-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="5fa04-253">W większości przypadków informacje poprzednich hello są wszystkie potrzebne tooknow o jak element podrzędny dostępu ACL jest określana.</span><span class="sxs-lookup"><span data-stu-id="5fa04-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="5fa04-254">Jednak jeśli znasz POSIX systemów i chcesz toounderstand szczegółowe jak uzyskuje się tej transformacji, zobacz sekcję hello [umask — w roli w tworzeniu hello dostępu ACL dla nowych plików i folderów](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="5fa04-255">Domyślna lista ACL folderu podrzędnego</span><span class="sxs-lookup"><span data-stu-id="5fa04-255">A child folder's Default ACL</span></span>

<span data-ttu-id="5fa04-256">Po utworzeniu folderu podrzędnego w folderze nadrzędnym ACL domyślny folder nadrzędny hello jest kopiowana za pośrednictwem jest folder podrzędny toohello domyślne ACL.</span><span class="sxs-lookup"><span data-stu-id="5fa04-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="5fa04-258">Zaawansowane tematy związane z listami ACL w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5fa04-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="5fa04-259">Poniżej przedstawiono niektóre toohelp Tematy zaawansowane zrozumieć, jak listy kontroli dostępu są określone dla usługi Data Lake Store plików lub folderów.</span><span class="sxs-lookup"><span data-stu-id="5fa04-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="5fa04-260">Umask — w roli w tworzeniu hello dostępu ACL dla nowych plików i folderów</span><span class="sxs-lookup"><span data-stu-id="5fa04-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="5fa04-261">W systemie standardem POSIX, ogólnej koncepcji hello jest tego umask — 9-bitową wartość folderu nadrzędnego hello używanej tootransform hello uprawnienia dla **użytkownik będący właścicielem**, **grupy będącej właścicielem**, i  **inne** na powitania dostępu ACL podrzędnego nowego pliku lub folderu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="5fa04-262">bity Hello umask — określić które tooturn usługi bits poza hello podrzędny element dostępu ACL.</span><span class="sxs-lookup"><span data-stu-id="5fa04-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="5fa04-263">W związku z tym służy tooselectively zapobiec hello propagację uprawnień dla **użytkownik będący właścicielem**, **grupy będącej właścicielem**, i **innych**.</span><span class="sxs-lookup"><span data-stu-id="5fa04-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="5fa04-264">W systemie HDFS umask — Witaj jest zwykle w całym serwisie opcji konfiguracji, które są kontrolowane przez administratorów.</span><span class="sxs-lookup"><span data-stu-id="5fa04-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="5fa04-265">Usługa Data Lake Store używa **maski umask obejmującej całe konto**, której nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="5fa04-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="5fa04-266">Witaj w następującej tabeli przedstawiono hello maskowanie dla usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="5fa04-267">Grupa użytkowników</span><span class="sxs-lookup"><span data-stu-id="5fa04-267">User group</span></span>  | <span data-ttu-id="5fa04-268">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="5fa04-268">Setting</span></span> | <span data-ttu-id="5fa04-269">Wpływ na listę ACL dostępu nowego elementu podrzędnego</span><span class="sxs-lookup"><span data-stu-id="5fa04-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="5fa04-270">Użytkownik będący właścicielem</span><span class="sxs-lookup"><span data-stu-id="5fa04-270">Owning user</span></span> | ---     | <span data-ttu-id="5fa04-271">Brak wpływu</span><span class="sxs-lookup"><span data-stu-id="5fa04-271">No effect</span></span>                             |
| <span data-ttu-id="5fa04-272">Grupa będąca właścicielem</span><span class="sxs-lookup"><span data-stu-id="5fa04-272">Owning group</span></span>| ---     | <span data-ttu-id="5fa04-273">Brak wpływu</span><span class="sxs-lookup"><span data-stu-id="5fa04-273">No effect</span></span>                             |
| <span data-ttu-id="5fa04-274">Inne</span><span class="sxs-lookup"><span data-stu-id="5fa04-274">Other</span></span>       | <span data-ttu-id="5fa04-275">RWX</span><span class="sxs-lookup"><span data-stu-id="5fa04-275">RWX</span></span>     | <span data-ttu-id="5fa04-276">Usuwanie uprawnień do odczytu, zapisu, wykonania</span><span class="sxs-lookup"><span data-stu-id="5fa04-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="5fa04-277">Hello następującej ilustracji przedstawiono ten umask — w akcji.</span><span class="sxs-lookup"><span data-stu-id="5fa04-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="5fa04-278">Efekt netto Hello jest tooremove **odczytu i zapisu i wykonać** dla **innych** użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5fa04-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="5fa04-279">Ponieważ hello umask — nie określono bitów dla **użytkownik będący właścicielem** i **grupy będącej właścicielem**, te uprawnienia nie są przekształcane.</span><span class="sxs-lookup"><span data-stu-id="5fa04-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Listy ACL usługi Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="5fa04-281">bit trwałe Hello</span><span class="sxs-lookup"><span data-stu-id="5fa04-281">hello sticky bit</span></span>

<span data-ttu-id="5fa04-282">bit trwałe Hello jest bardziej zaawansowanych funkcji systemu plików POSIX.</span><span class="sxs-lookup"><span data-stu-id="5fa04-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="5fa04-283">W kontekście hello usługi Data Lake Store najprawdopodobniej tego bit trwałe hello będą potrzebne.</span><span class="sxs-lookup"><span data-stu-id="5fa04-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="5fa04-284">Witaj poniższej tabeli przedstawiono jak hello trwałe bitowa działa w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="5fa04-285">Grupa użytkowników</span><span class="sxs-lookup"><span data-stu-id="5fa04-285">User group</span></span>         | <span data-ttu-id="5fa04-286">Plik</span><span class="sxs-lookup"><span data-stu-id="5fa04-286">File</span></span>    | <span data-ttu-id="5fa04-287">Folder</span><span class="sxs-lookup"><span data-stu-id="5fa04-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="5fa04-288">Sticky bit **WYŁ.**</span><span class="sxs-lookup"><span data-stu-id="5fa04-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="5fa04-289">Brak wpływu</span><span class="sxs-lookup"><span data-stu-id="5fa04-289">No effect</span></span>   | <span data-ttu-id="5fa04-290">Brak wpływu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-290">No effect.</span></span>           |
| <span data-ttu-id="5fa04-291">Sticky bit **WŁ.**</span><span class="sxs-lookup"><span data-stu-id="5fa04-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="5fa04-292">Brak wpływu</span><span class="sxs-lookup"><span data-stu-id="5fa04-292">No effect</span></span>   | <span data-ttu-id="5fa04-293">Każda osoba, z wyjątkiem uniemożliwia **nadtypem użytkowników** i hello **użytkownik będący właścicielem** elementu podrzędnego, usuwanie lub zmiana nazwy elementu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="5fa04-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="5fa04-294">bit trwałe Hello nie jest wyświetlany w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5fa04-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="5fa04-295">Często zadawane pytania dotyczące list ACL w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5fa04-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="5fa04-296">Oto kilka często zadawanych pytań dotyczących list ACL w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="5fa04-297">Obsługa tooenable listy ACL są dostępne?</span><span class="sxs-lookup"><span data-stu-id="5fa04-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="5fa04-298">Nie.</span><span class="sxs-lookup"><span data-stu-id="5fa04-298">No.</span></span> <span data-ttu-id="5fa04-299">Kontrola dostępu za pośrednictwem list ACL jest zawsze włączona dla konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="5fa04-300">Jakie uprawnienia są wymagane toorecursively Usuń folder i jego zawartość?</span><span class="sxs-lookup"><span data-stu-id="5fa04-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="5fa04-301">folder nadrzędny Hello musi mieć **zapisu i wykonywania** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="5fa04-302">Witaj toobe folderu usunięte i wymaga każdego folderu, to **odczytu i zapisu i wykonać** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="5fa04-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="5fa04-303">Nie należy, uprawnienia do zapisu plików toodelete w folderach.</span><span class="sxs-lookup"><span data-stu-id="5fa04-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="5fa04-304">Ponadto hello folderu głównego "/" można **nigdy nie** można usunąć.</span><span class="sxs-lookup"><span data-stu-id="5fa04-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="5fa04-305">Kto jest właścicielem hello pliku lub folderu?</span><span class="sxs-lookup"><span data-stu-id="5fa04-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="5fa04-306">Twórca Hello pliku lub folderu staje się właścicielem hello.</span><span class="sxs-lookup"><span data-stu-id="5fa04-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="5fa04-307">Grupy, do której jest ustawiony jako hello-właściciel pliku lub folderu podczas tworzenia grupy?</span><span class="sxs-lookup"><span data-stu-id="5fa04-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="5fa04-308">Grupa będący właścicielem Hello jest kopiowana z hello-właściciel grupy hello folderu nadrzędnego, w których hello jest tworzony nowy plik lub folder.</span><span class="sxs-lookup"><span data-stu-id="5fa04-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="5fa04-309">Jestem hello użytkownik pliku będący właścicielem, ale nie mam hello RWX uprawnienia, które należy.</span><span class="sxs-lookup"><span data-stu-id="5fa04-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="5fa04-310">Co mam zrobić?</span><span class="sxs-lookup"><span data-stu-id="5fa04-310">What do I do?</span></span>

<span data-ttu-id="5fa04-311">Hello będący właścicielem użytkownik może zmienić uprawnień hello hello pliku toogive się żadnych uprawnień RWX, które są im potrzebne.</span><span class="sxs-lookup"><span data-stu-id="5fa04-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="5fa04-312">Podczas wyświetlania listy kontroli dostępu w portalu Azure hello widać nazwy użytkownika, ale za pośrednictwem interfejsów API, wyświetlane identyfikatory GUID, dlaczego?</span><span class="sxs-lookup"><span data-stu-id="5fa04-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="5fa04-313">Wpisy w hello listy ACL są przechowywane jako identyfikatory GUID, które odpowiadają toousers w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fa04-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="5fa04-314">Witaj interfejsów API zwraca hello identyfikatorów GUID, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="5fa04-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="5fa04-315">Witaj portalu Azure próbuje toouse łatwiejsze toomake listy ACL przez tłumaczenie hello identyfikatorów GUID do przyjaznych nazw, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="5fa04-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="5fa04-316">Dlaczego czasami wyświetlane identyfikatory GUID w listy ACL hello Kiedy używam hello portalu Azure?</span><span class="sxs-lookup"><span data-stu-id="5fa04-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="5fa04-317">Identyfikator GUID jest wyświetlany, jeśli użytkownik hello nie istnieje w usłudze Azure AD już.</span><span class="sxs-lookup"><span data-stu-id="5fa04-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="5fa04-318">Zazwyczaj dzieje się tak podczas hello użytkownik opuścił hello firmy lub jeśli ich konto zostało usunięte w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fa04-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="5fa04-319">Czy usługa Data Lake Store obsługuje dziedziczenie list ACL?</span><span class="sxs-lookup"><span data-stu-id="5fa04-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="5fa04-320">Nie.</span><span class="sxs-lookup"><span data-stu-id="5fa04-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="5fa04-321">Jaka jest różnica hello maski i umask —?</span><span class="sxs-lookup"><span data-stu-id="5fa04-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="5fa04-322">maska</span><span class="sxs-lookup"><span data-stu-id="5fa04-322">mask</span></span> | <span data-ttu-id="5fa04-323">maska umask</span><span class="sxs-lookup"><span data-stu-id="5fa04-323">umask</span></span>|
|------|------|
| <span data-ttu-id="5fa04-324">Witaj **maski** właściwość jest dostępna na każdym plików i folderów.</span><span class="sxs-lookup"><span data-stu-id="5fa04-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="5fa04-325">Witaj **umask —** jest właściwością hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="5fa04-326">To jest tylko jeden umask — hello usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5fa04-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="5fa04-327">może się zmienić właściwości mask Hello pliku lub folderu w hello będącej właścicielem, użytkownika lub grupy plików lub nadtypem użytkownika będącej właścicielem.</span><span class="sxs-lookup"><span data-stu-id="5fa04-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="5fa04-328">Nie można zmodyfikować właściwości umask — Witaj przez dowolnego użytkownika, nawet administratora.</span><span class="sxs-lookup"><span data-stu-id="5fa04-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="5fa04-329">Jest to niezmienna, stała wartość.</span><span class="sxs-lookup"><span data-stu-id="5fa04-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="5fa04-330">Właściwość maska Hello jest używany podczas algorytmu sprawdzania dostępu hello na toodetermine środowiska uruchomieniowego, czy użytkownik ma prawo tooperform hello na operacji na pliku lub folderu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="5fa04-331">Rola Hello maski hello jest toocreate "czynnych uprawnień" w czasie hello kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="5fa04-332">umask — Witaj nie jest używany podczas sprawdzania dostępu w ogóle.</span><span class="sxs-lookup"><span data-stu-id="5fa04-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="5fa04-333">umask — Hello jest używany toodetermine hello dostępu ACL nowych elementów podrzędnych folderu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="5fa04-334">Maska Hello jest 3-bitową wartość RWX, która dotyczy użytkownika toonamed, nazwaną grupę i będący właścicielem użytkownika w czasie hello kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="5fa04-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="5fa04-335">Witaj umask — jest wartość 9-bitowego, która dotyczy toohello będącej właścicielem, jeśli użytkownik będący właścicielem grupy, a **innych** nowego elementu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="5fa04-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="5fa04-336">Gdzie można dowiedzieć się więcej na temat modelu kontroli dostępu POSIX?</span><span class="sxs-lookup"><span data-stu-id="5fa04-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="5fa04-337">Listy kontroli dostępu w modelu POSIX w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="5fa04-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="5fa04-338">Przewodnik po uprawnieniach systemu plików HDFS</span><span class="sxs-lookup"><span data-stu-id="5fa04-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="5fa04-339">POSIX — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="5fa04-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="5fa04-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="5fa04-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="5fa04-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="5fa04-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="5fa04-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="5fa04-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="5fa04-343">Listy ACL modelu POSIX w systemie Ubuntu</span><span class="sxs-lookup"><span data-stu-id="5fa04-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="5fa04-344">Listy ACL korzystające z list kontroli dostępu w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="5fa04-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="5fa04-345">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5fa04-345">See also</span></span>

* [<span data-ttu-id="5fa04-346">Omówienie usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5fa04-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
