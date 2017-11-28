---
title: 'Samouczek: Integracji Azure Active Directory z GaggleAMP | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: c591cf99aecc4153e378c42a530b80deeca63158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="af2e6-103">Samouczek: Integracji Azure Active Directory z GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="af2e6-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="af2e6-104">Z tego samouczka dowiesz się integrowanie GaggleAMP z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="af2e6-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="af2e6-105">Integracja z usługą Azure AD GaggleAMP zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="af2e6-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="af2e6-106">Można kontrolować w usłudze Azure AD, który ma dostęp do GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="af2e6-106">You can control in Azure AD who has access to GaggleAMP</span></span>
- <span data-ttu-id="af2e6-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do GaggleAMP (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2e6-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="af2e6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="af2e6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="af2e6-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af2e6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af2e6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="af2e6-110">Prerequisites</span></span>

<span data-ttu-id="af2e6-111">Aby skonfigurować integrację usługi Azure AD z GaggleAMP, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="af2e6-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

- <span data-ttu-id="af2e6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2e6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="af2e6-113">GaggleAMP jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="af2e6-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="af2e6-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="af2e6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="af2e6-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="af2e6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="af2e6-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="af2e6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="af2e6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="af2e6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="af2e6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="af2e6-118">Scenario description</span></span>
<span data-ttu-id="af2e6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="af2e6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="af2e6-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="af2e6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="af2e6-121">Dodawanie GaggleAMP z galerii</span><span class="sxs-lookup"><span data-stu-id="af2e6-121">Adding GaggleAMP from the gallery</span></span>
2. <span data-ttu-id="af2e6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="af2e6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-the-gallery"></a><span data-ttu-id="af2e6-123">Dodawanie GaggleAMP z galerii</span><span class="sxs-lookup"><span data-stu-id="af2e6-123">Adding GaggleAMP from the gallery</span></span>
<span data-ttu-id="af2e6-124">Aby skonfigurować integrację usługi Azure AD GaggleAMP, należy dodać GaggleAMP z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="af2e6-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="af2e6-125">**Aby dodać GaggleAMP z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="af2e6-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="af2e6-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="af2e6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="af2e6-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="af2e6-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="af2e6-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="af2e6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="af2e6-133">W polu wyszukiwania wpisz **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-133">In the search box, type **GaggleAMP**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="af2e6-135">W panelu wyników wybierz **GaggleAMP**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="af2e6-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="af2e6-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="af2e6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="af2e6-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z GaggleAMP w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="af2e6-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="af2e6-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w GaggleAMP jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="af2e6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span></span> <span data-ttu-id="af2e6-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w GaggleAMP musi się.</span><span class="sxs-lookup"><span data-stu-id="af2e6-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="af2e6-141">W GaggleAMP, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="af2e6-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="af2e6-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z GaggleAMP, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="af2e6-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="af2e6-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="af2e6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="af2e6-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="af2e6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="af2e6-145">**[Tworzenie użytkownika testowego GaggleAMP](#creating-a-gaggleamp-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta GaggleAMP połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="af2e6-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="af2e6-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="af2e6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="af2e6-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="af2e6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="af2e6-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="af2e6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="af2e6-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="af2e6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="af2e6-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z GaggleAMP, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="af2e6-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="af2e6-151">W portalu Azure na **GaggleAMP** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="af2e6-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="af2e6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="af2e6-155">Na **GaggleAMP domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="af2e6-155">On the **GaggleAMP Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="af2e6-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="af2e6-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="af2e6-158">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="af2e6-158">The value is not real.</span></span> <span data-ttu-id="af2e6-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="af2e6-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="af2e6-160">Skontaktuj się z [zespołem pomocy technicznej klienta GaggleAMP](mailto:sales@gaggleamp.com) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="af2e6-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get the value.</span></span> 
 
