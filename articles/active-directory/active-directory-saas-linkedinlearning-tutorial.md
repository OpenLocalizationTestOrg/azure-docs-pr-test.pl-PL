---
title: 'Samouczek: Integracji Azure Active Directory z LinkedIn Learning | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i uczenie się LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 6ad28cb3adaa63ddc3d3769a650d26ca6a7e2695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="37b8b-103">Samouczek: Integracji Azure Active Directory z LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="37b8b-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="37b8b-104">Z tego samouczka dowiesz się integrowanie LinkedIn Learning z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37b8b-104">In this tutorial, you learn how to integrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37b8b-105">Integrowanie LinkedIn Learning z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="37b8b-105">Integrating LinkedIn Learning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37b8b-106">Można kontrolować w usłudze Azure AD, który ma dostęp do uczenia LinkedIn</span><span class="sxs-lookup"><span data-stu-id="37b8b-106">You can control in Azure AD who has access to LinkedIn Learning</span></span>
- <span data-ttu-id="37b8b-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do uczenia LinkedIn (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="37b8b-107">You can enable your users to automatically get signed-on to LinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37b8b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="37b8b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37b8b-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37b8b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37b8b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="37b8b-110">Prerequisites</span></span>

<span data-ttu-id="37b8b-111">Aby skonfigurować integrację usługi Azure AD przy użyciu LinkedIn Learning, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="37b8b-111">To configure Azure AD integration with LinkedIn Learning, you need the following items:</span></span>

- <span data-ttu-id="37b8b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="37b8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37b8b-113">LinkedIn Learning jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="37b8b-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37b8b-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37b8b-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="37b8b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37b8b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="37b8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37b8b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37b8b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37b8b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="37b8b-118">Scenario description</span></span>
<span data-ttu-id="37b8b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="37b8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37b8b-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="37b8b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37b8b-121">Dodawanie LinkedIn Learning z galerii</span><span class="sxs-lookup"><span data-stu-id="37b8b-121">Adding LinkedIn Learning from the gallery</span></span>
2. <span data-ttu-id="37b8b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="37b8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-the-gallery"></a><span data-ttu-id="37b8b-123">Dodawanie LinkedIn Learning z galerii</span><span class="sxs-lookup"><span data-stu-id="37b8b-123">Adding LinkedIn Learning from the gallery</span></span>
<span data-ttu-id="37b8b-124">Aby skonfigurować integrację LinkedIn Learning z usługą Azure AD, należy dodać LinkedIn Learning z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="37b8b-124">To configure the integration of LinkedIn Learning into Azure AD, you need to add LinkedIn Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37b8b-125">**Aby dodać LinkedIn Learning z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37b8b-125">**To add LinkedIn Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37b8b-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="37b8b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="37b8b-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37b8b-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="37b8b-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="37b8b-133">W polu wyszukiwania wpisz **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-133">In the search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="37b8b-134">Z poziomu panelu wyników, kliknij przycisk **LinkedIn Learning** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="37b8b-134">From results panel, click **LinkedIn Learning** to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="37b8b-136">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="37b8b-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="37b8b-137">W tej sekcji skonfigurować i przetestować usługi Azure AD logowania jednokrotnego przy użyciu Learning LinkedIn w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37b8b-138">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w uczeniu LinkedIn jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37b8b-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Learning is to a user in Azure AD.</span></span> <span data-ttu-id="37b8b-139">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w uczeniu LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="37b8b-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Learning needs to be established.</span></span>

