---
title: "Zarządzanie kontem usługi Azure Automation | Microsoft Docs"
description: "W tym artykule opisano sposób zarządzania konfiguracją konta usługi Automation obejmującą np. odnawianie certyfikatów, usuwanie i błędną konfigurację."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 41efdbcacede74bac038342688362ff480cadc7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="5c043-103">Zarządzanie kontem usługi Azure Automation</span><span class="sxs-lookup"><span data-stu-id="5c043-103">Manage Azure Automation account</span></span>
<span data-ttu-id="5c043-104">W pewnym momencie przed wygaśnięciem ważności konta usługi Automation należy odnowić certyfikat.</span><span class="sxs-lookup"><span data-stu-id="5c043-104">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="5c043-105">Jeśli uważasz, że bezpieczeństwo konta Uruchom jako zostało naruszone, możesz je usunąć i utworzyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="5c043-105">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="5c043-106">W tej sekcji opisano kroki umożliwiające wykonanie tych operacji.</span><span class="sxs-lookup"><span data-stu-id="5c043-106">This section discusses how to perform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="5c043-107">Odnawianie certyfikatu z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="5c043-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="5c043-108">Certyfikat z podpisem własnym utworzony dla konta Uruchom jako wygasa rok od daty utworzenia.</span><span class="sxs-lookup"><span data-stu-id="5c043-108">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="5c043-109">Można go odnowić w dowolnym momencie przed wygaśnięciem jego ważności.</span><span class="sxs-lookup"><span data-stu-id="5c043-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="5c043-110">Po odnowieniu bieżący ważny certyfikat zostanie zachowany w celu zapewnienia, że ta zmiana nie wpłynie negatywnie na żadne umieszczone w kolejce lub aktywnie działające elementy runbook, które uwierzytelniają się przy użyciu konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="5c043-110">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="5c043-111">Certyfikat pozostanie ważny aż do daty wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="5c043-111">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="5c043-112">Jeśli konto Uruchom jako usługi Automation skonfigurowano do użycia certyfikatu wystawionego przez urząd certyfikacji przedsiębiorstwa, w przypadku użycia tej opcji certyfikat przedsiębiorstwa zostanie zastąpiony certyfikatem z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="5c043-112">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="5c043-113">Aby odnowić certyfikat, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c043-113">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="5c043-114">W witrynie Azure Portal otwórz konto usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="5c043-114">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="5c043-115">W bloku **Konto usługi Automation** w okienku **Właściwości konta** w obszarze **Ustawienia konta** wybierz pozycję **Konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="5c043-115">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Okienko właściwości konta usługi Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="5c043-117">W bloku właściwości **Konta Uruchom jako** wybierz konto Uruchom jako albo klasyczne konto Uruchom jako, dla którego chcesz odnowić certyfikat.</span><span class="sxs-lookup"><span data-stu-id="5c043-117">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="5c043-118">W bloku **Właściwości** wybranego konta kliknij pozycję **Odnów certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="5c043-118">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Odnawianie certyfikatu konta Uruchom jako](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="5c043-120">W trakcie odnawiania certyfikatu postęp można śledzić po wybraniu z menu opcji **Powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="5c043-120">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="5c043-121">Usuwanie konta Uruchom jako lub klasycznego konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="5c043-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="5c043-122">W tej sekcji opisano sposób usuwania i ponownego tworzenia konta Uruchom jako lub klasycznego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="5c043-122">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="5c043-123">Konto usługi Automation jest zachowywane podczas wykonywania tej akcji.</span><span class="sxs-lookup"><span data-stu-id="5c043-123">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="5c043-124">Po usunięciu konta Uruchom jako lub klasycznego konta Uruchom jako możesz je ponownie utworzyć w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="5c043-124">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="5c043-125">W witrynie Azure Portal otwórz konto usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="5c043-125">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="5c043-126">W bloku **Konto usługi Automation** w okienku właściwości konta wybierz pozycję **Konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="5c043-126">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="5c043-127">W bloku właściwości **Konta Uruchom jako** wybierz konto Uruchom jako albo klasyczne konto Uruchom jako, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="5c043-127">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="5c043-128">Następnie w bloku **Właściwości** wybranego konta kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="5c043-128">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Usuwanie konta Uruchom jako](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="5c043-130">W trakcie usuwania konta postęp można śledzić po wybraniu z menu opcji **Powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="5c043-130">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="5c043-131">Po usunięciu konta możesz je ponownie utworzyć w bloku właściwości **Konta Uruchom jako**, wybierając opcję tworzenia **Konto Uruchom jako platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="5c043-131">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Ponowne tworzenie konta Uruchom jako usługi Automation](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="5c043-133">Błąd konfiguracji</span><span class="sxs-lookup"><span data-stu-id="5c043-133">Misconfiguration</span></span>
<span data-ttu-id="5c043-134">Niektóre elementy konfiguracji niezbędne do poprawnego działania konta Uruchom jako lub klasycznego konta Uruchom jako zostały usunięte lub nie zostały utworzone prawidłowo podczas początkowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5c043-134">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="5c043-135">Te elementy to na przykład:</span><span class="sxs-lookup"><span data-stu-id="5c043-135">The items include:</span></span>

* <span data-ttu-id="5c043-136">Zasób certyfikatu</span><span class="sxs-lookup"><span data-stu-id="5c043-136">Certificate asset</span></span>
* <span data-ttu-id="5c043-137">Zasób połączenia</span><span class="sxs-lookup"><span data-stu-id="5c043-137">Connection asset</span></span>
* <span data-ttu-id="5c043-138">Konto Uruchom jako zostało usunięte z roli współautora</span><span class="sxs-lookup"><span data-stu-id="5c043-138">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="5c043-139">Nazwa główna usługi lub aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c043-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="5c043-140">W poprzednim i innych przypadkach błędnej konfiguracji konto usługi Automation wykrywa te zmiany i wyświetla stan *Niekompletne* w bloku właściwości **Konta Uruchom jako** dla konta.</span><span class="sxs-lookup"><span data-stu-id="5c043-140">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Stan Niekompletne dla konfiguracji konta Uruchom jako](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="5c043-142">Po wybraniu konta Uruchom jako w okienku **Właściwości** konta zostanie wyświetlony następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="5c043-142">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Komunikat ostrzegawczy Niekompletne dla konfiguracji konta Uruchom jako](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="5c043-144">.</span><span class="sxs-lookup"><span data-stu-id="5c043-144">.</span></span>

<span data-ttu-id="5c043-145">Te problemy związane z kontem Uruchom jako można szybko rozwiązać, usuwając konto i tworząc je ponownie.</span><span class="sxs-lookup"><span data-stu-id="5c043-145">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c043-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5c043-146">Next steps</span></span>
* <span data-ttu-id="5c043-147">Więcej informacji na temat nazw głównych usługi można znaleźć w temacie [Obiekty aplikacji i obiekty nazwę głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="5c043-147">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="5c043-148">Więcej informacji na temat kontroli dostępu opartej na rolach w usłudze Automatyzacja platformy Azure można znaleźć w temacie [Kontrola dostępu oparta na rolach w usłudze Automatyzacja platformy Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="5c043-148">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="5c043-149">Aby uzyskać więcej informacji na temat certyfikatów i usług Azure, zobacz [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md) (Omówienie certyfikatów usług Azure Cloud Services).</span><span class="sxs-lookup"><span data-stu-id="5c043-149">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>