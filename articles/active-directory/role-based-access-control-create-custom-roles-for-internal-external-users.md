---
title: "Tworzenie niestandardowych ról kontroli dostępu opartej na rolach i przypisać do użytkowników wewnętrznych i zewnętrznych na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przypisz role RBAC niestandardowe utworzone przy użyciu programu PowerShell i interfejsu wiersza polecenia dla użytkowników wewnętrznych i zewnętrznych"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="15941-103">Wprowadzenie dotyczących kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="15941-103">Intro on role-based access control</span></span>

<span data-ttu-id="15941-104">Kontrola dostępu oparta na rolach to Azure portalu funkcja tylko stosowanie właściciele subskrypcji do przypisywania ról szczegółowego do innych użytkowników zarządzających zasobów dla określonych zakresów w swoim środowisku.</span><span class="sxs-lookup"><span data-stu-id="15941-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="15941-105">RBAC umożliwia lepsze zarządzanie zabezpieczeniami dla dużych organizacji oraz dla małych i średnich firmach, Praca z zewnętrznym współpracownikom, dostawców lub freelancers, które wymagają dostępu do określonych zasobów w danym środowisku, ale niekoniecznie całej infrastruktury lub żadnych zakresów związanych z rozliczeniami.</span><span class="sxs-lookup"><span data-stu-id="15941-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="15941-106">RBAC umożliwia elastyczność będący właścicielem jedną subskrypcją platformy Azure zarządzanych przez administratora konta (usługi roli administrator na poziomie subskrypcji) i mieć wielu użytkowników zaproszenie do pracy w ramach tej samej subskrypcji, ale bez jakichkolwiek praw administracyjnych dla niego.</span><span class="sxs-lookup"><span data-stu-id="15941-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="15941-107">Zarządzanie i rozliczeń funkcję RBAC okaże się, że czas i zarządzanie wydajne opcji korzystania z funkcji Azure w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="15941-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15941-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="15941-108">Prerequisites</span></span>
<span data-ttu-id="15941-109">W środowisku platformy Azure przy użyciu funkcji RBAC wymaga:</span><span class="sxs-lookup"><span data-stu-id="15941-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="15941-110">Posiadanie autonomiczny subskrypcji platformy Azure powierzonych użytkownika jako właściciela (rola subskrypcji)</span><span class="sxs-lookup"><span data-stu-id="15941-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="15941-111">Rola właściciela subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="15941-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="15941-112">Ma dostęp do [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="15941-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="15941-113">Upewnij się, że ma następujących dostawców zasobów w zarejestrowany dla subskrypcji użytkownika: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="15941-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="15941-114">Aby uzyskać więcej informacji na temat rejestrowania dostawców zasobów, zobacz [dostawców usługi Resource Manager, regiony, wersje interfejsu API i schematów](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="15941-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="15941-115">Licencje usługi Azure Active Directory lub subskrypcji usługi Office 365 (na przykład: dostęp do usługi Azure Active Directory) z usługi Office 365, portal nie jakości przy użyciu funkcji RBAC.</span><span class="sxs-lookup"><span data-stu-id="15941-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="15941-116">Jak można użyć RBAC</span><span class="sxs-lookup"><span data-stu-id="15941-116">How can RBAC be used</span></span>
<span data-ttu-id="15941-117">RBAC można zastosować na trzy różne zakresy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="15941-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="15941-118">Z najwyższą zakresu na najniższym jeden są następujące:</span><span class="sxs-lookup"><span data-stu-id="15941-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="15941-119">Subskrypcja (najwyższy)</span><span class="sxs-lookup"><span data-stu-id="15941-119">Subscription (highest)</span></span>
* <span data-ttu-id="15941-120">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="15941-120">Resource group</span></span>
* <span data-ttu-id="15941-121">Zakres zasobów (najniższy poziom dostępu do oferty docelowe uprawnienia do zakresu poszczególnych zasobów platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="15941-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="15941-122">Przypisz role RBAC w zakresie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="15941-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="15941-123">Istnieją dwie typowe przykłady dotyczące RBAC jest używana (między innymi):</span><span class="sxs-lookup"><span data-stu-id="15941-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="15941-124">Użytkowników zewnętrznych z organizacji (nie jest częścią dzierżawy usługi Azure Active Directory dla użytkownika administracyjnego) zaproszenie do zarządzania niektórych zasobów lub całej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="15941-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="15941-125">Praca z użytkownikami w organizacji (są one częścią dzierżawy usługi Azure Active Directory użytkownika), ale należy do różnych zespołów lub grup, które wymagają szczegółowego dostępu do całej subskrypcji lub do określonych grup zasobów lub zakresy zasobów w środowisku</span><span class="sxs-lookup"><span data-stu-id="15941-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="15941-126">Udziel dostępu na poziomie subskrypcji dla użytkownika poza usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15941-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="15941-127">Role RBAC może zostać przydzielony tylko przez **właścicieli** subskrypcji w związku z tym administrator musi być zalogowany z nazwą użytkownika, które tej roli wstępnie przypisany lub została utworzona subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="15941-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="15941-128">W portalu Azure po można zalogować jako administrator, wybierz "Subskrypcji" i wybierz jedno.</span><span class="sxs-lookup"><span data-stu-id="15941-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="15941-129">![Subskrypcja bloku w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) domyślnie, jeśli dla użytkownika administracyjnego kupiła subskrypcji platformy Azure, użytkownik będzie wyświetlany jako **administrator konta**, to jest rola subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="15941-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="15941-130">Więcej szczegółów na rolach subskrypcji platformy Azure, zobacz [Dodawanie lub zmienianie ról administrator usługi Azure, które zarządzają subskrypcji lub usługi](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="15941-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="15941-131">W tym przykładzie użytkownik "alflanigan@outlook.com" jest **właściciela** z "Bezpłatnej wersji próbnej" subskrypcji w usłudze AAD dzierżawy "Dzierżawy Azure Default".</span><span class="sxs-lookup"><span data-stu-id="15941-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="15941-132">Ponieważ ten użytkownik jest twórca subskrypcji platformy Azure z początkowej Account Microsoft "Outlook" (Account Microsoft = programu Outlook, Live itp.) będzie domyślna nazwa domeny dla wszystkich innych użytkowników dodane w tej dzierżawie **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="15941-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="15941-133">Zgodnie z projektem składni nowej domeny jest tworzony przez zestawienie nazwę użytkownika i domenę nazwę użytkownika, który utworzył dzierżawcy i dodawanie rozszerzenia **". onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="15941-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="15941-134">Ponadto użytkownicy mogą logowania z niestandardowej nazwy domeny w dzierżawie po dodaniu i weryfikowanie jego dla nowej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="15941-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="15941-135">Aby uzyskać więcej szczegółów na sposób weryfikacji niestandardowej nazwy domeny w dzierżawie usługi Azure Active Directory, zobacz [Dodawanie niestandardowej nazwy domeny do katalogu](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="15941-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="15941-136">W tym przykładzie katalog "Domyślna dzierżawa usługi Azure" zawiera tylko użytkownicy z nazwą domeny "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="15941-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="15941-137">Po wybraniu subskrypcji, administrator musi kliknij **kontroli dostępu (IAM)** , a następnie **dodania roli**.</span><span class="sxs-lookup"><span data-stu-id="15941-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Funkcja IAM kontroli dostępu w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Dodaj nowego użytkownika w funkcja IAM kontroli dostępu w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="15941-140">Następnym krokiem jest wybranie roli do przypisania i użytkownika, którego rola RBAC zostanie przypisana do.</span><span class="sxs-lookup"><span data-stu-id="15941-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="15941-141">W **roli** menu rozwijane dla użytkownika administracyjnego widzi tylko wbudowane role RBAC, które są dostępne w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="15941-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="15941-142">Aby uzyskać bardziej szczegółowe wyjaśnienia dotyczące poszczególnych ról i ich zakresy możliwe do przypisania, zobacz [wbudowanych ról dla kontroli dostępu](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="15941-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="15941-143">Następnie administrator musi dodać adres e-mail użytkownika zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="15941-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="15941-144">Oczekiwane zachowanie jest dla użytkownika zewnętrznego, które nie są wyświetlani w istniejącej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="15941-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="15941-145">Po Zaproszono użytkownika zewnętrznego, on będą widoczne w obszarze **subskrypcji > kontroli dostępu (IAM)** z wszystkich bieżących użytkowników, które są obecnie przypisane roli RBAC w zakresie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="15941-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![Dodaj uprawnienia do nowej roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Lista ról RBAC na poziomie subskrypcji](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="15941-148">Użytkownik "chessercarlton@gmail.com" zaproszono jako **właściciela** dla subskrypcji "Bezpłatnej wersji próbnej".</span><span class="sxs-lookup"><span data-stu-id="15941-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="15941-149">Po wysłaniu zaproszenia, zewnętrznych użytkownik otrzyma wiadomość e-mail z potwierdzeniem z link aktywacji.</span><span class="sxs-lookup"><span data-stu-id="15941-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="15941-150">![wiadomość e-mail z zaproszeniem dla roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="15941-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="15941-151">Trwa spoza organizacji, nowy użytkownik nie ma żadnych istniejących atrybutów w katalogu "Domyślna dzierżawa usługi Azure".</span><span class="sxs-lookup"><span data-stu-id="15941-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="15941-152">Będzie można utworzyć po uzyskaniu zgody użytkownika zewnętrznego mają być rejestrowane w katalogu, który jest skojarzony z subskrypcją, który został przydzielony do roli.</span><span class="sxs-lookup"><span data-stu-id="15941-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![wiadomość e-mail zaproszenia dla roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="15941-154">Pokazuje użytkownika zewnętrznego w dzierżawcy usługi Azure Active Directory od teraz jako użytkownik zewnętrzny i to można wyświetlić zarówno w portalu Azure, jak i w klasycznym portalu.</span><span class="sxs-lookup"><span data-stu-id="15941-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![Użytkownicy portalu Azure usługi active directory bloku azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Użytkownicy bloku usługi azure active directory klasycznego portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="15941-157">W **użytkowników** widoku w obu portalach użytkownicy zewnętrzni mogą być rozpoznawane przez:</span><span class="sxs-lookup"><span data-stu-id="15941-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="15941-158">Typ inną ikonę w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="15941-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="15941-159">Inny punkt źródeł w klasycznym portalu</span><span class="sxs-lookup"><span data-stu-id="15941-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="15941-160">Jednak udzielanie **właściciela** lub **współautora** dostępu do użytkownika zewnętrznego w **subskrypcji** zakresu, nie zezwala na dostęp do katalogu dla użytkownika administracyjnego, chyba że **administratora globalnego** pozwala.</span><span class="sxs-lookup"><span data-stu-id="15941-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="15941-161">W ich właściwości użytkownika **typ użytkownika** mającego dwóch parametrów typowych, **elementu członkowskiego** i **gościa** mogą zostać zidentyfikowane.</span><span class="sxs-lookup"><span data-stu-id="15941-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="15941-162">Element członkowski jest użytkownik, który jest zarejestrowany w katalogu, gdy Gość jest użytkownikiem zaproszenie do katalogu z zewnętrznego źródła.</span><span class="sxs-lookup"><span data-stu-id="15941-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="15941-163">Aby uzyskać więcej informacji, zobacz [jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="15941-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="15941-164">Upewnij się, że po wprowadzeniu poświadczeń w portalu, zewnętrznych użytkownik wybierze do logowania się w poprawnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="15941-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="15941-165">Tego samego użytkownika może mieć dostęp do wielu katalogów i można wybrać jedną z nich, klikając nazwę użytkownika w góry po prawej stronie w portalu Azure a następnie wybierz odpowiedniego katalogu z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="15941-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="15941-166">Będąc gościa w katalogu użytkownika zewnętrznego mogą zarządzać zasobami wszystkich subskrypcji platformy Azure, ale nie można uzyskać dostępu do katalogu.</span><span class="sxs-lookup"><span data-stu-id="15941-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![dostęp ograniczony do portalu Azure usługi azure active directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="15941-168">Azure Active Directory i subskrypcji platformy Azure nie ma relacji relacji nadrzędny podrzędny, takich jak innych zasobów platformy Azure (na przykład: maszyn wirtualnych, sieci wirtualnych, aplikacje sieci web, magazynu itp.) z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="15941-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="15941-169">Wszystkie ostatnie jest tworzony, zarządzane i rozliczany w ramach subskrypcji platformy Azure, podczas gdy subskrypcji platformy Azure jest używany do zarządzania dostępem do usługi Azure directory.</span><span class="sxs-lookup"><span data-stu-id="15941-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="15941-170">Aby uzyskać więcej informacji, zobacz [subskrypcji jak Azure jest powiązana z usługą Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="15941-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="15941-171">Z wszystkich wbudowane role RBAC **właściciela** i **współautora** oferują pełnego zarządzania dostęp do wszystkich zasobów w środowisku różnica, że współautora nie może tworzyć i usuwać nowe role RBAC.</span><span class="sxs-lookup"><span data-stu-id="15941-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="15941-172">Inne role wbudowane, takich jak **współautora maszyny wirtualnej** oferować pełnego zarządzania dostęp tylko do zasobów, jest określany przez nazwę, niezależnie od tego **grupy zasobów** jest tworzona w.</span><span class="sxs-lookup"><span data-stu-id="15941-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="15941-173">Przypisywanie roli RBAC wbudowanych **Współautor·maszyny·wirtualnej** na poziomie subskrypcji, oznacza, że użytkownikowi przypisano rolę:</span><span class="sxs-lookup"><span data-stu-id="15941-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="15941-174">Można wyświetlić wszystkich maszyn wirtualnych niezależnie od daty wdrożenia i grupy zasobów, które są częścią</span><span class="sxs-lookup"><span data-stu-id="15941-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="15941-175">Ma dostęp do pełnego zarządzania do maszyn wirtualnych w subskrypcji</span><span class="sxs-lookup"><span data-stu-id="15941-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="15941-176">Nie można wyświetlić inne typy zasobów w subskrypcji</span><span class="sxs-lookup"><span data-stu-id="15941-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="15941-177">Nie można wykonać operacji zmiany z punktu widzenia rozliczeń</span><span class="sxs-lookup"><span data-stu-id="15941-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="15941-178">RBAC jest funkcją Azure tylko portalu, nie udziela dostępu do klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="15941-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="15941-179">Przypisywanie roli RBAC wbudowanych do użytkownika zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="15941-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="15941-180">Dla innego scenariusza, w tym teście użytkownika zewnętrznego "alflanigan@gmail.com" zostanie dodany jako **Współautor·maszyny·wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="15941-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![wbudowana Rola współautora maszyny wirtualnej](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="15941-182">Normalne zachowanie dla tego użytkownika zewnętrznego z tą rolą wbudowanych jest wyświetlanie i zarządzanie nimi tylko maszyny wirtualne i ich sąsiadujących ze sobą Menedżer zasobów tylko zasoby niezbędne podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="15941-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="15941-183">Zgodnie z projektem, te role ograniczone oferują dostęp tylko do ich zasobów odpowiedniego utworzone w portalu Azure, niezależnie od tego niektóre nadal można wdrożyć w portalu klasycznym (na przykład: maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="15941-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![Omówienie roli współautora maszyny wirtualnej w portalu azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="15941-185">Udziel dostępu na poziomie subskrypcji dla użytkownika w tym samym katalogu</span><span class="sxs-lookup"><span data-stu-id="15941-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="15941-186">Przepływ procesu jest taki sam jak dodawanie użytkownika zewnętrznego, zarówno z perspektywy administracyjnej przyznania roli RBAC, a także użytkownika zostanie im przyznany dostęp do roli.</span><span class="sxs-lookup"><span data-stu-id="15941-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="15941-187">Różnica polega na tym że zaproszonych użytkownik nie będzie otrzymywać żadnych zaproszeń do skorzystania z poczty e-mail, jak wszystkie zakresy zasobów w subskrypcji będą dostępne na pulpicie nawigacyjnym po zalogowaniu się.</span><span class="sxs-lookup"><span data-stu-id="15941-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="15941-188">Przypisz role RBAC w zakresie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="15941-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="15941-189">Przypisywanie roli RBAC **grupy zasobów** zakres ma taki sam proces przypisywania roli na poziomie subskrypcji dla obu typów użytkownicy — zewnętrznym lub wewnętrznym (część z tym samym katalogu).</span><span class="sxs-lookup"><span data-stu-id="15941-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="15941-190">Użytkownicy, którzy mają przypisaną rolę RBAC ma zobacz w swoim środowisku tylko grupy zasobów z przypisanym dostępem z **grup zasobów** ikonę w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15941-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="15941-191">Przypisz role RBAC w zakresie zasobów</span><span class="sxs-lookup"><span data-stu-id="15941-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="15941-192">Przypisywanie roli RBAC w zakresie zasobów na platformie Azure mają identyczne proces przypisywania roli na poziomie subskrypcji lub na poziomie grupy zasobów, po tym samym przepływie pracy w obydwu scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="15941-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="15941-193">Ponownie, użytkowników, którzy mają przypisaną rolę RBAC można zobaczyć tylko elementy, które przypisano dostępu do w **wszystkie zasoby** kartę lub bezpośrednio w ich pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="15941-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="15941-194">Jest istotnym elementem do RBAC zarówno w zakresie grupy zasobów lub zasobów zakresie użytkownikom upewnij się, że do logowania się w poprawnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="15941-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![katalog logowania w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="15941-196">Przypisz role RBAC dla grupy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15941-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="15941-197">Wszystkie scenariusze na trzy różne zakresy na platformie Azure przy użyciu funkcji RBAC oferują uprawnienie Zarządzanie, wdrażanie i administrowanie różnych zasobów jako przypisany użytkownik bez konieczności zarządzania osobiste subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="15941-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="15941-198">Niezależnie od roli RBAC jest przypisany do subskrypcji, grupy zasobów lub zasobów zakresu, wszystkie zasoby utworzone dalej przez przypisanych użytkowników są rozliczane zgodnie z jedną subskrypcją platformy Azure, której użytkownicy mają dostęp do.</span><span class="sxs-lookup"><span data-stu-id="15941-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="15941-199">Dzięki temu użytkowników, którzy mają rozliczeń uprawnień administratora dla całej subskrypcji platformy Azure ma pełny przegląd zużycia, niezależnie od tego, kto jest zarządzania zasobami.</span><span class="sxs-lookup"><span data-stu-id="15941-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="15941-200">W przypadku większych organizacji role RBAC można zastosować w taki sam sposób dla uwzględnieniu perspektywy administrator chce szczegółowego dostęp dla zespołów lub całego działów, indywidualnie dla każdego użytkownika, w związku z tym uwzględnieniu bardzo czas i zarządzanie wydajne opcja grup usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15941-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="15941-201">Przykład ilustrujący **współautora** rola została dodana do jednej z grup w dzierżawie na poziomie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="15941-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![Dodaj rolę RBAC dla grup usługi AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="15941-203">Te grupy są grupami zabezpieczeń, które są udostępniane i zarządzane tylko w ramach usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15941-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="15941-204">Utwórz niestandardową rolę RBAC można otworzyć żądania obsługi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="15941-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="15941-205">Wbudowane role RBAC, które są dostępne w systemie Azure zapewnia określone poziomy uprawnień na podstawie dostępnych zasobów w środowisku.</span><span class="sxs-lookup"><span data-stu-id="15941-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="15941-206">Jeśli żadna z tych ról potrzeb dla użytkownika administracyjnego, istnieje jednak możliwość ograniczenia dostępu nawet więcej, tworząc niestandardowe role RBAC.</span><span class="sxs-lookup"><span data-stu-id="15941-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="15941-207">Tworzenie niestandardowych ról RBAC wymaga, aby zająć jedną rolę wbudowanych, edycji, a następnie zaimportuj go ponownie w środowisku.</span><span class="sxs-lookup"><span data-stu-id="15941-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="15941-208">Pobieranie i przekazywania roli są zarządzane przy użyciu programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="15941-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="15941-209">Należy zrozumieć wymagania wstępne utworzenia niestandardowej roli zabezpieczeń, które można udostępniać szczegółowe na poziomie subskrypcji, a także umożliwić zaproszonych użytkowników elastyczność otwarcia żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="15941-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="15941-210">W tym przykładzie wbudowanej roli **czytnika** umożliwia użytkownikom dostęp do wyświetlania wszystkich zakresów zasobów, ale nie do je edytować lub utworzyć nowe został dostosowany do Zezwalaj użytkownikom z możliwością otwarcia żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="15941-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="15941-211">Pierwszą akcją eksportowania **czytnika** roli musi zostać wykonane w programie PowerShell został uruchomiony z podwyższonym poziomem uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="15941-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Zrzut ekranu programu PowerShell dla roli czytnika RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="15941-213">Następnie należy wyodrębnić szablonu JSON w roli.</span><span class="sxs-lookup"><span data-stu-id="15941-213">Then you need to extract the JSON template of the role.</span></span>





![Szablon JSON dla niestandardowej roli zabezpieczeń czytnika RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="15941-215">Typowa rola RBAC składa się z trzech głównych sekcji, **akcje**, **NotActions** i **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="15941-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="15941-216">W **akcji** sekcji są wymienione wszystkie działania dozwolone dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="15941-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="15941-217">Należy zrozumieć, że każda akcja przypisano od dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="15941-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="15941-218">W takim przypadku służący do tworzenia biletów pomocy technicznej **Microsoft.Support** musi być wymieniona dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="15941-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="15941-219">Aby można było wyświetlić wszystkich dostawców zasobów dostępnych i zarejestrowanych w ramach subskrypcji, można użyć programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15941-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="15941-220">Ponadto można sprawdzić wszystkie dostępne polecenia cmdlet programu PowerShell do zarządzania dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="15941-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="15941-221">![Zrzut ekranu programu PowerShell do zarządzania dostawcy zasobów](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="15941-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="15941-222">Aby ograniczyć wszystkie akcje dla określonej roli RBAC, dostawców zasobów są wymienione w sekcji **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="15941-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="15941-223">Ostatnio jest to konieczne, że rola RBAC zawiera jawne subskrypcji identyfikatorów, w którym została użyta.</span><span class="sxs-lookup"><span data-stu-id="15941-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="15941-224">Identyfikatory subskrypcji są wyświetlane w obszarze **AssignableScopes**, w przeciwnym razie będzie nie można zaimportować roli w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="15941-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="15941-225">Po utworzeniu i dostosowywanie roli RBAC, musi zostać zaimportowany kopii środowiska.</span><span class="sxs-lookup"><span data-stu-id="15941-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="15941-226">W tym przykładzie niestandardową nazwę dla tej roli RBAC jest "Czytnika obsługi biletów poziom dostępu" dzięki czemu użytkownik, aby wyświetlić wszystkie elementy w ramach subskrypcji, a także do otwarcia żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="15941-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="15941-227">Są dwa tylko wbudowane role RBAC umożliwiając akcji otwarcia żądania pomocy technicznej **właściciela** i **współautora**.</span><span class="sxs-lookup"><span data-stu-id="15941-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="15941-228">Użytkownik może mieć możliwość otwarcia żądania pomocy technicznej on musi posiadać rolę RBAC tylko w zakresie subskrypcji, ponieważ wszystkie żądania pomocy technicznej są tworzone na podstawie subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="15941-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="15941-229">Tę rolę niestandardową nowe zostanie przypisana do użytkownika z tym samym katalogu.</span><span class="sxs-lookup"><span data-stu-id="15941-229">This new custom role has been assigned to an user from the same directory.</span></span>





![Zrzut ekranu przedstawiający niestandardową rolę RBAC zaimportowany w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Zrzut ekranu przedstawiający przypisywanie niestandardowej roli zabezpieczeń RBAC zaimportowane do użytkownika w tym samym katalogu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Zrzut ekranu przedstawiający uprawnienia niestandardowe importowanych roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="15941-233">Przykład został opisany bardziej szczegółowo aby podkreślić limitów tę rolę niestandardową RBAC w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="15941-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="15941-234">Można tworzyć nowe żądania pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="15941-234">Can create new support requests</span></span>
* <span data-ttu-id="15941-235">Nie można utworzyć nowe zakresy zasobów (na przykład: maszyny wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="15941-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="15941-236">Nie można utworzyć nowej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="15941-236">Can't create new resource groups</span></span>





![Zrzut ekranu przedstawiający niestandardową rolę RBAC tworzenia żądań obsługi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![Zrzut ekranu przedstawiający niestandardową rolę RBAC nie można utworzyć maszyny wirtualne](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![Zrzut ekranu przedstawiający niestandardowych nie można utworzyć nowego RGs roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="15941-240">Utwórz niestandardową rolę RBAC można otworzyć żądania obsługi przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="15941-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="15941-241">Uruchomiony na komputerze Mac i bez uzyskiwania dostępu do programu PowerShell, interfejsu wiersza polecenia Azure to sposób go.</span><span class="sxs-lookup"><span data-stu-id="15941-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="15941-242">Kroki umożliwiające utworzenie niestandardowej roli zabezpieczeń są takie same, z wyjątkiem wyłącznie przy użyciu interfejsu wiersza polecenia roli nie można pobrać szablonu JSON, ale można je wyświetlić w interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="15941-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="15941-243">W tym przykładzie wybrano I wbudowana rola **czytnika kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="15941-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Pokaż zrzut ekranu interfejsu wiersza polecenia rolę czytelnika kopii zapasowej](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="15941-245">Edytowanie roli w programie Visual Studio po skopiowaniu ich właściwości w szablonie JSON **Microsoft.Support** dostawca zasobów został dodany w **akcje** sekcjach, aby ten użytkownik może otworzyć żądania pomocy technicznej pozostawiając można czytnik dla magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="15941-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="15941-246">Ponownie należy dodać identyfikator subskrypcji, w którym ta rola będzie używany w **AssignableScopes** sekcji.</span><span class="sxs-lookup"><span data-stu-id="15941-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Zrzut ekranu interfejsu wiersza polecenia importowania niestandardowej roli zabezpieczeń RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="15941-248">Nowa rola jest teraz dostępna w portalu Azure i proces assignation jest taki sam, jak w poprzednich przykładach.</span><span class="sxs-lookup"><span data-stu-id="15941-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![Azure portalu zrzut ekranu przedstawiający niestandardową rolę RBAC utworzone za pomocą interfejsu wiersza polecenia 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="15941-250">Od najnowszej 2017 kompilacji powłoka chmury Azure jest ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="15941-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="15941-251">Powłoka chmury Azure jest uzupełnienie IDE i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="15941-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="15941-252">Z tą usługą Pobierz powłoką bazujące na przeglądarce, która jest uwierzytelniane i hostowanej na platformie Azure i można go użyć zamiast interfejsu wiersza polecenia na komputerze jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="15941-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Powłoka w chmurze Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
