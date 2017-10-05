---
title: 'Samouczek: Integracji Azure Active Directory z Zscaler | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 73c81691b68ee820e1d905a17b4f2ab6b6ceb5fd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="9866b-103">Samouczek: Integracji Azure Active Directory z Zscaler</span><span class="sxs-lookup"><span data-stu-id="9866b-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="9866b-104">Z tego samouczka dowiesz się integrowanie Zscaler z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9866b-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9866b-105">Integracja z usługą Azure AD Zscaler zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9866b-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9866b-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Zscaler</span><span class="sxs-lookup"><span data-stu-id="9866b-106">You can control in Azure AD who has access to Zscaler</span></span>
- <span data-ttu-id="9866b-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Zscaler (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9866b-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9866b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9866b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9866b-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9866b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9866b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9866b-110">Prerequisites</span></span>

<span data-ttu-id="9866b-111">Aby skonfigurować integrację usługi Azure AD z Zscaler, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9866b-111">To configure Azure AD integration with Zscaler, you need the following items:</span></span>

- <span data-ttu-id="9866b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9866b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9866b-113">Zscaler logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9866b-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9866b-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9866b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9866b-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9866b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9866b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9866b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9866b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9866b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9866b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9866b-118">Scenario description</span></span>
<span data-ttu-id="9866b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9866b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9866b-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9866b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9866b-121">Dodawanie Zscaler z galerii</span><span class="sxs-lookup"><span data-stu-id="9866b-121">Adding Zscaler from the gallery</span></span>
2. <span data-ttu-id="9866b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9866b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-the-gallery"></a><span data-ttu-id="9866b-123">Dodawanie Zscaler z galerii</span><span class="sxs-lookup"><span data-stu-id="9866b-123">Adding Zscaler from the gallery</span></span>
<span data-ttu-id="9866b-124">Aby skonfigurować integrację usługi Azure AD Zscaler, należy dodać Zscaler z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9866b-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9866b-125">**Aby dodać Zscaler z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9866b-125">**To add Zscaler from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9866b-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9866b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9866b-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9866b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9866b-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9866b-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9866b-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9866b-133">W polu wyszukiwania wpisz **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="9866b-133">In the search box, type **Zscaler**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="9866b-135">W panelu wyników wybierz **Zscaler**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9866b-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9866b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9866b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9866b-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zscaler w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9866b-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Zscaler jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9866b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span></span> <span data-ttu-id="9866b-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Zscaler musi się.</span><span class="sxs-lookup"><span data-stu-id="9866b-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span></span>

