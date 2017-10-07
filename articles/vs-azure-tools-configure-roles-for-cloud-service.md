---
title: "aaaConfigure hello ról platformy Azure w chmurze usługi z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset Konfigurowanie i konfigurowania ról dla usług w chmurze Azure przy użyciu programu Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="7c809-103">Skonfigurować role usługi w chmurze Azure z programem Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c809-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="7c809-104">Usługi w chmurze Azure może mieć co najmniej jednego procesu roboczego lub role sieci web.</span><span class="sxs-lookup"><span data-stu-id="7c809-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="7c809-105">Dla każdej roli należy toodefine sposób konfigurowania tej roli, a także skonfigurować sposób uruchamiania tej roli.</span><span class="sxs-lookup"><span data-stu-id="7c809-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="7c809-106">toolearn więcej informacji na temat ról w usługach w chmurze, zobacz film hello [tooAzure wprowadzenie usługi w chmurze](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="7c809-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="7c809-107">Witaj informacje dla usługi w chmurze są przechowywane w hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="7c809-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="7c809-108">**ServiceDefinition.csdef** -pliku definicji usługi hello definiuje ustawienia środowiska uruchomieniowego hello tym, jakie role są wymagane usługi w chmurze, punktów końcowych i rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7c809-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="7c809-109">Brak hello danych przechowywanych w `ServiceDefinition.csdef` można zmieniać w przypadku roli użytkownika jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7c809-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="7c809-110">**Pliku ServiceConfiguration.cscfg** — plik konfiguracji usługi hello konfiguruje liczbę wystąpień roli są uruchamiane i hello wartości ustawień hello zdefiniowane dla roli.</span><span class="sxs-lookup"><span data-stu-id="7c809-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="7c809-111">Witaj danych przechowywanych w `ServiceConfiguration.cscfg` można zmienić uruchomionej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7c809-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="7c809-112">toostore różne wartości dla ustawień hello kontrolujących sposób uruchamiania roli, można zdefiniować wiele konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="7c809-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="7c809-113">W przypadku używania konfiguracji innej usługi, dla poszczególnych środowisk wdrażania.</span><span class="sxs-lookup"><span data-stu-id="7c809-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="7c809-114">Na przykład można ustawić Twojego konta połączenia ciąg toouse hello lokalnego magazynu Azure emulatora magazynu w konfiguracji usługi lokalnej i utwórz inny toouse konfiguracji usługi Azure storage w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="7c809-115">Podczas tworzenia usługi w chmurze platformy Azure w programie Visual Studio, dwie konfiguracje usług są tworzone automatycznie i dodane tooyour projektu platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="7c809-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="7c809-116">Konfigurowanie usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="7c809-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="7c809-117">Usługi w chmurze Azure z Eksploratora rozwiązań można skonfigurować w programie Visual Studio, pokazane na powitania następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7c809-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="7c809-118">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c809-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7c809-119">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz z menu kontekstowego hello **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="7c809-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![Menu kontekstowe projektu Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="7c809-121">Na stronie właściwości projektu hello, wybierz hello **programowanie** kartę.</span><span class="sxs-lookup"><span data-stu-id="7c809-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![Strona właściwości projektu — karta programowanie](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="7c809-123">W hello **konfiguracji usługi** listy, wybierz opcję hello nazwę hello konfiguracji usługi, które mają tooedit.</span><span class="sxs-lookup"><span data-stu-id="7c809-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="7c809-124">(Toomake zmian konfiguracji usługi hello tooall dla tej roli, zaznacz **wszystkie konfiguracje**.)</span><span class="sxs-lookup"><span data-stu-id="7c809-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="7c809-125">Jeśli wybierzesz opcję konfiguracji określonej usługi, niektóre właściwości są wyłączone, ponieważ ich można ustawić tylko w przypadku wszystkich konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7c809-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="7c809-126">tooedit te właściwości, należy wybrać **wszystkie konfiguracje**.</span><span class="sxs-lookup"><span data-stu-id="7c809-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Lista konfiguracji usługi dla usługi w chmurze Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="7c809-128">Zmień hello liczbę wystąpień roli</span><span class="sxs-lookup"><span data-stu-id="7c809-128">Change hello number of role instances</span></span>
<span data-ttu-id="7c809-129">wydajność hello tooimprove usługi w chmurze, można zmienić hello liczbę wystąpień roli, które działają na podstawie hello liczby użytkowników lub obciążenia hello oczekiwany dla określonej roli.</span><span class="sxs-lookup"><span data-stu-id="7c809-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="7c809-130">Oddzielnej maszynie wirtualnej jest tworzony dla każdego wystąpienia roli, gdy usługa w chmurze hello działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7c809-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="7c809-131">Ma to wpływ na rozliczenia hello hello wdrożenia tej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7c809-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="7c809-132">Aby uzyskać więcej informacji dotyczących rozliczeń, zobacz [zrozumieć rachunku platformy Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="7c809-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="7c809-133">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c809-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7c809-134">W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="7c809-135">W obszarze hello **ról** węzła, kliknij prawym przyciskiem myszy hello roli tooupdate, a następnie, wybierz z menu kontekstowego hello **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="7c809-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu kontekstowe roli Azure Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="7c809-137">Wybierz hello **konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="7c809-137">Select hello **Configuration** tab.</span></span>

    ![Karta Konfiguracja](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="7c809-139">W hello **konfiguracji usługi** listy, wybierz opcję hello konfiguracji usługi, które mają tooupdate.</span><span class="sxs-lookup"><span data-stu-id="7c809-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![Konfiguracji usługi na liście](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="7c809-141">W hello **wystąpienia licznika** tekst Wprowadź hello liczbę wystąpień mają toostart dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="7c809-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="7c809-142">Każde wystąpienie działa na oddzielnej maszynie wirtualnej podczas publikowania tooAzure usługi chmury hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Aktualizowanie hello liczba wystąpień](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="7c809-144">Z hello Visual Studio narzędzi, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7c809-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="7c809-145">Zarządzanie parametry połączenia dla konta magazynu</span><span class="sxs-lookup"><span data-stu-id="7c809-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="7c809-146">Można dodać, usunąć ani zmodyfikować parametrów połączenia dla konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="7c809-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="7c809-147">Na przykład może być ciąg połączenia lokalnej konfiguracji usługi lokalnej, która ma wartość `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="7c809-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="7c809-148">Można także tooconfigure konfiguracji usługi chmury, korzystającej z konta magazynu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7c809-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="7c809-149">Po wprowadzeniu hello Azure klucza informacji o koncie magazynu dla parametrów połączenia konta magazynu, te informacje są przechowywane lokalnie w pliku konfiguracji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="7c809-150">Jednak ta informacje obecnie nie są przechowywane jako tekst zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="7c809-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="7c809-151">Za pomocą innej wartości dla każdej konfiguracji usługi, nie ma toouse innymi parametrami połączenia w usłudze w chmurze lub zmodyfikuj kodu podczas publikowania z tooAzure usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="7c809-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="7c809-152">Możesz użyć tej samej nazwy dla hello parametry połączenia w kodzie i hello wartość jest inny, na podstawie konfiguracji usługi hello, wybranej podczas tworzenia usługi w chmurze lub podczas jego publikowania powitalne.</span><span class="sxs-lookup"><span data-stu-id="7c809-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="7c809-153">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c809-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7c809-154">W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="7c809-155">W obszarze hello **ról** węzła, kliknij prawym przyciskiem myszy hello roli tooupdate, a następnie, wybierz z menu kontekstowego hello **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="7c809-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu kontekstowe roli Azure Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="7c809-157">Wybierz hello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="7c809-157">Select hello **Settings** tab.</span></span>

    ![Karta Ustawienia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="7c809-159">W hello **konfiguracji usługi** listy, wybierz opcję hello konfiguracji usługi, które mają tooupdate.</span><span class="sxs-lookup"><span data-stu-id="7c809-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Konfiguracja usługi](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="7c809-161">Wybierz tooadd ciąg połączenia **Dodaj ustawienie**.</span><span class="sxs-lookup"><span data-stu-id="7c809-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![Dodaj ciąg połączenia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="7c809-163">Po dodaniu nowego ustawienia hello listy toohello, należy zaktualizować wiersza hello liście hello hello niezbędne informacje.</span><span class="sxs-lookup"><span data-stu-id="7c809-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nowe parametry połączenia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="7c809-165">**Nazwa** — wprowadź nazwę hello mają toouse hello ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="7c809-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="7c809-166">**Typ** — wybierz tę opcję **ciąg połączenia** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="7c809-167">**Wartość** — możesz wprowadzić parametry połączenia hello bezpośrednio do hello **wartość** komórki lub hello wybierz wielokropek (...) toowork w hello **utworzyć parametry połączenia magazynu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7c809-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="7c809-168">W hello **utworzyć parametry połączenia magazynu** okno dialogowe, wybierz opcję **łączyć się przy użyciu**.</span><span class="sxs-lookup"><span data-stu-id="7c809-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="7c809-169">Następnie wykonaj instrukcje hello opcja hello:</span><span class="sxs-lookup"><span data-stu-id="7c809-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="7c809-170">**Emulator magazynu Microsoft Azure** — Jeśli ta opcja hello pozostałe ustawienia w oknie dialogowym hello są wyłączone, ponieważ mają one zastosowanie tylko tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7c809-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="7c809-171">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c809-171">Select **OK**.</span></span>
    - <span data-ttu-id="7c809-172">**Subskrypcja** — w przypadku wybrania tej opcji, użyj hello listy rozwijanej listy tooeither wybierz i zaloguj się do konta Microsoft, lub Dodawanie konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7c809-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="7c809-173">Wybierz konto platformy Azure subskrypcji i magazynu.</span><span class="sxs-lookup"><span data-stu-id="7c809-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="7c809-174">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c809-174">Select **OK**.</span></span>
    - <span data-ttu-id="7c809-175">**Ręcznie wprowadzić poświadczenia** — wprowadź nazwę konta magazynu hello i albo hello klucz podstawowy lub drugiego.</span><span class="sxs-lookup"><span data-stu-id="7c809-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="7c809-176">Wybierz opcję wyznaczenia **połączenia** (HTTPS jest zalecane dla większości scenariuszy). Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c809-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="7c809-177">toodelete ciąg połączenia wybierz hello parametry połączenia, a następnie wybierz **Usuń ustawienie**.</span><span class="sxs-lookup"><span data-stu-id="7c809-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="7c809-178">Z hello Visual Studio narzędzi, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7c809-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="7c809-179">Uzyskania programowego dostępu do parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="7c809-179">Programmatically access a connection string</span></span>

<span data-ttu-id="7c809-180">Witaj poniższej procedurze pokazano, jak tooprogrammatically uzyskują dostęp do ciągu połączenia przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="7c809-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="7c809-181">Dodaj następujące hello przy użyciu dyrektywy tooa C# pliku, gdzie będą toouse hello ustawienia:</span><span class="sxs-lookup"><span data-stu-id="7c809-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="7c809-182">Witaj poniższy kod przedstawia przykładowy sposób tooaccess ciąg połączenia.</span><span class="sxs-lookup"><span data-stu-id="7c809-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="7c809-183">Zastąp hello &lt;ConnectionStringName > symbolu zastępczego hello odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="7c809-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="7c809-184">Dodatek toouse niestandardowe ustawienia usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="7c809-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="7c809-185">Ustawienia niestandardowe w pliku konfiguracji usługi hello pozwalają Dodaj nazwę i wartość ciągu dla określonej usługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7c809-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="7c809-186">Możesz wybrać toouse tego tooconfigure ustawienie to funkcja usługi w chmurze, odczytując wartości hello hello ustawienie i przy użyciu tej logiki hello toocontrol wartości w kodzie.</span><span class="sxs-lookup"><span data-stu-id="7c809-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="7c809-187">Bez konieczności toorebuild pakietu usługi lub usługi w chmurze jest uruchomiona, można zmienić tych wartości konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="7c809-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="7c809-188">Powiadomienia o kodzie można sprawdzić podczas zmiany ustawień.</span><span class="sxs-lookup"><span data-stu-id="7c809-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="7c809-189">Zobacz [RoleEnvironment.Changing zdarzeń](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c809-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="7c809-190">Można dodać, usunąć ani zmodyfikować własne ustawienia konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="7c809-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="7c809-191">Może być różne wartości dla tych ciągów w przypadku konfiguracji z innej usługi.</span><span class="sxs-lookup"><span data-stu-id="7c809-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="7c809-192">Za pomocą innej wartości dla każdej konfiguracji usługi, nie mają różne ciągi toouse w usłudze w chmurze lub zmodyfikuj kodu podczas publikowania z tooAzure usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="7c809-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="7c809-193">Możesz użyć tej samej nazwy dla ciąg hello w polu wartość kodu i hello jest inny, na podstawie konfiguracji usługi hello, wybranej podczas tworzenia usługi w chmurze lub podczas jego publikowania powitalne.</span><span class="sxs-lookup"><span data-stu-id="7c809-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="7c809-194">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c809-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7c809-195">W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="7c809-196">W obszarze hello **ról** węzła, kliknij prawym przyciskiem myszy hello roli tooupdate, a następnie, wybierz z menu kontekstowego hello **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="7c809-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu kontekstowe roli Azure Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="7c809-198">Wybierz hello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="7c809-198">Select hello **Settings** tab.</span></span>

    ![Karta Ustawienia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="7c809-200">W hello **konfiguracji usługi** listy, wybierz opcję hello konfiguracji usługi, które mają tooupdate.</span><span class="sxs-lookup"><span data-stu-id="7c809-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Konfiguracji usługi na liście](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="7c809-202">tooadd niestandardową wartość ustawienia, wybierz **Dodaj ustawienie**.</span><span class="sxs-lookup"><span data-stu-id="7c809-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![Dodaj niestandardową wartość ustawienia](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="7c809-204">Po dodaniu nowego ustawienia hello listy toohello, należy zaktualizować wiersza hello liście hello hello niezbędne informacje.</span><span class="sxs-lookup"><span data-stu-id="7c809-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nowe ustawienie niestandardowe](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="7c809-206">**Nazwa** — wprowadź nazwę hello hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="7c809-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="7c809-207">**Typ** — wybierz tę opcję **ciąg** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="7c809-208">**Wartość** — wprowadź wartość hello hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="7c809-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="7c809-209">Możesz wprowadzić wartość hello bezpośrednio do hello **wartość** komórki lub hello wybierz wielokropek (...) tooenter hello wartości w hello **Edytowanie ciągu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7c809-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="7c809-210">toodelete niestandardową wartość ustawienia, wybierz ustawienie hello, a następnie wybierz **Usuń ustawienie**.</span><span class="sxs-lookup"><span data-stu-id="7c809-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="7c809-211">Z hello Visual Studio narzędzi, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7c809-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="7c809-212">Uzyskania programowego dostępu do wartości ustawienia niestandardowego</span><span class="sxs-lookup"><span data-stu-id="7c809-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="7c809-213">Witaj poniższej procedurze pokazano, jak tooprogrammatically dostępu niestandardową wartość ustawienia przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="7c809-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="7c809-214">Dodaj następujące hello przy użyciu dyrektywy tooa C# pliku, gdzie będą toouse hello ustawienia:</span><span class="sxs-lookup"><span data-stu-id="7c809-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="7c809-215">Witaj poniższy kod przedstawia przykładowy sposób tooaccess ustawienia niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="7c809-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="7c809-216">Zastąp hello &lt;SettingName > symbolu zastępczego hello odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="7c809-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="7c809-217">Zarządzanie magazynem lokalnym dla każdego wystąpienia roli</span><span class="sxs-lookup"><span data-stu-id="7c809-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="7c809-218">Możesz dodać magazyn systemu pliku lokalnego dla każdego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="7c809-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="7c809-219">Hello danych przechowywanych w pamięci masowej nie jest dostępny przez innych wystąpień roli hello, dla których hello są przechowywane dane lub innych ról.</span><span class="sxs-lookup"><span data-stu-id="7c809-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="7c809-220">Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c809-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="7c809-221">W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="7c809-222">W obszarze hello **ról** węzła, kliknij prawym przyciskiem myszy hello roli tooupdate, a następnie, wybierz z menu kontekstowego hello **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="7c809-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu kontekstowe roli Azure Eksploratora rozwiązań](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="7c809-224">Wybierz hello **Magazyn lokalny** kartę.</span><span class="sxs-lookup"><span data-stu-id="7c809-224">Select hello **Local Storage** tab.</span></span>

    ![Karta magazynu lokalnego](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="7c809-226">W hello **konfiguracji usługi** listy, upewnij się, że **wszystkie konfiguracje** jest zaznaczona, jak ustawienia magazynu lokalne powitania tooall usługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7c809-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="7c809-227">Wszelkie inne wartości powoduje wszystkie pola wejściowe hello na stronie powitania wyłączana.</span><span class="sxs-lookup"><span data-stu-id="7c809-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![Konfiguracji usługi na liście](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="7c809-229">Wybierz tooadd wpisem Magazyn lokalny **dodać magazyn lokalny**.</span><span class="sxs-lookup"><span data-stu-id="7c809-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![Dodaj magazyn lokalny](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="7c809-231">Po dodaniu nowego wpisu magazynu lokalnego hello listy toohello, należy zaktualizować wiersza hello liście hello hello niezbędne informacje.</span><span class="sxs-lookup"><span data-stu-id="7c809-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nowy wpis w lokalnej pamięci masowej](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="7c809-233">**Nazwa** — wprowadź nazwę hello mają toouse dla nowego magazynu lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="7c809-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="7c809-234">**Rozmiar (MB)** — wprowadź hello rozmiar w MB potrzebnym do nowego magazynu lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="7c809-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="7c809-235">**Wyczyść na roli odtworzenia** — wybierz dane hello tooremove tej opcji w hello nowego magazynu lokalnego, podczas odtwarzania hello maszyny wirtualnej dla roli hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="7c809-236">toodelete wpisu magazynu lokalnego, wybierz wpis hello, a następnie wybierz **usunąć magazyn lokalny**.</span><span class="sxs-lookup"><span data-stu-id="7c809-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="7c809-237">Z hello Visual Studio narzędzi, wybierz opcję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7c809-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="7c809-238">Uzyskiwania dostępu do lokalnego magazynu</span><span class="sxs-lookup"><span data-stu-id="7c809-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="7c809-239">W tej części przedstawiono sposób tooprogrammatically uzyskiwania dostępu do magazynu lokalnego przy użyciu języka C# zapisując plik tekstowy testu `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="7c809-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="7c809-240">Pisanie tekstu toolocal magazynem</span><span class="sxs-lookup"><span data-stu-id="7c809-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="7c809-241">Hello następującego kodu przedstawiono przykład sposobu toolocal magazyn plików toowrite tekstu.</span><span class="sxs-lookup"><span data-stu-id="7c809-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="7c809-242">Zastąp hello &lt;LocalStorageName > symbolu zastępczego hello odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="7c809-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="7c809-243">Znajdź plik zapisany toolocal magazynu</span><span class="sxs-lookup"><span data-stu-id="7c809-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="7c809-244">tooview hello plik utworzony przez kod hello w poprzedniej sekcji hello, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7c809-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="7c809-245">Witaj obszaru powiadomień systemu Windows, kliknij prawym przyciskiem myszy hello Azure ikona i, wybierz z menu kontekstowego hello, **Pokaż interfejs użytkownika emulatora obliczeń**.</span><span class="sxs-lookup"><span data-stu-id="7c809-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Pokaż emulatora obliczeń platformy Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="7c809-247">Wybierz rolę sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="7c809-247">Select hello web role.</span></span>

    ![Emulator obliczeń platformy Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="7c809-249">Na powitania **Microsoft Azure obliczeniowe emulatora** menu, wybierz opcję **narzędzia** > **Otwórz magazyn lokalny**.</span><span class="sxs-lookup"><span data-stu-id="7c809-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Otwórz magazyn lokalny element menu](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="7c809-251">Po otwarciu okna Eksploratora Windows hello, wprowadź "MyLocalStorageTest.txt" do hello **wyszukiwania** pola tekstowego, a następnie wybierz **Enter** toostart hello wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7c809-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7c809-252">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c809-252">Next steps</span></span>
<span data-ttu-id="7c809-253">Dowiedz się więcej o Azure projekty w programie Visual Studio, odczytując [Konfigurowanie projektu platformy Azure](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="7c809-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="7c809-254">Więcej informacji na temat schematu usługi w chmurze hello odczytując [odwołanie do schematu](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="7c809-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

