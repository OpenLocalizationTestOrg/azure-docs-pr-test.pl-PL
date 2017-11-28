---
title: "aaaHPC pakiet klastra w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toointegrate HPC Pack 2016 klaster na platformie Azure za pomocą usługi Azure Active Directory"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="b5449-103">Zarządzanie klastra HPC Pack platformie Azure przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5449-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="b5449-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) obsługuje integrację z [usługi Azure Active Directory](../../active-directory/index.md) (Azure AD) dla administratorów, którzy wdrożenie klastra HPC Pack na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b5449-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="b5449-105">Wykonaj kroki hello w tym artykule hello następujące zadania wysokiego poziomu:</span><span class="sxs-lookup"><span data-stu-id="b5449-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="b5449-106">Ręcznie integracji klastra HPC Pack z dzierżawy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5449-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="b5449-107">Zarządzanie i planowanie zadań w klastrze HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b5449-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="b5449-108">Inne aplikacje i usługi toointegrate standardowe kroki integracji z usługą Azure AD rozwiązanie klastra HPC Pack jest zgodna.</span><span class="sxs-lookup"><span data-stu-id="b5449-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="b5449-109">W tym artykule przyjęto założenie, że czytelnik zna podstawowe użytkownika zarządzania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5449-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="b5449-110">Aby uzyskać więcej informacji i tło, zobacz hello [dokumentacji usługi Azure Active Directory](../../active-directory/index.md) i hello następujących sekcji.</span><span class="sxs-lookup"><span data-stu-id="b5449-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="b5449-111">Korzyści wynikające z integracji</span><span class="sxs-lookup"><span data-stu-id="b5449-111">Benefits of integration</span></span>


<span data-ttu-id="b5449-112">Azure Active Directory (Azure AD) to wielodostępne oparte na chmurze katalogami i tożsamościami zarządzania usługa, która zapewnia dostęp do rejestracji jednokrotnej (SSO) toocloud rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b5449-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="b5449-113">Integracja z usługą Azure AD klastra HPC Pack można osiągnąć następujące cele hello:</span><span class="sxs-lookup"><span data-stu-id="b5449-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="b5449-114">Usuń hello tradycyjnych kontrolera domeny usługi Active Directory z klastra HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="b5449-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="b5449-115">To może pomóc zmniejszyć koszty utrzymania hello klastra, jeśli nie jest to niezbędne do firmy oraz proces wdrażania hello przyspieszyć hello.</span><span class="sxs-lookup"><span data-stu-id="b5449-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="b5449-116">Wykorzystanie hello następujące korzyści, które zostały podane przy użyciu usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b5449-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="b5449-117">Logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b5449-117">Single sign-on</span></span> 
    *   <span data-ttu-id="b5449-118">Dla klastra HPC Pack hello na platformie Azure przy użyciu lokalnej tożsamości usługi AD</span><span class="sxs-lookup"><span data-stu-id="b5449-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Środowiska usługi Active Directory platformy Azure](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="b5449-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b5449-120">Prerequisites</span></span>
