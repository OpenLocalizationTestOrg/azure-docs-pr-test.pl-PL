---
title: "Samouczek: Integracji Azure Active Directory z podniesienia uprawnień LinkedIn | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i podnieść LinkedIn."
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
ms.openlocfilehash: 5336543e06d60be555722a615568b12048c2aa2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="689f0-103">Samouczek: Integracji Azure Active Directory z LinkedIn podniesienia uprawnień</span><span class="sxs-lookup"><span data-stu-id="689f0-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="689f0-104">Z tego samouczka dowiesz się integrowanie LinkedIn podniesienia uprawnień w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="689f0-104">In this tutorial, you learn how to integrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="689f0-105">Integrowanie LinkedIn podniesienia uprawnień w usłudze Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="689f0-105">Integrating LinkedIn Elevate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="689f0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do LinkedIn podniesienia uprawnień</span><span class="sxs-lookup"><span data-stu-id="689f0-106">You can control in Azure AD who has access to LinkedIn Elevate</span></span>
- <span data-ttu-id="689f0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane LinkedIn podniesienie poziomu (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="689f0-107">You can enable your users to automatically get signed-on to LinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="689f0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="689f0-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="689f0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="689f0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="689f0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="689f0-110">Prerequisites</span></span>

<span data-ttu-id="689f0-111">Aby skonfigurować integrację usługi Azure AD z LinkedIn podniesienia uprawnień, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="689f0-111">To configure Azure AD integration with LinkedIn Elevate, you need the following items:</span></span>

- <span data-ttu-id="689f0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="689f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="689f0-113">Podniesienie poziomu LinkedIn jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="689f0-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="689f0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="689f0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="689f0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="689f0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="689f0-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="689f0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="689f0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="689f0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="689f0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="689f0-118">Scenario description</span></span>
<span data-ttu-id="689f0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="689f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="689f0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="689f0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="689f0-121">Dodawanie podniesienia uprawnień LinkedIn z galerii</span><span class="sxs-lookup"><span data-stu-id="689f0-121">Adding LinkedIn Elevate from the gallery</span></span>
2. <span data-ttu-id="689f0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="689f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-the-gallery"></a><span data-ttu-id="689f0-123">Dodawanie podniesienia uprawnień LinkedIn z galerii</span><span class="sxs-lookup"><span data-stu-id="689f0-123">Adding LinkedIn Elevate from the gallery</span></span>
<span data-ttu-id="689f0-124">Aby skonfigurować integrację LinkedIn podniesienia uprawnień w usłudze Azure Active Directory, należy dodać podniesienia uprawnień LinkedIn z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="689f0-124">To configure the integration of LinkedIn Elevate into Azure AD, you need to add LinkedIn Elevate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="689f0-125">**Aby dodać podniesienia uprawnień LinkedIn z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="689f0-125">**To add LinkedIn Elevate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="689f0-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="689f0-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="689f0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="689f0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="689f0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="689f0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="689f0-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="689f0-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="689f0-133">W polu wyszukiwania wpisz **LinkedIn podniesienia uprawnień**.</span><span class="sxs-lookup"><span data-stu-id="689f0-133">In the search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="689f0-134">Z poziomu panelu wyników, kliknij przycisk **LinkedIn podniesienia uprawnień** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="689f0-134">From results panel, click **LinkedIn Elevate** to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="689f0-136">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="689f0-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="689f0-137">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LinkedIn podnoszenia uprawnień w oparciu o użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="689f0-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="689f0-138">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w LinkedIn podniesienia uprawnień do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="689f0-138">For single sign-on to work, Azure AD needs to know what the counterpart user in LinkedIn Elevate is to a user in Azure AD.</span></span> <span data-ttu-id="689f0-139">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w LinkedIn podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="689f0-139">In other words, a link relationship between an Azure AD user and the related user in LinkedIn Elevate needs to be established.</span></span>

