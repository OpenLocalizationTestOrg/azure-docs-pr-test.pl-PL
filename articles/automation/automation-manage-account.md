---
title: "Konto usługi Automatyzacja Azure aaaManage | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toomanage hello konfiguracji Twoje konto usługi Automatyzacja, takie jak odnawiania certyfikatu, usuwanie i błędnej konfiguracji."
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
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="aef81-103">Zarządzanie kontem usługi Azure Automation</span><span class="sxs-lookup"><span data-stu-id="aef81-103">Manage Azure Automation account</span></span>
<span data-ttu-id="aef81-104">W pewnym momencie przed upływem Twoje konto usługi Automatyzacja, konieczne będzie toorenew hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="aef81-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="aef81-105">Jeśli uważasz, że naruszono tego hello konta Uruchom jako, można usunąć i ponownie go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="aef81-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="aef81-106">W tej sekcji omówiono sposób tooperform te operacje.</span><span class="sxs-lookup"><span data-stu-id="aef81-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="aef81-107">Odnawianie certyfikatu z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="aef81-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="aef81-108">Witaj podpisem utworzony certyfikat dla hello konta Uruchom jako wygasa rok z daty utworzenia hello.</span><span class="sxs-lookup"><span data-stu-id="aef81-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="aef81-109">Można go odnowić w dowolnym momencie przed wygaśnięciem jego ważności.</span><span class="sxs-lookup"><span data-stu-id="aef81-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="aef81-110">Podczas odnawiania go hello bieżącego prawidłowy certyfikat jest zachowanych tooensure, że wszystkie elementy runbook umieszczonych w kolejce maksymalnie lub aktywnie działa i że uwierzytelniania za pomocą hello konta Uruchom jako nie negatywnie zainfekowane.</span><span class="sxs-lookup"><span data-stu-id="aef81-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="aef81-111">certyfikat Hello pozostaje ważny aż do daty jego wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="aef81-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="aef81-112">Jeśli zostały skonfigurowane z automatyzacji Uruchom jako konta toouse certyfikat wystawiony przez urząd certyfikacji w Twojej organizacji, możesz użyć tej opcji hello firmowy certyfikat zostanie zastąpione przez certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="aef81-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="aef81-113">Witaj toorenew certyfikatów, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="aef81-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="aef81-114">Hello portalu Azure Otwórz hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="aef81-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="aef81-115">Na powitania **konto automatyzacji** bloku w hello **konta właściwości** okienku w obszarze **ustawienia konta**, wybierz pozycję **konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="aef81-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Okienko właściwości konta usługi Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="aef81-117">Na powitania **konta Uruchom jako** bloku właściwości, wybierz albo hello Uruchom jako konta lub hello klasycznego konto Uruchom jako ma toorenew hello certyfikat dla.</span><span class="sxs-lookup"><span data-stu-id="aef81-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="aef81-118">Na powitania **właściwości** bloku hello wybranego konta, kliknij przycisk **odnawiania certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="aef81-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Odnawianie certyfikatu konta Uruchom jako](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="aef81-120">Gdy hello certyfikat zostanie odnowiony, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.</span><span class="sxs-lookup"><span data-stu-id="aef81-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="aef81-121">Usuwanie konta Uruchom jako lub klasycznego konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="aef81-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="aef81-122">W tej sekcji opisano sposób toodelete i ponownie utwórz konto Uruchom jako lub klasycznego Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="aef81-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="aef81-123">Podczas wykonywania tej akcji jest zachowywana hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="aef81-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="aef81-124">Po usunięciu konta Uruchom jako lub klasycznego Uruchom jako, można go utworzyć ponownie w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="aef81-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="aef81-125">Hello portalu Azure Otwórz hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="aef81-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="aef81-126">Na powitania **konto automatyzacji** bloku w hello konta w okienku właściwości, wybierz opcję **konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="aef81-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="aef81-127">Na powitania **konta Uruchom jako** bloku właściwości, albo hello Uruchom jako konto klasycznego konto Uruchom jako lub wybierz konto, które mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="aef81-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="aef81-128">Następnie na powitania **właściwości** bloku hello wybranego konta, kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="aef81-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Usuwanie konta Uruchom jako](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="aef81-130">Gdy konto hello jest usuwany, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.</span><span class="sxs-lookup"><span data-stu-id="aef81-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="aef81-131">Po usunięciu konta hello, można go ponownie utworzyć na powitania **konta Uruchom jako** opcja tworzenia bloku właściwości, wybierając hello **Azure konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="aef81-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Ponownie utwórz konto Uruchom jako automatyzacji hello](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="aef81-133">Błąd konfiguracji</span><span class="sxs-lookup"><span data-stu-id="aef81-133">Misconfiguration</span></span>
<span data-ttu-id="aef81-134">Niektóre elementy konfiguracji niezbędne do toofunction konta Uruchom jako klasycznego konto Uruchom jako lub hello prawidłowo może zostały usunięte lub nieprawidłowo utworzone podczas instalacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="aef81-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="aef81-135">elementy Hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="aef81-135">hello items include:</span></span>

* <span data-ttu-id="aef81-136">Zasób certyfikatu</span><span class="sxs-lookup"><span data-stu-id="aef81-136">Certificate asset</span></span>
* <span data-ttu-id="aef81-137">Zasób połączenia</span><span class="sxs-lookup"><span data-stu-id="aef81-137">Connection asset</span></span>
* <span data-ttu-id="aef81-138">Konto Uruchom jako zostało usunięte z hello roli współautora</span><span class="sxs-lookup"><span data-stu-id="aef81-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="aef81-139">Nazwa główna usługi lub aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="aef81-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="aef81-140">W poprzednim hello i inne wystąpienia błędnej konfiguracji hello konta automatyzacji wykrywa hello zmiany i ma stan *niepełnym* na powitania **konta Uruchom jako** bloku właściwości hello konto.</span><span class="sxs-lookup"><span data-stu-id="aef81-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Stan Niekompletne dla konfiguracji konta Uruchom jako](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="aef81-142">Po wybraniu konta Uruchom jako hello hello konta **właściwości** okienko zawierające hello następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="aef81-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Komunikat ostrzegawczy Niekompletne dla konfiguracji konta Uruchom jako](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="aef81-144">.</span><span class="sxs-lookup"><span data-stu-id="aef81-144">.</span></span>

<span data-ttu-id="aef81-145">Przez usunięcie i ponowne utworzenie konta hello można szybko rozwiązać te problemy Uruchom jako konta.</span><span class="sxs-lookup"><span data-stu-id="aef81-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aef81-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aef81-146">Next steps</span></span>
* <span data-ttu-id="aef81-147">Aby uzyskać więcej informacji na temat nazwy główne usług można znaleźć zbyt[obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="aef81-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="aef81-148">Aby uzyskać więcej informacji na temat opartej na rolach kontroli dostępu w usłudze Automatyzacja Azure można znaleźć zbyt[kontroli dostępu opartej na rolach w automatyzacji Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="aef81-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="aef81-149">Aby uzyskać więcej informacji na temat certyfikatów i usług Azure można znaleźć zbyt[Omówienie certyfikatów dla usług w chmurze Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="aef81-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
