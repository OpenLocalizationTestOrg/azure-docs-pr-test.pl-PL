
* Konwersja Hello wymaga ponownego uruchomienia hello maszyny Wirtualnej, więc zaplanować hello migracji maszyn wirtualnych w istniejącym oknie obsługi. 

* Konwersja Hello jest nieodwracalne. 

* Należy się tootest hello konwersji. Przeprowadź migrację testowej maszyny wirtualnej, przed przeprowadzeniem migracji hello w środowisku produkcyjnym.

* Podczas konwersji hello cofnięcie przydziału hello maszyny Wirtualnej. Hello wirtualna odbiera nowego adresu IP po uruchomieniu po konwersji hello. W razie potrzeby można [Przypisz statyczny adres IP](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello maszyny Wirtualnej.

* Witaj oryginalnego wirtualne dyski twarde i konto magazynu hello używane przez hello maszyny Wirtualnej przed konwersją nie są usuwane. Nadal tooincur opłat. tooavoid są rozliczane tych artefaktów usunąć obiekty BLOB dysków VHD oryginalnego hello po zweryfikowaniu o ukończeniu konwersji hello.
