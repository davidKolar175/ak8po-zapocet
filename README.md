## Scénář
V naší firmě máme Model First přístup ke tvorbě aplikací. To znamená, že analytici napřed systém navrhnou pomocí UML diagamů. Každá naše aplikace (interně nazýváme projekt, této terminilogie se budeme dále držet) se může skládat z několika takzvaných modelů. Model je izolovaným logicko/funkčním celkem. Máme například model pro tvoru grafiky, model s finanční logikou, model pro sklady, atd.

Každý tento model je designován pomocí nástroje Select Architect, který slouží k tvorbě UML diagramů. Jakmile analytik model namodeluje, provede jeho export, který vtvoří tzv. XMI export. To je xml soubor, který obsahuje informace o třídách, metodách, atributech, use casech a dalších entitách UML. Tyto soubory se ukládají do speciálního síťového úložiště. V rámci firmy nyní vzniká nutnost mít informace o těchto exportech v jednotné formě, která je dostatečně rychlá pro použití ve webových aplikacích (například když někdo potřebuje znát seznam všech tříd, které jsou v modelech, které vznikly za posledních 24 hodin).

Na základě této nutnosti jsem se tedy rozhodl vytvořit na pozadí běžící službu, která bude 24/7 kontrolovat obsah síťového úložiště s XMI exporty, při změně nějakého souboru načte jeho obsah a transformuje jej do sql databáze.


## Požadavky
* Kontrolovat složky s XMI exporty uml modelů.
* Při změně nějakého XMI exportu načíst jeho soubor, vyčíst z něj seznam UML tříd, atributů, asociací,... a tyto entity nahrát do databáze.
* Udržovat stav složek 1:1 s databází.
* Mít možnost konfigurovat, jaké složky se mají kontrolovat.
* Problémy se synchronizací vypisovat do EventVieweru systému.

## Technologie
* ASP.NET Core 6
* C#
* MSSQL

## Časový plán
* 4 hodiny - studium ASP.NET Core 6, instalace služeb na systém, provozvání služeb
* 8 hodin - parser XML souborů
* 2 hodiny - namodelování databáze
* 16 hodin - programování samotné služby
* 6 - programování unit testů
* 4 hodiny - testování

## Otázky
* Co se bude dít v době neaktivnosti služby?
* Jak se služna uvede do provozu?
* Jak poznáme, co je XMI Export?
* Jaká bude frekvence změn XMI Exportů?
* Může složka s Exporty obsahovat i jiné soubory? Jiné složky?
