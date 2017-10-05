---
title: 'Samouczek: Integracji Azure Active Directory z Thoughtworks Mingle | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Thoughtworks Mingle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 268ae5affb88a718f68c08daa94fe7aba4a99c11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="eee8b-103">Samouczek: Integracji Azure Active Directory z Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="eee8b-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="eee8b-104">Z tego samouczka dowiesz się integrowanie Thoughtworks Mingle w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eee8b-104">In this tutorial, you learn how to integrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eee8b-105">Integrowanie Thoughtworks Mingle z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="eee8b-105">Integrating Thoughtworks Mingle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="eee8b-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="eee8b-106">You can control in Azure AD who has access to Thoughtworks Mingle</span></span>
- <span data-ttu-id="eee8b-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Thoughtworks Mingle (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee8b-107">You can enable your users to automatically get signed-on to Thoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eee8b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="eee8b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="eee8b-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eee8b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eee8b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eee8b-110">Prerequisites</span></span>

<span data-ttu-id="eee8b-111">Aby skonfigurować integrację usługi Azure AD z Thoughtworks Mingle, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="eee8b-111">To configure Azure AD integration with Thoughtworks Mingle, you need the following items:</span></span>

- <span data-ttu-id="eee8b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eee8b-113">Thoughtworks Mingle logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eee8b-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eee8b-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="eee8b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eee8b-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="eee8b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eee8b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="eee8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eee8b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eee8b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eee8b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="eee8b-118">Scenario description</span></span>
<span data-ttu-id="eee8b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="eee8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eee8b-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="eee8b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eee8b-121">Dodawanie Thoughtworks Mingle z galerii</span><span class="sxs-lookup"><span data-stu-id="eee8b-121">Adding Thoughtworks Mingle from the gallery</span></span>
2. <span data-ttu-id="eee8b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eee8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-the-gallery"></a><span data-ttu-id="eee8b-123">Dodawanie Thoughtworks Mingle z galerii</span><span class="sxs-lookup"><span data-stu-id="eee8b-123">Adding Thoughtworks Mingle from the gallery</span></span>
<span data-ttu-id="eee8b-124">Aby skonfigurować integrację Thoughtworks Mingle do usługi Azure AD, należy dodać Thoughtworks Mingle z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="eee8b-124">To configure the integration of Thoughtworks Mingle into Azure AD, you need to add Thoughtworks Mingle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eee8b-125">**Aby dodać Thoughtworks Mingle z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eee8b-125">**To add Thoughtworks Mingle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eee8b-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eee8b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="eee8b-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="eee8b-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="eee8b-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eee8b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="eee8b-133">W polu wyszukiwania wpisz **Thoughtworks Mingle**, wybierz pozycję **Thoughtworks Mingle** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="eee8b-133">In the search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button to add the application.</span></span>

    ![Thoughtworks Mingle na liście wyników](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="eee8b-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eee8b-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="eee8b-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="eee8b-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eee8b-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Thoughtworks Mingle jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eee8b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Thoughtworks Mingle is to a user in Azure AD.</span></span> <span data-ttu-id="eee8b-138">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Thoughtworks Mingle musi się.</span><span class="sxs-lookup"><span data-stu-id="eee8b-138">In other words, a link relationship between an Azure AD user and the related user in Thoughtworks Mingle needs to be established.</span></span>

<span data-ttu-id="eee8b-139">W Thoughtworks Mingle, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="eee8b-139">In Thoughtworks Mingle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="eee8b-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="eee8b-140">To configure and test Azure AD single sign-on with Thoughtworks Mingle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eee8b-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="eee8b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eee8b-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eee8b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eee8b-143">**[Tworzenie użytkownika testowego Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Thoughtworks Mingle połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="eee8b-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - to have a counterpart of Britta Simon in Thoughtworks Mingle that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="eee8b-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eee8b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eee8b-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="eee8b-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="eee8b-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eee8b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="eee8b-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="eee8b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="eee8b-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Thoughtworks Mingle, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eee8b-148">**To configure Azure AD single sign-on with Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="eee8b-149">W portalu Azure na **Thoughtworks Mingle** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-149">In the Azure portal, on the **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="eee8b-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="eee8b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="eee8b-153">Na **Thoughtworks Mingle domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eee8b-153">On the **Thoughtworks Mingle Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny Mingle Thoughtworks pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="eee8b-155">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="eee8b-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eee8b-156">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="eee8b-156">The value is not real.</span></span> <span data-ttu-id="eee8b-157">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="eee8b-157">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="eee8b-158">Skontaktuj się z [zespołem pomocy technicznej klienta Mingle Thoughtworks](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="eee8b-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) to get the value.</span></span> 
 
