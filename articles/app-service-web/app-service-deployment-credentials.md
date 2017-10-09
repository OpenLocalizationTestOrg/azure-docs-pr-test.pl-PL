---
title: "aaaAzure poświadczenia wdrożenia usługi aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello poświadczenia wdrożenia usługi Azure App Service."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="774ee-103">Skonfiguruj poświadczenia wdrażania dla usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="774ee-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="774ee-104">[Usługa aplikacji Azure](http://go.microsoft.com/fwlink/?LinkId=529714) obsługuje dwa rodzaje poświadczenia [lokalnego wdrożenia Git](app-service-deploy-local-git.md) i [wdrożenia FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="774ee-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="774ee-105">Są one nie hello taki sam jak swoje poświadczenia usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="774ee-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="774ee-106">**Poświadczenia użytkownika na poziomie**: jeden zestaw poświadczeń hello całego konta Azure.</span><span class="sxs-lookup"><span data-stu-id="774ee-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="774ee-107">Może być używane toodeploy tooApp usługi dla wszystkich aplikacji, w dowolnej subskrypcji, która hello konta Azure ma tooaccess uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="774ee-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="774ee-108">Są to hello domyślne poświadczenia zestaw, który należy skonfigurować w **usługi aplikacji** > **&lt;nazwa_aplikacji >** > **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="774ee-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="774ee-109">To jest również hello domyślnego zestawu, który jest wyświetlana w portalu hello graficznego interfejsu użytkownika (takich jak hello **omówienie** i **właściwości** aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="774ee-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="774ee-110">Podczas delegować dostęp do zasobów tooAzure za pomocą kontroli dostępu na podstawie ról (RBAC) lub współadministratora uprawnienia, każdy użytkownik usługi Azure, który otrzymuje dostęp tooan aplikacji można użyć jego osobistych poświadczeń na poziomie użytkownika do momentu dostęp został odwołany.</span><span class="sxs-lookup"><span data-stu-id="774ee-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="774ee-111">Te poświadczenia wdrożenia nie powinny być udostępniać innym użytkownikom Azure.</span><span class="sxs-lookup"><span data-stu-id="774ee-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="774ee-112">**Poświadczeń na poziomie aplikacji**: jeden zestaw poświadczeń dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="774ee-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="774ee-113">Może być używane toodeploy toothat tylko aplikacji.</span><span class="sxs-lookup"><span data-stu-id="774ee-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="774ee-114">Witaj poświadczeń dla każdej aplikacji jest generowany automatycznie podczas tworzenia aplikacji i znajduje się w aplikacji hello profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="774ee-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="774ee-115">Nie można ręcznie skonfigurować hello poświadczeń, ale można je zresetować w każdej chwili dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="774ee-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="774ee-116">W kolejności toogive komuś dostęp toothese poświadczeń za pomocą roli na podstawie kontroli dostępu (RBAC), należy toomake ich współautora lub nowszej na powitania aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="774ee-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="774ee-117">Czytniki nie są dozwolone toopublish i dlatego nie można uzyskać dostępu do tych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="774ee-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="774ee-118"><a name="userscope"></a>Ustaw i zresetowanie poświadczeń na poziomie użytkownika</span><span class="sxs-lookup"><span data-stu-id="774ee-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="774ee-119">Poświadczenia na poziomie użytkownika można skonfigurować w dowolnej aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="774ee-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="774ee-120">Niezależnie od tego w aplikacji należy skonfigurować te poświadczenia, stosuje tooall aplikacji, a wszystkie subskrypcje w Azure kont.</span><span class="sxs-lookup"><span data-stu-id="774ee-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="774ee-121">tooconfigure poświadczeń na poziomie użytkownika:</span><span class="sxs-lookup"><span data-stu-id="774ee-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="774ee-122">W hello [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="774ee-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="774ee-123">W portalu hello musi mieć co najmniej jedną aplikację, zanim dostęp do bloku poświadczenia wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="774ee-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="774ee-124">Jednak w przypadku hello [interfejsu wiersza polecenia Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), można skonfigurować poświadczeń na poziomie użytkownika bez istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="774ee-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="774ee-125">Skonfiguruj hello nazwę użytkownika i hasło, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="774ee-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="774ee-126">Po ustawieniu poświadczenia wdrażania, można znaleźć hello *Git* username wdrożenia w aplikacji **omówienie**,</span><span class="sxs-lookup"><span data-stu-id="774ee-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="774ee-127">i i *FTP* username wdrożenia w aplikacji **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="774ee-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="774ee-128">Azure nie są wyświetlane hasło użytkownika na poziomie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="774ee-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="774ee-129">Jeśli zapomnisz hasła hello, nie można go pobrać.</span><span class="sxs-lookup"><span data-stu-id="774ee-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="774ee-130">Jednak można zresetować swoje poświadczenia, wykonując kroki hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="774ee-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="774ee-131"><a name="appscope"></a>Pobierz i zresetowanie poświadczeń na poziomie aplikacji</span><span class="sxs-lookup"><span data-stu-id="774ee-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="774ee-132">Dla każdej aplikacji w usłudze App Service, jego poświadczeń na poziomie aplikacji są przechowywane w hello XML profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="774ee-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="774ee-133">tooget poświadczeń na poziomie aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="774ee-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="774ee-134">W hello [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="774ee-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="774ee-135">Kliknij przycisk **... Więcej** > **profilu publikowania Get**, i uruchamia pobierania. Plik ustawień publikacji.</span><span class="sxs-lookup"><span data-stu-id="774ee-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="774ee-136">Otwórz hello. Plik ustawień publikacji i Znajdź hello `<publishProfile>` tag z atrybutem hello `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="774ee-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="774ee-137">Następnie należy pobrać jego `userName` i `password` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="774ee-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="774ee-138">Są to hello poświadczeń na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="774ee-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="774ee-139">Podobne poświadczeń na poziomie użytkownika toohello, username wdrożenia hello FTP jest w formacie hello `<app_name>\<username>`, oraz nazwy użytkownika wdrożenia Git hello jest po prostu `<username>` bez hello poprzedniego `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="774ee-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="774ee-140">tooreset poświadczeń na poziomie aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="774ee-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="774ee-141">W hello [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="774ee-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="774ee-142">Kliknij przycisk **... Więcej** > **Resetowanie profilu publikowania**.</span><span class="sxs-lookup"><span data-stu-id="774ee-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="774ee-143">Kliknij przycisk **tak** tooconfirm hello resetowania.</span><span class="sxs-lookup"><span data-stu-id="774ee-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="774ee-144">Akcja reset Hello unieważnia żadnego pobrane wcześniej. Pliki ustawień publikacji.</span><span class="sxs-lookup"><span data-stu-id="774ee-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="774ee-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="774ee-145">Next steps</span></span>

<span data-ttu-id="774ee-146">Dowiedz się, jak toouse toodeploy te poświadczenia aplikacji z [lokalnego Git](app-service-deploy-local-git.md) lub przy użyciu [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="774ee-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
