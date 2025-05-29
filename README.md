## Bandymas paleisti lokaliai

1.  Iš pradžių klonavau repozitorija lokaliai pas save per git bash.

„ git clone <https://github.com/microsoft/sample-app-aoai-chatGPT.git>"

![](media/image1.png)

2.  Sukūriau Azure paskyrą.

![](media/image2.png)

3. Atsisiunčiau AZ CLI 
![](/media/image3.png)
![](media/image4.png)

4.  AOAI setupas.
![](media/image5.png)
Regioną palikau, kaip East US, kad
išvengti busimų nesutapimų, nes:
![](media/image6.png)

5.  Lokalios aplinkos tvarkymas
![](media/image8.png)
![](media/image7.png)
6.  Paleidęs aplikaciją susiduriau su 500 server error
![](media/image9.png)

Greitai pastebėjau klaidą, kad įterpiau endpointą .env faile į
„AZURE_OPENAI_RESOURCE="

7.  Sekanti klaidą susijusi taip pat dėl blogo įterpimo
![](media/image11.png)
![](media/image10.png)
> Problema iškilo dėl „AZURE_OPENAI_MODEL=". Iš
> nežinojimo nebuvau sukūręs modelio Azure Ai foundry. Darant
> deploymenta ten susiduriau su kvotų apribojimų visose regionose
> visiems modeliams sample-aoai-app scopui, todėl turėjau paprašyti
> kvotų butent šiam scopui.
![](media/image12.png)

Po kvotų suteikimo, viskas veikė puikiai.
![](media/image13.png)
## Deploymentas naudojant AZ CLI

1.  Konfigūravimas

![](media/image14.png)

Root direktorijoje surašiau tokią eilutę, iš repo: „az webapp up
\--runtime PYTHON:3.11 \--sku B1 \--name \<new-app-name\>
\--resource-group \<resource-group-name\> \--location \<azure-region\>
\--subscription \<subscription-name\>" su --track-status False, dėl
\"2.73.0\" azure-cli versijos, ir pabandžiau išjungti AUTH_ENABLED.

Turėjau keletą nereikšmingų klaidų, kurios greitai sprendžiamos, vienas
iš pavyzdžių tai:

![](media/image15.png)

![](media/image16.png)
2. Problema "the subscription is not
registered to use namespace 'Microsoft.Web'.

Išsprendžiau „az provider register --namespace Microsoft.Web" eilute.

3\. Paleidimas
![](media/image17.png)

3\. Startup komandos nustatymas.
![](media/image18.png)

4\. SCM išjungimas
![](media/image19.png)


5. Perkelimas .env į JSON formatą
![](media/image20.png)
6. .env įkelimas
![](media/image21.png)
7.Aplikacijos atnaujinimas
![](media/image23.png)
Darant šį žingsnį susiduriau su tokia klaida:
![](media/image22.png)
Nesigilinau stipriai į šią problemą, nes
pabandžiau greitai pakeisti internetą iš Wi-fi į mobilųjį, nes tuo metu
kai kuriau konfiguraciją naudojau telefono ryšį, tad buvo įtarimas, kad
problema susijusi su tuo ir tai suveikė.
![](media/image24.png)
8.  Start-up file'o nustatymas
![](media/image25.png)
9.  Aplikacijos patikrinimas
![](media/image26.png)
Kuriant konfigūraciją buvau nustatęs, autentifikavimo argumentą, bet
kažkodėl tai nesuveikė.

10. AUTH_ENABLE atnaujinimas 
![](media/image27.png)
![](media/image28.png)

11. Aplikacijos patikrinimas
![](media/image29.png)
![](media/image30.png)

## Apibendrinamas:

Iš pradžių pabandžiau paleisti aplikaciją lokaliai, kur didžiausia
problema buvo kvotų apribojimas ir nežinojimas, kad reikia dar sukurti
AI foundry deploymentą.

Darant deploymenta su Azure CLI, nesusiduriau su didesniomis
problemomis, nes dokumentacija yra labai aiški. Greičiausiai problema
7-tame punkte yra susijusi su tinklu nustatymu, bet neatsirado poreikio
gilintis toliau, nes greitai išsprendžiau šią problemą pakeitus tinklą,
kuriame dariau konfigūraciją.

Aplikaciją galima patikrinti -
https://sample-aoai-webapp.azurewebsites.net