<span data-ttu-id="37b8b-140">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w uczeniu LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="37b8b-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="37b8b-141">Aby skonfigurować i przetestować usługi Azure AD logowania jednokrotnego przy użyciu LinkedIn Learning, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="37b8b-141">To configure and test Azure AD single sign-on with LinkedIn Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37b8b-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="37b8b-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="37b8b-143">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="37b8b-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37b8b-144">**[Tworzenie użytkownika testowego LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="37b8b-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="37b8b-145">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="37b8b-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37b8b-146">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="37b8b-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="37b8b-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="37b8b-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="37b8b-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="37b8b-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="37b8b-149">**Aby skonfigurować usługi Azure AD logowania jednokrotnego przy użyciu LinkedIn Learning, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37b8b-149">**To configure Azure AD single sign-on with LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="37b8b-150">W portalu Azure na **LinkedIn Learning** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-150">In the Azure portal, on the **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="37b8b-152">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="37b8b-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="37b8b-154">W oknie przeglądarki innej witryny sieci web logowanie do dzierżawy LinkedIn Learning jako administrator.</span><span class="sxs-lookup"><span data-stu-id="37b8b-154">In a different web browser window, sign-on to your LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="37b8b-155">W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="37b8b-156">Zaznacz również **Learning - domyślne** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="37b8b-156">Also, select **Learning - Default** from the dropdown list.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="37b8b-158">Kliknij przycisk **lub kliknij tutaj, aby załadować i skopiuj poszczególnych pól w formularzu** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**</span><span class="sxs-lookup"><span data-stu-id="37b8b-158">Click **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="37b8b-160">W portalu Azure w obszarze **domeny Learning LinkedIn i adres URL**, wykonaj następujące kroki, aby skonfigurować logowanie Jednokrotne w **inicjowane IdP** tryb</span><span class="sxs-lookup"><span data-stu-id="37b8b-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="37b8b-162">a.</span><span class="sxs-lookup"><span data-stu-id="37b8b-162">a.</span></span> <span data-ttu-id="37b8b-163">W **identyfikator** pole tekstowe, wprowadź **identyfikator jednostki** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="37b8b-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="37b8b-164">b.</span><span class="sxs-lookup"><span data-stu-id="37b8b-164">b.</span></span> <span data-ttu-id="37b8b-165">W **adres URL odpowiedzi** pole tekstowe, wprowadź **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="37b8b-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="37b8b-166">Jeśli chcesz skonfigurować logowanie Jednokrotne w **inicjowane SP**, następnie kliknij opcję Ustawienia Pokaż zaawansowane adres URL w sekcji konfiguracji i skonfigurować adres URL logowania przy użyciu następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="37b8b-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign-on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="37b8b-168">Aplikacja LinkedIn Learning oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="37b8b-168">Your LinkedIn Learning application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="37b8b-169">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="37b8b-170">Wartość domyślna **identyfikator użytkownika** jest **user.userprincipalname** , ale LinkedIn Learning oczekuje to być mapowane z adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37b8b-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="37b8b-171">W przypadku którego można użyć **user.mail** atrybutu z listy lub użyj wartości atrybutu odpowiednie na podstawie konfiguracji organizacji.</span><span class="sxs-lookup"><span data-stu-id="37b8b-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="37b8b-173">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustawić atrybutów.</span><span class="sxs-lookup"><span data-stu-id="37b8b-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="37b8b-174">Użytkownik chce dodać cztery oświadczeń o nazwie **e-mail**, **działu**, **imię**, i **nazwisko** i wartość ma być zmapowana z **user.mail**, **user.department**, **user.givenname**, i **user.surname** odpowiednio</span><span class="sxs-lookup"><span data-stu-id="37b8b-174">The user needs to add four claims named **email**, **department**, **firstname**, and **lastname** and the value is to be mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="37b8b-175">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="37b8b-175">Attribute Name</span></span> | <span data-ttu-id="37b8b-176">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="37b8b-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="37b8b-177">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="37b8b-177">email</span></span>| <span data-ttu-id="37b8b-178">User.mail</span><span class="sxs-lookup"><span data-stu-id="37b8b-178">user.mail</span></span> |    
    | <span data-ttu-id="37b8b-179">Dział</span><span class="sxs-lookup"><span data-stu-id="37b8b-179">department</span></span>| <span data-ttu-id="37b8b-180">User.Department</span><span class="sxs-lookup"><span data-stu-id="37b8b-180">user.department</span></span> |
    | <span data-ttu-id="37b8b-181">Imię</span><span class="sxs-lookup"><span data-stu-id="37b8b-181">firstname</span></span>| <span data-ttu-id="37b8b-182">User.givenName</span><span class="sxs-lookup"><span data-stu-id="37b8b-182">user.givenname</span></span> |
    | <span data-ttu-id="37b8b-183">nazwisko</span><span class="sxs-lookup"><span data-stu-id="37b8b-183">lastname</span></span>| <span data-ttu-id="37b8b-184">User.surname</span><span class="sxs-lookup"><span data-stu-id="37b8b-184">user.surname</span></span> |
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="37b8b-186">a.</span><span class="sxs-lookup"><span data-stu-id="37b8b-186">a.</span></span> <span data-ttu-id="37b8b-187">Kliknij przycisk **Dodawanie atrybutu** aby otworzyć okno dialogowe atrybutu.</span><span class="sxs-lookup"><span data-stu-id="37b8b-187">Click **Add Attribute** to open the attribute dialog.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="37b8b-190">b.</span><span class="sxs-lookup"><span data-stu-id="37b8b-190">b.</span></span> <span data-ttu-id="37b8b-191">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="37b8b-191">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="37b8b-192">c.</span><span class="sxs-lookup"><span data-stu-id="37b8b-192">c.</span></span> <span data-ttu-id="37b8b-193">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="37b8b-193">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="37b8b-194">d.</span><span class="sxs-lookup"><span data-stu-id="37b8b-194">d.</span></span> <span data-ttu-id="37b8b-195">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="37b8b-195">Click **Ok**</span></span>

10. <span data-ttu-id="37b8b-196">Wykonaj następujące czynności na **nazwa** — atrybut</span><span class="sxs-lookup"><span data-stu-id="37b8b-196">Perform the following steps on the **name** attribute-</span></span>

    <span data-ttu-id="37b8b-197">a.</span><span class="sxs-lookup"><span data-stu-id="37b8b-197">a.</span></span> <span data-ttu-id="37b8b-198">Kliknij ten atrybut można otworzyć **atrybutu Edytuj** okna.</span><span class="sxs-lookup"><span data-stu-id="37b8b-198">Click on the attribute to open the **Edit Attribute** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="37b8b-200">b.</span><span class="sxs-lookup"><span data-stu-id="37b8b-200">b.</span></span> <span data-ttu-id="37b8b-201">Usuń wartość adresu URL z **przestrzeni nazw**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-201">Delete the URL value from the **namespace**.</span></span>
    
    <span data-ttu-id="37b8b-202">c.</span><span class="sxs-lookup"><span data-stu-id="37b8b-202">c.</span></span> <span data-ttu-id="37b8b-203">Kliknij przycisk **Ok** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="37b8b-203">Click **Ok** to save the setting.</span></span>

11. <span data-ttu-id="37b8b-204">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="37b8b-204">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="37b8b-206">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-206">Click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="37b8b-208">Przejdź do **ustawienia administratora LinkedIn** sekcji.</span><span class="sxs-lookup"><span data-stu-id="37b8b-208">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="37b8b-209">Przekaż plik XML, który został pobrany z portalu Azure, klikając opcję pliku XML, Przekaż.</span><span class="sxs-lookup"><span data-stu-id="37b8b-209">Upload the XML file you downloaded from the Azure portal by clicking the Upload XML file option.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="37b8b-211">Kliknij przycisk **na** do włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-211">Click **On** to enable SSO.</span></span> <span data-ttu-id="37b8b-212">Zmiany stanu rejestracji Jednokrotnej z **niepołączone** do **połączony**</span><span class="sxs-lookup"><span data-stu-id="37b8b-212">SSO status changes from **Not Connected** to **Connected**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="37b8b-214">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="37b8b-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="37b8b-215">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="37b8b-215">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="37b8b-217">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37b8b-217">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37b8b-218">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="37b8b-218">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37b8b-220">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-220">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37b8b-222">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-222">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37b8b-224">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="37b8b-224">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37b8b-226">a.</span><span class="sxs-lookup"><span data-stu-id="37b8b-226">a.</span></span> <span data-ttu-id="37b8b-227">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-227">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37b8b-228">b.</span><span class="sxs-lookup"><span data-stu-id="37b8b-228">b.</span></span> <span data-ttu-id="37b8b-229">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37b8b-229">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37b8b-230">c.</span><span class="sxs-lookup"><span data-stu-id="37b8b-230">c.</span></span> <span data-ttu-id="37b8b-231">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-231">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37b8b-232">d.</span><span class="sxs-lookup"><span data-stu-id="37b8b-232">d.</span></span> <span data-ttu-id="37b8b-233">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="37b8b-234">Tworzenie użytkownika testowego LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="37b8b-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="37b8b-235">Obsługuje połączonych aplikacji Learning.</span><span class="sxs-lookup"><span data-stu-id="37b8b-235">Linked Learning Application supports.</span></span> <span data-ttu-id="37b8b-236">Tylko na czas Inicjowanie obsługi użytkowników, a następnie uwierzytelniania użytkowników są tworzone automatycznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37b8b-236">Just in time user provisioning and after authentication users are created in the application automatically.</span></span> <span data-ttu-id="37b8b-237">Na administrator ustawienia strony na Przerzucanie portalu LinkedIn Learning przełącznika **automatycznie przypisywać licencje** aktywna można włączyć tylko w czasie inicjowania obsługi administracyjnej i to będzie również przypisać licencję do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37b8b-237">On the admin settings page on the LinkedIn Learning portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="37b8b-239">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="37b8b-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="37b8b-240">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do uczenia LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="37b8b-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LinkedIn Learning.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="37b8b-242">**Aby przypisać Simona Britta LinkedIn Learning, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="37b8b-242">**To assign Britta Simon to LinkedIn Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="37b8b-243">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="37b8b-245">Na liście aplikacji zaznacz **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-245">In the applications list, select **LinkedIn Learning**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="37b8b-247">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="37b8b-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="37b8b-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="37b8b-249">Click **Add** button.</span></span> <span data-ttu-id="37b8b-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="37b8b-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="37b8b-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="37b8b-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37b8b-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="37b8b-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="37b8b-255">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="37b8b-255">Testing single sign-on</span></span>

<span data-ttu-id="37b8b-256">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="37b8b-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="37b8b-257">Po kliknięciu kafelka LinkedIn Learning w panelu dostępu, należy pobrać strony Azure logowania jednokrotnego i na po pomyślnym logowania, należy pobrać do aplikacji LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="37b8b-257">When you click the LinkedIn Learning tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37b8b-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="37b8b-258">Additional resources</span></span>

* [<span data-ttu-id="37b8b-259">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37b8b-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37b8b-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37b8b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png