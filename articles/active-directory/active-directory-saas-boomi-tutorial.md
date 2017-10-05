---
title: 'Samouczek: Integracji Azure Active Directory z Boomi | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 1121d22beddf73fd2109a4b410422f76dd37478e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="ae12f-103">Samouczek: Integracji Azure Active Directory z Boomi</span><span class="sxs-lookup"><span data-stu-id="ae12f-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="ae12f-104">Z tego samouczka dowiesz się integrowanie Boomi z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae12f-104">In this tutorial, you learn how to integrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae12f-105">Integracja z usługą Azure AD Boomi zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ae12f-105">Integrating Boomi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae12f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Boomi</span><span class="sxs-lookup"><span data-stu-id="ae12f-106">You can control in Azure AD who has access to Boomi</span></span>
- <span data-ttu-id="ae12f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Boomi (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae12f-107">You can enable your users to automatically get signed-on to Boomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae12f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ae12f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae12f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae12f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae12f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ae12f-110">Prerequisites</span></span>

<span data-ttu-id="ae12f-111">Aby skonfigurować integrację usługi Azure AD z Boomi, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ae12f-111">To configure Azure AD integration with Boomi, you need the following items:</span></span>

- <span data-ttu-id="ae12f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae12f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae12f-113">Boomi logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ae12f-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae12f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae12f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ae12f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae12f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ae12f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae12f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae12f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae12f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ae12f-118">Scenario description</span></span>
<span data-ttu-id="ae12f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ae12f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae12f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ae12f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae12f-121">Dodawanie Boomi z galerii</span><span class="sxs-lookup"><span data-stu-id="ae12f-121">Adding Boomi from the gallery</span></span>
2. <span data-ttu-id="ae12f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ae12f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-the-gallery"></a><span data-ttu-id="ae12f-123">Dodawanie Boomi z galerii</span><span class="sxs-lookup"><span data-stu-id="ae12f-123">Adding Boomi from the gallery</span></span>
<span data-ttu-id="ae12f-124">Aby skonfigurować integrację usługi Azure AD Boomi, należy dodać Boomi z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ae12f-124">To configure the integration of Boomi into Azure AD, you need to add Boomi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae12f-125">**Aby dodać Boomi z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ae12f-125">**To add Boomi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae12f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ae12f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ae12f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae12f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ae12f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ae12f-133">W polu wyszukiwania wpisz **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-133">In the search box, type **Boomi**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="ae12f-135">W panelu wyników wybierz **Boomi**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ae12f-135">In the results panel, select **Boomi**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae12f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ae12f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae12f-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Boomi w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae12f-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Boomi jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae12f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Boomi is to a user in Azure AD.</span></span> <span data-ttu-id="ae12f-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Boomi musi się.</span><span class="sxs-lookup"><span data-stu-id="ae12f-140">In other words, a link relationship between an Azure AD user and the related user in Boomi needs to be established.</span></span>