* <span data-ttu-id="b5449-121">**Klaster HPC Pack 2016 wdrożonymi na maszynach wirtualnych Azure** — Aby uzyskać instrukcje, zobacz [wdrożenie klastra HPC Pack 2016 na platformie Azure](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b5449-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="b5449-122">Należy nazwę DNS hello hello węzła głównego i hello poświadczenia administratora klastrów, aby wykonać kroki hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="b5449-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b5449-123">Integracja z usługą Azure Active Directory nie jest obsługiwany w wersjach pakietu HPC przed HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="b5449-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="b5449-124">**Komputer kliencki** — należy Windows lub Windows Server klienta zbyt Uruchom HPC Pack klienta narzędzia komputera.</span><span class="sxs-lookup"><span data-stu-id="b5449-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="b5449-125">Jeśli chcesz tylko zadania toosubmit interfejsu API REST lub portalu internetowego HPC Pack hello toouse, można użyć dowolnego komputera klienckiego wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5449-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="b5449-126">**HPC Pack narzędzi klienta** -Zainstaluj narzędzia klienta HPC Pack hello na komputerze klienckim hello przy użyciu pakietu instalacyjnego wolnego hello dostępnej w sklepie hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="b5449-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="b5449-127">Krok 1: Zarejestruj serwera klastra HPC hello dzierżawy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5449-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="b5449-128">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b5449-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b5449-129">Kliknij przycisk **usługi Active Directory** w hello menu po lewej stronie, a następnie kliknij przycisk hello żądanego katalogu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b5449-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="b5449-130">Musi mieć uprawnienie tooaccess zasobów w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="b5449-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="b5449-131">Kliknij przycisk **użytkowników**i upewnij się, że istnieją już konta użytkowników utworzone lub skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="b5449-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="b5449-132">Kliknij przycisk **aplikacji** > **Dodaj**, a następnie kliknij przycisk **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="b5449-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="b5449-133">Wprowadź następujące informacje w Kreatorze hello hello:</span><span class="sxs-lookup"><span data-stu-id="b5449-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="b5449-134">**Nazwa** -HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="b5449-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="b5449-135">**Typ** — wybierz tę opcję **aplikacji i/lub sieci Web interfejs API sieci Web**</span><span class="sxs-lookup"><span data-stu-id="b5449-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="b5449-136">**Adres URL logowania na**— Witaj bazowy adres URL dla próbki hello jest domyślnie`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="b5449-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="b5449-137">**Identyfikator URI aplikacji** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="b5449-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="b5449-138">Zastąp `<Directory_name`> z hello Pełna nazwa dzierżawy usługi Azure AD, na przykład `hpclocal.onmicrosoft.com`i Zastąp `<application_name>` o nazwie hello wybrano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b5449-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="b5449-139">Po dodaniu aplikacji hello, kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="b5449-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="b5449-140">Skonfiguruj hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="b5449-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="b5449-141">Wybierz **tak** dla **aplikacji jest wieloma dzierżawcami**</span><span class="sxs-lookup"><span data-stu-id="b5449-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="b5449-142">Wybierz **tak** dla **aplikacji wymagane tooaccess przypisanie użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="b5449-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="b5449-143">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b5449-143">Click **Save**.</span></span> <span data-ttu-id="b5449-144">Po zakończeniu zapisywania, kliknij przycisk **Zarządzanie manifestu**.</span><span class="sxs-lookup"><span data-stu-id="b5449-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="b5449-145">Ta akcja spowoduje pobranie aplikacji manifestu JavaScript object notation (JSON) pliku.</span><span class="sxs-lookup"><span data-stu-id="b5449-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="b5449-146">Edytuj hello pobrane manifeście dzięki umieszczeniu hello `appRoles` Ustawianie i dodawanie hello następującej roli aplikacji:</span><span class="sxs-lookup"><span data-stu-id="b5449-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="b5449-147">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="b5449-147">Save hello file.</span></span> <span data-ttu-id="b5449-148">Następnie kliknij w portalu hello **Zarządzanie manifestu** > **przekazać manifestu**.</span><span class="sxs-lookup"><span data-stu-id="b5449-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="b5449-149">Następnie możesz przekazać hello edytowanych manifestu.</span><span class="sxs-lookup"><span data-stu-id="b5449-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="b5449-150">Kliknij przycisk **użytkowników**, wybierz użytkownika, a następnie kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="b5449-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="b5449-151">Przypisać jeden hello dostępnych ról (HpcUsers lub HpcAdminMirror) toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b5449-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="b5449-152">Powtórz ten krok z dodatkowym użytkownikom w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="b5449-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="b5449-153">Aby uzyskać ogólne informacje o użytkownikach z klastra, zobacz [Zarządzanie użytkownikami klastra](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="b5449-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="b5449-154">Użytkownicy toomanage, zaleca się używanie bloku w wersji zapoznawczej usługi Azure Active Directory hello w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5449-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="b5449-155">Krok 2: Zarejestruj klienta klastra HPC hello dzierżawy usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5449-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="b5449-156">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b5449-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b5449-157">Kliknij przycisk **usługi Active Directory** w hello menu po lewej stronie, a następnie kliknij przycisk hello żądanego katalogu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b5449-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="b5449-158">Musi mieć uprawnienie tooaccess zasobów w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="b5449-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="b5449-159">Kliknij przycisk **aplikacji** > **Dodaj**, a następnie kliknij przycisk **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="b5449-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="b5449-160">Wprowadź następujące informacje w Kreatorze hello hello:</span><span class="sxs-lookup"><span data-stu-id="b5449-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="b5449-161">**Nazwa** -HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="b5449-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="b5449-162">**Typ** — wybierz tę opcję **aplikację Native Client**</span><span class="sxs-lookup"><span data-stu-id="b5449-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="b5449-163">**Identyfikator URI przekierowania** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="b5449-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="b5449-164">Po dodaniu aplikacji hello, kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="b5449-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="b5449-165">Kopiuj hello **identyfikator klienta** wartość i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="b5449-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="b5449-166">Należy to później podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5449-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="b5449-167">W **uprawnienia aplikacji tooother**, kliknij przycisk **Dodawanie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b5449-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="b5449-168">Wyszukiwanie i dodaj aplikację HpcPackClusterServer hello (utworzonego w kroku 1).</span><span class="sxs-lookup"><span data-stu-id="b5449-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="b5449-169">W hello **delegowane uprawnienia** listy rozwijanej wybierz **HpcClusterServer dostępu**.</span><span class="sxs-lookup"><span data-stu-id="b5449-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="b5449-170">Następnie kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="b5449-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="b5449-171">Krok 3: Konfigurowanie klastra HPC hello</span><span class="sxs-lookup"><span data-stu-id="b5449-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="b5449-172">Połącz toohello HPC Pack 2016 węzła głównego na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b5449-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="b5449-173">Uruchom program HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5449-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="b5449-174">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b5449-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="b5449-175">gdzie</span><span class="sxs-lookup"><span data-stu-id="b5449-175">where</span></span>

    * <span data-ttu-id="b5449-176">`AADTenant`Określa nazwę dzierżawy usługi Azure AD hello, takich jak`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="b5449-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="b5449-177">`AADClientAppId`Określa identyfikator klienta hello aplikacji hello utworzony w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="b5449-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="b5449-178">Uruchom ponownie usługę HpcSchedulerStateful hello.</span><span class="sxs-lookup"><span data-stu-id="b5449-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="b5449-179">W klastrze z wieloma węzłami head można uruchomić następujące polecenia programu PowerShell na powitania węzła głównego tooswitch hello repliki podstawowej dla usługi HpcSchedulerStateful hello hello:</span><span class="sxs-lookup"><span data-stu-id="b5449-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="b5449-180">Krok 4: Zarządzania i przesyłania zadań z powitania klienta</span><span class="sxs-lookup"><span data-stu-id="b5449-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="b5449-181">narzędzi tooinstall hello HPC Pack klienta na komputerze, pobrać pliki instalacyjne HPC Pack 2016 (Instalacja pełna) z hello Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="b5449-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="b5449-182">Po rozpoczęciu instalacji hello, wybierz opcję instalacji hello hello **narzędzi klienta HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="b5449-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="b5449-183">komputer kliencki hello tooprepare, zainstaluj certyfikat hello używane podczas [Konfiguracja klastra HPC](hpcpack-2016-cluster.md) na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="b5449-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="b5449-184">Użyj standardowych systemu Windows certyfikatu zarządzania procedury tooinstall hello certyfikatu publicznego toohello **Certyfikaty — bieżący użytkownik** > **zaufane główne urzędy certyfikacji** przechowywania.</span><span class="sxs-lookup"><span data-stu-id="b5449-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="b5449-185">Można teraz Uruchom polecenia HPC Pack hello lub użyj toosubmit hello graficznego interfejsu użytkownika Menedżera HPC Pack zadania i zarządzać zadaniami klastra przy użyciu konta hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5449-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="b5449-186">Dla opcji przesyłania zadań, zobacz [klastra HPC przesyłania zadań tooan HPC Pack na platformie Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="b5449-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="b5449-187">Podczas próby tooconnect klastra HPC Pack toohello na platformie Azure na powitania po raz pierwszy, zostanie wyświetlony okna podręczne.</span><span class="sxs-lookup"><span data-stu-id="b5449-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="b5449-188">Wprowadź toolog poświadczeń użytkownika usługi Azure AD w.</span><span class="sxs-lookup"><span data-stu-id="b5449-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="b5449-189">Hello token następnie są buforowane.</span><span class="sxs-lookup"><span data-stu-id="b5449-189">hello token is then cached.</span></span> <span data-ttu-id="b5449-190">Nowsze klastra toohello połączeń w hello Azure Użyj buforowane token, o ile nie jest brany pod uwagę zmiany lub hello w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="b5449-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="b5449-191">Na przykład po wykonaniu poprzednich kroków hello, musisz mogą wykonywać kwerendę o zadań z klienta lokalnego w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b5449-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="b5449-192">Przydatne polecenia cmdlet umożliwiające przesyłanie zadań o integracji z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5449-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="b5449-193">Zarządzanie pamięci podręcznej tokenu lokalne powitania</span><span class="sxs-lookup"><span data-stu-id="b5449-193">Manage hello local token cache</span></span>

<span data-ttu-id="b5449-194">HPC Pack 2016 zawiera dwa nowe polecenia cmdlet środowiska PowerShell klastra HPC toomanage hello lokalnej pamięci podręcznej tokenu.</span><span class="sxs-lookup"><span data-stu-id="b5449-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="b5449-195">Te polecenia cmdlet są przydatne do przesyłania zadań nieinteraktywnie.</span><span class="sxs-lookup"><span data-stu-id="b5449-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="b5449-196">Zobacz poniższy przykład hello:</span><span class="sxs-lookup"><span data-stu-id="b5449-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="b5449-197">Ustaw poświadczenia hello przesyłania zadań przy użyciu konta hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5449-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="b5449-198">Czasami może być toorun hello zadania w obszarze użytkownika klastra HPC hello (dla klastra HPC przyłączonych do domeny, Uruchom jako jedną domenę użytkownika; dla klastra HPC przyłączone do domeny, Uruchom jako jeden użytkownik lokalny na powitania węzła głównego).</span><span class="sxs-lookup"><span data-stu-id="b5449-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="b5449-199">Użyj hello następujące polecenia tooset hello poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="b5449-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="b5449-200">Następnie przesłać zadania hello w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="b5449-200">Then submit hello job as follows.</span></span> <span data-ttu-id="b5449-201">Hello zadanie działa w obszarze $localUser na powitania węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="b5449-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="b5449-202">Jeśli `–Credential` nie zostanie określony z `Submit-HpcJob`, hello lub zadania uruchamiana zamapowanych użytkownika lokalnego jako hello konto usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5449-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="b5449-203">(klaster HPC hello tworzy użytkownika lokalnego z hello takie same nazwy jako hello zadań hello toorun konta usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5449-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="b5449-204">Ustaw datę rozszerzonej dla hello konto usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5449-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="b5449-205">Jest to przydatne podczas uruchamiania zadań MPI w węzłach systemu Linux przy użyciu konta hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5449-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="b5449-206">Ustaw datę rozszerzonej dla hello samo konto usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5449-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="b5449-207">Ustaw zwiększoną ilość danych, a następnie uruchom jako użytkownika klastra HPC</span><span class="sxs-lookup"><span data-stu-id="b5449-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

