---
title: 'Samouczek: Integracji Azure Active Directory z Pantheon | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 3f4ac1db2ee83d9f9fcb375d0fb7c40ad21c4688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="afee6-103">Samouczek: Integracji Azure Active Directory z Pantheon</span><span class="sxs-lookup"><span data-stu-id="afee6-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="afee6-104">Z tego samouczka dowiesz się integrowanie Pantheon z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="afee6-104">In this tutorial, you learn how to integrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="afee6-105">Integracja z usługą Azure AD Pantheon zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="afee6-105">Integrating Pantheon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="afee6-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Pantheon</span><span class="sxs-lookup"><span data-stu-id="afee6-106">You can control in Azure AD who has access to Pantheon</span></span>
- <span data-ttu-id="afee6-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Pantheon (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="afee6-107">You can enable your users to automatically get signed-on to Pantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="afee6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="afee6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="afee6-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="afee6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afee6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="afee6-110">Prerequisites</span></span>

<span data-ttu-id="afee6-111">Aby skonfigurować integrację usługi Azure AD z Pantheon, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="afee6-111">To configure Azure AD integration with Pantheon, you need the following items:</span></span>

- <span data-ttu-id="afee6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="afee6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="afee6-113">Pantheon logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="afee6-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="afee6-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="afee6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="afee6-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="afee6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="afee6-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="afee6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="afee6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="afee6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="afee6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="afee6-118">Scenario description</span></span>
<span data-ttu-id="afee6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="afee6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="afee6-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="afee6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="afee6-121">Dodawanie Pantheon z galerii</span><span class="sxs-lookup"><span data-stu-id="afee6-121">Adding Pantheon from the gallery</span></span>
2. <span data-ttu-id="afee6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="afee6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-the-gallery"></a><span data-ttu-id="afee6-123">Dodawanie Pantheon z galerii</span><span class="sxs-lookup"><span data-stu-id="afee6-123">Adding Pantheon from the gallery</span></span>
<span data-ttu-id="afee6-124">Aby skonfigurować integrację usługi Azure AD Pantheon, należy dodać Pantheon z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="afee6-124">To configure the integration of Pantheon into Azure AD, you need to add Pantheon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="afee6-125">**Aby dodać Pantheon z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="afee6-125">**To add Pantheon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="afee6-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="afee6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="afee6-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="afee6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="afee6-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="afee6-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="afee6-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="afee6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="afee6-133">W polu wyszukiwania wpisz **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="afee6-133">In the search box, type **Pantheon**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="afee6-135">W panelu wyników wybierz **Pantheon**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="afee6-135">In the results panel, select **Pantheon**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="afee6-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="afee6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="afee6-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pantheon w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="afee6-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="afee6-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Pantheon jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afee6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Pantheon is to a user in Azure AD.</span></span> <span data-ttu-id="afee6-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Pantheon musi się.</span><span class="sxs-lookup"><span data-stu-id="afee6-140">In other words, a link relationship between an Azure AD user and the related user in Pantheon needs to be established.</span></span>

<span data-ttu-id="afee6-141">W Pantheon, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="afee6-141">In Pantheon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="afee6-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pantheon, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="afee6-142">To configure and test Azure AD single sign-on with Pantheon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="afee6-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="afee6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="afee6-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="afee6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="afee6-145">**[Tworzenie użytkownika testowego Pantheon](#creating-a-pantheon-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Pantheon połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afee6-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - to have a counterpart of Britta Simon in Pantheon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="afee6-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="afee6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="afee6-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="afee6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="afee6-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="afee6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="afee6-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Pantheon.</span><span class="sxs-lookup"><span data-stu-id="afee6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="afee6-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Pantheon, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="afee6-150">**To configure Azure AD single sign-on with Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="afee6-151">W portalu Azure na **Pantheon** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="afee6-151">In the Azure portal, on the **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="afee6-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="afee6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="afee6-155">Na **Pantheon domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="afee6-155">On the **Pantheon Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="afee6-157">a.</span><span class="sxs-lookup"><span data-stu-id="afee6-157">a.</span></span> <span data-ttu-id="afee6-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="afee6-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="afee6-159">b.</span><span class="sxs-lookup"><span data-stu-id="afee6-159">b.</span></span> <span data-ttu-id="afee6-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="afee6-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="afee6-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="afee6-161">These values are not real.</span></span> <span data-ttu-id="afee6-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="afee6-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="afee6-163">Skontaktuj się z [zespołem pomocy technicznej Pantheon](https://pantheon.io/docs/getting-support/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="afee6-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) to get these values.</span></span>

