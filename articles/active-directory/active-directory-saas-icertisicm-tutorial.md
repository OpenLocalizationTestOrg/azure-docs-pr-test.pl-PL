---
title: "Samouczek: Azure Active Directory Integracja z platformą zarządzania kontraktu Icertis | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i platformy zarządzania Icertis kontraktu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 9dd002f71b7a960338071db869f7c8cf88071342
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="9cfc9-103">Samouczek: Azure Active Directory Integracja z platformą zarządzania Icertis kontraktu</span><span class="sxs-lookup"><span data-stu-id="9cfc9-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="9cfc9-104">Z tego samouczka dowiesz sposobu integracji platformy zarządzania Icertis umowy z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9cfc9-104">In this tutorial, you learn how to integrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cfc9-105">Integracja platformy zarządzania kontraktu Icertis z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9cfc9-105">Integrating Icertis Contract Management Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9cfc9-106">Można kontrolować w usłudze Azure AD, który ma dostęp do platformy zarządzania Icertis kontraktu</span><span class="sxs-lookup"><span data-stu-id="9cfc9-106">You can control in Azure AD who has access to Icertis Contract Management Platform</span></span>
- <span data-ttu-id="9cfc9-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do platformy zarządzania kontraktu Icertis (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cfc9-107">You can enable your users to automatically get signed-on to Icertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cfc9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9cfc9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9cfc9-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cfc9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cfc9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9cfc9-110">Prerequisites</span></span>

<span data-ttu-id="9cfc9-111">Aby skonfigurować integrację usługi Azure AD z platformą zarządzania Icertis kontraktu, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9cfc9-111">To configure Azure AD integration with Icertis Contract Management Platform, you need the following items:</span></span>

- <span data-ttu-id="9cfc9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cfc9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cfc9-113">Platforma zarządzania kontraktu Icertis logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9cfc9-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cfc9-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cfc9-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9cfc9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cfc9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cfc9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cfc9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cfc9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9cfc9-118">Scenario description</span></span>
<span data-ttu-id="9cfc9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cfc9-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9cfc9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cfc9-121">Dodawanie platformy zarządzania kontraktu Icertis z galerii</span><span class="sxs-lookup"><span data-stu-id="9cfc9-121">Adding Icertis Contract Management Platform from the gallery</span></span>
2. <span data-ttu-id="9cfc9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9cfc9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-the-gallery"></a><span data-ttu-id="9cfc9-123">Dodawanie platformy zarządzania kontraktu Icertis z galerii</span><span class="sxs-lookup"><span data-stu-id="9cfc9-123">Adding Icertis Contract Management Platform from the gallery</span></span>
<span data-ttu-id="9cfc9-124">Aby skonfigurować integrację usługi Azure AD platformy zarządzania Icertis kontraktu, należy dodać platformy zarządzania kontraktu Icertis z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-124">To configure the integration of Icertis Contract Management Platform into Azure AD, you need to add Icertis Contract Management Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9cfc9-125">**Aby dodać platformę zarządzania kontraktu Icertis z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9cfc9-125">**To add Icertis Contract Management Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9cfc9-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9cfc9-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9cfc9-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9cfc9-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9cfc9-133">W polu wyszukiwania wpisz **platformy zarządzania kontraktu Icertis**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-133">In the search box, type **Icertis Contract Management Platform**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="9cfc9-135">W panelu wyników wybierz **platformy zarządzania kontraktu Icertis**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-135">In the results panel, select **Icertis Contract Management Platform**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cfc9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9cfc9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cfc9-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z platformą zarządzania kontraktu Icertis w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9cfc9-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem platformy zarządzania kontraktu Icertis jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Icertis Contract Management Platform is to a user in Azure AD.</span></span> <span data-ttu-id="9cfc9-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi na platformie zarządzania kontraktu Icertis musi określone.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-140">In other words, a link relationship between an Azure AD user and the related user in Icertis Contract Management Platform needs to be established.</span></span>

