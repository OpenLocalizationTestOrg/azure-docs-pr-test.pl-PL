---
title: "Zawsze zaszyfrowane: Azure SQL Database — magazynu certyfikatów systemu Windows | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toosecure poufnych danych w bazie danych SQL przy użyciu szyfrowania bazy danych przy użyciu hello zawsze zaszyfrowane kreatora w programu SQL Server Management Studio (SSMS). Przedstawia on także sposób toostore kluczy szyfrowania w certyfikacie Windows hello przechowywania."
keywords: szyfrowanie danych, szyfrowania sql, szyfrowania bazy danych poufnych danych, zawsze zaszyfrowane
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="a9a4d-105">Zawsze zaszyfrowane: Ochrona poufnych danych w bazie danych SQL i przechowywania kluczy szyfrowania w magazynie certyfikatów systemu Windows hello</span><span class="sxs-lookup"><span data-stu-id="a9a4d-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="a9a4d-106">W tym artykule opisano, jak toosecure poufne dane zawarte w SQL bazy danych przy użyciu szyfrowania bazy danych przy użyciu hello [zawsze szyfrowany Kreator](https://msdn.microsoft.com/library/mt459280.aspx) w [programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="a9a4d-107">Przedstawia on także sposób toostore kluczy szyfrowania w certyfikacie Windows hello przechowywania.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="a9a4d-108">Zawsze zaszyfrowane jest nową technologią szyfrowania danych w bazie danych SQL Azure i programu SQL Server, która pomaga chronić poufnych danych przechowywanych na serwerze hello podczas przenoszenia między klientem a serwerem i gdy danych hello jest używany, zapewnienie poufnych danych, nigdy nie będzie wyświetlany jako zwykły tekst wewnątrz hello bazy danych systemu.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="a9a4d-109">Po dane są szyfrowane, tylko aplikacje klienckie lub serwery aplikacji, które mają dostęp toohello klucze mogą uzyskać dostęp do danych w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="a9a4d-110">Aby uzyskać szczegółowe informacje, zobacz [zawsze zaszyfrowane (aparat bazy danych)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="a9a4d-111">Po skonfigurowaniu hello toouse bazy danych zawsze zaszyfrowane, spowoduje utworzenie aplikacji klienckiej w języku C# z programu Visual Studio toowork hello zaszyfrowanych danych.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="a9a4d-112">Wykonaj kroki hello w tym artykule toolearn jak tooset się zawsze zaszyfrowane dla bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="a9a4d-113">W tym artykule dowiesz się, jak hello tooperform następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="a9a4d-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="a9a4d-114">Użyj hello zawsze zaszyfrowane kreatora w programie SSMS toocreate [zawsze zaszyfrowane klucze](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="a9a4d-115">Utwórz [klucza głównego kolumny (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="a9a4d-116">Utwórz [klucza szyfrowania kolumny (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="a9a4d-117">Tworzenie tabeli bazy danych i szyfrowania kolumn.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="a9a4d-118">Utwórz aplikację, która wstawia, wybiera i wyświetla dane z hello zaszyfrowanych kolumn.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9a4d-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a9a4d-119">Prerequisites</span></span>
<span data-ttu-id="a9a4d-120">W tym samouczku potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="a9a4d-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="a9a4d-121">Konto i subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-121">An Azure account and subscription.</span></span> <span data-ttu-id="a9a4d-122">Jeśli nie masz, zaloguj się do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a9a4d-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) wersji 13.0.700.242 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="a9a4d-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) lub nowszej (na komputerze klienckim hello).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="a9a4d-125">Program [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="a9a4d-126">Utwórz pustą bazę danych SQL</span><span class="sxs-lookup"><span data-stu-id="a9a4d-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="a9a4d-127">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a9a4d-128">Kliknij przycisk **nowe** > **dane i magazyn** > **bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="a9a4d-129">Utwórz **puste** bazy danych o nazwie **Clinic** na nowym lub istniejącym serwerze.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="a9a4d-130">Aby uzyskać szczegółowe instrukcje dotyczące tworzenia bazy danych w hello portalu Azure, zobacz [pierwszą bazę danych Azure SQL](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Tworzenie pustej bazy danych](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="a9a4d-132">Parametry połączenia hello trzeba będzie później w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="a9a4d-133">Po utworzeniu bazy danych hello Przejdź toohello nowe Clinic bazy danych i skopiuj hello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="a9a4d-134">Można pobrać ciągu połączenia hello w dowolnym momencie, ale jest łatwe toocopy go w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="a9a4d-135">Kliknij przycisk **baz danych SQL** > **Clinic** > **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="a9a4d-136">Skopiuj parametry połączenia hello **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Skopiuj parametry połączenia hello](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="a9a4d-138">Połączenie bazy danych toohello z SSMS</span><span class="sxs-lookup"><span data-stu-id="a9a4d-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="a9a4d-139">Otwórz SSMS i połączenia z bazą danych Clinic hello toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="a9a4d-140">Otwórz program SSMS.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-140">Open SSMS.</span></span> <span data-ttu-id="a9a4d-141">(Kliknij **Connect** > **aparatu bazy danych** tooopen hello **połączyć tooServer** okna, jeśli nie jest otwarty).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="a9a4d-142">Wprowadź nazwę serwera i poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-142">Enter your server name and credentials.</span></span> <span data-ttu-id="a9a4d-143">Nazwa serwera Hello można znaleźć w bloku bazy danych SQL hello i w parametrach połączenia hello wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="a9a4d-144">Typ hello pełną serwerów nazw, w tym *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Skopiuj parametry połączenia hello](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="a9a4d-146">Jeśli hello **nowej reguły zapory** okno, zaloguj się tooAzure i let SSMS Utwórz nową regułę zapory dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="a9a4d-147">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="a9a4d-147">Create a table</span></span>
<span data-ttu-id="a9a4d-148">W tej sekcji utworzysz danych pacjenta toohold tabeli.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="a9a4d-149">Będzie to normalna tabeli początkowo — skonfiguruje szyfrowania w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="a9a4d-150">Rozwiń węzeł **baz danych**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="a9a4d-151">Kliknij prawym przyciskiem myszy hello **Clinic** bazy danych, a następnie kliknij przycisk **nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="a9a4d-152">Wklej powitania po języka Transact-SQL (T-SQL) do okna nowej kwerendy hello i **Execute** go.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="a9a4d-153">Szyfrowania kolumn (Konfigurowanie zawsze szyfrowane)</span><span class="sxs-lookup"><span data-stu-id="a9a4d-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="a9a4d-154">SSMS udostępnia kreatora tooeasily Konfigurowanie zawsze szyfrowane przez skonfigurowanie hello CMK, CEK i zaszyfrowanych kolumn dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="a9a4d-155">Rozwiń węzeł **baz danych** > **Clinic** > **tabel**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="a9a4d-156">Powitania kliknij prawym przyciskiem myszy **pacjentów** tabeli i wybierz **szyfrowania kolumn** tooopen hello zawsze zaszyfrowane kreatora:</span><span class="sxs-lookup"><span data-stu-id="a9a4d-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Szyfrowania kolumn](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="a9a4d-158">Witaj zawsze zaszyfrowane Kreator zawiera następujące sekcje hello: **kolumn wybór**, **konfiguracji klucza głównego** (CMK), **weryfikacji**, i  **Podsumowanie**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="a9a4d-159">Wybór kolumny</span><span class="sxs-lookup"><span data-stu-id="a9a4d-159">Column Selection</span></span>
<span data-ttu-id="a9a4d-160">Kliknij przycisk **dalej** na powitania **wprowadzenie** hello tooopen strony **kolumn wybór** strony.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="a9a4d-161">Na tej stronie możesz wybrać kolumny, które chcesz tooencrypt, [hello typ szyfrowania i jakie klucza szyfrowania kolumny (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="a9a4d-162">Szyfrowanie **SSN** i **Data urodzenia** informacje dotyczące każdego pacjenta.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="a9a4d-163">Witaj **SSN** kolumny użyje deterministyczne szyfrowania, który obsługuje równości wyszukiwań, sprzężeń i Grupuj według.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="a9a4d-164">Witaj **Data urodzenia** kolumny użyje losowego szyfrowania, który nie obsługuje operacji.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="a9a4d-165">Zestaw hello **typ szyfrowania** dla hello **SSN** kolumny zbyt**Deterministic** i hello **Data urodzenia** kolumny zbyt **Wybierane**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="a9a4d-166">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-166">Click **Next**.</span></span>

![Szyfrowania kolumn](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="a9a4d-168">Konfiguracja klucza głównego</span><span class="sxs-lookup"><span data-stu-id="a9a4d-168">Master Key Configuration</span></span>
<span data-ttu-id="a9a4d-169">Witaj **konfiguracji klucza głównego** strona jest, gdzie skonfigurować swoją CMK i dostawcy magazynu kluczy hello wybierz gdzie hello CMK będą przechowywane.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="a9a4d-170">Obecnie można przechowywać CMK w magazynie certyfikatów systemu Windows hello, usługi Azure Key Vault lub sprzętowego modułu zabezpieczeń (HSM).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="a9a4d-171">Ten samouczek pokazuje, jak toostore klucze w certyfikacie Windows hello przechowywania.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="a9a4d-172">Sprawdź, czy **magazynu certyfikatów systemu Windows** jest zaznaczone, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Konfiguracja klucza głównego](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="a9a4d-174">Walidacja</span><span class="sxs-lookup"><span data-stu-id="a9a4d-174">Validation</span></span>
<span data-ttu-id="a9a4d-175">Można zaszyfrować kolumny hello teraz lub później zapisać toorun skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="a9a4d-176">W tym samouczku, wybierz **teraz kontynuować toofinish** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="a9a4d-177">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a9a4d-177">Summary</span></span>
<span data-ttu-id="a9a4d-178">Sprawdź, czy ustawienia hello są wszystkie prawidłowe, a następnie kliknij przycisk **Zakończ** toocomplete hello ustawienia zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Podsumowanie](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="a9a4d-180">Sprawdź akcje hello Kreatora</span><span class="sxs-lookup"><span data-stu-id="a9a4d-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="a9a4d-181">Po zakończeniu pracy Kreatora hello bazy danych jest skonfigurowane dla zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="a9a4d-182">Witaj Witaj kreatora wykonywane następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="a9a4d-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="a9a4d-183">Utworzyć CMK.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-183">Created a CMK.</span></span>
* <span data-ttu-id="a9a4d-184">Utworzyć CEK.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-184">Created a CEK.</span></span>
* <span data-ttu-id="a9a4d-185">Skonfigurowany hello wybrane kolumny do szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="a9a4d-186">Twoje **pacjentów** tabeli obecnie nie ma danych, ale wszystkie istniejące dane w hello wybrane kolumny jest teraz zaszyfrowana.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="a9a4d-187">Sprawdź hello tworzenia kluczy hello w programie SSMS, przechodząc zbyt**Clinic** > **zabezpieczeń** > **zawsze zaszyfrowane klucze**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="a9a4d-188">Możesz teraz przeglądać hello nowych kluczy, które hello wygenerowany przez kreatora.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="a9a4d-189">Tworzenie aplikacji klienckiej, która współdziała z hello zaszyfrowanych danych</span><span class="sxs-lookup"><span data-stu-id="a9a4d-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="a9a4d-190">Teraz, gdy skonfigurowano zawsze zaszyfrowane, można utworzyć aplikację, która wykonuje *wstawia* i *wybiera* na powitania zaszyfrowanych kolumn.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="a9a4d-191">toosuccessfully Uruchom hello przykładowej aplikacji, należy uruchomić je na powitania tym samym komputerze, na których są uruchomione hello Kreator zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="a9a4d-192">toorun aplikacji hello na innym komputerze, należy wdrożyć zawsze zaszyfrowane certyfikaty toohello komputera z systemem powitania klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a9a4d-193">Aplikacja musi używać [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) obiekty podczas przekazywania serwera toohello danych w postaci zwykłego tekstu z kolumnami zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="a9a4d-194">Przekazywanie wartości literałów bez przy użyciu obiektów SqlParameter spowoduje Wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="a9a4d-195">Otwórz program Visual Studio i utworzyć nową aplikację konsoli języka C#.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="a9a4d-196">Upewnij się, że projekt jest ustawiona zbyt**.NET Framework 4.6** lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="a9a4d-197">Nazwa projektu hello **AlwaysEncryptedConsoleApp** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Nową aplikację konsoli](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="a9a4d-199">Modyfikowanie użytkownika tooenable ciąg połączenia zawsze zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="a9a4d-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="a9a4d-200">W tej sekcji opisano sposób tooenable zawsze zaszyfrowane w ciągu połączenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="a9a4d-201">Należy zmodyfikować aplikacji konsoli hello utworzonego w następnej sekcji Witaj, "Zawsze zaszyfrowane Przykładowa aplikacja konsolowa".</span><span class="sxs-lookup"><span data-stu-id="a9a4d-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="a9a4d-202">tooenable zawsze zaszyfrowane, potrzebujesz tooadd hello **ustawienie szyfrowania kolumny** połączenia tooyour — słowo kluczowe string i ustaw dla niej zbyt**włączone**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="a9a4d-203">Możesz ustawić bezpośrednio w parametrach połączenia hello, lub jest on ustawiany za pomocą [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="a9a4d-204">Hello przykładowej aplikacji w hello obok sekcji przedstawiono sposób toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="a9a4d-205">Jest to hello zmiany tylko w tooAlways określonych aplikacji zaszyfrowane klienta wymagane.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="a9a4d-206">Jeśli masz istniejącą aplikację przechowujący zewnętrznie parametrach połączenia (to znaczy w pliku konfiguracyjnym), może być możliwe tooenable zawsze zaszyfrowane bez konieczności zmieniania kodu.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="a9a4d-207">Włącz zawsze zaszyfrowane w parametrach połączenia hello</span><span class="sxs-lookup"><span data-stu-id="a9a4d-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="a9a4d-208">Dodaj następujące parametry połączenia tooyour — słowo kluczowe hello:</span><span class="sxs-lookup"><span data-stu-id="a9a4d-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="a9a4d-209">Włącz zawsze zaszyfrowane przy SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="a9a4d-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="a9a4d-210">Witaj poniższy kod przedstawia sposób hello tooenable zawsze szyfrowane przez ustawienie [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) za[włączone](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="a9a4d-211">Zawsze zaszyfrowane Przykładowa aplikacja konsolowa</span><span class="sxs-lookup"><span data-stu-id="a9a4d-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="a9a4d-212">W przykładzie pokazano, jak:</span><span class="sxs-lookup"><span data-stu-id="a9a4d-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="a9a4d-213">Modyfikowanie sieci tooenable ciąg połączenia zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="a9a4d-214">Wstawianie danych do hello zaszyfrowanych kolumn.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="a9a4d-215">Wybierz rekord filtrując określonej wartości w zaszyfrowanej kolumny.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="a9a4d-216">Zamień zawartość hello **Program.cs** z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="a9a4d-217">Zastąp hello parametry połączenia dla zmiennej globalnej connectionString hello w wierszu hello bezpośrednio nad hello metody Main ciągu prawidłowe połączenie z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="a9a4d-218">To jest zmiana tylko hello należy toomake toothis kodu.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="a9a4d-219">Uruchom toosee aplikacji hello zawsze zaszyfrowane w akcji.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-219">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="a9a4d-220">Sprawdź, czy hello dane są szyfrowane</span><span class="sxs-lookup"><span data-stu-id="a9a4d-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="a9a4d-221">Można szybko sprawdzić szyfrowanie danych rzeczywistych hello na powitania serwera, badając hello **pacjentów** danych za pomocą narzędzia SSMS.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="a9a4d-222">(Użyj tego połączenia gdzie ustawienie szyfrowania kolumny hello nie jest jeszcze włączone).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="a9a4d-223">Uruchom następujące zapytanie w bazie danych Clinic hello hello.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="a9a4d-224">Widać hello zaszyfrowanych kolumn nie zawierają żadnych danych w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nową aplikację konsoli](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="a9a4d-226">toouse SSMS tooaccess hello dane w postaci zwykłego tekstu, można dodać hello **ustawienie szyfrowania kolumny = włączone** parametru toohello połączenia.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="a9a4d-227">W programie SSMS, kliknij prawym przyciskiem myszy serwer w **Eksplorator obiektów**, a następnie kliknij przycisk **rozłączenia**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="a9a4d-228">Kliknij przycisk **Connect** > **aparatu bazy danych** tooopen hello **połączyć tooServer** okna, a następnie kliknij przycisk **opcje**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="a9a4d-229">Kliknij przycisk **dodatkowe parametry połączenia** i typ **ustawienie szyfrowania kolumny = włączone**.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nową aplikację konsoli](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="a9a4d-231">Uruchom hello następujące zapytanie na powitania **Clinic** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="a9a4d-232">Możesz teraz przeglądać dane w postaci zwykłego tekstu hello hello zaszyfrowanych kolumn.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nową aplikację konsoli](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="a9a4d-234">Jeśli łączysz się z SSMS (lub dowolnego klienta) z innego komputera, nie będą miały klucze szyfrowania toohello dostępu i nie będą mogli toodecrypt hello danych.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a9a4d-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9a4d-235">Next steps</span></span>
<span data-ttu-id="a9a4d-236">Po utworzeniu bazy danych, która używa zawsze zaszyfrowane, może być toodo hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="a9a4d-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="a9a4d-237">W tym przykładzie należy uruchomić na innym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-237">Run this sample from a different computer.</span></span> <span data-ttu-id="a9a4d-238">Nie ma on dostęp do kluczy szyfrowania toohello, nie ma dostępu do danych w postaci zwykłego tekstu toohello i nie będzie działać prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="a9a4d-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="a9a4d-239">[Obracanie i wyczyścić klucze](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="a9a4d-240">[Migracja danych, które jest już zaszyfrowane za pomocą zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="a9a4d-241">[Wdrażanie komputerów klienckich zawsze zaszyfrowane tooother certyfikaty](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (zobacz sekcję "TooApplications dostępnych certyfikatów i użytkowników co" hello).</span><span class="sxs-lookup"><span data-stu-id="a9a4d-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="a9a4d-242">Informacje pokrewne</span><span class="sxs-lookup"><span data-stu-id="a9a4d-242">Related information</span></span>
* [<span data-ttu-id="a9a4d-243">Zawsze zaszyfrowane (Programowanie klienta)</span><span class="sxs-lookup"><span data-stu-id="a9a4d-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="a9a4d-244">Przezroczystego szyfrowania danych</span><span class="sxs-lookup"><span data-stu-id="a9a4d-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="a9a4d-245">Szyfrowanie serwera SQL</span><span class="sxs-lookup"><span data-stu-id="a9a4d-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="a9a4d-246">Kreator zawsze zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="a9a4d-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="a9a4d-247">Blog zawsze zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="a9a4d-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

