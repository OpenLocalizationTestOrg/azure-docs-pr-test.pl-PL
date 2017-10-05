---
title: 'Samouczek: Integracji Azure Active Directory z Citrix GoToMeeting | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="dd48c-103">Samouczek: Integracji Azure Active Directory z Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="dd48c-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="dd48c-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="dd48c-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd48c-105">Integracja z usługą Azure AD Citrix GoToMeeting zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="dd48c-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dd48c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="dd48c-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="dd48c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Citrix GoToMeeting (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd48c-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd48c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="dd48c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dd48c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd48c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd48c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dd48c-110">Prerequisites</span></span>

<span data-ttu-id="dd48c-111">Aby skonfigurować integrację usługi Azure AD z Citrix GoToMeeting, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="dd48c-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="dd48c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd48c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd48c-113">Citrix GoToMeeting jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="dd48c-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd48c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd48c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="dd48c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd48c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="dd48c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd48c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd48c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd48c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="dd48c-118">Scenario description</span></span>
<span data-ttu-id="dd48c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="dd48c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd48c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="dd48c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd48c-121">Dodawanie Citrix GoToMeeting z galerii</span><span class="sxs-lookup"><span data-stu-id="dd48c-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="dd48c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dd48c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="dd48c-123">Dodawanie Citrix GoToMeeting z galerii</span><span class="sxs-lookup"><span data-stu-id="dd48c-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="dd48c-124">Aby skonfigurować integrację usługi Azure AD Citrix GoToMeeting, należy dodać Citrix GoToMeeting z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="dd48c-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dd48c-125">**Aby dodać Citrix GoToMeeting z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dd48c-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dd48c-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dd48c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="dd48c-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dd48c-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="dd48c-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="dd48c-133">W polu wyszukiwania wpisz **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="dd48c-135">W panelu wyników wybierz **Citrix GoToMeeting**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="dd48c-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd48c-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="dd48c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dd48c-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Citrix GoToMeeting oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="dd48c-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dd48c-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Citrix GoToMeeting jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd48c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="dd48c-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="dd48c-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="dd48c-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="dd48c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="dd48c-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Citrix GoToMeeting, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="dd48c-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dd48c-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="dd48c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dd48c-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dd48c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd48c-145">**[Tworzenie użytkownika testowego Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Citrix GoToMeeting, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dd48c-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd48c-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dd48c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd48c-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="dd48c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd48c-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dd48c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd48c-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="dd48c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="dd48c-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Citrix GoToMeeting, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dd48c-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="dd48c-151">W portalu Azure na **Citrix GoToMeeting** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="dd48c-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="dd48c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="dd48c-155">Na **Citrix GoToMeeting domeny i adres URL** sekcji, nie trzeba wykonywać żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="dd48c-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="dd48c-157">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dd48c-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="dd48c-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dd48c-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="dd48c-161">W sekcji konfiguracyjnej SAML GoToMeeting Citrix kliknij przycisk Konfiguruj SAML GoToMeeting Citrix można otworzyć Konfigurowanie logowania jednokrotnego okna.</span><span class="sxs-lookup"><span data-stu-id="dd48c-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="dd48c-162">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="dd48c-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="dd48c-163">W oknie innej przeglądarki, zaloguj się do Twojego [Center organizacji Citrix](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="dd48c-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="dd48c-164">Kliknij przycisk **dostawcy tożsamości** karcie, a następnie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dd48c-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="dd48c-165">![Instalator SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Instalatora SAML")</span><span class="sxs-lookup"><span data-stu-id="dd48c-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="dd48c-166">a.</span><span class="sxs-lookup"><span data-stu-id="dd48c-166">a.</span></span> <span data-ttu-id="dd48c-167">Wybierz **ręczne**</span><span class="sxs-lookup"><span data-stu-id="dd48c-167">Select **Manual**</span></span>

    <span data-ttu-id="dd48c-168">b.</span><span class="sxs-lookup"><span data-stu-id="dd48c-168">b.</span></span> <span data-ttu-id="dd48c-169">W portalu Azure na **skonfigurować logowanie jednokrotne w Citrix GoToMeeting** strony okna dialogowego, kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej ją do **adres URL logowania strony** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="dd48c-170">c.</span><span class="sxs-lookup"><span data-stu-id="dd48c-170">c.</span></span> <span data-ttu-id="dd48c-171">W portalu Azure na **skonfigurować logowanie jednokrotne w Citrix GoToMeeting** strony okna dialogowego, kopiowania **Sign-Out URL** wartość, a następnie wklej ją do **adres URL strony wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="dd48c-172">d.</span><span class="sxs-lookup"><span data-stu-id="dd48c-172">d.</span></span> <span data-ttu-id="dd48c-173">W portalu Azure na **skonfigurować logowanie jednokrotne w Citrix GoToMeeting** strony okna dialogowego, kopiowania **identyfikator jednostki SAML** wartość, a następnie wklej ją do **identyfikator jednostki dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="dd48c-174">e.</span><span class="sxs-lookup"><span data-stu-id="dd48c-174">e.</span></span> <span data-ttu-id="dd48c-175">Aby przekazać certyfikat pobrany, kliknij przycisk **Przekaż certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="dd48c-176">f.</span><span class="sxs-lookup"><span data-stu-id="dd48c-176">f.</span></span> <span data-ttu-id="dd48c-177">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dd48c-178">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="dd48c-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dd48c-179">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="dd48c-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dd48c-180">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd48c-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd48c-181">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd48c-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd48c-182">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dd48c-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="dd48c-184">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dd48c-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dd48c-185">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dd48c-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd48c-187">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd48c-189">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd48c-191">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="dd48c-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd48c-193">a.</span><span class="sxs-lookup"><span data-stu-id="dd48c-193">a.</span></span> <span data-ttu-id="dd48c-194">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd48c-195">b.</span><span class="sxs-lookup"><span data-stu-id="dd48c-195">b.</span></span> <span data-ttu-id="dd48c-196">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd48c-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd48c-197">c.</span><span class="sxs-lookup"><span data-stu-id="dd48c-197">c.</span></span> <span data-ttu-id="dd48c-198">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dd48c-199">d.</span><span class="sxs-lookup"><span data-stu-id="dd48c-199">d.</span></span> <span data-ttu-id="dd48c-200">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="dd48c-201">Tworzenie użytkownika testowego Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="dd48c-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="dd48c-202">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="dd48c-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="dd48c-203">Citrix GoToMeeting obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="dd48c-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="dd48c-204">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="dd48c-204">There is no action item for you in this section.</span></span> <span data-ttu-id="dd48c-205">Jeśli użytkownik nie istnieje w Citrix GoToMeeting, nowy jest tworzony podczas próby uzyskania dostępu Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="dd48c-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="dd48c-206">Jeśli trzeba ręcznie utworzyć użytkownika, skontaktuj się z [Citrix GoToMeeting zespołem pomocy technicznej](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="dd48c-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dd48c-207">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd48c-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dd48c-208">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="dd48c-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="dd48c-210">**Aby przypisać Simona Britta Citrix GoToMeeting, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="dd48c-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="dd48c-211">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="dd48c-213">Na liście aplikacji zaznacz **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="dd48c-215">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dd48c-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="dd48c-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dd48c-217">Click **Add** button.</span></span> <span data-ttu-id="dd48c-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="dd48c-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="dd48c-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dd48c-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd48c-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd48c-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd48c-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dd48c-223">Testing single sign-on</span></span>

<span data-ttu-id="dd48c-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dd48c-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dd48c-225">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="dd48c-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="dd48c-226">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd48c-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd48c-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dd48c-227">Additional resources</span></span>

* [<span data-ttu-id="dd48c-228">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd48c-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd48c-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dd48c-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="dd48c-230">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="dd48c-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

