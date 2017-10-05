---
title: 'Samouczek: Integracji Azure Active Directory z Mixpanel | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3dd11b3477de1329c1c8e45a6dbf212b1635fd95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="8ce29-103">Samouczek: Integracji Azure Active Directory z Mixpanel</span><span class="sxs-lookup"><span data-stu-id="8ce29-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="8ce29-104">Z tego samouczka dowiesz się integrowanie Mixpanel z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ce29-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ce29-105">Integracja z usługą Azure AD Mixpanel zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8ce29-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8ce29-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Mixpanel</span><span class="sxs-lookup"><span data-stu-id="8ce29-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="8ce29-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Mixpanel (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce29-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ce29-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8ce29-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8ce29-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ce29-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ce29-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ce29-110">Prerequisites</span></span>

<span data-ttu-id="8ce29-111">Aby skonfigurować integrację usługi Azure AD z Mixpanel, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8ce29-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="8ce29-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ce29-113">Mixpanel logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8ce29-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ce29-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ce29-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ce29-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8ce29-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ce29-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8ce29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ce29-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ce29-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ce29-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8ce29-118">Scenario description</span></span>
<span data-ttu-id="8ce29-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8ce29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ce29-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8ce29-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ce29-121">Dodawanie Mixpanel z galerii</span><span class="sxs-lookup"><span data-stu-id="8ce29-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="8ce29-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ce29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="8ce29-123">Dodawanie Mixpanel z galerii</span><span class="sxs-lookup"><span data-stu-id="8ce29-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="8ce29-124">Aby skonfigurować integrację usługi Azure AD Mixpanel, należy dodać Mixpanel z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ce29-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8ce29-125">**Aby dodać Mixpanel z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ce29-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ce29-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ce29-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8ce29-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8ce29-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8ce29-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ce29-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8ce29-133">W polu wyszukiwania wpisz **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-133">In the search box, type **Mixpanel**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="8ce29-135">W panelu wyników wybierz **Mixpanel**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8ce29-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ce29-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ce29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ce29-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mixpanel w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8ce29-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ce29-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Mixpanel jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ce29-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="8ce29-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Mixpanel musi się.</span><span class="sxs-lookup"><span data-stu-id="8ce29-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="8ce29-141">W Mixpanel, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="8ce29-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8ce29-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mixpanel, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8ce29-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ce29-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8ce29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ce29-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ce29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ce29-145">**[Tworzenie użytkownika testowego Mixpanel](#creating-a-mixpanel-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Mixpanel połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ce29-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ce29-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ce29-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ce29-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8ce29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ce29-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ce29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ce29-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="8ce29-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="8ce29-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Mixpanel, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ce29-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="8ce29-151">W portalu Azure na **Mixpanel** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8ce29-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="8ce29-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="8ce29-155">Na **Mixpanel domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8ce29-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="8ce29-157">W **adres URL logowania** tekstowym, wpisz adres URL jako:`https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="8ce29-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ce29-158">Zarejestruj w [https://mixpanel.com/register/](https://mixpanel.com/register/) skonfigurować poświadczenia logowania i skontaktuj się z [zespołem pomocy technicznej Mixpanel](mailto:support@mixpanel.com) Aby włączyć ustawienia logowania jednokrotnego dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="8ce29-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="8ce29-159">Możesz również uzyskać wartość na adres URL logowania w razie potrzeby z zespołem pomocy technicznej Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="8ce29-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="8ce29-160">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8ce29-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="8ce29-162">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ce29-162">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8ce29-164">Na **konfiguracji Mixpanel** , kliknij przycisk **skonfigurować Mixpanel** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8ce29-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8ce29-165">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8ce29-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="8ce29-167">W oknie innej przeglądarki logowanie do aplikacji Mixpanel jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8ce29-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="8ce29-168">W dolnej części strony, kliknij polecenie trochę **narzędzi** ikonę w lewym rogu.</span><span class="sxs-lookup"><span data-stu-id="8ce29-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Mixpanel rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="8ce29-170">Kliknij przycisk **dostęp zabezpieczeń** , a następnie kliknij pozycję **zmienić ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Ustawienia Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="8ce29-172">Na **zmienić certyfikat** strony okna dialogowego, kliknij przycisk **wybierz plik** przekazanie pobranego certyfikatu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Ustawienia Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="8ce29-174">W polu tekstowym adres URL uwierzytelniania na **zmienić adres URL uwierzytelniania** okna dialogowego strony, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Ustawienia Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="8ce29-176">Kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="8ce29-177">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="8ce29-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8ce29-178">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8ce29-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8ce29-179">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ce29-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ce29-180">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce29-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ce29-181">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ce29-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8ce29-183">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ce29-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ce29-184">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ce29-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ce29-186">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ce29-188">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ce29-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ce29-190">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8ce29-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ce29-192">a.</span><span class="sxs-lookup"><span data-stu-id="8ce29-192">a.</span></span> <span data-ttu-id="8ce29-193">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ce29-194">b.</span><span class="sxs-lookup"><span data-stu-id="8ce29-194">b.</span></span> <span data-ttu-id="8ce29-195">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ce29-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ce29-196">c.</span><span class="sxs-lookup"><span data-stu-id="8ce29-196">c.</span></span> <span data-ttu-id="8ce29-197">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8ce29-198">d.</span><span class="sxs-lookup"><span data-stu-id="8ce29-198">d.</span></span> <span data-ttu-id="8ce29-199">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="8ce29-200">Tworzenie użytkownika testowego Mixpanel</span><span class="sxs-lookup"><span data-stu-id="8ce29-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="8ce29-201">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="8ce29-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="8ce29-202">Zalogować się do witryny firmy Mixpanel jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8ce29-202">Sign on to your Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="8ce29-203">W dolnej części strony, kliknij przycisk Koło zębate małego na lewym rogu, aby otworzyć **ustawienia** okna.</span><span class="sxs-lookup"><span data-stu-id="8ce29-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

3. <span data-ttu-id="8ce29-204">Kliknij przycisk **zespołu** kartę.</span><span class="sxs-lookup"><span data-stu-id="8ce29-204">Click the **Team** tab.</span></span>

4. <span data-ttu-id="8ce29-205">W **członek zespołu** tekstowym, wpisz adres e-mail Britta na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="8ce29-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Ustawienia Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="8ce29-207">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="8ce29-208">Użytkownik otrzyma wiadomość e-mail, aby skonfigurować profil.</span><span class="sxs-lookup"><span data-stu-id="8ce29-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8ce29-209">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce29-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8ce29-210">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="8ce29-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8ce29-212">**Aby przypisać Simona Britta Mixpanel, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8ce29-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="8ce29-213">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8ce29-215">Na liście aplikacji zaznacz **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-215">In the applications list, select **Mixpanel**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="8ce29-217">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8ce29-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8ce29-219">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ce29-219">Click **Add** button.</span></span> <span data-ttu-id="8ce29-220">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ce29-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8ce29-222">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8ce29-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8ce29-223">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ce29-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ce29-224">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ce29-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ce29-225">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ce29-225">Testing single sign-on</span></span>

<span data-ttu-id="8ce29-226">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8ce29-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8ce29-227">Po kliknięciu kafelka Mixpanel w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="8ce29-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="8ce29-228">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ce29-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ce29-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8ce29-229">Additional resources</span></span>

* [<span data-ttu-id="8ce29-230">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ce29-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ce29-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ce29-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

