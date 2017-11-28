---
<span data-ttu-id="4965b-101">title: aaa "lekcji samouczka usług Azure Analysis Services 11: tworzyć role | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate ról w hello projekt samouczka usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="4965b-101">title: aaa"Azure Analysis Services tutorial lesson 11: Create roles | Microsoft Docs" description: Describes how toocreate roles in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="4965b-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="4965b-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="4965b-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="4965b-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-11-create-roles"></a><span data-ttu-id="4965b-104">Lekcja 11. Tworzenie ról</span><span class="sxs-lookup"><span data-stu-id="4965b-104">Lesson 11: Create roles</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="4965b-105">W tej lekcji utworzysz role.</span><span class="sxs-lookup"><span data-stu-id="4965b-105">In this lesson, you create roles.</span></span> <span data-ttu-id="4965b-106">Role zawierają modelu zabezpieczeń danych i obiektów bazy danych przez ograniczenie tooonly dostęp do tych użytkowników, którzy są członkami roli.</span><span class="sxs-lookup"><span data-stu-id="4965b-106">Roles provide model database object and data security by limiting access tooonly those users that are role members.</span></span> <span data-ttu-id="4965b-107">Każda rola jest zdefiniowana z jednym uprawnieniem: Brak, Odczyt, Odczyt i przetwarzanie, Przetwarzanie lub Administrator.</span><span class="sxs-lookup"><span data-stu-id="4965b-107">Each role is defined with a single permission: None, Read, Read and Process, Process, or Administrator.</span></span> <span data-ttu-id="4965b-108">Role można zdefiniować podczas tworzenia modelu przy użyciu menedżera ról.</span><span class="sxs-lookup"><span data-stu-id="4965b-108">Roles can be defined during model authoring by using Role Manager.</span></span> <span data-ttu-id="4965b-109">Po wdrożeniu modelu rolami można zarządzać przy użyciu programu SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="4965b-109">After a model has been deployed, you can manage roles by using SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="4965b-110">toolearn więcej, zobacz [ról](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="4965b-110">toolearn more, see [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).</span></span>
  
> [!NOTE]  
> <span data-ttu-id="4965b-111">Tworzenie ról jest toocomplete nie jest konieczna w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="4965b-111">Creating roles is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="4965b-112">Domyślnie konto hello, które są obecnie zalogowani przy użyciu ma uprawnienia administratora na powitania modelu.</span><span class="sxs-lookup"><span data-stu-id="4965b-112">By default, hello account you are currently logged in with has Administrator privileges on hello model.</span></span> <span data-ttu-id="4965b-113">Jednak dla innych użytkowników w Twojej organizacji toobrowse przy użyciu klienta raportowania, należy utworzyć co najmniej jedną rolę z odczytu uprawnienia i Dodaj tych użytkowników jako elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="4965b-113">However, for other users in your organization toobrowse by using a reporting client, you must create at least one role with Read permissions and add those users as members.</span></span>  
  
<span data-ttu-id="4965b-114">Utworzysz trzy role:</span><span class="sxs-lookup"><span data-stu-id="4965b-114">You create three roles:</span></span>  
  
-   <span data-ttu-id="4965b-115">**Kierownik** — ta rola może zawierać użytkowników w organizacji, dla której ma zostać toohave odczytu uprawnień tooall modelu obiektów i danych.</span><span class="sxs-lookup"><span data-stu-id="4965b-115">**Sales Manager** – This role can include users in your organization for which you want toohave Read permission tooall model objects and data.</span></span>  
  
-   <span data-ttu-id="4965b-116">**Analityk sprzedaży USA** — tej roli można dołączyć użytkowników w organizacji, dla którego chcesz tylko dane o stanie toobrowse toobe powiązane toosales w hello Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="4965b-116">**Sales Analyst US** – This role can include users in your organization for which you want only toobe able toobrowse data related toosales in hello United States.</span></span> <span data-ttu-id="4965b-117">Dla tej roli, możesz użyć toodefine formuły języka DAX *Filtr wierszy*, co ogranicza liczbę elementów członkowskich danych toobrowse tylko w przypadku hello Stanów Zjednoczonych.</span><span class="sxs-lookup"><span data-stu-id="4965b-117">For this role, you use a DAX formula toodefine a *Row Filter*, which restricts members toobrowse data only for hello United States.</span></span>  
  
-   <span data-ttu-id="4965b-118">**Administrator** — ta rola może zawierać użytkowników, dla których mają uprawnienia administratora toohave, dzięki czemu nieograniczonego dostępu i uprawnienia tooperform zadań administracyjnych na powitania bazy danych modelu.</span><span class="sxs-lookup"><span data-stu-id="4965b-118">**Administrator** – This role can include users for which you want toohave Administrator permission, which allows unlimited access and permissions tooperform administrative tasks on hello model database.</span></span>  
  
<span data-ttu-id="4965b-119">Ponieważ kont użytkowników i grup systemu Windows w Twojej organizacji są unikatowe, można dodać konta z toomembers Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="4965b-119">Because Windows user and group accounts in your organization are unique, you can add accounts from your particular organization toomembers.</span></span> <span data-ttu-id="4965b-120">Jednak w tym samouczku, można również puste elementy członkowskie hello.</span><span class="sxs-lookup"><span data-stu-id="4965b-120">However, for this tutorial, you can also leave hello members blank.</span></span> <span data-ttu-id="4965b-121">Testowanie wpływu hello każdej roli w dalszej części lekcji 12: analizować w programie Excel.</span><span class="sxs-lookup"><span data-stu-id="4965b-121">You test hello effect of each role later in Lesson 12: Analyze in Excel.</span></span>  
  
<span data-ttu-id="4965b-122">Szacowany czas toocomplete tej lekcji: **15 minut**</span><span class="sxs-lookup"><span data-stu-id="4965b-122">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="4965b-123">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4965b-123">Prerequisites</span></span>  
<span data-ttu-id="4965b-124">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="4965b-124">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="4965b-125">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [10 lekcji: tworzenie partycji](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="4965b-125">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span>  
  
## <a name="create-roles"></a><span data-ttu-id="4965b-126">Tworzenie ról</span><span class="sxs-lookup"><span data-stu-id="4965b-126">Create roles</span></span>  
  
#### <a name="toocreate-a-sales-manager-user-role"></a><span data-ttu-id="4965b-127">toocreate roli użytkownika Menedżer sprzedaży</span><span class="sxs-lookup"><span data-stu-id="4965b-127">toocreate a Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="4965b-128">W Eksploratorze modelu tabelarycznego kliknij prawym przyciskiem myszy pozycje **Role** > **Role**.</span><span class="sxs-lookup"><span data-stu-id="4965b-128">In Tabular Model Explorer, right-click **Roles** > **Roles**.</span></span>  
  
2.  <span data-ttu-id="4965b-129">W Menedżerze ról kliknij przycisk **Nowa**.</span><span class="sxs-lookup"><span data-stu-id="4965b-129">In Role Manager, click **New**.</span></span>  
  
3.  <span data-ttu-id="4965b-130">Kliknij hello nową rolę, a następnie w hello **nazwa** kolumny, Zmień nazwę roli hello zbyt**Menedżer sprzedaży**.</span><span class="sxs-lookup"><span data-stu-id="4965b-130">Click hello new role, and then in hello **Name** column, rename hello role too**Sales Manager**.</span></span>  
  
4.  <span data-ttu-id="4965b-131">W hello **uprawnienia** kolumny, kliknij listę rozwijaną hello, a następnie wybierz hello **odczytu** uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="4965b-131">In hello **Permissions** column, click hello dropdown list, and then select hello **Read** permission.</span></span> 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  <span data-ttu-id="4965b-133">Opcjonalnie: Kliknij hello **członków** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="4965b-133">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="4965b-134">W hello **Wybieranie użytkowników lub grup** okna dialogowego wprowadź użytkowników systemu Windows hello lub grup z Twojej organizacji mają tooinclude hello roli.</span><span class="sxs-lookup"><span data-stu-id="4965b-134">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a><span data-ttu-id="4965b-135">toocreate rolę użytkownika Analityk sprzedaży stany USA</span><span class="sxs-lookup"><span data-stu-id="4965b-135">toocreate a Sales Analyst US user role</span></span>  
  
1.  <span data-ttu-id="4965b-136">W Menedżerze ról kliknij przycisk **Nowa**.</span><span class="sxs-lookup"><span data-stu-id="4965b-136">In Role Manager, click **New**.</span></span>    
  
2.  <span data-ttu-id="4965b-137">Zmień nazwę roli hello zbyt**analityka sprzedaży USA**.</span><span class="sxs-lookup"><span data-stu-id="4965b-137">Rename hello role too**Sales Analyst US**.</span></span>  
  
3.  <span data-ttu-id="4965b-138">Nadaj tej roli uprawnienie **Odczyt**.</span><span class="sxs-lookup"><span data-stu-id="4965b-138">Give this role **Read** permission.</span></span>  
  
4.  <span data-ttu-id="4965b-139">Kliknij kartę filtrów wierszy hello, a następnie hello **DimGeography** tabeli, kolumny filtru DAX hello, hello typu następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="4965b-139">Click hello Row Filters tab, and then for hello **DimGeography** table only, in hello DAX Filter column, type hello following formula:</span></span>  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    <span data-ttu-id="4965b-140">Filtr wierszy A formuła musi rozpoznać tooa wartość logiczna (PRAWDA/FAŁSZ).</span><span class="sxs-lookup"><span data-stu-id="4965b-140">A Row Filter formula must resolve tooa Boolean (TRUE/FALSE) value.</span></span> <span data-ttu-id="4965b-141">Tą formułą jest określenie, czy użytkownik toohello widoczne tylko wiersze z hello wartość numer kierunkowy kraju Region "PL".</span><span class="sxs-lookup"><span data-stu-id="4965b-141">With this formula, you are specifying that only rows with hello Country Region Code value of “US” are visible toohello user.</span></span>  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  <span data-ttu-id="4965b-143">Opcjonalnie: Kliknij hello **członków** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="4965b-143">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="4965b-144">W hello **Wybieranie użytkowników lub grup** okna dialogowego wprowadź użytkowników systemu Windows hello lub grup z Twojej organizacji mają tooinclude hello roli.</span><span class="sxs-lookup"><span data-stu-id="4965b-144">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span>  
  
#### <a name="toocreate-an-administrator-user-role"></a><span data-ttu-id="4965b-145">toocreate roli użytkownika Administrator</span><span class="sxs-lookup"><span data-stu-id="4965b-145">toocreate an Administrator user role</span></span>  
  
1.  <span data-ttu-id="4965b-146">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="4965b-146">Click **New**.</span></span>  
  
2.  <span data-ttu-id="4965b-147">Zmień nazwę roli hello zbyt**administratora**.</span><span class="sxs-lookup"><span data-stu-id="4965b-147">Rename hello role too**Administrator**.</span></span>  
  
3.  <span data-ttu-id="4965b-148">Nadaj tej roli uprawnienie **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="4965b-148">Give this role **Administrator** permission.</span></span>  
  
4.  <span data-ttu-id="4965b-149">Opcjonalnie: Kliknij hello **członków** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="4965b-149">Optional: Click hello **Members** tab, and then click **Add**.</span></span> <span data-ttu-id="4965b-150">W hello **Wybieranie użytkowników lub grup** okna dialogowego wprowadź użytkowników systemu Windows hello lub grup z Twojej organizacji mają tooinclude hello roli.</span><span class="sxs-lookup"><span data-stu-id="4965b-150">In hello **Select Users or Groups** dialog box, enter hello Windows users or groups from your organization you want tooinclude in hello role.</span></span> 
  
  
## <a name="whats-next"></a><span data-ttu-id="4965b-151">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="4965b-151">What's next?</span></span>
<span data-ttu-id="4965b-152">[Lekcja 12. Analiza w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="4965b-152">[Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>

  
  
