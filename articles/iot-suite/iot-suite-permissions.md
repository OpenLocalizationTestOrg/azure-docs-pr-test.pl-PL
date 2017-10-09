---
title: aaaAzure pakiet IoT i Azure Active Directory | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak pakiet IoT Azure używa usługi Azure Active Directory toomanage uprawnienia."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="10ca4-103">Uprawnienia w witrynie azureiotsuite.com hello</span><span class="sxs-lookup"><span data-stu-id="10ca4-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="10ca4-104">Co się stanie po zalogowaniu</span><span class="sxs-lookup"><span data-stu-id="10ca4-104">What happens when you sign in</span></span>

<span data-ttu-id="10ca4-105">Witaj pierwszym zalogowaniu się na [azureiotsuite.com][lnk-azureiotsuite], lokacji hello Określa poziomy uprawnień hello oparte na powitania aktualnie wybrane dzierżawy usługi Azure Active Directory (AAD) i Azure Subskrypcja.</span><span class="sxs-lookup"><span data-stu-id="10ca4-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="10ca4-106">Najpierw toopopulate hello listę dzierżawców widoczne dalej tooyour username, hello lokacji znajduje z platformy Azure dzierżaw usługi AAD, które należą do.</span><span class="sxs-lookup"><span data-stu-id="10ca4-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="10ca4-107">Obecnie hello witryny można uzyskać tokeny użytkownika dla jednego dzierżawcy w czasie.</span><span class="sxs-lookup"><span data-stu-id="10ca4-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="10ca4-108">W związku z tym po przełączeniu dzierżawcy przy użyciu listy rozwijanej hello w prawym górnym rogu hello lokacji hello loguje użytkownika w tokenach hello tooobtain dzierżawy toothat dla tej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="10ca4-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="10ca4-109">Następnie hello lokacji znajduje z dzierżawy wybrane subskrypcje, które zostały skojarzone z hello Azure.</span><span class="sxs-lookup"><span data-stu-id="10ca4-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="10ca4-110">Podczas tworzenia nowego rozwiązania wstępnie skonfigurowane są wyświetlane hello dostępnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="10ca4-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="10ca4-111">Na koniec hello lokacji pobiera wszystkie zasoby hello w subskrypcjach hello i grup zasobów oznakowane jako wstępnie skonfigurowanych rozwiązań i wypełnia hello Kafelki na stronie głównej hello.</span><span class="sxs-lookup"><span data-stu-id="10ca4-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="10ca4-112">Hello następujące sekcje opisują role hello, kontrolujących dostęp toohello wstępnie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="10ca4-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="10ca4-113">Role usługi AAD</span><span class="sxs-lookup"><span data-stu-id="10ca4-113">AAD roles</span></span>

<span data-ttu-id="10ca4-114">role AAD Hello kontrolować hello możliwości należy wstępnie skonfigurować rozwiązań i zarządzanie użytkownikami w wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="10ca4-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="10ca4-115">Można znaleźć więcej informacji na temat ról administratorów w usłudze AAD w [przypisywanie ról administratorów w usłudze Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="10ca4-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="10ca4-116">Witaj bieżącego artykuł skupia się na powitania **administratora globalnego** i hello **użytkownika** ról katalogu jako używane przez hello wstępnie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="10ca4-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="10ca4-117">Administrator globalny</span><span class="sxs-lookup"><span data-stu-id="10ca4-117">Global administrator</span></span>

