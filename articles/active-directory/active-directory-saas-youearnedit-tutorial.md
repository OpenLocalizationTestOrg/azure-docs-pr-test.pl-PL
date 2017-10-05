---
title: 'Samouczek: Integracji Azure Active Directory z YouEarnedIt | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i YouEarnedIt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: c29d218dbca581f102caf8070fa40894e7006e71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="c6ac8-103">Samouczek: Integracji Azure Active Directory z YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="c6ac8-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="c6ac8-104">Z tego samouczka dowiesz się integrowanie YouEarnedIt z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c6ac8-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c6ac8-105">Integracja z usługą Azure AD YouEarnedIt zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c6ac8-106">Można kontrolować w usłudze Azure AD, który ma dostęp do YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="c6ac8-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do YouEarnedIt (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c6ac8-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c6ac8-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c6ac8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6ac8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6ac8-110">Prerequisites</span></span>

<span data-ttu-id="c6ac8-111">Aby skonfigurować integrację usługi Azure AD z YouEarnedIt, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="c6ac8-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6ac8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c6ac8-113">YouEarnedIt logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="c6ac8-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c6ac8-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c6ac8-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c6ac8-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c6ac8-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6ac8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c6ac8-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c6ac8-118">Scenario description</span></span>
<span data-ttu-id="c6ac8-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c6ac8-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c6ac8-121">Dodawanie YouEarnedIt z galerii</span><span class="sxs-lookup"><span data-stu-id="c6ac8-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="c6ac8-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c6ac8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="c6ac8-123">Dodawanie YouEarnedIt z galerii</span><span class="sxs-lookup"><span data-stu-id="c6ac8-123">Adding YouEarnedIt from the gallery</span></span>
<span data-ttu-id="c6ac8-124">Aby skonfigurować integrację usługi Azure AD YouEarnedIt, należy dodać YouEarnedIt z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c6ac8-125">**Aby dodać YouEarnedIt z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6ac8-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c6ac8-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="c6ac8-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c6ac8-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="c6ac8-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="c6ac8-133">W polu wyszukiwania wpisz **YouEarnedt**, wybierz pozycję **YouEarnedt** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![YouEarnedIt na liście wyników](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c6ac8-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6ac8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c6ac8-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z YouEarnedIt w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c6ac8-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w YouEarnedIt jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="c6ac8-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w YouEarnedIt musi się.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="c6ac8-139">W YouEarnedIt, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c6ac8-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z YouEarnedIt, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c6ac8-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c6ac8-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c6ac8-143">**[Tworzenie użytkownika testowego YouEarnedIt](#create-a-youearnedit-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta YouEarnedIt połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c6ac8-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c6ac8-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c6ac8-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6ac8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c6ac8-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="c6ac8-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z YouEarnedIt, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6ac8-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="c6ac8-149">W portalu Azure na **YouEarnedIt** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="c6ac8-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="c6ac8-153">Na **YouEarnedIt domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny YouEarnedIt pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="c6ac8-155">a.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-155">a.</span></span> <span data-ttu-id="c6ac8-156">W **adres URL logowania** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="c6ac8-157">Środowisko</span><span class="sxs-lookup"><span data-stu-id="c6ac8-157">Environment</span></span>  | <span data-ttu-id="c6ac8-158">wzorzec</span><span class="sxs-lookup"><span data-stu-id="c6ac8-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="c6ac8-159">Produkcji</span><span class="sxs-lookup"><span data-stu-id="c6ac8-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="c6ac8-160">Piaskownica</span><span class="sxs-lookup"><span data-stu-id="c6ac8-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="c6ac8-161">b.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-161">b.</span></span> <span data-ttu-id="c6ac8-162">W **identyfikator** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="c6ac8-163">Środowisko</span><span class="sxs-lookup"><span data-stu-id="c6ac8-163">Environment</span></span>  | <span data-ttu-id="c6ac8-164">wzorzec</span><span class="sxs-lookup"><span data-stu-id="c6ac8-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="c6ac8-165">Produkcji</span><span class="sxs-lookup"><span data-stu-id="c6ac8-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="c6ac8-166">Piaskownica</span><span class="sxs-lookup"><span data-stu-id="c6ac8-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="c6ac8-167">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-167">These values are not real.</span></span> <span data-ttu-id="c6ac8-168">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c6ac8-169">Skontaktuj się z [zespołem pomocy technicznej klienta YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) to get these values.</span></span> 
 
