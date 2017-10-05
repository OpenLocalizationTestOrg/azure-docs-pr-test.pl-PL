---
title: 'Samouczek: Integracji Azure Active Directory z Sansan | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Sansan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e1a9653d5feea910308cefabdbdfe3a6af44bbe4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="76b32-103">Samouczek: Integracji Azure Active Directory z Sansan</span><span class="sxs-lookup"><span data-stu-id="76b32-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="76b32-104">Z tego samouczka dowiesz się integrowanie Sansan z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76b32-104">In this tutorial, you learn how to integrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76b32-105">Integracja z usługą Azure AD Sansan zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="76b32-105">Integrating Sansan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="76b32-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Sansan</span><span class="sxs-lookup"><span data-stu-id="76b32-106">You can control in Azure AD who has access to Sansan</span></span>
- <span data-ttu-id="76b32-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Sansan (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="76b32-107">You can enable your users to automatically get signed-on to Sansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76b32-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="76b32-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="76b32-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76b32-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76b32-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="76b32-110">Prerequisites</span></span>

<span data-ttu-id="76b32-111">Aby skonfigurować integrację usługi Azure AD z Sansan, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="76b32-111">To configure Azure AD integration with Sansan, you need the following items:</span></span>

- <span data-ttu-id="76b32-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="76b32-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76b32-113">Sansan logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="76b32-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76b32-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="76b32-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76b32-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="76b32-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76b32-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="76b32-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76b32-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76b32-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76b32-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="76b32-118">Scenario description</span></span>
<span data-ttu-id="76b32-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="76b32-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76b32-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="76b32-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76b32-121">Dodawanie Sansan z galerii</span><span class="sxs-lookup"><span data-stu-id="76b32-121">Adding Sansan from the gallery</span></span>
2. <span data-ttu-id="76b32-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="76b32-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-the-gallery"></a><span data-ttu-id="76b32-123">Dodawanie Sansan z galerii</span><span class="sxs-lookup"><span data-stu-id="76b32-123">Adding Sansan from the gallery</span></span>
<span data-ttu-id="76b32-124">Aby skonfigurować integrację usługi Azure AD Sansan, należy dodać Sansan z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="76b32-124">To configure the integration of Sansan into Azure AD, you need to add Sansan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="76b32-125">**Aby dodać Sansan z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="76b32-125">**To add Sansan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="76b32-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="76b32-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="76b32-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="76b32-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="76b32-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="76b32-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="76b32-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="76b32-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="76b32-133">W polu wyszukiwania wpisz **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="76b32-133">In the search box, type **Sansan**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="76b32-135">W panelu wyników wybierz **Sansan**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="76b32-135">In the results panel, select **Sansan**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76b32-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="76b32-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76b32-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sansan w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="76b32-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76b32-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Sansan jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76b32-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sansan is to a user in Azure AD.</span></span> <span data-ttu-id="76b32-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Sansan musi się.</span><span class="sxs-lookup"><span data-stu-id="76b32-140">In other words, a link relationship between an Azure AD user and the related user in Sansan needs to be established.</span></span>

