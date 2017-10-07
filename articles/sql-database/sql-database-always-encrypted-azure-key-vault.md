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
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a>Zawsze zaszyfrowane: Ochrona poufnych danych w bazie danych SQL i przechowywania kluczy szyfrowania w usłudze Azure Key Vault

W tym artykule opisano, jak toosecure poufne dane zawarte w SQL bazy danych przy użyciu szyfrowania danych przy użyciu hello [zawsze szyfrowany Kreator](https://msdn.microsoft.com/library/mt459280.aspx) w [programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Zawiera również instrukcje, które zawierają jak toostore każdego klucza szyfrowania w usłudze Azure Key Vault.

Zawsze zaszyfrowane to nowa technologia szyfrowania danych w bazie danych SQL Azure i programu SQL Server, która pomaga chronić poufne dane przechowywane na serwerze hello podczas przepływu między klientem a serwerem, gdy dane hello jest używany. Zawsze zaszyfrowane gwarantuje, że poufne dane nigdy nie jest wyświetlana jako zwykły tekst wewnątrz hello bazy danych systemu. Po skonfigurowaniu szyfrowania danych tylko aplikacje klienckie lub serwery aplikacji, które mają dostęp toohello kluczy można uzyskać dostępu do danych w postaci zwykłego tekstu. Aby uzyskać szczegółowe informacje, zobacz [zawsze zaszyfrowane (aparat bazy danych)](https://msdn.microsoft.com/library/mt163865.aspx).

Po skonfigurowaniu hello toouse bazy danych zawsze zaszyfrowane spowoduje utworzenie aplikacji klienckiej w języku C# z programu Visual Studio toowork hello zaszyfrowanych danych.

Wykonaj kroki hello w tym artykule i Dowiedz się, jak tooset się zawsze zaszyfrowane dla bazy danych Azure SQL. W tym artykule dowiesz się, jak hello tooperform następujące zadania:

* Użyj hello zawsze zaszyfrowane kreatora w programie SSMS toocreate [zawsze zaszyfrowane klucze](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Utwórz [klucza głównego kolumny (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Utwórz [klucza szyfrowania kolumny (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).
* Tworzenie tabeli bazy danych i szyfrowania kolumn.
* Utwórz aplikację, która wstawia, wybiera i wyświetla dane z hello zaszyfrowanych kolumn.

## <a name="prerequisites"></a>Wymagania wstępne
W tym samouczku potrzebne są:

* Konto i subskrypcja platformy Azure. Jeśli nie masz, zaloguj się do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) wersji 13.0.700.242 lub nowszej.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) lub nowszej (na komputerze klienckim hello).
* Program [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* [Program Azure PowerShell](/powershell/azure/overview), w wersji 1.0 lub nowszej. Typ **(Get-Module azure flagą-ListAvailable). Wersja** toosee jakiej wersji programu PowerShell są uruchomione.

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a>Włączanie usługi SQL Database hello tooaccess aplikacji klienta
Należy włączyć usługi baza danych SQL klienta aplikacji tooaccess hello konfigurując wymagane uwierzytelnianie hello i uzyskiwania hello *ClientId* i *klucz tajny* należy tooauthenticate Aplikacja hello następującego kodu.

1. Otwórz hello [klasycznego portalu Azure](http://manage.windowsazure.com).
2. Wybierz **usługi Active Directory** i kliknij przycisk hello wystąpienie usługi Active Directory, który będzie używany przez aplikację.
3. Kliknij przycisk **aplikacji**, a następnie kliknij przycisk **dodać**.
4. Wpisz nazwę dla aplikacji (na przykład: *myClientApp*), wybierz pozycję **aplikacji sieci WEB**i kliknij przycisk toocontinue strzałkę hello.
5. Dla hello **adres URL logowania** i **identyfikator URI aplikacji** możesz wpisać prawidłowy adres URL (na przykład *http://myClientApp*) i kontynuować.
6. Kliknij przycisk **Konfiguruj**.
7. Kopiowanie z **identyfikator klienta**. (Należy tej wartości w kodzie później.)
8. W hello **klucze** zaznacz **1 rok** z hello **wybierz czas trwania** listy rozwijanej. (Kopiowanie klucza hello zapisany w kroku 13.)
9. Przewiń w dół i kliknij przycisk **Dodaj aplikację**.
10. Pozostaw **Pokaż** ustawić także**Microsoft Apps** i wybierz **interfejs API zarządzania usługami Microsoft Azure**. Kliknij przycisk hello toocontinue znacznik wyboru.
11. Wybierz **dostęp do zarządzania usługą Azure...**  z hello **delegowane uprawnienia** listy rozwijanej.
12. Kliknij przycisk **SAVE** (Zapisz).
13. Po hello Zapisz zakończenie, skopiuj wartość klucza hello hello **klucze** sekcji. (Należy tej wartości w kodzie później.)

## <a name="create-a-key-vault-toostore-your-keys"></a>Tworzenie kluczy toostore magazyn kluczy
Skonfigurowano aplikację klienta, a masz Identyfikatora klienta, jest czas toocreate magazyn kluczy i skonfigurować jego zasady dostępu, aby aplikacji dostępnym hello magazynu kluczy tajnych (hello zawsze zaszyfrowane kluczy). Witaj *utworzyć*, *uzyskać*, *listy*, *logowania*, *Sprawdź*, *wrapKey*, i *unwrapKey* uprawnienia są wymagane do utworzenia nowego klucza głównego kolumny i konfigurowania szyfrowania za pomocą programu SQL Server Management Studio.

Może szybko utworzyć magazyn kluczy, uruchamiając hello następującego skryptu. Aby uzyskać dokładniejsze objaśnienie tych poleceń cmdlet i więcej informacji na temat tworzenia i konfigurowania magazynu kluczy, zobacz [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md).

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




## <a name="create-a-blank-sql-database"></a>Utwórz pustą bazę danych SQL
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Przejdź za**nowy** > **dane i magazyn** > **bazy danych SQL**.
3. Utwórz **puste** bazy danych o nazwie **Clinic** na nowym lub istniejącym serwerze. Aby uzyskać szczegółowe informacje o toocreate bazy danych w hello portalu Azure, zobacz temat [pierwszą bazę danych Azure SQL](sql-database-get-started-portal.md).
   
    ![Tworzenie pustej bazy danych](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

Będzie konieczne hello parametry połączenia później w samouczku hello, więc po utworzeniu bazy danych hello Przejdź toohello nowe Clinic bazy danych i skopiuj hello parametry połączenia. Można pobrać ciągu połączenia hello w dowolnym momencie, ale jest łatwe toocopy w hello portalu Azure.

1. Przejdź za**baz danych SQL** > **Clinic** > **Pokaż parametry połączenia bazy danych**.
2. Skopiuj parametry połączenia hello **ADO.NET**.
   
    ![Skopiuj parametry połączenia hello](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Połączenie bazy danych toohello z SSMS
Otwórz SSMS i połączenia z bazą danych Clinic hello toohello serwera.

1. Otwórz program SSMS. (Przejdź zbyt**Connect** > **aparatu bazy danych** tooopen hello **połączyć tooServer** okna, jeśli nie jest otwarty.)
2. Wprowadź nazwę serwera i poświadczenia. Nazwa serwera Hello można znaleźć w bloku bazy danych SQL hello i w parametrach połączenia hello wcześniej zostały skopiowane. Typ hello pełną nazwę serwera, łącznie z *database.windows.net*.
   
    ![Skopiuj parametry połączenia hello](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

Jeśli hello **nowej reguły zapory** okno, zaloguj się tooAzure i let SSMS Utwórz nową regułę zapory dla Ciebie.

## <a name="create-a-table"></a>Tworzenie tabeli
W tej sekcji utworzysz danych pacjenta toohold tabeli. Nie jest początkowo szyfrowane — skonfiguruj szyfrowania w następnej sekcji hello.

1. Rozwiń węzeł **baz danych**.
2. Kliknij prawym przyciskiem myszy hello **Clinic** bazy danych, a następnie kliknij przycisk **nowe zapytanie**.
3. Wklej powitania po języka Transact-SQL (T-SQL) do okna nowej kwerendy hello i **Execute** go.

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


## <a name="encrypt-columns-configure-always-encrypted"></a>Szyfrowania kolumn (Konfigurowanie zawsze szyfrowane)
SSMS udostępnia kreatora, który pomoże Ci łatwe konfigurowanie zawsze zaszyfrowane poprzez ustawienie klucza głównego kolumny hello, klucz szyfrowania kolumny i zaszyfrowanych kolumn dla Ciebie.

1. Rozwiń węzeł **baz danych** > **Clinic** > **tabel**.
2. Powitania kliknij prawym przyciskiem myszy **pacjentów** tabeli i wybierz **szyfrowania kolumn** tooopen hello zawsze zaszyfrowane kreatora:
   
    ![Szyfrowania kolumn](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

Witaj zawsze zaszyfrowane Kreator zawiera następujące sekcje hello: **kolumn wybór**, **konfiguracji klucza głównego**, **weryfikacji**, i **podsumowanie** .

### <a name="column-selection"></a>Wybór kolumny
Kliknij przycisk **dalej** na powitania **wprowadzenie** hello tooopen strony **kolumn wybór** strony. Na tej stronie możesz wybrać kolumny, które chcesz tooencrypt, [hello typ szyfrowania i jakie klucza szyfrowania kolumny (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Szyfrowanie **SSN** i **Data urodzenia** informacje dotyczące każdego pacjenta. Kolumna SSN Hello użyje deterministyczne szyfrowania, który obsługuje równości wyszukiwań, sprzężeń i Grupuj według. kolumny Data urodzenia Hello użyje losowego szyfrowania, który nie obsługuje operacji.

Zestaw hello **typ szyfrowania** dla kolumny hello SSN zbyt**Deterministic** i zbyt hello kolumny Data urodzenia**Randomized**. Kliknij przycisk **Dalej**.

![Szyfrowania kolumn](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a>Konfiguracja klucza głównego
Witaj **konfiguracji klucza głównego** strona jest, gdzie skonfigurować swoją CMK i dostawcy magazynu kluczy hello wybierz gdzie hello CMK będą przechowywane. Obecnie można przechowywać CMK w magazynie certyfikatów systemu Windows hello, usługi Azure Key Vault lub sprzętowego modułu zabezpieczeń (HSM).

Ten samouczek pokazuje, jak toostore klucze w usłudze Azure Key Vault.

1. Wybierz **usługi Azure Key Vault**.
2. Wybierz żądaną magazynu kluczy hello z listy rozwijanej hello.
3. Kliknij przycisk **Dalej**.

![Konfiguracja klucza głównego](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a>Walidacja
Można zaszyfrować kolumny hello teraz lub później zapisać toorun skrypt programu PowerShell. W tym samouczku, wybierz **teraz kontynuować toofinish** i kliknij przycisk **dalej**.

### <a name="summary"></a>Podsumowanie
Sprawdź, czy ustawienia hello są wszystkie prawidłowe, a następnie kliknij przycisk **Zakończ** toocomplete hello ustawienia zawsze szyfrowane.

![Podsumowanie](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a>Sprawdź akcje hello Kreatora
Po zakończeniu pracy Kreatora hello bazy danych jest skonfigurowane dla zawsze szyfrowane. Witaj Witaj kreatora wykonywane następujące akcje:

* Utworzony klucza głównego kolumny i zapisana w usłudze Azure Key Vault.
* Utworzony klucz szyfrowania kolumny i zapisana w usłudze Azure Key Vault.
* Skonfigurowany hello wybrane kolumny do szyfrowania. Tabela pacjentów Hello obecnie nie ma danych, ale wszystkie istniejące dane w hello wybrane kolumny jest teraz zaszyfrowana.

Sprawdź hello tworzenia kluczy hello w programie SSMS, rozwijając **Clinic** > **zabezpieczeń** > **zawsze zaszyfrowane klucze**.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Tworzenie aplikacji klienckiej, która współdziała z hello zaszyfrowanych danych
Teraz, gdy skonfigurowano zawsze zaszyfrowane, można utworzyć aplikację, która wykonuje *wstawia* i *wybiera* na powitania zaszyfrowanych kolumn.  

> [!IMPORTANT]
> Aplikacja musi używać [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) obiekty podczas przekazywania serwera toohello danych w postaci zwykłego tekstu z kolumnami zawsze szyfrowane. Przekazywanie wartości literałów bez przy użyciu obiektów SqlParameter spowoduje Wystąpił wyjątek.
> 
> 

1. Otwórz program Visual Studio i utworzyć nowe C# **aplikacji konsoli** (Visual Studio 2015 lub starszym) lub **aplikacji konsoli (.NET Framework)** (Visual Studio 2017 i nowsze). Upewnij się, że projekt jest ustawiona zbyt**.NET Framework 4.6** lub nowszym.
2. Nazwa projektu hello **AlwaysEncryptedConsoleAKVApp** i kliknij przycisk **OK**.
3. Zainstaluj hello następujące pakiety NuGet, przechodząc zbyt**narzędzia** > **Menedżera pakietów NuGet** > **Konsola Menedżera pakietów**.

Uruchom te dwa wiersze kodu w hello Konsola Menedżera pakietów.

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modyfikowanie użytkownika tooenable ciąg połączenia zawsze zaszyfrowane
W tej sekcji opisano sposób tooenable zawsze zaszyfrowane w ciągu połączenia bazy danych.

tooenable zawsze zaszyfrowane, potrzebujesz tooadd hello **ustawienie szyfrowania kolumny** połączenia tooyour — słowo kluczowe string i ustaw dla niej zbyt**włączone**.

Możesz ustawić bezpośrednio w parametrach połączenia hello, lub jest on ustawiany za pomocą [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). Hello przykładowej aplikacji w hello obok sekcji przedstawiono sposób toouse **SqlConnectionStringBuilder**.

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Włącz zawsze zaszyfrowane w parametrach połączenia hello
Dodaj następujące parametry połączenia tooyour — słowo kluczowe hello.

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a>Włącz zawsze zaszyfrowane przy SqlConnectionStringBuilder
Witaj następującego kodu pokazuje sposób tooenable zawsze szyfrowane przez ustawienie [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) za[włączone](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a>Zarejestruj dostawcę usługi Azure Key Vault hello
Witaj poniższy kod przedstawia sposób tooregister hello dostawcy usługi Azure Key Vault ze sterownikiem programu ADO.NET hello.

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



## <a name="always-encrypted-sample-console-application"></a>Zawsze zaszyfrowane Przykładowa aplikacja konsolowa
W przykładzie pokazano, jak:

* Modyfikowanie sieci tooenable ciąg połączenia zawsze szyfrowane.
* Rejestrowanie usługi Azure Key Vault, jako dostawcy magazynu kluczy aplikacji hello.  
* Wstawianie danych do hello zaszyfrowanych kolumn.
* Wybierz rekord filtrując określonej wartości w zaszyfrowanej kolumny.

Zamień zawartość hello **Program.cs** z hello następującego kodu. Zastąp hello parametry połączenia dla zmiennej globalnej connectionString hello w hello wiersza, który bezpośrednio poprzedza metody Main hello z Twojej prawidłowe parametry połączenia z hello portalu Azure. To jest zmiana tylko hello należy toomake toothis kodu.

Uruchom toosee aplikacji hello zawsze zaszyfrowane w akcji.

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



## <a name="verify-that-hello-data-is-encrypted"></a>Sprawdź, czy hello dane są szyfrowane
Można szybko sprawdzić szyfrowanie danych rzeczywistych hello na powitania serwera, badając hello pacjentów danych za pomocą narzędzia SSMS (przy użyciu tego połączenia gdzie **ustawienie szyfrowania kolumny** nie jest jeszcze włączona).

Uruchom następujące zapytanie w bazie danych Clinic hello hello.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Widać hello zaszyfrowanych kolumn nie zawierają żadnych danych w postaci zwykłego tekstu.

   ![Nową aplikację konsoli](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

toouse SSMS tooaccess hello dane w postaci zwykłego tekstu, można dodać hello *ustawienie szyfrowania kolumny = włączone* parametru toohello połączenia.

1. W programie SSMS, kliknij prawym przyciskiem myszy serwer w **Eksplorator obiektów** i wybierz polecenie **rozłączenia**.
2. Kliknij przycisk **Connect** > **aparatu bazy danych** tooopen hello **połączyć tooServer** i kliknij **opcje**.
3. Kliknij przycisk **dodatkowe parametry połączenia** i typ **ustawienie szyfrowania kolumny = włączone**.
   
    ![Nową aplikację konsoli](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. Uruchom następujące zapytanie w bazie danych Clinic hello hello.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Możesz teraz przeglądać dane w postaci zwykłego tekstu hello hello zaszyfrowanych kolumn.

    ![Nową aplikację konsoli](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a>Następne kroki
Po utworzeniu bazy danych, która używa zawsze zaszyfrowane, może być toodo hello poniżej:

* [Obracanie i wyczyścić klucze](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migracja danych, które jest już zaszyfrowane za pomocą zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt621539.aspx).

## <a name="related-information"></a>Informacje pokrewne
* [Zawsze zaszyfrowane (Programowanie klienta)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Niewidoczne szyfrowanie danych](https://msdn.microsoft.com/library/bb934049.aspx)
* [SQL Server szyfrowania](https://msdn.microsoft.com/library/bb510663.aspx)
* [Zawsze zaszyfrowane Kreatora](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog zawsze zaszyfrowane](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