4. <span data-ttu-id="c6ac8-170">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="c6ac8-172">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-172">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c6ac8-174">Na **konfiguracji YouEarnedIt** , kliknij przycisk **skonfigurować YouEarnedIt** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c6ac8-175">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="c6ac8-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfiguracja YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="c6ac8-177">Aby skonfigurować logowanie jednokrotne w **YouEarnedIt** stronie, musisz wysłać pobrany **Certificate(Base64)** i **SAML pojedynczy znak na adres URL usługi** do [ Zespołem pomocy technicznej YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="c6ac8-177">To configure single sign-on on **YouEarnedIt** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="c6ac8-178">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c6ac8-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="c6ac8-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c6ac8-180">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c6ac8-181">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c6ac8-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c6ac8-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6ac8-182">Create an Azure AD test user</span></span>

<span data-ttu-id="c6ac8-183">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="c6ac8-185">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6ac8-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c6ac8-186">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c6ac8-188">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c6ac8-190">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c6ac8-192">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c6ac8-192">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c6ac8-194">a.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-194">a.</span></span> <span data-ttu-id="c6ac8-195">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c6ac8-196">b.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-196">b.</span></span> <span data-ttu-id="c6ac8-197">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c6ac8-198">c.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-198">c.</span></span> <span data-ttu-id="c6ac8-199">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c6ac8-200">d.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-200">d.</span></span> <span data-ttu-id="c6ac8-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="c6ac8-202">Tworzenie użytkownika testowego YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="c6ac8-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="c6ac8-203">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="c6ac8-204">Należy współpracować z zespołem pomocy technicznej YouEarnedIt Aby dodać użytkowników do platformy YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="c6ac8-205">YouEarnedIt oczekiwać dostawcy tożsamości, umożliwiają określanie wartości w atrybucie NameID EmailAddress lub nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="c6ac8-206">Uwierzytelnianie nie powiedzie się, jeśli odpowiednie nazwy użytkownika i EmailAddress nie został znaleziony w bazie danych lub nie jest dokładnie zgodny.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="c6ac8-207">Będzie to wymagało, że konta będzie importowana do systemu YouEarnedIt przed włączeniem rejestracji Jednokrotnej (zazwyczaj albo za pośrednictwem interfejsu API lub CSV import).</span><span class="sxs-lookup"><span data-stu-id="c6ac8-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c6ac8-208">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c6ac8-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="c6ac8-209">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="c6ac8-211">**Aby przypisać Simona Britta YouEarnedIt, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="c6ac8-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="c6ac8-212">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="c6ac8-214">Na liście aplikacji zaznacz **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-214">In the applications list, select **YouEarnedIt**.</span></span>

    ![Łącze YouEarnedIt na liście aplikacji](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="c6ac8-216">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="c6ac8-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-218">Click **Add** button.</span></span> <span data-ttu-id="c6ac8-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="c6ac8-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c6ac8-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c6ac8-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c6ac8-224">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c6ac8-224">Test single sign-on</span></span>

<span data-ttu-id="c6ac8-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c6ac8-226">Po kliknięciu kafelka YouEarnedIt w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="c6ac8-226">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="c6ac8-227">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c6ac8-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c6ac8-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c6ac8-228">Additional resources</span></span>

* [<span data-ttu-id="c6ac8-229">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6ac8-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c6ac8-230">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6ac8-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

