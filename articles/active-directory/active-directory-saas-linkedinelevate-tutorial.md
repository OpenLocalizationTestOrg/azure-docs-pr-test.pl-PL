---
title: "Samouczek: Integracji Azure Active Directory z podniesienia uprawnień LinkedIn | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i podnieść LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="a3737-103">Samouczek: Integracji Azure Active Directory z LinkedIn podniesienia uprawnień</span><span class="sxs-lookup"><span data-stu-id="a3737-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="a3737-104">Z tego samouczka, dowiesz się, jak toointegrate LinkedIn podnoszenia uprawnień w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3737-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3737-105">Integrowanie LinkedIn podniesienia uprawnień w usłudze Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a3737-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a3737-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLinkedIn podniesienie uprawnień</span><span class="sxs-lookup"><span data-stu-id="a3737-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="a3737-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLinkedIn podniesienie uprawnień (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3737-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a3737-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="a3737-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="a3737-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3737-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3737-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a3737-110">Prerequisites</span></span>

<span data-ttu-id="a3737-111">tooconfigure integracji usługi Azure AD z LinkedIn podniesienia uprawnień, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a3737-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="a3737-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3737-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3737-113">Podniesienie poziomu LinkedIn jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a3737-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3737-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a3737-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3737-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a3737-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3737-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a3737-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a3737-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3737-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3737-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a3737-118">Scenario description</span></span>
<span data-ttu-id="a3737-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a3737-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3737-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a3737-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3737-121">Dodawanie podniesienia uprawnień LinkedIn z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a3737-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="a3737-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a3737-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="a3737-123">Dodawanie podniesienia uprawnień LinkedIn z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a3737-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="a3737-124">tooconfigure hello integracji LinkedIn podniesienia uprawnień w usłudze Azure Active Directory, należy tooadd podniesienia uprawnień LinkedIn z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a3737-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a3737-125">**tooadd LinkedIn podniesienia uprawnień z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a3737-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3737-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a3737-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a3737-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a3737-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a3737-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a3737-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a3737-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a3737-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a3737-133">W polu wyszukiwania hello wpisz **LinkedIn podniesienia uprawnień**.</span><span class="sxs-lookup"><span data-stu-id="a3737-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="a3737-134">Z poziomu panelu wyników, kliknij przycisk **LinkedIn podniesienia uprawnień** tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a3737-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a3737-136">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a3737-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a3737-137">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LinkedIn podnoszenia uprawnień w oparciu o użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a3737-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a3737-138">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w LinkedIn podniesienia uprawnień jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3737-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="a3737-139">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w LinkedIn podniesienia uprawnień musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="a3737-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="a3737-140">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w LinkedIn podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="a3737-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="a3737-141">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z LinkedIn podniesienia uprawnień, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a3737-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a3737-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a3737-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a3737-143">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a3737-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3737-144">**[Tworzenie użytkownika testowego podniesienia uprawnień LinkedIn](#creating-a-linkedin-elevate-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a3737-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="a3737-145">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a3737-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3737-146">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="a3737-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a3737-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a3737-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a3737-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji LinkedIn podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="a3737-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="a3737-149">**tooconfigure usługi Azure AD rejestracji jednokrotnej z LinkedIn podniesienia uprawnień, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a3737-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3737-150">W portalu zarządzania Azure hello na powitania **podniesienia uprawnień LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a3737-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a3737-152">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a3737-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="a3737-154">W oknie przeglądarki innej witryny sieci web, logowania jednokrotnego tooyour LinkedIn podniesienia uprawnień dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="a3737-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="a3737-155">W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="a3737-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="a3737-156">Zaznacz również **podniesienie uprawnień — podniesienie poziomu testu AAD** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="a3737-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="a3737-158">Polecenie **lub kliknij tutaj tooload i skopiuj poszczególnych pól formularza hello** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**</span><span class="sxs-lookup"><span data-stu-id="a3737-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="a3737-160">W portalu Azure w obszarze **LinkedIn podniesienie poziomu domeny i adres URL**, wykonaj następujące kroki, jeśli chcesz, aby tooconfigure logowania jednokrotnego hello w **inicjowane IdP** tryb</span><span class="sxs-lookup"><span data-stu-id="a3737-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="a3737-162">a.</span><span class="sxs-lookup"><span data-stu-id="a3737-162">a.</span></span> <span data-ttu-id="a3737-163">W hello **identyfikator** pole tekstowe, wprowadź hello **identyfikator jednostki** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="a3737-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="a3737-164">b.</span><span class="sxs-lookup"><span data-stu-id="a3737-164">b.</span></span> <span data-ttu-id="a3737-165">W hello **adres URL odpowiedzi** pole tekstowe, wprowadź hello **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="a3737-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="a3737-166">Jeśli chcesz, aby tooconfigure logowania jednokrotnego w **inicjowane SP**, następnie kliknij opcję Ustawienia Pokaż zaawansowane adres URL w sekcji konfiguracji hello i konfigurowania rejestracji hello na adres URL hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="a3737-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="a3737-168">Podniesienie poziomu LinkedIn aplikacji oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a3737-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="a3737-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="a3737-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="a3737-170">Witaj wartość domyślną **identyfikator użytkownika** jest **user.userprincipalname** , ale LinkedIn podniesienia uprawnień oczekuje toobe, ten adres e-mail użytkownika hello zamapowana.</span><span class="sxs-lookup"><span data-stu-id="a3737-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="a3737-171">W przypadku którego można użyć **user.mail** atrybutu z listy hello lub użyj wartości atrybutu odpowiednie hello zgodnie z konfiguracją organizacji.</span><span class="sxs-lookup"><span data-stu-id="a3737-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="a3737-173">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty.</span><span class="sxs-lookup"><span data-stu-id="a3737-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="a3737-174">Należy tooadd innego oświadczeń o nazwie **działu** i wartość hello musi toobe mapowane za**user.department**.</span><span class="sxs-lookup"><span data-stu-id="a3737-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="a3737-175">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="a3737-175">Attribute Name</span></span> | <span data-ttu-id="a3737-176">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="a3737-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="a3737-177">Dział</span><span class="sxs-lookup"><span data-stu-id="a3737-177">department</span></span>| <span data-ttu-id="a3737-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="a3737-178">user.department</span></span> |

      ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="a3737-180">a.</span><span class="sxs-lookup"><span data-stu-id="a3737-180">a.</span></span> <span data-ttu-id="a3737-181">Dodaj atrybut tooopen hello atrybutu szczegóły strony, kliknij polecenie Dodaj atrybut działu hello, jak pokazano poniżej-</span><span class="sxs-lookup"><span data-stu-id="a3737-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="a3737-183">b.</span><span class="sxs-lookup"><span data-stu-id="a3737-183">b.</span></span> <span data-ttu-id="a3737-184">Polecenie **Ok** toosave hello atrybutu.</span><span class="sxs-lookup"><span data-stu-id="a3737-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="a3737-185">c.</span><span class="sxs-lookup"><span data-stu-id="a3737-185">c.</span></span> <span data-ttu-id="a3737-186">Zmień nazwę hello atrybutu hello **emailaddress** za**e-mail**.</span><span class="sxs-lookup"><span data-stu-id="a3737-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="a3737-187">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a3737-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="a3737-189">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a3737-189">Click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="a3737-191">Przejdź za**ustawienia administratora LinkedIn** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a3737-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="a3737-192">Przekaż plik XML hello pobrany z hello portalu Azure, klikając hello opcja pliku XML, Przekaż.</span><span class="sxs-lookup"><span data-stu-id="a3737-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="a3737-194">Kliknij przycisk **na** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a3737-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="a3737-195">Stan rejestracji Jednokrotnej ulegnie zmianie z **niepołączone** zbyt**połączony**</span><span class="sxs-lookup"><span data-stu-id="a3737-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a3737-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3737-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="a3737-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a3737-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a3737-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a3737-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3737-201">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a3737-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a3737-203">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a3737-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a3737-205">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a3737-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a3737-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a3737-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a3737-209">a.</span><span class="sxs-lookup"><span data-stu-id="a3737-209">a.</span></span> <span data-ttu-id="a3737-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3737-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3737-211">b.</span><span class="sxs-lookup"><span data-stu-id="a3737-211">b.</span></span> <span data-ttu-id="a3737-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a3737-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a3737-213">c.</span><span class="sxs-lookup"><span data-stu-id="a3737-213">c.</span></span> <span data-ttu-id="a3737-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a3737-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a3737-215">d.</span><span class="sxs-lookup"><span data-stu-id="a3737-215">d.</span></span> <span data-ttu-id="a3737-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a3737-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="a3737-217">Tworzenie użytkownika testowego LinkedIn podniesienia uprawnień</span><span class="sxs-lookup"><span data-stu-id="a3737-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="a3737-218">Połączone podniesienia uprawnień aplikacji obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a3737-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="a3737-219">Na stronie Ustawienia administratora hello na przełączniku portalu hello przerzucania podniesienia uprawnień LinkedIn hello **automatycznie przypisywać licencje** tooactive tooenable tylko w czasie inicjowania obsługi administracyjnej i to również przypisać licencję użytkownika toohello.</span><span class="sxs-lookup"><span data-stu-id="a3737-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a3737-221">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3737-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a3737-222">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooLinkedIn dostępu podniesienie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="a3737-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a3737-224">**tooassign tooLinkedIn Simona Britta podniesienie uprawnień, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a3737-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="a3737-225">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a3737-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a3737-227">Z listy aplikacji hello wybierz **LinkedIn podniesienia uprawnień**.</span><span class="sxs-lookup"><span data-stu-id="a3737-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="a3737-229">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a3737-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a3737-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a3737-231">Click **Add** button.</span></span> <span data-ttu-id="a3737-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a3737-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a3737-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a3737-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a3737-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a3737-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3737-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a3737-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a3737-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a3737-237">Testing single sign-on</span></span>

<span data-ttu-id="a3737-238">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a3737-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a3737-239">Po kliknięciu kafelka hello LinkedIn podniesienia uprawnień w hello Panel dostępu, należy pobrać hello Azure logowania jednokrotnego strony i na po pomyślnym logowania, należy pobrać w aplikacji, LinkedIn podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="a3737-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3737-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a3737-240">Additional resources</span></span>

* [<span data-ttu-id="a3737-241">Samouczek: Konfigurowanie LinkedIn podniesienia uprawnień dla użytkownika automatycznego inicjowania obsługi administracyjnej w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3737-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="a3737-242">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3737-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3737-243">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3737-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
