---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem Igloo | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między oprogramowaniem Igloo i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="d7ba7-103">Samouczek: Azure Active Directory integracji z oprogramowaniem Igloo</span><span class="sxs-lookup"><span data-stu-id="d7ba7-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="d7ba7-104">Z tego samouczka dowiesz się integrowanie Igloo oprogramowania z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7ba7-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7ba7-105">Integracja oprogramowania Igloo z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d7ba7-106">Można kontrolować w usłudze Azure AD, który ma dostęp do oprogramowania Igloo</span><span class="sxs-lookup"><span data-stu-id="d7ba7-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="d7ba7-107">Umożliwia użytkownikom automatycznie pobrać zalogowane oprogramowania Igloo (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ba7-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7ba7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d7ba7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d7ba7-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7ba7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7ba7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d7ba7-110">Prerequisites</span></span>

<span data-ttu-id="d7ba7-111">Aby skonfigurować integrację usługi Azure AD z oprogramowaniem Igloo, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="d7ba7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ba7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7ba7-113">Oprogramowanie Igloo logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d7ba7-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7ba7-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7ba7-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7ba7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7ba7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7ba7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7ba7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d7ba7-118">Scenario description</span></span>
<span data-ttu-id="d7ba7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7ba7-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7ba7-121">Dodawanie oprogramowania Igloo z galerii</span><span class="sxs-lookup"><span data-stu-id="d7ba7-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="d7ba7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d7ba7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="d7ba7-123">Dodawanie oprogramowania Igloo z galerii</span><span class="sxs-lookup"><span data-stu-id="d7ba7-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="d7ba7-124">Aby skonfigurować integrację usługi Azure AD Igloo oprogramowania, należy dodać Igloo oprogramowania z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d7ba7-125">**Aby dodać Igloo oprogramowanie z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d7ba7-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d7ba7-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d7ba7-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d7ba7-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d7ba7-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d7ba7-133">W polu wyszukiwania wpisz **oprogramowania Igloo**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-133">In the search box, type **Igloo Software**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="d7ba7-135">W panelu wyników wybierz **oprogramowania Igloo**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7ba7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d7ba7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7ba7-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7ba7-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w oprogramowaniu Igloo jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="d7ba7-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w oprogramowaniu Igloo musi określone.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="d7ba7-141">W oprogramowaniu Igloo, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d7ba7-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d7ba7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d7ba7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7ba7-145">**[Tworzenie użytkownika testowego oprogramowania Igloo](#creating-an-igloo-software-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Igloo oprogramowania, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7ba7-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7ba7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7ba7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d7ba7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7ba7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w używanej aplikacji Igloo.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="d7ba7-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z oprogramowaniem Igloo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d7ba7-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="d7ba7-151">W portalu Azure na **oprogramowania Igloo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d7ba7-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="d7ba7-155">Na **Igloo oprogramowania domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="d7ba7-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-157">a.</span></span> <span data-ttu-id="d7ba7-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="d7ba7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="d7ba7-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-159">b.</span></span> <span data-ttu-id="d7ba7-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="d7ba7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="d7ba7-161">c.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-161">c.</span></span> <span data-ttu-id="d7ba7-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="d7ba7-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7ba7-163">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-163">These values are not real.</span></span> <span data-ttu-id="d7ba7-164">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d7ba7-165">Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania Igloo](https://www.igloosoftware.com/services/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="d7ba7-166">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="d7ba7-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="d7ba7-170">Na **konfiguracji oprogramowania Igloo** , kliknij przycisk **Konfigurowanie oprogramowania Igloo** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d7ba7-171">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d7ba7-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="d7ba7-173">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Igloo oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="d7ba7-174">Przejdź do **Panel sterowania**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="d7ba7-175">![Panel sterowania](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Panel sterowania")</span><span class="sxs-lookup"><span data-stu-id="d7ba7-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="d7ba7-176">W **członkostwa** , kliknij pozycję **znak ustawień**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="d7ba7-177">![Zaloguj się w ustawieniach](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Zaloguj ustawienia")</span><span class="sxs-lookup"><span data-stu-id="d7ba7-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="d7ba7-178">W sekcji Konfiguracja SAML kliknij **skonfigurować uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="d7ba7-179">![Konfiguracja SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Konfiguracja SAML")</span><span class="sxs-lookup"><span data-stu-id="d7ba7-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="d7ba7-180">W **Konfiguracja ogólna** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d7ba7-181">![Konfiguracja ogólna](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "konfiguracji ogólnej")</span><span class="sxs-lookup"><span data-stu-id="d7ba7-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="d7ba7-182">a.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-182">a.</span></span> <span data-ttu-id="d7ba7-183">W **nazwa połączenia** tekstowym, wpisz nazwę niestandardową dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="d7ba7-184">b.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-184">b.</span></span> <span data-ttu-id="d7ba7-185">W **adres URL logowania IdP** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d7ba7-186">c.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-186">c.</span></span> <span data-ttu-id="d7ba7-187">W **adresu URL wylogowania IdP** pole tekstowe, Wklej wartość **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d7ba7-188">d.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-188">d.</span></span> <span data-ttu-id="d7ba7-189">Wybierz **wylogowania odpowiedzi i żądania HTTP typu** jako **POST**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="d7ba7-190">e.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-190">e.</span></span> <span data-ttu-id="d7ba7-191">Otwórz z **base-64** zakodowanego certyfikatu w programie Notatnik pobrany z portalu Azure, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu publicznego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="d7ba7-192">W **odpowiedzi i konfiguracji uwierzytelniania**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="d7ba7-193">![Odpowiedź i konfiguracji uwierzytelniania](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "odpowiedzi i konfiguracji uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="d7ba7-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="d7ba7-194">a.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-194">a.</span></span> <span data-ttu-id="d7ba7-195">Jako **dostawcy tożsamości**, wybierz pozycję **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="d7ba7-196">b.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-196">b.</span></span> <span data-ttu-id="d7ba7-197">Jako **typ identyfikatora**, wybierz pozycję **adres E-mail**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="d7ba7-198">c.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-198">c.</span></span> <span data-ttu-id="d7ba7-199">W **atrybut poczty E-mail** pole tekstowe, typ **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="d7ba7-200">d.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-200">d.</span></span> <span data-ttu-id="d7ba7-201">W **atrybutu imię** pole tekstowe, typ **givenname**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="d7ba7-202">e.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-202">e.</span></span> <span data-ttu-id="d7ba7-203">W **ostatniego atrybutu Name** pole tekstowe, typ **nazwisko**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="d7ba7-204">Wykonaj poniższe kroki, aby zakończyć konfigurację:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="d7ba7-205">![Tworzenie użytkownika na logowania](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Tworzenie użytkownika na logowania")</span><span class="sxs-lookup"><span data-stu-id="d7ba7-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="d7ba7-206">a.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-206">a.</span></span> <span data-ttu-id="d7ba7-207">Jako **Tworzenie użytkownika na logowania**, wybierz pozycję **utworzenie nowego użytkownika w swojej witrynie, po zalogowaniu**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="d7ba7-208">b.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-208">b.</span></span> <span data-ttu-id="d7ba7-209">Jako **Zaloguj ustawienia**, wybierz pozycję **SAML użyj przycisku na ekranie "Zaloguj"**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="d7ba7-210">c.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-210">c.</span></span> <span data-ttu-id="d7ba7-211">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d7ba7-212">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="d7ba7-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d7ba7-213">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d7ba7-214">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7ba7-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7ba7-215">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ba7-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7ba7-216">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d7ba7-218">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d7ba7-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d7ba7-219">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7ba7-221">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7ba7-223">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7ba7-225">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7ba7-227">a.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-227">a.</span></span> <span data-ttu-id="d7ba7-228">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7ba7-229">b.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-229">b.</span></span> <span data-ttu-id="d7ba7-230">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7ba7-231">c.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-231">c.</span></span> <span data-ttu-id="d7ba7-232">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d7ba7-233">d.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-233">d.</span></span> <span data-ttu-id="d7ba7-234">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="d7ba7-235">Tworzenie użytkownika testowego Igloo oprogramowania</span><span class="sxs-lookup"><span data-stu-id="d7ba7-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="d7ba7-236">Nie ma elementu akcji do konfiguracji oprogramowania Igloo Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="d7ba7-237">Gdy przypisany użytkownik próbuje zalogować się do oprogramowania Igloo za pomocą panelu dostępu, oprogramowania Igloo sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="d7ba7-238">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez oprogramowanie Igloo.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d7ba7-239">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ba7-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d7ba7-240">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do oprogramowania Igloo.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d7ba7-242">**Aby przypisać Simona Britta Igloo oprogramowania, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d7ba7-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="d7ba7-243">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d7ba7-245">Na liście aplikacji zaznacz **oprogramowania Igloo**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-245">In the applications list, select **Igloo Software**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="d7ba7-247">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d7ba7-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-249">Click **Add** button.</span></span> <span data-ttu-id="d7ba7-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d7ba7-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d7ba7-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7ba7-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7ba7-255">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d7ba7-255">Testing single sign-on</span></span>

<span data-ttu-id="d7ba7-256">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d7ba7-257">Po kliknięciu kafelka oprogramowania Igloo w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji oprogramowania Igloo.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="d7ba7-258">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7ba7-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d7ba7-259">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d7ba7-259">Additional resources</span></span>

* [<span data-ttu-id="d7ba7-260">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7ba7-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7ba7-261">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d7ba7-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

