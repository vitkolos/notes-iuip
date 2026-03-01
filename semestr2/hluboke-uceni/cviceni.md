# Cvičení

- `reshape([inputs.shape[0], -1])`
	- `-1` je wild card, PyTorch použije velikost dat
- je zvykem, že se obrázky ukládají jako pole bytů a pak se převádějí na floaty až během tréninku (?)
- nepoužívat pythoní seznam jako seznam vrstev – PyTorch je nenajde při hledání parametrů