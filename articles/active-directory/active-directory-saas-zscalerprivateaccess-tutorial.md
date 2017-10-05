---
title: "Samouczek: Integracji Azure Active Directory z Zscaler prywatny dostęp (ZPA) | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Zscaler prywatny dostęp (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 5c598bfa5b6725d21a89df54dbcb3314cc631d80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="a5fd3-103">Samouczek: Integracji Azure Active Directory z Zscaler prywatny dostęp (ZPA)</span><span class="sxs-lookup"><span data-stu-id="a5fd3-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="a5fd3-104">Z tego samouczka dowiesz się integrowanie Zscaler prywatny dostęp (ZPA) z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5fd3-105">Integrowanie Zscaler prywatny dostęp (ZPA) z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a5fd3-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5fd3-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Zscaler prywatny dostęp (ZPA)</span><span class="sxs-lookup"><span data-stu-id="a5fd3-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="a5fd3-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Zscaler prywatny dostęp (ZPA) (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5fd3-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5fd3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="a5fd3-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="a5fd3-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5fd3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a5fd3-110">Prerequisites</span></span>

<span data-ttu-id="a5fd3-111">Aby skonfigurować integrację usługi Azure AD z Zscaler prywatny dostęp (ZPA), potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a5fd3-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span></span>

- <span data-ttu-id="a5fd3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5fd3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5fd3-113">Zscaler prywatny dostęp (ZPA) jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a5fd3-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="a5fd3-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="a5fd3-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a5fd3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5fd3-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a5fd3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="a5fd3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a5fd3-118">Scenario description</span></span>
<span data-ttu-id="a5fd3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5fd3-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a5fd3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5fd3-121">Dodawanie Zscaler prywatny dostęp (ZPA) z galerii</span><span class="sxs-lookup"><span data-stu-id="a5fd3-121">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
2. <span data-ttu-id="a5fd3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a5fd3-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-the-gallery"></a><span data-ttu-id="a5fd3-123">Dodawanie Zscaler prywatny dostęp (ZPA) z galerii</span><span class="sxs-lookup"><span data-stu-id="a5fd3-123">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
<span data-ttu-id="a5fd3-124">Aby skonfigurować integrację z Zscaler prywatny dostęp (ZPA) do usługi Azure AD, należy dodać Zscaler prywatny dostęp (ZPA) z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5fd3-125">**Aby dodać Zscaler prywatny dostęp (ZPA) z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a5fd3-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5fd3-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a5fd3-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5fd3-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a5fd3-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a5fd3-133">W polu wyszukiwania wpisz **Zscaler prywatny dostęp (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-133">In the search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="a5fd3-135">W panelu wyników wybierz **Zscaler prywatny dostęp (ZPA)**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5fd3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a5fd3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a5fd3-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zscaler prywatny dostęp (ZPA) w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a5fd3-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Zscaler prywatny dostęp (ZPA) jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span></span> <span data-ttu-id="a5fd3-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span></span>

<span data-ttu-id="a5fd3-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="a5fd3-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Zscaler prywatny dostęp (ZPA), należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a5fd3-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5fd3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a5fd3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a5fd3-145">**[Tworzenie użytkownika testowego Zscaler prywatny dostęp (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  — aby mieć odpowiednikiem Simona Britta w Zscaler prywatny dostęp (ZPA) połączonej z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a5fd3-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a5fd3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5fd3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a5fd3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5fd3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="a5fd3-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Zscaler prywatny dostęp (ZPA), wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a5fd3-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="a5fd3-151">W portalu zarządzania Azure na **Zscaler prywatny dostęp (ZPA)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a5fd3-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="a5fd3-155">Na **domeny Zscaler prywatny dostęp (ZPA) i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5fd3-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="a5fd3-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-157">a.</span></span> <span data-ttu-id="a5fd3-158">W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="a5fd3-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="a5fd3-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-159">b.</span></span> <span data-ttu-id="a5fd3-160">W **identyfikator** tekstowym, wpisz:`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="a5fd3-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a5fd3-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-161">Please note that these are not the real values.</span></span> <span data-ttu-id="a5fd3-162">Należy zaktualizować te wartości przy użyciu rzeczywistego logowania na adres URL i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="a5fd3-163">W tym miejscu zalecamy użycia w identyfikatorze unikatową wartość adresu URL.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-163">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="a5fd3-164">Skontaktuj się z [zespołem pomocy technicznej Zscaler prywatny dostęp (ZPA)](https://help.zscaler.com/zpa-submit-ticket) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>

4. <span data-ttu-id="a5fd3-165">Na **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="a5fd3-167">Na **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="a5fd3-168">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-168">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="a5fd3-170">Na **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="a5fd3-172">W oknie podręcznym **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="a5fd3-174">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="a5fd3-176">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Zscaler prywatny dostęp (ZPA) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="a5fd3-177">Przejdź do **administratora** , a następnie kliknij przycisk **konfiguracji Idp**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-177">Navigate to **Administrator** and then click **Idp Configuration**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="a5fd3-179">W **konfiguracji Idp** kliknij **dodać nową konfigurację IDP**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="a5fd3-181">W **nowej konfiguracji IDP** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5fd3-181">In the **New IDP Configuration** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="a5fd3-183">a.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-183">a.</span></span> <span data-ttu-id="a5fd3-184">Kliknij przycisk **wybierz plik** i przesłać plik pobrany metadanych.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="a5fd3-185">b.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-185">b.</span></span> <span data-ttu-id="a5fd3-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5fd3-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5fd3-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5fd3-188">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a5fd3-190">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a5fd3-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5fd3-191">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a5fd3-193">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a5fd3-195">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a5fd3-197">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a5fd3-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5fd3-199">a.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-199">a.</span></span> <span data-ttu-id="a5fd3-200">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5fd3-201">b.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-201">b.</span></span> <span data-ttu-id="a5fd3-202">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5fd3-203">c.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-203">c.</span></span> <span data-ttu-id="a5fd3-204">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5fd3-205">d.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-205">d.</span></span> <span data-ttu-id="a5fd3-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="a5fd3-207">Tworzenie użytkownika testowego Zscaler prywatny dostęp (ZPA)</span><span class="sxs-lookup"><span data-stu-id="a5fd3-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="a5fd3-208">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="a5fd3-209">We współpracy z [zespołem pomocy technicznej Zscaler prywatny dostęp (ZPA)](https://help.zscaler.com/zpa-submit-ticket) Aby dodać użytkowników do platformy Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a5fd3-210">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a5fd3-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a5fd3-211">W tej sekcji można włączyć Simona Britta do używania usługi Azure logowania jednokrotnego za udostępnienie jej do Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a5fd3-213">**Aby przypisać Simona Britta do Zscaler prywatny dostęp (ZPA), wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a5fd3-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="a5fd3-214">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a5fd3-216">Na liście aplikacji zaznacz **Zscaler prywatny dostęp (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="a5fd3-218">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a5fd3-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-220">Click **Add** button.</span></span> <span data-ttu-id="a5fd3-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a5fd3-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a5fd3-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a5fd3-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="a5fd3-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a5fd3-226">Testing single sign-on</span></span>

<span data-ttu-id="a5fd3-227">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a5fd3-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5fd3-228">Po kliknięciu kafelka Zscaler prywatny dostęp (ZPA) w panelu dostępu użytkownik powinien uzyskać automatycznie zalogowane do aplikacji Zscaler prywatny dostęp (ZPA).</span><span class="sxs-lookup"><span data-stu-id="a5fd3-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a5fd3-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a5fd3-229">Additional resources</span></span>

* [<span data-ttu-id="a5fd3-230">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5fd3-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a5fd3-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5fd3-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png