<span data-ttu-id="9866b-141">W Zscaler, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="9866b-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9866b-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zscaler, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9866b-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9866b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9866b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9866b-144">**[Konfigurowanie ustawień serwera proxy](#configuring-proxy-settings)**  — Aby skonfigurować ustawienia serwera proxy w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="9866b-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="9866b-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9866b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="9866b-146">**[Tworzenie użytkownika testowego Zscaler](#creating-a-zscaler-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Zscaler połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9866b-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="9866b-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9866b-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="9866b-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9866b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9866b-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9866b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9866b-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Zscaler.</span><span class="sxs-lookup"><span data-stu-id="9866b-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="9866b-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Zscaler, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9866b-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="9866b-152">W portalu Azure na **Zscaler** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9866b-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9866b-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9866b-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="9866b-156">Na **Zscaler domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9866b-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="9866b-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="9866b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9866b-159">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9866b-159">This value is not real.</span></span> <span data-ttu-id="9866b-160">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="9866b-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="9866b-161">Skontaktuj się z [zespołem pomocy technicznej klienta Zscaler](https://www.zscaler.com/company/contact) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="9866b-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

4. <span data-ttu-id="9866b-162">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9866b-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="9866b-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9866b-164">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9866b-166">Na **konfiguracji Zscaler** , kliknij przycisk **skonfigurować Zscaler** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9866b-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9866b-167">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9866b-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="9866b-169">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy ZScaler.</span><span class="sxs-lookup"><span data-stu-id="9866b-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="9866b-170">W menu u góry kliknij **administracji**.</span><span class="sxs-lookup"><span data-stu-id="9866b-170">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="9866b-171">![Administracja](./media/active-directory-saas-zscaler-tutorial/ic800206.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="9866b-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="9866b-172">W obszarze **administratorom zarządzanie & role**, kliknij przycisk **Zarządzanie użytkownikami & uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="9866b-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="9866b-173">![Zarządzaj użytkownikami & uwierzytelniania](./media/active-directory-saas-zscaler-tutorial/ic800207.png "zarządzania użytkownikami i uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="9866b-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="9866b-174">W **wybierz opcje uwierzytelniania dla Twojej organizacji** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9866b-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="9866b-175">![Uwierzytelnianie](./media/active-directory-saas-zscaler-tutorial/ic800208.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="9866b-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="9866b-176">a.</span><span class="sxs-lookup"><span data-stu-id="9866b-176">a.</span></span> <span data-ttu-id="9866b-177">Wybierz **uwierzytelnianie przy użyciu SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="9866b-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="9866b-178">b.</span><span class="sxs-lookup"><span data-stu-id="9866b-178">b.</span></span> <span data-ttu-id="9866b-179">Kliknij przycisk **skonfigurować SAML pojedynczego logowania jednokrotnego parametry**.</span><span class="sxs-lookup"><span data-stu-id="9866b-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="9866b-180">Na **skonfigurować SAML pojedynczych logowania jednokrotnego parametrów** strony okna dialogowego, wykonaj następujące czynności, a następnie kliknij **gotowe**</span><span class="sxs-lookup"><span data-stu-id="9866b-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="9866b-181">![Logowanie jednokrotne](./media/active-directory-saas-zscaler-tutorial/ic800209.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="9866b-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="9866b-182">a.</span><span class="sxs-lookup"><span data-stu-id="9866b-182">a.</span></span> <span data-ttu-id="9866b-183">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure do **adres URL portalu SAML, do którego użytkownicy są wysyłane do uwierzytelniania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="9866b-184">b.</span><span class="sxs-lookup"><span data-stu-id="9866b-184">b.</span></span> <span data-ttu-id="9866b-185">W **atrybutu zawierającego nazwę logowania** pole tekstowe, typ **NameID**.</span><span class="sxs-lookup"><span data-stu-id="9866b-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="9866b-186">c.</span><span class="sxs-lookup"><span data-stu-id="9866b-186">c.</span></span> <span data-ttu-id="9866b-187">Aby przekazać certyfikat pobrany, kliknij przycisk **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="9866b-187">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="9866b-188">d.</span><span class="sxs-lookup"><span data-stu-id="9866b-188">d.</span></span> <span data-ttu-id="9866b-189">Wybierz **Włącz SAML automatycznego inicjowania obsługi**.</span><span class="sxs-lookup"><span data-stu-id="9866b-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="9866b-190">Na **skonfigurować uwierzytelnianie użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9866b-190">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="9866b-191">![Administracja](./media/active-directory-saas-zscaler-tutorial/ic800210.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="9866b-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="9866b-192">a.</span><span class="sxs-lookup"><span data-stu-id="9866b-192">a.</span></span> <span data-ttu-id="9866b-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9866b-193">Click **Save**.</span></span>

    <span data-ttu-id="9866b-194">b.</span><span class="sxs-lookup"><span data-stu-id="9866b-194">b.</span></span> <span data-ttu-id="9866b-195">Kliknij przycisk **Aktywuj teraz**.</span><span class="sxs-lookup"><span data-stu-id="9866b-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="9866b-196">Konfigurowanie ustawień serwera proxy</span><span class="sxs-lookup"><span data-stu-id="9866b-196">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="9866b-197">Aby skonfigurować ustawienia serwera proxy w programie Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="9866b-197">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="9866b-198">Uruchom **programu Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9866b-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="9866b-199">Wybierz **Opcje internetowe** z **narzędzia** menu otwartego **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="9866b-200">![Opcje internetowe](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Opcje internetowe")</span><span class="sxs-lookup"><span data-stu-id="9866b-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="9866b-201">Kliknij przycisk **połączeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="9866b-201">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="9866b-202">![Połączenia](./media/active-directory-saas-zscaler-tutorial/ic769493.png "połączeń")</span><span class="sxs-lookup"><span data-stu-id="9866b-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="9866b-203">Kliknij przycisk **ustawienia sieci LAN** otworzyć **ustawienia sieci LAN** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-203">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="9866b-204">W sekcji serwer Proxy wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9866b-204">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="9866b-205">![Serwer proxy](./media/active-directory-saas-zscaler-tutorial/ic769494.png "serwera Proxy")</span><span class="sxs-lookup"><span data-stu-id="9866b-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="9866b-206">a.</span><span class="sxs-lookup"><span data-stu-id="9866b-206">a.</span></span> <span data-ttu-id="9866b-207">Wybierz **Użyj serwera proxy dla sieci LAN**.</span><span class="sxs-lookup"><span data-stu-id="9866b-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="9866b-208">b.</span><span class="sxs-lookup"><span data-stu-id="9866b-208">b.</span></span> <span data-ttu-id="9866b-209">W polu tekstowym adres typu **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="9866b-209">In the Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="9866b-210">c.</span><span class="sxs-lookup"><span data-stu-id="9866b-210">c.</span></span> <span data-ttu-id="9866b-211">W polu tekstowym portu, wpisz **80**.</span><span class="sxs-lookup"><span data-stu-id="9866b-211">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="9866b-212">d.</span><span class="sxs-lookup"><span data-stu-id="9866b-212">d.</span></span> <span data-ttu-id="9866b-213">Wybierz **używaj serwera proxy dla adresów lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="9866b-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="9866b-214">e.</span><span class="sxs-lookup"><span data-stu-id="9866b-214">e.</span></span> <span data-ttu-id="9866b-215">Kliknij przycisk **OK** zamknąć **ustawienia sieci lokalnej (LAN)** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="9866b-216">Kliknij przycisk **OK** zamknąć **Opcje internetowe** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-216">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="9866b-217">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9866b-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9866b-218">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9866b-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9866b-219">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9866b-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9866b-220">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9866b-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="9866b-221">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9866b-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9866b-223">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9866b-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9866b-224">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9866b-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9866b-226">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9866b-226">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9866b-228">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-228">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9866b-230">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9866b-230">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9866b-232">a.</span><span class="sxs-lookup"><span data-stu-id="9866b-232">a.</span></span> <span data-ttu-id="9866b-233">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9866b-233">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9866b-234">b.</span><span class="sxs-lookup"><span data-stu-id="9866b-234">b.</span></span> <span data-ttu-id="9866b-235">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9866b-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9866b-236">c.</span><span class="sxs-lookup"><span data-stu-id="9866b-236">c.</span></span> <span data-ttu-id="9866b-237">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9866b-237">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9866b-238">d.</span><span class="sxs-lookup"><span data-stu-id="9866b-238">d.</span></span> <span data-ttu-id="9866b-239">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9866b-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="9866b-240">Tworzenie użytkownika testowego Zscaler</span><span class="sxs-lookup"><span data-stu-id="9866b-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="9866b-241">Aby umożliwić użytkownikom usługi Azure AD zalogować się do ZScaler, muszą mieć przydzielone do ZScaler.</span><span class="sxs-lookup"><span data-stu-id="9866b-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span></span>  