<span data-ttu-id="ae12f-141">W Boomi, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="ae12f-141">In Boomi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae12f-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Boomi, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ae12f-142">To configure and test Azure AD single sign-on with Boomi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae12f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ae12f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae12f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ae12f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae12f-145">**[Tworzenie użytkownika testowego Boomi](#creating-a-boomi-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Boomi połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ae12f-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - to have a counterpart of Britta Simon in Boomi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae12f-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ae12f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae12f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ae12f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae12f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ae12f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae12f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Boomi.</span><span class="sxs-lookup"><span data-stu-id="ae12f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="ae12f-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Boomi, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ae12f-150">**To configure Azure AD single sign-on with Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="ae12f-151">W portalu Azure na **Boomi** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-151">In the Azure portal, on the **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ae12f-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ae12f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="ae12f-155">Na **Boomi domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ae12f-155">On the **Boomi Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="ae12f-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae12f-157">a.</span></span> <span data-ttu-id="ae12f-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="ae12f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="ae12f-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae12f-159">b.</span></span> <span data-ttu-id="ae12f-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="ae12f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae12f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ae12f-161">These values are not real.</span></span> <span data-ttu-id="ae12f-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="ae12f-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ae12f-163">Skontaktuj się z [zespołem pomocy technicznej Boomi](https://boomi.com/company/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="ae12f-163">Contact [Boomi support team](https://boomi.com/company/contact/) to get these values.</span></span>

4. <span data-ttu-id="ae12f-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ae12f-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="ae12f-166">Aplikacja Boomi oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="ae12f-166">Boomi application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ae12f-167">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae12f-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="ae12f-168">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae12f-168">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ae12f-169">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-169">The following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="ae12f-171">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, dla każdego wiersza w tabeli poniżej, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ae12f-171">In the **User Attributes** section on the **Single sign-on** dialog, for each row shown in the table below, perform the following steps:</span></span>

    | <span data-ttu-id="ae12f-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="ae12f-172">Attribute Name</span></span> | <span data-ttu-id="ae12f-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="ae12f-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="ae12f-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="ae12f-174">FEDERATION_ID</span></span> | <span data-ttu-id="ae12f-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="ae12f-175">user.mail</span></span> |
    
    <span data-ttu-id="ae12f-176">a.</span><span class="sxs-lookup"><span data-stu-id="ae12f-176">a.</span></span> <span data-ttu-id="ae12f-177">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ae12f-180">b.</span><span class="sxs-lookup"><span data-stu-id="ae12f-180">b.</span></span> <span data-ttu-id="ae12f-181">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ae12f-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="ae12f-182">c.</span><span class="sxs-lookup"><span data-stu-id="ae12f-182">c.</span></span> <span data-ttu-id="ae12f-183">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ae12f-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="ae12f-184">d.</span><span class="sxs-lookup"><span data-stu-id="ae12f-184">d.</span></span> <span data-ttu-id="ae12f-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-185">Click **Ok**.</span></span>

6. <span data-ttu-id="ae12f-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ae12f-186">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ae12f-188">Na **konfiguracji Boomi** , kliknij przycisk **skonfigurować Boomi** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ae12f-188">On the **Boomi Configuration** section, click **Configure Boomi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ae12f-189">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ae12f-189">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="ae12f-191">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Boomi jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ae12f-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="ae12f-192">Przejdź do **nazwa firmy** i przejdź do **Konfigurowanie**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-192">Navigate to **Company Name** and go to **Set up**.</span></span>

10. <span data-ttu-id="ae12f-193">Kliknij przycisk **opcje logowania jednokrotnego** karcie i wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="ae12f-193">Click the **SSO Options** tab and perform below steps.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="ae12f-195">a.</span><span class="sxs-lookup"><span data-stu-id="ae12f-195">a.</span></span> <span data-ttu-id="ae12f-196">Sprawdź **Włącz SAML logowania jednokrotnego** wyboru.</span><span class="sxs-lookup"><span data-stu-id="ae12f-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="ae12f-197">b.</span><span class="sxs-lookup"><span data-stu-id="ae12f-197">b.</span></span> <span data-ttu-id="ae12f-198">Kliknij przycisk **importu** można przekazać certyfikatu pobrane z usługi Azure AD do **certyfikat dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-198">Click **Import** to upload the downloaded certificate from Azure AD to **Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="ae12f-199">c.</span><span class="sxs-lookup"><span data-stu-id="ae12f-199">c.</span></span> <span data-ttu-id="ae12f-200">W **adresu URL logowania do dostawcy tożsamości** pole tekstowe, umieścić wartość elementu **SAML pojedynczy znak na adres URL usługi** z okna konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae12f-200">In the **Identity Provider Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="ae12f-201">d.</span><span class="sxs-lookup"><span data-stu-id="ae12f-201">d.</span></span> <span data-ttu-id="ae12f-202">Jako **federacyjnego identyfikator lokalizacji**, wybierz pozycję **identyfikator federacyjnej jest w elemencie atrybutu FEDERATION_ID** przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="ae12f-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="ae12f-203">e.</span><span class="sxs-lookup"><span data-stu-id="ae12f-203">e.</span></span> <span data-ttu-id="ae12f-204">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ae12f-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="ae12f-205">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="ae12f-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae12f-206">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="ae12f-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae12f-207">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae12f-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae12f-208">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae12f-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae12f-209">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ae12f-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ae12f-211">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ae12f-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae12f-212">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ae12f-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae12f-214">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae12f-216">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae12f-218">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ae12f-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae12f-220">a.</span><span class="sxs-lookup"><span data-stu-id="ae12f-220">a.</span></span> <span data-ttu-id="ae12f-221">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae12f-222">b.</span><span class="sxs-lookup"><span data-stu-id="ae12f-222">b.</span></span> <span data-ttu-id="ae12f-223">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae12f-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae12f-224">c.</span><span class="sxs-lookup"><span data-stu-id="ae12f-224">c.</span></span> <span data-ttu-id="ae12f-225">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae12f-226">d.</span><span class="sxs-lookup"><span data-stu-id="ae12f-226">d.</span></span> <span data-ttu-id="ae12f-227">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="ae12f-228">Tworzenie użytkownika testowego Boomi</span><span class="sxs-lookup"><span data-stu-id="ae12f-228">Creating a Boomi test user</span></span>

<span data-ttu-id="ae12f-229">Aby umożliwić użytkownikom zalogować się do Boomi usługi Azure AD, musi być przygotowana do Boomi.</span><span class="sxs-lookup"><span data-stu-id="ae12f-229">In order to enable Azure AD users to log in to Boomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="ae12f-230">W przypadku Boomi Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ae12f-230">In the case of Boomi, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="ae12f-231">Aby udostępnić konta użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ae12f-231">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="ae12f-232">Zaloguj się do witryny firmy Boomi jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ae12f-232">Log in to your Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="ae12f-233">Po zalogowaniu, przejdź do **Zarządzanie użytkownikami** i przejdź do **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-233">After logging in, navigate to **User Management** and go to **Users**.</span></span>

    <span data-ttu-id="ae12f-234">![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="ae12f-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="ae12f-235">Kliknij przycisk  **+**  ikonę i **ról użytkownika Add/Zachowaj** zostanie otwarte okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ae12f-235">Click **+**  icon and the **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="ae12f-236">![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="ae12f-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="ae12f-237">![Użytkownicy](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="ae12f-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="ae12f-238">a.</span><span class="sxs-lookup"><span data-stu-id="ae12f-238">a.</span></span> <span data-ttu-id="ae12f-239">W **adres e-mail użytkownika** tekstowym, wpisz adres e-mail użytkownika, takich jak BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ae12f-239">In the **User e-mail address** textbox, type the email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="ae12f-240">b.</span><span class="sxs-lookup"><span data-stu-id="ae12f-240">b.</span></span> <span data-ttu-id="ae12f-241">W **imię** pole tekstowe, nazwę użytkownika, takich jak Britta typu pierwszy.</span><span class="sxs-lookup"><span data-stu-id="ae12f-241">In the **First name** textbox, type the First name of user like Britta.</span></span>

    <span data-ttu-id="ae12f-242">c.</span><span class="sxs-lookup"><span data-stu-id="ae12f-242">c.</span></span> <span data-ttu-id="ae12f-243">W **nazwisko** tekstowym, wpisz nazwisko użytkownika, takich jak Simona.</span><span class="sxs-lookup"><span data-stu-id="ae12f-243">In the **Last name** textbox, type the Last name of user like Simon.</span></span>
    
    <span data-ttu-id="ae12f-244">d.</span><span class="sxs-lookup"><span data-stu-id="ae12f-244">d.</span></span> <span data-ttu-id="ae12f-245">Wprowadź nazwę danego użytkownika **identyfikator federacyjnej**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-245">Enter the user's **Federation ID**.</span></span> <span data-ttu-id="ae12f-246">Każdy użytkownik musi mieć identyfikator federacyjnego, który unikatowo identyfikuje użytkownika w ramach konta.</span><span class="sxs-lookup"><span data-stu-id="ae12f-246">Each user must have a Federation ID that uniquely identifies the user within the account.</span></span>
    
    <span data-ttu-id="ae12f-247">e.</span><span class="sxs-lookup"><span data-stu-id="ae12f-247">e.</span></span> <span data-ttu-id="ae12f-248">Przypisz **użytkownika standardowego** rolę dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ae12f-248">Assign the **Standard User** role to the user.</span></span> <span data-ttu-id="ae12f-249">Nie należy przypisywać roli administratora, ponieważ który spowodowałoby to nadanie mu dostęp do atmosfery, a także dostępu rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ae12f-249">Do not assign the Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="ae12f-250">f.</span><span class="sxs-lookup"><span data-stu-id="ae12f-250">f.</span></span> <span data-ttu-id="ae12f-251">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ae12f-252">Użytkownik nie otrzyma wiadomość e-mail z powiadomieniem powitalnej zawierającą hasła, który może służyć do logowania się w AtomSphere konta, ponieważ jego hasło jest zarządzane przez dostawcę tożsamości.</span><span class="sxs-lookup"><span data-stu-id="ae12f-252">The user will not receive a welcome notification email containing a password that can be used to log in to the AtomSphere account because his password is managed through the identity provider.</span></span> <span data-ttu-id="ae12f-253">Możesz użyć innych Boomi użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Boomi do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="ae12f-253">You may use any other Boomi user account creation tools or APIs provided by Boomi to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae12f-254">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae12f-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae12f-255">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Boomi.</span><span class="sxs-lookup"><span data-stu-id="ae12f-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Boomi.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ae12f-257">**Aby przypisać Simona Britta Boomi, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ae12f-257">**To assign Britta Simon to Boomi, perform the following steps:**</span></span>

1. <span data-ttu-id="ae12f-258">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ae12f-260">Na liście aplikacji zaznacz **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-260">In the applications list, select **Boomi**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="ae12f-262">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ae12f-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ae12f-264">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ae12f-264">Click **Add** button.</span></span> <span data-ttu-id="ae12f-265">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ae12f-267">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="ae12f-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae12f-268">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae12f-269">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae12f-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae12f-270">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ae12f-270">Testing single sign-on</span></span>

<span data-ttu-id="ae12f-271">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ae12f-271">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae12f-272">Po kliknięciu kafelka Boomi w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Boomi.</span><span class="sxs-lookup"><span data-stu-id="ae12f-272">When you click the Boomi tile in the Access Panel, you should get automatically signed-on to your Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae12f-273">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ae12f-273">Additional resources</span></span>

* [<span data-ttu-id="ae12f-274">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae12f-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae12f-275">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae12f-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

