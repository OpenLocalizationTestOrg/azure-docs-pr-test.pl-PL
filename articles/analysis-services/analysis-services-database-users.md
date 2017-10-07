---
title: "aaaManage bazy danych, ról i użytkowników w usłudze Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage bazy danych, ról i użytkowników na serwerze usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>Zarządzanie ról bazy danych i użytkowników

Na poziomie bazy danych modelu hello wszyscy użytkownicy muszą należeć tooa roli. Role definiują użytkowników z uprawnieniami określonego dla hello bazy danych modelu. Dowolnego użytkownika lub grupy zabezpieczeń dodaje tooa roli musi mieć konto w dzierżawie usługi Azure AD w hello tej samej subskrypcji co powitania serwera.

Sposób definiowania ról jest różne w zależności od używanego narzędzia hello, ale wpływ hello jest hello takie same.

Uprawnienia roli obejmują:
*  **Administrator** — użytkownicy mają pełne uprawnienia do hello bazy danych. Role bazy danych z uprawnieniami administratora różnią się od administratorów serwera.
*  **Proces** — użytkownicy mogą nawiązywać połączenie tooand wykonanie procesu na powitania bazy danych i analizowanie danych bazy danych modelu.
*  **Odczyt** — użytkownicy mogą używać klienta aplikacji tooconnect tooand analizowanie danych bazy danych modelu.

