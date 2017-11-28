---
title: 'Samouczek: Integracji Azure Active Directory z Dropbox dla firm | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i skrzynki dla firm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a56a5af171eaca259db29f25fee4331a77313420
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="78607-103">Samouczek: Integracji Azure Active Directory z Dropbox dla firm</span><span class="sxs-lookup"><span data-stu-id="78607-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="78607-104">Z tego samouczka dowiesz się integrowanie skrzynki dla firm z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78607-104">In this tutorial, you learn how to integrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78607-105">Integrowanie usługi Dropbox dla firm z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="78607-105">Integrating Dropbox for Business with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78607-106">Można kontrolować w usłudze Azure AD, który ma dostęp do skrzynki dla firm</span><span class="sxs-lookup"><span data-stu-id="78607-106">You can control in Azure AD who has access to Dropbox for Business</span></span>
- <span data-ttu-id="78607-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do skrzynki dla firm (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="78607-107">You can enable your users to automatically get signed-on to Dropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78607-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="78607-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78607-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78607-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78607-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="78607-110">Prerequisites</span></span>

<span data-ttu-id="78607-111">Aby skonfigurować integrację usługi Azure AD z Dropbox dla firm, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="78607-111">To configure Azure AD integration with Dropbox for Business, you need the following items:</span></span>

- <span data-ttu-id="78607-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="78607-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78607-113">Dropbox dla firm logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="78607-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78607-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="78607-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78607-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="78607-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78607-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="78607-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78607-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78607-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78607-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="78607-118">Scenario description</span></span>
<span data-ttu-id="78607-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="78607-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78607-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="78607-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78607-121">Dodawanie skrzynki dla firm z galerii</span><span class="sxs-lookup"><span data-stu-id="78607-121">Adding Dropbox for Business from the gallery</span></span>
2. <span data-ttu-id="78607-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="78607-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-the-gallery"></a><span data-ttu-id="78607-123">Dodawanie skrzynki dla firm z galerii</span><span class="sxs-lookup"><span data-stu-id="78607-123">Adding Dropbox for Business from the gallery</span></span>
<span data-ttu-id="78607-124">Aby skonfigurować integrację usługi Dropbox dla firm z usługą Azure AD, należy dodać skrzynki dla firm z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="78607-124">To configure the integration of Dropbox for Business into Azure AD, you need to add Dropbox for Business from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78607-125">**Aby dodać skrzynki dla firm z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="78607-125">**To add Dropbox for Business from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78607-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="78607-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="78607-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="78607-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78607-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="78607-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="78607-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78607-131">Click **New application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="78607-133">W polu wyszukiwania wpisz **Dropbox dla firm**.</span><span class="sxs-lookup"><span data-stu-id="78607-133">In the search box, type **Dropbox for Business**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="78607-135">W panelu wyników wybierz **Dropbox dla firm**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="78607-135">In the results panel, select **Dropbox for Business**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78607-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="78607-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78607-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="78607-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="78607-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Dropbox dla firm jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78607-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dropbox for Business is to a user in Azure AD.</span></span> <span data-ttu-id="78607-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="78607-140">In other words, a link relationship between an Azure AD user and the related user in Dropbox for Business needs to be established.</span></span>

