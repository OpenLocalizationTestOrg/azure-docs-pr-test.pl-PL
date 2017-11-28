---
title: "Zawsze zaszyfrowane: Baza danych SQL — usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toosecure poufnych danych w bazie danych SQL z szyfrowania danych przy użyciu hello zawsze zaszyfrowane kreatora w programie SQL Server Management Studio. Zawiera również instrukcje, które zawierają jak toostore każdego klucza szyfrowania w usłudze Azure Key Vault."
keywords: szyfrowanie klucza szyfrowania danych w chmurze szyfrowania
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="be2dc-105">Zawsze zaszyfrowane: Ochrona poufnych danych w bazie danych SQL i przechowywania kluczy szyfrowania w usłudze Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="be2dc-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="be2dc-106">W tym artykule opisano, jak toosecure poufne dane zawarte w SQL bazy danych przy użyciu szyfrowania danych przy użyciu hello [zawsze szyfrowany Kreator](https://msdn.microsoft.com/library/mt459280.aspx) w [programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="be2dc-107">Zawiera również instrukcje, które zawierają jak toostore każdego klucza szyfrowania w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be2dc-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="be2dc-108">Zawsze zaszyfrowane to nowa technologia szyfrowania danych w bazie danych SQL Azure i programu SQL Server, która pomaga chronić poufne dane przechowywane na serwerze hello podczas przepływu między klientem a serwerem, gdy dane hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="be2dc-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="be2dc-109">Zawsze zaszyfrowane gwarantuje, że poufne dane nigdy nie jest wyświetlana jako zwykły tekst wewnątrz hello bazy danych systemu.</span><span class="sxs-lookup"><span data-stu-id="be2dc-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="be2dc-110">Po skonfigurowaniu szyfrowania danych tylko aplikacje klienckie lub serwery aplikacji, które mają dostęp toohello kluczy można uzyskać dostępu do danych w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="be2dc-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="be2dc-111">Aby uzyskać szczegółowe informacje, zobacz [zawsze zaszyfrowane (aparat bazy danych)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="be2dc-112">Po skonfigurowaniu hello toouse bazy danych zawsze zaszyfrowane spowoduje utworzenie aplikacji klienckiej w języku C# z programu Visual Studio toowork hello zaszyfrowanych danych.</span><span class="sxs-lookup"><span data-stu-id="be2dc-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="be2dc-113">Wykonaj kroki hello w tym artykule i Dowiedz się, jak tooset się zawsze zaszyfrowane dla bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="be2dc-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="be2dc-114">W tym artykule dowiesz się, jak hello tooperform następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="be2dc-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="be2dc-115">Użyj hello zawsze zaszyfrowane kreatora w programie SSMS toocreate [zawsze zaszyfrowane klucze](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="be2dc-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="be2dc-116">Utwórz [klucza głównego kolumny (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="be2dc-117">Utwórz [klucza szyfrowania kolumny (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="be2dc-118">Tworzenie tabeli bazy danych i szyfrowania kolumn.</span><span class="sxs-lookup"><span data-stu-id="be2dc-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="be2dc-119">Utwórz aplikację, która wstawia, wybiera i wyświetla dane z hello zaszyfrowanych kolumn.</span><span class="sxs-lookup"><span data-stu-id="be2dc-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be2dc-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="be2dc-120">Prerequisites</span></span>
<span data-ttu-id="be2dc-121">W tym samouczku potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="be2dc-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="be2dc-122">Konto i subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="be2dc-122">An Azure account and subscription.</span></span> <span data-ttu-id="be2dc-123">Jeśli nie masz, zaloguj się do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="be2dc-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="be2dc-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) wersji 13.0.700.242 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="be2dc-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="be2dc-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) lub nowszej (na komputerze klienckim hello).</span><span class="sxs-lookup"><span data-stu-id="be2dc-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="be2dc-126">Program [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="be2dc-127">[Program Azure PowerShell](/powershell/azure/overview), w wersji 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="be2dc-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="be2dc-128">Typ **(Get-Module azure flagą-ListAvailable). Wersja** toosee jakiej wersji programu PowerShell są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="be2dc-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="be2dc-129">Włączanie usługi SQL Database hello tooaccess aplikacji klienta</span><span class="sxs-lookup"><span data-stu-id="be2dc-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="be2dc-130">Należy włączyć usługi baza danych SQL klienta aplikacji tooaccess hello konfigurując wymagane uwierzytelnianie hello i uzyskiwania hello *ClientId* i *klucz tajny* należy tooauthenticate Aplikacja hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="be2dc-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="be2dc-131">Otwórz hello [klasycznego portalu Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="be2dc-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="be2dc-132">Wybierz **usługi Active Directory** i kliknij przycisk hello wystąpienie usługi Active Directory, który będzie używany przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="be2dc-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="be2dc-133">Kliknij przycisk **aplikacji**, a następnie kliknij przycisk **dodać**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="be2dc-134">Wpisz nazwę dla aplikacji (na przykład: *myClientApp*), wybierz pozycję **aplikacji sieci WEB**i kliknij przycisk toocontinue strzałkę hello.</span><span class="sxs-lookup"><span data-stu-id="be2dc-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="be2dc-135">Dla hello **adres URL logowania** i **identyfikator URI aplikacji** możesz wpisać prawidłowy adres URL (na przykład *http://myClientApp*) i kontynuować.</span><span class="sxs-lookup"><span data-stu-id="be2dc-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="be2dc-136">Kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="be2dc-137">Kopiowanie z **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="be2dc-138">(Należy tej wartości w kodzie później.)</span><span class="sxs-lookup"><span data-stu-id="be2dc-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="be2dc-139">W hello **klucze** zaznacz **1 rok** z hello **wybierz czas trwania** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="be2dc-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="be2dc-140">(Kopiowanie klucza hello zapisany w kroku 13.)</span><span class="sxs-lookup"><span data-stu-id="be2dc-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="be2dc-141">Przewiń w dół i kliknij przycisk **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="be2dc-142">Pozostaw **Pokaż** ustawić także**Microsoft Apps** i wybierz **interfejs API zarządzania usługami Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="be2dc-143">Kliknij przycisk hello toocontinue znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="be2dc-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="be2dc-144">Wybierz **dostęp do zarządzania usługą Azure...**  z hello **delegowane uprawnienia** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="be2dc-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="be2dc-145">Kliknij przycisk **SAVE** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="be2dc-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="be2dc-146">Po hello Zapisz zakończenie, skopiuj wartość klucza hello hello **klucze** sekcji.</span><span class="sxs-lookup"><span data-stu-id="be2dc-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="be2dc-147">(Należy tej wartości w kodzie później.)</span><span class="sxs-lookup"><span data-stu-id="be2dc-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="be2dc-148">Tworzenie kluczy toostore magazyn kluczy</span><span class="sxs-lookup"><span data-stu-id="be2dc-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="be2dc-149">Skonfigurowano aplikację klienta, a masz Identyfikatora klienta, jest czas toocreate magazyn kluczy i skonfigurować jego zasady dostępu, aby aplikacji dostępnym hello magazynu kluczy tajnych (hello zawsze zaszyfrowane kluczy).</span><span class="sxs-lookup"><span data-stu-id="be2dc-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="be2dc-150">Witaj *utworzyć*, *uzyskać*, *listy*, *logowania*, *Sprawdź*, *wrapKey*, i *unwrapKey* uprawnienia są wymagane do utworzenia nowego klucza głównego kolumny i konfigurowania szyfrowania za pomocą programu SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="be2dc-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="be2dc-151">Może szybko utworzyć magazyn kluczy, uruchamiając hello następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="be2dc-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="be2dc-152">Aby uzyskać dokładniejsze objaśnienie tych poleceń cmdlet i więcej informacji na temat tworzenia i konfigurowania magazynu kluczy, zobacz [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="be2dc-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="be2dc-153">Utwórz pustą bazę danych SQL</span><span class="sxs-lookup"><span data-stu-id="be2dc-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="be2dc-154">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="be2dc-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="be2dc-155">Przejdź za**nowy** > **dane i magazyn** > **bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="be2dc-156">Utwórz **puste** bazy danych o nazwie **Clinic** na nowym lub istniejącym serwerze.</span><span class="sxs-lookup"><span data-stu-id="be2dc-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="be2dc-157">Aby uzyskać szczegółowe informacje o toocreate bazy danych w hello portalu Azure, zobacz temat [pierwszą bazę danych Azure SQL](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be2dc-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Tworzenie pustej bazy danych](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="be2dc-159">Będzie konieczne hello parametry połączenia później w samouczku hello, więc po utworzeniu bazy danych hello Przejdź toohello nowe Clinic bazy danych i skopiuj hello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="be2dc-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="be2dc-160">Można pobrać ciągu połączenia hello w dowolnym momencie, ale jest łatwe toocopy w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="be2dc-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="be2dc-161">Przejdź za**baz danych SQL** > **Clinic** > **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="be2dc-162">Skopiuj parametry połączenia hello **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Skopiuj parametry połączenia hello](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="be2dc-164">Połączenie bazy danych toohello z SSMS</span><span class="sxs-lookup"><span data-stu-id="be2dc-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="be2dc-165">Otwórz SSMS i połączenia z bazą danych Clinic hello toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="be2dc-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="be2dc-166">Otwórz program SSMS.</span><span class="sxs-lookup"><span data-stu-id="be2dc-166">Open SSMS.</span></span> <span data-ttu-id="be2dc-167">(Przejdź zbyt**Connect** > **aparatu bazy danych** tooopen hello **połączyć tooServer** okna, jeśli nie jest otwarty.)</span><span class="sxs-lookup"><span data-stu-id="be2dc-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="be2dc-168">Wprowadź nazwę serwera i poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="be2dc-168">Enter your server name and credentials.</span></span> <span data-ttu-id="be2dc-169">Nazwa serwera Hello można znaleźć w bloku bazy danych SQL hello i w parametrach połączenia hello wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="be2dc-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="be2dc-170">Typ hello pełną nazwę serwera, łącznie z *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="be2dc-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![Skopiuj parametry połączenia hello](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="be2dc-172">Jeśli hello **nowej reguły zapory** okno, zaloguj się tooAzure i let SSMS Utwórz nową regułę zapory dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="be2dc-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="be2dc-173">Tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="be2dc-173">Create a table</span></span>
<span data-ttu-id="be2dc-174">W tej sekcji utworzysz danych pacjenta toohold tabeli.</span><span class="sxs-lookup"><span data-stu-id="be2dc-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="be2dc-175">Nie jest początkowo szyfrowane — skonfiguruj szyfrowania w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="be2dc-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="be2dc-176">Rozwiń węzeł **baz danych**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="be2dc-177">Kliknij prawym przyciskiem myszy hello **Clinic** bazy danych, a następnie kliknij przycisk **nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="be2dc-178">Wklej powitania po języka Transact-SQL (T-SQL) do okna nowej kwerendy hello i **Execute** go.</span><span class="sxs-lookup"><span data-stu-id="be2dc-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="be2dc-179">Szyfrowania kolumn (Konfigurowanie zawsze szyfrowane)</span><span class="sxs-lookup"><span data-stu-id="be2dc-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="be2dc-180">SSMS udostępnia kreatora, który pomoże Ci łatwe konfigurowanie zawsze zaszyfrowane poprzez ustawienie klucza głównego kolumny hello, klucz szyfrowania kolumny i zaszyfrowanych kolumn dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="be2dc-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="be2dc-181">Rozwiń węzeł **baz danych** > **Clinic** > **tabel**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="be2dc-182">Powitania kliknij prawym przyciskiem myszy **pacjentów** tabeli i wybierz **szyfrowania kolumn** tooopen hello zawsze zaszyfrowane kreatora:</span><span class="sxs-lookup"><span data-stu-id="be2dc-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Szyfrowania kolumn](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="be2dc-184">Witaj zawsze zaszyfrowane Kreator zawiera następujące sekcje hello: **kolumn wybór**, **konfiguracji klucza głównego**, **weryfikacji**, i **podsumowanie** .</span><span class="sxs-lookup"><span data-stu-id="be2dc-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="be2dc-185">Wybór kolumny</span><span class="sxs-lookup"><span data-stu-id="be2dc-185">Column Selection</span></span>
<span data-ttu-id="be2dc-186">Kliknij przycisk **dalej** na powitania **wprowadzenie** hello tooopen strony **kolumn wybór** strony.</span><span class="sxs-lookup"><span data-stu-id="be2dc-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="be2dc-187">Na tej stronie możesz wybrać kolumny, które chcesz tooencrypt, [hello typ szyfrowania i jakie klucza szyfrowania kolumny (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="be2dc-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="be2dc-188">Szyfrowanie **SSN** i **Data urodzenia** informacje dotyczące każdego pacjenta.</span><span class="sxs-lookup"><span data-stu-id="be2dc-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="be2dc-189">Kolumna SSN Hello użyje deterministyczne szyfrowania, który obsługuje równości wyszukiwań, sprzężeń i Grupuj według.</span><span class="sxs-lookup"><span data-stu-id="be2dc-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="be2dc-190">kolumny Data urodzenia Hello użyje losowego szyfrowania, który nie obsługuje operacji.</span><span class="sxs-lookup"><span data-stu-id="be2dc-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="be2dc-191">Zestaw hello **typ szyfrowania** dla kolumny hello SSN zbyt**Deterministic** i zbyt hello kolumny Data urodzenia**Randomized**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="be2dc-192">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-192">Click **Next**.</span></span>

![Szyfrowania kolumn](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="be2dc-194">Konfiguracja klucza głównego</span><span class="sxs-lookup"><span data-stu-id="be2dc-194">Master Key Configuration</span></span>
<span data-ttu-id="be2dc-195">Witaj **konfiguracji klucza głównego** strona jest, gdzie skonfigurować swoją CMK i dostawcy magazynu kluczy hello wybierz gdzie hello CMK będą przechowywane.</span><span class="sxs-lookup"><span data-stu-id="be2dc-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="be2dc-196">Obecnie można przechowywać CMK w magazynie certyfikatów systemu Windows hello, usługi Azure Key Vault lub sprzętowego modułu zabezpieczeń (HSM).</span><span class="sxs-lookup"><span data-stu-id="be2dc-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="be2dc-197">Ten samouczek pokazuje, jak toostore klucze w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be2dc-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="be2dc-198">Wybierz **usługi Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="be2dc-199">Wybierz żądaną magazynu kluczy hello z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="be2dc-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="be2dc-200">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-200">Click **Next**.</span></span>

![Konfiguracja klucza głównego](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="be2dc-202">Walidacja</span><span class="sxs-lookup"><span data-stu-id="be2dc-202">Validation</span></span>
<span data-ttu-id="be2dc-203">Można zaszyfrować kolumny hello teraz lub później zapisać toorun skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be2dc-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="be2dc-204">W tym samouczku, wybierz **teraz kontynuować toofinish** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="be2dc-205">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="be2dc-205">Summary</span></span>
<span data-ttu-id="be2dc-206">Sprawdź, czy ustawienia hello są wszystkie prawidłowe, a następnie kliknij przycisk **Zakończ** toocomplete hello ustawienia zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="be2dc-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Podsumowanie](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="be2dc-208">Sprawdź akcje hello Kreatora</span><span class="sxs-lookup"><span data-stu-id="be2dc-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="be2dc-209">Po zakończeniu pracy Kreatora hello bazy danych jest skonfigurowane dla zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="be2dc-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="be2dc-210">Witaj Witaj kreatora wykonywane następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="be2dc-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="be2dc-211">Utworzony klucza głównego kolumny i zapisana w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be2dc-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="be2dc-212">Utworzony klucz szyfrowania kolumny i zapisana w usłudze Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="be2dc-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="be2dc-213">Skonfigurowany hello wybrane kolumny do szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="be2dc-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="be2dc-214">Tabela pacjentów Hello obecnie nie ma danych, ale wszystkie istniejące dane w hello wybrane kolumny jest teraz zaszyfrowana.</span><span class="sxs-lookup"><span data-stu-id="be2dc-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="be2dc-215">Sprawdź hello tworzenia kluczy hello w programie SSMS, rozwijając **Clinic** > **zabezpieczeń** > **zawsze zaszyfrowane klucze**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="be2dc-216">Tworzenie aplikacji klienckiej, która współdziała z hello zaszyfrowanych danych</span><span class="sxs-lookup"><span data-stu-id="be2dc-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="be2dc-217">Teraz, gdy skonfigurowano zawsze zaszyfrowane, można utworzyć aplikację, która wykonuje *wstawia* i *wybiera* na powitania zaszyfrowanych kolumn.</span><span class="sxs-lookup"><span data-stu-id="be2dc-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="be2dc-218">Aplikacja musi używać [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) obiekty podczas przekazywania serwera toohello danych w postaci zwykłego tekstu z kolumnami zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="be2dc-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="be2dc-219">Przekazywanie wartości literałów bez przy użyciu obiektów SqlParameter spowoduje Wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="be2dc-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="be2dc-220">Otwórz program Visual Studio i utworzyć nowe C# **aplikacji konsoli** (Visual Studio 2015 lub starszym) lub **aplikacji konsoli (.NET Framework)** (Visual Studio 2017 i nowsze).</span><span class="sxs-lookup"><span data-stu-id="be2dc-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="be2dc-221">Upewnij się, że projekt jest ustawiona zbyt**.NET Framework 4.6** lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="be2dc-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="be2dc-222">Nazwa projektu hello **AlwaysEncryptedConsoleAKVApp** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="be2dc-223">Zainstaluj hello następujące pakiety NuGet, przechodząc zbyt**narzędzia** > **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="be2dc-224">Uruchom te dwa wiersze kodu w hello Konsola Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="be2dc-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="be2dc-225">Modyfikowanie użytkownika tooenable ciąg połączenia zawsze zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="be2dc-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="be2dc-226">W tej sekcji opisano sposób tooenable zawsze zaszyfrowane w ciągu połączenia bazy danych.</span><span class="sxs-lookup"><span data-stu-id="be2dc-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="be2dc-227">tooenable zawsze zaszyfrowane, potrzebujesz tooadd hello **ustawienie szyfrowania kolumny** połączenia tooyour — słowo kluczowe string i ustaw dla niej zbyt**włączone**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="be2dc-228">Możesz ustawić bezpośrednio w parametrach połączenia hello, lub jest on ustawiany za pomocą [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="be2dc-229">Hello przykładowej aplikacji w hello obok sekcji przedstawiono sposób toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="be2dc-230">Włącz zawsze zaszyfrowane w parametrach połączenia hello</span><span class="sxs-lookup"><span data-stu-id="be2dc-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="be2dc-231">Dodaj następujące parametry połączenia tooyour — słowo kluczowe hello.</span><span class="sxs-lookup"><span data-stu-id="be2dc-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="be2dc-232">Włącz zawsze zaszyfrowane przy SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="be2dc-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="be2dc-233">Witaj następującego kodu pokazuje sposób tooenable zawsze szyfrowane przez ustawienie [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) za[włączone](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="be2dc-234">Zarejestruj dostawcę usługi Azure Key Vault hello</span><span class="sxs-lookup"><span data-stu-id="be2dc-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="be2dc-235">Witaj poniższy kod przedstawia sposób tooregister hello dostawcy usługi Azure Key Vault ze sterownikiem programu ADO.NET hello.</span><span class="sxs-lookup"><span data-stu-id="be2dc-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="be2dc-236">Zawsze zaszyfrowane Przykładowa aplikacja konsolowa</span><span class="sxs-lookup"><span data-stu-id="be2dc-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="be2dc-237">W przykładzie pokazano, jak:</span><span class="sxs-lookup"><span data-stu-id="be2dc-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="be2dc-238">Modyfikowanie sieci tooenable ciąg połączenia zawsze szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="be2dc-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="be2dc-239">Rejestrowanie usługi Azure Key Vault, jako dostawcy magazynu kluczy aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="be2dc-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="be2dc-240">Wstawianie danych do hello zaszyfrowanych kolumn.</span><span class="sxs-lookup"><span data-stu-id="be2dc-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="be2dc-241">Wybierz rekord filtrując określonej wartości w zaszyfrowanej kolumny.</span><span class="sxs-lookup"><span data-stu-id="be2dc-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="be2dc-242">Zamień zawartość hello **Program.cs** z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="be2dc-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="be2dc-243">Zastąp hello parametry połączenia dla zmiennej globalnej connectionString hello w hello wiersza, który bezpośrednio poprzedza metody Main hello z Twojej prawidłowe parametry połączenia z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="be2dc-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="be2dc-244">To jest zmiana tylko hello należy toomake toothis kodu.</span><span class="sxs-lookup"><span data-stu-id="be2dc-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="be2dc-245">Uruchom toosee aplikacji hello zawsze zaszyfrowane w akcji.</span><span class="sxs-lookup"><span data-stu-id="be2dc-245">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
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



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="be2dc-246">Sprawdź, czy hello dane są szyfrowane</span><span class="sxs-lookup"><span data-stu-id="be2dc-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="be2dc-247">Można szybko sprawdzić szyfrowanie danych rzeczywistych hello na powitania serwera, badając hello pacjentów danych za pomocą narzędzia SSMS (przy użyciu tego połączenia gdzie **ustawienie szyfrowania kolumny** nie jest jeszcze włączona).</span><span class="sxs-lookup"><span data-stu-id="be2dc-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="be2dc-248">Uruchom następujące zapytanie w bazie danych Clinic hello hello.</span><span class="sxs-lookup"><span data-stu-id="be2dc-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="be2dc-249">Widać hello zaszyfrowanych kolumn nie zawierają żadnych danych w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="be2dc-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nową aplikację konsoli](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="be2dc-251">toouse SSMS tooaccess hello dane w postaci zwykłego tekstu, można dodać hello *ustawienie szyfrowania kolumny = włączone* parametru toohello połączenia.</span><span class="sxs-lookup"><span data-stu-id="be2dc-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="be2dc-252">W programie SSMS, kliknij prawym przyciskiem myszy serwer w **Eksplorator obiektów** i wybierz polecenie **rozłączenia**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="be2dc-253">Kliknij przycisk **Connect** > **aparatu bazy danych** tooopen hello **połączyć tooServer** i kliknij **opcje**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="be2dc-254">Kliknij przycisk **dodatkowe parametry połączenia** i typ **ustawienie szyfrowania kolumny = włączone**.</span><span class="sxs-lookup"><span data-stu-id="be2dc-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nową aplikację konsoli](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="be2dc-256">Uruchom następujące zapytanie w bazie danych Clinic hello hello.</span><span class="sxs-lookup"><span data-stu-id="be2dc-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="be2dc-257">Możesz teraz przeglądać dane w postaci zwykłego tekstu hello hello zaszyfrowanych kolumn.</span><span class="sxs-lookup"><span data-stu-id="be2dc-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nową aplikację konsoli](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="be2dc-259">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="be2dc-259">Next steps</span></span>
<span data-ttu-id="be2dc-260">Po utworzeniu bazy danych, która używa zawsze zaszyfrowane, może być toodo hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="be2dc-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="be2dc-261">[Obracanie i wyczyścić klucze](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="be2dc-262">[Migracja danych, które jest już zaszyfrowane za pomocą zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="be2dc-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="be2dc-263">Informacje pokrewne</span><span class="sxs-lookup"><span data-stu-id="be2dc-263">Related information</span></span>
* [<span data-ttu-id="be2dc-264">Zawsze zaszyfrowane (Programowanie klienta)</span><span class="sxs-lookup"><span data-stu-id="be2dc-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="be2dc-265">Niewidoczne szyfrowanie danych</span><span class="sxs-lookup"><span data-stu-id="be2dc-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="be2dc-266">SQL Server szyfrowania</span><span class="sxs-lookup"><span data-stu-id="be2dc-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="be2dc-267">Zawsze zaszyfrowane Kreatora</span><span class="sxs-lookup"><span data-stu-id="be2dc-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="be2dc-268">Blog zawsze zaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="be2dc-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

