---
title: 'Samouczek: Integracji Azure Active Directory z TigerText Secure Messenger | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i TigerText Secure Messenger."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="09b3c-103">Samouczek: Integracji Azure Active Directory z TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="09b3c-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="09b3c-104">W tym samouczku Dowiedz się integrowanie TigerText Secure Messenger z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09b3c-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09b3c-105">Integracja z usługą Azure AD TigerText Secure Messenger zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="09b3c-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="09b3c-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do programu Messenger TigerText Secure</span><span class="sxs-lookup"><span data-stu-id="09b3c-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="09b3c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do programu Messenger Secure TigerText (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="09b3c-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="09b3c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="09b3c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="09b3c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="09b3c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09b3c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="09b3c-110">Prerequisites</span></span>

<span data-ttu-id="09b3c-111">Aby skonfigurować integrację usługi Azure AD z TigerText Secure Messenger, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="09b3c-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="09b3c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="09b3c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="09b3c-113">TigerText Secure Messenger logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="09b3c-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09b3c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="09b3c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="09b3c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="09b3c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="09b3c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="09b3c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="09b3c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09b3c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09b3c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="09b3c-118">Scenario description</span></span>
<span data-ttu-id="09b3c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="09b3c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="09b3c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="09b3c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09b3c-121">Dodaj TigerText Secure Messenger z galerii</span><span class="sxs-lookup"><span data-stu-id="09b3c-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="09b3c-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="09b3c-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="09b3c-123">Dodaj TigerText Secure Messenger z galerii</span><span class="sxs-lookup"><span data-stu-id="09b3c-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="09b3c-124">Aby skonfigurować integrację usługi Azure AD TigerText Secure Messenger, należy dodać TigerText Secure Messenger z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="09b3c-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="09b3c-125">**Aby dodać TigerText Secure Messenger z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="09b3c-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="09b3c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="09b3c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="09b3c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="09b3c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="09b3c-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09b3c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="09b3c-133">W polu wyszukiwania wpisz **TigerText Secure Messenger**, wybierz pozycję **TigerText Secure Messenger** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="09b3c-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![Dodaj z galerii](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="09b3c-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="09b3c-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="09b3c-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z TigerText Messenger zabezpieczenia oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="09b3c-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="09b3c-137">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednik w programie Messenger TigerText bezpieczny do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09b3c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="09b3c-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązane użytkownika w programie Messenger TigerText Secure musi określone.</span><span class="sxs-lookup"><span data-stu-id="09b3c-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="09b3c-139">W programie Messenger Secure TigerText, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="09b3c-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="09b3c-140">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z TigerText Secure Messenger, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="09b3c-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="09b3c-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="09b3c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="09b3c-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="09b3c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="09b3c-143">**[Tworzenie użytkownika testowego TigerText Secure Messenger](#create-a-tigertext-secure-messenger-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta TigerText Secure programu Messenger połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09b3c-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="09b3c-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="09b3c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="09b3c-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="09b3c-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="09b3c-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="09b3c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="09b3c-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="09b3c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="09b3c-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z TigerText Secure Messenger, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="09b3c-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="09b3c-149">W portalu Azure na **TigerText Secure Messenger** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="09b3c-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="09b3c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Na podstawie SAML logowania jednokrotnego](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="09b3c-153">Na **TigerText Secure Messenger domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="09b3c-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![Sekcja TigerText Secure Messenger domeny i adresy URL](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="09b3c-155">a.</span><span class="sxs-lookup"><span data-stu-id="09b3c-155">a.</span></span> <span data-ttu-id="09b3c-156">W **adres URL logowania** pole tekstowe, wprowadź adres URL jako:`https://home.tigertext.com`</span><span class="sxs-lookup"><span data-stu-id="09b3c-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="09b3c-157">b.</span><span class="sxs-lookup"><span data-stu-id="09b3c-157">b.</span></span> <span data-ttu-id="09b3c-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="09b3c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="09b3c-159">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="09b3c-159">This value is not real.</span></span> <span data-ttu-id="09b3c-160">Zaktualizuj tę wartość z rzeczywistego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="09b3c-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="09b3c-161">Skontaktuj się z [zespołem pomocy technicznej kliencie Secure TigerText](mailTo:prosupport@tigertext.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="09b3c-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="09b3c-162">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="09b3c-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Sekcja certyfikat podpisywania SAML](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="09b3c-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="09b3c-164">Click **Save** button.</span></span>

    ![Przycisk Zapisz](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="09b3c-166">Aby uzyskać rejestracji jednokrotnej skonfigurowana dla aplikacji, skontaktuj się z [TigerText Secure Messenger zespołem pomocy technicznej](mailTo:prosupport@tigertext.com) i udostępniać je **metadanych pobrane**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="09b3c-167">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="09b3c-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="09b3c-168">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="09b3c-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="09b3c-169">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="09b3c-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="09b3c-170">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="09b3c-170">Create an Azure AD test user</span></span>
<span data-ttu-id="09b3c-171">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="09b3c-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="09b3c-173">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="09b3c-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="09b3c-174">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="09b3c-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="09b3c-176">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Użytkownicy i grupy -> Wszyscy użytkownicy](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="09b3c-178">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09b3c-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Dodawanie przycisku](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="09b3c-180">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="09b3c-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="09b3c-182">a.</span><span class="sxs-lookup"><span data-stu-id="09b3c-182">a.</span></span> <span data-ttu-id="09b3c-183">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="09b3c-184">b.</span><span class="sxs-lookup"><span data-stu-id="09b3c-184">b.</span></span> <span data-ttu-id="09b3c-185">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="09b3c-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="09b3c-186">c.</span><span class="sxs-lookup"><span data-stu-id="09b3c-186">c.</span></span> <span data-ttu-id="09b3c-187">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="09b3c-188">d.</span><span class="sxs-lookup"><span data-stu-id="09b3c-188">d.</span></span> <span data-ttu-id="09b3c-189">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="09b3c-190">Tworzenie użytkownika testowego TigerText zabezpieczenia w programie Messenger</span><span class="sxs-lookup"><span data-stu-id="09b3c-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="09b3c-191">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w TigerText.</span><span class="sxs-lookup"><span data-stu-id="09b3c-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="09b3c-192">Sprawdź dotrzeć do [zespołem pomocy technicznej kliencie Secure TigerText](mailTo:prosupport@tigertext.com) Aby dodać użytkowników do platformy TigerText.</span><span class="sxs-lookup"><span data-stu-id="09b3c-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="09b3c-193">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="09b3c-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="09b3c-194">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do programu Messenger TigerText bezpieczny.</span><span class="sxs-lookup"><span data-stu-id="09b3c-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="09b3c-196">**Aby przypisać Simona Britta TigerText Secure Messenger, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="09b3c-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="09b3c-197">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="09b3c-199">Na liście aplikacji zaznacz **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger listy aplikacji](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="09b3c-201">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="09b3c-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="09b3c-203">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="09b3c-203">Click **Add** button.</span></span> <span data-ttu-id="09b3c-204">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09b3c-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="09b3c-206">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="09b3c-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="09b3c-207">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09b3c-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="09b3c-208">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="09b3c-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="09b3c-209">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="09b3c-209">Test single sign-on</span></span>

<span data-ttu-id="09b3c-210">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="09b3c-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="09b3c-211">Po kliknięciu kafelka TigerText w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji TigerText.</span><span class="sxs-lookup"><span data-stu-id="09b3c-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="09b3c-212">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="09b3c-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09b3c-213">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="09b3c-213">Additional resources</span></span>

* [<span data-ttu-id="09b3c-214">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09b3c-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09b3c-215">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="09b3c-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