<span data-ttu-id="9866b-242">W przypadku ZScaler Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="9866b-242">In the case of ZScaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="9866b-243">Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9866b-243">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="9866b-244">Zaloguj się do Twojego **Zscaler** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="9866b-244">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="9866b-245">Kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="9866b-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="9866b-246">![Administracja](./media/active-directory-saas-zscaler-tutorial/ic781035.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="9866b-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="9866b-247">Kliknij przycisk **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="9866b-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="9866b-248">![Dodaj](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="9866b-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="9866b-249">W **użytkowników** , kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9866b-249">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="9866b-250">![Dodaj](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Dodaj")</span><span class="sxs-lookup"><span data-stu-id="9866b-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="9866b-251">W sekcji Dodaj użytkownika wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9866b-251">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="9866b-252">![Dodaj użytkownika](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="9866b-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="9866b-253">a.</span><span class="sxs-lookup"><span data-stu-id="9866b-253">a.</span></span> <span data-ttu-id="9866b-254">Typu **UserID**, **Nazwa wyświetlana użytkownika**, **hasło**, **Potwierdź hasło**, a następnie wybierz **grup** i **działu** poprawnego konta usługi AAD chcesz udostępnić.</span><span class="sxs-lookup"><span data-stu-id="9866b-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="9866b-255">b.</span><span class="sxs-lookup"><span data-stu-id="9866b-255">b.</span></span> <span data-ttu-id="9866b-256">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9866b-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="9866b-257">Możesz użyć innych ZScaler użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ZScaler do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="9866b-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9866b-258">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9866b-258">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9866b-259">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Zscaler.</span><span class="sxs-lookup"><span data-stu-id="9866b-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9866b-261">**Aby przypisać Simona Britta Zscaler, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9866b-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="9866b-262">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9866b-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9866b-264">Na liście aplikacji zaznacz **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="9866b-264">In the applications list, select **Zscaler**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="9866b-266">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9866b-266">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9866b-268">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9866b-268">Click **Add** button.</span></span> <span data-ttu-id="9866b-269">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9866b-271">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9866b-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9866b-272">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9866b-273">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9866b-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9866b-274">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9866b-274">Testing single sign-on</span></span>

<span data-ttu-id="9866b-275">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9866b-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9866b-276">Po kliknięciu kafelka Zscaler w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Zscaler.</span><span class="sxs-lookup"><span data-stu-id="9866b-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span></span>
<span data-ttu-id="9866b-277">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9866b-277">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9866b-278">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9866b-278">Additional resources</span></span>

* [<span data-ttu-id="9866b-279">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9866b-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9866b-280">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9866b-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

