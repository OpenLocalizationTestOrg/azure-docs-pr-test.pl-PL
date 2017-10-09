
Domyślnie interfejsy API w zaplecze aplikacji mobilnej można wywołać anonimowo. Następnie należy toorestrict dostęp uwierzytelniony tooonly klientów.  

* **Ponownie node.js zakończenia (za pośrednictwem portalu Azure hello)** :  

    W ustawieniach aplikacji mobilnej kliknij **łatwe tabele** i wybierz tabelę. Kliknij przycisk **zmienić uprawnienia**, wybierz pozycję **uwierzytelniony dostęp tylko** wszystkie uprawnienia, a następnie kliknij przycisk **zapisać**.
* **.NET zaplecza (C#)**:  

    W projekcie serwera hello Przejdź zbyt**kontrolerów** > **TodoItemController.cs**. Dodaj hello `[Authorize]` atrybutu toohello **TodoItemController** klasy, w następujący sposób. toorestrict tylko toospecific metody dostępu, można także zastosować dla tej metody toothose tylko atrybut zamiast hello klasy. Ponownie opublikować hello na serwerze project Server.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Zaplecza node.js (za pośrednictwem kodu Node.js)** :  

    toorequire uwierzytelniania dostępu do tabeli można dodać powitania po wierszu toohello Node.js server skryptu:

        table.access = 'authenticated';

    Aby uzyskać więcej informacji, zobacz [porady: Wymagaj uwierzytelniania dostępu tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). toolearn toodownload hello szybkiego startu kodu projektu z lokacji, zobacz temat [porady: pobieranie hello Node.js zaplecza projekt szybkiego startu kodu przy użyciu narzędzia Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
