---
title: "aaaEnable pulpitu zdalnego w usługi w chmurze platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure platformy azure w chmurze usługi połączeń pulpitu zdalnego tooallow aplikacji"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="e70ec-103">Włączanie połączeń usług pulpitu zdalnego dla roli usług w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="e70ec-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e70ec-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e70ec-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="e70ec-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e70ec-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="e70ec-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e70ec-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="e70ec-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e70ec-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="e70ec-108">Umożliwia Podłączanie pulpitu zdalnego w roli podczas tworzenia przez uwzględnienie hello modułów usług pulpitu zdalnego w definicji usługi. można też tooenable pulpitu zdalnego za pośrednictwem hello rozszerzenia usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="e70ec-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="e70ec-109">Hello preferowana metoda się toouse hello pulpitu zdalnego rozszerzenie można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji hello bez konieczności tooredeploy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e70ec-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="e70ec-110">Konfigurowanie pulpitu zdalnego z hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e70ec-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="e70ec-111">Hello klasycznego portalu Azure używa hello podejście rozszerzenia usług pulpitu zdalnego, więc można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e70ec-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="e70ec-112">Witaj **Konfiguruj** strony dla usługi w chmurze pozwala tooenable pulpitu zdalnego, zmiana konta administratora lokalnego hello używane maszyny wirtualne toohello tooconnect, hello certyfikat używany podczas uwierzytelniania i ustawić hello Data wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="e70ec-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="e70ec-113">Kliknij przycisk **usługi w chmurze**, kliknij nazwę hello hello usługi w chmurze, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="e70ec-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="e70ec-114">Kliknij przycisk hello **zdalnego** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e70ec-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Usługi w chmurze zdalnego](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="e70ec-116">Wszystkie wystąpienia roli zostanie ponownie uruchomiony, gdy najpierw włączyć pulpitu zdalnego i kliknij przycisk OK (znacznikiem wyboru).</span><span class="sxs-lookup"><span data-stu-id="e70ec-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="e70ec-117">tooprevent ponowne uruchomienie komputera, hello certyfikatu używane tooencrypt hello hasło musi być zainstalowany na powitania roli.</span><span class="sxs-lookup"><span data-stu-id="e70ec-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="e70ec-118">tooprevent ponowne uruchomienie, [przekazywanie certyfikatu dla usługi w chmurze hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , a następnie wróć toothis okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e70ec-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="e70ec-119">W **ról**, wybierz rolę hello tooupdate lub wybierz **wszystkie** dla wszystkich ról.</span><span class="sxs-lookup"><span data-stu-id="e70ec-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="e70ec-120">Wprowadź jedną hello następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="e70ec-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="e70ec-121">tooenable pulpitu zdalnego, wybierz opcję hello **Włącz pulpit zdalny** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="e70ec-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="e70ec-122">toodisable pulpitu zdalnego, hello wyczyść pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="e70ec-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="e70ec-123">Utwórz konto toouse połączeń pulpitu zdalnego toohello wystąpień roli.</span><span class="sxs-lookup"><span data-stu-id="e70ec-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="e70ec-124">Zaktualizuj hasło hello hello istniejącego konta.</span><span class="sxs-lookup"><span data-stu-id="e70ec-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="e70ec-125">Wybierz toouse przekazano certyfikat dla uwierzytelniania (przekazywanie hello certyfikatu przy użyciu **przekazać** na powitania **certyfikaty** strony) lub Utwórz nowy certyfikat.</span><span class="sxs-lookup"><span data-stu-id="e70ec-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="e70ec-126">Zmień datę wygaśnięcia hello hello konfiguracji pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="e70ec-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="e70ec-127">Po zakończeniu aktualizacji konfiguracji, kliknij przycisk **OK** (znacznikiem wyboru).</span><span class="sxs-lookup"><span data-stu-id="e70ec-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="e70ec-128">Zdalne do wystąpień roli</span><span class="sxs-lookup"><span data-stu-id="e70ec-128">Remote into role instances</span></span>
<span data-ttu-id="e70ec-129">Włączenie pulpitu zdalnego na powitania role można zdalnego do wystąpienia roli za pomocą różnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="e70ec-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="e70ec-130">wystąpienie roli tooa tooconnect z hello klasycznego portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="e70ec-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="e70ec-131">Kliknij przycisk **wystąpień** tooopen hello **wystąpień** strony.</span><span class="sxs-lookup"><span data-stu-id="e70ec-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="e70ec-132">Wybierz wystąpienia roli, który ma pulpitu zdalnego skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="e70ec-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="e70ec-133">Kliknij przycisk **Connect**i wykonaj hello instrukcje tooopen hello pulpitu.</span><span class="sxs-lookup"><span data-stu-id="e70ec-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="e70ec-134">Kliknij przycisk **Otwórz** , a następnie **Connect** toostart hello Podłączanie pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="e70ec-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="e70ec-135">Za pomocą programu Visual Studio tooremote do wystąpienia roli</span><span class="sxs-lookup"><span data-stu-id="e70ec-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="e70ec-136">W programie Visual Studio, Eksploratora serwera:</span><span class="sxs-lookup"><span data-stu-id="e70ec-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="e70ec-137">Rozwiń węzeł hello **Azure** > **usługi w chmurze** > **[nazwa usługi w chmurze]** węzła.</span><span class="sxs-lookup"><span data-stu-id="e70ec-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="e70ec-138">Rozwiń pozycję **przemieszczania** lub **produkcji**.</span><span class="sxs-lookup"><span data-stu-id="e70ec-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="e70ec-139">Rozwiń hello poszczególnych ról.</span><span class="sxs-lookup"><span data-stu-id="e70ec-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="e70ec-140">Kliknij prawym przyciskiem myszy jeden z wystąpień roli hello, kliknij przycisk **łączyć się przy użyciu pulpitu zdalnego...** , a następnie wprowadź hello nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="e70ec-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![Pulpit zdalny Eksploratora serwera](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="e70ec-142">Użyj pliku RDP hello tooget środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="e70ec-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="e70ec-143">Można użyć hello [Get AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) plik RDP hello tooretrieve polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e70ec-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="e70ec-144">Plik RDP hello można następnie użyć z usługą w chmurze hello tooaccess Podłączanie pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="e70ec-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="e70ec-145">Programowo Pobierz plik RDP hello za pośrednictwem hello interfejs API REST zarządzania usługami</span><span class="sxs-lookup"><span data-stu-id="e70ec-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="e70ec-146">Można użyć hello [Pobierz plik RDP](https://msdn.microsoft.com/library/jj157183.aspx) plik RDP hello toodownload operacji REST.</span><span class="sxs-lookup"><span data-stu-id="e70ec-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="e70ec-147">tooconfigure pulpitu zdalnego w pliku definicji usługi hello</span><span class="sxs-lookup"><span data-stu-id="e70ec-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="e70ec-148">Ta metoda umożliwia tooenable pulpitu zdalnego dla aplikacji hello podczas programowania.</span><span class="sxs-lookup"><span data-stu-id="e70ec-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="e70ec-149">Ta metoda wymaga szyfrowania haseł można przechowywać w konfiguracji usługi plików i wszelkie aktualizacje toohello konfigurację pulpitu zdalnego wymaga ponownego wdrażania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e70ec-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="e70ec-150">Jeśli chcesz, aby tooavoid tych downsides, należy użyć rozszerzenia usług pulpitu zdalnego hello na podstawie podejścia opisanego powyżej.</span><span class="sxs-lookup"><span data-stu-id="e70ec-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="e70ec-151">Można użyć programu Visual Studio za[połączeń usług pulpitu zdalnego włączyć](../vs-azure-tools-remote-desktop-roles.md) podejście pliku definicji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="e70ec-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="e70ec-152">Poniższe kroki Hello opisano hello zmiany wymagane toohello usługi modelu pliki tooenable pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="e70ec-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="e70ec-153">Visual Studio będzie automatycznie tworzy te zmiany podczas publikowania.</span><span class="sxs-lookup"><span data-stu-id="e70ec-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="e70ec-154">Skonfiguruj połączenie hello w modelu usług hello</span><span class="sxs-lookup"><span data-stu-id="e70ec-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="e70ec-155">Użyj hello **importów** hello tooimport elementu **RemoteAccess** modułu i hello **RemoteForwarder** toohello modułu [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) pliku.</span><span class="sxs-lookup"><span data-stu-id="e70ec-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="e70ec-156">Witaj pliku definicji usługi powinny być podobne toohello poniższy przykład z hello `<Imports>` elementu dodany.</span><span class="sxs-lookup"><span data-stu-id="e70ec-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="e70ec-157">Witaj [pliku ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) plik powinien być toohello podobnie poniższy przykład, należy zwrócić uwagę hello `<ConfigurationSettings>` i `<Certificates>` elementy.</span><span class="sxs-lookup"><span data-stu-id="e70ec-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="e70ec-158">Witaj określony certyfikat musi być [przekazać usługi w chmurze toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="e70ec-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="e70ec-159">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e70ec-159">Additional Resources</span></span>
<span data-ttu-id="e70ec-160">[Jak usługi w chmurze tooConfigure](cloud-services-how-to-configure.md)
[usług w chmurze — często zadawane pytania — pulpitu zdalnego](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e70ec-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
