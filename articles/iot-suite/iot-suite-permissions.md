---
title: Pakiet Azure IoT i Azure Active Directory | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak pakiet IoT Azure używa usługi Azure Active Directory do zarządzania uprawnieniami."
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
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="0fc5c-103">Uprawnienia w witrynie the azureiotsuite.com</span><span class="sxs-lookup"><span data-stu-id="0fc5c-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="0fc5c-104">Co się stanie po zalogowaniu</span><span class="sxs-lookup"><span data-stu-id="0fc5c-104">What happens when you sign in</span></span>

<span data-ttu-id="0fc5c-105">Przy pierwszym zalogowaniu się na [azureiotsuite.com][lnk-azureiotsuite], witryny Określa poziomy uprawnień, należy mieć na podstawie aktualnie wybranej dzierżawy usługi Azure Active Directory (AAD) i subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="0fc5c-106">Najpierw do wypełnienia listy dzierżawców widoczne obok nazwy użytkownika, lokacji znajduje na platformie Azure dzierżaw usługi AAD, które należą do.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="0fc5c-107">Obecnie witryny można uzyskać tokeny użytkownika dla jednego dzierżawcy w czasie.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="0fc5c-108">W związku z tym podczas przełączania dzierżawcy przy użyciu listy rozwijanej w prawym górnym rogu lokacji rejestruje w tej dzierżawy uzyskać tokenów dla tej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="0fc5c-109">Następnie lokacji znajduje z platformy Azure, subskrypcje, które zostały skojarzone z wybranej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="0fc5c-110">Podczas tworzenia nowego rozwiązania wstępnie skonfigurowane są wyświetlane dostępnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="0fc5c-111">Na koniec lokacji pobiera wszystkie zasoby w subskrypcji i grup zasobów oznakowane jako wstępnie skonfigurowanych rozwiązań i wypełnia Kafelki na stronie głównej.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="0fc5c-112">W poniższych sekcjach opisano role, które kontrolują dostęp do wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="0fc5c-113">Role usługi AAD</span><span class="sxs-lookup"><span data-stu-id="0fc5c-113">AAD roles</span></span>

