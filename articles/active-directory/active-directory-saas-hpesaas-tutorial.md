---
title: 'Samouczek: Integracji Azure Active Directory z HPE SaaS | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i HPE SaaS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 5e6f0da531df85359aa47477248dd020a039e7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="e426e-103">Samouczek: Integracji Azure Active Directory z HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="e426e-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>

<span data-ttu-id="e426e-104">Z tego samouczka dowiesz się integrowanie HPE SaaS w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e426e-104">In this tutorial, you learn how to integrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e426e-105">Integracja z usługą Azure AD HPE SaaS zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e426e-105">Integrating HPE SaaS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e426e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="e426e-106">You can control in Azure AD who has access to HPE SaaS</span></span>
- <span data-ttu-id="e426e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do HPE SaaS (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e426e-107">You can enable your users to automatically get signed-on to HPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e426e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e426e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e426e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e426e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e426e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e426e-110">Prerequisites</span></span>

<span data-ttu-id="e426e-111">Aby skonfigurować integrację usługi Azure AD z HPE SaaS, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e426e-111">To configure Azure AD integration with HPE SaaS, you need the following items:</span></span>

- <span data-ttu-id="e426e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e426e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e426e-113">HPE SaaS logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e426e-113">An HPE SaaS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e426e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e426e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e426e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e426e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e426e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e426e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e426e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e426e-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e426e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e426e-118">Scenario description</span></span>
<span data-ttu-id="e426e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e426e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e426e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e426e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e426e-121">Dodawanie HPE SaaS z galerii</span><span class="sxs-lookup"><span data-stu-id="e426e-121">Adding HPE SaaS from the gallery</span></span>
2. <span data-ttu-id="e426e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e426e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-the-gallery"></a><span data-ttu-id="e426e-123">Dodawanie HPE SaaS z galerii</span><span class="sxs-lookup"><span data-stu-id="e426e-123">Adding HPE SaaS from the gallery</span></span>
<span data-ttu-id="e426e-124">Aby skonfigurować integrację usługi Azure AD HPE SaaS, należy dodać HPE SaaS z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e426e-124">To configure the integration of HPE SaaS into Azure AD, you need to add HPE SaaS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e426e-125">**Aby dodać HPE SaaS z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e426e-125">**To add HPE SaaS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e426e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e426e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e426e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e426e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e426e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e426e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e426e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e426e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e426e-133">W polu wyszukiwania wpisz **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="e426e-133">In the search box, type **HPE SaaS**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_search.png)

5. <span data-ttu-id="e426e-135">W panelu wyników wybierz **HPE SaaS**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e426e-135">In the results panel, select **HPE SaaS**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e426e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e426e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e426e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SaaS HPE w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e426e-138">In this section, you configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e426e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednik w modelu SaaS HPE jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e426e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HPE SaaS is to a user in Azure AD.</span></span> <span data-ttu-id="e426e-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w modelu SaaS HPE musi się.</span><span class="sxs-lookup"><span data-stu-id="e426e-140">In other words, a link relationship between an Azure AD user and the related user in HPE SaaS needs to be established.</span></span>

