---
title: 'Samouczek: Integracji Azure Active Directory z AnswerHub | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="48a3d-103">Samouczek: Integracji Azure Active Directory z AnswerHub</span><span class="sxs-lookup"><span data-stu-id="48a3d-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="48a3d-104">Z tego samouczka dowiesz się integrowanie AnswerHub z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48a3d-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48a3d-105">Integracja z usługą Azure AD AnswerHub zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="48a3d-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48a3d-106">Można kontrolować w usłudze Azure AD, który ma dostęp do AnswerHub</span><span class="sxs-lookup"><span data-stu-id="48a3d-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="48a3d-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do AnswerHub (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="48a3d-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48a3d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="48a3d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48a3d-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48a3d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48a3d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="48a3d-110">Prerequisites</span></span>

<span data-ttu-id="48a3d-111">Aby skonfigurować integrację usługi Azure AD z AnswerHub, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="48a3d-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="48a3d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="48a3d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48a3d-113">AnswerHub logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="48a3d-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48a3d-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="48a3d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48a3d-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="48a3d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48a3d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="48a3d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48a3d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48a3d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48a3d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="48a3d-118">Scenario description</span></span>
<span data-ttu-id="48a3d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="48a3d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48a3d-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="48a3d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48a3d-121">Dodawanie AnswerHub z galerii</span><span class="sxs-lookup"><span data-stu-id="48a3d-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="48a3d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="48a3d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="48a3d-123">Dodawanie AnswerHub z galerii</span><span class="sxs-lookup"><span data-stu-id="48a3d-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="48a3d-124">Aby skonfigurować integrację usługi Azure AD AnswerHub, należy dodać AnswerHub z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="48a3d-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48a3d-125">**Aby dodać AnswerHub z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="48a3d-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48a3d-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="48a3d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="48a3d-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48a3d-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="48a3d-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48a3d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="48a3d-133">W polu wyszukiwania wpisz **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-133">In the search box, type **AnswerHub**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="48a3d-135">W panelu wyników wybierz **AnswerHub**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="48a3d-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48a3d-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="48a3d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48a3d-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AnswerHub w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="48a3d-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48a3d-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w AnswerHub jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48a3d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="48a3d-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w AnswerHub musi się.</span><span class="sxs-lookup"><span data-stu-id="48a3d-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="48a3d-141">W AnswerHub, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="48a3d-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48a3d-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AnswerHub, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="48a3d-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48a3d-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="48a3d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48a3d-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="48a3d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48a3d-145">**[Tworzenie użytkownika testowego AnswerHub](#creating-an-answerhub-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta AnswerHub połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="48a3d-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48a3d-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="48a3d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48a3d-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="48a3d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48a3d-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="48a3d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48a3d-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="48a3d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="48a3d-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z AnswerHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="48a3d-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="48a3d-151">W portalu Azure na **AnswerHub** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="48a3d-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="48a3d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="48a3d-155">Na **AnswerHub domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="48a3d-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="48a3d-157">a.</span><span class="sxs-lookup"><span data-stu-id="48a3d-157">a.</span></span> <span data-ttu-id="48a3d-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="48a3d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="48a3d-159">b.</span><span class="sxs-lookup"><span data-stu-id="48a3d-159">b.</span></span> <span data-ttu-id="48a3d-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="48a3d-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48a3d-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="48a3d-161">These values are not real.</span></span> <span data-ttu-id="48a3d-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="48a3d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="48a3d-163">Skontaktuj się z [zespołem pomocy technicznej klienta AnswerHub](mailto:success@answerhub.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="48a3d-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="48a3d-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="48a3d-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="48a3d-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="48a3d-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48a3d-168">Na **konfiguracji AnswerHub** , kliknij przycisk **skonfigurować AnswerHub** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="48a3d-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="48a3d-169">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="48a3d-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="48a3d-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy AnswerHub jako administrator.</span><span class="sxs-lookup"><span data-stu-id="48a3d-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="48a3d-172">Jeśli potrzebujesz pomocy przy konfigurowaniu AnswerHub, skontaktuj się z [zespołem pomocy technicznej firmy AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="48a3d-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="48a3d-173">Przejdź do **administracji**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="48a3d-174">Kliknij przycisk **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="48a3d-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="48a3d-175">W okienku nawigacji po lewej stronie w **społecznościowych ustawienia** kliknij **Instalatora SAML**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="48a3d-176">Kliknij przycisk **IDP Config** kartę.</span><span class="sxs-lookup"><span data-stu-id="48a3d-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="48a3d-177">Na **IDP Config** karcie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="48a3d-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="48a3d-178">![Instalator SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Instalatora SAML")</span><span class="sxs-lookup"><span data-stu-id="48a3d-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="48a3d-179">a.</span><span class="sxs-lookup"><span data-stu-id="48a3d-179">a.</span></span> <span data-ttu-id="48a3d-180">W **adres URL logowania IDP** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="48a3d-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="48a3d-181">b.</span><span class="sxs-lookup"><span data-stu-id="48a3d-181">b.</span></span> <span data-ttu-id="48a3d-182">W **adresu URL wylogowania IDP** pole tekstowe, Wklej **Sign-Out URL** wartość, która została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="48a3d-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="48a3d-183">c.</span><span class="sxs-lookup"><span data-stu-id="48a3d-183">c.</span></span> <span data-ttu-id="48a3d-184">W **Format identyfikatora nazwy IDP** pole tekstowe, wprowadź nazwę użytkownika, wartość identyfikatora sam jako wybrane w portalu Azure w **atrybuty użytkownika** sekcji.</span><span class="sxs-lookup"><span data-stu-id="48a3d-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="48a3d-185">d.</span><span class="sxs-lookup"><span data-stu-id="48a3d-185">d.</span></span> <span data-ttu-id="48a3d-186">Kliknij przycisk **klucze i certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="48a3d-187">Na karcie klucze i certyfikaty wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="48a3d-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="48a3d-188">![Klucze i certyfikaty](./media/active-directory-saas-answerhub-tutorial/ic785173.png "klucze i certyfikaty")</span><span class="sxs-lookup"><span data-stu-id="48a3d-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="48a3d-189">a.</span><span class="sxs-lookup"><span data-stu-id="48a3d-189">a.</span></span> <span data-ttu-id="48a3d-190">Otwórz z zakodowanego certyfikatu base-64, który został pobrany z portalu Azure w programie Notatnik, skopiuj zawartość go do Schowka, a następnie wklej go do **IDP klucza publicznego (x 509 Format)** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="48a3d-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="48a3d-191">b.</span><span class="sxs-lookup"><span data-stu-id="48a3d-191">b.</span></span> <span data-ttu-id="48a3d-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-192">Click **Save**.</span></span>