<span data-ttu-id="689f0-140">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w LinkedIn podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="689f0-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="689f0-141">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z LinkedIn podniesienia uprawnień, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="689f0-141">To configure and test Azure AD single sign-on with LinkedIn Elevate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="689f0-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="689f0-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="689f0-143">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="689f0-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="689f0-144">**[Tworzenie użytkownika testowego podniesienia uprawnień LinkedIn](#creating-a-linkedin-elevate-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="689f0-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="689f0-145">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="689f0-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="689f0-146">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="689f0-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="689f0-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="689f0-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="689f0-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji LinkedIn podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="689f0-148">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="689f0-149">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z LinkedIn podniesienia uprawnień, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="689f0-149">**To configure Azure AD single sign-on with LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="689f0-150">W portalu zarządzania Azure na **podniesienia uprawnień LinkedIn** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="689f0-150">In the Azure Management portal, on the **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="689f0-152">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="689f0-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="689f0-154">W oknie przeglądarki innej witryny sieci web logowanie do podniesienia uprawnień LinkedIn dzierżawy z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="689f0-154">In a different web browser window, sign-on to your LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="689f0-155">W **Centrum konta**, kliknij przycisk **ustawienia globalne** w obszarze **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="689f0-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="689f0-156">Zaznacz również **podniesienie uprawnień — podniesienie poziomu testu AAD** z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="689f0-156">Also, select **Elevate - Elevate AAD Test** from the dropdown list.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="689f0-158">Polecenie **lub kliknij tutaj, aby załadować i skopiuj poszczególnych pól w formularzu** i skopiuj **identyfikator jednostki** i **adresu Url potwierdzenia konsumenta dostępu (ACS)**</span><span class="sxs-lookup"><span data-stu-id="689f0-158">Click on **OR Click Here to load and copy individual fields from the form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="689f0-160">W portalu Azure w obszarze **LinkedIn podniesienie poziomu domeny i adres URL**, wykonaj następujące kroki, aby skonfigurować logowanie Jednokrotne w **inicjowane IdP** tryb</span><span class="sxs-lookup"><span data-stu-id="689f0-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform the following steps if you want to configure SSO in **IdP Initiated** mode</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="689f0-162">a.</span><span class="sxs-lookup"><span data-stu-id="689f0-162">a.</span></span> <span data-ttu-id="689f0-163">W **identyfikator** pole tekstowe, wprowadź **identyfikator jednostki** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="689f0-163">In the **Identifier** textbox, enter the **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="689f0-164">b.</span><span class="sxs-lookup"><span data-stu-id="689f0-164">b.</span></span> <span data-ttu-id="689f0-165">W **adres URL odpowiedzi** pole tekstowe, wprowadź **potwierdzenia konsumenta dostępu (ACS) adres Url** skopiowany z portalu LinkedIn</span><span class="sxs-lookup"><span data-stu-id="689f0-165">In the **Reply URL** textbox, enter the **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="689f0-166">Jeśli chcesz skonfigurować logowanie Jednokrotne w **inicjowane SP**, kliknij opcję Ustawienia Pokaż zaawansowane adres URL w sekcji konfiguracji oraz konfigurowania logowania na adres URL jest następujący wzór:</span><span class="sxs-lookup"><span data-stu-id="689f0-166">If you want to configure SSO in **SP Initiated**, then click Show Advanced URL setting option in the configuration section and configure the sign on URL with the following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="689f0-168">Podniesienie poziomu LinkedIn aplikacji oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="689f0-168">Your LinkedIn Elevate application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="689f0-169">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="689f0-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="689f0-170">Wartość domyślna **identyfikator użytkownika** jest **user.userprincipalname** , ale oczekuje LinkedIn podniesienia uprawnień, to można mapować z adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="689f0-170">The default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="689f0-171">W przypadku którego można użyć **user.mail** atrybutu z listy lub użyj wartości atrybutu odpowiednie na podstawie konfiguracji organizacji.</span><span class="sxs-lookup"><span data-stu-id="689f0-171">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="689f0-173">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustawić atrybutów.</span><span class="sxs-lookup"><span data-stu-id="689f0-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span> <span data-ttu-id="689f0-174">Należy dodać inny oświadczeń o nazwie **działu** i wartość ta musi być zamapowany na **user.department**.</span><span class="sxs-lookup"><span data-stu-id="689f0-174">You need to add another claim named **department** and the value needs to be mapped to **user.department**.</span></span>

    | <span data-ttu-id="689f0-175">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="689f0-175">Attribute Name</span></span> | <span data-ttu-id="689f0-176">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="689f0-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="689f0-177">Dział</span><span class="sxs-lookup"><span data-stu-id="689f0-177">department</span></span>| <span data-ttu-id="689f0-178">User.Department</span><span class="sxs-lookup"><span data-stu-id="689f0-178">user.department</span></span> |

      ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="689f0-180">a.</span><span class="sxs-lookup"><span data-stu-id="689f0-180">a.</span></span> <span data-ttu-id="689f0-181">Atrybutu Dodaj, aby otworzyć stronę szczegółów atrybutu, kliknij polecenie Dodaj atrybut działu, jak pokazano poniżej-</span><span class="sxs-lookup"><span data-stu-id="689f0-181">Click on Add attribute to open the attribute details page add the department attribute as shown below-</span></span>

      ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="689f0-183">b.</span><span class="sxs-lookup"><span data-stu-id="689f0-183">b.</span></span> <span data-ttu-id="689f0-184">Polecenie **Ok** można zapisać atrybutu.</span><span class="sxs-lookup"><span data-stu-id="689f0-184">Click on **Ok** to save the attribute.</span></span>

      <span data-ttu-id="689f0-185">c.</span><span class="sxs-lookup"><span data-stu-id="689f0-185">c.</span></span> <span data-ttu-id="689f0-186">Zmień nazwę atrybutu **emailaddress** do **e-mail**.</span><span class="sxs-lookup"><span data-stu-id="689f0-186">Change the name of the attribute **emailaddress** to **email**.</span></span>


10. <span data-ttu-id="689f0-187">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="689f0-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="689f0-189">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="689f0-189">Click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="689f0-191">Przejdź do **ustawienia administratora LinkedIn** sekcji.</span><span class="sxs-lookup"><span data-stu-id="689f0-191">Go to **LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="689f0-192">Przekaż plik XML, który pobrany z portalu Azure, klikając opcję pliku XML przekazać.</span><span class="sxs-lookup"><span data-stu-id="689f0-192">Upload the XML file you just downloaded from the Azure portal by clicking on the Upload XML file option.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="689f0-194">Kliknij przycisk **na** do włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="689f0-194">Click **On** to enable SSO.</span></span> <span data-ttu-id="689f0-195">Stan rejestracji Jednokrotnej ulegnie zmianie z **niepołączone** do **połączony**</span><span class="sxs-lookup"><span data-stu-id="689f0-195">SSO status will change from **Not Connected** to **Connected**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="689f0-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="689f0-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="689f0-198">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="689f0-198">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="689f0-200">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="689f0-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="689f0-201">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="689f0-201">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="689f0-203">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="689f0-203">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="689f0-205">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="689f0-205">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="689f0-207">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="689f0-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="689f0-209">a.</span><span class="sxs-lookup"><span data-stu-id="689f0-209">a.</span></span> <span data-ttu-id="689f0-210">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="689f0-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="689f0-211">b.</span><span class="sxs-lookup"><span data-stu-id="689f0-211">b.</span></span> <span data-ttu-id="689f0-212">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="689f0-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="689f0-213">c.</span><span class="sxs-lookup"><span data-stu-id="689f0-213">c.</span></span> <span data-ttu-id="689f0-214">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="689f0-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="689f0-215">d.</span><span class="sxs-lookup"><span data-stu-id="689f0-215">d.</span></span> <span data-ttu-id="689f0-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="689f0-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="689f0-217">Tworzenie użytkownika testowego LinkedIn podniesienia uprawnień</span><span class="sxs-lookup"><span data-stu-id="689f0-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="689f0-218">Połączone podniesienia uprawnień aplikacji obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji automatycznie.</span><span class="sxs-lookup"><span data-stu-id="689f0-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="689f0-219">Na administrator ustawienia strony na Przerzucanie portalu LinkedIn podniesienia uprawnień przełącznika **automatycznie przypisywać licencje** aktywna można włączyć tylko w czasie inicjowania obsługi administracyjnej i to będzie również przypisać licencję do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="689f0-219">On the admin settings page on the LinkedIn Elevate portal flip the switch **Automatically Assign licenses** to active to enable Just in time provisioning and this will also assign a license to the user.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="689f0-221">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="689f0-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="689f0-222">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udostępnienie jej do podniesienia uprawnień LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="689f0-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to LinkedIn Elevate.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="689f0-224">**Aby przypisać Simona Britta LinkedIn podniesienia uprawnień, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="689f0-224">**To assign Britta Simon to LinkedIn Elevate, perform the following steps:**</span></span>

1. <span data-ttu-id="689f0-225">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="689f0-225">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="689f0-227">Na liście aplikacji zaznacz **LinkedIn podniesienia uprawnień**.</span><span class="sxs-lookup"><span data-stu-id="689f0-227">In the applications list, select **LinkedIn Elevate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="689f0-229">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="689f0-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="689f0-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="689f0-231">Click **Add** button.</span></span> <span data-ttu-id="689f0-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="689f0-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="689f0-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="689f0-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="689f0-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="689f0-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="689f0-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="689f0-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="689f0-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="689f0-237">Testing single sign-on</span></span>

<span data-ttu-id="689f0-238">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="689f0-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="689f0-239">Po kliknięciu kafelka LinkedIn podniesienia uprawnień w panelu dostępu, należy pobrać strony Azure logowania i na po pomyślnym logowania, należy pobrać w aplikacji, LinkedIn podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="689f0-239">When you click the LinkedIn Elevate tile in the Access Panel, you should get the Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="689f0-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="689f0-240">Additional resources</span></span>

* [<span data-ttu-id="689f0-241">Samouczek: Konfigurowanie LinkedIn podniesienia uprawnień dla użytkownika automatycznego inicjowania obsługi administracyjnej w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="689f0-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="689f0-242">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="689f0-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="689f0-243">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="689f0-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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
