---
title: "Tworzenie środowiska uruchomieniowego integracji usług SSIS Azure w fabryce danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć środowiska uruchomieniowego integracji usług SSIS Azure, dzięki czemu można uruchomić pakiet SSIS w chmurze Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/22/2018
ms.author: spelluru
ms.openlocfilehash: 6eec344761df67fd8e8b3c6fceedb8ee68e85b9a
ms.sourcegitcommit: 99d29d0aa8ec15ec96b3b057629d00c70d30cfec
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="create-an-azure-ssis-integration-runtime-in-azure-data-factory"></a>Tworzenie środowiska uruchomieniowego integracji usług SSIS Azure w fabryce danych Azure
Ten artykuł zawiera kroki do inicjowania obsługi środowiska uruchomieniowego integracji usług SSIS Azure w fabryce danych Azure. Następnie możesz użyć programu SQL Server Data Tools (SSDT) lub SQL Server Management Studio (SSMS) do wdrożenia pakietów usług SQL Server Integration Services (SSIS) w tym środowisku uruchomieniowym na platformie Azure.

Samouczek: [samouczek: Wdrażanie pakietów usług SQL Server Integration Services (SSIS) na platformie Azure](tutorial-deploy-ssis-packages-azure.md) pokazano, jak utworzyć środowiska uruchomieniowego integracji usług SSIS Azure (IR) przy użyciu bazy danych SQL Azure do przechowywania dla katalogu usług SSIS. W tym artykule rozszerzenie samouczka i pokazuje, jak wykonać następujące czynności: 

- Używać wystąpienia zarządzane Azure SQL (wersja zapoznawcza prywatne) do obsługi katalogu SSIS (baza danych usług SSIS).
- Dołącz IR Azure SSIS do sieci wirtualnej platformy Azure (VNet). Aby uzyskać informacje koncepcyjne na dołączenie IR Azure SSIS do sieci wirtualnej i konfigurowanie sieci wirtualnej w portalu Azure, zobacz [Join IR Azure SSIS do sieci wirtualnej](join-azure-ssis-integration-runtime-virtual-network.md). 

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz dostępnej ogólnie wersji 1 usługi Data Factory, zobacz [dokumentację dotyczącą usługi Data Factory w wersji 1](v1/data-factory-introduction.md).


## <a name="overview"></a>Przegląd
W tym artykule przedstawiono różne sposoby udostępniania IR Azure SSIS:

