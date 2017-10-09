## <a name="next-steps"></a><span data-ttu-id="4812d-101">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4812d-101">Next steps</span></span>

<span data-ttu-id="4812d-102">Po włączeniu integracji magazynu kluczy Azure, programu SQL Server szyfrowanie można włączyć na maszynie Wirtualnej SQL.</span><span class="sxs-lookup"><span data-stu-id="4812d-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="4812d-103">Najpierw należy toocreate klucza asymetrycznego wewnątrz magazynu kluczy oraz klucz symetryczny w programie SQL Server na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4812d-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="4812d-104">Następnie będzie można tooexecute T-SQL instrukcje tooenable szyfrowania dla baz danych i tworzenie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="4812d-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="4812d-105">Istnieje kilka metod można korzystać z szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="4812d-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="4812d-106">Przezroczystego szyfrowania danych (funkcji TDE)</span><span class="sxs-lookup"><span data-stu-id="4812d-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="4812d-107">Zaszyfrowanej kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="4812d-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="4812d-108">Szyfrowanie na poziomie kolumny (CLE)</span><span class="sxs-lookup"><span data-stu-id="4812d-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="4812d-109">Witaj następujące skrypty języka Transact-SQL zawierają przykłady dla każdego z tych obszarów.</span><span class="sxs-lookup"><span data-stu-id="4812d-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="4812d-110">Wymagania wstępne dotyczące przykłady</span><span class="sxs-lookup"><span data-stu-id="4812d-110">Prerequisites for examples</span></span>

<span data-ttu-id="4812d-111">Każdy przykład jest oparty na powitania dwa warunki wstępne: klucza asymetrycznego z magazynu kluczy o nazwie **CONTOSO_KEY** i poświadczeń utworzonych przez funkcję Integracja hello **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="4812d-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="4812d-112">Witaj następujących poleceń języka Transact-SQL, należy skonfigurować te wymagania wstępne dotyczące uruchamiania hello przykłady.</span><span class="sxs-lookup"><span data-stu-id="4812d-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

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

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="4812d-113">Przezroczystego szyfrowania danych (funkcji TDE)</span><span class="sxs-lookup"><span data-stu-id="4812d-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="4812d-114">Utwórz toobe logowania programu SQL Server, używany przez hello aparatu bazy danych dla funkcji TDE, a następnie dodaj hello tooit poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="4812d-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="4812d-115">Utwórz hello klucza szyfrowania bazy danych, który będzie używany dla funkcji TDE.</span><span class="sxs-lookup"><span data-stu-id="4812d-115">Create hello database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="4812d-116">Zaszyfrowanej kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="4812d-116">Encrypted backups</span></span>

1. <span data-ttu-id="4812d-117">Utwórz toobe logowania programu SQL Server, używany przez hello aparatu bazy danych do szyfrowania kopii zapasowych, a następnie dodaj hello tooit poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="4812d-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="4812d-118">Określanie szyfrowania przy użyciu klucza asymetrycznego hello przechowywane w magazynie kluczy hello hello kopii zapasowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4812d-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="4812d-119">Szyfrowanie na poziomie kolumny (CLE)</span><span class="sxs-lookup"><span data-stu-id="4812d-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="4812d-120">Ten skrypt tworzy chroniony przez klucz asymetryczny hello w magazynie kluczy hello klucza symetrycznego, a następnie używa danych tooencrypt klucza symetrycznego hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4812d-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="4812d-121">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4812d-121">Additional resources</span></span>

<span data-ttu-id="4812d-122">Aby uzyskać więcej informacji na temat toouse te funkcje szyfrowania, zobacz temat [EKM korzystanie z funkcji programu SQL Server szyfrowania](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="4812d-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="4812d-123">Należy pamiętać, że hello opisanych w tym artykule założono, że istnieje już programu SQL Server uruchomionego na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4812d-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="4812d-124">Jeśli nie, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server na platformie Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="4812d-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="4812d-125">Aby inne programem SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4812d-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
