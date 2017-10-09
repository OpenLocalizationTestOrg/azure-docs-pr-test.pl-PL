---
title: "krok aaaGeneric krok przez łącznik usług SQL | Dokumentacja firmy Microsoft"
description: "W tym artykule jest przedstawienie za pomocą prostego systemu HR krok po kroku przy użyciu hello ogólny Łącznik usług SQL."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="6b211-103">Instrukcja krok po kroku dotycząca ogólnego łącznika SQL</span><span class="sxs-lookup"><span data-stu-id="6b211-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="6b211-104">Ten temat jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="6b211-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="6b211-105">Tworzy HR proste przykładową bazę danych i używać go do importowania niektórym użytkownikom i ich członkostwa w grupie.</span><span class="sxs-lookup"><span data-stu-id="6b211-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="6b211-106">Przygotowanie hello przykładowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="6b211-106">Prepare hello sample database</span></span>
<span data-ttu-id="6b211-107">Na serwerze z uruchomionym programem SQL Server, uruchom skrypt SQL hello w [dodatek a.](#appendix-a). Ten skrypt tworzy przykładowa baza danych o nazwie hello GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="6b211-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="6b211-108">Witaj model obiektów dla hello utworzone bazy danych prawdopodobnie tego obrazu:</span><span class="sxs-lookup"><span data-stu-id="6b211-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="6b211-109">![Model obiektu](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="6b211-110">Utwórz również użytkownika ma toouse tooconnect toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6b211-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="6b211-111">W tym przewodniku hello użytkownik o nazwie FABRIKAM\SQLUser i znajduje się w domenie hello.</span><span class="sxs-lookup"><span data-stu-id="6b211-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="6b211-112">Tworzenie pliku połączenia ODBC hello</span><span class="sxs-lookup"><span data-stu-id="6b211-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="6b211-113">Hello ogólny Łącznik usług SQL korzysta z serwera zdalnego toohello tooconnect ODBC.</span><span class="sxs-lookup"><span data-stu-id="6b211-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="6b211-114">Najpierw musimy toocreate plik o hello informacje dotyczące połączenia ODBC.</span><span class="sxs-lookup"><span data-stu-id="6b211-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="6b211-115">Uruchom narzędzie do zarządzania ODBC hello na serwerze:</span><span class="sxs-lookup"><span data-stu-id="6b211-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="6b211-117">Witaj wybierz kartę **pliku DSN**.</span><span class="sxs-lookup"><span data-stu-id="6b211-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="6b211-118">Kliknij przycisk **Dodaj...** .</span><span class="sxs-lookup"><span data-stu-id="6b211-118">Click **Add...**.</span></span>  
   <span data-ttu-id="6b211-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="6b211-120">Witaj działa sterownik out-of-box drobne, więc zaznacz go i kliknij **Dalej >**.</span><span class="sxs-lookup"><span data-stu-id="6b211-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="6b211-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="6b211-122">Określ plik hello nazwę, takich jak **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="6b211-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="6b211-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="6b211-124">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6b211-124">Click **Finish**.</span></span>  
   <span data-ttu-id="6b211-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="6b211-126">Połączenia hello tooconfigure czasu.</span><span class="sxs-lookup"><span data-stu-id="6b211-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="6b211-127">Nadaj hello źródła danych czytelny opis, a następnie podaj nazwę hello powitania serwera z uruchomionym programem SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6b211-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="6b211-129">Wybierz jak tooauthenticate z SQL.</span><span class="sxs-lookup"><span data-stu-id="6b211-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="6b211-130">W takim przypadku stosujemy uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="6b211-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="6b211-132">Podaj nazwę hello hello przykładowej bazy danych, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="6b211-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="6b211-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="6b211-134">Zachowaj domyślne wszystko na tym ekranie.</span><span class="sxs-lookup"><span data-stu-id="6b211-134">Keep everything default on this screen.</span></span> <span data-ttu-id="6b211-135">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6b211-135">Click **Finish**.</span></span>  
   <span data-ttu-id="6b211-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="6b211-137">tooverify wszystko działa zgodnie z oczekiwaniami, kliknij przycisk **Testuj źródło danych**.</span><span class="sxs-lookup"><span data-stu-id="6b211-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="6b211-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="6b211-139">Upewnij się, że hello test zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6b211-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="6b211-141">plik konfiguracji ODBC Hello teraz powinny być widoczne w pliku DSN.</span><span class="sxs-lookup"><span data-stu-id="6b211-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="6b211-143">Mamy teraz plik hello możemy muszą i może rozpocząć tworzenie hello łącznika.</span><span class="sxs-lookup"><span data-stu-id="6b211-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="6b211-144">Utwórz hello ogólny Łącznik usług SQL</span><span class="sxs-lookup"><span data-stu-id="6b211-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="6b211-145">Hello interfejsu użytkownika Menedżera usługi synchronizacji, wybierz **łączniki** i **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6b211-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="6b211-146">Wybierz **ogólnego SQL (Microsoft)** i nadaj mu nazwę opisową.</span><span class="sxs-lookup"><span data-stu-id="6b211-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="6b211-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="6b211-148">Znajdź plik DSN hello, który został utworzony w poprzedniej sekcji hello i przekaż go toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="6b211-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="6b211-149">Podaj hello poświadczenia tooconnect toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6b211-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="6b211-151">W tym przewodniku, to aby ułatwić firmie Microsoft firma Microsoft i powiedzieć, że istnieją dwa typy obiektów, **użytkownika** i **grupy**.</span><span class="sxs-lookup"><span data-stu-id="6b211-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="6b211-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="6b211-153">atrybuty hello toofind, chcemy hello toodetect łącznika te atrybuty analizując hello samej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6b211-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="6b211-154">Ponieważ **użytkowników** jest słowem zastrzeżonym SQL, potrzebujemy tooprovide w kwadratowe nawiasy kwadratowe [].</span><span class="sxs-lookup"><span data-stu-id="6b211-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="6b211-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="6b211-156">Czas toodefine hello zakotwiczenia atrybut i atrybut DN hello.</span><span class="sxs-lookup"><span data-stu-id="6b211-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="6b211-157">Aby uzyskać **użytkowników**, możemy użyć kombinacji hello hello dwa atrybuty username i identyfikator pracownika.</span><span class="sxs-lookup"><span data-stu-id="6b211-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="6b211-158">Dla **grupy**, używamy, Nazwa_grupy (nie realistyczne w rzeczywistych, ale w ramach tego przewodnika działa).</span><span class="sxs-lookup"><span data-stu-id="6b211-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="6b211-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="6b211-160">Nie wszystkie typy atrybutów, można wykryć w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="6b211-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="6b211-161">w szczególności nie Hello odwołanie do atrybutu typu.</span><span class="sxs-lookup"><span data-stu-id="6b211-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="6b211-162">Typ obiektu grupy hello potrzebujemy toochange hello OwnerID i MemberID tooreference.</span><span class="sxs-lookup"><span data-stu-id="6b211-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="6b211-164">atrybuty Hello Wybraliśmy atrybuty odwołania w poprzednim kroku hello wymagać hello typ obiektu, który te wartości są odwołania do.</span><span class="sxs-lookup"><span data-stu-id="6b211-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="6b211-165">W tym przypadku hello typ obiektu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6b211-165">In our case, hello User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="6b211-167">Na stronie powitania parametry globalne zaznacz **znaku wodnego** jako hello strategii delta.</span><span class="sxs-lookup"><span data-stu-id="6b211-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="6b211-168">Także wpisać w formacie daty/godziny hello **RRRR MM-dd gg**.</span><span class="sxs-lookup"><span data-stu-id="6b211-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="6b211-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="6b211-170">Na powitania **Konfiguruj partycje i hierarchie** wybierz oba typy obiektów.</span><span class="sxs-lookup"><span data-stu-id="6b211-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="6b211-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="6b211-172">Na powitania **wybierz typy obiektów** i **wybierz atrybuty**, zaznacz typy obiektów i wszystkich atrybutów.</span><span class="sxs-lookup"><span data-stu-id="6b211-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="6b211-173">Na powitania **Konfiguruj zakotwiczenia** kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6b211-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="6b211-174">Tworzenie profilów uruchamiania</span><span class="sxs-lookup"><span data-stu-id="6b211-174">Create Run Profiles</span></span>
1. <span data-ttu-id="6b211-175">Hello interfejsu użytkownika Menedżera usługi synchronizacji, wybierz **łączniki**, i **Konfigurowanie profilów uruchamiania**.</span><span class="sxs-lookup"><span data-stu-id="6b211-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="6b211-176">Kliknij przycisk **nowy profil**.</span><span class="sxs-lookup"><span data-stu-id="6b211-176">Click **New Profile**.</span></span> <span data-ttu-id="6b211-177">Możemy zaczynać **pełny Import**.</span><span class="sxs-lookup"><span data-stu-id="6b211-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="6b211-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="6b211-179">Wybierz typ hello **pełny Import (tylko etap)**.</span><span class="sxs-lookup"><span data-stu-id="6b211-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="6b211-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="6b211-181">Wybierz partycję hello **obiektu = użytkownik**.</span><span class="sxs-lookup"><span data-stu-id="6b211-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="6b211-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="6b211-183">Wybierz **tabeli** i typ **[użytkownicy]**.</span><span class="sxs-lookup"><span data-stu-id="6b211-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="6b211-184">Przewiń w dół toohello wielowartościowe obiektu typu sekcji, a następnie wprowadź dane hello tak jak na poniższej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="6b211-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="6b211-185">Wybierz **Zakończ** toosave hello kroku.</span><span class="sxs-lookup"><span data-stu-id="6b211-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="6b211-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="6b211-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="6b211-188">Wybierz **nowy krok**.</span><span class="sxs-lookup"><span data-stu-id="6b211-188">Select **New Step**.</span></span> <span data-ttu-id="6b211-189">Teraz, wybierz opcję **obiektu = grupy**.</span><span class="sxs-lookup"><span data-stu-id="6b211-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="6b211-190">Na ostatniej stronie powitania Użyj konfiguracji hello jak hello poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="6b211-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="6b211-191">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6b211-191">Click **Finish**.</span></span>  
   <span data-ttu-id="6b211-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="6b211-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="6b211-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="6b211-194">Opcjonalnie: Jeśli chcesz, można skonfigurować dodatkowe profile uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="6b211-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="6b211-195">W ramach tego przewodnika hello pełny Import jest używany.</span><span class="sxs-lookup"><span data-stu-id="6b211-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="6b211-196">Kliknij przycisk **OK** toofinish zmienianie profilów uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="6b211-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="6b211-197">Dodać niektóre importu hello testu, jak dane i testu</span><span class="sxs-lookup"><span data-stu-id="6b211-197">Add some test data and test hello import</span></span>
<span data-ttu-id="6b211-198">Wprowadź dane testowe w przykładowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6b211-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="6b211-199">Gdy wszystko będzie gotowe, wybierz **Uruchom** i **pełny import**.</span><span class="sxs-lookup"><span data-stu-id="6b211-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="6b211-200">Oto użytkownika z dwóch numery telefonów i grupy z niektóre elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="6b211-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="6b211-203">Dodatek A</span><span class="sxs-lookup"><span data-stu-id="6b211-203">Appendix A</span></span>
<span data-ttu-id="6b211-204">**Skrypt toocreate hello przykładowa baza danych SQL**</span><span class="sxs-lookup"><span data-stu-id="6b211-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