<span data-ttu-id="0fc5c-114">Role AAD kontrolowanie możliwości rozwiązania wstępnie udostępnić i zarządzanie użytkownikami w wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="0fc5c-115">Można znaleźć więcej informacji na temat ról administratorów w usłudze AAD w [przypisywanie ról administratorów w usłudze Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="0fc5c-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="0fc5c-116">Bieżący artykuł skupia się na **administratora globalnego** i **użytkownika** ról katalogu jako używane przez wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="0fc5c-117">Administrator globalny</span><span class="sxs-lookup"><span data-stu-id="0fc5c-117">Global administrator</span></span>

<span data-ttu-id="0fc5c-118">Może istnieć wiele Administratorzy globalni na dzierżawę usługi AAD:</span><span class="sxs-lookup"><span data-stu-id="0fc5c-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="0fc5c-119">Podczas tworzenia dzierżawy usługi AAD jest domyślnie administratora globalnego tej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="0fc5c-120">Administrator globalny może udostępnić wstępnie skonfigurowane rozwiązanie i przypisano **Admin** roli dla aplikacji w ich dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="0fc5c-121">Jeśli inny użytkownik w tej samej dzierżawie usługi AAD tworzy aplikację, domyślna rola przyznane administratora globalnego jest **tylko do odczytu**.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="0fc5c-122">Administrator globalny można przypisać użytkowników do ról aplikacji za pomocą [portalu Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="0fc5c-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="0fc5c-123">Użytkownik domeny</span><span class="sxs-lookup"><span data-stu-id="0fc5c-123">Domain user</span></span>

<span data-ttu-id="0fc5c-124">Może istnieć wiele użytkowników domeny w dzierżawie usługi AAD:</span><span class="sxs-lookup"><span data-stu-id="0fc5c-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="0fc5c-125">Użytkownik domeny można udostępnić wstępnie skonfigurowane rozwiązanie za pośrednictwem [azureiotsuite.com] [ lnk-azureiotsuite] lokacji.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="0fc5c-126">Domyślnie udzielony jest użytkownik domeny **Admin** roli w aplikacji elastycznie.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="0fc5c-127">Użytkownik domeny, można utworzyć aplikację przy użyciu skryptu build.cmd w [azure iot — zdalnego monitorowania][lnk-rm-github-repo], [azure-iot —-konserwacji predykcyjnej][lnk-pm-github-repo], lub [azure iot — połączony fabryka] [ lnk-cf-github-repo] repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="0fc5c-128">Domyślna rola przyznane użytkownikowi domeny jest jednak **tylko do odczytu**, ponieważ użytkownik domeny nie ma uprawnień do przypisywania ról.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="0fc5c-129">Jeśli inny użytkownik w dzierżawie usługi AAD tworzy aplikację, są przypisane do użytkownika domeny **tylko do odczytu** roli domyślnie dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="0fc5c-130">Użytkownik domeny nie można przypisać role w aplikacji; w związku z tym użytkownikiem domeny nie można dodać użytkowników lub ról użytkowników dla aplikacji, nawet jeśli ich obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="0fc5c-131">Gość</span><span class="sxs-lookup"><span data-stu-id="0fc5c-131">Guest User</span></span>

<span data-ttu-id="0fc5c-132">Może istnieć wiele gości na dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="0fc5c-133">Goście mają ograniczony zestaw praw w dzierżawie usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="0fc5c-134">W związku z tym gości nie może obsłużyć wstępnie skonfigurowane rozwiązanie w dzierżawie usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="0fc5c-135">Aby uzyskać więcej informacji dotyczących użytkowników i role w usłudze AAD zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="0fc5c-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="0fc5c-136">[Tworzenie użytkowników w usłudze Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="0fc5c-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="0fc5c-137">[Przypisywanie użytkowników do aplikacji][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="0fc5c-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="0fc5c-138">Role administratorów subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0fc5c-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="0fc5c-139">Role administratora platformy Azure kontrolować możliwość mapowania subskrypcji platformy Azure do dzierżawy usługi AD.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="0fc5c-140">Dowiedz się więcej o rolach administratora platformy Azure w artykule [jak dodać lub zmienić administratora współpracującego Azure, Administrator usługi i konto administratora][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="0fc5c-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="0fc5c-141">Role aplikacji</span><span class="sxs-lookup"><span data-stu-id="0fc5c-141">Application roles</span></span>

<span data-ttu-id="0fc5c-142">Role aplikacji kontroli dostępu na urządzeniach w wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="0fc5c-143">Istnieją dwa zdefiniowanych ról i jedną rolę niejawne zdefiniowanych w aplikacji udostępnione:</span><span class="sxs-lookup"><span data-stu-id="0fc5c-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="0fc5c-144">**Administrator:** ma pełną kontrolę do dodawania, zarządzania, usuń urządzenia i zmodyfikować ustawienia.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="0fc5c-145">**Tylko do odczytu:** mogą wyświetlać urządzenia, zasad, akcje, zadania i dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="0fc5c-146">Można znaleźć uprawnienia przypisane do każdej roli w [RolePermissions.cs] [ lnk-resource-cs] pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="0fc5c-147">Zmiana aplikacji ról użytkownika</span><span class="sxs-lookup"><span data-stu-id="0fc5c-147">Changing application roles for a user</span></span>

<span data-ttu-id="0fc5c-148">Poniższa procedura służy do wyznaczenia użytkownika w usłudze Active Directory administratora wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="0fc5c-149">Musi być administratorem globalnym usługi AAD, aby zmienić role dla użytkownika:</span><span class="sxs-lookup"><span data-stu-id="0fc5c-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="0fc5c-150">Przejdź do witryny [Azure Portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="0fc5c-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="0fc5c-151">Wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="0fc5c-152">Upewnij się, że używasz katalogu, który wybrano w azureiotsuite.com podczas przydzielania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="0fc5c-153">Jeśli masz wiele katalogów, skojarzonymi z Twoją subskrypcją, można przełączać się między nimi po kliknięciu nazwę swojego konta w prawym górnym rogu portalu.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="0fc5c-154">Kliknij przycisk **aplikacje dla przedsiębiorstw**, następnie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="0fc5c-155">Pokaż **wszystkie aplikacje** z **żadnych** stanu.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="0fc5c-156">Następnie wyszukaj aplikację o nazwie wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="0fc5c-157">Kliknij nazwę aplikacji, która jest zgodna z nazwą wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="0fc5c-158">Kliknij przycisk **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="0fc5c-159">Wybierz użytkownika, aby przełączyć role.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="0fc5c-160">Kliknij przycisk **przypisać** i wybierz rolę (takich jak **Admin**) ma zostać przypisany do użytkownika, kliknij znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="0fc5c-161">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="0fc5c-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="0fc5c-162">Jestem administratorem usługi, a chcę zmienić katalogu mapowanie między mojej subskrypcji i określonych dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="0fc5c-163">Jak wykonać to zadanie?</span><span class="sxs-lookup"><span data-stu-id="0fc5c-163">How do I complete this task?</span></span>

1. <span data-ttu-id="0fc5c-164">Przejdź do [klasycznego portalu Azure][lnk-classic-portal], kliknij przycisk **ustawienia** na liście usług po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="0fc5c-165">Wybierz subskrypcję chcesz zmienić mapowanie katalogu.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="0fc5c-166">Kliknij przycisk **Edytuj katalog**.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="0fc5c-167">Wybierz **katalogu** chcesz użyć na liście rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="0fc5c-168">Kliknij strzałkę w przód.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="0fc5c-169">Potwierdź mapowanie katalogu i wpływ współadministratorów.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="0fc5c-170">Jeśli przenosisz z innego katalogu współadministratorów z oryginalnym katalogu zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="0fc5c-171">Jestem użytkownika/członek domeny na dzierżawę usługi AAD i utworzono wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="0fc5c-172">Jak pobrać przypisane roli dla mojej aplikacji?</span><span class="sxs-lookup"><span data-stu-id="0fc5c-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="0fc5c-173">Skontaktuj się administratorem globalnym, aby utworzyć administratora globalnego dla dzierżawcy usługi AAD i przypisz role użytkowników samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="0fc5c-174">Alternatywnie poproś administratora globalnego przypisanie roli bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="0fc5c-175">Jeśli chcesz zmienić dzierżawę usługi AAD wstępnie skonfigurowane rozwiązanie zostało wdrożone do, zobacz następne pytanie.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="0fc5c-176">Jak zmienić dzierżawę usługi AAD, który Moje zdalnego monitorowania wstępnie skonfigurowane rozwiązanie i aplikacji, które są przypisane do?</span><span class="sxs-lookup"><span data-stu-id="0fc5c-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="0fc5c-177">Można uruchamiać wdrożeń w chmurze z <https://github.com/Azure/azure-iot-remote-monitoring> i wdrożenie z nowo utworzonego dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="0fc5c-178">Ponieważ jesteś, domyślnie administratorem globalnym, podczas tworzenia dzierżawy usługi AAD, masz uprawnienia do dodawania użytkowników i przypisać role do tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="0fc5c-179">Tworzenie katalogu usługi AAD w [portalu Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="0fc5c-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="0fc5c-180">Przejdź do <https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="0fc5c-181">Uruchom `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (na przykład `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="0fc5c-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="0fc5c-182">Po wyświetleniu monitu, ustaw **tenantid** się nowo utworzone dzierżawy zamiast dzierżawy poprzedniej.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="0fc5c-183">Zmienianie administratorem usługi ani Współadministratorem podczas logowania się za pomocą konta organizacyjnego</span><span class="sxs-lookup"><span data-stu-id="0fc5c-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="0fc5c-184">Zobacz artykuł pomocy technicznej [zmiany administratora usługi i Współadministrator podczas logowania się przy użyciu konta organizacyjne][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="0fc5c-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="0fc5c-185">Dlaczego widzę ten błąd?</span><span class="sxs-lookup"><span data-stu-id="0fc5c-185">Why am I seeing this error?</span></span> <span data-ttu-id="0fc5c-186">"Twoje konto nie ma odpowiednich uprawnień do utworzenia rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="0fc5c-187">Spróbuj skontaktować się z administratorem konta lub za pomocą innego konta."</span><span class="sxs-lookup"><span data-stu-id="0fc5c-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="0fc5c-188">Szukaj na poniższym diagramie, aby uzyskać wskazówki:</span><span class="sxs-lookup"><span data-stu-id="0fc5c-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="0fc5c-189">Jeśli nadal wyświetlany błąd po weryfikacji można administratora globalnego dla dzierżawcy usługi AAD i współadministratorem subskrypcji, poproś administratora konta, Usuń użytkownika i przypisać odpowiednie uprawnienia w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="0fc5c-190">Najpierw dodaj użytkownika jako administrator globalny, a następnie dodaj użytkownika jako współadministratorem subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="0fc5c-191">Jeśli problemy będą się powtarzać, skontaktuj się z [Pomoc i obsługa techniczna][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="0fc5c-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="0fc5c-192">Dlaczego widzę ten błąd gdy subskrypcji platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="0fc5c-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="0fc5c-193">"Subskrypcji platformy Azure jest wymagane do utworzenia wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="0fc5c-194">Użytkownik może utworzyć bezpłatne konto próbne w zaledwie kilka minut."</span><span class="sxs-lookup"><span data-stu-id="0fc5c-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="0fc5c-195">Jeśli masz pewność, że masz subskrypcję platformy Azure, sprawdź poprawność mapowania dla Twojej subskrypcji dzierżawcy i upewnij się, że wybrano poprawny dzierżawy na liście rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="0fc5c-196">Jeśli zostały sprawdzone żądaną dzierżawy jest poprawna, postępuj zgodnie z wcześniejszym diagramie i sprawdzić poprawności mapowania subskrypcji i tego dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="0fc5c-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fc5c-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0fc5c-197">Next steps</span></span>
<span data-ttu-id="0fc5c-198">Aby kontynuować zapoznawanie pakiet IoT, zobacz temat [dostosować wstępnie skonfigurowane rozwiązanie][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="0fc5c-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

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
