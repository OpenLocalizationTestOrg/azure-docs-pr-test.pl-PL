---
title: 'Samouczek: Integracji Azure Active Directory z Weekdone | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Weekdone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34921f9a-5637-4420-ab4c-9beb34421909
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 84aa0069dce55a6623398a99e1cac6bb21bf52f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-weekdone"></a><span data-ttu-id="a8e76-103">Samouczek: Integracji Azure Active Directory z Weekdone</span><span class="sxs-lookup"><span data-stu-id="a8e76-103">Tutorial: Azure Active Directory integration with Weekdone</span></span>

<span data-ttu-id="a8e76-104">Z tego samouczka dowiesz się integrowanie Weekdone z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8e76-104">In this tutorial, you learn how to integrate Weekdone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8e76-105">Integracja z usługą Azure AD Weekdone zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a8e76-105">Integrating Weekdone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8e76-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Weekdone</span><span class="sxs-lookup"><span data-stu-id="a8e76-106">You can control in Azure AD who has access to Weekdone</span></span>
- <span data-ttu-id="a8e76-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Weekdone (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8e76-107">You can enable your users to automatically get signed-on to Weekdone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8e76-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a8e76-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8e76-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8e76-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8e76-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a8e76-110">Prerequisites</span></span>

<span data-ttu-id="a8e76-111">Aby skonfigurować integrację usługi Azure AD z Weekdone, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a8e76-111">To configure Azure AD integration with Weekdone, you need the following items:</span></span>

- <span data-ttu-id="a8e76-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8e76-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8e76-113">Weekdone logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a8e76-113">A Weekdone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8e76-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a8e76-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8e76-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a8e76-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8e76-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a8e76-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8e76-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8e76-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8e76-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a8e76-118">Scenario description</span></span>
<span data-ttu-id="a8e76-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a8e76-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8e76-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a8e76-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8e76-121">Dodawanie Weekdone z galerii</span><span class="sxs-lookup"><span data-stu-id="a8e76-121">Adding Weekdone from the gallery</span></span>
2. <span data-ttu-id="a8e76-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a8e76-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-weekdone-from-the-gallery"></a><span data-ttu-id="a8e76-123">Dodawanie Weekdone z galerii</span><span class="sxs-lookup"><span data-stu-id="a8e76-123">Adding Weekdone from the gallery</span></span>
<span data-ttu-id="a8e76-124">Aby skonfigurować integrację usługi Azure AD Weekdone, należy dodać Weekdone z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a8e76-124">To configure the integration of Weekdone into Azure AD, you need to add Weekdone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8e76-125">**Aby dodać Weekdone z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a8e76-125">**To add Weekdone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8e76-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a8e76-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a8e76-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8e76-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a8e76-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a8e76-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a8e76-133">W polu wyszukiwania wpisz **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-133">In the search box, type **Weekdone**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_search.png)

5. <span data-ttu-id="a8e76-135">W panelu wyników wybierz **Weekdone**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a8e76-135">In the results panel, select **Weekdone**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8e76-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a8e76-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a8e76-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Weekdone w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a8e76-138">In this section, you configure and test Azure AD single sign-on with Weekdone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a8e76-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Weekdone jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8e76-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Weekdone is to a user in Azure AD.</span></span> <span data-ttu-id="a8e76-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Weekdone musi się.</span><span class="sxs-lookup"><span data-stu-id="a8e76-140">In other words, a link relationship between an Azure AD user and the related user in Weekdone needs to be established.</span></span>

<span data-ttu-id="a8e76-141">W Weekdone, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="a8e76-141">In Weekdone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a8e76-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Weekdone, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a8e76-142">To configure and test Azure AD single sign-on with Weekdone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8e76-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a8e76-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8e76-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a8e76-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8e76-145">**[Tworzenie użytkownika testowego Weekdone](#creating-a-weekdone-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Weekdone połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a8e76-145">**[Creating a Weekdone test user](#creating-a-weekdone-test-user)** - to have a counterpart of Britta Simon in Weekdone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8e76-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a8e76-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8e76-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a8e76-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8e76-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a8e76-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8e76-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Weekdone.</span><span class="sxs-lookup"><span data-stu-id="a8e76-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Weekdone application.</span></span>

<span data-ttu-id="a8e76-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Weekdone, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a8e76-150">**To configure Azure AD single sign-on with Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="a8e76-151">W portalu Azure na **Weekdone** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-151">In the Azure portal, on the **Weekdone** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a8e76-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="a8e76-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_samlbase.png)

3. <span data-ttu-id="a8e76-155">Na **Weekdone domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="a8e76-155">On the **Weekdone Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url1.png)

    <span data-ttu-id="a8e76-157">a.</span><span class="sxs-lookup"><span data-stu-id="a8e76-157">a.</span></span> <span data-ttu-id="a8e76-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="a8e76-158">In the **Identifier** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

    <span data-ttu-id="a8e76-159">b.</span><span class="sxs-lookup"><span data-stu-id="a8e76-159">b.</span></span> <span data-ttu-id="a8e76-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="a8e76-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>

