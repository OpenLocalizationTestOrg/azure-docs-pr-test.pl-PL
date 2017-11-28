## <a name="next-steps"></a><span data-ttu-id="ed8da-101">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ed8da-101">Next steps</span></span>

<span data-ttu-id="ed8da-102">Po włączeniu integracji magazynu kluczy Azure, programu SQL Server szyfrowanie można włączyć na maszynie Wirtualnej SQL.</span><span class="sxs-lookup"><span data-stu-id="ed8da-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="ed8da-103">Najpierw należy utworzyć klucz asymetryczny wewnątrz magazynu kluczy oraz klucz symetryczny w programie SQL Server na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ed8da-103">First, you will need to create an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="ed8da-104">Następnie można wykonać instrukcje T-SQL, aby włączyć szyfrowanie dla baz danych i tworzenie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ed8da-104">Then, you will be able to execute T-SQL statements to enable encryption for your databases and backups.</span></span>

<span data-ttu-id="ed8da-105">Istnieje kilka metod można korzystać z szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="ed8da-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="ed8da-106">Przezroczystego szyfrowania danych (funkcji TDE)</span><span class="sxs-lookup"><span data-stu-id="ed8da-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="ed8da-107">Zaszyfrowanej kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="ed8da-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="ed8da-108">Szyfrowanie na poziomie kolumny (CLE)</span><span class="sxs-lookup"><span data-stu-id="ed8da-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="ed8da-109">Następujące skrypty języka Transact-SQL zawierają przykłady dla każdego z tych obszarów.</span><span class="sxs-lookup"><span data-stu-id="ed8da-109">The following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="ed8da-110">Wymagania wstępne dotyczące przykłady</span><span class="sxs-lookup"><span data-stu-id="ed8da-110">Prerequisites for examples</span></span>

<span data-ttu-id="ed8da-111">Każdy przykład jest oparty na dwóch wymagań wstępnych: klucza asymetrycznego z magazynu kluczy o nazwie **CONTOSO_KEY** i wywołać poświadczenie utworzona przez funkcję Integracja **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="ed8da-111">Each example is based on the two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by the AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="ed8da-112">Następujące polecenia języka Transact-SQL, należy skonfigurować te wymagania wstępne dotyczące uruchamiania przykładów.</span><span class="sxs-lookup"><span data-stu-id="ed8da-112">The following Transact-SQL commands setup these prerequisites for running the examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="ed8da-113">Przezroczystego szyfrowania danych (funkcji TDE)</span><span class="sxs-lookup"><span data-stu-id="ed8da-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="ed8da-114">Utwórz dane logowania programu SQL Server używanego przez aparat bazy danych dla funkcji TDE, a następnie Dodaj poświadczenia do niej.</span><span class="sxs-lookup"><span data-stu-id="ed8da-114">Create a SQL Server login to be used by the Database Engine for TDE, then add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the TDE Login to add the credential for use by the
   -- Database Engine to access the key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="ed8da-115">Utwórz klucz szyfrowania bazy danych, który będzie używany dla funkcji TDE.</span><span class="sxs-lookup"><span data-stu-id="ed8da-115">Create the database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the database to enable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="ed8da-116">Zaszyfrowanej kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="ed8da-116">Encrypted backups</span></span>

1. <span data-ttu-id="ed8da-117">Utwórz dane logowania programu SQL Server używanego przez aparat bazy danych do szyfrowania kopii zapasowych, a następnie Dodaj poświadczenia do niej.</span><span class="sxs-lookup"><span data-stu-id="ed8da-117">Create a SQL Server login to be used by the Database Engine for encrypting backups, and add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it is encrypting the backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the Encrypted Backup Login to add the credential for use by
   -- the Database Engine to access the key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="ed8da-118">Kopia zapasowa szyfrowania Określanie bazy danych przy użyciu klucza asymetrycznego przechowywane w magazynie kluczy.</span><span class="sxs-lookup"><span data-stu-id="ed8da-118">Backup the database specifying encryption with the asymmetric key stored in the key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   TO DISK = N'[PATH TO BACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="ed8da-119">Szyfrowanie na poziomie kolumny (CLE)</span><span class="sxs-lookup"><span data-stu-id="ed8da-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="ed8da-120">Ten skrypt tworzy klucza symetrycznego chronione za pomocą klucza asymetrycznego w magazynie kluczy, a następnie używa klucza symetrycznego do szyfrowania danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="ed8da-120">This script creates a symmetric key protected by the asymmetric key in the key vault, and then uses the symmetric key to encrypt data in the database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open the symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close the symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="ed8da-121">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ed8da-121">Additional resources</span></span>

<span data-ttu-id="ed8da-122">Aby uzyskać więcej informacji na temat sposobu korzystania z tych funkcji szyfrowania, zobacz [EKM korzystanie z funkcji programu SQL Server szyfrowania](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="ed8da-122">For more information on how to use these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="ed8da-123">Należy pamiętać, że kroki opisane w tym artykule założono, że już istnieje na serwerze SQL działa na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8da-123">Note that the steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="ed8da-124">Jeśli nie, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server na platformie Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ed8da-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="ed8da-125">Aby inne programem SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed8da-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>