<span data-ttu-id="76b32-141">W Sansan, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="76b32-141">In Sansan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="76b32-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Sansan, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="76b32-142">To configure and test Azure AD single sign-on with Sansan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="76b32-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="76b32-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="76b32-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="76b32-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76b32-145">**[Tworzenie użytkownika testowego Sansan](#creating-a-sansan-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Sansan połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="76b32-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - to have a counterpart of Britta Simon in Sansan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="76b32-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="76b32-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76b32-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="76b32-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76b32-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="76b32-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="76b32-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Sansan.</span><span class="sxs-lookup"><span data-stu-id="76b32-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="76b32-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Sansan, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="76b32-150">**To configure Azure AD single sign-on with Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="76b32-151">W portalu Azure na **Sansan** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="76b32-151">In the Azure portal, on the **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="76b32-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="76b32-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="76b32-155">Na **Sansan domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="76b32-155">On the **Sansan Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="76b32-157">a.</span><span class="sxs-lookup"><span data-stu-id="76b32-157">a.</span></span> <span data-ttu-id="76b32-158">W **adres URL logowania** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="76b32-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | <span data-ttu-id="76b32-159">Środowisko</span><span class="sxs-lookup"><span data-stu-id="76b32-159">Environment</span></span> | <span data-ttu-id="76b32-160">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="76b32-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="76b32-161">Komputer w sieci web</span><span class="sxs-lookup"><span data-stu-id="76b32-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="76b32-162">Natywnych aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="76b32-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="76b32-163">Ustawienia przeglądarki przenośnych</span><span class="sxs-lookup"><span data-stu-id="76b32-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="76b32-164">b.</span><span class="sxs-lookup"><span data-stu-id="76b32-164">b.</span></span> <span data-ttu-id="76b32-165">W **identyfikator** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="76b32-165">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="76b32-166">Środowisko</span><span class="sxs-lookup"><span data-stu-id="76b32-166">Environment</span></span>             | <span data-ttu-id="76b32-167">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="76b32-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="76b32-168">Komputer w sieci web</span><span class="sxs-lookup"><span data-stu-id="76b32-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="76b32-169">Natywnych aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="76b32-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="76b32-170">Ustawienia przeglądarki przenośnych</span><span class="sxs-lookup"><span data-stu-id="76b32-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="76b32-171">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="76b32-171">These values are not real.</span></span> <span data-ttu-id="76b32-172">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="76b32-172">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="76b32-173">Skontaktuj się z [zespołem pomocy technicznej klienta Sansan](https://www.sansan.com/form/contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="76b32-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) to get these values.</span></span> 

4. <span data-ttu-id="76b32-174">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="76b32-174">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="76b32-176">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="76b32-176">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="76b32-178">Na **konfiguracji Sansan** , kliknij przycisk **skonfigurować Sansan** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="76b32-178">On the **Sansan Configuration** section, click **Configure Sansan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="76b32-179">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="76b32-179">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="76b32-181">Skonfigurować logowanie jednokrotne w **Sansan** stronie, musisz wysłać pobrany **certyfikatu**, **Sign-Out adres URL**, **identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** do [Sansan zespołem pomocy technicznej](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="76b32-181">To configure single sign-on on **Sansan** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="76b32-182">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="76b32-182">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="76b32-183">Ustawienia przeglądarki komputera również działać dla aplikacji mobilnej oraz przeglądarkę dla telefonów wraz z Komputerami w sieci web.</span><span class="sxs-lookup"><span data-stu-id="76b32-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="76b32-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="76b32-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="76b32-185">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="76b32-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="76b32-186">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76b32-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76b32-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="76b32-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="76b32-188">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="76b32-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="76b32-190">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="76b32-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="76b32-191">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="76b32-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="76b32-193">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="76b32-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="76b32-195">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="76b32-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76b32-197">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="76b32-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="76b32-199">a.</span><span class="sxs-lookup"><span data-stu-id="76b32-199">a.</span></span> <span data-ttu-id="76b32-200">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76b32-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76b32-201">b.</span><span class="sxs-lookup"><span data-stu-id="76b32-201">b.</span></span> <span data-ttu-id="76b32-202">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="76b32-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="76b32-203">c.</span><span class="sxs-lookup"><span data-stu-id="76b32-203">c.</span></span> <span data-ttu-id="76b32-204">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="76b32-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="76b32-205">d.</span><span class="sxs-lookup"><span data-stu-id="76b32-205">d.</span></span> <span data-ttu-id="76b32-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="76b32-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="76b32-207">Tworzenie użytkownika testowego Sansan</span><span class="sxs-lookup"><span data-stu-id="76b32-207">Creating a Sansan test user</span></span>

<span data-ttu-id="76b32-208">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w SanSan.</span><span class="sxs-lookup"><span data-stu-id="76b32-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="76b32-209">Aplikacja SanSan musi użytkownika na potrzeby aprowizacji w aplikacji przed wykonaniem logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="76b32-209">SanSan application needs the user to be provisioned in the application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="76b32-210">Jeśli trzeba ręcznie utworzyć użytkownika ani partii użytkowników, należy skontaktować się [zespołem pomocy technicznej Sansan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="76b32-210">If you need to create a user manually or batch of users, you need to contact the [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="76b32-211">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="76b32-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="76b32-212">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Sansan.</span><span class="sxs-lookup"><span data-stu-id="76b32-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sansan.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="76b32-214">**Aby przypisać Simona Britta Sansan, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="76b32-214">**To assign Britta Simon to Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="76b32-215">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="76b32-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="76b32-217">Na liście aplikacji zaznacz **Sansan**.</span><span class="sxs-lookup"><span data-stu-id="76b32-217">In the applications list, select **Sansan**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="76b32-219">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="76b32-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="76b32-221">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="76b32-221">Click **Add** button.</span></span> <span data-ttu-id="76b32-222">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="76b32-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="76b32-224">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="76b32-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="76b32-225">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="76b32-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="76b32-226">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="76b32-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="76b32-227">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="76b32-227">Testing single sign-on</span></span>

<span data-ttu-id="76b32-228">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="76b32-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="76b32-229">Po kliknięciu kafelka Sansan w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Sansan.</span><span class="sxs-lookup"><span data-stu-id="76b32-229">When you click the Sansan tile in the Access Panel, you should get automatically signed-on to your Sansan application.</span></span>
<span data-ttu-id="76b32-230">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76b32-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="76b32-231">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="76b32-231">Additional resources</span></span>

* [<span data-ttu-id="76b32-232">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76b32-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76b32-233">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="76b32-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

