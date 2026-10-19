# Cvičení

- https://ktiml.mff.cuni.cz/~pilat/cs/evolucni-algoritmy/
- *spojitá optimalizace*
	- prostor řešení je spojitý – tzn. nemusí se nutně jednat o prostor spojitých funkcí
- úkoly
	- nemusíme popisovat do detailu standardní operátory, naopak je dobré napsat hyperparametry
	- závěr může být pár vět, nepsat nic extra dlouhého
	- deadliny nejsou tvrdé, ale je dobré je dodržet
	- když tam bude něco blbě, tak můžeme poslat novou verzi
- můžeme přijít i na jiné cvičení

## OneMAX

- maximalizujeme počet jedniček v binárním jedinci
- ale stejně tak bychom mohli hledat nějaký tajný vzor
- v domácím úkolu budeme hledat alternující jedničky a nuly – budou tam dvě optima
- pseudokód
	- pop ← náhodná populace
	- while not happy
		- off ← $\emptyset$
		- for i in 1 … pop_size / 2
			- $p_1, p_2$ ← selekce(pop, 2)
				- např. ruletová selekce $P_i=\frac{f_i}{\sum_j f_j}$ (dále lze použít turnajovou selekci)
			- $o_1',o_2'$ ← křížení($p_1,p_2$)
				- např. jednobodové křížení (dále lze použít dvojbodové křížení, uniformní křížení)
			- $o_1$ ← mutace($o_1'$)
				- bit flip (typicky chceme pravděpodobnost zvolit tak, abychom v jednom mutovaném jedinci změnili průměrně jeden bit)
			- $o_2$ ← mutace($o_2'$)
			- off ← off $\cup\set{o_1,o_2}$
		- pop ← off
- jak může vypadat fitness u maximalizace střídání nul a jedniček
	- buď porovnáme rozdíl oproti optimu (respektive oběma optimům)
	- nebo spočítáme přechody z nuly na jedničku
	- první varianta je lepší z hlediska mutací, druhá potřebuje křížení
- loupežníci
	- mutace přehodí předmět na jinou hromádku
	- alternativní mutace: vyměníme dva předměty (swap)
		- hint: dají se parametry původní mutace nastavit tak, aby se nám často děly tyhle swapy?
	- jednobodové křížení – pomáhá nám? asi ani ne, ale když ho vypneme, tak to funguje hůř
		- potíž je asi v tom, že „třetí hromádka“ může v každém jedinci znamenat něco jiného
	- chytré (memetic) operátory
		- swap předmětů mezi lehkou a těžkou hromádkou
			- vlastně bychom k tomu nepotřebovali další výpočet fitness (ale nemusíme to takhle optimalizovat v naší implementaci)
		- extrém: operátor kompletně řeší náš problém
		- je to vždycky tradeoff mezi rychlostí operátorů a rychlostí konvergence