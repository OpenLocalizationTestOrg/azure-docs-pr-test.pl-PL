---
title: "aaaCreate tożsamość aplikacji usługi Azure w portalu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate nową aplikację usługi Azure Active Directory i usługi podmiotu zabezpieczeń, które mogą być używane z kontroli dostępu opartej na rolach hello w usłudze Azure Resource Manager toomanage dostępu tooresources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="de28a-103">Użyj portalu toocreate aplikacji usługi Azure Active Directory oraz nazwy głównej usługi, który ma dostęp do zasobów</span><span class="sxs-lookup"><span data-stu-id="de28a-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="de28a-104">Jeśli masz aplikację, która wymaga tooaccess lub modyfikowania zasobów, należy skonfigurować aplikację Azure Active Directory (AD) i przypisać hello wymagane uprawnienia tooit.</span><span class="sxs-lookup"><span data-stu-id="de28a-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="de28a-105">Ta metoda jest preferowana toorunning aplikacji hello z poświadczeniami użytkownika ponieważ:</span><span class="sxs-lookup"><span data-stu-id="de28a-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="de28a-106">Można przypisać uprawnienia toohello tożsamości aplikacji, które są inne niż własnych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="de28a-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="de28a-107">Zazwyczaj te uprawnienia są ograniczone tooexactly jakie aplikacji hello musi toodo.</span><span class="sxs-lookup"><span data-stu-id="de28a-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="de28a-108">Nie masz aplikacji hello toochange poświadczenia, jeśli Twoje obowiązki zmiany.</span><span class="sxs-lookup"><span data-stu-id="de28a-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="de28a-109">Uwierzytelnianie tooautomate certyfikatu można użyć podczas wykonywania skryptu instalacji nienadzorowanej.</span><span class="sxs-lookup"><span data-stu-id="de28a-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="de28a-110">W tym temacie pokazano, jak tooperform te kroki za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="de28a-111">Głównie aplikacji pojedynczej dzierżawy, gdzie aplikacja hello jest zamierzone toorun w tylko jednej z organizacji.</span><span class="sxs-lookup"><span data-stu-id="de28a-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="de28a-112">Zwykle użyć pojedynczej dzierżawy aplikacji dla aplikacji — biznesowych, które uruchamiane w danej organizacji.</span><span class="sxs-lookup"><span data-stu-id="de28a-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="de28a-113">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="de28a-113">Required permissions</span></span>
<span data-ttu-id="de28a-114">toocomplete w tym temacie, musi mieć wystarczające uprawnienia tooregister aplikację z dzierżawą usługi Azure AD i przypisać rolę tooa aplikacji hello w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de28a-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="de28a-115">Teraz upewnij się, że masz tooperform odpowiednie uprawnienia hello tych kroków.</span><span class="sxs-lookup"><span data-stu-id="de28a-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="de28a-116">Sprawdź uprawnienia usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de28a-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="de28a-117">Zaloguj się za tooyour konto platformy Azure za pośrednictwem hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de28a-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="de28a-118">Wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de28a-118">Select **Azure Active Directory**.</span></span>

     ![Wybierz usługę azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="de28a-120">W usłudze Azure Active Directory, zaznacz **ustawienia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="de28a-120">In Azure Active Directory, select **User settings**.</span></span>

     ![Wybierz ustawienia użytkownika](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="de28a-122">Sprawdź hello **rejestracji aplikacji** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="de28a-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="de28a-123">Jeśli ustawiona zbyt**tak**, użytkownicy niebędący administratorami można zarejestrować aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="de28a-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="de28a-124">To ustawienie oznacza, że każdy użytkownik w dzierżawie usługi Azure AD hello można zarejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de28a-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="de28a-125">Możesz przejść za[uprawnienia subskrypcji Azure Sprawdź](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="de28a-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![Wyświetlanie rejestracji aplikacji](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="de28a-127">Jeśli ustawienie rejestracji aplikacji hello ustawiono zbyt**nr**tylko administrator użytkownicy będą mogli zarejestrować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de28a-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="de28a-128">Należy toocheck, czy Twoje konto jest administratora dla dzierżawy usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="de28a-129">Wybierz **omówienie** i **znaleźć użytkownika** z szybkiego zadania.</span><span class="sxs-lookup"><span data-stu-id="de28a-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Znajdź użytkownika](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="de28a-131">Wyszukaj Twoje konto i wybrania go podczas go znaleźć.</span><span class="sxs-lookup"><span data-stu-id="de28a-131">Search for your account, and select it when you find it.</span></span>

     ![Wyszukaj użytkownika](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="de28a-133">Dla Twojego konta, wybierz **roli katalogu**.</span><span class="sxs-lookup"><span data-stu-id="de28a-133">For your account, select **Directory role**.</span></span> 

     ![Rola katalogu](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="de28a-135">Wyświetl roli użytkownika przypisany katalog w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de28a-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="de28a-136">Jeśli konto jest przypisaną rolę użytkownika toohello, ale hello ustawienia rejestracji aplikacji (w poprzednich krokach hello) jest ograniczona tooadmin użytkowników, poproś tooeither Twojego administratora przypisać możesz tooan rolę administratora lub tooenable użytkowników tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de28a-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![Rola widoku](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="de28a-138">Sprawdź uprawnienia subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="de28a-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="de28a-139">W Twojej subskrypcji platformy Azure, jego konto musi mieć `Microsoft.Authorization/*/Write` dostępu tooassign roli tooa aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="de28a-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="de28a-140">Ta akcja jest przyznawane za pośrednictwem hello [właściciela](../active-directory/role-based-access-built-in-roles.md#owner) roli lub [Administrator dostępu użytkowników](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) roli.</span><span class="sxs-lookup"><span data-stu-id="de28a-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="de28a-141">Jeśli Twoje konto jest przypisany toohello **współautora** roli, nie masz odpowiedniego uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="de28a-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="de28a-142">Podczas próby tooassign hello usługi tooa głównej roli, zostanie zwrócony błąd.</span><span class="sxs-lookup"><span data-stu-id="de28a-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="de28a-143">toocheck uprawnienia subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="de28a-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="de28a-144">Jeśli nie już poszukujesz konta usługi Azure AD z hello w poprzednich krokach, wybierz **usługi Azure Active Directory** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="de28a-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="de28a-145">Znajdź konto usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de28a-145">Find your Azure AD account.</span></span> <span data-ttu-id="de28a-146">Wybierz **omówienie** i **znaleźć użytkownika** z szybkiego zadania.</span><span class="sxs-lookup"><span data-stu-id="de28a-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Znajdź użytkownika](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="de28a-148">Wyszukaj Twoje konto i wybrania go podczas go znaleźć.</span><span class="sxs-lookup"><span data-stu-id="de28a-148">Search for your account, and select it when you find it.</span></span>

     ![Wyszukaj użytkownika](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="de28a-150">Wybierz **zasobów Azure**.</span><span class="sxs-lookup"><span data-stu-id="de28a-150">Select **Azure resources**.</span></span>

     ![Wybierz zasoby](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="de28a-152">Wyświetl przypisane role i określić, czy tooassign odpowiednie uprawnienia roli tooa aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="de28a-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="de28a-153">Jeśli nie, poproś tooadd administratora z subskrypcji możesz tooUser dostępu do roli administratora.</span><span class="sxs-lookup"><span data-stu-id="de28a-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="de28a-154">W hello po obrazu użytkownik hello jest toohello przypisanej roli dla dwóch subskrypcji, co oznacza, że użytkownik ma odpowiednie uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="de28a-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![Pokaż uprawnienia](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="de28a-156">Tworzenie aplikacji usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de28a-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="de28a-157">Zaloguj się za tooyour konto platformy Azure za pośrednictwem hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de28a-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="de28a-158">Wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="de28a-158">Select **Azure Active Directory**.</span></span>

     ![Wybierz usługę azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="de28a-160">Wybierz **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="de28a-160">Select **App registrations**.</span></span>   

     ![Wybierz rejestracji aplikacji](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="de28a-162">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="de28a-162">Select **Add**.</span></span>

     ![Dodaj aplikację](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="de28a-164">Podaj nazwę i adres URL dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="de28a-165">Wybierz opcję **aplikacji sieci Web / interfejs API** lub **natywnego** dla typu aplikacji hello ma toocreate.</span><span class="sxs-lookup"><span data-stu-id="de28a-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="de28a-166">Po ustawieniu wartości hello, wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="de28a-166">After setting hello values, select **Create**.</span></span>

     ![Nazwa aplikacji](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="de28a-168">Utworzono aplikację.</span><span class="sxs-lookup"><span data-stu-id="de28a-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="de28a-169">Pobierz klucz aplikacji identyfikator i uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="de28a-169">Get application ID and authentication key</span></span>
<span data-ttu-id="de28a-170">Podczas logowania programowo, potrzebny jest identyfikator hello aplikacji i klucz uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="de28a-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="de28a-171">tooget tych wartości, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="de28a-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="de28a-172">Z **rejestracji aplikacji** w usłudze Azure Active Directory, wybierz aplikację.</span><span class="sxs-lookup"><span data-stu-id="de28a-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![Wybierz aplikację](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="de28a-174">Kopiuj hello **identyfikator aplikacji** i zapisze go w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de28a-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="de28a-175">Witaj aplikacji hello [przykładowe aplikacje](#sample-applications) toothis wartość jako hello identyfikator klienta można znaleźć sekcji.</span><span class="sxs-lookup"><span data-stu-id="de28a-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![Identyfikator klienta](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="de28a-177">Wybierz toogenerate klucz uwierzytelniania **klucze**.</span><span class="sxs-lookup"><span data-stu-id="de28a-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![Wybierz klucze](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="de28a-179">Podaj opis klucza hello i czas trwania hello klucza.</span><span class="sxs-lookup"><span data-stu-id="de28a-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="de28a-180">Po zakończeniu wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="de28a-180">When done, select **Save**.</span></span>

     ![Zapisz klucz](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="de28a-182">Po zapisaniu hello klucza, jest wyświetlana wartość hello hello klucza.</span><span class="sxs-lookup"><span data-stu-id="de28a-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="de28a-183">Skopiować tę wartość, ponieważ nie ma klucza hello tooretrieve można później.</span><span class="sxs-lookup"><span data-stu-id="de28a-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="de28a-184">Podanie wartości klucza hello toolog identyfikator aplikacji hello w jako aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="de28a-185">Zapisywanie wartości klucza hello gdzie aplikacji mogą być pobierane.</span><span class="sxs-lookup"><span data-stu-id="de28a-185">Store hello key value where your application can retrieve it.</span></span>

     ![zapisano klucza](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="de28a-187">Uzyskanie Identyfikatora dzierżawy</span><span class="sxs-lookup"><span data-stu-id="de28a-187">Get tenant ID</span></span>
<span data-ttu-id="de28a-188">Podczas logowania programowo, potrzebny jest identyfikator dzierżawcy hello toopass do żądania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="de28a-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="de28a-189">Identyfikator dzierżawy hello tooget, wybierz **właściwości** dla dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de28a-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Wybierz właściwości usługi Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="de28a-191">Kopiuj hello **identyfikator katalogu**.</span><span class="sxs-lookup"><span data-stu-id="de28a-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="de28a-192">Ta wartość jest swojego identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="de28a-192">This value is your tenant ID.</span></span>

     ![Identyfikator dzierżawy](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="de28a-194">Przypisz toorole aplikacji</span><span class="sxs-lookup"><span data-stu-id="de28a-194">Assign application toorole</span></span>
<span data-ttu-id="de28a-195">tooaccess zasobów w ramach subskrypcji, należy przypisać rolę tooa aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="de28a-196">Zdecyduj, które roli reprezentuje hello odpowiednich uprawnień dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="de28a-197">Zobacz toolearn o dostępnych ról hello [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="de28a-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="de28a-198">Zakres hello można ustawić na poziomie hello hello subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="de28a-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="de28a-199">Uprawnienia są dziedziczone toolower poziomy zakresu.</span><span class="sxs-lookup"><span data-stu-id="de28a-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="de28a-200">Na przykład dodając rolę czytelnika toohello aplikacji dla grupy zasobów oznacza, że mogą odczytywać hello grupy zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="de28a-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="de28a-201">Przejdź na poziom toohello zakresu, które mają tooassign aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="de28a-202">Na przykład tooassign rola w zakresie subskrypcji hello, wybierz pozycję **subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="de28a-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="de28a-203">Zamiast tego możesz określić, grupy zasobów lub zasobu.</span><span class="sxs-lookup"><span data-stu-id="de28a-203">You could instead select a resource group or resource.</span></span>

     ![Wybierz subskrypcję](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="de28a-205">Wybierz hello określonej subskrypcji (grupę zasobów lub zasobów) tooassign hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de28a-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![Wybierz subskrypcję do przypisania](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="de28a-207">Wybierz **(IAM) kontroli dostępu**.</span><span class="sxs-lookup"><span data-stu-id="de28a-207">Select **Access Control (IAM)**.</span></span>

     ![Wybierz dostępu](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="de28a-209">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="de28a-209">Select **Add**.</span></span>

     ![Wybierz opcję Dodaj](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="de28a-211">Wybierz rolę hello mają tooassign toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de28a-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="de28a-212">Witaj poniższy obraz przedstawia hello **czytnika** roli.</span><span class="sxs-lookup"><span data-stu-id="de28a-212">hello following image shows hello **Reader** role.</span></span>

     ![Wybierz rolę](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="de28a-214">Wyszukaj aplikację i zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="de28a-214">Search for your application, and select it.</span></span>

     ![Wyszukiwanie aplikacji](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="de28a-216">Wybierz **OK** toofinish przypisywanie roli hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="de28a-217">Zostanie wyświetlona aplikacja hello na liście Użytkownicy z przypisaną rolę tooa dla tego zakresu.</span><span class="sxs-lookup"><span data-stu-id="de28a-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="de28a-218">Zaloguj się jako aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="de28a-218">Log in as hello application</span></span>

<span data-ttu-id="de28a-219">Aplikacja jest teraz skonfigurowane w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de28a-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="de28a-220">Masz identyfikator i toouse kluczy dla logowania jako aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="de28a-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="de28a-221">Aplikacja Hello jest przypisaną rolę tooa, zapewniająca pewne akcje, które może wykonywać.</span><span class="sxs-lookup"><span data-stu-id="de28a-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="de28a-222">Aby uzyskać informacje o zalogowanie się jako aplikacji hello za pomocą różnych platform zobacz:</span><span class="sxs-lookup"><span data-stu-id="de28a-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="de28a-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de28a-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="de28a-224">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="de28a-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="de28a-225">REST</span><span class="sxs-lookup"><span data-stu-id="de28a-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="de28a-226">.NET</span><span class="sxs-lookup"><span data-stu-id="de28a-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="de28a-227">Java</span><span class="sxs-lookup"><span data-stu-id="de28a-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="de28a-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="de28a-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="de28a-229">Python</span><span class="sxs-lookup"><span data-stu-id="de28a-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="de28a-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="de28a-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="de28a-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de28a-231">Next steps</span></span>
* <span data-ttu-id="de28a-232">tooset się aplikację wielu dzierżawców, zobacz [tooauthorization przewodnik dewelopera programu z interfejsu API usługi Azure Resource Manager hello](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="de28a-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="de28a-233">toolearn dotyczące określania zasad zabezpieczeń, zobacz [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="de28a-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="de28a-234">Aby uzyskać listę dostępnych akcji, które można udzielić lub odmówić toousers, zobacz [operacji dostawcy zasobów usługi Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="de28a-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
