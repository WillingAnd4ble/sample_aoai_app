## Bandymas paleisti lokaliai

1.  Iš pradžių klonavau repozitorija lokaliai pas save per git bash.

„ git clone <https://github.com/microsoft/sample-app-aoai-chatGPT.git>"

![A screenshot of a computer AI-generated content may be
incorrect.](media/image1.png){width="6.5in"
height="1.4256944444444444in"}

2.  Sukūriau Azure paskyrą.

![A screenshot of a computer AI-generated content may be
incorrect.](media/image2.png){width="6.5in"
height="3.1958333333333333in"}

3.  ![](/media/image3.png){width="6.5in"
    height="1.4777777777777779in"}![](media/image4.png){width="5.375in"
    height="2.814699256342957in"}Atsisiunčiau AZ CLI

4.  ![](media/image5.png){width="3.0395833333333333in"
    height="2.35625in"}AOAI setupas.

> ![](media/image6.png){width="6.34375in"
> height="0.6770833333333334in"}Regioną palikau, kaip East US, kad
> išvengti busimų nesutapimų, nes:

5.  ![](media/image7.png){width="6.5in"
    height="1.6513888888888888in"}![](vertopal_a4781dea2cb340dfa4bdb2f8b155a40e/media/image8.png){width="6.5in"
    height="2.2444444444444445in"}Lokalios aplinkos tvarkymas

6.  ![](media/image9.png){width="6.075in"
    height="3.2291666666666665in"}Paleidęs aplikaciją susiduriau su 500
    server error

Greitai pastbėjau klaidą, kad įterpiau endpointą .env faile į
„AZURE_OPENAI_RESOURCE="

7.  ![](media/image10.png){width="6.052083333333333in"
    height="0.4756944444444444in"}![](vertopal_a4781dea2cb340dfa4bdb2f8b155a40e/media/image11.png){width="6.64375in"
    height="3.439583333333333in"}Sekanti klaidą susijusi taip pat dėl
    blogo įterpimo

> ![](media/image12.png){width="2.6666666666666665in"
> height="2.7375in"}Problema iškilo dėl „AZURE_OPENAI_MODEL=". Iš
> nežinojimo nebuvau sukūręs modelio Azure Ai foundry. Darant
> deploymenta ten susiduriau su kvotų apribojimų visose regionose
> visiems modeliams sample-aoai-app scopui, todėl turėjau paprašyti
> kvotų butent šiam scopui.

![](media/image13.png){width="6.604166666666667in"
height="3.6590277777777778in"}Po kvotų suteikimo, viskas veikė puikiai.

## Deploymentas naudojant AZ CLI

1.  Konfigūravimas

![](media/image14.png){width="8.22944116360455in"
height="0.3349803149606299in"}

Root direktorijoje surašiau tokią eilutę, iš repo: „az webapp up
\--runtime PYTHON:3.11 \--sku B1 \--name \<new-app-name\>
\--resource-group \<resource-group-name\> \--location \<azure-region\>
\--subscription \<subscription-name\>" su --track-status False, dėl
\"2.73.0\" azure-cli versijos, ir pabandžiau išjungti AUTH_ENABLED.

Turėjau keletą nereikšmingų klaidų, kurios greitai sprendžiamos, vienas
iš pavyzdžių tai:

![](media/image15.png){width="6.5in"
height="0.3486111111111111in"}

![](media/image16.png){width="4.986111111111111in"
height="3.910416666666667in"}2. Problema "the subscription is not
registered to use namespace 'Microsoft.Web'.

Išsprendžiau „az provider register --namespace Microsoft.Web" eilute.

3\. Paleidimas

![A screenshot of a computer AI-generated content may be
incorrect.](media/image17.png){width="6.5in"
height="2.1180555555555554in"}

3\. Startup komandos nustatymas.![A screenshot of a computer
AI-generated content may be
incorrect.](media/image18.png){width="6.5in"
height="3.222916666666667in"}

4\. SCM išjungimas![A black rectangular object with white lines
AI-generated content may be
incorrect.](media/image19.png){width="6.5in"
height="1.761111111111111in"}

![](vertopal_a4781dea2cb340dfa4bdb2f8b155a40e/media/image20.png){width="6.5in"
height="0.8708333333333333in"}5. Perkelimas .env į JSON formatą

![](media/image21.png){width="6.5in"
height="1.25625in"}6. .env įkelimas

7.Aplikacijos atnaujinimas

![](media/image22.png){width="6.5in"
height="0.6034722222222222in"}![](vertopal_a4781dea2cb340dfa4bdb2f8b155a40e/media/image23.png){width="6.415277777777778in"
height="1.2326388888888888in"}Darant šį žingsnį susiduriau su tokia
klaida:

![](media/image24.png){width="6.5in"
height="4.085416666666666in"}Nesigilinau stipriai į šią problemą, nes
pabandžiau greitai pakeisti internetą iš Wi-fi į mobilųjį, nes tuo metu
kai kuriau konfiguraciją naudojau telefono ryšį, tad buvo įtarimas, kad
problema susijusi su tuo ir tai suveikė.

8.  ![](media/image25.png){width="4.742361111111111in"
    height="1.6145833333333333in"}Start-up file'o nustatymas

9.  ![](media/image26.png){width="4.311805555555556in"
    height="2.2805555555555554in"}Aplikacijos patikrinimas

Kuriant konfigūraciją buvau nustatęs, autentifikavimo argumentą, bet
kažkodėl tai nesuveikė.

10. ![](media/image27.png){width="6.5in"
    height="0.9270833333333334in"}AUTH_ENABLE atnaujinimas

![](media/image28.png){width="6.5in"
height="0.21319444444444444in"}

11. ![](media/image29.png){width="6.419444444444444in"
    height="3.5430555555555556in"}Aplikacijos patikrinimas

![](media/image30.png){width="6.788194444444445in"
height="3.334722222222222in"}

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
