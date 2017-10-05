---
title: "Samouczek: Integracji Azure Active Directory z pomocą techniczną Jitbit | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Jitbit pracy działu pomocy technicznej."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="c21a0-103">Samouczek: Integracji Azure Active Directory z pomocą techniczną Jitbit</span><span class="sxs-lookup"><span data-stu-id="c21a0-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="c21a0-104">Z tego samouczka dowiesz integrowanie pomocy technicznej Jitbit z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c21a0-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c21a0-105">Integrowanie pomocy technicznej Jitbit z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c21a0-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c21a0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do działu pomocy technicznej Jitbit</span><span class="sxs-lookup"><span data-stu-id="c21a0-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="c21a0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do działu pomocy technicznej Jitbit (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c21a0-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c21a0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c21a0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c21a0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c21a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c21a0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c21a0-110">Prerequisites</span></span>

<span data-ttu-id="c21a0-111">Aby skonfigurować integrację usługi Azure AD z pomocą techniczną Jitbit, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c21a0-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="c21a0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c21a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c21a0-113">Pomoc techniczna Jitbit logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c21a0-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c21a0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c21a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c21a0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c21a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c21a0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c21a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c21a0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c21a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c21a0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c21a0-118">Scenario description</span></span>
<span data-ttu-id="c21a0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c21a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c21a0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c21a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c21a0-121">Dodawanie pomocy technicznej Jitbit z galerii</span><span class="sxs-lookup"><span data-stu-id="c21a0-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="c21a0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c21a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="c21a0-123">Dodawanie pomocy technicznej Jitbit z galerii</span><span class="sxs-lookup"><span data-stu-id="c21a0-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="c21a0-124">Aby skonfigurować integrację usługi Azure AD Jitbit pracy działu pomocy technicznej, należy dodać techniczną Jitbit z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c21a0-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c21a0-125">**Aby dodać techniczną Jitbit z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c21a0-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c21a0-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c21a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="c21a0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c21a0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="c21a0-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c21a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="c21a0-133">W polu wyszukiwania wpisz **techniczną Jitbit**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="c21a0-135">W panelu wyników wybierz **techniczną Jitbit**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c21a0-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c21a0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c21a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c21a0-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z pomocą techniczną Jitbit w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c21a0-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c21a0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Jitbit pomoc techniczna jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c21a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="c21a0-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w Jitbit pomoc techniczna musi określone.</span><span class="sxs-lookup"><span data-stu-id="c21a0-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="c21a0-141">Pomoc techniczna Jitbit, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c21a0-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c21a0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z pomocą techniczną Jitbit, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c21a0-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c21a0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c21a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c21a0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c21a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c21a0-145">**[Tworzenie użytkownika testowego techniczną Jitbit](#creating-a-jitbit-helpdesk-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Jitbit pomocy, w którym jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c21a0-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c21a0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c21a0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c21a0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c21a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c21a0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c21a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c21a0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Jitbit pracy działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="c21a0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="c21a0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z pomocą techniczną Jitbit, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c21a0-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="c21a0-151">W portalu Azure na **techniczną Jitbit** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="c21a0-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c21a0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="c21a0-155">Na **Jitbit pomoc techniczna domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c21a0-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="c21a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="c21a0-157">a.</span></span> <span data-ttu-id="c21a0-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="c21a0-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="c21a0-159">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c21a0-159">This value is not real.</span></span> <span data-ttu-id="c21a0-160">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="c21a0-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c21a0-161">Skontaktuj się z [zespołem pomocy technicznej klienta techniczną Jitbit](https://www.jitbit.com/support/) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="c21a0-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="c21a0-162">b.</span><span class="sxs-lookup"><span data-stu-id="c21a0-162">b.</span></span>  <span data-ttu-id="c21a0-163">W **identyfikator** tekstowym, wpisz adres URL jako poniżej:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="c21a0-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="c21a0-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c21a0-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="c21a0-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c21a0-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c21a0-168">Na **konfiguracji pomoc techniczna Jitbit** , kliknij przycisk **skonfigurować Pomoc techniczna Jitbit** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c21a0-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c21a0-169">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c21a0-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="c21a0-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny Jitbit pracy działu pomocy technicznej firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c21a0-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="c21a0-172">Na pasku narzędzi u góry kliknij **administracji**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="c21a0-173">![Administracja](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="c21a0-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="c21a0-174">Kliknij przycisk **ustawienia ogólne**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="c21a0-175">![Użytkownicy, firm i uprawnienia](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "użytkowników, firmach i uprawnień")</span><span class="sxs-lookup"><span data-stu-id="c21a0-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="c21a0-176">W **ustawienia uwierzytelniania** konfiguracji sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c21a0-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="c21a0-177">![Ustawienia uwierzytelniania](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "ustawienia uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="c21a0-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="c21a0-178">a.</span><span class="sxs-lookup"><span data-stu-id="c21a0-178">a.</span></span> <span data-ttu-id="c21a0-179">Wybierz **Włącz SAML 2.0 pojedynczego logowania**, aby zalogować się przy użyciu pojedynczego logowania jednokrotnego (SSO), z **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="c21a0-180">b.</span><span class="sxs-lookup"><span data-stu-id="c21a0-180">b.</span></span> <span data-ttu-id="c21a0-181">W **adres URL punktu końcowego** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c21a0-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c21a0-182">c.</span><span class="sxs-lookup"><span data-stu-id="c21a0-182">c.</span></span> <span data-ttu-id="c21a0-183">Otwórz z **base-64** zakodowane certyfikatów w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu X.509** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="c21a0-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="c21a0-184">d.</span><span class="sxs-lookup"><span data-stu-id="c21a0-184">d.</span></span> <span data-ttu-id="c21a0-185">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c21a0-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c21a0-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c21a0-187">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c21a0-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c21a0-188">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c21a0-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c21a0-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c21a0-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="c21a0-190">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c21a0-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="c21a0-192">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c21a0-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c21a0-193">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c21a0-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c21a0-195">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c21a0-197">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c21a0-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c21a0-199">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c21a0-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c21a0-201">a.</span><span class="sxs-lookup"><span data-stu-id="c21a0-201">a.</span></span> <span data-ttu-id="c21a0-202">W **nazwa** pole tekstowe, nazwa typu jako **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="c21a0-203">b.</span><span class="sxs-lookup"><span data-stu-id="c21a0-203">b.</span></span> <span data-ttu-id="c21a0-204">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c21a0-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c21a0-205">c.</span><span class="sxs-lookup"><span data-stu-id="c21a0-205">c.</span></span> <span data-ttu-id="c21a0-206">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c21a0-207">d.</span><span class="sxs-lookup"><span data-stu-id="c21a0-207">d.</span></span> <span data-ttu-id="c21a0-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="c21a0-209">Tworzenie użytkownika testowego Jitbit pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="c21a0-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="c21a0-210">Aby włączyć użytkowników usługi Azure AD zalogować się do pomocy technicznej Jitbit, muszą mieć przydzielone do Jitbit pracy działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="c21a0-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="c21a0-211">W przypadku Jitbit pomocy technicznej Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c21a0-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="c21a0-212">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c21a0-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c21a0-213">Zaloguj się do Twojego **techniczną Jitbit** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="c21a0-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="c21a0-214">W menu u góry kliknij **administracji**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="c21a0-215">![Administracja](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="c21a0-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="c21a0-216">Kliknij przycisk **użytkowników, firmach i uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="c21a0-217">![Użytkownicy, firm i uprawnienia](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "użytkowników, firmach i uprawnień")</span><span class="sxs-lookup"><span data-stu-id="c21a0-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="c21a0-218">Kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="c21a0-219">![Dodaj użytkownika](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="c21a0-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="c21a0-220">W sekcji Tworzenie wpisz dane konto usługi Azure AD, którą chcesz udostępnić w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c21a0-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="c21a0-221">![Utwórz](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="c21a0-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="c21a0-222">a.</span><span class="sxs-lookup"><span data-stu-id="c21a0-222">a.</span></span> <span data-ttu-id="c21a0-223">W **Username** pole tekstowe, typ **BrittaSimon**, nazwę użytkownika w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c21a0-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="c21a0-224">b.</span><span class="sxs-lookup"><span data-stu-id="c21a0-224">b.</span></span> <span data-ttu-id="c21a0-225">W **E-mail** tekstowym, wpisz adres e-mail użytkownika, takich jak  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c21a0-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="c21a0-226">c.</span><span class="sxs-lookup"><span data-stu-id="c21a0-226">c.</span></span> <span data-ttu-id="c21a0-227">W **imię** tekstowym, wpisz imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="c21a0-228">d.</span><span class="sxs-lookup"><span data-stu-id="c21a0-228">d.</span></span> <span data-ttu-id="c21a0-229">W **nazwisko** tekstowym, wpisz nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="c21a0-230">e.</span><span class="sxs-lookup"><span data-stu-id="c21a0-230">e.</span></span> <span data-ttu-id="c21a0-231">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="c21a0-232">Inne narzędzia do tworzenia konta użytkownika Jitbit pracy działu pomocy technicznej lub interfejsów API dostarczonych przez Pomoc techniczna Jitbit służy do obsługi administracyjnej kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c21a0-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c21a0-233">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c21a0-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c21a0-234">W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do działu pomocy technicznej Jitbit.</span><span class="sxs-lookup"><span data-stu-id="c21a0-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="c21a0-236">**Aby przypisać Simona Britta do działu pomocy technicznej Jitbit, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c21a0-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="c21a0-237">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c21a0-239">Na liście aplikacji zaznacz **techniczną Jitbit**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="c21a0-241">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c21a0-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="c21a0-243">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c21a0-243">Click **Add** button.</span></span> <span data-ttu-id="c21a0-244">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c21a0-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="c21a0-246">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c21a0-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c21a0-247">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c21a0-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c21a0-248">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c21a0-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c21a0-249">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c21a0-249">Testing single sign-on</span></span>

<span data-ttu-id="c21a0-250">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c21a0-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c21a0-251">Po kliknięciu kafelka Jitbit pomoc techniczna w panelu dostępu, należy pobrać strony logowania aplikacji Jitbit pracy działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="c21a0-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="c21a0-252">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c21a0-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c21a0-253">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c21a0-253">Additional resources</span></span>

* [<span data-ttu-id="c21a0-254">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c21a0-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c21a0-255">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c21a0-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