4. <span data-ttu-id="eee8b-159">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="eee8b-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="eee8b-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eee8b-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eee8b-163">Zaloguj się do Twojego **Thoughtworks Mingle** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="eee8b-163">Log in to your **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="eee8b-164">Kliknij przycisk **Admin** , a następnie kliknij **konfiguracji logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-164">Click the **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="eee8b-165">![Karta Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="eee8b-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="eee8b-166">W **konfiguracji logowania jednokrotnego** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eee8b-166">In the **SSO Config** section, perform the following steps:</span></span>
   
    <span data-ttu-id="eee8b-167">![Konfiguracja rejestracji Jednokrotnej](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "konfiguracji logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="eee8b-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="eee8b-168">a.</span><span class="sxs-lookup"><span data-stu-id="eee8b-168">a.</span></span> <span data-ttu-id="eee8b-169">Aby przekazać plik metadanych, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-169">To upload the metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="eee8b-170">b.</span><span class="sxs-lookup"><span data-stu-id="eee8b-170">b.</span></span> <span data-ttu-id="eee8b-171">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="eee8b-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="eee8b-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="eee8b-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="eee8b-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="eee8b-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eee8b-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eee8b-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee8b-175">Create an Azure AD test user</span></span>
<span data-ttu-id="eee8b-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eee8b-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="eee8b-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eee8b-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eee8b-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eee8b-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eee8b-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eee8b-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eee8b-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eee8b-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eee8b-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eee8b-187">a.</span><span class="sxs-lookup"><span data-stu-id="eee8b-187">a.</span></span> <span data-ttu-id="eee8b-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eee8b-189">b.</span><span class="sxs-lookup"><span data-stu-id="eee8b-189">b.</span></span> <span data-ttu-id="eee8b-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eee8b-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eee8b-191">c.</span><span class="sxs-lookup"><span data-stu-id="eee8b-191">c.</span></span> <span data-ttu-id="eee8b-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="eee8b-193">d.</span><span class="sxs-lookup"><span data-stu-id="eee8b-193">d.</span></span> <span data-ttu-id="eee8b-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="eee8b-195">Tworzenie użytkownika testowego Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="eee8b-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="eee8b-196">Dla użytkowników usługi Azure AD można było się zalogować muszą mieć przydzielone do Thoughtworks Mingle aplikacji, przy użyciu nazwy użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eee8b-196">For Azure AD users to be able to sign in, they must be provisioned to the Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="eee8b-197">W przypadku Thoughtworks Mingle Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="eee8b-197">In the case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="eee8b-198">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eee8b-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="eee8b-199">Zaloguj się do witryny firmy Thoughtworks Mingle jako administrator.</span><span class="sxs-lookup"><span data-stu-id="eee8b-199">Log in to your Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="eee8b-200">Kliknij przycisk **profilu**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="eee8b-201">![Pierwszy projekt](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "pierwszego projektu")</span><span class="sxs-lookup"><span data-stu-id="eee8b-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="eee8b-202">Kliknij przycisk **Admin** , a następnie kliknij pozycję **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-202">Click the **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="eee8b-203">![Użytkownicy](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="eee8b-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="eee8b-204">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-204">Click **New User**.</span></span>
   
    <span data-ttu-id="eee8b-205">![Nowy użytkownik](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="eee8b-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="eee8b-206">Na **nowego użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eee8b-206">On the **New User** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="eee8b-207">![Okno dialogowe nowego użytkownika](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="eee8b-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="eee8b-208">a.</span><span class="sxs-lookup"><span data-stu-id="eee8b-208">a.</span></span> <span data-ttu-id="eee8b-209">Typ **nazwy logowania**, **Nazwa wyświetlana**, **hasła wybierz**, **Potwierdź hasło** prawidłowy Azure AD konta chcesz udostępnić do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="eee8b-209">Type the **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="eee8b-210">b.</span><span class="sxs-lookup"><span data-stu-id="eee8b-210">b.</span></span> <span data-ttu-id="eee8b-211">Jako **typ użytkownika**, wybierz pozycję **pełnej**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="eee8b-212">c.</span><span class="sxs-lookup"><span data-stu-id="eee8b-212">c.</span></span> <span data-ttu-id="eee8b-213">Kliknij przycisk **utworzyć ten profil**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="eee8b-214">Możesz użyć innych Thoughtworks Mingle użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Thoughtworks Mingle do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="eee8b-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle to provision AAD user accounts.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="eee8b-215">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eee8b-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="eee8b-216">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do Thoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="eee8b-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Thoughtworks Mingle.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="eee8b-218">**Aby przypisać Simona Britta Thoughtworks Mingle, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eee8b-218">**To assign Britta Simon to Thoughtworks Mingle, perform the following steps:**</span></span>

1. <span data-ttu-id="eee8b-219">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="eee8b-221">Na liście aplikacji zaznacz **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-221">In the applications list, select **Thoughtworks Mingle**.</span></span>

    ![Łącze Thoughtworks Mingle na liście aplikacji](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="eee8b-223">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="eee8b-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="eee8b-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eee8b-225">Click **Add** button.</span></span> <span data-ttu-id="eee8b-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eee8b-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="eee8b-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="eee8b-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="eee8b-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eee8b-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eee8b-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eee8b-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="eee8b-231">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eee8b-231">Test single sign-on</span></span>

<span data-ttu-id="eee8b-232">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="eee8b-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="eee8b-233">Po kliknięciu kafelka Thoughtworks Mingle w panelu dostępu użytkownik powinien uzyskać automatycznie zalogowane Thoughtworks Mingle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eee8b-233">When you click the Thoughtworks Mingle tile in the Access Panel, you should get automatically signed-on to your Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eee8b-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="eee8b-234">Additional resources</span></span>

* [<span data-ttu-id="eee8b-235">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eee8b-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eee8b-236">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eee8b-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

