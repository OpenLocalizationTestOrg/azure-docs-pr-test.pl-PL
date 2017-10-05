---
title: 'Samouczek: Integracji Azure Active Directory z PostBeyond | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i PostBeyond."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 80b920dc99619795cbc86e8cb2e3ac2a78a71932
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="59e7b-103">Samouczek: Integracji Azure Active Directory z PostBeyond</span><span class="sxs-lookup"><span data-stu-id="59e7b-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>

<span data-ttu-id="59e7b-104">Z tego samouczka dowiesz się integrowanie PostBeyond z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59e7b-104">In this tutorial, you learn how to integrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="59e7b-105">Integracja z usługą Azure AD PostBeyond zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="59e7b-105">Integrating PostBeyond with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="59e7b-106">Można kontrolować w usłudze Azure AD, który ma dostęp do PostBeyond</span><span class="sxs-lookup"><span data-stu-id="59e7b-106">You can control in Azure AD who has access to PostBeyond</span></span>
- <span data-ttu-id="59e7b-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do PostBeyond (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e7b-107">You can enable your users to automatically get signed-on to PostBeyond (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="59e7b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="59e7b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="59e7b-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59e7b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59e7b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59e7b-110">Prerequisites</span></span>

<span data-ttu-id="59e7b-111">Aby skonfigurować integrację usługi Azure AD z PostBeyond, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="59e7b-111">To configure Azure AD integration with PostBeyond, you need the following items:</span></span>

- <span data-ttu-id="59e7b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e7b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="59e7b-113">PostBeyond logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="59e7b-113">A PostBeyond single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59e7b-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="59e7b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="59e7b-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="59e7b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="59e7b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="59e7b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="59e7b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59e7b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59e7b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="59e7b-118">Scenario description</span></span>
<span data-ttu-id="59e7b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="59e7b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="59e7b-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="59e7b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59e7b-121">Dodawanie PostBeyond z galerii</span><span class="sxs-lookup"><span data-stu-id="59e7b-121">Adding PostBeyond from the gallery</span></span>
2. <span data-ttu-id="59e7b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="59e7b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-postbeyond-from-the-gallery"></a><span data-ttu-id="59e7b-123">Dodawanie PostBeyond z galerii</span><span class="sxs-lookup"><span data-stu-id="59e7b-123">Adding PostBeyond from the gallery</span></span>
<span data-ttu-id="59e7b-124">Aby skonfigurować integrację PostBeyond do usługi Azure AD, należy dodać PostBeyond z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="59e7b-124">To configure the integration of PostBeyond into Azure AD, you need to add PostBeyond from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="59e7b-125">**Aby dodać PostBeyond z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="59e7b-125">**To add PostBeyond from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="59e7b-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="59e7b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="59e7b-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="59e7b-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="59e7b-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59e7b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="59e7b-133">W polu wyszukiwania wpisz **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-133">In the search box, type **PostBeyond**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_search.png)

5. <span data-ttu-id="59e7b-135">W panelu wyników wybierz **PostBeyond**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="59e7b-135">In the results panel, select **PostBeyond**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59e7b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="59e7b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59e7b-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PostBeyond w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="59e7b-138">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59e7b-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w PostBeyond jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e7b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PostBeyond is to a user in Azure AD.</span></span> <span data-ttu-id="59e7b-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w PostBeyond musi się.</span><span class="sxs-lookup"><span data-stu-id="59e7b-140">In other words, a link relationship between an Azure AD user and the related user in PostBeyond needs to be established.</span></span>

<span data-ttu-id="59e7b-141">W PostBeyond, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="59e7b-141">In PostBeyond, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="59e7b-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z PostBeyond, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="59e7b-142">To configure and test Azure AD single sign-on with PostBeyond, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="59e7b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="59e7b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="59e7b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="59e7b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59e7b-145">**[Tworzenie użytkownika testowego PostBeyond](#creating-a-postbeyond-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta PostBeyond połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59e7b-145">**[Creating a PostBeyond test user](#creating-a-postbeyond-test-user)** - to have a counterpart of Britta Simon in PostBeyond that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="59e7b-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="59e7b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59e7b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="59e7b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59e7b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59e7b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="59e7b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w PostBeyond aplikacji.</span><span class="sxs-lookup"><span data-stu-id="59e7b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="59e7b-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z PostBeyond, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="59e7b-150">**To configure Azure AD single sign-on with PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="59e7b-151">W portalu Azure na **PostBeyond** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-151">In the Azure portal, on the **PostBeyond** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="59e7b-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="59e7b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_samlbase.png)

3. <span data-ttu-id="59e7b-155">Na **PostBeyond domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59e7b-155">On the **PostBeyond Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_url.png)

    <span data-ttu-id="59e7b-157">a.</span><span class="sxs-lookup"><span data-stu-id="59e7b-157">a.</span></span> <span data-ttu-id="59e7b-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="59e7b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    <span data-ttu-id="59e7b-159">b.</span><span class="sxs-lookup"><span data-stu-id="59e7b-159">b.</span></span> <span data-ttu-id="59e7b-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.postbeyond.com`</span><span class="sxs-lookup"><span data-stu-id="59e7b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.postbeyond.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="59e7b-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="59e7b-161">These values are not real.</span></span> <span data-ttu-id="59e7b-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="59e7b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="59e7b-163">Skontaktuj się z [zespołem pomocy technicznej klienta PostBeyond](mailto:sso@postbeyond.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="59e7b-163">Contact [PostBeyond Client support team](mailto:sso@postbeyond.com) to get these values.</span></span> 
 
4. <span data-ttu-id="59e7b-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="59e7b-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_certificate.png) 

