---
title: "Poświadczenia wdrożenia usługi Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać poświadczenia wdrożenia usługi Azure App Service."
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
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="c2bd9-103">Skonfiguruj poświadczenia wdrażania dla usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c2bd9-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="c2bd9-104">[Usługa aplikacji Azure](http://go.microsoft.com/fwlink/?LinkId=529714) obsługuje dwa rodzaje poświadczenia [lokalnego wdrożenia Git](app-service-deploy-local-git.md) i [wdrożenia FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="c2bd9-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="c2bd9-105">Nie są takie same, jak poświadczenia usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="c2bd9-106">**Poświadczenia użytkownika na poziomie**: jeden zestaw poświadczeń dla całego konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="c2bd9-107">Może służyć do wdrożenia do usługi App Service dla dowolnej aplikacji, w żadnej subskrypcji z uprawnień dostępu do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="c2bd9-108">Są to domyślny zestaw poświadczeń, skonfigurowanym w **usługi aplikacji** > **&lt;nazwa_aplikacji >** > **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="c2bd9-109">Jest to domyślny zestaw, który jest wyświetlana w portalu graficznego interfejsu użytkownika (takich jak **— omówienie** i **właściwości** aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="c2bd9-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c2bd9-110">Podczas delegować dostęp do zasobów platformy Azure przy użyciu kontroli dostępu na podstawie ról (RBAC) lub współadministratora uprawnienia, każdy użytkownik usługi Azure, który uzyskuje dostęp do aplikacji można użyć jego osobistych poświadczeń na poziomie użytkownika do momentu dostęp został odwołany.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="c2bd9-111">Te poświadczenia wdrożenia nie powinny być udostępniać innym użytkownikom Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="c2bd9-112">**Poświadczeń na poziomie aplikacji**: jeden zestaw poświadczeń dla każdej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="c2bd9-113">Może służyć do wdrożenia tej aplikacji tylko.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="c2bd9-114">Poświadczenia dla każdej aplikacji jest generowany automatycznie podczas tworzenia aplikacji i znajduje się w aplikacji profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="c2bd9-115">Nie można ręcznie skonfigurować poświadczenia, ale można je zresetować w każdej chwili dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c2bd9-116">Aby dać komuś dostęp do tych poświadczeń za pomocą roli na podstawie kontroli dostępu (RBAC), które należy rozważyć ich współautora lub nowszego w aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="c2bd9-117">Czytelnicy nie mogą opublikować i dlatego nie można uzyskać dostępu do tych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="c2bd9-118"><a name="userscope"></a>Ustaw i zresetowanie poświadczeń na poziomie użytkownika</span><span class="sxs-lookup"><span data-stu-id="c2bd9-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="c2bd9-119">Poświadczenia na poziomie użytkownika można skonfigurować w dowolnej aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="c2bd9-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="c2bd9-120">Niezależnie od tego w aplikacji należy skonfigurować te poświadczenia, ma to zastosowanie do wszystkich aplikacji i dla wszystkich subskrypcji na koncie Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="c2bd9-121">Aby skonfigurować poświadczeń na poziomie użytkownika:</span><span class="sxs-lookup"><span data-stu-id="c2bd9-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="c2bd9-122">W [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c2bd9-123">W portalu musi mieć co najmniej jedną aplikację, aby dostęp do bloku poświadczenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="c2bd9-124">Jednak w przypadku [interfejsu wiersza polecenia Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), można skonfigurować poświadczeń na poziomie użytkownika bez istniejącej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="c2bd9-125">Konfigurowanie nazwy użytkownika i hasła, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="c2bd9-126">Po ustawieniu poświadczenia wdrażania, można znaleźć *Git* username wdrożenia w aplikacji **omówienie**,</span><span class="sxs-lookup"><span data-stu-id="c2bd9-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="c2bd9-127">i i *FTP* username wdrożenia w aplikacji **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="c2bd9-128">Azure nie są wyświetlane hasło użytkownika na poziomie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="c2bd9-129">Jeśli zapomnisz hasło, nie można go pobrać.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="c2bd9-130">Jednak można zresetować swoje poświadczenia, wykonując kroki opisane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="c2bd9-131"><a name="appscope"></a>Pobierz i zresetowanie poświadczeń na poziomie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c2bd9-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="c2bd9-132">Dla każdej aplikacji w usłudze App Service, jego poświadczeń na poziomie aplikacji są przechowywane w pliku XML profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="c2bd9-133">Aby uzyskać poświadczeń z poziomu aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c2bd9-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="c2bd9-134">W [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="c2bd9-135">Kliknij przycisk **... Więcej** > **profilu publikowania Get**, i uruchamia pobierania. Plik ustawień publikacji.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="c2bd9-136">Otwórz. Plik ustawień publikacji i Znajdź `<publishProfile>` tag z atrybutem `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="c2bd9-137">Następnie należy pobrać jego `userName` i `password` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="c2bd9-138">Są to poświadczeń na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="c2bd9-139">Podobnie jak poświadczeń na poziomie użytkownika, nazwa użytkownika wdrożenia FTP jest w formacie `<app_name>\<username>`, i username wdrożenia Git jest po prostu `<username>` bez poprzedzających `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="c2bd9-140">Aby zresetować poświadczeń na poziomie aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c2bd9-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="c2bd9-141">W [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="c2bd9-142">Kliknij przycisk **... Więcej** > **Resetowanie profilu publikowania**.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="c2bd9-143">Kliknij przycisk **tak** o potwierdzenie resetowania.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="c2bd9-144">Akcja reset unieważnia żadnego pobrane wcześniej. Pliki ustawień publikacji.</span><span class="sxs-lookup"><span data-stu-id="c2bd9-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2bd9-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2bd9-145">Next steps</span></span>

<span data-ttu-id="c2bd9-146">Dowiedz się, jak używać tych poświadczeń do wdrożenia aplikacji z [lokalnego Git](app-service-deploy-local-git.md) lub przy użyciu [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="c2bd9-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