<span data-ttu-id="78607-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="78607-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="78607-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="78607-142">To configure and test Azure AD single sign-on with Dropbox for Business, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78607-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="78607-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78607-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="78607-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78607-145">**[Tworzenie skrzynki dla użytkownika testowego firm](#creating-a-dropbox-for-business-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Dropbox dla firm, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="78607-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - to have a counterpart of Britta Simon in Dropbox for Business that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78607-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="78607-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78607-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="78607-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78607-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="78607-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78607-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w usłudze Dropbox dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="78607-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="78607-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Dropbox dla firm, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="78607-150">**To configure Azure AD single sign-on with Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="78607-151">W portalu Azure na **Dropbox dla firm** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="78607-151">In the Azure portal, on the **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="78607-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="78607-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="78607-155">Na **Dropbox domeny biznesowych i adresów URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="78607-155">On the **Dropbox for Business Domain and URLs** section, perform the following steps:</span></span>

    <span data-ttu-id="78607-156">a.</span><span class="sxs-lookup"><span data-stu-id="78607-156">a.</span></span> <span data-ttu-id="78607-157">Zaloguj się do Twojej skrzynki dla firm dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="78607-157">Sign on to your Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="78607-158">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="78607-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="78607-159">b.</span><span class="sxs-lookup"><span data-stu-id="78607-159">b.</span></span> <span data-ttu-id="78607-160">W okienku nawigacji po lewej stronie kliknij **konsoli administracyjnej**.</span><span class="sxs-lookup"><span data-stu-id="78607-160">In the navigation pane on the left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="78607-161">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="78607-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="78607-162">c.</span><span class="sxs-lookup"><span data-stu-id="78607-162">c.</span></span> <span data-ttu-id="78607-163">Na **konsoli administracyjnej**, kliknij przycisk **uwierzytelniania** w lewym okienku nawigacji.</span><span class="sxs-lookup"><span data-stu-id="78607-163">On the **Admin Console**, click **Authentication** in the left navigation pane.</span></span> 
   
    <span data-ttu-id="78607-164">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="78607-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="78607-165">d.</span><span class="sxs-lookup"><span data-stu-id="78607-165">d.</span></span> <span data-ttu-id="78607-166">W **logowanie jednokrotne** zaznacz **Włącz rejestrację jednokrotną**, a następnie kliknij przycisk **więcej** do Rozwiń tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="78607-166">In the **Single sign-on** section, select **Enable single sign-on**, and then click **More** to expand this section.</span></span>  
   
    <span data-ttu-id="78607-167">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="78607-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="78607-168">e.</span><span class="sxs-lookup"><span data-stu-id="78607-168">e.</span></span> <span data-ttu-id="78607-169">Skopiuj adres URL w polu **użytkownicy mogą rejestrować wprowadź swój adres e-mail lub można przejść bezpośrednio do**.</span><span class="sxs-lookup"><span data-stu-id="78607-169">Copy the URL next to **Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="78607-171">f.</span><span class="sxs-lookup"><span data-stu-id="78607-171">f.</span></span> <span data-ttu-id="78607-172">W portalu Azure w **adres URL logowania** pole tekstowe, wklej adres URL.</span><span class="sxs-lookup"><span data-stu-id="78607-172">On the Azure portal, in the **Sign-on URL** textbox, paste the URL.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="78607-174">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="78607-174">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78607-175">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="78607-175">This value is not real value.</span></span> <span data-ttu-id="78607-176">Zaktualizuj wartość rzeczywista URL logowania jednokrotnego uzyskać z jednej sekcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="78607-176">Update the value with the actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="78607-177">Skontaktuj się z [Dropbox dla zespołu pomocy technicznej klienta Business](https://www.dropbox.com/business/contact) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="78607-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="78607-178">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="78607-178">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="78607-180">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="78607-180">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78607-182">Na **Dropbox konfiguracji Business** , kliknij przycisk **Konfigurowanie skrzynki dla firm** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="78607-182">On the **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** to open **Configure sign-on** window.</span></span> <span data-ttu-id="78607-183">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="78607-183">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="78607-185">Skonfigurować logowanie jednokrotne w **Dropbox dla firm** po stronie znajduje się w usłudze Dropbox dla dzierżawy biznesowych w **logowanie jednokrotne** sekcji **uwierzytelniania** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="78607-185">To configure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in the **Single sign-on** section of the **Authentication** page, perform the following steps:</span></span> 
   
    <span data-ttu-id="78607-186">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="78607-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="78607-187">a.</span><span class="sxs-lookup"><span data-stu-id="78607-187">a.</span></span> <span data-ttu-id="78607-188">Kliknij przycisk **wymagane**.</span><span class="sxs-lookup"><span data-stu-id="78607-188">Click **Required**.</span></span>
   
    <span data-ttu-id="78607-189">b.</span><span class="sxs-lookup"><span data-stu-id="78607-189">b.</span></span> <span data-ttu-id="78607-190">W portalu Azure na **Konfigurowanie logowania jednokrotnego** okna, kopiowania **SAML pojedynczy znak na adres URL usługi** wartość, a następnie wklej ją do **adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="78607-190">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="78607-191">c.</span><span class="sxs-lookup"><span data-stu-id="78607-191">c.</span></span> <span data-ttu-id="78607-192">Kliknij przycisk **wybierz certyfikat**, a następnie przejdź do Twojej **pliku zakodowanego certyfikatu Base64**.</span><span class="sxs-lookup"><span data-stu-id="78607-192">Click **Choose certificate**, and then browse to your **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="78607-193">d.</span><span class="sxs-lookup"><span data-stu-id="78607-193">d.</span></span> <span data-ttu-id="78607-194">Kliknij przycisk **zapisać zmiany** w celu ukończenia konfiguracji w usłudze DropBox dla dzierżawy biznesowych.</span><span class="sxs-lookup"><span data-stu-id="78607-194">Click **Save changes** to complete the configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="78607-195">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="78607-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78607-196">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="78607-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78607-197">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78607-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78607-198">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="78607-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="78607-199">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="78607-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="78607-201">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="78607-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78607-202">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="78607-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="78607-204">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="78607-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78607-206">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78607-206">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78607-208">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="78607-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78607-210">a.</span><span class="sxs-lookup"><span data-stu-id="78607-210">a.</span></span> <span data-ttu-id="78607-211">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78607-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78607-212">b.</span><span class="sxs-lookup"><span data-stu-id="78607-212">b.</span></span> <span data-ttu-id="78607-213">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="78607-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78607-214">c.</span><span class="sxs-lookup"><span data-stu-id="78607-214">c.</span></span> <span data-ttu-id="78607-215">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="78607-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78607-216">d.</span><span class="sxs-lookup"><span data-stu-id="78607-216">d.</span></span> <span data-ttu-id="78607-217">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="78607-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="78607-218">Tworzenie skrzynki dla firm użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="78607-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="78607-219">W tej sekcji użytkownika o nazwie Simona Britta jest tworzony w Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="78607-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="78607-220">Dropbox dla firm obsługę w czasie, który jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="78607-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="78607-221">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="78607-221">There is no action item for you in this section.</span></span> <span data-ttu-id="78607-222">Jeśli użytkownik nie istnieje w Dropbox dla firm, nowy jest tworzony podczas próby dostępu Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="78607-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt to access Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="78607-223">Jeśli trzeba ręcznie utworzyć użytkownika, skontaktuj się z [Dropbox dla zespołu pomocy technicznej klienta biznesowa](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="78607-223">If you need to create a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78607-224">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="78607-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78607-225">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do usługi Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="78607-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dropbox for Business.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="78607-227">**Aby przypisać Simona Britta Dropbox dla firm, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="78607-227">**To assign Britta Simon to Dropbox for Business, perform the following steps:**</span></span>

1. <span data-ttu-id="78607-228">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="78607-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="78607-230">Na liście aplikacji zaznacz **Dropbox dla firm**.</span><span class="sxs-lookup"><span data-stu-id="78607-230">In the applications list, select **Dropbox for Business**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="78607-232">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="78607-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="78607-234">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="78607-234">Click **Add** button.</span></span> <span data-ttu-id="78607-235">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78607-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="78607-237">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="78607-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78607-238">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78607-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78607-239">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="78607-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78607-240">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="78607-240">Testing single sign-on</span></span>

<span data-ttu-id="78607-241">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="78607-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="78607-242">Po kliknięciu skrzynki dla firm kafelka w panelu dostępu, należy pobrać strony logowania o usłudze Dropbox dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="78607-242">When you click the Dropbox for Business tile in the Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78607-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="78607-243">Additional resources</span></span>

* [<span data-ttu-id="78607-244">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78607-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78607-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78607-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="78607-246">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="78607-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

