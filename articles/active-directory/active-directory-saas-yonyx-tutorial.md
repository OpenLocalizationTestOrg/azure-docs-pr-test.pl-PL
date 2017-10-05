---
title: "Samouczek: Integracji Azure Active Directory z przewodników interaktywnych Yonyx | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i przewodników interaktywnych Yonyx."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: 522f440a0b3746e1101aed845678b3930e030fec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="f68fc-103">Samouczek: Integracji Azure Active Directory z przewodników interaktywnych Yonyx</span><span class="sxs-lookup"><span data-stu-id="f68fc-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>

<span data-ttu-id="f68fc-104">Z tego samouczka dowiesz się integrowanie przewodników interaktywnych Yonyx z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f68fc-104">In this tutorial, you learn how to integrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f68fc-105">Integracja z usługą Azure AD przewodników interaktywnych Yonyx zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f68fc-105">Integrating Yonyx Interactive Guides with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f68fc-106">Można kontrolować w usłudze Azure AD, który ma dostęp do przewodników interaktywnych Yonyx</span><span class="sxs-lookup"><span data-stu-id="f68fc-106">You can control in Azure AD who has access to Yonyx Interactive Guides</span></span>
- <span data-ttu-id="f68fc-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Yonyx prowadnic interakcyjne (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f68fc-107">You can enable your users to automatically get signed-on to Yonyx Interactive Guides (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f68fc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f68fc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f68fc-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f68fc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f68fc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f68fc-110">Prerequisites</span></span>

<span data-ttu-id="f68fc-111">Aby skonfigurować integrację usługi Azure AD z przewodników interaktywnych Yonyx, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f68fc-111">To configure Azure AD integration with Yonyx Interactive Guides, you need the following items:</span></span>

- <span data-ttu-id="f68fc-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f68fc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f68fc-113">Yonyx przewodniki interakcyjne logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f68fc-113">A Yonyx Interactive Guides single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f68fc-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f68fc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f68fc-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f68fc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f68fc-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f68fc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f68fc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f68fc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f68fc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f68fc-118">Scenario description</span></span>
<span data-ttu-id="f68fc-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f68fc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f68fc-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f68fc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f68fc-121">Dodawanie przewodników interaktywnych Yonyx z galerii</span><span class="sxs-lookup"><span data-stu-id="f68fc-121">Adding Yonyx Interactive Guides from the gallery</span></span>
2. <span data-ttu-id="f68fc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f68fc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yonyx-interactive-guides-from-the-gallery"></a><span data-ttu-id="f68fc-123">Dodawanie przewodników interaktywnych Yonyx z galerii</span><span class="sxs-lookup"><span data-stu-id="f68fc-123">Adding Yonyx Interactive Guides from the gallery</span></span>
<span data-ttu-id="f68fc-124">Aby skonfigurować integrację usługi Azure AD Yonyx przewodników interaktywnych, należy dodać przewodników interaktywnych Yonyx z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f68fc-124">To configure the integration of Yonyx Interactive Guides into Azure AD, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f68fc-125">**Aby dodać przewodników interaktywnych Yonyx z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f68fc-125">**To add Yonyx Interactive Guides from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f68fc-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f68fc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="f68fc-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f68fc-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="f68fc-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f68fc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="f68fc-133">W polu wyszukiwania wpisz **przewodników interaktywnych Yonyx**, wybierz pozycję **przewodników interaktywnych Yonyx** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f68fc-133">In the search box, type **Yonyx Interactive Guides**, select  **Yonyx Interactive Guides**  from result panel then click **Add** button to add the application.</span></span>

    ![Przewodniki interakcyjne Yonyx na liście wyników](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f68fc-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f68fc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f68fc-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przewodników interaktywnych Yonyx w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f68fc-136">In this section, you configure and test Azure AD single sign-on with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f68fc-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w przewodnikach interakcyjne Yonyx jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f68fc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Yonyx Interactive Guides is to a user in Azure AD.</span></span> <span data-ttu-id="f68fc-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w przewodnikach interakcyjne Yonyx musi określone.</span><span class="sxs-lookup"><span data-stu-id="f68fc-138">In other words, a link relationship between an Azure AD user and the related user in Yonyx Interactive Guides needs to be established.</span></span>

<span data-ttu-id="f68fc-139">W przewodnikach interakcyjne Yonyx, przypisz wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f68fc-139">In Yonyx Interactive Guides, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f68fc-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przewodników interaktywnych Yonyx, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f68fc-140">To configure and test Azure AD single sign-on with Yonyx Interactive Guides, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f68fc-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f68fc-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f68fc-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f68fc-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f68fc-143">**[Tworzenie użytkownika testowego przewodników interaktywnych Yonyx](#create-a-yonyx-interactive-guides-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Yonyx przewodników interaktywnych połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f68fc-143">**[Create a Yonyx Interactive Guides test user](#create-a-yonyx-interactive-guides-test-user)** - to have a counterpart of Britta Simon in Yonyx Interactive Guides that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f68fc-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f68fc-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f68fc-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f68fc-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f68fc-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f68fc-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f68fc-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Yonyx przewodników interaktywnych.</span><span class="sxs-lookup"><span data-stu-id="f68fc-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="f68fc-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z przewodników interaktywnych Yonyx, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f68fc-148">**To configure Azure AD single sign-on with Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="f68fc-149">W portalu Azure na **przewodników interaktywnych Yonyx** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-149">In the Azure portal, on the **Yonyx Interactive Guides** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="f68fc-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f68fc-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_samlbase.png)

3. <span data-ttu-id="f68fc-153">Na **Yonyx interakcyjne przewodniki domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f68fc-153">On the **Yonyx Interactive Guides Domain and URLs** section, perform the following steps:</span></span>

    ![Yonyx interakcyjne przewodniki domeny i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_url.png)

    <span data-ttu-id="f68fc-155">a.</span><span class="sxs-lookup"><span data-stu-id="f68fc-155">a.</span></span> <span data-ttu-id="f68fc-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span><span class="sxs-lookup"><span data-stu-id="f68fc-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`</span></span>

    <span data-ttu-id="f68fc-157">b.</span><span class="sxs-lookup"><span data-stu-id="f68fc-157">b.</span></span> <span data-ttu-id="f68fc-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.yonyx.com`</span><span class="sxs-lookup"><span data-stu-id="f68fc-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f68fc-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f68fc-159">These values are not real.</span></span> <span data-ttu-id="f68fc-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f68fc-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f68fc-161">Skontaktuj się z [zespołem pomocy technicznej Yonyx interakcyjne przewodników klienta](mailto:support@yonyx.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="f68fc-161">Contact [Yonyx Interactive Guides Client support team](mailto:support@yonyx.com) to get these values.</span></span> 
 
4. <span data-ttu-id="f68fc-162">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f68fc-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_certificate.png) 

5. <span data-ttu-id="f68fc-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f68fc-164">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-yonyx-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f68fc-166">Na **Yonyx interakcyjne przewodniki konfiguracji** , kliknij przycisk **skonfigurować przewodników interaktywnych Yonyx** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f68fc-166">On the **Yonyx Interactive Guides Configuration** section, click **Configure Yonyx Interactive Guides** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f68fc-167">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f68fc-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Yonyx interakcyjne przewodniki konfiguracji](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_configure.png) 

7. <span data-ttu-id="f68fc-169">Skonfigurować logowanie jednokrotne w **przewodników interaktywnych Yonyx** stronie, musisz wysłać pobrany **Certificate(Base64)**, **Sign-Out adres URL**, **pojedynczego SAML Adres URL logowania jednokrotnego usługi** **identyfikator jednostki SAML** do [zespołu obsługi przewodników interaktywnych Yonyx](mailto:support@yonyx.com).</span><span class="sxs-lookup"><span data-stu-id="f68fc-169">To configure single sign-on on **Yonyx Interactive Guides** side, you need to send the downloaded **Certificate(Base64)**, **Sign-Out URL**, **SAML Single Sign-On Service URL** **SAML Entity ID** to [Yonyx Interactive Guides support team](mailto:support@yonyx.com).</span></span> <span data-ttu-id="f68fc-170">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="f68fc-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f68fc-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f68fc-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f68fc-172">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f68fc-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f68fc-173">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f68fc-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f68fc-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f68fc-174">Create an Azure AD test user</span></span>

<span data-ttu-id="f68fc-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f68fc-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

  ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="f68fc-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f68fc-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f68fc-178">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f68fc-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-yonyx-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f68fc-180">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-yonyx-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f68fc-182">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f68fc-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f68fc-184">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f68fc-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f68fc-186">a.</span><span class="sxs-lookup"><span data-stu-id="f68fc-186">a.</span></span> <span data-ttu-id="f68fc-187">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f68fc-188">b.</span><span class="sxs-lookup"><span data-stu-id="f68fc-188">b.</span></span> <span data-ttu-id="f68fc-189">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f68fc-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f68fc-190">c.</span><span class="sxs-lookup"><span data-stu-id="f68fc-190">c.</span></span> <span data-ttu-id="f68fc-191">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f68fc-192">d.</span><span class="sxs-lookup"><span data-stu-id="f68fc-192">d.</span></span> <span data-ttu-id="f68fc-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-193">Click **Create**.</span></span>
 
### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="f68fc-194">Tworzenie użytkownika testowego przewodników interaktywnych Yonyx</span><span class="sxs-lookup"><span data-stu-id="f68fc-194">Create a Yonyx Interactive Guides test user</span></span>

<span data-ttu-id="f68fc-195">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Yonyx przewodników interaktywnych.</span><span class="sxs-lookup"><span data-stu-id="f68fc-195">The objective of this section is to create a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="f68fc-196">Przewodniki interakcyjne Yonyx obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="f68fc-196">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="f68fc-197">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="f68fc-197">There is no action item for you in this section.</span></span> <span data-ttu-id="f68fc-198">Nowy użytkownik został utworzony podczas próby dostępu Yonyx przewodników interaktywnych, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f68fc-198">A new user is created during an attempt to access Yonyx Interactive Guides if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="f68fc-199">Jeśli trzeba ręcznie utworzyć użytkownika, musisz skontaktuj się z zespołem pomocy technicznej przewodników interaktywnych Yonyx za pośrednictwem < mailto:support@yonyx.com >.</span><span class="sxs-lookup"><span data-stu-id="f68fc-199">If you need to create a user manually, you need to contact the Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f68fc-200">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f68fc-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="f68fc-201">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do interaktywnego prowadnic Yonyx.</span><span class="sxs-lookup"><span data-stu-id="f68fc-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yonyx Interactive Guides.</span></span>

![Przypisanie roli użytkownika][200]

<span data-ttu-id="f68fc-203">**Aby przypisać Simona Britta Yonyx przewodników interaktywnych, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f68fc-203">**To assign Britta Simon to Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="f68fc-204">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f68fc-206">Na liście aplikacji zaznacz **przewodników interaktywnych Yonyx**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-206">In the applications list, select **Yonyx Interactive Guides**.</span></span>

    ![Łącze przewodników interaktywnych Yonyx na liście aplikacji](./media/active-directory-saas-yonyx-tutorial/tutorial_yonyxinteractiveguides_app.png) 

3. <span data-ttu-id="f68fc-208">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f68fc-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="f68fc-210">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f68fc-210">Click **Add** button.</span></span> <span data-ttu-id="f68fc-211">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f68fc-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="f68fc-213">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f68fc-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f68fc-214">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f68fc-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f68fc-215">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f68fc-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f68fc-216">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f68fc-216">Test single sign-on</span></span>

<span data-ttu-id="f68fc-217">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f68fc-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f68fc-218">Po kliknięciu kafelka przewodników interaktywnych Yonyx w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji przewodników interaktywnych Yonyx.</span><span class="sxs-lookup"><span data-stu-id="f68fc-218">When you click the Yonyx Interactive Guides tile in the Access Panel, you should get automatically signed-on to your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="f68fc-219">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f68fc-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f68fc-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f68fc-220">Additional resources</span></span>

* [<span data-ttu-id="f68fc-221">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f68fc-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f68fc-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f68fc-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png