<span data-ttu-id="10ca4-118">Może istnieć wiele Administratorzy globalni na dzierżawę usługi AAD:</span><span class="sxs-lookup"><span data-stu-id="10ca4-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="10ca4-119">Podczas tworzenia dzierżawy usługi AAD, są przez administratora globalnego hello domyślne tej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="10ca4-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="10ca4-120">administrator globalny Hello można udostępnić wstępnie skonfigurowane rozwiązanie i przypisano **Admin** roli dla aplikacji hello wewnątrz ich dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="10ca4-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="10ca4-121">Jeśli inny użytkownik w hello sam dzierżawę usługi AAD tworzy aplikację, hello domyślna rola przyznaje jest administrator globalny toohello **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="10ca4-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="10ca4-122">Administrator globalny można przypisać tooroles użytkowników dla aplikacji za pomocą hello [portalu Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="10ca4-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="10ca4-123">Użytkownik domeny</span><span class="sxs-lookup"><span data-stu-id="10ca4-123">Domain user</span></span>

<span data-ttu-id="10ca4-124">Może istnieć wiele użytkowników domeny w dzierżawie usługi AAD:</span><span class="sxs-lookup"><span data-stu-id="10ca4-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="10ca4-125">Użytkownik domeny można udostępnić wstępnie skonfigurowane rozwiązanie za pośrednictwem hello [azureiotsuite.com] [ lnk-azureiotsuite] lokacji.</span><span class="sxs-lookup"><span data-stu-id="10ca4-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="10ca4-126">Domyślnie program hello domeny użytkownik otrzymuje hello **Admin** roli w hello zainicjowano obsługę administracyjną aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10ca4-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="10ca4-127">Użytkownik domeny, można utworzyć aplikację przy użyciu skryptu build.cmd hello w hello [azure iot — zdalnego monitorowania][lnk-rm-github-repo], [azure-iot —-konserwacji predykcyjnej] [ lnk-pm-github-repo], lub [azure iot — połączony fabryka] [ lnk-cf-github-repo] repozytorium.</span><span class="sxs-lookup"><span data-stu-id="10ca4-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="10ca4-128">Jednak hello domyślnej roli przyznano jest użytkownik domeny toohello **tylko do odczytu**, ponieważ użytkownik domeny nie ma uprawnień tooassign ról.</span><span class="sxs-lookup"><span data-stu-id="10ca4-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="10ca4-129">Jeśli inny użytkownik w dzierżawie usługi AAD hello tworzy aplikację, użytkownika domeny hello jest przypisany hello **tylko do odczytu** roli domyślnie dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10ca4-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="10ca4-130">Użytkownik domeny nie można przypisać role w aplikacji; w związku z tym użytkownikiem domeny nie można dodać użytkowników lub ról użytkowników dla aplikacji, nawet jeśli ich obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="10ca4-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="10ca4-131">Gość</span><span class="sxs-lookup"><span data-stu-id="10ca4-131">Guest User</span></span>

<span data-ttu-id="10ca4-132">Może istnieć wiele gości na dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="10ca4-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="10ca4-133">Goście mają ograniczony zestaw praw w dzierżawie usługi AAD hello.</span><span class="sxs-lookup"><span data-stu-id="10ca4-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="10ca4-134">W związku z tym gości nie może obsłużyć wstępnie skonfigurowane rozwiązanie w dzierżawie usługi AAD hello.</span><span class="sxs-lookup"><span data-stu-id="10ca4-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="10ca4-135">Aby uzyskać więcej informacji dotyczących użytkowników i role w usłudze AAD zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="10ca4-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="10ca4-136">[Tworzenie użytkowników w usłudze Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="10ca4-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="10ca4-137">[Przypisywanie użytkowników tooapps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="10ca4-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="10ca4-138">Role administratorów subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="10ca4-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="10ca4-139">Role administratora platformy Azure Hello kontrolować hello możliwości toomap dzierżawę tooan AD subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10ca4-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="10ca4-140">Dowiedz się więcej o rolach administratora platformy Azure hello w artykule hello [jak tooadd lub zmień Współadministratorem Azure, Administrator usługi i konto administratora][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="10ca4-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="10ca4-141">Role aplikacji</span><span class="sxs-lookup"><span data-stu-id="10ca4-141">Application roles</span></span>

<span data-ttu-id="10ca4-142">Role aplikacji Hello kontroli dostępu toodevices w wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="10ca4-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="10ca4-143">Istnieją dwa zdefiniowanych ról i jedną rolę niejawne zdefiniowanych w aplikacji udostępnione:</span><span class="sxs-lookup"><span data-stu-id="10ca4-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="10ca4-144">**Administrator:** ma pełną kontrolę tooadd, zarządzania, usuń urządzenia i zmodyfikować ustawienia.</span><span class="sxs-lookup"><span data-stu-id="10ca4-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="10ca4-145">**Tylko do odczytu:** mogą wyświetlać urządzenia, zasad, akcje, zadania i dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="10ca4-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="10ca4-146">Można znaleźć roli tooeach w hello przypisane uprawnienia hello [RolePermissions.cs] [ lnk-resource-cs] pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="10ca4-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="10ca4-147">Zmiana aplikacji ról użytkownika</span><span class="sxs-lookup"><span data-stu-id="10ca4-147">Changing application roles for a user</span></span>

<span data-ttu-id="10ca4-148">Możesz użyć hello następujące procedury toomake użytkownika w usłudze Active Directory administrator wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="10ca4-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="10ca4-149">Musi być AAD administratora globalnego toochange role dla użytkownika:</span><span class="sxs-lookup"><span data-stu-id="10ca4-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="10ca4-150">Przejdź toohello [portalu Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="10ca4-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="10ca4-151">Wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="10ca4-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="10ca4-152">Upewnij się, że używasz hello katalog, który wybrano w azureiotsuite.com podczas przydzielania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="10ca4-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="10ca4-153">Jeśli masz wiele katalogów, skojarzonymi z Twoją subskrypcją, można przełączać się między nimi po kliknięciu nazwę swojego konta w hello prawym górnym rogu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="10ca4-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="10ca4-154">Kliknij przycisk **aplikacje dla przedsiębiorstw**, następnie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="10ca4-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="10ca4-155">Pokaż **wszystkie aplikacje** z **żadnych** stanu.</span><span class="sxs-lookup"><span data-stu-id="10ca4-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="10ca4-156">Następnie wyszukaj aplikację o nazwie wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="10ca4-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="10ca4-157">Kliknij nazwę hello aplikacji hello, która jest zgodna z nazwą wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="10ca4-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="10ca4-158">Kliknij przycisk **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="10ca4-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="10ca4-159">Wybierz użytkownika hello ma tooswitch ról.</span><span class="sxs-lookup"><span data-stu-id="10ca4-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="10ca4-160">Kliknij przycisk **przypisać** i wybierz hello roli (takich jak **Admin**) ma tooassign toohello użytkownika, kliknij znacznik wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="10ca4-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="10ca4-161">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="10ca4-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="10ca4-162">Jestem administratorem usługi, a chcę toochange hello katalogu mapowania między mojej subskrypcji i określonych dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="10ca4-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="10ca4-163">Jak wykonać to zadanie?</span><span class="sxs-lookup"><span data-stu-id="10ca4-163">How do I complete this task?</span></span>

1. <span data-ttu-id="10ca4-164">Przejdź toohello [klasycznego portalu Azure][lnk-classic-portal], kliknij przycisk **ustawienia** liście hello usług na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="10ca4-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="10ca4-165">Wybierz subskrypcję hello, którą chcesz mapowanie katalogu hello toochange na.</span><span class="sxs-lookup"><span data-stu-id="10ca4-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="10ca4-166">Kliknij przycisk **Edytuj katalog**.</span><span class="sxs-lookup"><span data-stu-id="10ca4-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="10ca4-167">Wybierz hello **katalogu** chcesz toouse w hello listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="10ca4-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="10ca4-168">Kliknij strzałkę w przód hello.</span><span class="sxs-lookup"><span data-stu-id="10ca4-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="10ca4-169">Potwierdź mapowanie katalogu hello i wpływ współadministratorów.</span><span class="sxs-lookup"><span data-stu-id="10ca4-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="10ca4-170">Jeśli przenosisz z innego katalogu, wszystkie hello współadministratorów z oryginalnym katalogu hello są usuwane.</span><span class="sxs-lookup"><span data-stu-id="10ca4-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="10ca4-171">Jestem użytkownika/członek domeny na powitania dzierżawę usługi AAD i utworzono wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="10ca4-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="10ca4-172">Jak pobrać przypisane roli dla mojej aplikacji?</span><span class="sxs-lookup"><span data-stu-id="10ca4-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="10ca4-173">Użytkownik administrator globalny na powitania AAD dzierżawy i przypisz role toousers samodzielnie, poproś toomake administratora globalnego.</span><span class="sxs-lookup"><span data-stu-id="10ca4-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="10ca4-174">Alternatywnie, poproś tooassign administratora globalnego należy bezpośrednio roli.</span><span class="sxs-lookup"><span data-stu-id="10ca4-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="10ca4-175">Jeśli chcesz dzierżawę usługi AAD hello toochange wdrożonej wstępnie skonfigurowane rozwiązanie w Zobacz hello następne pytanie.</span><span class="sxs-lookup"><span data-stu-id="10ca4-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="10ca4-176">Jak zmienić hello dzierżawę usługi AAD, który Moje zdalnego monitorowania wstępnie skonfigurowane rozwiązanie i aplikacji, które są przypisane do?</span><span class="sxs-lookup"><span data-stu-id="10ca4-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="10ca4-177">Można uruchamiać wdrożeń w chmurze z <https://github.com/Azure/azure-iot-remote-monitoring> i wdrożenie z nowo utworzonego dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="10ca4-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="10ca4-178">Ponieważ jesteś, domyślnie administratorem globalnym, podczas tworzenia dzierżawy usługi AAD, mają uprawnienia użytkowników tooadd i przypisz role użytkowników toothose.</span><span class="sxs-lookup"><span data-stu-id="10ca4-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="10ca4-179">Tworzenie katalogu usługi AAD w hello [portalu Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="10ca4-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="10ca4-180">Przejdź za<https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="10ca4-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="10ca4-181">Uruchom `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (na przykład `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="10ca4-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="10ca4-182">Po wyświetleniu monitu, ustaw hello **tenantid** toobe nowo utworzone dzierżawy zamiast poprzedniego dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="10ca4-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="10ca4-183">Chcę toochange administratorem usługi ani Współadministratorem podczas logowania się za pomocą konta organizacyjnego</span><span class="sxs-lookup"><span data-stu-id="10ca4-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="10ca4-184">Zobacz artykuł pomocy technicznej hello [zmiany administratora usługi i Współadministrator podczas logowania się przy użyciu konta organizacyjne][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="10ca4-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="10ca4-185">Dlaczego widzę ten błąd?</span><span class="sxs-lookup"><span data-stu-id="10ca4-185">Why am I seeing this error?</span></span> <span data-ttu-id="10ca4-186">"Twoje konto nie ma toocreate odpowiednie uprawnienia hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="10ca4-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="10ca4-187">Spróbuj skontaktować się z administratorem konta lub za pomocą innego konta."</span><span class="sxs-lookup"><span data-stu-id="10ca4-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="10ca4-188">Obejrzyj powitania po diagramu w celu uzyskania wskazówek:</span><span class="sxs-lookup"><span data-stu-id="10ca4-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="10ca4-189">Jeśli będziesz kontynuować toosee hello błąd po weryfikacji jesteś administratorem globalnym dzierżawcy usługi AAD hello i współadministrator subskrypcji hello, poproś administratora konta, Usuń hello użytkownika i przypisać odpowiednie uprawnienia w tej kolejności.</span><span class="sxs-lookup"><span data-stu-id="10ca4-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="10ca4-190">Najpierw dodaj hello użytkownika jako administratora globalnego, a następnie dodaj użytkownika jako administratora współpracującego na powitania subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10ca4-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="10ca4-191">Jeśli problemy będą się powtarzać, skontaktuj się z [Pomoc i obsługa techniczna][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="10ca4-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="10ca4-192">Dlaczego widzę ten błąd gdy subskrypcji platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="10ca4-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="10ca4-193">"Subskrypcji platformy Azure jest wymagane toocreate wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="10ca4-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="10ca4-194">Użytkownik może utworzyć bezpłatne konto próbne w zaledwie kilka minut."</span><span class="sxs-lookup"><span data-stu-id="10ca4-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="10ca4-195">Jeśli masz pewność, że masz subskrypcję platformy Azure, sprawdź poprawność mapowania dla Twojej subskrypcji dzierżawcy hello i upewnij się, że wybrano hello poprawne dzierżawy w listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="10ca4-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="10ca4-196">Jeśli zostały sprawdzone hello potrzeby czy dzierżawy jest prawidłowa, postępuj zgodnie hello poprzedzających diagram i sprawdzić poprawności mapowania hello subskrypcji i tego dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="10ca4-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10ca4-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10ca4-197">Next steps</span></span>
<span data-ttu-id="10ca4-198">toocontinue poznawania pakiet IoT, zobacz temat [dostosować wstępnie skonfigurowane rozwiązanie][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="10ca4-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
