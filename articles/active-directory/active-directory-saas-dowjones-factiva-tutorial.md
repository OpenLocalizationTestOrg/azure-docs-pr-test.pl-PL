---
title: 'Samouczek: Integracji Azure Active Directory z Factiva Nowak knie | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Factiva Nowak knie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: dab48c24ff25fd68df1ee540bb8f0929e7e81bcb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="370ee-103">Samouczek: Integracji Azure Active Directory z Factiva Nowak knie</span><span class="sxs-lookup"><span data-stu-id="370ee-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="370ee-104">Z tego samouczka dowiesz integrowanie Factiva Nowak knie z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="370ee-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="370ee-105">Integracja z usługą Azure AD Factiva Nowak knie zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="370ee-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="370ee-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Factiva Nowak knie</span><span class="sxs-lookup"><span data-stu-id="370ee-106">You can control in Azure AD who has access to Dow Jones Factiva</span></span>
- <span data-ttu-id="370ee-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Factiva Nowak knie (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="370ee-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="370ee-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="370ee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="370ee-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="370ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="370ee-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="370ee-110">Prerequisites</span></span>

<span data-ttu-id="370ee-111">Aby skonfigurować integrację usługi Azure AD z Factiva Nowak knie, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="370ee-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span></span>

- <span data-ttu-id="370ee-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="370ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="370ee-113">Knie Nowak Factiva jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="370ee-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="370ee-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="370ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="370ee-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="370ee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="370ee-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="370ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="370ee-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="370ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="370ee-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="370ee-118">Scenario description</span></span>
<span data-ttu-id="370ee-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="370ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="370ee-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="370ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="370ee-121">Dodawanie Factiva Nowak knie z galerii</span><span class="sxs-lookup"><span data-stu-id="370ee-121">Adding Dow Jones Factiva from the gallery</span></span>
2. <span data-ttu-id="370ee-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="370ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-the-gallery"></a><span data-ttu-id="370ee-123">Dodawanie Factiva Nowak knie z galerii</span><span class="sxs-lookup"><span data-stu-id="370ee-123">Adding Dow Jones Factiva from the gallery</span></span>
<span data-ttu-id="370ee-124">Aby skonfigurować integrację usługi Azure AD Factiva Nowak knie, należy dodać Factiva Nowak knie z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="370ee-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="370ee-125">**Aby dodać Factiva Nowak knie z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="370ee-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="370ee-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="370ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="370ee-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="370ee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="370ee-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="370ee-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="370ee-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="370ee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="370ee-133">W polu wyszukiwania wpisz **knie Nowak Factiva**.</span><span class="sxs-lookup"><span data-stu-id="370ee-133">In the search box, type **Dow Jones Factiva**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="370ee-135">W panelu wyników wybierz **Factiva Nowak knie**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="370ee-135">In the results panel, select **Dow Jones Factiva**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="370ee-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="370ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="370ee-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Factiva Nowak knie oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="370ee-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="370ee-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Factiva Nowak knie jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="370ee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span></span> <span data-ttu-id="370ee-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w knie Factiva Nowak musi można ustanowić.</span><span class="sxs-lookup"><span data-stu-id="370ee-140">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span></span>

<span data-ttu-id="370ee-141">W knie Nowak Factiva, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="370ee-141">In Dow Jones Factiva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="370ee-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Factiva Nowak knie, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="370ee-142">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="370ee-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="370ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="370ee-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="370ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="370ee-145">**[Tworzenie użytkownika testowego Factiva Nowak knie](#creating-a-dow-jones-factiva-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Factiva Nowak knie, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="370ee-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="370ee-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="370ee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="370ee-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="370ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="370ee-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="370ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="370ee-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Factiva Nowak knie.</span><span class="sxs-lookup"><span data-stu-id="370ee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="370ee-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Factiva Nowak knie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="370ee-150">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="370ee-151">W portalu Azure na **Factiva Nowak knie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="370ee-151">In the Azure portal, on the **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="370ee-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="370ee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="370ee-155">Na **knie Nowak Factiva domeny i adres URL** sekcji, użytkownik nie trzeba wykonywać żadnych czynności, jak aplikacja już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="370ee-155">On the **Dow Jones Factiva Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="370ee-157">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="370ee-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="370ee-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="370ee-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="370ee-161">Skonfigurować logowanie jednokrotne w **Factiva Nowak knie** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Factiva Nowak knie](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="370ee-161">To configure single sign-on on **Dow Jones Factiva** side, you need to send the downloaded **Metadata XML** to [Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="370ee-162">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="370ee-162">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="370ee-163">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="370ee-163">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="370ee-164">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="370ee-164">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="370ee-165">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="370ee-165">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="370ee-166">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="370ee-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="370ee-167">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="370ee-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="370ee-169">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="370ee-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="370ee-170">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="370ee-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="370ee-172">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="370ee-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="370ee-174">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="370ee-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="370ee-176">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="370ee-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="370ee-178">a.</span><span class="sxs-lookup"><span data-stu-id="370ee-178">a.</span></span> <span data-ttu-id="370ee-179">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="370ee-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="370ee-180">b.</span><span class="sxs-lookup"><span data-stu-id="370ee-180">b.</span></span> <span data-ttu-id="370ee-181">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="370ee-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="370ee-182">c.</span><span class="sxs-lookup"><span data-stu-id="370ee-182">c.</span></span> <span data-ttu-id="370ee-183">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="370ee-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="370ee-184">d.</span><span class="sxs-lookup"><span data-stu-id="370ee-184">d.</span></span> <span data-ttu-id="370ee-185">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="370ee-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="370ee-186">Tworzenie użytkownika testowego Factiva Nowak knie</span><span class="sxs-lookup"><span data-stu-id="370ee-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="370ee-187">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Factiva Nowak knie.</span><span class="sxs-lookup"><span data-stu-id="370ee-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="370ee-188">We współpracy z knie [zespołem pomocy technicznej Factiva Nowak](https://www.dowjones.com/contact/) Aby dodać użytkowników na platformie Factiva Nowak knie.</span><span class="sxs-lookup"><span data-stu-id="370ee-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) to add the users in the Dow Jones Factiva platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="370ee-189">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="370ee-189">Assigning the Azure AD test user</span></span>

<span data-ttu-id="370ee-190">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Factiva Nowak knie.</span><span class="sxs-lookup"><span data-stu-id="370ee-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dow Jones Factiva.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="370ee-192">**Aby przypisać Simona Britta knie Nowak Factiva, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="370ee-192">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="370ee-193">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="370ee-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="370ee-195">Na liście aplikacji zaznacz **knie Nowak Factiva**.</span><span class="sxs-lookup"><span data-stu-id="370ee-195">In the applications list, select **Dow Jones Factiva**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="370ee-197">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="370ee-197">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="370ee-199">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="370ee-199">Click **Add** button.</span></span> <span data-ttu-id="370ee-200">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="370ee-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="370ee-202">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="370ee-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="370ee-203">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="370ee-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="370ee-204">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="370ee-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="370ee-205">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="370ee-205">Testing single sign-on</span></span>

<span data-ttu-id="370ee-206">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="370ee-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="370ee-207">Po kliknięciu kafelka Factiva Nowak knie w panelu dostępu należy należy pobrać automatycznie zalogowane Factiva Nowak knie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="370ee-207">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span></span>
<span data-ttu-id="370ee-208">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="370ee-208">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="370ee-209">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="370ee-209">Additional resources</span></span>

* [<span data-ttu-id="370ee-210">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="370ee-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="370ee-211">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="370ee-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