- [Azure portal](#azure-portal)
- [Azure PowerShell](#azure-powershell)
- [Szablon usługi Azure Resource Manager](#azure-resource-manager-template)

Po utworzeniu IR Azure SSIS fabryki danych łączy się z bazy danych SQL Azure do przygotowania bazy danych usług SSIS katalogu (SSISDB). Skrypt konfiguruje również uprawnienia i ustawienia Twojej sieci wirtualnej, jeśli zostanie określona, i dołącza nowe wystąpienie środowiska Azure SSIS Integration Runtime do sieci wirtualnej.

Podczas obsługi administracyjnej wystąpienie usług SSIS Azure IR, instalowane są również Azure Feature Pack SSIS i pakiet redystrybucyjny programu Access. Te składniki zapewniają łączność programów Excel i dostęp do plików i różnych źródeł danych Azure, oprócz źródeł danych obsługiwane przez wbudowane składniki. W tym momencie (w tym składników innych firm firmy Microsoft, takich jak składniki Oracle i Teradata attunity i SAP BI), nie można zainstalować składników innych firm dla usług SSIS.

## <a name="prerequisites"></a>Wymagania wstępne

- **Subskrypcja platformy Azure**. Jeśli nie masz subskrypcji, możesz utworzyć konto [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/).
- **Serwer usługi Azure SQL Database** lub **zarządzane wystąpienie programu SQL Server (prywatna wersja zapoznawcza) (rozszerzona prywatna wersja zapoznawcza)**. Jeśli nie masz jeszcze serwera bazy danych, utwórz go w witrynie Azure Portal, zanim zaczniesz. Ten serwer hostuje bazę danych katalogu usług SSIS (SSISDB). Zaleca się utworzenie serwera bazy danych w tym samym regionie platformy Azure, co środowisko Integration Runtime. Ta konfiguracja pozwala środowisku Integration Runtime zapisywać dzienniki wykonywania SSISDB bez wykraczania poza granice regionów świadczenia usług platformy Azure. Zapamiętaj warstwy cenowej serwera Azure SQL. Aby uzyskać listę obsługiwanych warstw cenowych bazy danych SQL Azure, zobacz [limity zasobów bazy danych SQL](../sql-database/sql-database-resource-limits.md).

    Upewnij się, że serwer bazy danych SQL Azure lub zarządzane wystąpienie programu SQL Server (rozszerzonej podglądzie prywatnym) nie ma katalogu SSIS (SSIDB bazy danych). Inicjowanie obsługi administracyjnej IR Azure SSIS nie obsługuje przy użyciu istniejącego katalogu usług SSIS.
- **Klasycznym lub usługi Azure Resource Manager wirtualnego Network(VNet) (opcjonalnie)**. Jeśli co najmniej jeden z poniższych warunków jest spełniony, musisz mieć sieć Azure Virtual Network:
    - Hostujesz bazę danych katalogu usług SSIS na wystąpieniu zarządzanym programu SQL Server (prywatna wersja zapoznawcza), który jest częścią sieci wirtualnej.
    - Chcesz połączyć się z lokalnymi magazynami danych z pakietów usług SSIS działającymi w środowisku Azure SSIS Integration Runtime.
- Zainstalowanie programu **Azure PowerShell**. Wykonaj instrukcje podane w temacie [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/install-azurerm-ps). Program PowerShell służy do uruchamiania skryptu w celu aprowizacji środowiska Azure SSIS Integration Runtime, które uruchamia pakiety SSIS w chmurze. 

> [!NOTE]
> Aby uzyskać listę regionów obsługiwanych przez usługę Azure Data Factory w wersji 2 i środowisko Azure SSIS Integration Runtime, zobacz [Dostępność produktów według regionów](https://azure.microsoft.com/regions/services/). Rozwiń pozycję **Dane + analiza**, aby wyświetlić usługi **Data Factory V2** i **SSIS Integration Runtime**.

## <a name="azure-portal"></a>Azure Portal
W tej sekcji Użyj portalu Azure, w szczególności danych fabryki interfejsu użytkownika, można utworzyć IR. Azure SSIS 

### <a name="create-a-data-factory"></a>Tworzenie fabryki danych

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).    
2. Kliknij przycisk **Nowy** w lewym menu, kliknij pozycję **Dane + analiza**, a następnie kliknij pozycję **Data Factory**. 
   
   ![Nowy-> Fabryka danych](./media/tutorial-create-azure-ssis-runtime-portal/new-data-factory-menu.png)
3. Na stronie **Nowa fabryka danych** wprowadź jako **nazwę** wartość **MyAzureSsisDataFactory**. 
      
     ![Strona Nowa fabryka danych](./media/tutorial-create-azure-ssis-runtime-portal/new-azure-data-factory.png)
 
   Nazwa fabryki danych platformy Azure musi być **globalnie unikatowa**. Jeśli wystąpi poniższy błąd, zmień nazwę fabryki danych (np. twojanazwaMyAzureSsisDataFactory) i spróbuj utworzyć ją ponownie. Artykuł [Data Factory — Naming Rules (Usługa Data Factory — reguły nazewnictwa)](naming-rules.md) zawiera reguły nazewnictwa artefaktów usługi Data Factory.
  
       `Data factory name “MyAzureSsisDataFactory” is not available`
3. Wybierz **subskrypcję** Azure, w której chcesz utworzyć fabrykę danych. 
4. Dla opcji **Grupa zasobów** wykonaj jedną z następujących czynności:
     
      - Wybierz pozycję **Użyj istniejącej**, a następnie wybierz istniejącą grupę zasobów z listy rozwijanej. 
      - Wybierz pozycję **Utwórz nową**, a następnie wprowadź nazwę grupy zasobów.   
         
      Informacje na temat grup zasobów znajdują się w artykule [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md) (Używanie grup zasobów do zarządzania zasobami platformy Azure).  
4. Wybierz wartość **V2 (wersja zapoznawcza)** dla **wersji**.
5. Na liście **lokalizacja** wybierz lokalizację fabryki danych. Na liście są wyświetlane tylko lokalizacje obsługiwane na potrzeby tworzenia fabryk danych.
6. Wybierz opcję **Przypnij do pulpitu nawigacyjnego**.     
7. Kliknij przycisk **Utwórz**.
8. Na pulpicie nawigacyjnym jest widoczny następujący kafelek ze stanem: **Wdrażanie fabryki danych**. 

    ![kafelek Wdrażanie fabryki danych](media/tutorial-create-azure-ssis-runtime-portal/deploying-data-factory.png)
9. Po zakończeniu tworzenia zostanie wyświetlona strona **Fabryka danych**, jak pokazano na poniższej ilustracji.
   
   ![Strona główna fabryki danych](./media/tutorial-create-azure-ssis-runtime-portal/data-factory-home-page.png)
10. Kliknij pozycję **Tworzenie i monitorowanie**, aby w osobnej karcie uruchomić interfejs użytkownika usługi Data Factory. 

### <a name="provision-an-azure-ssis-integration-runtime"></a>Aprowizowanie środowiska Azure SSIS Integration Runtime

1. Na stronie wprowadzenia kliknij kafelek **Konfigurowanie środowiska SSIS Integration Runtime**. 

   ![Kafelek Konfigurowanie środowiska SSIS Integration Runtime](./media/tutorial-create-azure-ssis-runtime-portal/configure-ssis-integration-runtime-tile.png)
2. Na stronie **Ustawienia ogólne** kreatora **konfiguracji środowiska Integration Runtime** wykonaj następujące czynności: 

   ![Ustawienia ogólne](./media/tutorial-create-azure-ssis-runtime-portal/general-settings.png)

    1. Określ **nazwę** środowiska Integration Runtime.
    2. Wybierz **lokalizację** środowiska Integration Runtime. Wyświetlane są tylko obsługiwane lokalizacje.
    3. Wybierz **rozmiar węzła**, który ma zostać skonfigurowany ze środowiskiem uruchomieniowym usług SSIS.
    4. Określ **liczbę węzłów** w klastrze.
    5. Kliknij przycisk **Dalej**. 
1. W obszarze **Ustawienia SQL** wykonaj następujące czynności: 

    ![Ustawienia SQL](./media/tutorial-create-azure-ssis-runtime-portal/sql-settings.png)

    1. Określ **subskrypcję** platformy Azure, która ma serwer usługi SQL Azure. 
    2. Wybierz serwer usługi SQL Azure dla **punktu końcowego serwera bazy danych katalogu**.
    3. Wprowadź nazwę użytkownika **administratora**.
    4. Wprowadź **hasło** dla administratora.  
    5. Wybierz **warstwę usług** dla bazy danych SSISDB. Wartość domyślna to Podstawowa.
    6. Kliknij przycisk **Dalej**. 
1.  Na stronie **Ustawienia zaawansowane** wybierz wartość dla ustawienia **Maximum Parallel Executions Per Node** (Maksymalna liczba równoległych wykonań na węzeł).   

    ![Ustawienia zaawansowane](./media/tutorial-create-azure-ssis-runtime-portal/advanced-settings.png)    
5. Ten krok jest **opcjonalny**. Jeśli masz klasyczną sieć wirtualną (VNet), do której chcesz dołączyć środowisko Integration Runtime, wybierz opcję **Select a VNet for your Azure-SSIS integration runtime to join and allow Azure services to configure VNet permissions/settings** (Wybierz sieć wirtualną dla środowiska Azure-SSIS Integration Runtime do dołączenia i zezwalaj usługom platformy Azure na konfigurowanie uprawnień/ustawień sieci wirtualnej) i wykonaj następujące czynności: 

    ![Ustawienia zaawansowane za pomocą sieci wirtualnej](./media/tutorial-create-azure-ssis-runtime-portal/advanced-settings-vnet.png)    

    1. Określ **subskrypcję**, która ma klasyczną sieć wirtualną. 
    2. Wybierz **sieć wirtualną**. <br/>
    4. Wybierz **podsieć**.<br/> 
1. Kliknij pozycję **Zakończ**, aby rozpocząć tworzenie środowiska Azure-SSIS Integration Runtime. 

    > [!IMPORTANT]
    > - Ukończenie tego procesu zajmuje około 20 minut
    > - Usługa Data Factory łączy się z usługą Azure SQL Database w celu przygotowania bazy danych wykazu usług SSIS (SSISDB). Skrypt konfiguruje również uprawnienia i ustawienia Twojej sieci wirtualnej, jeśli zostanie określona, i dołącza nowe wystąpienie środowiska Azure SSIS Integration Runtime do sieci wirtualnej.
7. W oknie **Połączenia** w razie potrzeby przełącz do pozycji **Produkty Integration Runtime**. Kliknij przycisk **Odśwież**, aby odświeżyć status. 

    ![Stan tworzenia](./media/tutorial-create-azure-ssis-runtime-portal/azure-ssis-ir-creation-status.png)
8. Użyj linków w kolumnie **Akcje**, aby monitorować, zatrzymywać/uruchamiać, edytować lub usunąć środowisko Integration Runtime. Użyj ostatniego linku, aby wyświetlić kod JSON dla środowiska Integration Runtime. Przyciski edytowania i usuwania są włączone tylko wtedy, gdy środowisko IR jest zatrzymane. 

    ![Środowisko IR Azure SSIS — akcje](./media/tutorial-create-azure-ssis-runtime-portal/azure-ssis-ir-actions.png)        
9. Kliknij link **Monitorowanie** w obszarze **Akcje**.  

    ![Środowisko IR Azure SSIS — szczegóły](./media/tutorial-create-azure-ssis-runtime-portal/azure-ssis-ir-details.png)
10. Jeśli wystąpił **błąd** skojarzony ze środowiskiem Azure SSIS IR, na tej stronie będzie wyświetlana liczba błędów oraz link umożliwiający wyświetlenie szczegółowych informacji o błędzie. Na przykład jeśli wykaz usług SSIS już istnieje na serwerze bazy danych, zostanie wyświetlony błąd wskazujący, że baza danych SSISDB już istnieje.  
11. Kliknij pozycję **Środowiska Integration Runtime** u góry, aby przejść z powrotem do poprzedniej strony i wyświetlić wszystkie środowiska Integration Runtime skojarzone z fabryką danych.  

### <a name="azure-ssis-integration-runtimes-in-the-portal"></a>Środowiska Azure SSIS Integration Runtime w portalu

1. W interfejsie użytkownika usługi Azure Data Factory przejdź na kartę **Edycja**, kliknij pozycję **Połączenia**, a następnie przejdź na kartę **Środowiska Integration Runtime**, aby wyświetlić istniejące środowiska Integration Runtime w fabryce danych. 
    ![Wyświetlanie istniejących środowisk IR](./media/tutorial-create-azure-ssis-runtime-portal/view-azure-ssis-integration-runtimes.png)
1. Kliknij pozycję **Nowe**, aby utworzyć środowisko IR Azure-SSIS. 

    ![Środowisko Integration Runtime za pomocą menu](./media/tutorial-create-azure-ssis-runtime-portal/edit-connections-new-integration-runtime-button.png)
2. Aby utworzyć środowisko Azure-SSIS Integration Runtime, kliknij przycisk **Nowe**, jak pokazano na ilustracji. 
3. W oknie Integration Runtime Setup (Konfiguracja środowiska Integration Runtime) wybierz pozycję **Lift-and-shift existing SSIS packages to execute in Azure** (Migruj metodą „lift-and-shift” istniejące pakiety usług SSIS do wykonywania na platformie Azure), a następnie kliknij przycisk **Dalej**.

    ![Określanie typu środowiska Integration Runtime](./media/tutorial-create-azure-ssis-runtime-portal/integration-runtime-setup-options.png)
4. Zobacz sekcję [Aprowizowanie środowiska Azure SSIS Integration Runtime](#provision-an-azure-ssis-integration-runtime), zawierającą pozostałe kroki konfigurowania środowiska IR Azure-SSIS.

## <a name="azure-powershell"></a>Azure PowerShell
W tej sekcji można wykorzystać program Azure PowerShell do utworzenia IR. Azure SSIS

### <a name="create-variables"></a>Tworzenie zmiennych
Zdefiniuj zmienne do wykorzystania w skrypcie w tym samouczku:

```powershell
# Azure Data Factory version 2 information 
# If your input contains a PSH special character, e.g. "$", precede it with the escape character "`" like "`$".
$SubscriptionName = "[your Azure subscription name]"
$ResourceGroupName = "[your Azure resource group name]"
$DataFactoryName = "[your data factory name]"
$DataFactoryLocation = "EastUS" 

# Azure-SSIS integration runtime information - This is the Data Factory compute resource for running SSIS packages
$AzureSSISName = "[your Azure-SSIS integration runtime name]"
$AzureSSISDescription = "This is my Azure-SSIS integration runtime"
$AzureSSISLocation = "EastUS" 
# In public preview, only Standard_A4_v2|Standard_A8_v2|Standard_D1_v2|Standard_D2_v2|Standard_D3_v2|Standard_D4_v2 are supported.
$AzureSSISNodeSize = "Standard_D3_v2"
# In public preview, only 1-10 nodes are supported.
$AzureSSISNodeNumber = 2 
# For a Standard_D1_v2 node, 1-4 parallel executions per node are supported. For other nodes, it's 1-8.
$AzureSSISMaxParallelExecutionsPerNode = 2 

# SSISDB info
$SSISDBServerEndpoint = "[your Azure SQL Database server name.database.windows.net or your Azure SQL Managed Instance (private preview) server endpoint]"
$SSISDBServerAdminUserName = "[your server admin username]"
$SSISDBServerAdminPassword = "[your server admin password]"

# Remove the SSISDBPricingTier variable if you are using Azure SQL Managed Instance (private preview)
# This parameter applies only to Azure SQL Database. For the basic pricing tier, specify "Basic", not "B". For standard tiers, specify "S0", "S1", "S2", 'S3", etc.
$SSISDBPricingTier = "[your Azure SQL Database pricing tier. Examples: Basic, S0, S1, S2, S3, etc.]"

## These two parameters apply if you are using a VNet and an Azure SQL Managed Instance (private preview) 
# Specify information about your classic or Azure Resource Manager virtual network (VNet). 
$VnetId = "[your VNet resource ID or leave it empty]" 
$SubnetName = "[your subnet name or leave it empty]" 

```
### <a name="log-in-and-select-subscription"></a>Logowanie i wybieranie subskrypcji
Dodaj następujący kod, skrypt logowania i wybierz subskrypcję platformy Azure: 

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $SubscriptionName
```

### <a name="validate-the-connection-to-database"></a>Weryfikowanie połączenia z bazą danych
Dodaj następujący skrypt w celu zweryfikowania Twojej server.database.windows.net serwera bazy danych SQL Azure lub punkt końcowy serwera (podglądzie prywatnym) wystąpienia zarządzane SQL Azure. 

```powershell
$SSISDBConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $SSISDBConnectionString;
Try
{
    $sqlConnection.Open();
}
Catch [System.Data.SqlClient.SqlException]
{
    Write-Warning "Cannot connect to your Azure SQL DB logical server/Azure SQL MI server, exception: $_"  ;
    Write-Warning "Please make sure the server you specified has already been created. Do you want to proceed? [Y/N]"
    $yn = Read-Host
    if(!($yn -ieq "Y"))
    {
        Return;
    } 
}
```

### <a name="configure-virtual-network"></a>Konfigurowanie sieci wirtualnej
Dodaj następujący skrypt, aby automatycznie skonfigurować uprawnienia/ustawienia sieci wirtualnej do przyłączenia do Twojego środowiska Azure SSIS Integration Runtime.

```powershell
# Register to Azure Batch resource provider
if(![string]::IsNullOrEmpty($VnetId) -and ![string]::IsNullOrEmpty($SubnetName))
{
    $BatchObjectId = (Get-AzureRmADServicePrincipal -ServicePrincipalName "MicrosoftAzureBatch").Id
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
    while(!(Get-AzureRmResourceProvider -ProviderNamespace "Microsoft.Batch").RegistrationState.Contains("Registered"))
    {
    Start-Sleep -s 10
    }
    if($VnetId -match "/providers/Microsoft.ClassicNetwork/")
    {
        # Assign VM contributor role to Microsoft.Batch
        New-AzureRmRoleAssignment -ObjectId $BatchObjectId -RoleDefinitionName "Classic Virtual Machine Contributor" -Scope $VnetId
    }
}
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Utwórz [grupę zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) za pomocą polecenia [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Grupa zasobów to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy. Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myResourceGroup` w lokalizacji `westeurope`.

```powershell
New-AzureRmResourceGroup -Location $DataFactoryLocation -Name $ResourceGroupName
```

### <a name="create-a-data-factory"></a>Tworzenie fabryki danych
Uruchom następujące polecenie, aby utworzyć fabrykę danych:

```powershell
Set-AzureRmDataFactoryV2 -ResourceGroupName $ResourceGroupName `
                         -Location $DataFactoryLocation `
                         -Name $DataFactoryName
```

### <a name="create-an-integration-runtime"></a>Tworzenie środowiska Integration Runtime
Uruchom następujące polecenie, aby utworzyć środowisko uruchomieniowe integracji usług SSIS Azure, które pakiety usług SSIS działa na platformie Azure: Użyj skryptu z sekcji, na podstawie typu bazy danych (vs bazy danych SQL Azure. Azure SQL wystąpienia zarządzane (podglądzie prywatnym)) jest używany. 

#### <a name="azure-sql-database-to-host-the-ssisdb-database-ssis-catalog"></a>Azure SQL Database do hostowania bazy danych usług SSIS (SSIS katalogu) 

```powershell
$secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
$serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)
Set-AzureRmDataFactoryV2IntegrationRuntime  -ResourceGroupName $ResourceGroupName `
                                            -DataFactoryName $DataFactoryName `
                                            -Name $AzureSSISName `
                                            -Type Managed `
                                            -CatalogServerEndpoint $SSISDBServerEndpoint `
                                            -CatalogAdminCredential $serverCreds `
                                            -CatalogPricingTier $SSISDBPricingTier `
                                            -Description $AzureSSISDescription `
                                            -Location $AzureSSISLocation `
                                            -NodeSize $AzureSSISNodeSize `
                                            -NodeCount $AzureSSISNodeNumber `
                                            -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode
```

Nie trzeba przekazać wartości VNetId i podsieć, jeśli nie potrzebujesz dostępu do danych lokalnych, oznacza to, że masz lokalnych źródeł/miejsca docelowe danych w pakietów SSIS. Należy podać wartość parametru CatalogPricingTier. Aby uzyskać listę obsługiwanych warstw cenowych bazy danych SQL Azure, zobacz [limity zasobów bazy danych SQL](../sql-database/sql-database-resource-limits.md).

#### <a name="azure-sql-managed-instance-private-preview-to-host-the-ssisdb-database"></a>Azure zarządzane wystąpienia SQL (podglądzie prywatnym) do obsługi bazy danych usług SSIS

```powershell
$secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
$serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)
Set-AzureRmDataFactoryV2IntegrationRuntime  -ResourceGroupName $ResourceGroupName `
                                            -DataFactoryName $DataFactoryName `
                                            -Name $AzureSSISName `
                                            -Type Managed `
                                            -CatalogServerEndpoint $SSISDBServerEndpoint `
                                            -CatalogAdminCredential $serverCreds `
                                            -Description $AzureSSISDescription `
                                            -Location $AzureSSISLocation `
                                            -NodeSize $AzureSSISNodeSize `
                                            -NodeCount $AzureSSISNodeNumber `
                                            -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode `
                                            -VnetId $VnetId `
                                            -Subnet $SubnetName
```

Należy przekazać wartości parametrów VnetId i podsieci z Azure zarządzane wystąpienia SQL (podglądzie prywatnym), które łączy sieć wirtualną. Parametr CatalogPricingTier nie ma zastosowania dla wystąpienia zarządzane SQL Azure. 

### <a name="start-integration-runtime"></a>Uruchamianie środowiska Integration Runtime
Uruchom następujące polecenie, aby uruchomić środowisko Azure-SSIS Integration Runtime: 

```powershell
write-host("##### Starting #####")
Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                             -DataFactoryName $DataFactoryName `
                                             -Name $AzureSSISName `
                                             -Force

write-host("##### Completed #####")
write-host("If any cmdlet is unsuccessful, please consider using -Debug option for diagnostics.")                                  
```
Wykonanie tego polecenia trwa od **20 do 30 minut**. 


### <a name="full-script"></a>Pełny skrypt
W tym miejscu jest pełna skrypt, który tworzy IR Azure SSIS i dołącza go do sieci wirtualnej. Ten skrypt odnosi się wystąpienia zarządzane SQL Azure (MI) są używane do obsługi katalogu usług SSIS. 

```powershell
# Azure Data Factory version 2 information 
# If your input contains a PSH special character, e.g. "$", precede it with the escape character "`" like "`$". 
$SubscriptionName = "<Azure subscription name>"
$ResourceGroupName = "<Azure resource group name>"
# Data factory name. Must be globally unique
$DataFactoryName = "<Data factory name>" 
$DataFactoryLocation = "EastUS" 

# Azure-SSIS integration runtime information. This is a Data Factory compute resource for running SSIS packages
$AzureSSISName = "<Specify a name for your Azure-SSIS (IR)>"
$AzureSSISDescription = "<Specify description for your Azure-SSIS IR"
$AzureSSISLocation = "EastUS" 
 # In public preview, only Standard_A4_v2, Standard_A8_v2, Standard_D1_v2, Standard_D2_v2, Standard_D3_v2, Standard_D4_v2 are supported
$AzureSSISNodeSize = "Standard_D3_v2"
# In public preview, only 1-10 nodes are supported.
$AzureSSISNodeNumber = 2 
# For a Standard_D1_v2 node, 1-4 parallel executions per node are supported. For other nodes, it's 1-8.
$AzureSSISMaxParallelExecutionsPerNode = 2 

# SSISDB info
$SSISDBServerEndpoint = "<Azure SQL server name>.database.windows.net"
$SSISDBServerAdminUserName = "<Azure SQL server - user name>"
$SSISDBServerAdminPassword = "<Azure SQL server - user password>"
# Remove the SSISDBPricingTier variable if you are using Azure SQL Managed Instance (private preview)
# This parameter applies only to Azure SQL Database. For the basic pricing tier, specify "Basic", not "B". For standard tiers, specify "S0", "S1", "S2", 'S3", etc.
$SSISDBPricingTier = "<pricing tier of your Azure SQL server. Examples: Basic, S0, S1, S2, S3, etc.>" 

$SSISDBConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $SSISDBConnectionString;
Try
{
    $sqlConnection.Open();
}
Catch [System.Data.SqlClient.SqlException]
{
    Write-Warning "Cannot connect to your Azure SQL DB logical server/Azure SQL MI server, exception: $_"  ;
    Write-Warning "Please make sure the server you specified has already been created. Do you want to proceed? [Y/N]"
    $yn = Read-Host
    if(!($yn -ieq "Y"))
    {
        Return;
    } 
}

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

Set-AzureRmDataFactoryV2 -ResourceGroupName $ResourceGroupName `
                        -Location $DataFactoryLocation `
                        -Name $DataFactoryName

$secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
$serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)
Set-AzureRmDataFactoryV2IntegrationRuntime  -ResourceGroupName $ResourceGroupName `
                                            -DataFactoryName $DataFactoryName `
                                            -Name $AzureSSISName `
                                            -Type Managed `
                                            -CatalogServerEndpoint $SSISDBServerEndpoint `
                                            -CatalogAdminCredential $serverCreds `
                                            -CatalogPricingTier $SSISDBPricingTier `
                                            -Description $AzureSSISDescription `
                                            -Location $AzureSSISLocation `
                                            -NodeSize $AzureSSISNodeSize `
                                            -NodeCount $AzureSSISNodeNumber `
                                            -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode

write-host("##### Starting your Azure-SSIS integration runtime. This command takes 20 to 30 minutes to complete. #####")
Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                             -DataFactoryName $DataFactoryName `
                                             -Name $AzureSSISName `
                                             -Force

write-host("##### Completed #####")
write-host("If any cmdlet is unsuccessful, please consider using -Debug option for diagnostics.")
```

## <a name="azure-resource-manager-template"></a>Szablon usługi Azure Resource Manager
W tej sekcji Szablon usługi Azure Resource Manager służy do tworzenia środowiska uruchomieniowego integracji usług SSIS Azure. Poniżej przedstawiono wskazówki próbki: 

1. Utwórz plik JSON zawierający następujący szablon Menedżera zasobów. Zastąp wartości w nawiasach (symbole zastępcze) własne wartości. 

    ```json
    {
        "contentVersion": "1.0.0.0",
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "parameters": {},
        "variables": {},
        "resources": [{
            "name": "<Specify a name for your data factory>",
            "apiVersion": "2017-09-01-preview",
            "type": "Microsoft.DataFactory/factories",
            "location": "East US",
            "properties": {},
            "resources": [{
                "type": "integrationruntimes",
                "name": "<Specify a name for the Azure SSIS IR>",
                "dependsOn": [ "<The name of the data factory you specified at the beginning>" ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "Managed",
                    "typeProperties": {
                        "computeProperties": {
                            "location": "East US",
                            "nodeSize": "Standard_D1_v2",
                            "numberOfNodes": 1,
                            "maxParallelExecutionsPerNode": 1
                        },
                        "ssisProperties": {
                            "catalogInfo": {
                                "catalogServerEndpoint": "<Azure SQL server>.database.windows.net",
                                "catalogAdminUserName": "<Azure SQL user",
                                "catalogAdminPassword": {
                                    "type": "SecureString",
                                    "value": "<Azure SQL Password>"
                                },
                                "catalogPricingTier": "Basic"
                            }
                        }
                    }
                }
            }]
        }]
    }
    ```
2. Aby wdrożyć szablon usługi Resource Manager, uruchom polecenie New-AzureRmResourceGroupDeployment, jak pokazano w następujących exmaple. W tym przykładzie ADFTutorialResourceGroup jest nazwą grupy zasobów. ADFTutorialARM.json jest plikiem, który zawiera definicję JSON dla fabryki danych i podczerwieni Azure SSIS. 

    ```powershell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json
    ```

    To polecenie tworzy fabryki danych i tworzy IR Azure SSIS, ale nie uruchamia IR. 
3. Aby uruchomić IR Azure SSIS, uruchom polecenie Start-AzureRmDataFactoryV2IntegrationRuntime: 

    ```powershell
    Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName "<Resource Group Name> `
                                             -DataFactoryName <Data Factory Name> `
                                             -Name <Azure SSIS IR Name> `
                                             -Force
    ``` 

## <a name="deploy-ssis-packages"></a>Wdrażanie pakietów usług SSIS
Teraz użyj programu SQL Server Data Tools (SSDT) lub SQL Server Management Studio (SSMS), aby wdrożyć pakiety usług SSIS na platformie Azure. Połącz się ze swoim serwerem Azure SQL, który hostuje katalog usług SSIS (SSISDB). Nazwa serwera Azure SQL jest w formacie: &lt;nazwa_serwera&gt;.database.windows.net (dla usługi Azure SQL Database). Zobacz artykuł [Deploy packages (Wdrażanie pakietów)](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages#deploy-packages-to-integration-services-server), aby uzyskać instrukcje. 

## <a name="next-steps"></a>Kolejne kroki
Inne IR Azure SSIS w tematach w tej dokumentacji:

- [Środowisko uruchomieniowe integracji usług SSIS Azure](concepts-integration-runtime.md#azure-ssis-integration-runtime). Ten artykuł zawiera informacje o pojęciach dotyczących środowisk uruchomieniowych integracji ogólnie tym podczerwieni Azure SSIS. 
- [Samouczek: Wdrażanie pakietów usług SSIS na platformie Azure](tutorial-deploy-ssis-packages-azure.md). Ten artykuł zawiera szczegółowe instrukcje dotyczące tworzenia środowiska Azure-SSIS IR i używania bazy danych Azure SQL do hostowania wykazu usług SSIS. 
- [Monitor an Azure-SSIS IR (Monitorowanie środowiska Azure-SSIS IR)](monitor-integration-runtime.md#azure-ssis-integration-runtime). W tym artykule przedstawiono sposób pobierania informacji o środowisku Azure-SSIS IR i opisów stanów w pobranych informacjach. 
- [Manage an Azure-SSIS IR (Zarządzanie środowiskiem Azure-SSIS IR)](manage-azure-ssis-integration-runtime.md). W tym artykule przedstawiono sposób zatrzymywania, uruchamiania lub usuwania środowiska Azure-SSIS IR. Zawiera on również instrukcje skalowania środowiska Azure-SSIS IR do wewnątrz za pomocą dodawania do niego węzłów. 
- [Join an Azure-SSIS IR to a VNet (Dołączanie środowiska Azure-SSIS IR do sieci wirtualnej)](join-azure-ssis-integration-runtime-virtual-network.md). Ten artykuł zawiera podstawowe informacje na temat dołączania środowiska Azure-SSIS IR do sieci wirtualnej platformy Azure. Opisano w nim kroki konfigurowania sieci wirtualnej za pomocą witryny Azure Portal tak, aby umożliwić dołączanie środowiska Azure-SSIS IR do sieci wirtualnej. 