Podczas tworzenia projektu modelu tabelarycznego, tworzyć role i Dodawanie ról toothose użytkowników lub grup za pomocą menedżera ról programu SSDT. Wdrożone tooa serwera, korzystając SSMS, [poleceń cmdlet programu PowerShell usługi analizy](https://msdn.microsoft.com/library/hh758425.aspx), lub [język skryptów modelu tabelarycznego](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) lub usuwania ról i członkowie.

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd lub zarządzania rolami i użytkownicy programu SSDT  
  
1.  Programu SSDT > **Eksplorator modelu tabelarycznego**, kliknij prawym przyciskiem myszy **ról**.  
  
2.  W **Menedżerze ról** kliknij przycisk **Nowa**.  
  
3.  Wpisz nazwę roli hello.  
  
     Domyślnie nazwa hello hello domyślnej roli jest przyrostowo numerowane dla każdej nowej roli. Zaleca się, że wpisz nazwę, która jasno identyfikuje typ elementu członkowskiego hello, na przykład menedżerów finansowych lub specjalistami w zasoby ludzkie.  
  
4.  Wybierz jedną z następujących uprawnień hello:  
  
    |Uprawnienie|Opis|  
    |----------------|-----------------|  
    |**Brak**|Elementy członkowskie nie można zmodyfikować schematu modelu hello i nie można wykonać zapytania na danych.|  
    |**Odczyt**|Elementy członkowskie można zbadać danych (w oparciu filtrów wierszy), ale nie można zmodyfikować schematu modelu hello.|  
    |**Odczyt i procesu**|Elementy członkowskie danych (oparte na poziomie wiersza filtry) oraz wykonywania operacji procesu i przetwórz wszystko można zapytania, ale nie można zmodyfikować schematu modelu hello.|  
    |**Proces**|Elementy członkowskie można uruchomić proces i procesu wszystkie operacje. Nie można zmodyfikować schematu modelu hello i nie można wykonać zapytania na danych.|  
    |**Administrator**|Elementy członkowskie można zmodyfikować schematu modelu hello i wyszukiwać wszystkie dane.|   
  
5.  W przypadku roli hello tworzenie ma odczytu lub uprawnienia odczytu i procesu, można dodać filtrów wierszy przy użyciu formuły języka DAX. Kliknij przycisk hello **filtrów wierszy** , a następnie wybierz tabelę, a następnie kliknij hello **filtru DAX** pola, a następnie wpisz formułę języka DAX.
  
6.  Kliknij przycisk **członków** > **Dodaj zewnętrzne**.  
  
8.  W **dodawania zewnętrznego członka**, wprowadź użytkowników lub grup w dzierżawie usługi Azure AD za pomocą adresu e-mail. Po kliknij przycisk OK i zamknąć Menedżera ról, ról i członkowie roli są widoczne w Eksploratorze modelu tabelarycznego. 
 
     ![Role i użytkownicy w Eksploratorze modelu tabelarycznego](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. Wdrażanie tooyour serwera usług Azure Analysis Services.


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd lub zarządzania rolami i użytkowników w programie SSMS
tooadd ról i użytkowników tooa wdrożone bazy danych modelu, musi być toohello podłączonego serwera, administrator serwera lub jest już w roli bazy danych z uprawnieniami administratora.

1. W obiekcie Exporer, kliknij prawym przyciskiem myszy **ról** > **nową rolę**.

2. W **Utwórz rolę**, wprowadź nazwę roli i opis.

3. Wybierz uprawnienia.
   |Uprawnienie|Opis|  
   |----------------|-----------------|  
   |**Pełna kontrola (Administrator)**|Członkowie mogą modyfikować schematu modelu hello, przetwarzania i można zbadać wszystkie dane.| 
   |**Proces bazy danych**|Elementy członkowskie można uruchomić proces i procesu wszystkie operacje. Nie można zmodyfikować schematu modelu hello i nie można wykonać zapytania na danych.|  
   |**Odczyt**|Elementy członkowskie można zbadać danych (w oparciu filtrów wierszy), ale nie można zmodyfikować schematu modelu hello.|  
  
4. Kliknij przycisk **członkostwa**, wprowadź użytkownika lub grupy w dzierżawie usługi Azure AD za pomocą adresu e-mail.

     ![Dodawanie użytkownika](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. Jeśli rola hello, które tworzysz ma uprawnień do odczytu, możesz dodać filtrów wierszy przy użyciu formuły języka DAX. Kliknij przycisk **filtrów wierszy**, wybierz tabelę, a następnie wpisz formułę języka DAX w hello **filtru DAX** pola. 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd ról i użytkowników przy użyciu skryptu TMSL
W oknie XMLA hello w programie SSMS lub przy użyciu programu PowerShell, należy uruchomić skrypt TMSL. Użyj hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) polecenia i hello [ról](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) obiektu.

**Przykładowy skrypt TMSL**

W tym przykładzie użytkownik zewnętrzny B2B i grupy są dodawane rola analityka toohello o uprawnienia do odczytu dla bazy danych SalesBI hello. Zarówno hello użytkownika zewnętrznego i grupy musi być w tej samej dzierżawy usługi Azure AD.

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd ról i użytkowników przy użyciu programu PowerShell
Witaj [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) moduł dostarcza bazy danych specyficznych dla zadań zarządzania poleceń cmdlet i hello ogólnego przeznaczenia Invoke ASCmd polecenia cmdlet, które akceptuje zapytań tabelarycznych modelu skryptów języka (TMSL) lub skryptu. następujące polecenia cmdlet Hello są używane do zarządzania ról bazy danych i użytkowników.
  
|Polecenie cmdlet|Opis|
|------------|-----------------| 
|[Dodaj RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Dodaj element członkowski tooa roli bazy danych.| 
|[Usuń RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Usuwanie członka z roli bazy danych.|   
|[Wywołanie ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Wykonanie skryptu TMSL.|

## <a name="row-filters"></a>Filtrów wierszy  
Filtry wiersza definiują, które wiersze w tabeli mogą być przeszukiwane przez członków określonej roli. Filtrów wierszy są definiowane dla każdej tabeli w modelu przy użyciu formuły języka DAX.  
  
Filtrów wierszy można zdefiniować tylko do odczytu i odczytu ról i uprawnień procesu. Domyślnie jeśli filtr wiersza nie jest zdefiniowany dla danej tabeli, elementy Członkowskie mogą wysyłać zapytania wszystkie wiersze w tabeli hello, chyba że filtrowania krzyżowego stosuje z innej tabeli.
  
 Filtry wiersza wymagają formuły języka DAX, musi ocenić tooa wartość PRAWDA/FAŁSZ, toodefine hello wierszy, które mogą być przeszukiwane przez członków tej konkretnej roli. Nie można zbadać wierszy, które nie są objęte hello formuły języka DAX. Na przykład Witaj tabeli klientów z hello następującego wyrażenia filtrów wiersza, *= klientów [Kraj] = "USA"*, członkowie roli sprzedaży hello może zobaczyć tylko klientów z hello USA.  
  
Stosowane filtry wiersza toohello określone wiersze i powiązane wiersze. Tabela ma wiele relacji, filtry stosowane zabezpieczenia hello relacji, który jest aktywny. Filtrów wierszy są zakończone z innych filtrach wiersza zdefiniowane dla powiązane tabele, na przykład:  
  
|Tabela|Wyrażenie DAX|  
|-----------|--------------------|  
|Region|= Region [Kraj] = "USA"|  
|ProductCategory|= ProductCategory [nazwa] = "Rowerów"|  
|Transakcje|= Transakcje [rok] = 2016|  
  
 Efekt netto Hello jest członków można zbadać wiersze danych, gdzie powitania klienta znajduje się w hello USA, Kategoria produktu hello jest rowerów i rok hello jest 2016. Użytkownicy nie mogą badać transakcji poza hello USA, transakcje, które nie znajdują się nie rowerów lub transakcji w 2016, chyba że są one członkiem innej roli, która udziela te uprawnienia.
  
 Możesz użyć opcji Filtruj hello *=FALSE()*, toodeny dostępu tooall wierszy dla całej tabeli.

## <a name="next-steps"></a>Następne kroki
  [Administratorzy serwerów zarządzania](analysis-services-server-admins.md)   
  [Zarządzanie usług Azure Analysis Services przy użyciu programu PowerShell](analysis-services-powershell.md)  
  [Model tabelaryczny skryptów materiały referencyjne dotyczące języka (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