4. <span data-ttu-id="a8e76-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a8e76-162">Jeśli chcesz skonfigurować aplikację w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="a8e76-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_url2.png)

    <span data-ttu-id="a8e76-164">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://weekdone.com/a/<tenantname>`</span><span class="sxs-lookup"><span data-stu-id="a8e76-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://weekdone.com/a/<tenantname>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a8e76-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a8e76-165">These values are not real.</span></span> <span data-ttu-id="a8e76-166">Rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="a8e76-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a8e76-167">Skontaktuj się z [zespołem pomocy technicznej klienta Weekdone](mailto:hello@weekdone.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="a8e76-167">Contact [Weekdone Client support team](mailto:hello@weekdone.com) to get these values.</span></span> 

5. <span data-ttu-id="a8e76-168">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a8e76-168">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_certificate.png) 

6. <span data-ttu-id="a8e76-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a8e76-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a8e76-172">Na **konfiguracji Weekdone** , kliknij przycisk **skonfigurować Weekdone** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a8e76-172">On the **Weekdone Configuration** section, click **Configure Weekdone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a8e76-173">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="a8e76-173">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_configure.png) 

8. <span data-ttu-id="a8e76-175">Aby skonfigurować logowanie jednokrotne w **Weekdone** stronie, musisz wysłać pobrany **XML metadanych, adres URL Sign-Out identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [Weekdone zespołem pomocy technicznej ](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="a8e76-175">To configure single sign-on on **Weekdone** side, you need to send the downloaded **Metadata XML, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Weekdone support team](mailto:hello@weekdone.com).</span></span>

> [!TIP]
> <span data-ttu-id="a8e76-176">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="a8e76-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a8e76-177">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="a8e76-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8e76-178">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a8e76-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8e76-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8e76-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8e76-180">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a8e76-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a8e76-182">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a8e76-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8e76-183">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a8e76-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8e76-185">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8e76-187">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a8e76-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8e76-189">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a8e76-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-weekdone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8e76-191">a.</span><span class="sxs-lookup"><span data-stu-id="a8e76-191">a.</span></span> <span data-ttu-id="a8e76-192">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8e76-193">b.</span><span class="sxs-lookup"><span data-stu-id="a8e76-193">b.</span></span> <span data-ttu-id="a8e76-194">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a8e76-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8e76-195">c.</span><span class="sxs-lookup"><span data-stu-id="a8e76-195">c.</span></span> <span data-ttu-id="a8e76-196">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8e76-197">d.</span><span class="sxs-lookup"><span data-stu-id="a8e76-197">d.</span></span> <span data-ttu-id="a8e76-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-198">Click **Create**.</span></span>
 
### <a name="creating-a-weekdone-test-user"></a><span data-ttu-id="a8e76-199">Tworzenie użytkownika testowego Weekdone</span><span class="sxs-lookup"><span data-stu-id="a8e76-199">Creating a Weekdone test user</span></span>

<span data-ttu-id="a8e76-200">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Weekdone.</span><span class="sxs-lookup"><span data-stu-id="a8e76-200">The objective of this section is to create a user called Britta Simon in Weekdone.</span></span> <span data-ttu-id="a8e76-201">Weekdone obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="a8e76-201">Weekdone supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a8e76-202">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a8e76-202">There is no action item for you in this section.</span></span> <span data-ttu-id="a8e76-203">Nowy użytkownik został utworzony podczas próby dostępu Weekdone, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="a8e76-203">A new user is created during an attempt to access Weekdone if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a8e76-204">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [zespołem pomocy technicznej klienta Weekdone](mailto:hello@weekdone.com).</span><span class="sxs-lookup"><span data-stu-id="a8e76-204">If you need to create a user manually, you need to contact the [Weekdone Client support team](mailto:hello@weekdone.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8e76-205">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8e76-205">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8e76-206">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Weekdone.</span><span class="sxs-lookup"><span data-stu-id="a8e76-206">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Weekdone.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a8e76-208">**Aby przypisać Simona Britta Weekdone, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a8e76-208">**To assign Britta Simon to Weekdone, perform the following steps:**</span></span>

1. <span data-ttu-id="a8e76-209">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-209">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a8e76-211">Na liście aplikacji zaznacz **Weekdone**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-211">In the applications list, select **Weekdone**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-weekdone-tutorial/tutorial_weekdone_app.png) 

3. <span data-ttu-id="a8e76-213">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a8e76-213">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a8e76-215">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a8e76-215">Click **Add** button.</span></span> <span data-ttu-id="a8e76-216">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a8e76-216">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a8e76-218">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="a8e76-218">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8e76-219">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a8e76-219">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8e76-220">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a8e76-220">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8e76-221">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a8e76-221">Testing single sign-on</span></span>

<span data-ttu-id="a8e76-222">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a8e76-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a8e76-223">Po kliknięciu kafelka Weekdone w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Weekdone.</span><span class="sxs-lookup"><span data-stu-id="a8e76-223">When you click the Weekdone tile in the Access Panel, you should get automatically signed-on to your Weekdone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8e76-224">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a8e76-224">Additional resources</span></span>

* [<span data-ttu-id="a8e76-225">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8e76-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8e76-226">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a8e76-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-weekdone-tutorial/tutorial_general_203.png

