---
title: dane osobowe aaaManage na platformie Microsoft Azure | Dokumentacja firmy Microsoft
description: "wskazówki dotyczące jak toocorrect, aktualizowanie, usuwanie i eksportowanie danych osobowych w usłudze Azure Active Directory i bazy danych SQL Azure"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="af9e0-103">Zarządzanie danych osobowych w Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="af9e0-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="af9e0-104">Ten artykuł zawiera wskazówki dotyczące jak toocorrect, aktualizowanie, usuwanie i eksportowanie danych osobowych w usłudze Azure Active Directory i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="af9e0-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="af9e0-105">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="af9e0-105">Scenario</span></span>

<span data-ttu-id="af9e0-106">Na podstawie Dublin firmę kompleksowych zakup Śluby docelowego górną granicę w Irlandii i wokół Witaj świecie bazy klientów lokalnych i międzynarodowe.</span><span class="sxs-lookup"><span data-stu-id="af9e0-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="af9e0-107">Mają one oddziałów, klientów, pracowników i dostawców znajdujących się wokół systemu hello world toofully usługi hello miejsc oferują.</span><span class="sxs-lookup"><span data-stu-id="af9e0-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="af9e0-108">Wśród wielu innych elementów firmy hello przechowuje informacje o zbędne obejmujących alergii żywności i ustalenia preferencji.</span><span class="sxs-lookup"><span data-stu-id="af9e0-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="af9e0-109">Goście wesele można zarejestrować dla różnych działań, takich jak horseback jazda, przeglądania, łodzi było itp. i nawet współdziałać ze sobą na stronie sieci web centralnej w miesiącach hello doprowadziły toohello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="af9e0-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="af9e0-110">firmy Hello zbiera dane osobowe z pracowników, dostawców, klientów i wesele gości.</span><span class="sxs-lookup"><span data-stu-id="af9e0-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="af9e0-111">Ze względu na powitania międzynarodowe rodzaj hello firm hello firmy muszą być zgodne z różnych poziomach rozporządzenia.</span><span class="sxs-lookup"><span data-stu-id="af9e0-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="af9e0-112">Opis problemu</span><span class="sxs-lookup"><span data-stu-id="af9e0-112">Problem statement</span></span>

- <span data-ttu-id="af9e0-113">Administratorzy danych musi być w stanie toocorrect niedokładne osobiste informacje i aktualizacji niekompletne lub zmieniania informacji osobistych.</span><span class="sxs-lookup"><span data-stu-id="af9e0-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="af9e0-114">Potrzeby administratorzy danych musi być możliwe toodelete informacji osobistych na żądanie hello podmiotu danych.</span><span class="sxs-lookup"><span data-stu-id="af9e0-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="af9e0-115">Administratorzy danych konieczne tooexport danych i dostarczyć tooa dotyczą dane w formacie wspólnego, strukturalnych na jego żądanie.</span><span class="sxs-lookup"><span data-stu-id="af9e0-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="af9e0-116">Cele firmy</span><span class="sxs-lookup"><span data-stu-id="af9e0-116">Company goals</span></span>

