---
title: 'Samouczek: Integracji Azure Active Directory z Marketo | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e146fd5a8075bc9c7ba049b25e5f301fc2645ed9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="5bf65-103">Samouczek: Integracji Azure Active Directory z usługi Marketo</span><span class="sxs-lookup"><span data-stu-id="5bf65-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="5bf65-104">Z tego samouczka dowiesz się Integrowanie usługi Marketo w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bf65-104">In this tutorial, you learn how to integrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bf65-105">Integrowanie usługi Marketo w usłudze Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5bf65-105">Integrating Marketo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5bf65-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usługi Marketo</span><span class="sxs-lookup"><span data-stu-id="5bf65-106">You can control in Azure AD who has access to Marketo</span></span>
- <span data-ttu-id="5bf65-107">Umożliwia użytkownikom automatycznie pobrać podpisany w przypadku usługi Marketo (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bf65-107">You can enable your users to automatically get signed-on to Marketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bf65-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5bf65-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5bf65-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bf65-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bf65-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bf65-110">Prerequisites</span></span>

<span data-ttu-id="5bf65-111">Aby skonfigurować integrację usługi Azure AD z Marketo, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5bf65-111">To configure Azure AD integration with Marketo, you need the following items:</span></span>

- <span data-ttu-id="5bf65-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bf65-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bf65-113">Usługi Marketo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5bf65-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bf65-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bf65-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5bf65-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bf65-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5bf65-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bf65-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bf65-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bf65-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5bf65-118">Scenario description</span></span>
<span data-ttu-id="5bf65-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5bf65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bf65-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5bf65-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bf65-121">Dodawanie usługi Marketo z galerii</span><span class="sxs-lookup"><span data-stu-id="5bf65-121">Adding Marketo from the gallery</span></span>
2. <span data-ttu-id="5bf65-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bf65-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-the-gallery"></a><span data-ttu-id="5bf65-123">Dodawanie usługi Marketo z galerii</span><span class="sxs-lookup"><span data-stu-id="5bf65-123">Adding Marketo from the gallery</span></span>
<span data-ttu-id="5bf65-124">Aby skonfigurować integrację usługi Marketo w usłudze Azure Active Directory, należy dodać Marketo z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5bf65-124">To configure the integration of Marketo into Azure AD, you need to add Marketo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5bf65-125">**Aby dodać usługi Marketo z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bf65-125">**To add Marketo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5bf65-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bf65-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5bf65-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5bf65-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5bf65-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5bf65-133">W polu wyszukiwania wpisz **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-133">In the search box, type **Marketo**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="5bf65-135">W panelu wyników wybierz **Marketo**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5bf65-135">In the results panel, select **Marketo**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bf65-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bf65-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bf65-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Marketo oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5bf65-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bf65-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Marketo jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bf65-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Marketo is to a user in Azure AD.</span></span> <span data-ttu-id="5bf65-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Marketo.</span><span class="sxs-lookup"><span data-stu-id="5bf65-140">In other words, a link relationship between an Azure AD user and the related user in Marketo needs to be established.</span></span>

<span data-ttu-id="5bf65-141">W Marketo, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5bf65-141">In Marketo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5bf65-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Marketo, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5bf65-142">To configure and test Azure AD single sign-on with Marketo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5bf65-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5bf65-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5bf65-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bf65-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bf65-145">**[Tworzenie użytkownika testowego Marketo](#creating-a-marketo-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Marketo połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5bf65-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - to have a counterpart of Britta Simon in Marketo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bf65-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bf65-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bf65-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5bf65-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bf65-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bf65-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bf65-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji usługi Marketo.</span><span class="sxs-lookup"><span data-stu-id="5bf65-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="5bf65-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Marketo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bf65-150">**To configure Azure AD single sign-on with Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="5bf65-151">W portalu Azure na **Marketo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-151">In the Azure portal, on the **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5bf65-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5bf65-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="5bf65-155">Na **Marketo domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bf65-155">On the **Marketo Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="5bf65-157">a.</span><span class="sxs-lookup"><span data-stu-id="5bf65-157">a.</span></span> <span data-ttu-id="5bf65-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="5bf65-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="5bf65-159">b.</span><span class="sxs-lookup"><span data-stu-id="5bf65-159">b.</span></span> <span data-ttu-id="5bf65-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="5bf65-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5bf65-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5bf65-161">These values are not real.</span></span> <span data-ttu-id="5bf65-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5bf65-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="5bf65-163">Skontaktuj się z [zespołem pomocy technicznej usługi Marketo](http://investors.marketo.com/contactus.cfm) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="5bf65-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) to get these values.</span></span>
 
4. <span data-ttu-id="5bf65-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5bf65-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="5bf65-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bf65-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5bf65-168">Na **konfiguracji usługi Marketo** kliknij **Konfiguruj usługi Marketo** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5bf65-168">On the **Marketo Configuration** section, click **Configure Marketo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5bf65-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5bf65-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="5bf65-171">Aby uzyskać identyfikator Munchkin aplikacji, zaloguj się przy użyciu poświadczeń administratora usługi Marketo i wykonania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="5bf65-171">To get Munchkin Id of your application, log in to Marketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="5bf65-172">a.</span><span class="sxs-lookup"><span data-stu-id="5bf65-172">a.</span></span> <span data-ttu-id="5bf65-173">Zaloguj się do usługi Marketo aplikacji przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="5bf65-173">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="5bf65-174">b.</span><span class="sxs-lookup"><span data-stu-id="5bf65-174">b.</span></span> <span data-ttu-id="5bf65-175">Kliknij przycisk **Admin** przycisk w okienku nawigacji w górnym.</span><span class="sxs-lookup"><span data-stu-id="5bf65-175">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="5bf65-177">c.</span><span class="sxs-lookup"><span data-stu-id="5bf65-177">c.</span></span> <span data-ttu-id="5bf65-178">Przejdź do menu integracji i kliknij **łącze Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-178">Navigate to the Integration menu and click the **Munchkin link**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="5bf65-180">d.</span><span class="sxs-lookup"><span data-stu-id="5bf65-180">d.</span></span> <span data-ttu-id="5bf65-181">Skopiuj identyfikator Munchkin wyświetlone na ekranie i wykonaj adres URL odpowiedzi, w Kreatorze konfiguracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bf65-181">Copy the Munchkin Id shown on the screen and complete your Reply URL in the Azure AD configuration wizard.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="5bf65-183">Aby skonfigurować logowanie Jednokrotne w aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bf65-183">To configure the SSO in the application, follow the below steps:</span></span>
   
    <span data-ttu-id="5bf65-184">a.</span><span class="sxs-lookup"><span data-stu-id="5bf65-184">a.</span></span> <span data-ttu-id="5bf65-185">Zaloguj się do usługi Marketo aplikacji przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="5bf65-185">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="5bf65-186">b.</span><span class="sxs-lookup"><span data-stu-id="5bf65-186">b.</span></span> <span data-ttu-id="5bf65-187">Kliknij przycisk **Admin** przycisk w okienku nawigacji w górnym.</span><span class="sxs-lookup"><span data-stu-id="5bf65-187">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="5bf65-189">c.</span><span class="sxs-lookup"><span data-stu-id="5bf65-189">c.</span></span> <span data-ttu-id="5bf65-190">Przejdź do menu integracji i kliknij **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-190">Navigate to the Integration menu and click **Single Sign On**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="5bf65-192">d.</span><span class="sxs-lookup"><span data-stu-id="5bf65-192">d.</span></span> <span data-ttu-id="5bf65-193">Aby włączyć ustawienia SAML, kliknij przycisk **Edytuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bf65-193">To enable the SAML Settings, click **Edit** button.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="5bf65-195">e.</span><span class="sxs-lookup"><span data-stu-id="5bf65-195">e.</span></span> <span data-ttu-id="5bf65-196">**Włączone** ustawienia logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="5bf65-197">f.</span><span class="sxs-lookup"><span data-stu-id="5bf65-197">f.</span></span> <span data-ttu-id="5bf65-198">Wklej **identyfikator jednostki SAML**w **identyfikator wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-198">Paste the **SAML Entity ID**, in the **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="5bf65-199">g.</span><span class="sxs-lookup"><span data-stu-id="5bf65-199">g.</span></span> <span data-ttu-id="5bf65-200">W **identyfikator jednostki** pole tekstowe, wprowadź adres URL jako `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="5bf65-200">In the **Entity ID** textbox, enter the URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="5bf65-201">h.</span><span class="sxs-lookup"><span data-stu-id="5bf65-201">h.</span></span> <span data-ttu-id="5bf65-202">Wybierz lokalizację identyfikator użytkownika jako **element nazwa identyfikatora**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-202">Select the User ID Location as **Name Identifier element**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="5bf65-204">Jeśli Twojego identyfikatora użytkownika nie ma wartości głównej nazwy użytkownika, a następnie zmień wartość na karcie atrybutu.</span><span class="sxs-lookup"><span data-stu-id="5bf65-204">If your User Identifier is not UPN value then change the value in the Attribute tab.</span></span>
   
    <span data-ttu-id="5bf65-205">i.</span><span class="sxs-lookup"><span data-stu-id="5bf65-205">i.</span></span> <span data-ttu-id="5bf65-206">Przekaż certyfikat, który został pobrany z Kreatora konfiguracji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bf65-206">Upload the certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="5bf65-207">**Zapisz** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5bf65-207">**Save** the settings.</span></span>
   
    <span data-ttu-id="5bf65-208">j.</span><span class="sxs-lookup"><span data-stu-id="5bf65-208">j.</span></span> <span data-ttu-id="5bf65-209">Edytowanie ustawień stron przekierowania.</span><span class="sxs-lookup"><span data-stu-id="5bf65-209">Edit the Redirect Pages settings.</span></span>
   
    <span data-ttu-id="5bf65-210">k.</span><span class="sxs-lookup"><span data-stu-id="5bf65-210">k.</span></span> <span data-ttu-id="5bf65-211">Wklej **SAML pojedynczy znak na adres URL usługi** w **adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-211">Paste the **SAML Single Sign-On Service URL** in the **Login URL** textbox.</span></span>
   
    <span data-ttu-id="5bf65-212">l.</span><span class="sxs-lookup"><span data-stu-id="5bf65-212">l.</span></span> <span data-ttu-id="5bf65-213">Wklej **Sign-Out URL** w **adresu URL wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-213">Paste the **Sign-Out URL** in the **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="5bf65-214">m.</span><span class="sxs-lookup"><span data-stu-id="5bf65-214">m.</span></span> <span data-ttu-id="5bf65-215">W **adres URL błędu**, kopia programu **adresu URL wystąpienia usługi Marketo** i kliknij przycisk **zapisać** przycisk, aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5bf65-215">In the **Error URL**, copy your **Marketo instance URL** and click **Save** button to save settings.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="5bf65-217">Aby włączyć logowanie Jednokrotne dla użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bf65-217">To enable the SSO for users, complete the following actions:</span></span>
   
    <span data-ttu-id="5bf65-218">a.</span><span class="sxs-lookup"><span data-stu-id="5bf65-218">a.</span></span> <span data-ttu-id="5bf65-219">Zaloguj się do usługi Marketo aplikacji przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="5bf65-219">Log in to Marketo app using admin credentials.</span></span>
   
    <span data-ttu-id="5bf65-220">b.</span><span class="sxs-lookup"><span data-stu-id="5bf65-220">b.</span></span> <span data-ttu-id="5bf65-221">Kliknij przycisk **Admin** przycisk w okienku nawigacji w górnym.</span><span class="sxs-lookup"><span data-stu-id="5bf65-221">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="5bf65-223">c.</span><span class="sxs-lookup"><span data-stu-id="5bf65-223">c.</span></span> <span data-ttu-id="5bf65-224">Przejdź do **zabezpieczeń** menu i kliknij przycisk **ustawienia logowania**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-224">Navigate to the **Security** menu and click **Login Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="5bf65-226">d.</span><span class="sxs-lookup"><span data-stu-id="5bf65-226">d.</span></span> <span data-ttu-id="5bf65-227">Sprawdź **wymagają rejestracji Jednokrotnej** opcji i **zapisać** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5bf65-227">Check the **Require SSO** option and **Save** the settings.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="5bf65-229">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5bf65-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5bf65-230">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5bf65-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5bf65-231">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bf65-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bf65-232">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bf65-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bf65-233">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bf65-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5bf65-235">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bf65-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5bf65-236">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bf65-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bf65-238">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bf65-240">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bf65-242">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bf65-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bf65-244">a.</span><span class="sxs-lookup"><span data-stu-id="5bf65-244">a.</span></span> <span data-ttu-id="5bf65-245">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bf65-246">b.</span><span class="sxs-lookup"><span data-stu-id="5bf65-246">b.</span></span> <span data-ttu-id="5bf65-247">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5bf65-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bf65-248">c.</span><span class="sxs-lookup"><span data-stu-id="5bf65-248">c.</span></span> <span data-ttu-id="5bf65-249">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5bf65-250">d.</span><span class="sxs-lookup"><span data-stu-id="5bf65-250">d.</span></span> <span data-ttu-id="5bf65-251">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="5bf65-252">Tworzenie użytkownika testowego usługi Marketo</span><span class="sxs-lookup"><span data-stu-id="5bf65-252">Creating a Marketo test user</span></span>

<span data-ttu-id="5bf65-253">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Marketo.</span><span class="sxs-lookup"><span data-stu-id="5bf65-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="5bf65-254">wykonaj następujące kroki, aby utworzyć użytkownika usługi Marketo platformy.</span><span class="sxs-lookup"><span data-stu-id="5bf65-254">follow these steps to create a user in Marketo platform.</span></span>

1. <span data-ttu-id="5bf65-255">Zaloguj się do usługi Marketo aplikacji przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="5bf65-255">Log in to Marketo app using admin credentials.</span></span>

2. <span data-ttu-id="5bf65-256">Kliknij przycisk **Admin** przycisk w okienku nawigacji w górnym.</span><span class="sxs-lookup"><span data-stu-id="5bf65-256">Click the **Admin** button on the top navigation pane.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="5bf65-258">Przejdź do **zabezpieczeń** menu i kliknij przycisk **użytkownicy i role**</span><span class="sxs-lookup"><span data-stu-id="5bf65-258">Navigate to the **Security** menu and click **Users & Roles**</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="5bf65-260">Kliknij przycisk **zaprosić nowego użytkownika** link na karcie Użytkownicy</span><span class="sxs-lookup"><span data-stu-id="5bf65-260">Click the **Invite New User** link on the Users tab</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="5bf65-262">W Kreatorze nowego użytkownika z zaproszeniem wypełnij następujące informacje</span><span class="sxs-lookup"><span data-stu-id="5bf65-262">In the Invite New User wizard fill the following information</span></span>
   
    <span data-ttu-id="5bf65-263">a.</span><span class="sxs-lookup"><span data-stu-id="5bf65-263">a.</span></span> <span data-ttu-id="5bf65-264">Wprowadź nazwę danego użytkownika **E-mail** adres w polu tekstowym</span><span class="sxs-lookup"><span data-stu-id="5bf65-264">Enter the user **Email** address in the textbox</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="5bf65-266">b.</span><span class="sxs-lookup"><span data-stu-id="5bf65-266">b.</span></span> <span data-ttu-id="5bf65-267">Wprowadź **imię** w polu tekstowym</span><span class="sxs-lookup"><span data-stu-id="5bf65-267">Enter the **First Name** in the textbox</span></span>
   
    <span data-ttu-id="5bf65-268">c.</span><span class="sxs-lookup"><span data-stu-id="5bf65-268">c.</span></span> <span data-ttu-id="5bf65-269">Wprowadź **nazwisko** w polu tekstowym</span><span class="sxs-lookup"><span data-stu-id="5bf65-269">Enter the **Last Name**  in the textbox</span></span>
   
    <span data-ttu-id="5bf65-270">d.</span><span class="sxs-lookup"><span data-stu-id="5bf65-270">d.</span></span> <span data-ttu-id="5bf65-271">Kliknij przycisk **Dalej**</span><span class="sxs-lookup"><span data-stu-id="5bf65-271">Click **Next**</span></span>

6. <span data-ttu-id="5bf65-272">W **uprawnienia** wybierz opcję **roli użytkownika** i kliknij przycisk **dalej**</span><span class="sxs-lookup"><span data-stu-id="5bf65-272">In the **Permissions** tab, select the **userRoles** and click **Next**</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="5bf65-274">Kliknij przycisk **wysyłania** przycisk, aby wysłać zaproszenie użytkownika</span><span class="sxs-lookup"><span data-stu-id="5bf65-274">Click the **Send** button to send the user invitation</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="5bf65-276">Użytkownik otrzymuje powiadomienie e-mail i kliknij łącze i Zmień hasło, aby aktywować konto.</span><span class="sxs-lookup"><span data-stu-id="5bf65-276">User receives the email notification and has to click the link and change the password to activate the account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5bf65-277">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bf65-277">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5bf65-278">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do usługi Marketo.</span><span class="sxs-lookup"><span data-stu-id="5bf65-278">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Marketo.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5bf65-280">**Aby przypisać Simona Britta Marketo, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bf65-280">**To assign Britta Simon to Marketo, perform the following steps:**</span></span>

1. <span data-ttu-id="5bf65-281">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-281">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5bf65-283">Na liście aplikacji zaznacz **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-283">In the applications list, select **Marketo**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="5bf65-285">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-285">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5bf65-287">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bf65-287">Click **Add** button.</span></span> <span data-ttu-id="5bf65-288">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5bf65-290">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5bf65-290">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5bf65-291">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bf65-292">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bf65-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bf65-293">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bf65-293">Testing single sign-on</span></span>

<span data-ttu-id="5bf65-294">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5bf65-294">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5bf65-295">Po kliknięciu kafelka Marketo w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji usługi Marketo.</span><span class="sxs-lookup"><span data-stu-id="5bf65-295">When you click the Marketo tile in the Access Panel, you should get automatically signed-on to your Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bf65-296">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5bf65-296">Additional resources</span></span>

* [<span data-ttu-id="5bf65-297">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bf65-297">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bf65-298">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5bf65-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