4. <span data-ttu-id="af2e6-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="af2e6-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="af2e6-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="af2e6-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="af2e6-165">Na **konfiguracji GaggleAMP** , kliknij przycisk **skonfigurować GaggleAMP** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="af2e6-165">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="af2e6-166">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="af2e6-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="af2e6-168">W innym wystąpieniu przeglądarki, przejdź do strony logowania jednokrotnego SAML utworzone przez Gaggle obsługuje team (na przykład: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="af2e6-168">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="af2e6-169">W Twojej **logowania jednokrotnego SAML** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="af2e6-169">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![GaggleAMP rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="af2e6-171">a.</span><span class="sxs-lookup"><span data-stu-id="af2e6-171">a.</span></span> <span data-ttu-id="af2e6-172">W **wystawcy dostawcy tożsamości** pole tekstowe, Wklej wartość **adres URL wystawcy** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="af2e6-172">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="af2e6-173">b.</span><span class="sxs-lookup"><span data-stu-id="af2e6-173">b.</span></span> <span data-ttu-id="af2e6-174">W **tożsamości dostawcy pojedynczy adres URL logowania** pole tekstowe, Wklej wartość **pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="af2e6-174">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="af2e6-175">c.</span><span class="sxs-lookup"><span data-stu-id="af2e6-175">c.</span></span> <span data-ttu-id="af2e6-176">Kliknij przycisk **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="af2e6-176">Click **Save**</span></span>      

    <span data-ttu-id="af2e6-177">d.</span><span class="sxs-lookup"><span data-stu-id="af2e6-177">d.</span></span> <span data-ttu-id="af2e6-178">Wyślij **certyfikatu (Base64)** z certyfikatów z [zespołem pomocy technicznej GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="af2e6-178">Send the **Certificate (Base64)** certificate to your [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="af2e6-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="af2e6-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="af2e6-180">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="af2e6-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="af2e6-181">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="af2e6-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="af2e6-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2e6-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="af2e6-183">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="af2e6-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="af2e6-185">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="af2e6-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="af2e6-186">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="af2e6-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="af2e6-188">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="af2e6-190">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="af2e6-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="af2e6-192">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="af2e6-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="af2e6-194">a.</span><span class="sxs-lookup"><span data-stu-id="af2e6-194">a.</span></span> <span data-ttu-id="af2e6-195">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="af2e6-196">b.</span><span class="sxs-lookup"><span data-stu-id="af2e6-196">b.</span></span> <span data-ttu-id="af2e6-197">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="af2e6-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="af2e6-198">c.</span><span class="sxs-lookup"><span data-stu-id="af2e6-198">c.</span></span> <span data-ttu-id="af2e6-199">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="af2e6-200">d.</span><span class="sxs-lookup"><span data-stu-id="af2e6-200">d.</span></span> <span data-ttu-id="af2e6-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="af2e6-202">Tworzenie użytkownika testowego GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="af2e6-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="af2e6-203">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="af2e6-203">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="af2e6-204">GaggleAMP obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="af2e6-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="af2e6-205">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="af2e6-205">There is no action item for you in this section.</span></span> <span data-ttu-id="af2e6-206">Nowy użytkownik został utworzony podczas próby dostępu GaggleAMP, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="af2e6-206">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="af2e6-207">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="af2e6-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="af2e6-208">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="af2e6-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="af2e6-210">**Aby przypisać Simona Britta GaggleAMP, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="af2e6-210">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="af2e6-211">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="af2e6-213">Na liście aplikacji zaznacz **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-213">In the applications list, select **GaggleAMP**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="af2e6-215">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="af2e6-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="af2e6-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="af2e6-217">Click **Add** button.</span></span> <span data-ttu-id="af2e6-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="af2e6-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="af2e6-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="af2e6-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="af2e6-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="af2e6-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="af2e6-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="af2e6-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="af2e6-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="af2e6-223">Testing single sign-on</span></span>

<span data-ttu-id="af2e6-224">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="af2e6-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="af2e6-225">Po kliknięciu kafelka GaggleAMP w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="af2e6-225">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af2e6-226">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="af2e6-226">Additional resources</span></span>

* [<span data-ttu-id="af2e6-227">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af2e6-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="af2e6-228">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="af2e6-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