<span data-ttu-id="e426e-141">W modelu SaaS HPE, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e426e-141">In HPE SaaS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e426e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HPE SaaS, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e426e-142">To configure and test Azure AD single sign-on with HPE SaaS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e426e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e426e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e426e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e426e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e426e-145">**[Tworzenie użytkownika testowego HPE SaaS](#creating-an-hpe-saas-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SaaS HPE, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e426e-145">**[Creating an HPE SaaS test user](#creating-an-hpe-saas-test-user)** - to have a counterpart of Britta Simon in HPE SaaS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e426e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e426e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e426e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e426e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e426e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e426e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e426e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="e426e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="e426e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z HPE SaaS, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e426e-150">**To configure Azure AD single sign-on with HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="e426e-151">W portalu Azure na **HPE SaaS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e426e-151">In the Azure portal, on the **HPE SaaS** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e426e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e426e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_samlbase.png)

3. <span data-ttu-id="e426e-155">Na **HPE SaaS domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e426e-155">On the **HPE SaaS Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_url.png)

    <span data-ttu-id="e426e-157">a.</span><span class="sxs-lookup"><span data-stu-id="e426e-157">a.</span></span> <span data-ttu-id="e426e-158">W **adres URL logowania** tekstowym, wpisz adres URL jako:`https://login.saas.hpe.com/msg`</span><span class="sxs-lookup"><span data-stu-id="e426e-158">In the **Sign-on URL** textbox, type a URL as: `https://login.saas.hpe.com/msg`</span></span>

    <span data-ttu-id="e426e-159">b.</span><span class="sxs-lookup"><span data-stu-id="e426e-159">b.</span></span> <span data-ttu-id="e426e-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.saas.hpe.com`</span><span class="sxs-lookup"><span data-stu-id="e426e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.saas.hpe.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e426e-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e426e-161">These values are not real.</span></span> <span data-ttu-id="e426e-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e426e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e426e-163">Skontaktuj się z [zespołem pomocy technicznej klienta SaaS HPE](https://saas.hpe.com/en-us/contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e426e-163">Contact [HPE SaaS Client support team](https://saas.hpe.com/en-us/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="e426e-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e426e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_certificate.png) 

5. <span data-ttu-id="e426e-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e426e-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e426e-168">Skonfigurować logowanie jednokrotne w **HPE SaaS** stronie, musisz wysłać pobrany **XML metadanych** do [HPE SaaS obsługuje zespołu](https://saas.hpe.com/en-us/contact).</span><span class="sxs-lookup"><span data-stu-id="e426e-168">To configure single sign-on on **HPE SaaS** side, you need to send the downloaded **Metadata XML** to [HPE SaaS support team](https://saas.hpe.com/en-us/contact).</span></span> <span data-ttu-id="e426e-169">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="e426e-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e426e-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e426e-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e426e-171">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e426e-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e426e-172">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e426e-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e426e-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e426e-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="e426e-174">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e426e-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e426e-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e426e-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e426e-177">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e426e-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e426e-179">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e426e-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e426e-181">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e426e-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e426e-183">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e426e-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e426e-185">a.</span><span class="sxs-lookup"><span data-stu-id="e426e-185">a.</span></span> <span data-ttu-id="e426e-186">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e426e-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e426e-187">b.</span><span class="sxs-lookup"><span data-stu-id="e426e-187">b.</span></span> <span data-ttu-id="e426e-188">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e426e-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e426e-189">c.</span><span class="sxs-lookup"><span data-stu-id="e426e-189">c.</span></span> <span data-ttu-id="e426e-190">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e426e-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e426e-191">d.</span><span class="sxs-lookup"><span data-stu-id="e426e-191">d.</span></span> <span data-ttu-id="e426e-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e426e-192">Click **Create**.</span></span>
 
### <a name="creating-an-hpe-saas-test-user"></a><span data-ttu-id="e426e-193">Tworzenie użytkownika testowego HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="e426e-193">Creating an HPE SaaS test user</span></span>

<span data-ttu-id="e426e-194">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="e426e-194">The objective of this section is to create a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="e426e-195">We współpracy z [HPE SaaS obsługuje zespołu](https://saas.hpe.com/en-us/contact) Aby dodać użytkowników w ramach konta HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="e426e-195">Please work with [HPE SaaS support team](https://saas.hpe.com/en-us/contact) to add the users in the HPE SaaS account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e426e-196">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e426e-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e426e-197">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="e426e-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HPE SaaS.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e426e-199">**Aby przypisać Simona Britta HPE SaaS, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e426e-199">**To assign Britta Simon to HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="e426e-200">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e426e-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e426e-202">Na liście aplikacji zaznacz **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="e426e-202">In the applications list, select **HPE SaaS**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_app.png) 

3. <span data-ttu-id="e426e-204">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e426e-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e426e-206">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e426e-206">Click **Add** button.</span></span> <span data-ttu-id="e426e-207">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e426e-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e426e-209">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e426e-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e426e-210">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e426e-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e426e-211">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e426e-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e426e-212">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e426e-212">Testing single sign-on</span></span>

<span data-ttu-id="e426e-213">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e426e-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e426e-214">Po kliknięciu kafelka HPE SaaS w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="e426e-214">When you click the HPE SaaS tile in the Access Panel, you should get automatically signed-on to your HPE SaaS application.</span></span>
<span data-ttu-id="e426e-215">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e426e-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e426e-216">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e426e-216">Additional resources</span></span>

* [<span data-ttu-id="e426e-217">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e426e-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e426e-218">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e426e-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png