- <span data-ttu-id="af9e0-117">Nieprawidłowe lub niepełne klienta, gościa wesele pracowników i informacje osobiste dostawcy musi poprawione lub zaktualizowane w usłudze Azure Active Directory i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="af9e0-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="af9e0-118">Informacje osobiste, muszą zostać usunięte w usłudze Azure Active Directory i usługi Azure SQL Database na żądanie hello na temat danych.</span><span class="sxs-lookup"><span data-stu-id="af9e0-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="af9e0-119">Dane osobowe musi być eksportowany w formacie wspólnego, strukturalnych na żądanie hello na temat danych.</span><span class="sxs-lookup"><span data-stu-id="af9e0-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="af9e0-120">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="af9e0-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="af9e0-121">Usługi Azure Active Directory: rozwiązać/Popraw nieprawidłowe lub niekompletne dane osobowe i wymazywanie/usuwania osobistych danych/profili użytkowników</span><span class="sxs-lookup"><span data-stu-id="af9e0-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="af9e0-122">[Usługa Azure Active Directory](https://azure.microsoft.com/services/active-directory/) jest oparta na chmurze, wielodostępne katalogami i tożsamościami zarządzania usługi Microsoft.</span><span class="sxs-lookup"><span data-stu-id="af9e0-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="af9e0-123">Można poprawić, zaktualizować lub usunąć klientów i pracownika profili użytkowników oraz informacje o pracy użytkownika, które zawierają dane osobowe, takie jak nazwa użytkownika, tytuł pracy, adres lub numer telefonu, w Twojej [usługi Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) środowisko przy użyciu hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="af9e0-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="af9e0-124">Należy zalogować się przy użyciu konta administratora globalnego dla katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="af9e0-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="af9e0-125">Jak skorygować lub zaktualizować profil użytkownika i pracy informacji w usłudze Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="af9e0-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="af9e0-126">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="af9e0-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="af9e0-127">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="af9e0-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![nośnik/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="af9e0-129">Na powitania **użytkowników i grup** bloku, wybierz opcję **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="af9e0-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![nośnik/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="af9e0-131">Na powitania **użytkowników i grup — Użytkownicy** bloku, wybierz użytkownika z listy hello, a następnie w bloku hello hello wybranego użytkownika, wybierz opcję **profilu** tooview hello informacje o profilu użytkownika wymagające toobe rozwiązany lub zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="af9e0-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![nośnik/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="af9e0-133">Popraw lub zaktualizować hello informacje, a następnie, na pasku poleceń hello, wybierz **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="af9e0-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="af9e0-134">W bloku hello hello wybranego użytkownika, wybierz **pracy informacji** tooview pracy informacje o użytkowniku wymagające toobe poprawione lub aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="af9e0-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![nośnik/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="af9e0-136">Popraw lub zaktualizować informacje o pracy użytkownika hello, a następnie na pasku poleceń hello, wybierz opcję **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="af9e0-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="af9e0-137">Jak usunąć profil użytkownika w usłudze Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="af9e0-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="af9e0-138">Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="af9e0-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="af9e0-139">Wybierz **więcej usług**, wprowadź **użytkowników i grup** w hello pola tekstowego, a następnie wybierz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="af9e0-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="af9e0-140">Na powitania **użytkowników i grup** bloku, wybierz opcję **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="af9e0-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![nośnik/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="af9e0-142">Na powitania **użytkowników i grup — Użytkownicy** bloku, wybierz użytkownika z listy hello.</span><span class="sxs-lookup"><span data-stu-id="af9e0-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![nośnik/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="af9e0-144">W bloku hello hello wybranego użytkownika, wybierz **omówienie**, a następnie na pasku poleceń hello, wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="af9e0-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="af9e0-145">Baza danych SQL: rozwiązać Popraw nieprawidłowe lub niekompletne dane osobowe; wymazywanie lub Usuń dane osobowe; Eksportuj dane osobowe</span><span class="sxs-lookup"><span data-stu-id="af9e0-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="af9e0-146">[Baza danych SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) jest chmury bazy danych, która ułatwia deweloperom tworzenie i obsługa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af9e0-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="af9e0-147">Można aktualizować dane osobowe w [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) przy użyciu standardowego zapytania SQL, a także mogą być również usuwane.</span><span class="sxs-lookup"><span data-stu-id="af9e0-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="af9e0-148">Ponadto można wyeksportować dane osobowe z bazy danych SQL przy użyciu różnych metod, w tym hello importu serwera Azure SQL i Kreator eksportu i w różnych formatach, łącznie z plikiem pliku BACPAC.</span><span class="sxs-lookup"><span data-stu-id="af9e0-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="af9e0-149">Jak rozwiązać, zaktualizować lub wymazanie danych osobowych w bazie danych SQL?</span><span class="sxs-lookup"><span data-stu-id="af9e0-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="af9e0-150">toolearn jak toocorrect lub aktualizacji danych osobowych w bazie danych SQL, odwiedź stronę hello [aktualizacji (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Aktualizowanie tekstu](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [zaktualizować o wspólnym wyrażeniem tabeli](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), lub [ Aktualizowanie tekstu zapisu](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="af9e0-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="af9e0-151">toolearn jak toodelete danych osobowych w bazie danych SQL, odwiedź stronę hello [usunąć (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="af9e0-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="af9e0-152">Jak eksportować dane osobowe tooa pliku BACPAC pliku w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="af9e0-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="af9e0-153">Plik pliku BACPAC zawiera hello danych bazy danych SQL i metadanych i plik zip z rozszerzeniem pliku BACPAC.</span><span class="sxs-lookup"><span data-stu-id="af9e0-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="af9e0-154">Można to zrobić przy użyciu hello [portalu Azure](https://portal.azure.com/), hello SQLPackage narzędzie wiersza polecenia, programu SQL Server Management Studio (SSMS) lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="af9e0-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="af9e0-155">toolearn jak tooexport tooa pliku BACPAC plik danych hello odwiedziny [Eksportowanie pliku pliku BACPAC tooa bazy danych Azure SQL](https://docs.microsoft.com/azure/sql-database/sql-database-export) strony, który zawiera szczegółowe instrukcje dotyczące każdej z metod wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="af9e0-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="af9e0-156">Jak wyeksportować dane osobowe z bazy danych SQL z hello importu serwera SQL i Kreator eksportu?</span><span class="sxs-lookup"><span data-stu-id="af9e0-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="af9e0-157">Ten kreator pomaga skopiować dane z docelowym tooa źródła.</span><span class="sxs-lookup"><span data-stu-id="af9e0-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="af9e0-158">Aby Kreator toohello wprowadzenie, w tym jak tooget go, informacje o uprawnieniach i jak ułatwić tooget za pomocą narzędzia hello odwiedź hello [i eksportowanie danych z hello programu SQL Server zaimportuj Kreatora importu i eksportu](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="af9e0-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="af9e0-159">Omówienie kroków kreatora hello, odwiedź stronę hello [etapami hello importu serwera SQL i Kreator eksportu](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="af9e0-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af9e0-160">Następne kroki:</span><span class="sxs-lookup"><span data-stu-id="af9e0-160">Next Steps:</span></span>

[<span data-ttu-id="af9e0-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="af9e0-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="af9e0-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af9e0-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