<span data-ttu-id="9cfc9-141">W Icertis kontraktu platformy zarządzania, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-141">In Icertis Contract Management Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9cfc9-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z platformą zarządzania Icertis kontraktu, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9cfc9-142">To configure and test Azure AD single sign-on with Icertis Contract Management Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9cfc9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9cfc9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cfc9-145">**[Tworzenie użytkownika testowego platformy zarządzania kontraktu Icertis](#creating-an-icertis-contract-management-platform-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Icertis kontraktu platformy do zarządzania jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - to have a counterpart of Britta Simon in Icertis Contract Management Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cfc9-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cfc9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cfc9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9cfc9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cfc9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji platformy zarządzania Icertis kontraktu.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="9cfc9-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z platformą zarządzania Icertis kontraktu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9cfc9-150">**To configure Azure AD single sign-on with Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="9cfc9-151">W portalu Azure na **platformy zarządzania kontraktu Icertis** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-151">In the Azure portal, on the **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9cfc9-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="9cfc9-155">Na **adresy URL i domeny platformy zarządzania kontraktu Icertis** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9cfc9-155">On the **Icertis Contract Management Platform Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="9cfc9-157">a.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-157">a.</span></span> <span data-ttu-id="9cfc9-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="9cfc9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="9cfc9-159">b.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-159">b.</span></span> <span data-ttu-id="9cfc9-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="9cfc9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9cfc9-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-161">These values are not real.</span></span> <span data-ttu-id="9cfc9-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9cfc9-163">Skontaktuj się z [zespołem pomocy technicznej klienta platformy zarządzania kontraktu Icertis](https://www.icertis.com/company/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) to get these values.</span></span> 

4. <span data-ttu-id="9cfc9-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="9cfc9-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cfc9-168">Na **konfiguracji platformy zarządzania kontraktu Icertis** , kliknij przycisk **skonfigurować platformę zarządzania kontraktu Icertis** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-168">On the **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9cfc9-169">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9cfc9-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="9cfc9-171">Skonfigurować logowanie jednokrotne w **platformy zarządzania kontraktu Icertis** stronie, musisz wysłać pobrany **XML metadanych** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [zespołem pomocy technicznej platformy zarządzania kontraktu Icertis](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="9cfc9-171">To configure single sign-on on **Icertis Contract Management Platform** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="9cfc9-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9cfc9-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9cfc9-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9cfc9-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cfc9-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cfc9-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cfc9-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cfc9-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9cfc9-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9cfc9-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9cfc9-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cfc9-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cfc9-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cfc9-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9cfc9-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cfc9-187">a.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-187">a.</span></span> <span data-ttu-id="9cfc9-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cfc9-189">b.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-189">b.</span></span> <span data-ttu-id="9cfc9-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cfc9-191">c.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-191">c.</span></span> <span data-ttu-id="9cfc9-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9cfc9-193">d.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-193">d.</span></span> <span data-ttu-id="9cfc9-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="9cfc9-195">Tworzenie użytkownika testowego platformy zarządzania Icertis kontraktu</span><span class="sxs-lookup"><span data-stu-id="9cfc9-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="9cfc9-196">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta Icertis kontraktu zarządzania platformy.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="9cfc9-197">We współpracy z [zespołem pomocy technicznej platformy zarządzania kontraktu Icertis](https://www.icertis.com/company/contact/) Aby dodać użytkowników platformy zarządzania Icertis kontraktu.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) to add the users in the Icertis Contract Management Platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9cfc9-198">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cfc9-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9cfc9-199">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do platformy zarządzania Icertis kontraktu.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Icertis Contract Management Platform.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9cfc9-201">**Aby przypisać Simona Britta platformy zarządzania Icertis kontraktu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9cfc9-201">**To assign Britta Simon to Icertis Contract Management Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="9cfc9-202">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9cfc9-204">Na liście aplikacji zaznacz **platformy zarządzania kontraktu Icertis**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-204">In the applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="9cfc9-206">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9cfc9-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-208">Click **Add** button.</span></span> <span data-ttu-id="9cfc9-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9cfc9-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9cfc9-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cfc9-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cfc9-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9cfc9-214">Testing single sign-on</span></span>

<span data-ttu-id="9cfc9-215">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-215">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="9cfc9-216">Po kliknięciu kafelka platformy zarządzania Icertis kontraktu w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji platformy zarządzania Icertis kontraktu.</span><span class="sxs-lookup"><span data-stu-id="9cfc9-216">When you click the Icertis Contract Management Platform tile in the Access Panel, you should get automatically signed-on to your Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cfc9-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9cfc9-217">Additional resources</span></span>

* [<span data-ttu-id="9cfc9-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cfc9-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cfc9-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cfc9-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

