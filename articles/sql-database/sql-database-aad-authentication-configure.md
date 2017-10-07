---
title: "Uwierzytelnianie w usłudze Azure Active Directory aaaConfigure — SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooSQL bazy danych i usługi SQL Data Warehouse przy użyciu uwierzytelniania usługi Azure Active Directory."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Konfigurowanie i zarządzanie nimi uwierzytelniania usługi Azure Active Directory z bazą danych SQL lub SQL Data Warehouse

W tym artykule opisano sposób toocreate i wypełnić usługi Azure AD, a następnie użyć usługi Azure AD z bazy danych SQL Azure i SQL Data Warehouse. Aby uzyskać ogólne informacje, zobacz [uwierzytelniania usługi Azure Active Directory](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Łączenie tooSQL na serwerze działa na maszynie Wirtualnej platformy Azure nie jest obsługiwany przy użyciu konta usługi Azure Active Directory. Zamiast tego użyj domeny konta usługi Active Directory.

## <a name="create-and-populate-an-azure-ad"></a>Utworzyć i wypełnić usługi Azure AD
Tworzenie usługi Azure AD i wypełnić ją użytkowników i grup. Usługi Azure AD można domeny zarządzanej hello domeny początkowej usługi Azure AD. Usługi Azure AD można także lokalnych usług domenowych Active Directory, który jest Sfederowane przy użyciu hello Azure AD.

Aby uzyskać więcej informacji, zobacz [integrowanie tożsamości lokalnych z usługą Azure Active Directory](../active-directory/active-directory-aadconnect.md), [dodać własne tooAzure nazwy domeny AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure obsługuje teraz federacji z Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [administrowanie katalogiem usługi Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Zarządzanie usługą Azure AD przy użyciu programu Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), i [tożsamość hybrydowa Wymagane porty i protokoły](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>Opcjonalnie: Skojarz lub zmienić usługi active directory hello aktualnie skojarzony z subskrypcją platformy Azure
tooassociate bazy danych za pomocą katalogu hello Azure AD dla organizacji, Utwórz katalog hello zaufanego katalogu subskrypcji platformy Azure hostingu hello hello w bazie danych. Aby uzyskać więcej informacji, zobacz [Jak subskrypcje platformy Azure są kojarzone z usługą Azure Active Directory](https://msdn.microsoft.com/library/azure/dn629581.aspx).

**Informacje dodatkowe:** subskrypcji Azure co ma relację zaufania z wystąpieniem usługi Azure AD. Oznacza to, że subskrypcja ufa tooauthenticate tego katalogu użytkowników, usług i urządzeń. Wiele subskrypcji może ufać hello tym samym katalogu, ale subskrypcji ufać tylko jednemu katalogowi. Widać, katalog jest uważany za zaufany przez subskrypcję w obszarze hello **ustawienia** tab na [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Relacja zaufania między subskrypcją z katalogiem różni się od relacji hello, która ma subskrypcji z wszystkimi innymi zasobami na platformie Azure (witrynami sieci Web, baz danych i tak dalej), które przypominają bardziej podrzędne zasoby subskrypcji. Jeśli subskrypcja wygaśnie, dostęp do innych zasobów skojarzonych z subskrypcją hello toothose również nie będzie możliwy. Jednak hello katalog pozostanie na platformie Azure i można skojarzyć z nim inną subskrypcję i kontynuować toomanage hello katalogu użytkowników. Aby uzyskać więcej informacji o zasobach, zobacz [opis dostęp do zasobów na platformie Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Witaj poniższe procedury pokazują, jak toochange hello skojarzone katalogu w ramach danej subskrypcji.
1. Połącz tooyour [klasycznego portalu Azure](https://manage.windowsazure.com/) za pomocą administratora subskrypcji platformy Azure.
2. Na transparencie po lewej stronie powitania, wybierz **ustawienia**.
3. Subskrypcji są wyświetlane na ekranie Ustawienia hello. W razie potrzeby hello nie ma subskrypcji kliknij **subskrypcje** u góry hello listy rozwijanej hello **filtru przez katalog** i wybierz katalog hello, który zawiera subskrypcji, a następnie kliknij przycisk **Zastosuj**.
   
    ![Wybierz subskrypcję][4]
4. W hello **ustawienia** obszaru, kliknij subskrypcję, a następnie kliknij **Edytuj katalog** u dołu hello hello strony.
   
    ![AD ustawień portalu][5]
5. W hello **Edytuj katalog** polu, wybierz hello Azure Active Directory, który jest skojarzony z programu SQL Server lub SQL Data Warehouse, a następnie kliknij strzałkę hello następny.
   
    ![Edytuj katalog wyboru][6]
6. W hello **POTWIERDŹ** katalogu okno dialogowe Mapping, upewnij się, że "**zostaną usunięte wszystkie współadministratorów.**"
   
    ![Potwierdź katalogu edycji][7]
7. Kliknij przycisk hello wyboru tooreload hello portalu.

   > [!NOTE]
   > Podczas zmiany katalogu hello, współadministratorów tooall dostępu, usługi Azure AD użytkownicy i grupy i katalog kopii zasobu użytkownicy zostaną usunięci i mają już dostęp toothis subskrypcji lub jej zasobów. Tylko, administrator usługi, można skonfigurować dostęp dla podmiotów zabezpieczeń oparte na powitania nowego katalogu. Ta zmiana może trwać dość czasu toopropagate tooall zasobów. Zmienianie katalogu hello, również zmiany hello administratora usługi Azure AD dla bazy danych SQL i magazyn danych SQL i nie zezwalaj na dostęp do bazy danych dla wszystkich istniejących użytkowników usługi Azure AD. usługi Azure AD Witaj, Administratorze musi być resetowania (zgodnie z poniższym opisem) i nowej usługi Azure AD, użytkownicy muszą zostać utworzone.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Utwórz administrator usługi Azure AD dla serwera Azure SQL
Każdy serwer Azure SQL, (który jest hostem bazy danych SQL lub SQL Data Warehouse) rozpoczyna się od jednego serwera konta administratora, administratora hello hello całego serwera Azure SQL. Drugi administratora programu SQL Server musi zostać utworzony, który jest konto usługi Azure AD. Tego podmiotu zabezpieczeń jest tworzony jako użytkownik zawartej bazy danych w bazie danych master hello. Jako administratorów, kont administratora serwera hello są członkami hello **db_owner** roli w każdej użytkownika bazy danych, a następnie wprowadź każda baza danych użytkownika jako hello **dbo** użytkownika. Aby uzyskać więcej informacji na temat kont administratora serwera hello, zobacz [Zarządzanie bazami danych i Logowaniami w bazie danych SQL Azure](sql-database-manage-logins.md).

Podczas korzystania z usługi Azure Active Directory z replikacja geograficzna, administrator usługi Azure Active Directory hello musi być skonfigurowany zarówno hello podstawowego, jak i serwerów pomocniczych hello. Jeśli serwer nie ma administrator usługi Azure Active Directory, logowania do usługi Azure Active Directory, aby użytkownicy otrzymają komunikat o błędzie "Nie można połączyć z" tooserver.

> [!NOTE]
> Użytkowników, którzy nie są oparte na koncie usługi Azure AD (łącznie z konta administratora serwera Azure SQL hello), nie można utworzyć usługi Azure AD użytkownicy, ponieważ nie mają uprawnień toovalidate proponowane bazy danych użytkowników z hello Azure AD.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Zapewnij administrator usługi Azure Active Directory dla serwera Azure SQL

Witaj dwóch procedur przedstawionych przedstawia sposób tooprovision administratorem serwera Azure SQL w hello portalu Azure i przy użyciu programu PowerShell usługi Azure Active Directory.

### <a name="azure-portal"></a>Azure Portal
1. W hello [portalu Azure](https://portal.azure.com/), w prawym górnym rogu Witaj, kliknij przycisk toodrop Twojego połączenia w dół listę możliwych usług Active Directory. Wybierz hello Popraw usługi Active Directory jako domyślny hello Azure AD. Ten krok łącza hello subskrypcji skojarzenia z usługą Active Directory z serwerem Azure SQL, upewniając się, że hello tej samej subskrypcji jest używana zarówno dla usługi Azure AD i programu SQL Server. (hello Azure SQL server może obsługiwać, baza danych SQL Azure lub usługi Azure SQL Data Warehouse.)   
    ![Wybierz ad][8]   
    
2. W hello pozostałych wybierz Transparent **serwerów SQL**, wybierz pozycję z **programu SQL server**i następnie w hello **programu SQL Server** bloku, kliknij przycisk **administratora usługi Active Directory**.   
3. W hello **administratora usługi Active Directory** bloku, kliknij przycisk **ustawić administratora**.   
    ![Wybierz usługi active directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. W hello **dodać administratora** bloku, Wyszukaj użytkownika, wybierz hello użytkownika lub grupy toobe administrator, a następnie kliknij przycisk **wybierz**. (bloku administratora usługi Active Directory hello zawiera wszystkie elementy członkowskie i grup usługi Active Directory. Nie można wybrać użytkowników lub grup, które są wygaszone, ponieważ nie są obsługiwane jako administratorów usługi Azure AD. (Zobacz listę obsługiwanych Administratorzy w hello hello **funkcje usługi Azure AD i ograniczenia** sekcji [Użyj Azure uwierzytelnianie usługi Active Directory do uwierzytelniania przy użyciu bazy danych SQL lub SQL Data Warehouse](sql-database-aad-authentication.md).) Kontrola dostępu oparta na rolach (RBAC) dotyczy tylko portal toohello i nie jest propagowany tooSQL serwera.   
    ![Wybierz administratora](./media/sql-database-aad-authentication/select-admin.png)  
    
5. U góry hello hello **administratora usługi Active Directory** bloku, kliknij przycisk **ZAPISAĆ**.   
    ![Zapisz administratora](./media/sql-database-aad-authentication/save-admin.png)   

Witaj zmiany hello administrator może potrwać kilka minut. Następnie hello nowego administratora jest wyświetlana w hello **administratora usługi Active Directory** pole.

   > [!NOTE]
   > Podczas konfigurowania usługi Azure AD Witaj, Administratorze, hello nową nazwę administratora (użytkownik lub grupa) nie może być już dostępne w bazie danych master wirtualnego hello jako użytkownik uwierzytelniania programu SQL Server. Jeśli jest obecny, hello Azure AD administratora instalacja nie powiedzie się; Wycofywanie jej tworzenia i wskazujący tego takie jak administrator (nazwa) już istnieje. Ponieważ taki użytkownik uwierzytelniania programu SQL Server nie jest częścią hello Azure AD, dowolnego serwera toohello tooconnect nakładu pracy przy użyciu uwierzytelniania usługi Azure AD nie powiedzie się.
   > 


toolater usunąć administratora, u góry hello hello **administratora usługi Active Directory** bloku, kliknij przycisk **usunąć administratora**, a następnie kliknij przycisk **zapisać**.

### <a name="powershell"></a>PowerShell
toorun poleceń cmdlet programu PowerShell, należy toohave programu Azure PowerShell zainstalowany i uruchomiony. Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

tooprovision administratora usługi Azure AD, wykonaj hello następującego polecenia programu PowerShell systemu Azure:

* Add-AzureRmAccount
* SELECT-AzureRmSubscription

Polecenia cmdlet używane tooprovision oraz zarządzać nimi administratora usługi Azure AD:

| Nazwa polecenia cmdlet | Opis |
| --- | --- |
| [Zestaw AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Inicjuje administrator usługi Azure Active Directory dla serwera Azure SQL lub usługi Azure SQL Data Warehouse. (Musi być z bieżącej subskrypcji hello). |
| [Usuń AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Usuwa administratora usługi Azure Active Directory dla serwera Azure SQL lub usługi Azure SQL Data Warehouse. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Zwraca informacje o administrator usługi Azure Active Directory aktualnie skonfigurowanych dla serwera Azure SQL hello lub magazyn danych SQL Azure. |

Za pomocą polecenia get-help toosee więcej szczegółowych informacji dla każdego z tych poleceń, na przykład programu PowerShell ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Witaj następujące postanowienia skryptu o nazwie grupy administratorów usługi Azure AD **DBA_Group** (identyfikator obiektu `40b79501-b343-44ed-9ce7-da4c8cc7353f`) dla hello **demo_server** serwera w grupie zasobów o nazwie **grupy-23** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Witaj **DisplayName** akceptuje parametr wejściowy, nazwa wyświetlana hello Azure AD lub hello główna nazwa użytkownika. Na przykład ``DisplayName="John Smith"`` i ``DisplayName="johns@contoso.com"``. Dla usługi Azure AD grup tylko hello Azure AD Nazwa wyświetlana jest obsługiwane.

> [!NOTE]
> Witaj polecenia programu PowerShell Azure ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` nie uniemożliwiają inicjowania obsługi administracyjnej administratorów usługi Azure AD dla użytkowników nieobsługiwany. Nieobsługiwany użytkownika można udostępnić, ale nie można połączyć z tooa bazy danych. 
> 

Witaj poniższym przykładzie użyto hello opcjonalne **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Witaj w usłudze Azure AD **ObjectID** jest wymagany w przypadku hello **DisplayName** nie jest unikatowa. Witaj tooretrieve **ObjectID** i **DisplayName** wartości, za pomocą usługi Active Directory sekcji hello klasycznego portalu Azure i wyświetlić właściwości hello użytkownika lub grupy.
> 

Witaj poniższy przykład zwraca informacje na temat hello bieżącej usługi Azure AD administratora serwera Azure SQL:

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

Poniższy przykład Hello usuwa administrator usługi Azure AD:

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

Administrator usługi Azure Active Directory można również udostępniać za pomocą hello interfejsów API REST. Aby uzyskać więcej informacji, zobacz [operacje dla operacji bazy danych SQL Azure dla baz danych SQL Azure i dokumentacja interfejsu API REST usługi zarządzania](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>Interfejs wiersza polecenia  
Administrator usługi Azure AD można również udostępniać przez wywołanie hello następujące polecenia interfejsu wiersza polecenia:
| Polecenie | Opis |
| --- | --- |
|[Tworzenie serwera sql az ad — administrator](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Inicjuje administrator usługi Azure Active Directory dla serwera Azure SQL lub usługi Azure SQL Data Warehouse. (Musi być z bieżącej subskrypcji hello). |
|[Usuń ad administratora serwera sql az](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Usuwa administratora usługi Azure Active Directory dla serwera Azure SQL lub usługi Azure SQL Data Warehouse. |
|[Lista ad administratora serwera sql az](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Zwraca informacje o administrator usługi Azure Active Directory aktualnie skonfigurowanych dla serwera Azure SQL hello lub magazyn danych SQL Azure. |
|[Aktualizacja ad administratora programu sql server az](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Aktualizuje hello administratora usługi Active Directory dla serwera Azure SQL lub usługi Azure SQL Data Warehouse. |

Aby uzyskać więcej informacji na temat poleceń interfejsu wiersza polecenia, zobacz [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>Konfigurowanie komputerów klienckich
Na wszystkich komputerach klienckich, z których aplikacje lub użytkowników połączenie tooAzure bazy danych SQL lub magazyn danych SQL Azure przy użyciu tożsamości usługi Azure AD, należy zainstalować hello następującego oprogramowania:

* .NET framework 4.6 lub nowszy z [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* Azure Active Directory Authentication Library dla programu SQL Server (**ADALSQL. Biblioteki DLL**) są dostępne w wielu językach (x x86 i amd64) z Centrum pobierania hello [Microsoft Active Directory Authentication Library dla programu Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

Można spełnienia tych wymagań:

* Zainstalowanie dowolnej [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) lub [programu SQL Server Data Tools dla programu Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) spełnia hello wymaganie programu .NET Framework 4.6.
* SSMS instaluje wersję hello x86 **ADALSQL. Biblioteki DLL**.
* Program SSDT instaluje wersję amd64 hello **ADALSQL. Biblioteki DLL**.
* Witaj najnowsze Visual Studio z [Visual Studio pobiera](https://www.visualstudio.com/downloads/download-visual-studio-vs) spełnia wymagania hello .NET Framework 4.6, ale nie instaluje wersję wymagane amd64 hello **ADALSQL. Biblioteki DLL**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Utwórz użytkowników zawartej bazy danych w sieci tooAzure zamapować bazy danych tożsamości usługi AD

Uwierzytelnianie usługi Active Directory systemu Azure wymaga bazy danych użytkowników toobe utworzony jako użytkowników zawartej bazy danych. Użytkownik zawartej bazy danych na podstawie tożsamości usługi Azure AD jest użytkownika bazy danych, która nie ma nazwy logowania w bazie danych master hello i tożsamość tooan mapy w hello katalogu usługi Azure AD, który jest skojarzony z hello bazy danych. Witaj tożsamości usługi Azure AD może być indywidualne konto użytkownika lub grupę. Aby uzyskać więcej informacji dotyczących użytkowników zawartej bazy danych, zobacz [zawartych użytkowników bazy danych — wprowadzanie Your przenośne bazy danych](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Nie można utworzyć bazy danych użytkowników (z wyjątkiem hello administratorów) za pomocą portalu. Role RBAC nie są propagowany tooSQL serwera, SQL Database lub SQL Data Warehouse. Role RBAC Azure są używane do zarządzania zasobami Azure i nie stosuj uprawnień toodatabase. Na przykład Witaj **programu SQL Server współautora** roli nie powoduje przyznania dostępu tooconnect toohello SQL Database lub SQL Data Warehouse. uprawnienia dostępu Hello musi otrzymać bezpośrednio w hello bazy danych przy użyciu instrukcji języka Transact-SQL.
>

co najmniej hello Azure AD na podstawie zawarte bazy danych użytkownika (inne niż hello administrator serwera, który jest właścicielem hello bazy danych), połączenie toohello bazy danych przy użyciu tożsamości usługi Azure AD jako użytkownik z toocreate **ALTER dowolny użytkownik** uprawnienia. Następnie użyj hello składni języka Transact-SQL:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* może być hello nazwy głównej użytkownika usługi Azure AD użytkownika lub hello nazwę wyświetlaną grupy usługi Azure AD.

**Przykłady:** toocreate użytkownika zawartej bazy danych usługi Azure AD reprezentująca federacyjni lub zarządzani użytkownika domeny:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate reprezentujący usługi Azure AD lub grupy domeny federacyjnej użytkownika zawartej bazy danych Podaj nazwę wyświetlaną hello grupy zabezpieczeń:
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate użytkowników zawartej bazy danych, reprezentujący aplikacji, która łączy się przy użyciu tokenu usługi Azure AD:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  Nie można bezpośrednio utworzyć użytkownika z usługi Azure Active Directory niż hello Azure Active Directory, który jest skojarzony z subskrypcją platformy Azure. Jednak członkami innych katalogów Active, które są importowane użytkowników w hello skojarzone usługi Active Directory (nazywane użytkowników zewnętrznych) można dodać grupy usługi Active Directory tooan w dzierżawie powitalnych usługi Active Directory. Tworząc użytkownika zawartej bazy danych dla tej grupy AD hello użytkownikom hello zewnętrznej usługi Active Directory mogą uzyskać tooSQL dostępu do bazy danych.   

Aby uzyskać więcej informacji o tworzeniu zawarte bazy danych użytkowników na podstawie tożsamości usługi Azure Active Directory, zobacz [Tworzenie użytkownika (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Usuwania hello administratora usługi Azure Active Directory dla usługi Azure SQL server zapobiega łączenia serwera toohello każdy użytkownik uwierzytelniania usługi Azure AD. Jeśli to konieczne, korzystanie z niej użytkowników usługi Azure AD można usunąć ręcznie przez administratora bazy danych SQL.   

>  [!NOTE]
>  Jeśli zostanie wyświetlony **upłynął limit czasu połączenia**, może być konieczne tooset hello `TransparentNetworkIPResolution` parametru toofalse ciąg połączenia hello. Aby uzyskać więcej informacji, zobacz [problem limitu czasu połączenia z platformy .NET Framework 4.6.1 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).   

   
Podczas tworzenia użytkownika bazy danych, użytkownik otrzymuje hello **CONNECT** uprawnień i mogą łączyć się toothat bazy danych będące członkiem hello **publicznego** roli. Początkowo hello tylko uprawnienia użytkownika toohello dostępne są wszystkie uprawnienia przyznane toohello **publicznego** roli lub uprawnienia przyznane tooany grup systemu Windows są członkami. Po zainicjowaniu obsługi administracyjnej usługi Azure AD na podstawie zawarte bazy danych użytkownika, hello użytkownika dodatkowe uprawnienia można przyznać hello sam sposób, jak można przyznać uprawnień tooany innego typu użytkownika. Zazwyczaj uprawnienia toodatabase ról, a następnie dodaj tooroles użytkowników. Aby uzyskać więcej informacji, zobacz [podstawy uprawnień aparatu bazy danych](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx). Aby uzyskać więcej informacji na temat specjalne role bazy danych SQL, zobacz [Zarządzanie bazami danych i Logowaniami w bazie danych SQL Azure](sql-database-manage-logins.md).
Użytkownik domeny federacyjnej, który jest importowany do domeny zarządzania, musi używać tożsamości domeny hello zarządzane.

> [!NOTE]
> Użytkownicy usługi Azure AD są oznaczone w metadanych bazy danych hello z typem E (EXTERNAL_USER) i grupy typu X (EXTERNAL_GROUPS). Aby uzyskać więcej informacji, zobacz [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>Połącz przy użyciu narzędzia SSMS lub program SSDT toohello użytkownika bazy danych lub dane magazynu  
tooconfirm hello Azure AD administratora jest poprawnie skonfigurowana, Połącz toohello **wzorca** bazy danych przy użyciu konta administratora hello Azure AD.
tooprovision Azure AD na podstawie zawarte bazy danych użytkownika (inne niż hello administrator serwera, który jest właścicielem hello bazy danych), połączenie toohello bazy danych przy użyciu tożsamości usługi Azure AD, który ma toohello dostępu do bazy danych.

> [!IMPORTANT]
> Obsługa uwierzytelniania usługi Azure Active Directory jest dostępny z [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) i [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) w programie Visual Studio 2015. Witaj sierpnia 2016 wersji programu SSMS obejmuje również obsługę uniwersalnych uwierzytelnianie usługi Active Directory, dzięki czemu administratorzy toorequire za pomocą rozmowy telefonicznej, wiadomości tekstowej, karty inteligentne z numeru pin lub powiadomienie aplikacji mobilnej usługi Multi-Factor Authentication.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>Przy użyciu tooconnect tożsamości usługi Azure AD przy użyciu narzędzia SSMS lub program SSDT  

Hello zgodnie z procedurami pokazują, jak tooconnect tooa SQL bazy danych przy użyciu tożsamości usługi Azure AD przy użyciu programu SQL Server Management Studio lub narzędzia bazy danych programu SQL Server.

### <a name="active-directory-integrated-authentication"></a>Zintegrowane uwierzytelnianie usługi Active Directory

Użyj tej metody, jeśli użytkownik jest zalogowany w tooWindows z domeny federacyjnej przy użyciu poświadczeń usługi Azure Active Directory.

1. Uruchom Management Studio lub narzędzia danych w hello **połączyć tooServer** (lub **połączyć tooDatabase aparat**) okno dialogowe, w hello **uwierzytelniania** wybierz **Usługi active Directory — zintegrowane**. Hasło nie jest potrzebne lub można wprowadzić, ponieważ istniejących poświadczeń zostanie wyświetlone powitalne połączenia.   

    ![Wybierz opcję zintegrowanego uwierzytelniania AD][11]
2. Kliknij hello **opcje** przycisku i na powitania **właściwości połączenia** strony w hello **połączyć toodatabase** okno, nazwa typu hello hello bazy danych użytkowników ma tooconnect Aby. (hello **Identyfikatora nazwy lub dzierżawy domeny AD**"opcja jest obsługiwana tylko dla **uniwersalnych z połączeniem MFA** opcje, w przeciwnym razie on jest nieaktywna.)  

    ![Wybierz nazwę bazy danych hello][13]

## <a name="active-directory-password-authentication"></a>Uwierzytelnianie hasłem usługi Active Directory

Użyj tej metody, podczas nawiązywania połączenia z głównej nazwy usługi Azure AD przy użyciu usługi Azure AD hello zarządzanych domeny. Można również użyć do kontem federacyjnym bez dostępu toohello domeny, na przykład podczas pracy zdalnej.

Użyj tej metody, jeśli użytkownik jest zalogowany przy użyciu poświadczeń z domeny, która nie jest zintegrowany z platformy Azure, tooWindows lub korzystając z usługi Azure AD uwierzytelnianie przy użyciu usługi Azure AD oparte na powitania początkowej lub hello domeny klienta.

1. Uruchom Management Studio lub narzędzia danych w hello **połączyć tooServer** (lub **połączyć tooDatabase aparat**) okno dialogowe, w hello **uwierzytelniania** wybierz **Usługi active Directory — hasło**.
2. W hello **nazwy użytkownika** wpisz nazwę użytkownika usługi Azure Active Directory w formacie hello  **username@domain.com** . Musi to być konto z hello Azure Active Directory lub konta z domeny wykonana Federacja z hello Azure Active Directory.
3. W hello **hasło** wpisz hasło użytkownika dla konta usługi Azure Active Directory hello lub konta domeny federacyjnej.

    ![Wybierz uwierzytelnianie hasłem usługi AD][12]
4. Kliknij hello **opcje** przycisku i na powitania **właściwości połączenia** strony w hello **połączyć toodatabase** okno, nazwa typu hello hello bazy danych użytkowników ma tooconnect Aby. (Zobacz hello grafiki w poprzedniej opcji hello).

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>Za pomocą usługi Azure AD tooconnect tożsamości od aplikacji klienta

Hello zgodnie z procedurami pokazują, jak tooconnect tooa SQL bazy danych przy użyciu tożsamości usługi Azure AD z aplikacji klienta.

###  <a name="active-directory-integrated-authentication"></a>Zintegrowane uwierzytelnianie usługi Active Directory

toouse zintegrowane uwierzytelnianie systemu Windows, Twojej domeny usługi Active Directory musi Sfederowanych z usługą Azure Active Directory. Aplikacja kliencka (lub usługi), połączenie toohello bazy danych musi działać na komputerze przyłączonym do domeny z poświadczeniami użytkownika domeny.

przy użyciu bazy danych tooa tooconnect zintegrowane uwierzytelnianie i tożsamość usługi Azure AD, należy ustawić hello uwierzytelniania — słowo kluczowe w ciągu połączenia bazy danych hello tooActive Directory Integrated. Witaj poniższy przykład kodu C# używa ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Witaj słowo kluczowe parametrów połączenia ``Integrated Security=True`` nie jest obsługiwana dla łączenia tooAzure bazy danych SQL. Podczas tworzenia połączenia ODBC, będzie konieczne tooremove spacji i ustaw too'ActiveDirectoryIntegrated uwierzytelniania ".

### <a name="active-directory-password-authentication"></a>Uwierzytelnianie hasłem usługi Active Directory

przy użyciu bazy danych tooa tooconnect zintegrowane uwierzytelnianie i tożsamość usługi Azure AD, hello uwierzytelniania — słowo kluczowe musi być ustawiona tooActive hasła katalogu. Parametry połączenia Hello musi zawierać identyfikator/UID użytkownika i hasło/PWD słowa kluczowe i wartości. Witaj poniższy przykład kodu C# używa ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Dowiedz się więcej na temat metod uwierzytelniania usługi Azure AD przy użyciu przykłady kodu pokaz hello dostępne pod adresem [pokaz GitHub uwierzytelniania w usłudze Azure AD](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Token usługi Azure AD
Ta metoda uwierzytelniania umożliwia tooAzure tooconnect warstwy środkowej usługi SQL Database lub magazyn danych SQL Azure, uzyskując tokenu z usługi Azure Active Directory (AAD). Umożliwia zaawansowane scenariusze, w tym uwierzytelniania opartego na certyfikatach. Należy wykonać cztery podstawowe kroki toouse usługi Azure AD token uwierzytelniania:

1. Zarejestrować aplikację w usłudze Azure Active Directory i uzyskać identyfikator klienta hello na kodzie. 
2. Tworzenie bazy danych użytkownika reprezentujące hello aplikacji. (Ukończono wcześniej w kroku 6).
3. Utwórz certyfikat na powitania klienta komputer działa aplikacja hello.
4. Aby dodać certyfikat hello jako klucz dla aplikacji.

Przykładowy ciąg połączenia:

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Aby uzyskać więcej informacji, zobacz [Blog zabezpieczeń programu SQL Server](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).

### <a name="sqlcmd"></a>sqlcmd

Witaj następujące instrukcje, Połącz przy użyciu narzędzia sqlcmd, który jest dostępny z hello wersji 13.1 [Centrum pobierania](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Następne kroki
- Dostęp i kontrola w usłudze SQL Database zostały omówione w temacie [Kontrola dostępu w usłudze SQL Database](sql-database-control-access.md).
- Dane logowania, użytkownicy i role bazy danych w usłudze SQL Database zostały omówione w temacie [Logins, users, and database roles](sql-database-manage-logins.md) (Dane logowania, użytkownicy i role bazy danych).
- Aby uzyskać więcej informacji na temat podmiotów zabezpieczeń bazy danych, zobacz [Principals](https://msdn.microsoft.com/library/ms181127.aspx) (Podmioty zabezpieczeń).
- Aby uzyskać więcej informacji na temat ról bazy danych, zobacz [Database roles](https://msdn.microsoft.com/library/ms189121.aspx) (Role bazy danych).
- Aby uzyskać więcej informacji na temat reguł zapory w usłudze SQL Database, zobacz [Omówienie reguł zapory usługi SQL Database](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

