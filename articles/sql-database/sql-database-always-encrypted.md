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
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>Zawsze zaszyfrowane: Ochrona poufnych danych w bazie danych SQL i przechowywania kluczy szyfrowania w magazynie certyfikatów systemu Windows hello

W tym artykule opisano, jak toosecure poufne dane zawarte w SQL bazy danych przy użyciu szyfrowania bazy danych przy użyciu hello [zawsze szyfrowany Kreator](https://msdn.microsoft.com/library/mt459280.aspx) w [programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Przedstawia on także sposób toostore kluczy szyfrowania w certyfikacie Windows hello przechowywania.

Zawsze zaszyfrowane jest nową technologią szyfrowania danych w bazie danych SQL Azure i programu SQL Server, która pomaga chronić poufnych danych przechowywanych na serwerze hello podczas przenoszenia między klientem a serwerem i gdy danych hello jest używany, zapewnienie poufnych danych, nigdy nie będzie wyświetlany jako zwykły tekst wewnątrz hello bazy danych systemu. Po dane są szyfrowane, tylko aplikacje klienckie lub serwery aplikacji, które mają dostęp toohello klucze mogą uzyskać dostęp do danych w postaci zwykłego tekstu. Aby uzyskać szczegółowe informacje, zobacz [zawsze zaszyfrowane (aparat bazy danych)](https://msdn.microsoft.com/library/mt163865.aspx).

Po skonfigurowaniu hello toouse bazy danych zawsze zaszyfrowane, spowoduje utworzenie aplikacji klienckiej w języku C# z programu Visual Studio toowork hello zaszyfrowanych danych.

Wykonaj kroki hello w tym artykule toolearn jak tooset się zawsze zaszyfrowane dla bazy danych Azure SQL. W tym artykule dowiesz się, jak hello tooperform następujące zadania:

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

## <a name="create-a-blank-sql-database"></a>Utwórz pustą bazę danych SQL
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **nowe** > **dane i magazyn** > **bazy danych SQL**.
3. Utwórz **puste** bazy danych o nazwie **Clinic** na nowym lub istniejącym serwerze. Aby uzyskać szczegółowe instrukcje dotyczące tworzenia bazy danych w hello portalu Azure, zobacz [pierwszą bazę danych Azure SQL](sql-database-get-started-portal.md).
   
    ![Tworzenie pustej bazy danych](./media/sql-database-always-encrypted/create-database.png)

Parametry połączenia hello trzeba będzie później w samouczku hello. Po utworzeniu bazy danych hello Przejdź toohello nowe Clinic bazy danych i skopiuj hello parametry połączenia. Można pobrać ciągu połączenia hello w dowolnym momencie, ale jest łatwe toocopy go w hello portalu Azure.

1. Kliknij przycisk **baz danych SQL** > **Clinic** > **Pokaż parametry połączenia bazy danych**.
2. Skopiuj parametry połączenia hello **ADO.NET**.
   
    ![Skopiuj parametry połączenia hello](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Połączenie bazy danych toohello z SSMS
Otwórz SSMS i połączenia z bazą danych Clinic hello toohello serwera.

1. Otwórz program SSMS. (Kliknij **Connect** > **aparatu bazy danych** tooopen hello **połączyć tooServer** okna, jeśli nie jest otwarty).
2. Wprowadź nazwę serwera i poświadczenia. Nazwa serwera Hello można znaleźć w bloku bazy danych SQL hello i w parametrach połączenia hello wcześniej zostały skopiowane. Typ hello pełną serwerów nazw, w tym *database.windows.net*.
   
    ![Skopiuj parametry połączenia hello](./media/sql-database-always-encrypted/ssms-connect.png)

Jeśli hello **nowej reguły zapory** okno, zaloguj się tooAzure i let SSMS Utwórz nową regułę zapory dla Ciebie.

## <a name="create-a-table"></a>Tworzenie tabeli
W tej sekcji utworzysz danych pacjenta toohold tabeli. Będzie to normalna tabeli początkowo — skonfiguruje szyfrowania w następnej sekcji hello.

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
SSMS udostępnia kreatora tooeasily Konfigurowanie zawsze szyfrowane przez skonfigurowanie hello CMK, CEK i zaszyfrowanych kolumn dla Ciebie.

1. Rozwiń węzeł **baz danych** > **Clinic** > **tabel**.
2. Powitania kliknij prawym przyciskiem myszy **pacjentów** tabeli i wybierz **szyfrowania kolumn** tooopen hello zawsze zaszyfrowane kreatora:
   
    ![Szyfrowania kolumn](./media/sql-database-always-encrypted/encrypt-columns.png)

Witaj zawsze zaszyfrowane Kreator zawiera następujące sekcje hello: **kolumn wybór**, **konfiguracji klucza głównego** (CMK), **weryfikacji**, i  **Podsumowanie**.

### <a name="column-selection"></a>Wybór kolumny
Kliknij przycisk **dalej** na powitania **wprowadzenie** hello tooopen strony **kolumn wybór** strony. Na tej stronie możesz wybrać kolumny, które chcesz tooencrypt, [hello typ szyfrowania i jakie klucza szyfrowania kolumny (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Szyfrowanie **SSN** i **Data urodzenia** informacje dotyczące każdego pacjenta. Witaj **SSN** kolumny użyje deterministyczne szyfrowania, który obsługuje równości wyszukiwań, sprzężeń i Grupuj według. Witaj **Data urodzenia** kolumny użyje losowego szyfrowania, który nie obsługuje operacji.

Zestaw hello **typ szyfrowania** dla hello **SSN** kolumny zbyt**Deterministic** i hello **Data urodzenia** kolumny zbyt **Wybierane**. Kliknij przycisk **Dalej**.

![Szyfrowania kolumn](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>Konfiguracja klucza głównego
Witaj **konfiguracji klucza głównego** strona jest, gdzie skonfigurować swoją CMK i dostawcy magazynu kluczy hello wybierz gdzie hello CMK będą przechowywane. Obecnie można przechowywać CMK w magazynie certyfikatów systemu Windows hello, usługi Azure Key Vault lub sprzętowego modułu zabezpieczeń (HSM). Ten samouczek pokazuje, jak toostore klucze w certyfikacie Windows hello przechowywania.

Sprawdź, czy **magazynu certyfikatów systemu Windows** jest zaznaczone, a następnie kliknij przycisk **dalej**.

![Konfiguracja klucza głównego](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>Walidacja
Można zaszyfrować kolumny hello teraz lub później zapisać toorun skrypt programu PowerShell. W tym samouczku, wybierz **teraz kontynuować toofinish** i kliknij przycisk **dalej**.

### <a name="summary"></a>Podsumowanie
Sprawdź, czy ustawienia hello są wszystkie prawidłowe, a następnie kliknij przycisk **Zakończ** toocomplete hello ustawienia zawsze szyfrowane.

![Podsumowanie](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>Sprawdź akcje hello Kreatora
Po zakończeniu pracy Kreatora hello bazy danych jest skonfigurowane dla zawsze szyfrowane. Witaj Witaj kreatora wykonywane następujące akcje:

* Utworzyć CMK.
* Utworzyć CEK.
* Skonfigurowany hello wybrane kolumny do szyfrowania. Twoje **pacjentów** tabeli obecnie nie ma danych, ale wszystkie istniejące dane w hello wybrane kolumny jest teraz zaszyfrowana.

Sprawdź hello tworzenia kluczy hello w programie SSMS, przechodząc zbyt**Clinic** > **zabezpieczeń** > **zawsze zaszyfrowane klucze**. Możesz teraz przeglądać hello nowych kluczy, które hello wygenerowany przez kreatora.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Tworzenie aplikacji klienckiej, która współdziała z hello zaszyfrowanych danych
Teraz, gdy skonfigurowano zawsze zaszyfrowane, można utworzyć aplikację, która wykonuje *wstawia* i *wybiera* na powitania zaszyfrowanych kolumn. toosuccessfully Uruchom hello przykładowej aplikacji, należy uruchomić je na powitania tym samym komputerze, na których są uruchomione hello Kreator zawsze szyfrowane. toorun aplikacji hello na innym komputerze, należy wdrożyć zawsze zaszyfrowane certyfikaty toohello komputera z systemem powitania klienta aplikacji.  

> [!IMPORTANT]
> Aplikacja musi używać [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) obiekty podczas przekazywania serwera toohello danych w postaci zwykłego tekstu z kolumnami zawsze szyfrowane. Przekazywanie wartości literałów bez przy użyciu obiektów SqlParameter spowoduje Wystąpił wyjątek.
> 
> 

1. Otwórz program Visual Studio i utworzyć nową aplikację konsoli języka C#. Upewnij się, że projekt jest ustawiona zbyt**.NET Framework 4.6** lub nowszym.
2. Nazwa projektu hello **AlwaysEncryptedConsoleApp** i kliknij przycisk **OK**.

![Nową aplikację konsoli](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modyfikowanie użytkownika tooenable ciąg połączenia zawsze zaszyfrowane
W tej sekcji opisano sposób tooenable zawsze zaszyfrowane w ciągu połączenia bazy danych. Należy zmodyfikować aplikacji konsoli hello utworzonego w następnej sekcji Witaj, "Zawsze zaszyfrowane Przykładowa aplikacja konsolowa".

tooenable zawsze zaszyfrowane, potrzebujesz tooadd hello **ustawienie szyfrowania kolumny** połączenia tooyour — słowo kluczowe string i ustaw dla niej zbyt**włączone**.

Możesz ustawić bezpośrednio w parametrach połączenia hello, lub jest on ustawiany za pomocą [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). Hello przykładowej aplikacji w hello obok sekcji przedstawiono sposób toouse **SqlConnectionStringBuilder**.

> [!NOTE]
> Jest to hello zmiany tylko w tooAlways określonych aplikacji zaszyfrowane klienta wymagane. Jeśli masz istniejącą aplikację przechowujący zewnętrznie parametrach połączenia (to znaczy w pliku konfiguracyjnym), może być możliwe tooenable zawsze zaszyfrowane bez konieczności zmieniania kodu.
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Włącz zawsze zaszyfrowane w parametrach połączenia hello
Dodaj następujące parametry połączenia tooyour — słowo kluczowe hello:

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>Włącz zawsze zaszyfrowane przy SqlConnectionStringBuilder
Witaj poniższy kod przedstawia sposób hello tooenable zawsze szyfrowane przez ustawienie [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) za[włączone](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>Zawsze zaszyfrowane Przykładowa aplikacja konsolowa
W przykładzie pokazano, jak:

* Modyfikowanie sieci tooenable ciąg połączenia zawsze szyfrowane.
* Wstawianie danych do hello zaszyfrowanych kolumn.
* Wybierz rekord filtrując określonej wartości w zaszyfrowanej kolumny.

Zamień zawartość hello **Program.cs** z hello następującego kodu. Zastąp hello parametry połączenia dla zmiennej globalnej connectionString hello w wierszu hello bezpośrednio nad hello metody Main ciągu prawidłowe połączenie z hello portalu Azure. To jest zmiana tylko hello należy toomake toothis kodu.

Uruchom toosee aplikacji hello zawsze zaszyfrowane w akcji.

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


## <a name="verify-that-hello-data-is-encrypted"></a>Sprawdź, czy hello dane są szyfrowane
Można szybko sprawdzić szyfrowanie danych rzeczywistych hello na powitania serwera, badając hello **pacjentów** danych za pomocą narzędzia SSMS. (Użyj tego połączenia gdzie ustawienie szyfrowania kolumny hello nie jest jeszcze włączone).

Uruchom następujące zapytanie w bazie danych Clinic hello hello.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Widać hello zaszyfrowanych kolumn nie zawierają żadnych danych w postaci zwykłego tekstu.

   ![Nową aplikację konsoli](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess hello dane w postaci zwykłego tekstu, można dodać hello **ustawienie szyfrowania kolumny = włączone** parametru toohello połączenia.

1. W programie SSMS, kliknij prawym przyciskiem myszy serwer w **Eksplorator obiektów**, a następnie kliknij przycisk **rozłączenia**.
2. Kliknij przycisk **Connect** > **aparatu bazy danych** tooopen hello **połączyć tooServer** okna, a następnie kliknij przycisk **opcje**.
3. Kliknij przycisk **dodatkowe parametry połączenia** i typ **ustawienie szyfrowania kolumny = włączone**.
   
    ![Nową aplikację konsoli](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. Uruchom hello następujące zapytanie na powitania **Clinic** bazy danych.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Możesz teraz przeglądać dane w postaci zwykłego tekstu hello hello zaszyfrowanych kolumn.

    ![Nową aplikację konsoli](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> Jeśli łączysz się z SSMS (lub dowolnego klienta) z innego komputera, nie będą miały klucze szyfrowania toohello dostępu i nie będą mogli toodecrypt hello danych.
> 
> 

## <a name="next-steps"></a>Następne kroki
Po utworzeniu bazy danych, która używa zawsze zaszyfrowane, może być toodo hello poniżej:

* W tym przykładzie należy uruchomić na innym komputerze. Nie ma on dostęp do kluczy szyfrowania toohello, nie ma dostępu do danych w postaci zwykłego tekstu toohello i nie będzie działać prawidłowo.
* [Obracanie i wyczyścić klucze](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migracja danych, które jest już zaszyfrowane za pomocą zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt621539.aspx).
* [Wdrażanie komputerów klienckich zawsze zaszyfrowane tooother certyfikaty](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (zobacz sekcję "TooApplications dostępnych certyfikatów i użytkowników co" hello).

## <a name="related-information"></a>Informacje pokrewne
* [Zawsze zaszyfrowane (Programowanie klienta)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Przezroczystego szyfrowania danych](https://msdn.microsoft.com/library/bb934049.aspx)
* [Szyfrowanie serwera SQL](https://msdn.microsoft.com/library/bb510663.aspx)
* [Kreator zawsze zaszyfrowane](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog zawsze zaszyfrowane](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

