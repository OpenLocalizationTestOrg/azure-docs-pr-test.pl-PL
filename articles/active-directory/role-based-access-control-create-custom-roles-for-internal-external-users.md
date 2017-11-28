---
title: "role niestandardowe kontroli dostępu opartej na rolach aaaCreate i przypisać toointernal i użytkowników zewnętrznych na platformie Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="ab7d7-103">Wprowadzenie dotyczących kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="ab7d7-103">Intro on role-based access control</span></span>

<span data-ttu-id="ab7d7-104">Kontrola dostępu oparta na rolach to Azure portalu tylko funkcja umożliwia hello właściciele subskrypcji tooassign szczegółowego ról tooother użytkownikom, którzy mogą zarządzać zasobów dla określonych zakresów w swoim środowisku.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="ab7d7-105">RBAC umożliwia lepsze zarządzanie zabezpieczeniami dla dużych organizacji oraz dla małych i średnich firmach praca z zewnętrznym współpracownikom, dostawców lub freelancers, które wymagają dostępu do zasobów toospecific w danym środowisku, ale niekoniecznie toohello całej infrastruktury lub w dowolnej zakresy związanych z rozliczeniami.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="ab7d7-106">RBAC zapewnia elastyczność hello będący właścicielem jedną subskrypcją platformy Azure zarządza hello konta administratora (usługi roli administrator na poziomie subskrypcji) i ma wiele toowork zaproszonych użytkowników w obszarze hello tej samej subskrypcji ale bez żadnych administracyjnych prawa dla niego.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="ab7d7-107">Zarządzanie i rozliczeń funkcji RBAC hello okaże się toobe czas i zarządzanie wydajne opcji korzystania z funkcji Azure w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab7d7-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ab7d7-108">Prerequisites</span></span>
<span data-ttu-id="ab7d7-109">Przy użyciu funkcji RBAC w hello środowiska platformy Azure wymaga:</span><span class="sxs-lookup"><span data-stu-id="ab7d7-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="ab7d7-110">O autonomiczny subskrypcji platformy Azure przypisane toohello użytkownika jako właściciela (rola subskrypcji)</span><span class="sxs-lookup"><span data-stu-id="ab7d7-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="ab7d7-111">Ma rolę właściciela hello hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ab7d7-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="ab7d7-112">Ma dostęp toohello [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ab7d7-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="ab7d7-113">Upewnij się, że hello toohave następujących dostawców zasobów zarejestrowany dla subskrypcji użytkownika hello: **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="ab7d7-114">Aby uzyskać więcej informacji dotyczących sposobu tooregister hello dostawców zasobów, zobacz [dostawców usługi Resource Manager, regiony, wersje interfejsu API i schematów](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="ab7d7-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ab7d7-115">Licencje usługi Azure Active Directory lub subskrypcji usługi Office 365 (na przykład: dostęp do usługi Active Directory tooAzure) pobranego z portalu nie jakości przy użyciu funkcji RBAC hello usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="ab7d7-116">Jak można użyć RBAC</span><span class="sxs-lookup"><span data-stu-id="ab7d7-116">How can RBAC be used</span></span>
<span data-ttu-id="ab7d7-117">RBAC można zastosować na trzy różne zakresy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="ab7d7-118">Z hello najwyższy toohello zakres jednej najniższy są następujące:</span><span class="sxs-lookup"><span data-stu-id="ab7d7-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="ab7d7-119">Subskrypcja (najwyższy)</span><span class="sxs-lookup"><span data-stu-id="ab7d7-119">Subscription (highest)</span></span>
* <span data-ttu-id="ab7d7-120">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="ab7d7-120">Resource group</span></span>
* <span data-ttu-id="ab7d7-121">Zakres zasobów (hello najniższy poziom dostępu oferty uprawnienia docelowego zakresu poszczególnych zasobów platformy Azure tooan)</span><span class="sxs-lookup"><span data-stu-id="ab7d7-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="ab7d7-122">Przypisz role RBAC w zakresie subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="ab7d7-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="ab7d7-123">Istnieją dwie typowe przykłady dotyczące RBAC jest używana (między innymi):</span><span class="sxs-lookup"><span data-stu-id="ab7d7-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="ab7d7-124">Użytkowników zewnętrznych z hello organizacji (nie jest częścią dzierżawy usługi Azure Active Directory użytkownika administratora hello) zaproszenie toomanage niektórych zasobów lub subskrypcji całego hello</span><span class="sxs-lookup"><span data-stu-id="ab7d7-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="ab7d7-125">Praca z użytkownikami w organizacji hello (są one częścią hello użytkownik dzierżawy usługi Azure Active Directory), ale należy do różnych zespołów lub grup, które wymagają dostępu szczegółowe albo toohello całej subskrypcji lub grupy zasobów toocertain lub zasobu zakresów w hello środowisko</span><span class="sxs-lookup"><span data-stu-id="ab7d7-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="ab7d7-126">Udziel dostępu na poziomie subskrypcji dla użytkownika poza usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab7d7-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="ab7d7-127">Role RBAC może zostać przydzielony tylko przez **właścicieli** hello subskrypcji w związku z tym hello administrator musi być zalogowany z nazwą użytkownika, które tej roli wstępnie przypisany lub został utworzony hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="ab7d7-128">Z hello portalu Azure po zalogować jako administrator, wybierz pozycję "Subskrypcje" i wybierz opcję hello żądana jeden.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="ab7d7-129">![bloku subskrypcji w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) domyślnie, jeśli administrator hello kupiła hello subskrypcji platformy Azure, hello użytkownika będzie wyświetlany jako **administrator konta**, to jest rola subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="ab7d7-130">Więcej szczegółów na powitania ról subskrypcji platformy Azure, zobacz [Dodawanie lub zmienianie role administratora platformy Azure, zarządzających hello subskrypcji lub usługi](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="ab7d7-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="ab7d7-131">W tym przykładzie hello użytkownika "alflanigan@outlook.com" hello jest **właściciela** z hello "Bezpłatnej wersji próbnej" subskrypcji w hello AAD dzierżawy "Dzierżawy Azure Default".</span><span class="sxs-lookup"><span data-stu-id="ab7d7-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="ab7d7-132">Ponieważ ten użytkownik jest twórca hello hello subskrypcji platformy Azure z hello początkowa Account Microsoft "Outlook" (Account Microsoft = programu Outlook, Live itp.) będzie domyślna nazwa domeny dla wszystkich innych użytkowników dodane w tej dzierżawie powitalnych **"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="ab7d7-133">Zgodnie z projektem hello składni nowej domeny hello jest tworzony przez zestawienie hello nazwy użytkownika i nazwy domen hello użytkownika, który utworzył hello dzierżawy oraz dodawania rozszerzenia hello **". onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="ab7d7-134">Ponadto użytkownicy mogą logowania z niestandardowej nazwy domeny w dzierżawie powitalnych po dodaniu i weryfikowanie jego dla nowej dzierżawy hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="ab7d7-135">Aby uzyskać więcej informacji na tooverify niestandardowej nazwy domeny w dzierżawie usługi Azure Active Directory, zobacz temat [Dodaj katalog tooyour nazwy domeny niestandardowej](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="ab7d7-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="ab7d7-136">W tym przykładzie katalog hello "domyślna dzierżawa usługi Azure" zawiera tylko użytkownicy z nazwą domeny hello "@alflanigan.onmicrosoft.com".</span><span class="sxs-lookup"><span data-stu-id="ab7d7-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="ab7d7-137">Po wybraniu subskrypcji hello, musisz kliknąć przycisk Administrator hello **kontroli dostępu (IAM)** , a następnie **dodania roli**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Funkcja IAM kontroli dostępu w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Dodaj nowego użytkownika w funkcja IAM kontroli dostępu w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="ab7d7-140">Witaj następnym krokiem jest toobe roli hello tooselect przypisane i hello użytkownika, którego hello RBAC roli zostanie przypisana do.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="ab7d7-141">W hello **roli** listy rozwijanej menu hello administratora użytkownik widzi tylko hello wbudowanych RBAC role, które są dostępne w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="ab7d7-142">Aby uzyskać bardziej szczegółowe wyjaśnienia dotyczące poszczególnych ról i ich zakresy możliwe do przypisania, zobacz [wbudowanych ról dla kontroli dostępu](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ab7d7-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="ab7d7-143">Witaj administrator musi następnie tooadd hello adres e-mail użytkownika zewnętrznego hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="ab7d7-144">Hello oczekuje się, że zachowanie jest hello użytkownika zewnętrznego toonot będą wyświetlane w hello istniejącej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="ab7d7-145">Po zaproszono hello użytkownika zewnętrznego, on będą widoczne w obszarze **subskrypcji > kontroli dostępu (IAM)** wszystkim użytkownikom bieżącego hello, które są obecnie przypisane roli RBAC na powitania zakres subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![Dodaj rolę RBAC toonew uprawnień](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Lista ról RBAC na poziomie subskrypcji](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="ab7d7-148">Użytkownik Hello "chessercarlton@gmail.com" został zaproszony toobe **właściciela** dla subskrypcji "Bezpłatnej wersji próbnej" hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="ab7d7-149">Po wysłaniu hello zaproszenia, hello zewnętrznych użytkownik otrzyma wiadomość e-mail z potwierdzeniem z link aktywacji.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="ab7d7-150">![wiadomość e-mail z zaproszeniem dla roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="ab7d7-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="ab7d7-151">Stanowi organizacji toohello zewnętrznych, hello nowego użytkownika nie ma żadnych istniejących atrybutów w katalogu "Dzierżawy Azure Default" hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="ab7d7-152">Będzie można utworzyć po toobe zgody rejestrowane w katalogu hello, który jest skojarzony z subskrypcją hello, który został przydzielony do roli użytkownika zewnętrznego hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![wiadomość e-mail zaproszenia dla roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="ab7d7-154">Użytkownik zewnętrzny Hello pokazuje w hello dzierżawy usługi Azure Active Directory od teraz jako użytkownik zewnętrzny i to można wyświetlić zarówno w hello portalu Azure, jak i w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![Użytkownicy portalu Azure usługi active directory bloku azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Użytkownicy bloku usługi azure active directory klasycznego portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="ab7d7-157">W hello **użytkowników** widoku w obu portalach użytkowników zewnętrznych hello mogą być rozpoznawane przez:</span><span class="sxs-lookup"><span data-stu-id="ab7d7-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="ab7d7-158">Wpisz inną ikonę Hello hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ab7d7-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="ab7d7-159">Witaj różnych sourcing punktu w portalu klasycznym hello</span><span class="sxs-lookup"><span data-stu-id="ab7d7-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="ab7d7-160">Jednak udzielanie **właściciela** lub **współautora** tooan dostępu użytkownika zewnętrznego w hello **subskrypcji** zakresu, nie zezwala na powitania dostępu toohello administratora katalogu użytkownika, o ile hello **administratora globalnego** pozwala.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="ab7d7-161">W ich właściwości użytkownika hello, hello **typ użytkownika** mającego dwóch parametrów typowych, **elementu członkowskiego** i **gościa** mogą zostać zidentyfikowane.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="ab7d7-162">Element członkowski jest użytkownik, który jest zarejestrowany w katalogu hello podczas Gość jest katalogiem toohello zaproszonych użytkowników ze źródła zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="ab7d7-163">Aby uzyskać więcej informacji, zobacz [jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="ab7d7-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="ab7d7-164">Upewnij się, że po wprowadzeniu poświadczeń hello w portalu hello, użytkownik zewnętrzny hello wybiera poprawny katalog hello toosign w celu.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="ab7d7-165">Hello tego samego użytkownika ma katalogów toomultiple dostępu i można wybrać jedną z nich, klikając nazwę użytkownika hello w hello góry po prawej stronie w portalu Azure hello i następnie wybierz z listy rozwijanej hello hello odpowiedniego katalogu.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="ab7d7-166">Będąc gościa w katalogu hello użytkownika zewnętrznego hello można zarządzać wszystkie zasoby hello subskrypcji platformy Azure, ale nie można uzyskać dostępu do katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![dostęp do portalu Azure tooazure ograniczone usługi active directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="ab7d7-168">Azure Active Directory i subskrypcji platformy Azure nie ma relacji relacji nadrzędny podrzędny, takich jak innych zasobów platformy Azure (na przykład: maszyn wirtualnych, sieci wirtualnych, aplikacje sieci web, magazynu itp.) z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="ab7d7-169">Wszystkie ostatnie hello jest tworzony, zarządzane i rozliczane w ramach subskrypcji platformy Azure, gdy subskrypcja platformy Azure jest używana toomanage hello dostępu tooan katalogu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="ab7d7-170">Aby uzyskać więcej informacji, zobacz [jak Azure subskrypcji jest powiązane tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="ab7d7-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="ab7d7-171">Ze wszystkich hello wbudowanych RBAC ról **właściciela** i **współautora** oferują pełnego dostępu do zasobów tooall w środowisku hello, hello różnica podpisu współautora nie można utworzyć i usuwania nowych Role RBAC.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="ab7d7-172">Witaj innych wbudowanych ról, takich jak **współautora maszyny wirtualnej** oferują dostęp do pełnego zarządzania tylko zasoby toohello wskazywanym przez nazwę hello, niezależnie od hello **grupy zasobów** ich tworzenia do.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="ab7d7-173">Przypisywanie hello wbudowanych RBAC roli **współautora maszyny wirtualnej** na poziomie subskrypcji, oznacza tej roli hello przypisane przez użytkownika hello:</span><span class="sxs-lookup"><span data-stu-id="ab7d7-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="ab7d7-174">Można wyświetlić wszystkich maszyn wirtualnych niezależnie od ich wdrożenia daty i hello grup zasobów, które są częścią</span><span class="sxs-lookup"><span data-stu-id="ab7d7-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="ab7d7-175">Zawiera maszyny wirtualne toohello dostęp do pełnego zarządzania w ramach subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="ab7d7-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="ab7d7-176">Nie można wyświetlić inne typy zasobów w subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="ab7d7-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="ab7d7-177">Nie można wykonać operacji zmiany z punktu widzenia rozliczeń</span><span class="sxs-lookup"><span data-stu-id="ab7d7-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="ab7d7-178">RBAC jest funkcją Azure tylko portalu, nie udziela dostępu toohello klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="ab7d7-179">Przypisz wbudowanych RBAC roli tooan użytkownika zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="ab7d7-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="ab7d7-180">Do innego scenariusza w teście hello użytkownika zewnętrznego "alflanigan@gmail.com" zostanie dodany jako **Współautor·maszyny·wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![wbudowana Rola współautora maszyny wirtualnej](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="ab7d7-182">Hello jest ich normalne zachowanie dla tego użytkownika zewnętrznego z tą rolą wbudowanych jest toosee i zarządzaj nimi tylko dla maszyn wirtualnych i ich sąsiadujących ze sobą Menedżer zasobów tylko zasoby niezbędne podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="ab7d7-183">Zgodnie z projektem, te role ograniczone oferować dostęp tylko zasoby odpowiedniego tootheir utworzone w portalu Azure hello, niezależnie od tego niektóre nadal można wdrożyć w hello również klasyczny portal (na przykład: maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="ab7d7-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![Omówienie roli współautora maszyny wirtualnej w portalu azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="ab7d7-185">Udziel dostępu na poziomie subskrypcji dla użytkownika w hello sam katalogu</span><span class="sxs-lookup"><span data-stu-id="ab7d7-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="ab7d7-186">przepływ procesu Hello jest identyczne tooadding użytkownika zewnętrznego, zarówno z hello perspektywy udzielającym hello RBAC rolę administratora, a także hello użytkownika zostanie im przyznany dostęp toohello roli.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="ab7d7-187">Hello różnicą jest ten użytkownik hello zaproszenie nie będą otrzymywać żadnych zaproszeń do skorzystania z poczty e-mail jako wszystkie zakresy zasobów hello w ramach subskrypcji hello będą dostępne na pulpicie nawigacyjnym powitania po zalogowaniu się.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="ab7d7-188">Przypisz role RBAC w zakresie grupy zasobów hello</span><span class="sxs-lookup"><span data-stu-id="ab7d7-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="ab7d7-189">Przypisywanie roli RBAC **grupy zasobów** zakres ma taki sam proces przypisywania roli hello na poziomie subskrypcji hello, dla obu typów użytkownicy — zewnętrznym lub wewnętrznym (część hello tego samego katalogu).</span><span class="sxs-lookup"><span data-stu-id="ab7d7-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="ab7d7-190">Witaj użytkowników, którzy mają przypisaną rolę RBAC hello jest toosee w swoim środowisku tylko grupy zasobów hello z przypisanym dostępu z hello **grup zasobów** ikonę w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="ab7d7-191">Przypisz role RBAC w zakresie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="ab7d7-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="ab7d7-192">Przypisywanie roli RBAC w zakresie zasobów na platformie Azure mają taki sam proces przypisywania roli hello na poziomie subskrypcji hello lub na poziomie grupy zasobów hello, następujące hello sam przepływ pracy oba scenariusze.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="ab7d7-193">Ponownie hello użytkowników, którzy mają przypisaną rolę RBAC hello widzą tylko elementy hello czy przypisano dostęp do obu hello w **wszystkie zasoby** kartę lub bezpośrednio w ich pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="ab7d7-194">Istotnym elementem do RBAC zarówno w zakresie grupy zasobów lub zasobów zakresie dotyczy hello użytkowników toomake toohello się, że toosign w poprawnym katalogu.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![katalog logowania w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="ab7d7-196">Przypisz role RBAC dla grupy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab7d7-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="ab7d7-197">Wszystkie scenariusze hello przy użyciu funkcji RBAC na trzy różne zakresy hello w uprawnień hello platformy Azure, zarządzanie, wdrażanie i administrowanie różnych zasobów jako przypisany użytkownik bez hello konieczne Zarządzanie subskrypcją osobistych.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="ab7d7-198">Dla subskrypcji, grupy zasobów lub zasobów zakresu przypisano rolę RBAC hello niezależnie od tego, wszystkie zasoby hello utworzone dalej przez użytkowników hello przypisane są rozliczane w ramach subskrypcji platformy Azure z jednego hello której hello użytkownicy mają dostęp do.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="ab7d7-199">Dzięki temu hello użytkowników, którzy mają rozliczeń uprawnień administratora dla całej subskrypcji platformy Azure ma pełny przegląd zużycia hello, niezależnie od tego, kto jest zarządzanie zasobami hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="ab7d7-200">W przypadku większych organizacji role RBAC można zastosować w hello taki sam sposób dla grup usługi Azure Active Directory uwzględnieniu perspektywy hello tego użytkownika administracyjnego hello potrzebuje dostępu szczegółowego hello toogrant dla zespołów lub całego działów, indywidualnie dla każdego użytkownika, w związku z tym biorąc pod uwagę go jako bardzo czas i zarządzanie wydajne opcji.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="ab7d7-201">tooillustrate ten przykład, hello **współautora** dodano rolę tooone grup hello w dzierżawie powitalnych na poziomie subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![Dodaj rolę RBAC dla grup usługi AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="ab7d7-203">Te grupy są grupami zabezpieczeń, które są udostępniane i zarządzane tylko w ramach usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="ab7d7-204">Utwórz niestandardowe Obsługa tooopen roli RBAC żądania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab7d7-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="ab7d7-205">określone poziomy uprawnień na podstawie dostępnych zasobów hello w środowisku hello upewnij się, Hello wbudowanych RBAC role, które są dostępne w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="ab7d7-206">Jednak jeśli żadna z tych ról potrzeb użytkownika administratora hello, jest dostępny hello opcja toolimit jeszcze więcej, tworząc niestandardowe role RBAC.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="ab7d7-207">Tworzenie niestandardowych ról RBAC wymaga jednej wbudowanej roli tootake, edytować, a następnie zaimportuj go ponownie w środowisku hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="ab7d7-208">Hello pobierania i przekazywanie roli hello są zarządzane przy użyciu programu PowerShell lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="ab7d7-209">Jest ważne toounderstand hello wymagania wstępne tworzenie niestandardowej roli zabezpieczeń, które można przyznać szczegółowego dostęp na poziomie subskrypcji hello i również umożliwić hello zaproszonych użytkowników hello elastyczność otwarcia żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="ab7d7-210">Dla tej roli wbudowanych hello przykład **czytnika** co pozwala użytkownikom dostępu tooview zasobów hello wszystkich zakresów ale nie tooedit je lub utworzyć nowe został dostosowany tooallow hello użytkownika hello możliwością otwarcia żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="ab7d7-211">Witaj pierwszą akcją eksportowania hello **czytnika** roli toobe musi ukończyć w programie PowerShell został uruchomiony z podwyższonym poziomem uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Zrzut ekranu programu PowerShell dla roli czytnika RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="ab7d7-213">Następnie należy tooextract hello JSON szablonu hello roli.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-213">Then you need tooextract hello JSON template of hello role.</span></span>





![Szablon JSON dla niestandardowej roli zabezpieczeń czytnika RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="ab7d7-215">Typowa rola RBAC składa się z trzech głównych sekcji, **akcje**, **NotActions** i **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="ab7d7-216">W hello **akcji** sekcji są wyświetlane wszystkie hello dozwolonych operacji dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="ab7d7-217">Jest ważne toounderstand, każda akcja przypisany od dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="ab7d7-218">W takim przypadku służący do tworzenia hello biletów pomocy technicznej **Microsoft.Support** musi być wymieniona dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="ab7d7-219">toosee stanie toobe hello wszystkich dostawców zasobów dostępnych i zarejestrowanych w ramach subskrypcji, możesz użyć programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="ab7d7-220">Ponadto możesz sprawdzić hello wszystkich hello dostępne PowerShell polecenia cmdlet toomanage hello dostawców zasobów.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="ab7d7-221">![Zrzut ekranu programu PowerShell do zarządzania dostawcy zasobów](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="ab7d7-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="ab7d7-222">Witaj wszystkie akcje dla konkretnej roli RBAC zasobów dostawcy są wymienione w sekcji hello toorestrict **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="ab7d7-223">Ostatnio jest to konieczne, że tej roli RBAC hello zawiera jawne subskrypcji hello identyfikatorów, w którym została użyta.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="ab7d7-224">Witaj identyfikatorów subskrypcji są wyświetlane w obszarze hello **AssignableScopes**, w przeciwnym razie użytkownik nie będzie można tooimport hello roli w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="ab7d7-225">Po utworzeniu i dostosowywanie hello RBAC roli, musi on toobe importowanych hello wstecz środowiska.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="ab7d7-226">W tym przykładzie hello niestandardową nazwę dla tej roli RBAC jest "Czytnika obsługi biletów poziom dostępu" stosowanie wszystko hello tooview użytkownika w subskrypcji hello, a także tooopen żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="ab7d7-227">Witaj tylko dwa wbudowane role RBAC, umożliwiając akcji hello otwarcia żądania pomocy technicznej są **właściciela** i **współautora**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="ab7d7-228">Dla użytkownika toobe stanie tooopen żądania pomocy technicznej on musi posiadać rolę RBAC tylko w zakresie subskrypcji hello, ponieważ wszystkie żądania pomocy technicznej są tworzone na podstawie subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="ab7d7-229">Ta nowa rola niestandardowych przypisano tooan użytkownika z hello tego samego katalogu.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![Zrzut ekranu przedstawiający niestandardowej roli zabezpieczeń RBAC zaimportowana hello portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Zrzut ekranu przedstawiający przypisywanie niestandardowych toouser roli RBAC importowanych w hello tym samym katalogu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Zrzut ekranu przedstawiający uprawnienia niestandardowe importowanych roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="ab7d7-233">przykład Witaj został dalsze szczegółowe tooemphasize limitów hello tę rolę niestandardową RBAC w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab7d7-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="ab7d7-234">Można tworzyć nowe żądania pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="ab7d7-234">Can create new support requests</span></span>
* <span data-ttu-id="ab7d7-235">Nie można utworzyć nowe zakresy zasobów (na przykład: maszyny wirtualnej)</span><span class="sxs-lookup"><span data-stu-id="ab7d7-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="ab7d7-236">Nie można utworzyć nowej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="ab7d7-236">Can't create new resource groups</span></span>





![Zrzut ekranu przedstawiający niestandardową rolę RBAC tworzenia żądań obsługi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![Zrzut ekranu przedstawiający niestandardowej roli zabezpieczeń RBAC nie jest w stanie toocreate maszyny wirtualne](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![Zrzut ekranu przedstawiający niestandardowej roli zabezpieczeń RBAC nie jest w stanie toocreate RGs nowy](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="ab7d7-240">Utwórz niestandardowe Obsługa tooopen roli RBAC żądań przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ab7d7-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="ab7d7-241">Uruchomiony na komputerze Mac i bez potrzeby dostępu tooPowerShell, Azure CLI jest hello toogo sposób.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="ab7d7-242">toocreate kroki Hello niestandardowej roli zabezpieczeń są powitalne takie same, z wyjątkiem wyłącznie hello, że przy użyciu interfejsu wiersza polecenia hello roli nie można pobrać szablonu JSON, ale można je wyświetlać w hello interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="ab7d7-243">W tym przykładzie wybrano I role wbudowane hello **czytnika kopii zapasowej**.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Pokaż zrzut ekranu interfejsu wiersza polecenia rolę czytelnika kopii zapasowej](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="ab7d7-245">Edytowanie hello roli w programie Visual Studio po skopiowaniu hello ich właściwości w szablonie JSON, hello **Microsoft.Support** dostawca zasobów został dodany w hello **akcje** sekcje, tak aby mogli otworzyć tego użytkownika żądania pomocy technicznej, pozostawiając toobe czytnik hello magazynów kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="ab7d7-246">Ponownie jest identyfikator subskrypcji hello niezbędne tooadd gdy ta rola będzie używany w hello **AssignableScopes** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Zrzut ekranu interfejsu wiersza polecenia importowania niestandardowej roli zabezpieczeń RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="ab7d7-248">Nowa rola Hello jest teraz dostępna w portalu Azure hello i procesu assignation hello jest hello takie same jak w poprzednich przykładach hello.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![Azure portalu zrzut ekranu przedstawiający niestandardową rolę RBAC utworzone za pomocą interfejsu wiersza polecenia 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="ab7d7-250">Począwszy od hello 2017 najnowszej kompilacji, hello powłoki chmury Azure jest ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="ab7d7-251">Powłoka chmury Azure to tooIDE dopełnienia i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="ab7d7-252">Z tą usługą Pobierz powłoką bazujące na przeglądarce, która jest uwierzytelniane i hostowanej na platformie Azure i można go użyć zamiast interfejsu wiersza polecenia na komputerze jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="ab7d7-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Powłoka w chmurze Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
