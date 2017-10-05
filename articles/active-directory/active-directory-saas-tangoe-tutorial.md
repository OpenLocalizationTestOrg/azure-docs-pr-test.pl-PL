---
title: 'Samouczek: Integracji Azure Active Directory z Tangoe polecenia Premium Mobile | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Tangoe polecenie Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 595541e7248a7486e58123927389c552af0e50f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="6a4b7-103">Samouczek: Integracji Azure Active Directory z Tangoe polecenia Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="6a4b7-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="6a4b7-104">Z tego samouczka dowiesz się integrowanie Tangoe polecenia Premium Mobile w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a4b7-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a4b7-105">Integracja z usługą Azure AD Tangoe polecenia Premium Mobile zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6a4b7-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6a4b7-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Tangoe polecenia Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="6a4b7-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
- <span data-ttu-id="6a4b7-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Tangoe polecenia Premium powyżej (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a4b7-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a4b7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6a4b7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6a4b7-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a4b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a4b7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6a4b7-110">Prerequisites</span></span>

<span data-ttu-id="6a4b7-111">Aby skonfigurować integrację usługi Azure AD z Tangoe polecenia Premium Mobile, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6a4b7-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

- <span data-ttu-id="6a4b7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a4b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a4b7-113">Mobile Premium polecenia Tangoe logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6a4b7-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a4b7-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a4b7-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6a4b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a4b7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a4b7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a4b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a4b7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6a4b7-118">Scenario description</span></span>
<span data-ttu-id="6a4b7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a4b7-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6a4b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a4b7-121">Dodaj Mobile Premium polecenie Tangoe z galerii</span><span class="sxs-lookup"><span data-stu-id="6a4b7-121">Add Tangoe Command Premium Mobile from the gallery</span></span>
2. <span data-ttu-id="6a4b7-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6a4b7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="6a4b7-123">Dodaj Mobile Premium polecenie Tangoe z galerii</span><span class="sxs-lookup"><span data-stu-id="6a4b7-123">Add Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="6a4b7-124">Aby skonfigurować integrację Tangoe polecenia Premium Mobile w usłudze Azure Active Directory, należy dodać Mobile Premium polecenie Tangoe z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6a4b7-125">**Aby dodać Mobile Premium polecenie Tangoe z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6a4b7-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6a4b7-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6a4b7-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6a4b7-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6a4b7-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6a4b7-133">W polu wyszukiwania wpisz **Tangoe polecenia Premium Mobile**, wybierz pozycję **Tangoe polecenia Premium Mobile** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span></span>

    ![<span data-ttu-id="6a4b7-134">Dodaj Mobile Premium polecenie Tangoe z galerii</span><span class="sxs-lookup"><span data-stu-id="6a4b7-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6a4b7-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6a4b7-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="6a4b7-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mobile Premium polecenia Tangoe w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6a4b7-137">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w Tangoe polecenia Premium Mobile do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="6a4b7-138">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Tangoe polecenia Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="6a4b7-139">W Tangoe polecenia Premium urządzeń przenośnych, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6a4b7-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Tangoe polecenia Premium Mobile, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6a4b7-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6a4b7-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6a4b7-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a4b7-143">**[Tworzenie użytkownika testowego Mobile Premium polecenia Tangoe](#create-a-tangoe-command-premium-mobile-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Tangoe polecenia Premium Mobile połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a4b7-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a4b7-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6a4b7-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6a4b7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6a4b7-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji mobilnych — wersja Premium polecenia Tangoe.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="6a4b7-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Tangoe polecenia Premium Mobile, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6a4b7-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="6a4b7-149">W portalu Azure na **Tangoe polecenia Premium Mobile** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6a4b7-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="6a4b7-153">Na **Tangoe polecenia Premium Mobile domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6a4b7-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span></span>

    ![Polecenie Tangoe Premium przenośnych domeny i adres URL](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="6a4b7-155">a.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-155">a.</span></span> <span data-ttu-id="6a4b7-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="6a4b7-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="6a4b7-157">b.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-157">b.</span></span> <span data-ttu-id="6a4b7-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="6a4b7-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a4b7-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-159">These values are not real.</span></span> <span data-ttu-id="6a4b7-160">Rzeczywisty adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-160">Update these values with the actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="6a4b7-161">Skontaktuj się z [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to get these values.</span></span> 

4. <span data-ttu-id="6a4b7-162">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="6a4b7-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-164">Click **Save** button.</span></span>

    ![Przyciskiem Zapisz](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="6a4b7-166">Na **Tangoe polecenia Premium Mobile konfiguracji** , kliknij przycisk **skonfigurować Mobile Premium polecenia Tangoe** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6a4b7-167">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6a4b7-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Sekcja konfiguracji Mobile Premium polecenia Tangoe](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="6a4b7-169">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z z [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) i zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6a4b7-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide the following:</span></span>

   - <span data-ttu-id="6a4b7-170">Plik metadanych pobranych</span><span class="sxs-lookup"><span data-stu-id="6a4b7-170">The downloaded metadata file</span></span>
   - <span data-ttu-id="6a4b7-171">**Identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="6a4b7-171">The **SAML Entity ID**</span></span>
   - <span data-ttu-id="6a4b7-172">**Adres URL usługi rejestracji jednokrotnej SAML**</span><span class="sxs-lookup"><span data-stu-id="6a4b7-172">The **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="6a4b7-173">**Adresu URL wylogowania**</span><span class="sxs-lookup"><span data-stu-id="6a4b7-173">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="6a4b7-174">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="6a4b7-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6a4b7-175">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6a4b7-176">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a4b7-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6a4b7-177">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a4b7-177">Create an Azure AD test user</span></span>
<span data-ttu-id="6a4b7-178">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6a4b7-180">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6a4b7-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6a4b7-181">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a4b7-183">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a4b7-185">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Dodawanie użytkownika](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a4b7-187">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6a4b7-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Strony okna dialogowego użytkownika](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a4b7-189">a.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-189">a.</span></span> <span data-ttu-id="6a4b7-190">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a4b7-191">b.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-191">b.</span></span> <span data-ttu-id="6a4b7-192">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a4b7-193">c.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-193">c.</span></span> <span data-ttu-id="6a4b7-194">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6a4b7-195">d.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-195">d.</span></span> <span data-ttu-id="6a4b7-196">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="6a4b7-197">Tworzenie użytkownika testowego Tangoe polecenia Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="6a4b7-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="6a4b7-198">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Tangoe polecenia Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="6a4b7-199">Aplikacji mobilnych — wersja Premium polecenia Tangoe musi wszystkich użytkowników na potrzeby aprowizacji w aplikacji przed wykonaniem rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="6a4b7-200">Pracy, dlatego należy z [zespołem pomocy technicznej klienta Mobile Premium polecenia Tangoe](https://www.tangoe.com/contact-2/) do udostępnienia tych użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to provision all these users into the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6a4b7-201">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a4b7-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="6a4b7-202">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Tangoe polecenia Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6a4b7-204">**Aby przypisać Simona Britta Tangoe polecenia Premium Mobile, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6a4b7-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="6a4b7-205">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6a4b7-207">Na liście aplikacji zaznacz **Tangoe polecenia Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-207">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe polecenia Premium Mobile listy aplikacji](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="6a4b7-209">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6a4b7-211">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-211">Click **Add** button.</span></span> <span data-ttu-id="6a4b7-212">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6a4b7-214">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6a4b7-215">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a4b7-216">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6a4b7-217">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6a4b7-217">Test single sign-on</span></span>

<span data-ttu-id="6a4b7-218">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6a4b7-219">Po kliknięciu kafelka Tangoe polecenia Premium Mobile w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji mobilnych — wersja Premium polecenia Tangoe.</span><span class="sxs-lookup"><span data-stu-id="6a4b7-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="6a4b7-220">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6a4b7-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6a4b7-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6a4b7-221">Additional resources</span></span>

* [<span data-ttu-id="6a4b7-222">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a4b7-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a4b7-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6a4b7-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

