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