4. <span data-ttu-id="afee6-164">Aplikacja pantheon oczekuje potwierdzenia języka SAML w określonym formacie, który należy ustawić wartość atrybutu UserIdentifier z adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afee6-164">Pantheon application expects the SAML assertion in specific format, which requires you to set the UserIdentifier attribute value with the user’s email address.</span></span> <span data-ttu-id="afee6-165">Domyślnie usługi Azure AD używa właściwości UserPrincipalName UserIdentifier atrybutu.</span><span class="sxs-lookup"><span data-stu-id="afee6-165">By default Azure AD uses the UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="afee6-166">Jednak dla pomyślnej integracji musisz dostosować tę wartość do dopasowania z adresu e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afee6-166">But for successful integration you need to adjust this value to match with user’s email address.</span></span> <span data-ttu-id="afee6-167">Integracja działa tylko po wykonaniu poprawne mapowania.</span><span class="sxs-lookup"><span data-stu-id="afee6-167">The integration will only work after doing the correct mapping.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="afee6-169">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="afee6-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="afee6-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="afee6-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="afee6-173">Na **konfiguracji Pantheon** , kliknij przycisk **skonfigurować Pantheon** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="afee6-173">On the **Pantheon Configuration** section, click **Configure Pantheon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="afee6-174">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="afee6-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="afee6-176">Aby skonfigurować logowanie jednokrotne w **Pantheon** stronie, musisz wysłać pobrany **certyfikatu** i **SAML pojedynczy znak na adres URL usługi** do [Pantheon obsługuje zespołu](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="afee6-176">To configure single sign-on on **Pantheon** side, you need to send the downloaded **Certificate** and **SAML Single Sign-On Service URL** to [Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="afee6-177">Należy również zawierają informacje domeny poczty E-mail oraz Data i godzina, gdy chcesz włączyć tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="afee6-177">You also need to provide the Email Domain(s) information and Date Time when you want to enable this connection.</span></span> <span data-ttu-id="afee6-178">Można znaleźć więcej szczegółów na temat z [tutaj](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="afee6-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="afee6-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="afee6-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="afee6-180">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="afee6-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="afee6-181">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="afee6-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="afee6-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="afee6-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="afee6-183">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="afee6-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="afee6-185">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="afee6-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="afee6-186">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="afee6-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="afee6-188">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="afee6-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="afee6-190">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="afee6-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="afee6-192">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="afee6-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="afee6-194">a.</span><span class="sxs-lookup"><span data-stu-id="afee6-194">a.</span></span> <span data-ttu-id="afee6-195">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="afee6-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="afee6-196">b.</span><span class="sxs-lookup"><span data-stu-id="afee6-196">b.</span></span> <span data-ttu-id="afee6-197">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="afee6-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="afee6-198">c.</span><span class="sxs-lookup"><span data-stu-id="afee6-198">c.</span></span> <span data-ttu-id="afee6-199">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="afee6-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="afee6-200">d.</span><span class="sxs-lookup"><span data-stu-id="afee6-200">d.</span></span> <span data-ttu-id="afee6-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="afee6-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="afee6-202">Tworzenie użytkownika testowego Pantheon</span><span class="sxs-lookup"><span data-stu-id="afee6-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="afee6-203">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Pantheon.</span><span class="sxs-lookup"><span data-stu-id="afee6-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="afee6-204">Wykonaj następujące czynności, aby dodać użytkownika w Pantheon.</span><span class="sxs-lookup"><span data-stu-id="afee6-204">Please follow the below steps to add the user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="afee6-205">Do logowania jednokrotnego pracować użytkownik musi najpierw należy utworzyć w Pantheon.</span><span class="sxs-lookup"><span data-stu-id="afee6-205">For SSO to work user needs to be created first in Pantheon.</span></span>

1. <span data-ttu-id="afee6-206">Zaloguj się do Pantheon przy użyciu poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="afee6-206">Login to Pantheon with admin credentials.</span></span>

2. <span data-ttu-id="afee6-207">Przejdź do **organizacji** strony pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="afee6-207">Navigate to **Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="afee6-208">Kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="afee6-208">Click **People**.</span></span>

4. <span data-ttu-id="afee6-209">Kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="afee6-209">Click **Add user**.</span></span>

5. <span data-ttu-id="afee6-210">Wprowadź adres e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afee6-210">Enter the user's email address.</span></span>

6. <span data-ttu-id="afee6-211">Wybierz rolę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="afee6-211">Choose the user's role.</span></span>

7. <span data-ttu-id="afee6-212">Kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="afee6-212">Click **Add user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="afee6-213">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="afee6-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="afee6-214">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Pantheon.</span><span class="sxs-lookup"><span data-stu-id="afee6-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Pantheon.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="afee6-216">**Aby przypisać Simona Britta Pantheon, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="afee6-216">**To assign Britta Simon to Pantheon, perform the following steps:**</span></span>

1. <span data-ttu-id="afee6-217">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="afee6-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="afee6-219">Na liście aplikacji zaznacz **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="afee6-219">In the applications list, select **Pantheon**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="afee6-221">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="afee6-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="afee6-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="afee6-223">Click **Add** button.</span></span> <span data-ttu-id="afee6-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="afee6-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="afee6-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="afee6-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="afee6-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="afee6-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="afee6-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="afee6-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="afee6-229">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="afee6-229">Testing single sign-on</span></span>

<span data-ttu-id="afee6-230">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="afee6-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="afee6-231">Po kliknięciu kafelka Pantheon w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Pantheon.</span><span class="sxs-lookup"><span data-stu-id="afee6-231">When you click the Pantheon tile in the Access Panel, you should get automatically signed-on to your Pantheon application.</span></span>
<span data-ttu-id="afee6-232">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="afee6-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="afee6-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="afee6-233">Additional resources</span></span>

* [<span data-ttu-id="afee6-234">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afee6-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="afee6-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="afee6-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