14. <span data-ttu-id="48a3d-193">Na **IDP Config** , kliknij pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="48a3d-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="48a3d-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48a3d-195">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="48a3d-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48a3d-196">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48a3d-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48a3d-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="48a3d-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="48a3d-198">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="48a3d-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="48a3d-200">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="48a3d-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48a3d-201">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="48a3d-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48a3d-203">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48a3d-205">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48a3d-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48a3d-207">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="48a3d-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48a3d-209">a.</span><span class="sxs-lookup"><span data-stu-id="48a3d-209">a.</span></span> <span data-ttu-id="48a3d-210">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48a3d-211">b.</span><span class="sxs-lookup"><span data-stu-id="48a3d-211">b.</span></span> <span data-ttu-id="48a3d-212">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48a3d-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48a3d-213">c.</span><span class="sxs-lookup"><span data-stu-id="48a3d-213">c.</span></span> <span data-ttu-id="48a3d-214">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48a3d-215">d.</span><span class="sxs-lookup"><span data-stu-id="48a3d-215">d.</span></span> <span data-ttu-id="48a3d-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="48a3d-217">Tworzenie użytkownika testowego AnswerHub</span><span class="sxs-lookup"><span data-stu-id="48a3d-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="48a3d-218">Aby umożliwić użytkownikom usługi Azure AD zalogować się do AnswerHub, musi być przygotowana do AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="48a3d-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="48a3d-219">W przypadku AnswerHub Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="48a3d-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="48a3d-220">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="48a3d-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="48a3d-221">Zaloguj się do Twojego **AnswerHub** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="48a3d-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="48a3d-222">Przejdź do **administracji**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="48a3d-223">Kliknij przycisk **użytkownicy i grupy** kartę.</span><span class="sxs-lookup"><span data-stu-id="48a3d-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="48a3d-224">W okienku nawigacji po lewej stronie w **Zarządzanie użytkownikami** kliknij **Tworzenie lub importowanie użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="48a3d-225">![Użytkownicy i grupy](./media/active-directory-saas-answerhub-tutorial/ic785175.png "użytkownicy i grupy")</span><span class="sxs-lookup"><span data-stu-id="48a3d-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="48a3d-226">Typ **adres E-mail**, **Username** i **hasło** prawidłowe konto usługi Azure Active Directory chcesz udostępnić do powiązanych pól tekstowych, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="48a3d-227">Możesz użyć innych AnswerHub użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez AnswerHub do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="48a3d-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48a3d-228">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="48a3d-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48a3d-229">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="48a3d-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="48a3d-231">**Aby przypisać Simona Britta AnswerHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="48a3d-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="48a3d-232">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="48a3d-234">Na liście aplikacji zaznacz **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-234">In the applications list, select **AnswerHub**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="48a3d-236">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="48a3d-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="48a3d-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="48a3d-238">Click **Add** button.</span></span> <span data-ttu-id="48a3d-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48a3d-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="48a3d-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="48a3d-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48a3d-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48a3d-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48a3d-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="48a3d-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48a3d-244">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="48a3d-244">Testing single sign-on</span></span>

<span data-ttu-id="48a3d-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="48a3d-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48a3d-246">Po kliknięciu kafelka AnswerHub w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="48a3d-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="48a3d-247">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48a3d-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48a3d-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="48a3d-248">Additional resources</span></span>

* [<span data-ttu-id="48a3d-249">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48a3d-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48a3d-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48a3d-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

