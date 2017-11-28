---
title: "Ogólny Łącznik usług SQL krok po kroku | Dokumentacja firmy Microsoft"
description: "W tym artykule jest Instruktaż prosty system HR krok po kroku przy użyciu ogólny łącznik SQL."
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
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="7a6f4-103">Instrukcja krok po kroku dotycząca ogólnego łącznika SQL</span><span class="sxs-lookup"><span data-stu-id="7a6f4-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="7a6f4-104">Ten temat jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="7a6f4-105">Tworzy HR proste przykładową bazę danych i używać go do importowania niektórym użytkownikom i ich członkostwa w grupie.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="7a6f4-106">Przygotowanie przykładowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="7a6f4-106">Prepare the sample database</span></span>
<span data-ttu-id="7a6f4-107">Na serwerze z uruchomionym programem SQL Server, uruchom skrypt SQL znaleziono [dodatek a.](#appendix-a). Ten skrypt tworzy przykładowa baza danych o nazwie GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="7a6f4-108">Model obiektów dla bazy danych utworzonej wygląda tego obrazu:</span><span class="sxs-lookup"><span data-stu-id="7a6f4-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="7a6f4-109">![Model obiektu](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="7a6f4-110">Również utworzyć użytkownika, którego chcesz używać do łączenia z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="7a6f4-111">W tym przewodniku użytkownik jest nazywany FABRIKAM\SQLUser i znajduje się w domenie.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="7a6f4-112">Tworzenie pliku połączenia ODBC</span><span class="sxs-lookup"><span data-stu-id="7a6f4-112">Create the ODBC connection file</span></span>
<span data-ttu-id="7a6f4-113">Ogólny łącznik SQL używa ODBC do łączenia się z serwerem zdalnym.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="7a6f4-114">Najpierw należy utworzyć plik z informacjami o połączenia ODBC.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="7a6f4-115">Uruchom narzędzie zarządzania ODBC na serwerze:</span><span class="sxs-lookup"><span data-stu-id="7a6f4-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="7a6f4-117">Wybierz kartę **pliku DSN**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="7a6f4-118">Kliknij przycisk **Dodaj...** .</span><span class="sxs-lookup"><span data-stu-id="7a6f4-118">Click **Add...**.</span></span>  
   <span data-ttu-id="7a6f4-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="7a6f4-120">Działania sterownika out-of-box drobne, więc zaznacz go i kliknij **Dalej >**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="7a6f4-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="7a6f4-122">Określ plik nazwę, taką jak **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="7a6f4-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="7a6f4-124">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-124">Click **Finish**.</span></span>  
   <span data-ttu-id="7a6f4-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="7a6f4-126">Czas, aby skonfigurować połączenie.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-126">Time to configure the connection.</span></span> <span data-ttu-id="7a6f4-127">Nadaj źródła danych czytelny opis, a następnie podaj nazwę serwera z uruchomionym programem SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="7a6f4-129">Wybierz sposób uwierzytelniania SQL.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="7a6f4-130">W takim przypadku stosujemy uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="7a6f4-132">Podaj nazwę przykładowej bazy danych, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="7a6f4-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="7a6f4-134">Zachowaj domyślne wszystko na tym ekranie.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-134">Keep everything default on this screen.</span></span> <span data-ttu-id="7a6f4-135">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-135">Click **Finish**.</span></span>  
   <span data-ttu-id="7a6f4-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="7a6f4-137">Aby sprawdzić, wszystko działa zgodnie z oczekiwaniami, kliknij przycisk **Testuj źródło danych**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="7a6f4-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="7a6f4-139">Upewnij się, że test zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="7a6f4-141">Powinno być teraz widoczne w pliku DSN ODBC pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="7a6f4-143">Mamy teraz plik możemy muszą i może rozpocząć tworzenie łącznika.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="7a6f4-144">Tworzenie łącznika ogólnego SQL</span><span class="sxs-lookup"><span data-stu-id="7a6f4-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="7a6f4-145">W Interfejsie użytkownika Menedżera usługi synchronizacji, wybierz **łączniki** i **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="7a6f4-146">Wybierz **ogólnego SQL (Microsoft)** i nadaj mu nazwę opisową.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="7a6f4-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="7a6f4-148">Znajdź plik DSN, który został utworzony w poprzedniej sekcji, a następnie przekaż go do serwera.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="7a6f4-149">Podaj poświadczenia do połączenia z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-149">Provide the credentials to connect to the database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="7a6f4-151">W tym przewodniku, to aby ułatwić firmie Microsoft firma Microsoft i powiedzieć, że istnieją dwa typy obiektów, **użytkownika** i **grupy**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="7a6f4-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="7a6f4-153">W celu znalezienia atrybutów, chcemy łącznik, aby wykryć te atrybuty analizując samej tabeli.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="7a6f4-154">Ponieważ **użytkowników** jest słowem zastrzeżonym SQL, należy podać go w nawiasy kwadratowe [].</span><span class="sxs-lookup"><span data-stu-id="7a6f4-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="7a6f4-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="7a6f4-156">Czas do definiowania atrybutu zakotwiczenia i atrybut nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="7a6f4-157">Aby uzyskać **użytkowników**, używamy kombinacja nazwy użytkownika dwa atrybuty i identyfikator pracownika.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="7a6f4-158">Dla **grupy**, używamy, Nazwa_grupy (nie realistyczne w rzeczywistych, ale w ramach tego przewodnika działa).</span><span class="sxs-lookup"><span data-stu-id="7a6f4-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="7a6f4-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="7a6f4-160">Nie wszystkie typy atrybutów, można wykryć w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="7a6f4-161">W szczególności nie odwołania typu atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="7a6f4-162">Dla typu obiektu grupy należy zmienić OwnerID i MemberID ma dotyczyć odwołanie.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="7a6f4-164">Atrybuty, które jako typ obiektu wymagają atrybutów odwołania w poprzednim kroku wybrano te wartości są odwołania do.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="7a6f4-165">W tym przypadku typ obiektu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-165">In our case, the User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="7a6f4-167">Na stronie parametry globalne wybierz **znaku wodnego** jako strategii delta.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="7a6f4-168">Także wpisać w formacie daty/godziny **RRRR MM-dd gg**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="7a6f4-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="7a6f4-170">Na **Konfiguruj partycje i hierarchie** wybierz oba typy obiektów.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="7a6f4-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="7a6f4-172">Na **wybierz typy obiektów** i **wybierz atrybuty**, zaznacz typy obiektów i wszystkich atrybutów.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="7a6f4-173">Na **Konfiguruj zakotwiczenia** kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="7a6f4-174">Tworzenie profilów uruchamiania</span><span class="sxs-lookup"><span data-stu-id="7a6f4-174">Create Run Profiles</span></span>
1. <span data-ttu-id="7a6f4-175">W Interfejsie użytkownika Menedżera usługi synchronizacji, wybierz **łączniki**, i **Konfigurowanie profilów uruchamiania**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="7a6f4-176">Kliknij przycisk **nowy profil**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-176">Click **New Profile**.</span></span> <span data-ttu-id="7a6f4-177">Możemy zaczynać **pełny Import**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="7a6f4-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="7a6f4-179">Wybierz typ **pełny Import (tylko etap)**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="7a6f4-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="7a6f4-181">Wybierz partycję **obiektu = użytkownik**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="7a6f4-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="7a6f4-183">Wybierz **tabeli** i typ **[użytkownicy]**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="7a6f4-184">Przewiń w dół do sekcji Typ obiektu wielowartościowe, a następnie wprowadź dane, tak jak na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="7a6f4-185">Wybierz **Zakończ** pominąć krok.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="7a6f4-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="7a6f4-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="7a6f4-188">Wybierz **nowy krok**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-188">Select **New Step**.</span></span> <span data-ttu-id="7a6f4-189">Teraz, wybierz opcję **obiektu = grupy**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="7a6f4-190">Na ostatniej stronie należy użyć konfiguracji, tak jak na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="7a6f4-191">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-191">Click **Finish**.</span></span>  
   <span data-ttu-id="7a6f4-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="7a6f4-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="7a6f4-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="7a6f4-194">Opcjonalnie: Jeśli chcesz, można skonfigurować dodatkowe profile uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="7a6f4-195">W ramach tego przewodnika jest używany tylko pełny Import.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="7a6f4-196">Kliknij przycisk **OK** aby zakończyć zmianę profile uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="7a6f4-197">Dodaj dane testowe i testowania importu</span><span class="sxs-lookup"><span data-stu-id="7a6f4-197">Add some test data and test the import</span></span>
<span data-ttu-id="7a6f4-198">Wprowadź dane testowe w przykładowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="7a6f4-199">Gdy wszystko będzie gotowe, wybierz **Uruchom** i **pełny import**.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="7a6f4-200">Oto użytkownika z dwóch numery telefonów i grupy z niektóre elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="7a6f4-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="7a6f4-203">Dodatek A</span><span class="sxs-lookup"><span data-stu-id="7a6f4-203">Appendix A</span></span>
<span data-ttu-id="7a6f4-204">**Skrypt SQL w celu utworzenia przykładowej bazy danych**</span><span class="sxs-lookup"><span data-stu-id="7a6f4-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
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