5. <span data-ttu-id="59e7b-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59e7b-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="59e7b-168">Na **konfiguracji PostBeyond** , kliknij przycisk **skonfigurować PostBeyond** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="59e7b-168">On the **PostBeyond Configuration** section, click **Configure PostBeyond** to open **Configure sign-on** window.</span></span> <span data-ttu-id="59e7b-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="59e7b-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_configure.png) 

7. <span data-ttu-id="59e7b-171">Aby skonfigurować logowanie jednokrotne w **PostBeyond** stronie, musisz wysłać pobrany **Certificate(Base64)**, **SAML identyfikator jednostki**, **SAML logowania jednokrotnego Adres URL usługi** i **Sign-Out URL** do [zespołem pomocy technicznej PostBeyond](mailto:sso@postbeyond.com).</span><span class="sxs-lookup"><span data-stu-id="59e7b-171">To configure single sign-on on **PostBeyond** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** to [PostBeyond support team](mailto:sso@postbeyond.com).</span></span> <span data-ttu-id="59e7b-172">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="59e7b-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="59e7b-173">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="59e7b-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="59e7b-174">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="59e7b-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="59e7b-175">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="59e7b-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59e7b-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e7b-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="59e7b-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="59e7b-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="59e7b-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="59e7b-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="59e7b-180">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="59e7b-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="59e7b-182">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="59e7b-184">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59e7b-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="59e7b-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59e7b-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="59e7b-188">a.</span><span class="sxs-lookup"><span data-stu-id="59e7b-188">a.</span></span> <span data-ttu-id="59e7b-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="59e7b-190">b.</span><span class="sxs-lookup"><span data-stu-id="59e7b-190">b.</span></span> <span data-ttu-id="59e7b-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="59e7b-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="59e7b-192">c.</span><span class="sxs-lookup"><span data-stu-id="59e7b-192">c.</span></span> <span data-ttu-id="59e7b-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="59e7b-194">d.</span><span class="sxs-lookup"><span data-stu-id="59e7b-194">d.</span></span> <span data-ttu-id="59e7b-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-195">Click **Create**.</span></span>
 
### <a name="creating-a-postbeyond-test-user"></a><span data-ttu-id="59e7b-196">Tworzenie użytkownika testowego PostBeyond</span><span class="sxs-lookup"><span data-stu-id="59e7b-196">Creating a PostBeyond test user</span></span>

<span data-ttu-id="59e7b-197">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="59e7b-197">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="59e7b-198">Jeśli nie wiadomo, jak dodać Simona Britta w PostBeyond, współpracy z [zespołem pomocy technicznej PostBeyond](mailto:sso@postbeyond.com) Aby dodać użytkownika testowego i włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="59e7b-198">If you don't know how to add Britta Simon in PostBeyond, please work with [PostBeyond support team](mailto:sso@postbeyond.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="59e7b-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="59e7b-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="59e7b-200">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="59e7b-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PostBeyond.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="59e7b-202">**Aby przypisać Simona Britta PostBeyond, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="59e7b-202">**To assign Britta Simon to PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="59e7b-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="59e7b-205">Na liście aplikacji zaznacz **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-205">In the applications list, select **PostBeyond**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_app.png) 

3. <span data-ttu-id="59e7b-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="59e7b-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="59e7b-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="59e7b-209">Click **Add** button.</span></span> <span data-ttu-id="59e7b-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59e7b-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="59e7b-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="59e7b-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="59e7b-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59e7b-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="59e7b-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="59e7b-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="59e7b-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="59e7b-215">Testing single sign-on</span></span>

<span data-ttu-id="59e7b-216">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="59e7b-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="59e7b-217">Po kliknięciu kafelka PostBeyond w panelu dostępu, należy pobrać na PostBeyond Zaloguj się na stronie.</span><span class="sxs-lookup"><span data-stu-id="59e7b-217">When you click the PostBeyond tile in the Access Panel, you should get to the PostBeyond sign in page.</span></span> <span data-ttu-id="59e7b-218">Polecenie **Zaloguj się przy użyciu usługi Office 365**, wprowadź swoje poświadczenia usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="59e7b-218">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="59e7b-219">Następnie możesz należy zalogować się do PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="59e7b-219">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59e7b-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="59e7b-220">Additional resources</span></span>

* [<span data-ttu-id="59e7b-221">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59e7b-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59e7b-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59e7b-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png

