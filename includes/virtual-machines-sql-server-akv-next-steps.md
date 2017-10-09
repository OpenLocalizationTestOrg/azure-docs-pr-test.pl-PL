## <a name="next-steps"></a>Następne kroki

Po włączeniu integracji magazynu kluczy Azure, programu SQL Server szyfrowanie można włączyć na maszynie Wirtualnej SQL. Najpierw należy toocreate klucza asymetrycznego wewnątrz magazynu kluczy oraz klucz symetryczny w programie SQL Server na maszynie Wirtualnej. Następnie będzie można tooexecute T-SQL instrukcje tooenable szyfrowania dla baz danych i tworzenie kopii zapasowych.

Istnieje kilka metod można korzystać z szyfrowania:

* [Przezroczystego szyfrowania danych (funkcji TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Zaszyfrowanej kopii zapasowych](https://msdn.microsoft.com/library/dn449489.aspx)
* [Szyfrowanie na poziomie kolumny (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

Witaj następujące skrypty języka Transact-SQL zawierają przykłady dla każdego z tych obszarów.

### <a name="prerequisites-for-examples"></a>Wymagania wstępne dotyczące przykłady

Każdy przykład jest oparty na powitania dwa warunki wstępne: klucza asymetrycznego z magazynu kluczy o nazwie **CONTOSO_KEY** i poświadczeń utworzonych przez funkcję Integracja hello **Azure_EKM_TDE_cred**. Witaj następujących poleceń języka Transact-SQL, należy skonfigurować te wymagania wstępne dotyczące uruchamiania hello przykłady.

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

### <a name="transparent-data-encryption-tde"></a>Przezroczystego szyfrowania danych (funkcji TDE)

1. Utwórz toobe logowania programu SQL Server, używany przez hello aparatu bazy danych dla funkcji TDE, a następnie dodaj hello tooit poświadczeń.

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

1. Utwórz hello klucza szyfrowania bazy danych, który będzie używany dla funkcji TDE.

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

### <a name="encrypted-backups"></a>Zaszyfrowanej kopii zapasowych

1. Utwórz toobe logowania programu SQL Server, używany przez hello aparatu bazy danych do szyfrowania kopii zapasowych, a następnie dodaj hello tooit poświadczeń.

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

1. Określanie szyfrowania przy użyciu klucza asymetrycznego hello przechowywane w magazynie kluczy hello hello kopii zapasowej bazy danych.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Szyfrowanie na poziomie kolumny (CLE)

Ten skrypt tworzy chroniony przez klucz asymetryczny hello w magazynie kluczy hello klucza symetrycznego, a następnie używa danych tooencrypt klucza symetrycznego hello hello bazy danych.

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

## <a name="additional-resources"></a>Dodatkowe zasoby

Aby uzyskać więcej informacji na temat toouse te funkcje szyfrowania, zobacz temat [EKM korzystanie z funkcji programu SQL Server szyfrowania](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Należy pamiętać, że hello opisanych w tym artykule założono, że istnieje już programu SQL Server uruchomionego na maszynie wirtualnej platformy Azure. Jeśli nie, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server na platformie Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Aby inne programem SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
